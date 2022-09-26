# java 알고리즘 문제풀이

### 220926 TIL
- 변수의 타입 확인하는 법 : .getClass()
- long타입 str로 형변환하기 : String.valueOf(long값);

- 문자열 쪼개서 하나씩 배열에 넣기 : 
String[] 배열이름= 쪼갤 문자열.split("");

- 배열 역순 정렬하기 : 
Arrays.sort(배열이름, Collections.reverseOrder());

- 제곱근 구하기 : 
double형으로 나온다.
Math.sqrt();

---

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
---

## 13. 2016년

https://school.programmers.co.kr/learn/courses/30/lessons/12901


1. 윤년 : 2월이 하루 더있는것 (2월29일)
월 중에 일수가 31일인 월과 30일인 월과 29일인 월을 구분한다.
2. 날짜에서 일을 빼서 요일을 구분한다.-> 1월1일이 금요일이니, 일주일 7에서 1을 뺀 수를 금요일로 지정
```
        String[] Day = new String[]{"SUN", "MON", "TUE", "WED", "THU", "FRI", "SAT"};
        String whatDay = "";

        int a = 1;
        int b = 31;
        if (whatDay == Day[0]) {
            System.out.println(Day[0]);
        }

        int num = 7;
        if (a == 1 || a == 3 || a == 5 || a == 7 || a == 8 || a == 10 || a == 12) {
            num = 7 - b;
            System.out.println(num);
            if (num == 6) {
                System.out.println(Day[5]);
            } else if (num == 5) {
                System.out.println(Day[6]);
            } else if (num == 4) {
                System.out.println(Day[0]);
            } else if (num == 3) {
                System.out.println(Day[2]);
            } else if (num == 2) {
                System.out.println(Day[1]);
            } else if (num == 1) {
                System.out.println(Day[2]);
            } else if (num == 0) {
                System.out.println(Day[3]);
            }
        } else if (a == 4 || a == 6 || a == 9 || a == 11) {

        } else {
            // 2월 (29일)일 때
        }
        if (b == 1) {
        }
```
7에서 b를 빼보려고 했는데.. 그러면 b가 7이 넘을때면 -값이 되어버린다.

---

## 14. 나누어 떨어지는 숫자 배열
https://school.programmers.co.kr/learn/courses/30/lessons/12910

1. for문으로 arr에 있는 값 하나씩 가져오기
2. 거기서 divisor과 나눠봐서 나머지가 0인 것 구별

```
        int[] arr = new int[] {5,9,7,10};
        int divisor = 5;
        int[] answer = new int[arr.length];

        for (int i = 0; i < arr.length; i++) {
            if(arr[i]%divisor == 0) {
                System.out.println("나누어떨어집니다");
                answer[i] = arr[i];
            } else {
                System.out.println("나누어떨어지지 않습니다");
            }
        }
        System.out.println(Arrays.toString(answer));
```
자꾸 [5,10] 처럼 나오지않고 [5,0,0,10]으로 나와서 이유를 헤맸는데, i번째를 돌면서 데이터를 넣어주다 보니까 나누어떨어지지 않더라도 i번째 자리를 채워버리게된다.

3. 그래서 count라는 변수를 하나 만들고, 나누어떨어지지 않는(값이 배열에 들어가지 않을때)때에 ++괴게하고, answer에 값을 넣을 때의 인덱스를 i-count로 했다.
4. 값이 차례대로 들어가긴 하는데, [5,10,0,0]처럼 여전히 0값이 남아있다 ㅠ.ㅠ
빈 배열을 하나 더만들어서, 길이를 유동적으로 줄일 수 있게 answer의길이-count로 만들었다.
5. 오름차순으로 배열한다.

### ArrayList를 이용하여 해결


