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
  
  * 확인사항  
      * 인덱스는 열 단위에 생성된다.  
      * where절에서 사용되는 열에 인덱스를 만들자.  
      * where절에 사용되더라도 자주 사용되야 가치가 있다.  
      * 데이터 중복도가 높은 열은 인덱스 만들어도 효과가 크지않다.  
      * 외래 키를 지정한 열에는 자동으로 외래 키 인덱스가 생성된다.
      * JOIN에 자주 사용되는 열에는 인덱스 생성해주는 것이 좋다.  
      * INSERT/UPDATE/DELETE가 얼마나 자주 일어나는지를 고려해야 한다.  
      * 사용하지 않는 인덱스는 제거하자.(공간확보 및 INSERT에서 발생하는 부하감소)  
    
 [< Back](https://git.io/JL704)
