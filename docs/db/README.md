## TRANSANCTION
* READ UNCOMMITTED  
This is also called a dirty read.  
An operation retrieves unreliable data which is updated by transaction that is not committed.
This kind of operation does not adhere to the ACID principle of database design.  
It is considered very risky because the data could be rolled back, or updated further before being committed; then, the transaction doing the dirty read would be using data that was never confirmed as accurate.
