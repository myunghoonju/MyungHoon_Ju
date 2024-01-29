_primary keys_  
 - partition key  
	- unique attribute  
 		- 실제 데이터가 들어가는 위치  

 - composite key  
	- partition key + sort key  
 	 		- same customer with a different purchase date  

_data access management_   
	- with aws IAM  
	
_index_    
  - global secondary index  
  	 	- 테이블 생성 후에도 추가/변경/삭제 가능  
 			- 다른 partition key, sort key 사용 가능

  - local secondary index  
  	 	- 테이블 생성 후 변경/삭제 불가능  
 			- 같은 partition key with different sort key  
