# java 알고리즘 문제풀이


## 1. 직사각형 별찍기

https://school.programmers.co.kr/learn/courses/30/lessons/12969

난이도 : 쉬움

1. 문제 코드 이해하기
sc.nextInt()는 입력값(숫자)를 받아내는 코드이다. 입력값이 5, 3이기 때문에 int a = 5, int b = 3 이다.
2. 별 5개 찍기
for문으로 a만큼의 별이 출력되게함
3. 3줄 만들기
println()은 줄바꿈임을 이용하여 5개가 찍힌 후마다 줄이 바뀌도록 함

```
        Scanner sc = new Scanner(System.in);
        int a = sc.nextInt();
        int b = sc.nextInt();

        String star = "*";
        for (int i = 0; i < b; i++) {
            for (int j = 0; j < a; j++) {
                System.out.print(star);
            }
            System.out.println();
```
---
## 2. 짝수와 홀수

https://school.programmers.co.kr/learn/courses/30/lessons/12937

난이도 : 쉬움

1. 문제 코드 이해하기
public String solution(int num)
이것을 보니 매개변수를 숫자로 받아 함수 안에서 짝홀 구분을 하여 Odd/Even 문자열을 반환하는것 같은데, java의 함수 다루는 법을 알아봐야겠다.

2. 출력까지 해야하는줄알았는데, 함수만 완성하면 되는거였다.

```
class Solution {
    public String solution(int num) {
        String answer = "";
        if (num % 2 == 0) {
            answer = "Even";
        } else {
            answer = "Odd";
        }
        return answer;
    }
}
```
--- 
## 3. 가운데 글자 가져오기

https://school.programmers.co.kr/learn/courses/30/lessons/12903

난이도 : 어려움

1. 단어의 길이 구하기 -> .length()
2. 단어의 길이가 짝수인지 홀수인지 구분 -> if문 2로 나눈 나머지
3. 단어 자르기 -> 단어의 길이 알아야함, 자르기 함수 (substr())
4. 또다른문제 : 단어가 2글자 이하이면, -1값이 들어가게됨 - if문으로 제어

```
        String str = "asdfㅁㄴㅇㄴㅁㅇ";
        if (str.length() > 2) {
            if (str.length() % 2 == 0) {
            System.out.println(str.substring(str.length()-3,str.length()-1));
                System.out.println("짝수");
            } else {
                System.out.println("홀수");
                System.out.println(str.substring(str.length() - 2, str.length() - 1));
            }
        } else {
            System.out.println(str);
        }
```
그래서 위의 코드처럼 했는데, 문제는 길이가 4,3일때만 작동한다. 특정 수를 빼는게 아니라 문자의 길이를 이용해서 다른 길이의 문자마다 다른 숫자가 연산되게 해야한다고 생각했다.

5. 
```
        String str = "12345";
        if (str.length() % 2 == 0) {
            System.out.println(str.substring(str.length() - (str.length() / 2 + 1), str.length() - (str.length() / 2 - 1)));
            System.out.println("짝수");
        } else {
            System.out.println("홀수");
            System.out.println(str.substring(str.length() - (str.length() / 2 + 1), str.length() - (str.length() / 2)));
        }
```
6. 이것을 solution메소드에 넣을때도 문제가 됐다. 변수 할당을 잘못해줬거나 필요한 부분을 실수로 지우는 등
```
class Solution {
    public String solution(String s) {
        String answer = "";
        if (s.length() % 2 == 0) {
            answer = s.substring(s.length() - (s.length() / 2 + 1), s.length() - (s.length() / 2 - 1));
        } else {
            answer = s.substring(s.length() - (s.length() / 2 + 1), s.length() - (s.length() / 2));
        }
        return answer;
    }
}
```

---

## 4. 두 정수 사이의 합

https://school.programmers.co.kr/learn/courses/30/lessons/12912

난이도 : 보통

