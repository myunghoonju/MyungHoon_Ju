#### class 이름
> 클래스는 new 키워드를 이용하여 객체를 생성한다  
> 이를 통하여 생성된 객체들에게 클래스는 이들의 부모가 되는 셈이다?!?!

>  절차지향적인 시선과 객체지향적인 시선에 따라 클래스의 이름은 다르게 나타낼 수 있다.    
>  객체는 단순히 데이터를 처리하는 통로 역할이 아닌, 다른 객체들과 그들의 조합을 나타내는 대표이다
>  클래스의 이름을 정의할 때 그것의 행위가 아닌 무엇인지에 대하여 더 생각해보자

> // Before  
>  class CashFormatter {  
>  &emsp; private int dollar;  
>  
>  &emsp; CashFormatter(int dlr) {  
>  &emsp; &emsp; this.dollar = dlr;  
>  &emsp; }
>  
>  &emsp; public String format() {  
>  &emsp; &emsp; return String.format("$ %d, dollar);  
>  &emsp; }  
>  }

> // After   
> class Cash {  
>  &emsp; private int dollar;
>
>  &emsp; Cash(int dlr) {  
>  &emsp; &emsp; this.dollar = dlr;  
>  &emsp; }
>
>  &emsp; public String usd() {  
>  &emsp; &emsp; return String.format("$ %d, dollar);  
>  &emsp; }  
>  }

#### method 이름
> 생성하는 함수는 명사, 조작하는 함수는 동사로 지어보자

> 아주 작은 차이지만 사고방식?!의 차이를 보여준다   
> 카페에서 주문을 할 때 우리는...  
> 1) 커피 한잔 주세요! &ensp; 2) 커피 좀 내려 주세요!  
> &emsp; -> 함수의 결과값을 기대하였다, 행동을 지시하지 않았다  
>> String read(File file); -> String content(File file);  
>> int add(int x, int y); -> int sum(int x, int y);
 
> 예외상황) Boolean 반환함수  
> 형용사를 붙여보자!(is-를 붙여보고 자연스럽게)  
>> boolean empty(); (is empty)  
>> boolean equals(); (is equals ?!?!) -> boolean equalTo()&ensp;/&ensp;present()  

> Boolean 반환함수는 명사가 어색할까?  
>> if (name.emptiness() == true) {} -> "if emptiness of the name is true" // 어색함  
>> if (name.empty()) {} -> "if name is empty" // 자연스러움