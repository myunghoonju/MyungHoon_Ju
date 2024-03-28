#### getter & setter

Q. Cash 클래스는 객체지향 스러운가?
- 함수의 이름(naming 참조)
- 생성자의 부재(객체를 생성하지 않음, 클래스라기 보다 자료구조에 더 가깝다)
- getter를 통한 필드 직접접근(캡슐화 위반)
  - 메세지를 통해서(메소드 호출) 객체간에 데이터를 주고 받는다
  - getter도 함수이며 단순 반환이 아닌 로직을 추가 할 수 있다 
    그럼에도 여전히 사용자에게 getXXX()는 행위가 아닌 데이터로 보일 뿐이다.
- setter를 통한 정체성의 가변성
```java
class Cash {
    
    private int dollars;
    
    public int getDollars() {
        return this.dollars;
    }
    
    public void setDollars(int val) {
        this.dollars = val;
    }
}
```
Q. 이름 한 끗차로 달라지는 의미(능동적, 수동적)
- dollars(): Cash야 달러를 얼마나 가지고 있니?
- getDollars(): Cash야 너의 정보 중에 달러를 찾아서 가져오련! 

```java
class Cash {
    private final int value;
    
    public int dollars() {
        return this.value;
    }
}

class Cash {
    private final int value;

    public int getDollars() {
        return this.value;
    }
}
```