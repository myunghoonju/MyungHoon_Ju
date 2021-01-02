## TRANSANCTION
* READ UNCOMMITTED  
This is also called a dirty read.  
An operation retrieves unreliable data which is updated by transaction that is not committed.
This kind of operation does not adhere to the ACID principle of database design.  
It is considered very risky because the data could be rolled back, or updated further before being committed; then, the transaction doing the dirty read would be using data that was never confirmed as accurate.  
RDBMS표준에서 트랜잭션 격리 수준으로 인정하지 않을 정도로 정합성에 문제가 많은 격리 수준.  
  
* READ COMMITTED  
It is the most used isolation level on online service.  
어떤 TRANSANCTION에서 변경한 내용이 COMMIT되기 전까지는 다른 TRANSACTION에서 변경 내역을 조회할 수 없다.  
e.g.., A가 인서트를 수행하는 경우 B가 조회를 하면 질의 결과는 UNDO영역에 백업된 레코드에서 가져오게 된다.
하지만 NON-REPEATABLE READ부정합 문제가 존재한다.(다른 시점에 TRANSACTION이 일어나는 경우 동일 질의문을 반복적으로 실행하면 결과가 상이할 수 있음)  

* REPEATABLE READ  
MySQL innoDB스트리지 엔진 default격리수준.  
  
[< Back](https://git.io/JL704)