```
import java.util.ArrayList;
import java.util.Collections;

class Solution {
    public ArrayList<Integer> solution(int[] arr, int divisor) {
        
                ArrayList<Integer> arr2 = new ArrayList<>();
        ArrayList<Integer> result = new ArrayList<>();
        int count = 0;
        
                for (int i = 0; i < arr.length; i++) {
            arr2.add(arr[i]);
        }

        for (int i =0; i < arr2.size(); i++) {
            if ( arr2.get(i)%divisor == 0) {
                result.add(arr2.get(i));
            } else {
                count ++;
            }
        }
        if (count == arr2.size()) {
            result.add(-1);
        }

        Collections.sort(result);
        System.out.println(result);
        
        return result;
    }
}
```

---

## 15. 내적
https://school.programmers.co.kr/learn/courses/30/lessons/70128

난이도 : 쉬움

1. 내적은 a와 b의 길이만큼 계속 꺼내서 곱하는것 -> a.length만큼 for문 돌리기
2. 값을 담을 변수를 만들고(result) 계속 +=

```
class Solution {
    public int solution(int[] a, int[] b) {
        int result = 0;

        for (int i = 0; i < a.length; i++) {
            result += a[i]*b[i];
        }

        return result;
    }
}
```

---

## 16. 문자열 내 p와 y의 개수

https://school.programmers.co.kr/learn/courses/30/lessons/12916

난이도 : 쉬움-중간

1. 문자열을 하나씩 보고 p와 y가 몇개인지 판별 -> arrayList로 하나씩 집어넣고, for문으로 판별
문제 : 문자열을 하나씩 잘라야함 -> sustring사용
```
        System.out.println("aaa".substring(0,1));
        System.out.println("abc".substring(1,2));
        System.out.println("abc".substring(2,3));
        
        // 즉, s.substring(i,i+1);
```
2. stringArr에서 p와 y의 개수를 세서 pNum, yNum에 각각 넣음.
3. pNum과 yNum을 비교하여 수가 같으면 true, 틀리면 false
```
import java.util.ArrayList;
class Solution {
    boolean solution(String s) {
        boolean answer = true;
        ArrayList<String> stringArr = new ArrayList<>();
        int pNum = 0;
        int yNum = 0;
        for (int i = 0; i < s.length(); i++) {
            stringArr.add(s.substring(i,i+1));

            if (stringArr.get(i).contains("p") || stringArr.get(i).contains("P")) {
                pNum++;
            } else if (stringArr.get(i).contains("y") || stringArr.get(i).contains("Y")) {
                yNum++;
            }
        }
        if (pNum == yNum) {
            answer = true;
        }else {
            answer = false;
        }
        System.out.println(answer);
        return answer;
    }
}
```
다른사람의 코드를 보니, pNum과 yNum의 크기가 같으면 +-로 0이 되니 count 변수 하나만 사용하고 count==0일때로 구분하는 것도 좋은 방법인것같다.

---

## 17. 문자열 다루기 기본

https://school.programmers.co.kr/learn/courses/30/lessons/12918

난이도 : 중간

1. 문자열을 잘라서 배열에 넣기 (16번과 비슷한듯)
2. 문자열에 문자가 있는지 확인 -> 문자열을 int로 형변환시켜서 안되는거 찾기..? 또는 0~9까지의 숫자를 모두 문자열과 비교시키기(이중for문)

```
        boolean answer = false;

        ArrayList<String> stringArr = new ArrayList<>();
        int numNum = 0;
        for (int i = 0; i < s.length(); i++) {
            stringArr.add(s.substring(i,i+1));
//            System.out.println(stringArr);

            for (int j = 0; j <= 9; j++) {
                System.out.println("j는 : " + Integer.toString(j));
                System.out.println("str는 : " + stringArr.get(i));
                if (Integer.toString(j) == stringArr.get(i)) {
                    System.out.println("숫자입니다.");
                    numNum ++;
                }
            }
        }
        System.out.println("숫자의 개수: "+numNum);
        if(numNum == s.length()) {
            answer =true;
        }

        return answer;
```
이중포문으로 0~9과 문자열을 비교했는데 0~9를 문자열로 형변환시켜줄 필요가 있었다.
그리고 문자열로 바꾼 j와 stringArr(i)가 일치하지 않는 판정이 난다..
그럼 0~9를 아예 배열로 만들어서 하나씩 꺼내보면 어떨까

