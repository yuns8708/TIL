# 220929 자바 조건문 - switch, break, continue

## switch

if와 달리 변수가 어떤 값을 갖느냐에 따라 실행문이 선택되는 조건문이다.

```java
switch(변수){
    case 값1:
        변수가 값1일 때 실행
        break;
    case 값2:
        변수가 값2일 때 실행
        break;
    case 값3:
        변수가 값3일 때 실행
        break;        
    case 값3:
        변수가 값3일 때 실행
        break;
    default:
        변수가 값1, 값2, 값3 모두 아닐 때 실행
        }
```

default는 생략 가능하다.

break;가 없으면 case를 실행하고 그 다음 case를 실행하게 되기때문에 break;를 붙여준다.

---

## break

반복문이 중첩되어있을 경우 break문은 가장 가까운 반복문만 종료하는데, 만약 바깥쪽 반복문까지 종료시키려면 바깥쪽 반복문에 라벨을 붙여야한다.

#### Label을 사용할 때 - 출력결과 : 0 1 2 3
```java
        Label: for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 5; j++) {
                System.out.println(j);
                if(j == 3) {
                    break Label;
                }
            }
        }
```


#### Label을 사용하지 않았을 때 - 출력결과 : 0 1 2 3 0 1 2 3 0 1 2 3
```java
        for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 5; j++) {
                System.out.println(j);
                if(j == 3) {
                break;
                }
            }
        }
```

---

## continue

블록 내부에서 실행될 시, for문의 증감식 / while문의 조건식으로 이동한다.

특정 조건을 만족하는 경우 continue를 실행시켜서 그 이후의 문장을 실행하지 않고 다음 반복으로 넘어가고싶을 때 사용한다.

```java
        for (int i = 0; i < 5; i++) {
            if (i == 3) {
                continue;
            }
            System.out.println(i);
        }
```

출력결과 : 0,1,2,4