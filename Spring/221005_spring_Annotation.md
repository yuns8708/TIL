# Annotation
사전상으로 주석이라는 의미이지만, Java에서는 자바 소스 코드에 추가하여 사용할 수 있는 메타데이터의 일종이다. 

소스 코드에 @를 이용하여 추가할 시 다양한 기능을 사용할 수 있다.

---

## Annotation의 장점

- 코드량이 감소하고 유지보수하기 쉽다.
- 생산성이 증가된다.

---

## Annotation의 종류

### @Component
- Class를 Spring의 Bean으로 등록함

### @Controller
- Class가 Controller라는 것을 알려줌

- View를 반환하기 위해 사용함. Model객체를 만들어서 데이터를 담고 View를 찾는 역할을 한다.

- 하지만 컨트롤러로 Data를 반환해야 하는 경우도 있는데, 이럴 경우 @ResponseBody를 이용해 JSON형태로 데이터를 반환할 수 있다.

### @RestController
- @Controller에 @ResponseBody가 추가된 것. 컨트롤러 클래스의 각 메소드마다 @ResponseBody를 붙일 필요가 없어진다.

- JSON형태로 객체 데이터를 반환하기위해 사용

### @ResponseBody
- 요청과 응답을 보낼 때, 본문(Body)에 데이터를 담아서 보내야한다. 이 때 사용되는 데이터 형식이 JSON이다.

- 서버 -> 클라이언트 통신 메시지 : 응답 (response)

- 자바객체 -> 컨트롤러 -> @ResponseBody가 HTTP응답 바디로 변환

### @RequestBody
- 클라이언트 -> 서버 통신 메시지 : 요청 (request)

- JSON데이터 -> 컨트롤러 -> @RequestBody가 자바 객체로 변환

- Body에 전달되는 데이터를 메소드의 인자와 매칭시켜


### @ReuestParam
- URL에 전달되는 파라미터를 메소드의 인자와 매칭시켜, 파라미터를 받아 처리 할 수 있다.

### @Entity
- 해당 클래스가 Entity라는 것을 알려줌
- 이 annotation을 붙일 경우 JAP에서 클래스에 정의된 필드들을 이용해 DB에 테이블을 만들어줌
- 엔티티란, 데이터베이스의 테이블과 같음. (세로 열은 Column, 가로열은 엔티티 객체, 테이블 전체가 엔티티)

### @Column
- 엔티티의 각 Column을 의미
- @Column(nullable = false) : null 값이 들어갈 수 없음
- @Column(name = "user_id") : 컬럼의 이름 지정
- @Column(unique = true) : 해당 컬럼과 중복된 값 생성 불가

### @Size
- @Size(min = 3, max = 50) : 최대, 최소값 지정 가능
- JAP와 Hibernate로부터 독립적인 bean을 만듦

### @Id
- 해당 필드가 테이블의 주 키(primary key)여할을 한다는 것을 알림

> @Id  
> @GeneratedValue(strategy = GenerationType.AUTO)  
> private Long id;


### @GeneratedValue
- 주 키의 값을 위한 자동 생성 전략 명시
- strategy = GenerationType.AUTO는 데이터베이스 종류에 따라 IDENTITY, SEQUENCE, TABLE 방법 중 하나를 자동으로 선택해준다.
- Primary Key가 자동으로 1씩 증가하는 형태로 생성된다

### @Transactional
- Service 클래스 내에서 메소드에 붙음
- DB의 상태를 변경하는 작업이나 한번에 수행되어야하는 연산들을 의미함
- begin, commit을 자동 수행
- 예외발생 시 rollback 처리 자동 수행

#### DB 운영 방식 - Primary, Repolica
스프링에 Primary DB endpoint, Replica DB endpoint를 설정하면 해당 개념을 사용할 수 있다.
- DB 훼손 가능성을 고려하여 쓰기 전용인 primary와 읽기 전용인 replica로 구분하여 사용함.

- primary에 문제가 생겼을 경우 replica서버 중 하나가 primary로 스위칭된다.

- @Transactional(readOnly = false) : 쓰기 전용 (기본값)
- @Transactional(readOnly = true) : 읽기 전용

### @AuthenticationPrincipal
- 스프링 시큐리티 어노테이션
- 로그인한 사용자의 정보를 매개변수로 전달받을 수 있음

---

## Lombok Annotation

### @RequiredArgsConstructor
- Lombok의 생성자 주입 Annotation
- final이 붙거나 @NotNull이 붙은 필드의 생성자를 자동으로 생성해준다.
- 
### @NoArgsConstructor
- Lombok의 생성자 주입 Annotation
- 파라미터가 없는 기본 생성자 생성

### @AllArgsConstructor	
- 모든 필드 값을 파라미터로 받는 생성자 생성

### @Getter / @Setter
- 해당 필드의 기본 getter / setter 생성