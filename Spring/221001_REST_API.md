
# REST

Representational State Tansfer

- HTTP URI를 통해 자원을 명시하고,
- HTTP Method(POST,GET,PUT,DELETE,PATCH 등)을 통해
- 해당 자원(URI)에 대한 CRUD operation(컴퓨터 소프트웨어가 가지는 기본적인 데이터 처리 기능, 생성, 읽기, 수정, 삭제)을 적용하는 것

### REST 의 특징
- 서버-클라이언트 구조
- 무상태
- 캐시 처리 가능
- 계층화
- 인터페이스 일관성


### REST 의 구성 요소
- 자원(resource) : HTTP URI
- 행위(verb) : HTTP Method
- 표현(Representation) : HTTP Message Pay Load

---

## REST API
REST의 원리를 따르는 API


### REST API 설계 규칙
- URI는 동사보다 명사, 대문자보다는 소문자를 사용한다
- 마지막에 슬래시/를 포함하지 않는다.
- 언더바 대신 하이픈을 사용한다
- 파일확장자를 URI에 포함하지 않는다. (.jpg등)
- 행위를 포함하지 않는다 (delete-post x / post o)

### RESTful이란?
REST의 원리를 따르는 것. REST API의 설계 규칙을 올바르게 지키고 적절한 Method를 사용하여 CRUD기능을 처리해야한다.