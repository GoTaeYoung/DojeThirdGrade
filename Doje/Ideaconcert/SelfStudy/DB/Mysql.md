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

* ## 클러스터 인덱스(Cluster Index) [&#128209;](http://mee2ro.tistory.com/2)

  * ### 정의 : 테이블 마다 한개만 가질 수 있고, 지정한 열의 행이 자동 정렬 된다

  * ### 임의의 열에 PRIMARY KEY 를 지정하면 해당 열에 클러스터 인덱스가 생성된다

  * ### 강제로 PRIMARY KEY 를 비클러스터 인덱스로 선언 할 수 있다

  * ### 많은 데이터가 있는 테이블에 클러스터 인덱스를 지정하면, 데이터가 바뀔 때마다 자동 정렬을 실행하기에 많은 리소스를 차지하게 된다