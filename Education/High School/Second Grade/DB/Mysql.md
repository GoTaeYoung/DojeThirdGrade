# Mysql의 특징

* ## Mysql 구조 [&#128209;](http://asuraiv.blogspot.com/2017/07/mysql-storage-engine.html)
  * ### 서버 엔진 : 사용자가 쿼리를 요청 할 때, 쿼리 파싱과 스토리지 엔진에 데이터를 요청하는 업무를 담당한다

  * ### 스토리지 엔진 : 서버 엔진이 필요한 데이터를 물리적 저장 장치에서 가져오는 역할을 담당한다
    * #### 스토리지 엔진의 종류
    	* ##### InnoDB [&#128209;](http://www.mysqlkorea.com/gnuboard4/bbs/board.php?bo_table=community_03&wr_id=1702) : 트랜잭션을 지원하며, 일반적인 서비스에 가장 많이 사용되는 엔진이다. '다중 버전 동시성 제어 메커니즘' 을 제공하고 행 단위의 잠금으로 데이터 변경 작업을 수행한다. 메모리에 인덱스와 데이터가 적재되어있기 때문에 메모리 버퍼 크기가 DB 성능에 큰 영향을 미친다.

  * ### 처리방식 : 기본적인 스토리지 엔진은 단일 코어로 데이터를 처리한다(병렬 처리 X). 따라서, CPU 코어 갯수를 늘리는 Sacle-Out 보다, 단위 처리량이 좋은 CPU로 Scale-Up 하는 것이 더 효율적이다 [&#128209;](http://gywn.net/2011/12/mysql-three-features/)

  * ### BNL(Block Nested Loop) [&#128209;](http://blog.naver.com/PostView.nhn?blogId=parkjy76&logNo=221069454499&categoryNo=14&parentCategoryNo=0&viewDate=&currentPage=1&postListTopCurrentPage=1&from=postView)

    * #### 정의 : 프로세스 내의 조인 버퍼에 Driving 테이블의 레코드를 저장한 후, 다른 테이블을 스캔하면서 조인 버퍼를 탐색하는 방식이다.

  * ### 쿼리 성능 진단

    * #### 쿼리 실행 계획 [&#128209;](http://multifrontgarden.tistory.com/149)

        ~~~mysql
        EXPLAIN
        SELECT 2*3 FROM DUAL;
        ~~~

* ## WHERE 조건 이해

  * ### 묵시적 형변환

    * #### 정의 : 조건절의 데이터 타입이 서로 다를 때, 우선순위가 높은 쪽으로 형 변환이 내부에서 되는 것을 말한다

    * #### 예제 : 문자열과 정수값을 비교하면, 우선순위가 낮은 문자열은 자동으로 정수 타입으로 형변환 처리 된다

        ```mysql
        create table test(
        inti int unsigned not null auto_increment,
        intj int unsigned not null,
        str varchar(64) not null,
        d datetime not null,
        primary key(inti)
        );
        
        alter table test add key(intj), add key(str), add key(d);
        
        insert into test(intj, str, d)
        values(
        crc32(rand()),
        crc32(rand() * 12345),
        date_add(now(), interval -crc32(rand())/5 second)
        );
        
        INSERT INTO test(intj, str, d)
        SELECT
        crc32(rand()),
        crc32(rand()) * 12345,
        date_add(now(), interval -crc32(rand())/5 second)
        FROM test;
        ```

        * ##### intj를 문자열로 검색했을 때

            ```mysql
            explain
            select * from test
            where intj = '2839990793';
            ```

            * ###### 실행결과 : 성공

            	* id, select_type, table, partitions, type, possible_keys, key, key_len, ref, rows, filtered, Extra

            	* '1', 'SIMPLE', 'test', NULL, 'ref', 'intj', 'intj', '4', 'const', '1', '100.00', NULL

            * ###### 이유 : 묵시적 형변환으로 인해서 문자열이 정수형으로 변환됐기 때문

        * ##### intj를 정수형으로 검색했을 때

          ```mysql
          explain
          select * from test
          where intj = 2839990793;
          ```

          * ###### 실행결과 : 성공

          	* id, select_type, table, partitions, type, possible_keys, key, key_len, ref, rows, filtered, Extra

          	* '1', 'SIMPLE', 'test', NULL, 'ref', 'intj', 'intj', '4', 'const', '1', '100.00', NULL

          * ###### 이유 : 컬럼 타입이 조건문과 일치했기 때문

        * ##### str을 정수형으로 검색했을 때

          ```mysql
          explain
          select * from test
          where str = 46829860833270;
          ```

          * ###### 실행결과 : 성공

          	* id, select_type, table, partitions, type, possible_keys, key, key_len, ref, rows, filtered, Extra

          	* '1', 'SIMPLE', 'test', NULL, 'ALL', 'str', NULL, NULL, NULL, '131594', '10.00', 'Using where'

          * ###### 이유 : 묵시적 형변환으로 인해 문자열이 정수형으로 변환되어 검색된다
          	* 하지만 인덱스가 있어도 묵시적 형변환으로 인해 모든 행을 조회하기 때문에 수행속도가 느려진다

        * ##### str을 문자열로 검색했을 때

          ```mysql
          explain
          select * from test
          where str = '46829860833270';
          ```

          * ###### 실행결과 : 성공

             * id, select_type, table, partitions, type, possible_keys, key, key_len, ref, rows, filtered, Extra

             * '1', 'SIMPLE', 'test', NULL, 'ref', 'str', 'str', '194', 'const', '1', '100.00', NULL

          * ###### 이유 : 컬럼 타입이 조건문과 일치했기 때문


