# Generics

메소드나 컬렉션 클래스에 컴파일 시의 타입 체크를 해주는 기능

객체의 타입을 컴파일 할 때 체크해주기 때문에 안정성이 높아진다. (의도하지 않은 타입의 객체가 저장되는 것이나, 잘못된 형변환을 막을 수 있음)

컬렉션을 만들 때 <>를 쓰는것 => 컬렉션이 이미 제네릭스를 이용해서 구현되어있기때문

---

ex)
List<String> strList = new ArrayList<String>();

=> <>안에 String이란 타입을 선언해서, strList가 사용할 객체의 타입을 지정해주는것.

---
## 와일드카드 <?>
제네릭스의 자리에 아무 것이나 와도 된다는 의미

하나 이상의 타입을 지정해야할 경우 사용한다.

---


# 람다
함수를 간단하게 표현하는 익명 함수

코드가 간결하고 편리해지지만, 똑같은 로직을 또 써야 할 때는 중복된 코드가 많아지기 때문에 함수로 만드는 것을 고려한다.

> 변수 -> { 실행할 내용 }

단일 실행문일 시, {} 생략 가능