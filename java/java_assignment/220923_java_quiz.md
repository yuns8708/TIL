## 문제1

- 다음 코드를 실행하면 출력 결과로 5를 기대했는데 4가 출력되었습니다. 어디에서 잘못 작성된 것일까요?
  ```java
  int var1=5;
  int var2=2;
  double var3=var1/var2;
  int var4=(int)(var3*var2);
  System.out.println(var4);
  ```

### 해결과정
1. var1은 5, var2는 2이고, var3는 var1에서 var2를 나눈 값이다. 출력 결과는 2.0
2. var3 * var2 = 2.0 * 2
여기서 궁금한 것은 (int)를 왜 사용하는걸까?
![](https://velog.velcdn.com/images/yuns8708/post/243d0d7a-5297-4998-9f73-c01ad9492a38/image.png)
그래서 int가 없도록 해봤더니 오류가 난다. double의 값이어서 int로 변환해주는것이었다.
3. 문제가 이해가 잘 안됐었는데, 잘 생각해보니 5에서 2를 나누면 2.5일텐데?! 2가 나왔다.
4. 'java 소수점 출력'을 검색해서 글들을 보니, 소수점이 나오게하려면 나누는 값들도 double이어야한다.

### 답안
int타입을 double타입으로 수정한다.
```
        double var1 = 5;
        double var2 = 2;
        double var3 = var1/var2;
        int var4 = (int)(var3*var2);
        System.out.println("결과");
        System.out.println(var4);
```

---

## 문제2

- 다음 코드를 실행했을 때 출력 결과는 무엇입니까? (증감연산자에 대해 알아보세요!)

  ```
  int x=10;
  int y=20;
  int z = (++x) + (y--);
  System.out.println(z);
  ```

### 해결과정

#### 증감연산자란?
피연산자(연산자를 연산하기 위해 필요한 다른 값)을 1씩 증가/감소 시킨다.

> ++x : x를 먼저 +1증가시킨 후 그 값을 사용
> --x : x를 먼저 -1감소시킨 후 그 값을 사용
> x++ : x를 먼저 사용한 후 1증가
> x-- : x를 먼저 사용한 후 1감소

z는 10에 1을 증가시킨 후 값을 사용한다. == 11
y는 20을 먼저 사용한 후, 1을 감소시킨다 == 즉 z를 위한 연산을 먼저 진행한 후, 1을 뺀다. == 20
11 + 20 = 31
y는 이 연산 이후에 19가 된다.
![](https://velog.velcdn.com/images/yuns8708/post/9e4fea63-4bff-48da-a8b1-96d8ac7a5a87/image.png)
출력결과



### 답안
출력결과는 31입니다.

---

## 문제3
- while문과 Math.random() 메소드를 이용해서 2개의 주사위를 던졌을 때 나오는 눈을 (눈1, 눈2) 형태로 출력하고, 눈의 합이 5가 아니면 계속 주사위를 던지고, 눈의 합이 5이면 실행을 멈추는 코드를 작성해보세요. 눈의 합이 5가 되는 조합은 (1,4), (4,1), (2,3), (3,2)입니다.


### 해결과정

1. 랜덤메소드 사용법 알아내기
Math.random()은 double형으로 0.0이상 1.0미만 사이의 값을 반환하는 함수이다.
0.21315313....같이 나오기때문에 정수를 원하는 우리는 여기에 수를 곱해주고, 소수점 부분을 버려야한다.
  ```
          // Math.random() 출력
          System.out.println(Math.random());
          // 소수점 위로 숫자 출력
          System.out.println(Math.random() * 10);
          // 소수점 아래 버리기
          System.out.println((int)(Math.random() * 10));
  ```
  소수점 아래까지 버렸으면 0~9까지의 숫자가 출력
  > (int)(Math.random() * a + b)
   b에서 a까지의 랜덤 수 반환
2. 주사위 출력하기
1~6까지의 랜덤 숫자를 담을 변수를 만든다.
  ```
          int dice1 = (int)(Math.random() * 6 + 1);
          int dice2 = (int)(Math.random() * 6 + 1);
  ```
3. 조건문으로 눈의 합이 5일때 맞추기
  ```
          if (dice1 + dice2 == 5) {
              System.out.println("주사위의 합은 : " + (dice1 + dice2));
          }
  ```
4. while문으로 계속 돌리고, 합이 5이면 빠져나오기
조건이 true일 경우 무한반복, break문으로 빠져나오기
  ```
          while(true) {
              if (dice1 + dice2 == 5) {
                  System.out.println("주사위의 합은 : " + (dice1 + dice2));
                  break;
              }
          }
  ```
  

### 오류 해결
계속 실행시켜도 '주사위의 합은 5' 라는게 안나왔다.
생각해보니 계속 새로운 랜덤 값을 가져오면서 바뀌려면 dice1 dice2의 값이 while 안에 있어야한다.


### 답안
```
        while (true) {
            int dice1 = (int) (Math.random() * 6 + 1);
            int dice2 = (int) (Math.random() * 6 + 1);
            if (dice1 + dice2 == 5) {
                System.out.println("주사위의 합은 : " + (dice1 + dice2));
                break;
            }
        }
```

---
### IntelliJ 자동 줄맞춤
> ctrl + alr + L
