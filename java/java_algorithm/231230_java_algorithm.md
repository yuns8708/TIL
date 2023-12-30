# 크기가 작은 부분 문자열
https://school.programmers.co.kr/learn/courses/30/lessons/147355

1. t 문자열을 잘라 arr 배열에 넣는다.
2. arr 배열을 돌면서, 임시 문자열인 temp에 arr의 문자열을 하나씩 넣어 p의 길이만큼이 되게 한다.
3. 문자열 temp와 p를 int로 전환하고, 크기를 비교하여 작거나 같으면 answer을 증가시킨다.

```java
        for (int i = 0; i < arr.length; i++) {
            String temp = "";
            for (int j = 0; j < p.length(); j++) {
                temp += arr[j];
                System.out.println(temp);
                // 문자열 숫자로 바꾸기
                int tempNum = Integer.parseInt(temp);
                int pNum = Integer.parseInt(p);
                if (tempNum <= pNum ) {
                    count++;
                }
            }
        }
```
2번을 구현할 때 처음 작성한 코드

temp에 arr의 j번째를 넣었는데, 그렇게 하니 0,1,2 / 0,1,2 / 0,1,2 이렇게 똑같이 도는 것을 확인했다.

내가 원하는 것은 0,1,2 / 1,2,3 / 2,3,4 .. 이기 때문에, j 에 i 를 더하는 것으로 고쳤는데, 그렇게 하면 j의 숫자가 arr의 배열 길이를 넘어버려 오류가 나온다.

for문에서 i의 길이를 arr.length - p.length() + 1로 만들어, j의 길이가 넘어가지 않도록 했다.

---

```java
public class Solution {
    public int solution(String t, String p) {
        int answer = 0;
        // t 문자열 잘라서 배열에 넣기
        String[] arr = t.split("");

        // p의 길이만큼 임시 문자열 temp 만들기
        for (int i = 0; i < arr.length - p.length()+1; i++) {
            String temp = "";
            for (int j = 0; j < p.length(); j++) {
                temp += arr[j + i];
                System.out.println(temp);
            }
            // 문자열 숫자로 바꾸기
            int tempNum = Integer.parseInt(temp);
            int pNum = Integer.parseInt(p);
            // 크기 비교
            if (tempNum <= pNum ) {
                answer++;
            }
        }
        System.out.println(answer);

        return answer;
    }
}
```