1. a가 b의 수가 될 때까지 1더하기 (for)
그런데, 1을 처음부터 더하다보니까 a가 1이 더해진상태로 시작하게된다. 그래서 아예 a를 -1시킨 변수를 만듦
2. 출력된 숫자 모두 더하기 (temp)

```
class Solution {
    public long solution(int a, int b) {
        long answer = 0;
        int sum = a - 1;

        for (int i = sum; i < b; i++) {
            int c = sum += 1;
            System.out.println(c);
            answer += c;
        }
        return answer;
    }
}
```
3. 문제발생 : a가 더 큰 수일때에는 에러 발생 -> 둘 중 어느것이 더 큰 수인지 판별할 필요 있음
```
class SumTotal {
    public long solution(int a, int b) {
        int answer = 0;
        int sum1 = a - 1;
        int sum2 = b - 1;

        if (a > b) {
            for (int i = sum2; i < a; i++) {
                int c = sum2 += 1;
                answer += c;
            }
        } else if (b > a) {
            for (int i = sum1; i < b; i++) {
                int c = sum1 += 1;
                answer += c;
            }
        } else {
            answer = a;
        }
        return answer;
    }
}
```
---

## 5. 문자열을 정수로 바꾸기
https://school.programmers.co.kr/learn/courses/30/lessons/12925

난이도 : 쉬움-보통

1. 문자열을 정수로 바꾸는 법 : Integer.parseInt()
2. 부호가 들어가있는지 확인하기 (if문, contains())
3. 부호가 있으면, 앞의 글자 잘라내고 정수 변환 -> substring()을 사용하는데, 끝나는 지점을 글자의 수만큼 해야함(가변성) (.length()이용)
4. 오잉?? 문제를 -, +를 떼고 출력하는것으로 알았는데 붙여서 출력하는거였다.
근데... parseInt가 -와 +도 인식해서 변환해준다...?!

```
class Solution {
    public int solution(String s) {
        int answer = 0;
        
        answer = Integer.parseInt(s);
        
        return answer;
    }
}
```
그럼 답안이 이렇게 된다.
아래는 3번까지(-, + 떼고 출력하기) 풀었던것
```
class Solution {
    public int solution(String s) {
        int answer = 0;
        
        answer = Integer.parseInt(s);
        if (s.contains("-") || s.contains("+")) {
            answer = Integer.parseInt(s);
        } else {
            answer = Integer.parseInt(s);
        }
        
        return answer;
    }
}
```
다른사람들의 해설을 보니까 함수를 쓰지 않고 알고리즘으로 풀이하는 방법이 있는듯하다.

---

# 6. 없는 숫자 더하기

https://school.programmers.co.kr/learn/courses/30/lessons/86051

난이도 : 중간

1. 1~10까지의 숫자 불러오기 (for)
2. numbers에 없는 숫자 판별하기 (if문으로 for문의 i와 numbers의 특정 인덱스가 같지 않을 때)
```
        for (int i = 0; i < arr.length; i++) {
            System.out.println(i);
            if (i != arr[i]) {
                
            }
        }
```
이라고 생각했는데, arr의 i번이 다른 자리에 있다면 일치하지 않는 취급을 하기 때문에 안된다.
그럼 for문이 한 번 돌 동안 arr[i]에 있는 모든 수를 한번씩 돌면서 꺼내서 비교해야하지 않을까?

3. 찾은 숫자 더하기
인데 숫자가 같을때는 한번만 찍히는데, 다를때는 여러번 찍히기때문에 값을 연산하기 어려웠다. 그래서 그냥 같을때의 수를 다 구해서 더하고 그것을 1-9까지 더한 값에서 빼는 방법을 사용했다.

```
class Solution {
    public int solution(int[] numbers) {
        int answer = 0;
        for (int i = 0; i < 10; i++) {
            for (int j = 0; j < numbers.length; j++) {
                if ( i == numbers[j]) {
                    answer += numbers[j];
                }
            }
        }
        answer = 45 - answer;
        return answer;
    }
}
```

