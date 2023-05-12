# K번째수
https://school.programmers.co.kr/learn/courses/30/lessons/42748

1. commands의 길이만큼 반복문을 돌면서, copyOfRange를 이용해 자른 배열을 sortedArr에 넣는다. (array를 기준으로, commands의 i번째의 0번째 - 1(문제에서 지정한 i번째)에서 시작하여 commands의 i번째의 1번째(문제에서 지정한 j번째)까지 자른다.)
2. sortedArr을 arrays.sort로 정렬한다
3. numArr이라는 arrayList에 commands의 i번째의 k번째 숫자를 넣도록 한다.

```java
import java.util.ArrayList;
import java.util.Arrays;

public class Solution {
    public int[] solution(int[] array, int[][] commands) {
        int[] answer = {};

        ArrayList<Integer> numArr = new ArrayList();

        for (int i = 0; i < commands.length; i++) {
            int[] sortedArr = Arrays.copyOfRange(array,commands[i][0] - 1,commands[i][1]);
            Arrays.sort(sortedArr);
            System.out.println(Arrays.toString(sortedArr));
            numArr.add(sortedArr[commands[i][2] - 1]);
        }

        for (int i = 0; i < numArr.size(); i++) {
            System.out.println(numArr.get(i));
        }

        return answer;
    }
}
```

구하는 법은 다 나왔는데, answer이라는 정해진 배열에 각각의 값들을 어떻게 집어넣는지에 대해 헤맸다.

'자바 ArrayList array'를 검색해 arrayList를 배열로 변환하는 법을 찾아봤다.

### ArrayList -> 배열 변환

```java
        int[] answer = new int[numArr.size()];
        int size = 0;
        for (int temp:numArr
        ) {
            answer[size++] = temp;
        }
```
1. answer이라는 int 배열을 만들 때 길이를 원하는 ArrayList의 size로 지정한다
2. numArr을 돌면서 answer의 0번째, 1번째, 2번째 .. 가 numArr의 각 인덱스가 되게 한다


내가 이해한 대로 정리해보자면 아래처럼 할 수도 있을것같다.

```java
        int[] answer = new int[numArr.size()];
        for (int i = 0; i < numArr.size(); i++) {
            answer[i] = numArr.get(i);
        }
```

---

```java
import java.util.ArrayList;
import java.util.Arrays;

public class Solution {
    public int[] solution(int[] array, int[][] commands) {
        // 답안 숫자들이 들어갈 arrayList
        ArrayList<Integer> numArr = new ArrayList();

        for (int i = 0; i < commands.length; i++) {
            // array에서 i번째 숫자부터 j번째 숫자까지 자르기
            int[] sortedArr = Arrays.copyOfRange(array,commands[i][0] - 1,commands[i][1]);
            // 정렬하기
            Arrays.sort(sortedArr);
            // arrayList에 k번째에 있는 수 넣기
            numArr.add(sortedArr[commands[i][2] - 1]);
        }

        // arrayList에 담은 답안 숫자를 answer배열에 넣기
        int[] answer = new int[numArr.size()];
        for (int i = 0; i < numArr.size(); i++) {
            answer[i] = numArr.get(i);
        }

        return answer;
    }
}
```