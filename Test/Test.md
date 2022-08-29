### Q. 테스트 코드를 작성하는 이유는?

<details>
<summary>답변 확인하기</summary>
  
```
결론적으로 개발에 도움이 되기 때문
 
1. 코드를 매번 수정할 때마다 WAS를 내렸다가 다시 실행하는 일을 반복할 필요가 없어짐

2. System.out.println 등을 통해 사람이 눈으로 검증하지 않게 자동 검증해줌

3. 어떤 기능을 추가할 때 기존 기능이 잘 작동되는 것을 편리하게 검증할 수 있음
```
  
</details>

### Q. @RunWith 애노테이션의 용도는?

<details>
<summary>답변 확인하기</summary>
  
```
테스트를 진행할 때 JUnit에 내장된 실행자 외에 다른 실행자를 실행시킴
예를 들어, @RunWith(SpringRunner.class)로 사용 시 SpringRunner라는 스프링 실행자를 사용한다는 의미인데,
이는 스프링 부트 테스트와 JUnit 사이에 연결자 역할을 함

※ JUnit5부터는 @ExtendWith(SpringExtension.class)로 변경됨
※ @SpringBootTest에는 이미 적용되었기에 @SpringBootTest 사용 시 생략 가능
```
  
</details>

### Q. @WebMvcTest의 용도는?

<details>
<summary>답변 확인하기</summary>
  
```
여러 스프링 테스트 어노테이션 중 Web(Spring MVC)에 집중할 수 있는 어노테이션으로 웹에서 테스트하기 어려운 컨트롤러를 테스트 하는데 적합
단, @WebMvcTest의 경우 @Service, @Component, @Repository 등은 사용 불가로 JPA 기능이 작동하지 않으며, @Controller, @ControllerAdvice 등 외부 연동과 관련된 부분만 활성화됨
따라서 간단하게 테스트 하기 위해서는 @AutoConfigureMockMvc가 아닌 @WebMvcTest이 적합
```
  
</details>

### Q. @AutoConfigureMockMvc란?

<details>
<summary>답변 확인하기</summary>
  
```
@WebMvcTest와 마찬가지로 컨트롤러를 테스트할 때 서블릿 컨테이너를 모킹하는데 사용된다.
@WebMvcTest와 가장 큰 차이점은 컨트롤러 뿐만 아니라 테스트 대상이 아닌 @Service나 @Repository가 붙은 객체들도 모두 메모리에 올린다.
@WebMvcTest 대비 MockMVC를 보다 세밀하게 제어하기 위해 사용

※ 전체 애플리케이션 구성을 로드하고 MockMVC를 사용하려는 경우 @AutoConfigureMockMvc와 결합된 @SpringBootTest를 고려
※ @WebMvcTest는 @SpringBootTest와 같이 사용될 수 없다. 왜냐하면 각자 서로의 MockMvc를 모킹하기 때문에 충돌이 발생하기 때문
  
참고자료 : https://we1cometomeanings.tistory.com/65  
```
  
</details>

### Q. MockMvc란?

<details>
<summary>답변 확인하기</summary>
  
```
웹 API를 테스트할 때 사용 하는 것으로서 스프링 MVC 테스트의 시작점으로 perform 메서드를 통해 HTTP GET, POST 등의 요청을 보낼 수 있음
```
  
</details>

### Q. JUnit의 assertThat 대신 assertj을 사용하는 이유는?

<details>
<summary>답변 확인하기</summary>
  
```

assertJ는 좀 더 풍부한 문법을 제공하고 개발 도구의 자동 완성 기능과 함께 메서드 체이닝 등을 통해 직관적인(가독성 있는) 테스트 흐름을 작성할 수 있음

JUnit5의 경우, assertEquals(expected, actual)과 같이 두 개의 인자를 받아서 비교 -> assertEquals()는 왼쪽이 expected인지 actual인지 혼동
  
assertThat()은 actual 인자 하나만 요구하고 그 뒤로 메소드 체이닝을 하므로 actual(왼쪽)과 expected(오른쪽)를 명확하게 구분

참고자료 : https://steady-coding.tistory.com/351
```
  
</details>
