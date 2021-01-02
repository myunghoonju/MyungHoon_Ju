### Mysql 워크벤치를 사용하여 db를 백업/복원해보기.  
  
1. 백업을 위해 data export를 클릭하고 원하는 database의 테이블을 선택한다.(필요하다면 모든 테이블 선택)  
2. Object to Export란에 있는 모든 란을 선택한다.  
3. Export to Self-Contained File란에는 백업db를 저장할 경로를 지정해준다.
4. Create Dump in ... , Include Create Schema 또한 선택한다.  
(2, 4번을 통하여 결국 백업하고자 하는 db의 모든 내용을 추출하게 된다.)  
  
![백업db 추출](/docs/files/backUp01.PNG)
  
  
  
#### 해당 테이블이 사라졌거나 복원해야 하는 경우 추출하였던 db를 import해보자.  
1. data import/restore를 클릭한다.  
2. Import from Self-Contained File에서 백업한 db.sql경로를 지정해준다.  
3. 복원할 정보가 어떤 database에 위치하는지 선택한다 (Default Target Schema)  
4. Import Progress탭을 선택하고 Start Import를 클릭하여 복원을 진행한다.  
5. 결과를 확인한다.  
  
![백업db 추출](/docs/files/backUp02.PNG)
  
 [< Back](https://git.io/JL704)
