#### static keyword with OOP
#### 1. declarative and imperative
> a) 다음은 명령형과 선언형 작성방식의 차이를 보여준다.
>   
>  imperative style
>> public static int between(int l, int r, int x) {  
>> &emsp; return Math.min(Max.max(l, x), r);  
>> }  
>  
>  작성하는 순간 바로 연산을 처리하여 값을 얻게된다  
>> int y = Math.between(5, 9, 13);
>   
> declarative style
>> class Between implements Number {  
>> &emsp; private final Number num;  
>> &emsp; Between(Number l, Number r, Number x) {  
>> &emsp; &emsp; num = new Min(new Max(l, x), r);  
>> &emsp; }  
>>  
>> &emsp; @Override  
>> &emsp; public int intValue() {  
>> &emsp; &emsp; return num.intValue();  
>> &emsp; }  
>> }  
>
> 중간값을 구한다라는 선언을 하였다.  
> 아직 CPU에게 연산을 수행하라 명령하지 않았다.  
> intValue() 가 정말 필요한 시점에 호출하여 사용할 수 있다.  
>> Number y = new Between(5, 9, 13);  
>
> <br> 
>
> b) 만약 중간값을 구하는 방식을 변경하고 싶다면?   
>> class Between implements Number {  
>> &emsp; private final Number num;  
>> &emsp; Between(Number l, Number r, Number x) {  
>> &emsp; &emsp; this(new Min(new Max(l, x), r));  
>> &emsp; }
>>
>> &emsp; Between(Number num) {  
>> &emsp; &emsp; this.num = num;  
>> &emsp; }  
>> }  
>     
> declarative - 다른 객체와 "조합" 할 수 있다(다형성)  
>> Integer x= new Between(new IntegerWithOtherWay(5, 9, 13));  
> 
> imperative - 재작성 외에 방법이 없다  
>> int y = Math.between(5, 9, 13);  
>
> <br> 
>
> c) 가독성 & 응집력은 어떤 것이 더 좋을까?  
>> List<Integer> evens = new ArrayList<>();  
>> for (int num : numbers) {  // 머릿속으로 반복문 과정을 상상하게 된다    
>> &emsp; if (num % 2 == 0) {     
>> &emsp; &emsp; evens.add(num);      
>  &emsp; }    
>> }  
>  
>> List<Integer> evens = new Filtered(...) 는 다음과 같다      
>> List<Integer> evens = new Filtered (    
>> &emsp; numbers,    
>> &emsp; new Predicate<Integer>() {    
>> &emsp; &emsp; @Override    
>> &emsp; &emsp; public boolean suitable(Integer number) {    
>> &emsp; &emsp; &emsp; return number % 2 == 0;    
>> &emsp; &emsp; }    
>> &emsp; }      
>> );  
    
#### 2. utility and singleton  