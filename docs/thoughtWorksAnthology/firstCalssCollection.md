#### First class collection  
클린코드 & TDD 강의를 시작하며 thoughtWorks anthology를 살펴보기로 했습니다.  
가장 먼저 살펴볼 내용은 일급 컬렉션(first class collection)입니다.:smile:  

 - 컬렉션을 포함한 클래스는 반드시 다른 멤버 변수가 없어야 합니다. (아래와 같은 이점들을 가질 수 있어요)  
   
        - 비즈니스에 종속적인 자료구조 (i.e.., 특정 비즈니스 로직에 필요한 자료구조를 커스텀 구현해요)  
        - Collection 불변성 보장(final 키워드는 재할당 금지, 불변 아님)  
        - 상태와 행위를 한 곳에서 관리  
        - 이름이 있는 컬렉션  
      
- 각각에 대한 예시는 https://jojoldu.tistory.com/412 를 참고하도록 해요!  
[< Back](https://git.io/JL704)  
