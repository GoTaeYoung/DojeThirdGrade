# DA 가이드
- ## 데이터 표준화
  - ### 데이터 표준화 개요
    - #### 데이터 표준화 필요성  [:bookmark_tabs:](http://www.dbguide.net/db.db?cmd=view&boardUid=12731&boardConfigUid=9&categoryUid=216&boardIdx=30&boardStep=1)<br/>명칭의 통일로 인한 명확한 의사소통의 증대, 필요한 데이터를 찾는 시간과 노력 감소, 데이터 품질 향상
    - #### 데이터 표준화 개념  [:bookmark_tabs:](http://www.dbguide.net/db.db?cmd=view&boardUid=12803&boardConfigUid=9&categoryUid=216&boardIdx=30&boardStep=1)<br/>데이터 정보 요소에 대한 원칙을 수립하고 이를 전사적으로 적용하여<br/>데이터의 정확한 의미를 파악하고 데이터에 대한 상반된 시각을 조정<br/>![](http://www.dbguide.net/publishing/img/dbguide/edu/070103_edu_01.gif)<br/>![](http://www.dbguide.net/publishing/img/dbguide/edu/070103_edu_02.gif)
    - #### 데이터 표준화  관리 도구 [:bookmark_tabs:](http://www.dbguide.net/db.db?cmd=view&boardUid=12809&boardConfigUid=9&categoryUid=216&boardIdx=30&boardStep=1)<br/>보통의 데이터 표준관리 시스템은 데이터 표준 관리, 데이터 구조 관리, 프로세스 관리의 기능으로 구성됨<br/>시스템 도입시에는 시스템의 확장성, 유연성, 편의성 관점에서 충분한 검토를 하고 고려해야 함.<br/>![](http://www.dbguide.net/publishing/img/dbguide/edu/070110_edu_01.gif)

  - ### 데이터 표준 수립
    - #### 데이터 표준화 원칙 정의 [:bookmark_tabs:](http://www.dbguide.net/db.db?cmd=view&boardUid=12866&boardConfigUid=9&boardIdx=44&boardStep=1)<br/>현행 데이터 표준의 개선 방안을 토대로 향후에 적용할 전사 데이터 표준<br/>기본 원칙을 정의하고 향후 전사 데이터 표준의 생성 및 변경시 참고하도록 각 데이터<br/>표준 대상별 데이터 표준 원칙을 작성하여 문서화한다.<br/>![](http://www.dbguide.net/publishing/img/dbguide/edu/070124_edu_04.gif)
    - #### 데이터 표준 정의  [:bookmark_tabs:](http://www.dbguide.net/db.db?cmd=view&boardUid=12867&boardConfigUid=9&categoryUid=216&boardIdx=44&boardStep=1)<br/>표준 용어 사전, 표준 단어 사전, 표준 도메인 사전, 표준 용어 사전을 정의한다.
    - #### 데이터 표준 확정  [:bookmark_tabs:](http://www.dbguide.net/db.db?cmd=view&boardUid=12868&boardConfigUid=9&categoryUid=216&boardIdx=44&boardStep=1)<br/>데이터 표준의 유일성, 완전성, 정확성, 범용성을 검토하고 승인을 결정한다.

  - ### 데이터 표준 관리
    - #### 데이터 표준 관리 [:bookmark_tabs:](http://www.dbguide.net/db.db?cmd=view&boardUid=12870&boardConfigUid=9&categoryUid=216&boardIdx=45&boardStep=1)<br/>개별적인 데이터 표준화 요소의 표준화 작업 이후, 데이터 표준 정의 단계에서 수립된<br/>데이터 표준에 근거하여 관리 프로세스를 정립하고 데이터 표준이 관리되게 한다.
    - #### 데이터 표준 관리 프로세스 [:bookmark_tabs:](http://www.dbguide.net/db.db?cmd=view&boardUid=12871&boardConfigUid=9&categoryUid=216&boardIdx=45&boardStep=1)<br/>전사적 차원의 일관된 데이터 형식 및 규칙의 적용으로 데이터 품질의 향상<br/>데이터 표준의 관리 프로세스를 정의함으로써 데이터 표준을 지속적으로 유지 가능.<br/>![](http://www.dbguide.net/publishing/img/dbguide/edu/070307_edu_01.gif)