// 두번째 방법
배열의 숫자를 다 더하고 1-9까지 더한값에서 뺌
```
class Solution {
    public int solution(int[] numbers) {
        int answer = 0;
        int sum = 0;
        for (int i = 0; i < numbers.length; i++) {
            answer = 45 - (sum += numbers[i]);
        }
        return answer;
    }
}
```
---

# 7. 음양 더하기
https://school.programmers.co.kr/learn/courses/30/lessons/76501

난이도 : 쉬움

문제를 처음 보고...
이게 무슨 소리인거지
이런 생각을 했다

절댓값을 찾아보니 0에서 그 수까지의 거리라고한다. -4도 될수있고, 4도 될수있고 그런 식이다.

그리고 보니까 입력값이 정해져있다. 이 입력값들을 함수 안에서 양수이면 더하고, 음수이면 빼라는 뜻인것같다.

1. absolutes의 값을 하나씩 불러온다. -> for
2. 그 값이 true인지 false인지 구분한다 -> if
3. true면 더해주고, false면 뺀다
```
class Solution {
    public int solution(int[] absolutes, boolean[] signs) {
                        int answer = 0;
        for (int i = 0; i < absolutes.length; i++) {
            if (signs[i] == true) {
                answer += absolutes[i];
            } else {
                answer -= absolutes[i];
            }
        }
        return answer;
    }
}
```

# 8. 평균 구하기
https://school.programmers.co.kr/learn/courses/30/lessons/12944

난이도 : 쉬움

1. 받은 수의 값 가져오기 -> for문
2. 값을 모두 더하기 -> +-
3. 배열의 길이만큼 나누기 -> arr.length()
```
class Solution {
    public double solution(int[] arr) {
        double answer = 0;
        for(int i = 0; i < arr.length; i++) {
            answer += arr[i];
        }
        answer /= arr.length;
        return answer;
    }
}
```

---

# 9. 핸드폰 번호 가리기
https://school.programmers.co.kr/learn/courses/30/lessons/12948

난이도 : 쉬움-중간

1. 전화번호 뒤 네자리 구하기 -> substring과 length()를 이용해서 시작하곳을 length()-4 / 끝나는곳을 length()로 하면 어떨까
2. 나머지를 *로 처리하기 -> length()-4 길이만큼 *을 생성해서 붙이고, 그것에 다시 phonNum을 붙임

```
class Solution {
    public String solution(String phone_number) {
        String answer = "";
        String phoneNum = phone_number.substring(phone_number.length() - 4, phone_number.length());

        for (int i = 0; i < phone_number.length() - 4; i++) {
            answer += "*";
        }
        answer += phoneNum;
        return answer;
    }
}
```

---

# 10. 행렬의 덧셈
https://school.programmers.co.kr/learn/courses/30/lessons/12950

난이도 : 어려움

1. arr1의 i번째와 arr2의 i번째 더하기
2. 그런데, arr의 길이가 가변이기 때문에 length()로 길이 구하기
3. 그런데...!! 자세히 보니 배열 안에 배열이 있는거같다. 아래와 같은 구조이다.
```
        int[][] arr1 = new int[][]{{1,2},{2,3}};
        System.out.println(arr1[0][1]); // 출력결과 : 2

        // 꺼낼때 : for안에 for넣기
        for (int i = 0; i < arr1.length; i++) {
            for (int j = 0; j < arr1.length; j++) {
                System.out.println(arr1[i][j]);
            }
        }
```

4. 그렇다면, 같은 행, 같은 열의 값을 더하려면 
arr1[0][0] + arr2[0][0]
arr1[0][1] + arr2[0][1]
arr1[1][0] + arr2[1][0]
arr1[1][1] + arr2[1][1]

```
        // 꺼낼때 : for안에 for넣기
        for (int i = 0; i < arr1.length; i++) {
            for (int j = 0; j < arr1.length; j++) {
                System.out.println(i + "arr1의" + j + "번째:" + arr1[i][j] + "//arr2의" + j + "번째 :" + arr2[i][j]);
            }
        }
```

