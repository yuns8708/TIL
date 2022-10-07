# enum 클래스

- 클래스처럼 보이게 하는 상수 (고정된 카테고리의 값들을 다루는 것)


- 서로 관련있는 상수들끼리 모아 상수들을 정의함


- 선언된 순서에 따라 index값을 가진다(0부터 시작)


- 열거형 변수 선언 후 ;세미콜론을 붙이지 않는다


- 상수와 특정 값을 연결시킬 경우에만 ;세미콜론을 붙인다.


---

## enum 클래스 만들기
회원 정보에서 사용자 / 관리자 둘 중 하나에 속하도록 세팅해보기

1. UserRoleEnum.java 파일 생성
2. class를 enum키워드로 변경
3. 필요한 변수 선언
```java
public enum UserRoleEnum {
    USER, // 사용자 권한
    ADMIN // 관리자 권한
}
 
```
4. User.java 파일 생성 후 필드 타입을 enum클래스 이름으로 지정

```java
    @Column(nullable = false)
    @Enumerated(value = EnumType.STRING) // enum 이름 값을 저장
    private UserRoleEnum role;
```

### @Enumerated

- EnumType.ORDINAL : enum 순서 값을(integer) DB에 저장


- EnumType.STRING : enum 이름을(String) DB에 저장