- ## JOIN 이해하기
- ### 생성문
  ~~~mysql
  create table tab1(
  tab1Pk int not null auto_increment primary key,
  intJ int unsigned not null,
  regdate datetime not null
  );
  
  create table tab2(
  tab2Pk int not null auto_increment primary key,
  tab1Pk integer, 
  intJ int unsigned not null,
  regdate datetime not null
  );
  
  create table tab3(
  tab3Pk int not null auto_increment primary key,
  tab2Pk integer, 
  intJ int unsigned not null,
  regdate datetime not null
  );
  
  create table tab4(
  tab4Pk int not null auto_increment primary key,
  tab3Pk integer, 
  intJ int unsigned not null,
  regdate datetime not null
  );
  
  create table tab5(
  tab5Pk int not null auto_increment primary key,
  tab4Pk integer, 
  intJ int unsigned not null,
  regdate datetime not null
  );
  ~~~


- ### 삽입문
  ~~~mysql
  insert into tab1(intJ, regdate)
  values(
  	crc32(rand()),
      date_add(now(), interval -crc32(rand())/5 second)
  );
  
  insert into tab1(intJ, regdate)
  	SELECT crc32(rand())
  	,date_add(now(), interval -crc32(rand())/5 second)
  from tab1;
  
  insert into tab2(tab1pk, intj, regdate)
  	select tab1pk, crc32(rand()),
      date_add(now(), interval -crc32(rand())/5 second)
  from tab1;
  
  insert into tab3(tab2pk, intj, regdate)
  	select tab2pk, crc32(rand()),
      date_add(now(), interval -crc32(rand())/5 second)
  from tab2;
  
  insert into tab4(tab3pk, intj, regdate)
  	select tab3pk, crc32(rand()),
      date_add(now(), interval -crc32(rand())/5 second)
  from tab3;
  
  insert into tab5(tab4pk, intj, regdate)
  	select tab4pk, crc32(rand()),
      date_add(now(), interval -crc32(rand())/5 second)
  from tab4;
  ~~~


- ### 실행문
  ~~~mysql
  explain
  select tab1.*, tab4.*
  from tab1 tab1
  	INNER JOIN tab2 tab2 on tab2.tab1pk = tab1.tab1pk
      INNER JOIN tab3 tab3 on tab3.tab2pk = tab2.tab2pk
      LEFT JOIN tab4 tab4 on tab4.tab3pk = tab3.tab3pk
  where (tab1.intj%10) in (1,2)
  		and (tab2.intj%10) not in (9)
  order by tab3.regdate, tab2.regdate desc;
  
  # 개선코드 1
  explain
  select tab1.*
  from tab1 tab1
  	INNER JOIN tab2 tab2 on tab2.tab1pk = tab1.tab1pk
      INNER JOIN tab3 tab3 on tab3.tab2pk = tab2.tab2pk
      LEFT JOIN tab4 tab4 on tab4.tab3pk = tab3.tab3pk
  where (tab1.intj%10) in (1,2)
  		and (tab2.intj%10) not in (9)
  order by tab3.regdate, tab2.regdate desc
  limit 0,20;

  # 개선코드 2
  explain
  select sub1.*
  from(
  select tab1.tab1Pk as tab1pk, tab3.tab3Pk as tab3pk
  from tab1 tab1
  inner join tab2 tab2 on tab2.tab1pk = tab1.tab1Pk
  inner join tab3 tab3 on tab3.tab2pk = tab2.tab2pk
  where (tab1.intj%10) in (1,2)
  and (tab2.intj%10) not in (9)
  order by tab3.regdate, tab2.regdate desc
  limit 0,20
  ) sub1
  inner join tab1 tab1 on tab1.tab1Pk = sub1.tab1Pk
  left join tab4 tab4 on tab4.tab3Pk = sub1.tab3pk;
  ~~~


- ### 예제
  ~~~mysql
  # 생성문
  create table code(
  pk integer auto_increment primary key,
  name varchar(50),
  regdate datetime
  );
  
  # 삽입문
  insert into code(name, regdate)
  values('1', now());
  insert into code(name, regdate)
  select crc32(rand())*123,
  date_add(now(), interval -crc32(rand())/5 second)
  from code;
  
  # 생성문
  create table item(
  pk integer auto_increment primary key,
  name varchar(50),
  codePk integer,
  regdate datetime
  );
    
  # 삽입문
  insert into item(name, codePk, regdate)
  select crc32(rand())*123, pk, date_add(now(), interval -			crc32(rand())/5 second)
  from code;
  
  #실행문
  explain
  select item.name itemName, code.Name as codeName
  from item item inner join code code on item.codePk = code.pk
  where item.codepk = code.pk and
  item.name ='452637069033';

  # 개선코드
  explain
  select sub.*
  from(
  select *
  from item
  WHERE ASD
  order by regdate desc
  limit 0,10
  ) sub
  inner join code code on code.pk = sub.codepk
  where sub.name = '452637069033';
  ~~~


* ## 클러스터 인덱스(Cluster Index) [&#128209;](http://mee2ro.tistory.com/2)

  * ### 정의 : 테이블 마다 한개만 가질 수 있고, 지정한 열의 행이 자동 정렬 된다

  * ### 임의의 열에 PRIMARY KEY 를 지정하면 해당 열에 클러스터 인덱스가 생성된다

  * ### 강제로 PRIMARY KEY 를 비클러스터 인덱스로 선언 할 수 있다

  * ### 많은 데이터가 있는 테이블에 클러스터 인덱스를 지정하면, 데이터가 바뀔 때마다 자동 정렬을 실행하기에 많은 리소스를 차지하게 된다