-----

- ## 데이터 모델링
  - ### 데이터 모델링 이해
    - #### 데이터 모델링 개요 [:bookmark_tabs:](http://www.dbguide.net/db.db?cmd=view&boardUid=12733&boardConfigUid=9&categoryUid=216&boardIdx=31&boardStep=1)<br/>기업 업무에서 발생하는 데이터의 데이터베이스화 하기 위해 이루어지는 과정의 하나<br/>데이터의 업무 규칙에 대하여 참 또는 거짓을 판단할 사실을 어떻게, 누가 접근하는지<br/>이에 대한 전산화와는 별개의 관점에서 이를 명확하게 표현하는 추상화 기법<br/>업무를 파악하여 문제를 찾고 개선 사항을 도출하며, 미래에 적합한 설계를<br/>이끌기 위해 인간이 해야 할 대부분의 결정들을 내리는 단계 모두 포함하는 것.<br/>![](http://www.dbguide.net/publishing/img/dbguide/edu/070321_gu_2.gif)
    - #### 데이터 모델링 기법 이해 [:bookmark_tabs:](http://www.dbguide.net/db.db?cmd=view&boardUid=12843&boardConfigUid=9&categoryUid=216&boardIdx=31&boardStep=1)<br/>설계 단계에서 조기에 오류를 찾고 정정되도록 원활한 의사소통이 필요하다<br/> 이러한 목적을 달성하려는 것에 데이터 모델은 최적의 수단으로 활용될 수 있음<br/>개체 - 관계 모델 기법 : 단순성을 지님, 현재 개념/논리 데이터 모델링에서 가장 일반적으로 사용

    - #### 데이터 모델링 표기법 이해 [:bookmark_tabs:](http://www.dbguide.net/db.db?cmd=view&boardUid=12845&boardConfigUid=9&categoryUid=216&boardIdx=31&boardStep=1)<br/>영국 컨설팅 회사 CACI에 의해 처음 개발되고 리차드 바커( Richard Barker )에 의해<br/>지속적인 업그레이드를 받은 바커 표기법을 사용한다.

  - ### 개념 데이터 모델링
    - #### 개념 데이터 모델링 이해 [:bookmark_tabs:](http://www.dbguide.net/db.db?cmd=view&boardUid=12847&boardConfigUid=9&boardIdx=40&boardStep=1)<br/>대상을 핵심 Entity로 한정지은 논리적 모델링과 같다<br/>아무리 상세한 모델링이 진행돼도 전체적인 골격은 개념적 모델을 벗어나지 않는다.
    - #### 주제 영역 정의 [:bookmark_tabs:](http://www.dbguide.net/db.db?cmd=view&boardUid=12848&boardConfigUid=9&categoryUid=216&boardIdx=40&boardStep=1)<br/>데이터의 최상위 집합. 하나의 주제 영역 속 데이터간의 관계는 밀접하다<br/>서로 다른 주제 영역의 데이터 간 상호작용은 최소화 되게 정의. 주제 영역은<br/>계층적 표현이 가능. 주제 영역을 쪼개면 하위 수준의 주제 영역이나 Entity가 생김.<br/>![](http://www.dbguide.net/publishing/img/dbguide/edu/da0502_02_01.gif)
    - #### 후보 Entity 선정 [:bookmark_tabs:](http://www.dbguide.net/db.db?cmd=view&boardUid=12849&boardConfigUid=9&categoryUid=216&boardIdx=40&boardStep=1)<br/>Entity를 선정하기 위해 Entity 후보를 수집함. 다양한 경로를 통해 수집하는게 바람직.<br/>Entity 후보 중 우선적용 대상을 분류 후, 그 데이터를 영역별로 분류한다.
    - #### 핵심 Entity 정의 [:bookmark_tabs:](http://www.dbguide.net/db.db?cmd=view&boardUid=12850&boardConfigUid=9&categoryUid=216&boardIdx=40&boardStep=1)<br/>업무 활동 중에 지속적인 관심을 가져야 하는 대상의 데이터를 저장 가능하고<br/>대상들 간의 동질성을 지닌 개체 또는 행위의 집합. Entity를 정의할 때는 어떤 대상이<br/>그 Entity에 속하는지 않는지를 명확히 정의할수 있어야 함.
    - #### 관계( Relationship ) 정의 [:bookmark_tabs:](http://www.dbguide.net/db.db?cmd=view&boardUid=12851&boardConfigUid=9&categoryUid=216&boardIdx=40&boardStep=1)<br/>Entity 와 Entity 사이의 관계. 관리하려는 업무 영역 내의 특정한 두 개의 Entity 사이에<br/>존재하는 많은 관계 중 특별히 관리하려는 직접적인 관계( 업무적 연관성 )<br/>![](http://www.dbguide.net/publishing/img/dbguide/edu/070523_1.gif)
    - #### 개념 데이터 모델 작성 [:bookmark_tabs:](http://www.dbguide.net/db.db?cmd=view&boardUid=173629&boardConfigUid=9&categoryUid=216&boardIdx=40&boardStep=1)<br/>핵심 Entity( Key Entity, Main Entity )와 핵심 Entity 사이의 관계 도출을 통해<br/>핵심 구조라 할 수 있는 데이터 모델의 골격을 정의한 것이다<br/>개괄 데이터 모델로부터 상세화 하거나, 수집된 Entity 후보로부터 작성하거나<br/>현행 데이터 리버스를 통해 작성하는 방법이 있다.<br/>![](http://www.dbguide.net/publishing/img/dbguide/edu/da0502_0601.gif)

  - ### 논리 데이터 모델링
    - #### 논리 데이터 모델링 이해 [:bookmark_tabs:](http://www.dbguide.net/db.db?cmd=view&boardUid=12853&boardConfigUid=9&boardIdx=41&boardStep=1)<br/>데이터베이스 설계 프로세스의 Input으로서 비즈니스 정보의 구조와 규칙을 명확히<br/>표현하는 기법. 데이터 모델링의 최종 상태. 어떻게 데이터에 액세스하며, 누가<br/>데이터에 액세스하며, 그러한 액세스의 전산화와 분리되어 비즈니스 데이터에<br/>존재하는 사실을 인식 · 기록하는 기법.
    - #### 속성 정의 [:bookmark_tabs:](http://www.dbguide.net/db.db?cmd=view&boardUid=12854&boardConfigUid=9&categoryUid=216&boardIdx=41&boardStep=1)<br/>Entity에서 관리되는 구체적인 정보 항목. 더 이상 분리가 안 되는 데이터 보관 최소 단위<br/>속성에 해당하는 값들을 구성요소로 하는 집합.
    - #### Entity 상세화 [:bookmark_tabs:](http://www.dbguide.net/db.db?cmd=view&boardUid=12855&boardConfigUid=9&categoryUid=216&boardIdx=41&boardStep=1)<br/>Entity 내의 모든 인스턴스는 유일하게 구분되야 함. 유일성을 보장하기 위해 식별자 필요<br/>본질, 실질( 주 ), 대체( 보조 ) 식별자로 구분 가능.
    - #### 이력 관리 정의 [:bookmark_tabs:](http://www.dbguide.net/db.db?cmd=view&boardUid=12856&boardConfigUid=9&categoryUid=216&boardIdx=41&boardStep=1)<br/>데이터는 버리지 말고 모아놓아, 더 좋은 정보를 제공할 수 있도록 해야한다.
    - #### 논리 데이터 모델 품질 검토 [:bookmark_tabs:](http://www.dbguide.net/db.db?cmd=view&boardUid=173630&boardConfigUid=9&categoryUid=216&boardIdx=41&boardStep=1)<br/>개념, 논리, 물리 데이터 모델링의 각 단계가 수행된 후 각 단계에서 작성된<br/>개념, 논리, 물리 데이터 모델에 대해 이루어짐. 모든 이해관계자가 동의하는 검토 기준이 필요.

  - ### 물리 데이터 모델링
    - #### 물리 데이터 모델링 이해 [:bookmark_tabs:](http://www.dbguide.net/db.db?cmd=view&boardUid=12858&boardConfigUid=9&boardIdx=42&boardStep=1)<br/>논리적 모델을 특정 데이터베이스로 설계하여 생성된, 데이터를 저장 가능한 물리적 스키마.<br/>논리 데이터 모델을 사용하려는 각 DBMS의 특성을 고려하여<br/>데이터베이스 저장 구조( 물리 데이터 모델 )로 변환한다.

    - #### 물리 요소 조사 및 분석 [:bookmark_tabs:](http://www.dbguide.net/db.db?cmd=view&boardUid=12859&boardConfigUid=9&categoryUid=216&boardIdx=42&boardStep=1)<br/>시스템 구축 관련 명명 규칙 파악, 하드웨어 자원 파악, 운영체제 및 DBMS 버전 파악,<br/>DBMS 파라미터 정보 파악, 데이터베이스 운영과 관련된 관리 요소 파악.

    - #### 논리 - 물리 모델 변환 [:bookmark_tabs:](http://www.dbguide.net/db.db?cmd=view&boardUid=12860&boardConfigUid=9&categoryUid=216&boardIdx=42&boardStep=1)<br/>논리 영역과 물리 영역은 여러 가지 관점에서 조금씩은 다르다.<br/>다음의 기준으로 논리 데이터 모델과 물리 데이터 모델의 영역을 구분하여 접근하고 있다.<br/>Entity - Table 변환, 속성 - Column 변환, 관계 변환, 관리상 필요한 Column 추가,<br/>데이터 타입 선택, 데이터 표준 적용.<br/>![](http://www.dbguide.net/publishing/img/dbguide/edu/070725_edu_1.gif)

    - #### 반정규화 [:bookmark_tabs:](http://www.dbguide.net/db.db?cmd=view&boardUid=12861&boardConfigUid=9&categoryUid=216&boardIdx=42&boardStep=1)<br/>정규화 된 데이터 모델은 시스템의 성능 향상, 개발 과정의 편의성, 운영의 단순화를<br/>위해 정규화 원칙에 위배되는 행위를 의도적으로 수행함. 이런 과정이 반정규화 과정임<br/>Table 과 Column 관점에서의 반정규화 과정이 존재함. 성능과 관리효율을 증대시킴<br/>데이터의 일관성 및 정합성을 해칠 위험을 내포함. 또한 유지하는데 그만큼 비용이 발생.

    - #### 물리 데이터 모델 품질 검토 [:bookmark_tabs:](http://www.dbguide.net/db.db?cmd=view&boardUid=173631&boardConfigUid=9&categoryUid=216&boardIdx=42&boardStep=1)<br/>모델 설계가 끝나고 데이터베이스 객체의 생성 후, 개발 단계로 가기 전. 이해관계자들이<br/>모두 동의하는 검토 기준으로, 향후에 발생 가능한 성능 문제를 사전에 검토하여 최소화.

