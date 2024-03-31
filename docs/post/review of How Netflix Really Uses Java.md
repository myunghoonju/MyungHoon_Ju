#### Java at Netflix
- 영상 개시일: FEB 26, 2024
- 발표영상을 보고 자바관련된 부분을 일부 기록해본다    
  - 대부분의 시스템에 java 17 적용되어 있다고 한다
  - Azul Platform Core 사용(https://www.azul.com/java-alternative-vendors/)
  - 참고로 IntelliJ 에디터를 기본으로 사용하고 plugin 개발도 한다고 한다
  - 최근까지 많은 서비스들의 java 버전은 8 또는 11이었다
  - 장점보다는 버전 업그레이드에 따르는 라이브러리 호환성을 맞춰주는 일이 더 부담되었기 떄문이다
  - 하지만 아무런 코드 변경 없이 자바 버전을 8에서 17로 변경하는 경우 다음의 장점을 발견하였다
    - 가비지 컬렉터(G1) 성능 향상에 따른 CPU 사용량이 약 20% 증가
  - java 21+, virtual thread
    - java 8 lambda 이후 주목 할 만한 기능
    - 리액티브 코드(RxJava & WebFlux)의 대체재로 사용하려 한다
      - 해당 부분의 경력이 많은 시니어임에도 불구하고 이해하기 수월하지 않음
    - CPU 사용량이 많은 경우 오히려 성능이 떨어지는 경우가 있었다
    - ZGC 가비지 컬렉터
      - G1 가비지 컬렉터보다 나은 성능을 제공할 것으로 기대된다

[see original presentation](https://www.infoq.com/presentations/netflix-java/)