3. 그렇게 해도 numNum의 숫자가 변화가 없어 '문자열 일치'를 검색해봤더니, ==로 비교하는 것이 아닌 .equals()로 비교하는 것이 있었다. 자바는 ==로 문자열을 비교할 수가 없고 .equals()를 사용해야한다고 한다.
.equals()로 문자열을 비교한 결과 잘 작동한다.
```
import java.util.ArrayList;

class Solution {
    public boolean solution(String s) {
        boolean answer = false;
        String[] numArr = new String[]{"0", "1", "2", "3", "4", "5", "6", "7", "8", "9"};
        ArrayList<String> stringArr = new ArrayList<>();
        int numNum = 0;
        for (int i = 0; i < s.length(); i++) {
            stringArr.add(s.substring(i, i + 1));
            System.out.println(stringArr);
            for (int j = 0; j < numArr.length; j++) {
                if (numArr[j].equals(stringArr.get(i))) {
                    numNum++;
                }
            }
        }
        if (numNum == s.length()) {
            answer = true;
        }

        return answer;
    }
}
```
근데 채점 결과 몇몇개가 실패가 떴다.
오잉...? 어딜 봐도 기능은 잘 작동해서 질문하기 창을 보니 길이가 4/6이 아닐 때의 처리를 해줘야한다고 한다. -> if문으로 글자 길이가 4 또는 6일때만 동작하게 했다.
```
import java.util.ArrayList;

class Solution {
    public boolean solution(String s) {
        boolean answer = false;

        ArrayList<String> stringArr = new ArrayList<>();
        int numNum = 0;

        if (s.length() == 4 || s.length() == 6) {
            for (int i = 0; i < s.length(); i++) {
                stringArr.add(s.substring(i, i + 1));
                for (int j = 0; j <= 9; j++) {
                    if (Integer.toString(j).equals(stringArr.get(i))) {
                        numNum++;
                    }
                }
            }
            if (numNum == s.length()) {
                answer = true;
            }
            System.out.println(answer);
        }
        return answer;
    }
}
```

---

## 18. 서울에서 김서방 찾기

https://school.programmers.co.kr/learn/courses/30/lessons/12919

난이도 : 쉬움

1. String 배열에 Kim 이 있는지 찾기
2. Kim의 위치 찾기
```
class Solution {
    public String solution(String[] seoul) {
        String answer = "";

       for (int i = 0; i < seoul.length; i++) {
           System.out.println(seoul[i]);
           if (seoul[i].equals("Kim")) {
               answer = "김서방은 " + i + "에 있다";
           }
       }
        return answer;
    }
}
```
if문에서 Kim을 찾았을 때 break;하는것이 좋다.

---

## 19. 수박수박수박수박수박수?

https://school.programmers.co.kr/learn/courses/30/lessons/12922

1. 홀수면 "수"나오고, 짝수면 "박"나오게 하기
2. 이것을 answer문자열에 붙이기 -> 문자열 붙이기를 처리해주는 명령어가 있지 않을까?? '자바 문자열 붙이기'를 검색해보니, concat(), append()등이 있지만, 그냥 +로 붙여도 된다고한다.. ㅋㅋㅋ!!!
3. n의 숫자만큼 반복시키기 -> if에 들어가는 조건이 n % 2 == 0 에서 i % 2 == 0 으로 변경됨!!

