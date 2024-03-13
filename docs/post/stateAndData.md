#### 정체성 & 상태 & 행위
- 기본적으로 객체는 다음 세가지의 요소를 가진다.  
  - 정체성: 다른 객체들과 구분이 되는 것
  - 상태: 객체가 알고있는 것
  - 행위: 요청에 대해서 객체가 할 수 있는 것
- 불변객체는 정체성을 가지지 않으며 상태가 변하지 않는다
- 결국 불변객체의 정체성은 상태와 일치한다

Q. 다음은 불변객체일까 가변객체일까?  
- content()가 반환하는 문자열은 코드상으로 어떤 것일지 알아내기 어렵다
- 아래의 객체를 사용하기 위하여 항상 new WebPage(path) 통해서 새로운 객체를 만든다
>> class WebPage {    
>> &emsp;  private final URI uri;  
>> &emsp;  WebPage(URI path) {  
>> &emsp;&emsp;  this.uri = path;  
>> &emsp;  }  
>> &emsp;  public String content() {  
>> &emsp;  // return web page content  
>> &emsp;   }  
>> }  

Q. 다음은 불변객체일까 가변객체일까?
- 상태에 따라서 파일 객체의 정체성 또한 함께 변화한다
>> public void echo() {  
>> &emsp;  File file = new File("/user/test.txt");  
>> &emsp;  System.err.print("File size: %d", file.length());  
>> }  

Q. 다음은 불변객체일까 가변객체일까?  
- 상태를 변화시키지 않으며, 여전히 불변객체이다  
- 내용이 수정될 수 있으나 동일 페이지를 가리킨다  
>> class WebPage {    
>> &emsp;  private final URI uri;  
>> &emsp;  WebPage(URI path) {  
>> &emsp;&emsp;  this.uri = path;  
>> &emsp;  }  
>> &emsp;  public void modify(String content) {  
>> &emsp;  // return web page modified content  
>> &emsp;   }  
>> }  

>> &emsp;  WebPage webPage = new WebPage("http://localhost:8080");  
>> &emsp;  webPage.modify("< html/>");  

- 불변과 가변에 대한 물음은 state와 data의 혼동에서 나온다  
  - 다음은 이러한 혼동에 의한 살짝 엉뚱한?! 테스트이다
  - results와 unmodifiableResults는 다른 정체성을 가진 객체이며 비교할 이유가 애초에 없다  
  - 덪붙여 add()를 통해서 입력받는 것은 상태가 아닌 데이터이다.  

> @Test  
> @DisplayName("Collections.unmodifiableList 변경 테스트")  
> &emsp; void collections_unmodifiable_() {
> &emsp; List<String> results = new ArrayList<>();  
> &emsp; results.add("a");  
> &emsp; results.add("b");  
> &emsp; results.add("c");  
> &emsp; results.add("d");  
> &emsp; List<String> unmodifiableResults = Collections.unmodifiableList(results);  
> &emsp; results.add("e");  
> &emsp; results.add("f");  
> &emsp; results.add("g");  
> &emsp; assertThat(unmodifiableResults).hasSize(7).contains("e", "f","g");  
> }  