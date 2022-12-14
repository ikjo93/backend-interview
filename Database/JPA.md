### Q. JPA를 사용하는 이유는?

<details>
<summary>답변 확인하기</summary>
  
```
관계형 데이터베이스를 사용하다보면 웹 개발이 점점 SQL 중심이 되버리는 문제 발생

이때 JPA를 사용하는 이유는 개발자가 SQL을 만들거나 유지보수 하는데 쓰는 시간을 줄이고 객체지향 프로그래밍에 좀 더 집중하기 위함임

JPA는 개발자가 객체지향 프로그래밍을 하면 이에 맞게 SQL 대신 생성해줌

이처럼 객체지향 프로그래밍(상속, 1:N 등 객체 모델링)에 좀 더 집중함으로써 ★생산성 향상과 유지 보수★ 극대화를 도모
```
  
</details>

### Q. Spring Data JPA를 사용하는 이유는?

<details>
<summary>답변 확인하기</summary>
  
```
JPA 구현체인 Hibernate 외에 다른 구현체로 쉽게 교체하기가 용이하며,
관계형 데이터베이스 외에 다른 저장소(비관계형 데이터베이스)로도 쉽게 교체하기 용이하기 때문
```
  
</details>

### Q. 도메인이란?

<details>
<summary>답변 확인하기</summary>
  
```
도메인은 게시글, 댓글, 회원, 정산, 결제 등 소프트웨어에 대한 요구사항 혹은 문제영역으로 "비지니스 로직 처리를 담당"하며,
화면, UI, 기술 인프라 등의 영역을 제외한 "시스템이 구현해야하는 핵심 비지니스 업무 영역"이다.

택시 앱을 예로 들면 배차, 탑승, 요금 등이 도메인이라고 볼 수 있다.

프로그래밍 관점에서는 @Entity가 사용된 영역을 도메인이라고 볼 수 있다.
이때 VO 같은 값 객체들도 도메인에 해당된다고 볼 수 있다.

이때 프로젝트 패키지 구조를 "도메인 영역"과 "웹 영역"으로 나누는 것이 좋다.
웹은 도메인을 의존해도 되지만 도메인은 웹을 의존하면 안되며, 향후에 웹 패키지를 삭제해도 도메인에는 전혀 영향이 없어야 한다.
예를 들어, 엔티티와 리포지토리(인터페이스)는 도메인 영역으로 하고 그 외 컨트롤러, 서비스, DTO 등은 웹 영역으로 한다.
```
  
</details>

### Q. 도메인 모델이란?

<details>
<summary>답변 확인하기</summary>
  
```
도메인이라 불리는 개발 대상을 "모든 사람(기획자 등 비개발자)이 동일한 관점에서 이해할 수 있고 공유할 수 있도록" 단순화 시킨 것
```
  
</details>

### Q. 영속성 컨텍스트란?

<details>
<summary>답변 확인하기</summary>
  
```
엔티티를 영구적으로 저장하는 환경(일종의 논리적인 개념)이다.

이때 엔티티가 영속성 컨텍스트에 포함되어 있냐 아니냐가 중요한 관건인데,
JPA의 엔티티 매니저가 활성화된 상태로 트랜잭션 안에서 데이터 베이스에서 데이터를 가져오면 이 데이터(엔티티)는 영속성 컨텍스트에 포함된 상태라고 볼 수 있다.

이 상태(엔티티가 영속성 컨텍스트에 포함)에서 해당 데이터의 값을 변경하면,
별도 Update 쿼리를 날릴 필요 없이 트랜잭션이 끝나는 시점에 해당 테이블에 변경분을 반영하며 이를 더티 체킹이라고 한다.
```
  
</details>

### Q. Entity의 PK 타입을 어떤 것으로 하는 것이 좋은지?

<details>
<summary>답변 확인하기</summary>
  
```
Long 타입(MySQL 기준 bigint 타입)

주민등록번호와 같이 비즈니스상 유니크 키나 여러 키를 조합한 복합키로 PK를 잡을 경우 유니크한 조건이 변경될 경우,
PK 전체를 수정해야하는 등의 문제가 생겨 주민등록번호나 복합키 등은 별도의 유니크 키로 추가하고 PK는 Long 타입의 정수로 두는 것이 나음
```
  
</details>

### Q. @MappedSuperclass란?

<details>
<summary>답변 확인하기</summary>
  
```
JPA Entity 클래스들이 이 어노테이션이 붙은 클래스를 상속할 경우 해당 필드들도 칼럼으로 인식하도록 함
```
  
</details>

### Q. @EntityListeners(AuditingEntityListener.class)란?

<details>
<summary>답변 확인하기</summary>
  
```
이 어노테이션이 붙은 클래스에 Auditing 기능을 포함시킴

이때 JPA Auditing 어노테이션들을 모두 활성화하기 위해서는 Application 클래스에 @EnableJpaAuditing을 추가해야함
```
  
</details>

### Q. @Enumerated란?

<details>
<summary>답변 확인하기</summary>
  
```
@Enumerated 애노테이션은 JPA로 DB에 Enum 타입의 데이터를 저장할 때 값을 어떤 형태로 저장할지 결정한다.
  
기본적으로는 int로 된 숫자가 저장되나,
숫자로 저장되면 DB로 확인할 때 그 값이 무슨 코드를 의미하는지 알 수가 없다.
  
그래서 아래와 같이 문자열로 저장될 수 있도록 선언한다.
@Enumerated(EnumType.STRING)
```
  
</details>

### Q. @EnableJpaAuditing이란?

<details>
<summary>답변 확인하기</summary>
  
```
@EnableJpaAuditing은 JPA Auditing 애노테이션들을 모두 활성화할 수 있도록 해주는 애노테이션이다.

@EnableJpaAuditing은 보통 Application 클래스에 같이 추가하나, 최소 하나의 @Entity 클래스가 필요해서 테스트 등의 목적으로 별도 JpaConfig로 추가하기도 한다.
```
  
</details>


