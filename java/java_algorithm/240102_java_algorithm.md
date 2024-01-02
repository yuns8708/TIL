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