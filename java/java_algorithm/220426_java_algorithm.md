# 과일 장수
https://school.programmers.co.kr/learn/courses/30/lessons/135808

1. 사과들의 점수 중 높은 순으로 배열한다 (내림차순)
    - Arrays.sort(score, Collections.reverseOrder());를 사용했으나, sort(오름차순)만 되고 reverse가 적용되지 않는 오류 -> int에서는 적용할 수 없기 때문에 Integer[]로 변수를 선언해야한다.
2. 상자 단위로만 팔기 때문에 m의 배수를 구하는데, 가장 낮은 점수 x m이 가격이니까 배수 묶음 중 가장 뒤에 있는 수, 즉 배수로 나눴을 때 나머지가 0인 수와 m을 곱해주면 된다.

```java
import java.util.*;

public class Solution {
    public int solution(int k, int m, Integer[] score) {
        Arrays.sort(score);
        Arrays.sort(score, Collections.reverseOrder());
        int answer = 0;

        for (int i = 0; i < score.length; i++) {
            if((i+1) % m == 0) {
                answer += score[i] * m ;
            }
        }
        return answer;
    }
}

```
처음 작성한 코드

인데 인텔리제이에서는 실행되지만, 프로그래머스에서 작동하지 않았다.

score의 타입을 건드리는 방법으로는 안되는듯하다.

'int 배열 integer 변환'을 검색하여, 배열 타입 변환 방법을 찾았다.
```
Integer[] scoreArr = Arrays.stream(score).boxed().toArray(Integer[]::new);
```

```java
import java.util.*;

public class Solution {
   public int solution(int k, int m, int[] score) {
      int answer = 0;

      // int -> Integer
      Integer[] scoreArr = Arrays.stream(score).boxed().toArray(Integer[]::new);
      // reverse
      Arrays.sort(scoreArr, Collections.reverseOrder());

      for (int i = 0; i < score.length; i++) {
         if((i+1) % m == 0) {
            answer += scoreArr[i] * m ;
         }
      }
      return answer;
   }
}
```