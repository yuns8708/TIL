# 221003 스프링 Controller, Service, Repository

![](https://velog.velcdn.com/images/yuns8708/post/3719993d-517b-47ee-ba1b-4d845baea021/image.png)

## 웹사이트의 흐름
1. 클라이언트가 요청을 보냄
2. 보낸 요청을 Controller가 받아서, 요청을 처리하기 위해 Service를 호출
3. Service가 요청을 처리함(비즈니스 로직을 수행)
4. Repository도 DB에 접근하여 데이털르 처리함
5. 처리된 정보를 Controller에게 전달함
6. Controller가 전달된 정보를 다시 클라이언트에게 보냄

---

## Controller
클라이언트의 요청을 받고 응답을 되돌려주는 가장 바깥 부분

## Service
사용자의 요구사항을 처리하고, DB정보가 필요할 시 Repository에 요청하는 중간 부분

## Repository
DB와 직접 맞닿아있어 자료를 생성, 조회, 변경, 삭제 처리하는 가장 안쪽 부분.

프로젝트 진행 시, 가장 안쪽인 Repository부터 바깥쪽인 Controller 순서로 작성하게 된다.

---

## Controller과 Service, Repository를 분리해서 사용하는 이유

Service와 Repository를 따로 만들지 않아도, Controller에서 모든 응답을 처리 할 수 있다.

하지만 굳이 나눠서 사용해야 하는 이유는 무엇일까?

### Controller에 몰아서 작성하면 안좋은 이유
- 한 개의 클래스에 너무 많은 양의 코드 존재. 코드 이해가 어려워짐
- 코드 추가 혹은 변경 요청이 생길 때, 모듈화가 되어있으면 변경이 쉬움
- 객체지향 프로그래밍에 맞지 않음. controller는 controller만의 일을 하는 것이 중요