```
class Solution {
    public String solution(int n) {
        String answer = "";
        for (int i = 0; i < n; i++) {
            if(i % 2 == 0) {
                answer += "수";
            } else {
                answer += "박";
            }
        }
        return answer;
    }
}
```
![](https://velog.velcdn.com/images/yuns8708/post/9a02c822-bdf3-4bdf-88d3-b3713cc4ee52/image.png)  다른사람의 풀이를 보니까 이런게 있어서 진짜 웃겼다ㅜㅜㅜㅜ

---


## 20. 완주하지 못한 선수

https://school.programmers.co.kr/learn/courses/30/lessons/42576

1. participant의 값 arrayList에 넣기 / completion의 값 arrayList에 넣기

2. 두개를 비교하여 같은 값 찾기

3. 같은 값 지우기

두 개의 값이 다른것을 하나 찾아 지워주면 간단한데, 두 개의 값이 같은것을 찾는 건 쉬운데 다른것을 찾으려면 for문에서 너무 많은 데이터가 찾아져서 어렵다..

두개의 값이 같다면 num을 뽑아 arrayList에 저장하고,
.add(), .remove()를 사용하여 numArr에 있는 숫자를 인덱스로 participantArr에서 지우려고했는데 잘 안 된다.

---

## 21. 이상한 문자 만들기

https://school.programmers.co.kr/learn/courses/30/lessons/12930

난이도 : 중간-어려움

### 문자열 하나씩 쪼개서 리스트에 넣는 법
```
for (int i = 0; i < 쪼갤 문자열.length(); i++) {
쪼갠것을 넣을 arraylist.add(쪼갤 문자열.substring(i, i + 1));
}
```
이라고 생각했는데, .split()이라는 걸 알게되었다.
""을 기준으로 잘라주면 글자가 하나하나씩 잘리게된다.
```
String[] strArr = 쪼갤 문자열.split("");
```

1. 문자열 쪼개서 빈 배열 strArr에 넣기
2. 각각자리의 알파벳이 홀수인지 짝수인지 판별
3. 짝수면 대문자로(.toUpperCase()), 홀수면 소문자로(.toLowerCase()) 변환


```
import java.util.ArrayList;

class Solution {
    public String solution(String s) {
        String answer = "";

        ArrayList<String> strArr = new ArrayList<>();

        for (int i = 0; i < s.length(); i++) {
            strArr.add(s.substring(i, i+1));

            if ( i % 2 == 0 || i == 0) {
//                System.out.println(strArr.get(i) + "는 짝수번째");
                answer += strArr.get(i).toUpperCase();
            } else {
//                System.out.println(strArr.get(i) + "는 홀수번째");
                answer += strArr.get(i).toLowerCase();
            }
        }
        System.out.println(answer);

        return answer;
    }
}
```
자신 있게 제출했는데 정확성이 18.8이다..

문제를 다시 보니, 전체 문장 "hello world"에서 단어 별로 인덱스를 세야한다고 한다. (즉 "hello"와 "world"의 인덱스를 따로 세야한다.)

그렇다면 공백일 때 단어를 잘라주는 무언가가 필요할것같다.

찾아보니 .split()을 사용하면 될 것 같다.

```
        String answer = "";

        String[] strArr = s.split("");

        for (int i = 0; i < s.length(); i++) {
            if (i % 2 == 0) {
                answer += strArr[i].toUpperCase();
            } else {
                answer += strArr[i].toLowerCase();
            }
        }
        System.out.println(answer);
```

그런데 이러면 공백이 있을 때의 대처를 할 수 없다.

카운트를 받는 변수를 하나 만들고 공백일 때는 count=0 처리를 해주기로 했다.

```
import java.util.ArrayList;

class Solution {
    public String solution(String s) {
        String answer = "";

        int count = 0;

        String[] strArr = s.split("");

        for (int i = 0; i < s.length(); i++) {
            if (strArr[i].equals(" ")) {
                answer += strArr[i];
                count = 0;
            } else if (count % 2 == 0 || count == 0) {
                answer += strArr[i].toUpperCase();
                count++;
            } else {
                answer += strArr[i].toLowerCase();
                count++;
            }
        }
        System.out.println(answer);

        return answer;
    }
}
```

---

## 22. 자릿수 더하기

https://school.programmers.co.kr/learn/courses/30/lessons/12931

난이도 : 쉬움

1. 받은 숫자 문자열로 변환하기 -> Integer.toString()
2. 빈 배열을 만들고, 1번의 문자열 하나씩 쪼개서 넣기
3. 2의 배열 값들을 숫자로 변환하고, numArr에 넣기
3. 각 배열 값 더하기

```
import java.util.*;

public class Solution {
    public int solution(int n) {
        int answer = 0;

        String numStr = Integer.toString(n);
        ArrayList<String> stringArr = new ArrayList<>();
        ArrayList<Integer> numArr = new ArrayList<>();

        for (int i = 0; i < numStr.length(); i++) {
            stringArr.add(numStr.substring(i, i + 1));
            numArr.add(Integer.parseInt(stringArr.get(i)));
            answer += numArr.get(i);
        }
        return answer;
    }
}
```

---

## 23. 자연수 뒤집어 배열로 만들기

https://school.programmers.co.kr/learn/courses/30/lessons/12932

중간 - 어려움

1. n을 받아 문자열로 변환, 쪼개서 하나씩 배열에 집어넣기(split) -> 이걸 Integer.toString()로 해보려했더니 n이 long타입이어서 에러가 났다. 찾아보니 String.valueOf()란걸 쓰면 된다고 한다.
2. 순서 바꾸기 -> 어떻게 인덱스 번호를 뒤집을것인가 많이 고민했다. 이중 for문으로 해보다가 그냥 for문으로 strArr의 길이-1에서 시작해서, 0이 될 때까지 --해주면 된다는 걸 깨달았다.

```
import java.util.ArrayList;

class Solution {
    public ArrayList<Integer> solution(long n) {
        
        ArrayList<Integer> result = new ArrayList<>();

        String numStr = String.valueOf(n);
        String[] strArr = numStr.split("");
        
        for (int j = strArr.length-1; j >= 0; j--) {
            result.add(Integer.parseInt(strArr[j]));
        }


        return result;
    }
}
```

---

## 24. 정수 내림차순으로 배치하기

https://school.programmers.co.kr/learn/courses/30/lessons/12933

1. 정수 n 문자열로 변환시켜 쪼개서 배열에 넣기 -> String.valueOf(n).split("")
2. 배열에서 내림차순 배치 -> Arrays.sort(strArr, Collections.reverseOrder());
3. temp 빈 문자열을 만들고, 배열에서 하나씩 꺼내서 붙이기
4. temp를 숫자로 형변환 -> 런타임 에러 : int말고 long으로 변환해야함!! Long.parseLong()

```
import java.util.Arrays;
import java.util.Collections;

class Solution {
    public long solution(long n) {
        long answer = 0;
        String temp = "";

        String[] strArr = String.valueOf(n).split("");
        for (int i = 0; i < strArr.length; i++) {
            System.out.println(strArr[i]);
        }

        Arrays.sort(strArr, Collections.reverseOrder());
        System.out.println(strArr[0]);
        for (int i = 0; i < strArr.length; i++) {
            temp += strArr[i];
        }

        answer = Long.parseLong(temp);

        return answer;
    }
}
```

---

## 25. 정수 제곱근 판별

https://school.programmers.co.kr/learn/courses/30/lessons/12934

난이도 : 중간

1. ........ 아무리 생각해도 잘 모르겠다.
2. '자바 제곱근'을 검색해보니, 제곱근을 구하는 메소드가 있다고한다. -> Math.sqrt()
3. 그렇다면 n의 제곱근 값인 square을 곱한 결과가 같은지 판별해준다.
4. 조건을 만족하면 answer = (square+1) * (square+1), 만족하지 않으면 answer = -1 -> 여기서, double과 long간의 형변환을 해야한다. (int)를 앞에 붙여줌

```
class Solution {
    public long solution(long n) {
        long answer = 0;

        double square = Math.sqrt(n);

        if(square * square == n) {
            answer = (int)(square+1) * (int)(square+1);
        } else {
            answer = -1;
        }
        System.out.println(answer);

        return answer;
    }
}
```

채점 결과 정확성 44.4......
아마 그냥 int로 바꿔주고 long타입이 아니어서 그런듯하다
이렇게 되면 double -> int -> long 이렇게 두번 바꿔치기 해주면 어떨까

```
        double square = Math.sqrt(n);
        int intSquare = (int)Math.sqrt(n);
        long longSquare = (long) (int) Math.sqrt(n);
```

삼단 변신 후
채점도 무사히 통과했다!!

```
class Solution {
    public long solution(long n) {
        long answer = 0;
        
        long longSquare = (long) (int) Math.sqrt(n);

        if(longSquare * longSquare == n) {
            answer = (longSquare+1) * (longSquare+1);
        } else {
            answer = -1;
        }
        System.out.println(answer);

        return answer;
    }
}
```

---

## 26. 제일 작은 수 제거하기

https://school.programmers.co.kr/learn/courses/30/lessons/12935

난이도 : 어려움

1. 배열 오름차순 정렬 -> Collections.sort()
2. 0번째 인덱스의 값 삭제 -> intArr.remove(0)
3. intArr의 size가 0이면, .add(-1)

```
class Solution {
    public ArrayList<Integer> solution(int[] arr) {
        ArrayList<Integer> intArr = new ArrayList<>();

        // 받은 배열에서 하나씩 꺼내서 arraylist에 넣기
        for (int i = 0; i < arr.length; i++) {
            intArr.add(arr[i]);
        }
        // 오름차순 정렬
        Collections.sort(intArr);
        
        // 0번째 인덱스 값 삭제하기
        intArr.remove(0);


        if (intArr.size() == 0) {
            intArr.add(-1);
        }

        return intArr;
    }
}
```
그런데 . . 문제가 있다.
![](https://velog.velcdn.com/images/yuns8708/post/60617089-a754-4101-95ea-27c31845a8be/image.png)


아예 오름차순 정렬을 하는게 아니라 원래의 배열 순서를 유지하면서 가장 작은 수를 지우는거였다.

그렇다면..
배열을 다 돌면서 두개의 숫자를 비교하고 나중에 가장 작은 수를 지우면?

1. 배열을 돌며 값 하나씩 꺼내오기
2. 이중for문으로 두개의 값 비교하기
3. 가장 작은 값의 인덱스를 변수에 저장해서 remove하기

```
import java.util.ArrayList;
import java.util.Collections;


class Solution {
    public ArrayList<Integer> solution(int[] arr) {
        ArrayList<Integer> intArr = new ArrayList<>();
        ArrayList<Integer> answer = new ArrayList<>();
        int smallNum = 0;

        // 받은 배열에서 하나씩 꺼내서 arraylist에 넣기
        for (int i = 0; i < arr.length; i++) {
            intArr.add(arr[i]);
        }

        for (int i = 0; i < intArr.size(); i++) {
            for (int j = 0; j < intArr.size(); j++) {
                if(intArr.get(i) > intArr.get(j)) {
                    smallNum = j;
                }
            }
        }

        intArr.remove(smallNum);
        
                if (intArr.size() == 0) {
            intArr.add(-1);
        }

        return intArr;
    }
}
```

![](https://velog.velcdn.com/images/yuns8708/post/c310d9db-0a55-4da0-b7dc-d56c71b76266/image.png)

..? ㅋㅋㅋ 정확성이 6.3이다..
println으로 다양한 값을 넣어보며 실험해봤더니, 
{-1,5,10,6}처럼 -값이 들어가있는 경우엔 -값을 지우지 않고 5를 지운다..

작은 수를 판별할 수 있는 방법은?

1. sort()로 가장 작은 수를 판별한다. 여기에서 원래 배열의 순서가 흐트러지면 안되기때문에 temp배열을 만들어 arr값을 넣어서 사용한다.
2. 가장 작은 값을 smallNum에 담고, arr의 각 값과 비교하여 아닌 값들만 배열에 넣는다.

```
import java.util.ArrayList;
import java.util.Collections;

class Solution {
    public ArrayList<Integer> solution(int[] arr) {
        ArrayList<Integer> answer = new ArrayList<>();

        if (arr.length == 1) {
            answer.add(-1);
            System.out.println(answer);
        } else {
            ArrayList<Integer> temp = new ArrayList<>();
            for (int i = 0; i < arr.length; i++) {
                temp.add(arr[i]);
            }
            Collections.sort(temp);
            int smallNum = temp.get(0);

            for (int i = 0; i < arr.length; i++) {
                if(arr[i] != smallNum) {
                    answer.add(arr[i]);
                }
            }
        }
        return answer;
    }
}
```