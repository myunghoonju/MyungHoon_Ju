#### hard-coded dependency
아래의 코드는 Cash 수정 없이는 Exchange 의존성을 수정할 수 없다
```java
class Cash01 {
    
    private final int dollars;
    
    public int euro() {
        return new Exchange().rate("USD", "EUR") * this.dollars;
    }
}
```
Cash 객체를 이용하여 다른 함수를 테스트 하고자 할 때
print() 테스트 임에도 five.euro() 에서 new Exchange 생성 및 함수 호출을 한다 
```java
Cash five = new Cash01("5.00");
print("$5 equals to " + five.euro());
```
결합도를 낮추고 테스트 실행 범위를 줄이려면?
```java
class Cash02 {

    private final int dollars;
    private final Exchange exchange;

    Cash(int dollars, Exchange exchange) {
        this.dollars = dollars;
        this.exchange = exchange;
    }
    
    public int euro() {
        return this.exchange.rate("USD", "EUR") * this.dollars;
    }
}

// 개선된 테스트
// 객체가 필요한 객체를 스스로 생성하여 주입받지 못하게 하자
// 생성자에 필요한 의존성 클래스를 주입받도록 하자
Cash02 five = new Cash02(5, new FakeExchange());
print("$5 equals to " + five.euro());
```

결합도가 낮은 상태를 유지하면서 new 키워드를 사용해야 한다면?  
생성자를 제공하여 하드코딩 주입을 하게 한다  
첫번째 예시보다 테스트에 용이하고, 유지보수성이 올라간다
```java
class Cash03 {

    private final int dollars;
    private final Exchange exchange;

    // secondary
    Cash03(int dollars) {
        this.dollars = dollars;
        this.exchange = new NYSE();
    }
    
    // primary
    Cash03(int dollars, Exchange exchange) {
        this.dollars = dollars;
        this.exchange = exchange;
    }
    
    public int euro() {
        return this.exchange.rate("USD", "EUR") * this.dollars;
    }
}
```