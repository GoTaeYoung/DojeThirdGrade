# intj를 문자열로 검색했을 때

`explain

select * from test

where intj = '2839990793';`

실행결과 : 성공

id, select_type, table, partitions, type, possible_keys, key, key_len, ref, rows, filtered, Extra

'1', 'SIMPLE', 'test', NULL, 'ref', 'intj', 'intj', '4', 'const', '1', '100.00', NULL

이유 : 묵시적 형변환으로 인해서 문자열이 정수형으로 변환됐기 때문



# intj를 정수형으로 검색했을 때

`explain

select * from test

where intj = 2839990793;`

실행결과 : 성공

id, select_type, table, partitions, type, possible_keys, key, key_len, ref, rows, filtered, Extra

'1', 'SIMPLE', 'test', NULL, 'ref', 'intj', 'intj', '4', 'const', '1', '100.00', NULL

이유 : 컬럼 타입이 조건문과 일치했기 때문



# str을 정수형으로 검색했을 때

`explain

select * from test

where str = 46829860833270;`

실행결과 : 성공

id, select_type, table, partitions, type, possible_keys, key, key_len, ref, rows, filtered, Extra

'1', 'SIMPLE', 'test', NULL, 'ALL', 'str', NULL, NULL, NULL, '131594', '10.00', 'Using where'

이유 : 묵시적 형변환으로 인해 문자열이 정수형으로 변환되어 검색된다

하지만 인덱스가 있어도 묵시적 형변환으로 인해 모든 행을 조회하기 때문에 수행속도가 느려진다



# str을 문자열로 검색했을 때

`explain

select * from test

where str = '46829860833270';`

실행결과 : 성공

id, select_type, table, partitions, type, possible_keys, key, key_len, ref, rows, filtered, Extra

'1', 'SIMPLE', 'test', NULL, 'ref', 'str', 'str', '194', 'const', '1', '100.00', NULL

이유 : 컬럼 타입이 조건문과 일치했기 때문