#### 인덱스
 * DBMS에서 인덱스는 데이터의 INSERT, UPDATE, DELETE성능을 저하시키는 대신 SELECT 속도를 높이는 기능이다.  
 * 대표적인 데이터 저장 방식(알고리즘)  
    * B-TREE (B for balanced)  
      * 안되는 경우: where 이후
         * not-equal로 비교된 경우
         * like 연산자
         * 인덱스 컬럼이 변형된 후 비교 되는 경우: e.g.., SUBSTRING(column, 1, 1) ...
         * 데이터 타입이 서로 다른 비교: 인덱스 컬럼의 타입을 변환해야 비교되는 경우: e.g.., where char_컬럼 = 10
         * 문자열 데이터 타입의 collation이 상이한 경우: e.g..,  where utf-8 컬럼 = euc-kr 컬럼  
           
       * MySQL은 NULL도 인덱스로 관리: e.g.., WHERE 컬럼 IS NULL...
    * Hash
    * Fractal-Tree  
  
    
 [< Back](https://git.io/JL704)
