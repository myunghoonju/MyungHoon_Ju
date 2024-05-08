```text
기본규칙: 소프트웨어에는 "언제나" 셀 수없이 많은 버그가 존재한다
```
```java
int sum(int a, int b) {
  return a + b;
}
```
```text
위의 짧은 함수도 아래와 같이 다양한 버그?!가 존재한다
1. 오버플로우 미처리
2. 기능설명 미흡
3. 객체지향적이지 않음
4. 두개를 초과하는 연산 불가
5. 소수점 연산 불가
6. long -> int 자동변환 불가
7. 둘 중 하나가 0인 경우에도 연산을 실행
8. 로그부재
...
```

```text
Q. 다음의 대화 내용은 주변에서 흔하게?! 들어본 적 있는 내용이다

A: 이번 배포판에는 버그가 3개 뿐이 없었어!
B: 엄청나군!

기본규칙에 따라 아래와 같이 생각하는 것이 더 타당하다

A: 이번 배포판에서 우리는 3개의 버그를 발견했고 수정했어!
B: 오호!
                                    OR
A: 이번 배포판에서 우리는 사용자들로부터 3개의 버그에 대한 제보를 받았고 수정했어!
B: 그렇구만!
```

```text
소프트웨어의 품질을 측정하는 기준으로 사용자에게 전달되기 이전에 
테스트를 통하여 얼마나 많은 버그를 발견하고, 수정하였는가로 품질을 가늠할 수 있다

-> 양질의 소프트웨어는 오류에 섬세하게 반응하지만 여전히 거의 오류를 일으키지 않는 소프트웨어를 말한다
```

오류 처리 방식

#### fail-safe
> 수행 중에 오류가 발생하지만 지속적으로 동작한다  
> 버그가 발생해도 원인파악이 어려워진다  
> 최악의 경우 원인도 모른체 의도하지 않은 동작을 지속한다

#### fail-fast
> 수행 중 오류가 발생하면 멈추고 사용자에게 알린다  
> 우리에게 알려진 버그를 수정한다

#### throw exception
> 객체 지향 프로그래밍에서의 섬세함을 의미한다

> 데코레이터 패턴을 이용하여 핵심로직을 간결하게 유지할 수 있다  
> 필요에 따라 핵심로직을 흩뜨리지 않고 검증을 할 수있다 

```java
Day day = new StrictDay(new JdkDay(new Date()));
int days = day.distanceTo(end);

interface Day {
    int distanceTo(Day end);
}

class JdkDay implements Day {
    private final Date date;
    JdkDay(Date d) {
        this.date = d;
    }
    
    @Override
    public int distanceTo(Day end) {
        return (int) ((end.date.getTime() - this.date.getTime()) / (24 * 60 * 60 * 1_000L));
    }
}

class StrictDay implements Day {
    private final Day origin;

    StrictDay(Day d) {
        this.origin = d;
    }

    @Override
    public int distanceTo(Day end) {
        if (day.compareTo(this) < 0) {
            throw new IllegalArgumentException(String.format("Start (%s) must be earlier than end (%s)", this, end));
        }

        return this.origin.distanceTo(day);
    }
}
```