오류 : answer배열을 아래처럼 선언, 초기화시키려했는데, 값이 안들어가있으면 오류가 나는 모양이다.

```
int[][] answer = new int[][]{};
```
5. 그래서 answer의 길이를 arr1의 길이로 설정하기로 했다

```
class Solution {
    public int[][] solution(int[][] arr1, int[][] arr2) {
        int[][] answer = new int[arr1.length][arr1[0].length];
        for (int i = 0; i < arr1.length; i++) {
            for (int j = 0; j < arr1[i].length; j++) {
                answer[i][j] = arr1[i][j] + arr2[i][j];
            }
        }
        return answer;
    }
}
```
---

# 11. x만큼 간격이 있는 n개의 숫자

https://school.programmers.co.kr/learn/courses/30/lessons/12954

난이도 : 중간

1. x부터 시작해 n개까지의 x만큼 증가하는 반복문 만들기 -> (for int i = 0; ??? ; i += x) 
2. 다른건 다 하겠는데 n까지가 아닌 n개까지를 어떻게 꺼내는건지 모르겠다. 
```
        int x = 2;
        int n = 5;
        int sum = 0;
        for (int j = 0; j < n; j++) {
//            System.out.println(j);
            for (int i = 0; i <= n; i += x) {
                if (sum <= n*x) {
                    System.out.println(sum += x);
                }
            }
        }
```
이런걸 생각해보다가..
3. 잘 생각해보니 그냥 n까지 for을 돌린 뒤에 그만큼 x에 x를 더해주면 되는것이었다
```
class Solution {
    public long[] solution(int x, int n) {
        long[] answer = {};
        int sum = 0;
        for (int i = 0; i < n; i++) {
            int temp = sum += x;
            answer[i] = temp;
            System.out.println(temp);
        }
        return answer;
    }
}
```
이게 맞는거같은데, 오류가 난다.
answer한테 무슨 문제가있는것같다. 위에서도 비슷한 문제를 겪었던 것이 생각나서, 초기화 시 배열의 길이를 지정해주는걸로 해결해봤다.

```
class Solution {
    public long[] solution(int x, int n) {
        long[] answer = new long[n];
        int sum = 0;
        for (int i = 0; i < n; i++) {
            answer[i] = sum += x;
        }
        return answer;
    }
}
```
![](https://velog.velcdn.com/images/yuns8708/post/78c6cad4-b1f7-463d-9843-65edfbcd09db/image.png)

처음으로 채점에서 실패가 떴다. 도무지 모르겠어서 찾아보니 sum의 타입 문제였다.

```
class Solution {
    public long[] solution(int x, int n) {
        long[] answer = new long[n];
        long sum = 0;
        for (int i = 0; i < n; i++) {
            answer[i] = sum += x;
        }
        return answer;
    }
}
```

---

## 12. 부족한 금액 계산하기
https://school.programmers.co.kr/learn/courses/30/lessons/82612

다른분들의 코드로 클래스 함수를 실행시키는 법을 알게되었다
```
class quiz12 {
    public long quiz12(int price, int money, int count) {
        long answer = -1;
        return answer;
    }

    public static void  main(String[] args){
        quiz12 q12 = new quiz12();
        System.out.println(q12.quiz12(3,20,4));
    }
}
```

1. count번 타게 되면 price가 얼마나 필요한지 계산 -> for문으로 count번을 돌리고, 안에서 num + 1 을 계속 price와 곱해줌
2. money가 필요한 요금보다 적을 시 필요한 요금에서 money를 빼줌, money가 같거나 더 크면 0

```
class quiz12 {
    public long quiz12(int price, int money, int count) {
        long answer = 0;
        int num = 0;
        for (int i = 1; i <= count; i++) {
            answer += price * (num+i);
        }
        if (money < answer) {
            answer = answer - money;
        } else {
            answer = 0;
        }
        return answer;
    }

    public static void  main(String[] args){
        quiz12 q12 = new quiz12();
        System.out.println(q12.quiz12(3,20,4));
    }
}
```
