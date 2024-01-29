#### 불변객체
- immutable 객체는 mutable 객체보다 간결하고 짧게 작성이 가능하다.
- mutable 객체들은 보통 절차지향 프로그래밍 방식에서 자주 보이게 된다.  

>    - mutable 객체는 일시적으로 결합도가 높은 코드를 작성하게 한다.  
>    - 아래의 코드는 의도한 값을 출력하기 위해서 코드 작성의 순서가 중요해진다. (bad)
> 
>>    Cash price = new Cash();  
>>    50줄 뒤  
>>    price.setDollars(29);  
>>    30줄 뒤  
>>    price.setCents(95);  
>>    25줄 뒤  
>>    System.err.print(price); // "$29.95"  

>    - immutable 객체는 인스턴스화 및 초기화를 동시에 하기 때문에  
>    - 코드 작성의 순서에 따른 값 변경에 걱정이 없다. (good)    
> 
>>    Cash price = new Cash(29, 95);

>   - 객체를 수정하는 경우 새로운 객체를 반환해보자  
>>  class Cash { // 가변객체  
>>     private int dollars;  
>>     public void multiply(int factor) {  
>>         this.dollars *= factor;  
>>      }  
>>  }
> 
>>  class Cash { // 불변객체    
>>    private int dollars;  
>>    public void multiply(int factor) {  
>>      return new Cash(this.dollars * factor);  
>>    }  
>>  }

>  - 불변객체를 이용하여 더욱 명확하게 나타낼 수 있다
>  - 아래 세가지 경우에서 가장 이해하기 수월할 것 같은 것은?
>> Cash five = new Cash(5);   
>> five.mul(10);  
>> System.err.print(five); // 50  
>>  
>> Cash five = new Cash(5);    
>> Cash ten = five.mul(2);  
>> System.err.print(ten); // 10  
>>  
>> Cash money = new Cash(5);    
>> money.mul(2);  
>> System.err.print(money); // 10  