-----



-----

# 용어 찾기

- ### ~~전사적~~<br/>기업 전체란 의미

- ### 도메인<br/>

- ### 특수 데이터 타입( CLOB, Long Raw )<br/>

- ### ~~표준 코드~~<br/>001 : 빨강, 002 : 파랑   처럼 미리 정의된 코드. 공통된 정보를 간략하게 표현하기 위해 만든 코드

- ### 정합성<br/>

- ### 데이터 리버스<br/>

- ### 메타 정보, 메타 시스템, 메타 데이터 시스템<br/>

- ### 프로세스 모델링<br/>

- ### 프로세스 중심 개발 방법, 프로세스 중심의 분석/설계 방법<br/>

- ### 계층형 데이터베이스<br/>

- ### 구조적 방법론 (프로세스 중심의 데이터 관리 기법)<br/>

- ### 데이터 품질 툴<br/>

- ### 통합 데이터 구조<br/>

- ### 난로 연통 시스템<br/>![](http://www.dbguide.net/publishing/img/dbguide/edu/070321_gu_1.gif)

- ### 정보 인프라<br/>

- ### M:M 관계<br/>

- ### 색인화<br/>

- ### 순환 관계( Recursive )<br/>

- ### 배타적 관계(Arc)<br/>

- ### 세그먼트<br/>

- ### 객체지향 모델링<br/>

- ### 데이터 아키텍처 프레임워크<br/>

- ### 아키텍처 모델<br/>

- ### 상향식( Bottom-Up )<br/>

- ### 하향식(Top-Down)<br/>

- ### 인조 식별자(Artificial Unique Identifier)<br/>

- ### 전산화<br/>

- ### 