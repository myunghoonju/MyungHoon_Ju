_Elastic block storage(ebs)_  
 - 저장 공간이 생성되며 ec2인스턴스에 부착된다.
 - 디스크 볼륨 위에 file system이 생성된다.
 - ebs는 특정 availability zone(az)에 생성된다.  
 	- 하나의 region에 다수의 az가 존재 할 수 있다.(digaster recovery)  

_ebs volume type_  
 - SSD
 	- general purpose SSD(GP2): 최대 10K IOPS를 지원, 1GB당 3IOPS 속도.
 	- provisioned IOPS SSD(IO1): 극도의 I/O 요구하는 환경에서 사용. 10K 이상의 IOPS 지원.

 - HDD
 	- throughput optimiozed HDD(ST1): bigdata datawarehouse, log processing 주로 사용(boot volume 사용불가)  
 	- CDD HDD(SC1): 파일 서버와 같이 드문 volume 접근시 사용, 가격 저렴(boot volume 사용불가)  
 	- magnetic(Sandard): 디스크 1GB당 가장 저렴한 비용.(boot volume 사용가능)  
 <sub>_*boot volume 사용가능 = os 장착 가능_</sub>
