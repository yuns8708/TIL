# 가장 가까운 같은 글자
https://school.programmers.co.kr/learn/courses/30/lessons/142086?language=java

고민한 부분은, j반복문을 돌 때 현재 글자 위치와 가장 같은 부분만 골라내는 것이었다.
(banana에서 마지막 a는 첫번째 a가 아닌 2번째 a만을 선택해야한다.)
그래서 원래 0부터 시작해서 ++였던 j 반복문을 반대로 조건붙여주었다.

그리고 배열에 값을 집어넣을 때 arraylist로 add하려고했는데, 그냥 answer[0]처럼 위치를 지정해서 넣어주기만 하면 된다.

```java
public class Solution {
    public int[] solution(String s) {
        int[] answer = new int[s.length()];
        // s 문자열을 잘라 arr 배열에 넣는다
        String[] arr = s.split("");
        // for문으로 돌면서 앞의 글자와 비교
        for (int i = 0; i < arr.length; i++) {
            // 첫번째 글자면 -1 추가
            if (i == 0) {
                answer[i] = -1;
            } else {
                for (int j = i - 1; j >= 0; j--) {
                    // 앞의 글자와 같을 때
                    if (arr[i].equals(arr[j])) {
                        answer[i] = i - j;
                        break;
                    }
                    // 다를 때
                    if (!arr[i].equals(arr[j])) {
                        answer[i] = -1;
                    }
                }
            }
        }
        return answer;
    }
}
```

--- 
## 개선 답안

### charAt(), indexOf()

```java
        String str = "가나다라";
        char c = str.charAt(0);
        System.out.println(c); // 출력값 : 가
```

charAt()은 String타입의 문자열에서 해당 index의 한 글자만을 가져올 수 있다.

```java
        String str = "apple";

        // 앞에서부터 찾기
        System.out.println(str.indexOf("e")); // 출력값 : 4
        System.out.println(str.indexOf("p")); // 출력값 : 1

        // 뒤에서부터 찾기
        System.out.println(str.lastIndexOf("p")); // 출력값 : 2
```

indexOf()는 해당 글자가 문자열의 앞에서부터 몇 번째인지 출력한다.

lastIndexOf()는 뒤에서부터 찾는다.



이것을 이용하여 아래처럼 개선해보았다.

이 방법 또한 현재 글자에서 가장 가까운 글자를 찾는 방법에 대해 가장 고민했다.

1. charAt()으로 현재 반복문의 글자를 찾는다.
2. substring()으로 현재 글자의 바로 앞까지의 문자열을 만들어, 
3. 그 뒤에서부터 찾아(lastIndexOf()) 같은 글자가 있는지 확인한다.
4. 없으면(-1이 나옴) answer에 -1을 넣고,
5. 있으면 (-1이 아닐 때) answer에 (현재 글자 위치 - 마지막 글자 위치)의 수를 넣는다.

```java
public class Solution {
    public int[] solution(String s) {
        int[] answer = new int[s.length()];

        for (int i = 0; i < s.length(); i++) {
            // s에서 각각 글자를 떼어낸 것에서 현재 글자
            char sChar = s.charAt(i);

            // 현재 글자의 바로 앞까지 잘라서 문자열 만들기
            String subStr = s.substring(0,i);

            // 현재 글자와 substr의 글자 중 뒤에서 찾아서 같은 글자 있는지
            // 만약 없다면, -1이 나옴
//            System.out.println(subStr.lastIndexOf(sChar));

            if(subStr.lastIndexOf(sChar) == -1) {
                // 같은 글자가 없을 때 (-1나올 때), answer은 -1
                answer[i] = -1;
            } else {
                // 같은 글자가 있을 때, answer은 현재 글자 (i번째)위치 - subStr의 뒤에서부터 같은 글자의 위치
                answer[i] = i - subStr.lastIndexOf(sChar);
            }
        }
        return answer;
    }
```


