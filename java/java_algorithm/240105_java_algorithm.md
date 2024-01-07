# 명예의 전당(1)

https://school.programmers.co.kr/learn/courses/30/lessons/138477


1. k만큼 명예의 전당에 등록한다. (kNums는 명예의 전당에 등록된 숫자들의 배열)
2. kNums의 가장 큰 숫자와 score의 값을 비교하여 크거나 같을 때를 확인한다.
3. 조건에 부합하면 kNums의 가장 작은 수를 삭제하고, 새로운 수를 명예의 전당에 등록한다.
4. kNums를 내림차순 정렬하며, 가장 작은 수를 answer에 입력한다.
4. 조건에 부합하지 않으면 kNums 그대로 가장 작은 수를 answer에 입력한다.

```java
import java.util.ArrayList;
import java.util.Collections;

public class Solution {
    public int[] solution(int k, int[] score) {
        int[] answer = new int[score.length];
        ArrayList <Integer> kNums = new ArrayList<>();
        //명예의전당 자리 수만큼 일단 넣음 (내림차순
        for (int i = 0; i < k; i++) {
            kNums.add(score[i]);
            Collections.sort(kNums,Collections.reverseOrder());
            answer[i] = kNums.get(kNums.size() - 1);
        }
        for (int i = k; i < score.length; i++) {
            // 숫자를 kNums의 첫번째 숫자 (가장 큰 숫자)와 비교
            for (int j = 0; j < kNums.size(); j++) {
                if(score[i] >= kNums.get(j)) {
                    // 가장 작은 수(마지막 수)를 지우고 새로 전당 등록
                    kNums.remove(kNums.size() - 1);
                    kNums.add(score[i]);
                    Collections.sort(kNums,Collections.reverseOrder());
                    answer[i] = kNums.get(kNums.size() - 1);
                    break;

                }
                if (score[i] < kNums.get(j)) {
                    answer[i] = kNums.get(kNums.size() - 1);
                }

            }
        }
        return answer;
    }
}
```

---

## 개선 답안

ArrayList에서 최소값을 찾아주는 Collections.min 메서드를 적용하여, 코드를 수정해보았다.

1. 명예의 전당에 올라갈 수를 담는 arrayList인 kNums를 만든다.
2. score의 값을 반복문으로 돌면서, kNums에 각 값을 넣어준다.
3. kNums의 크기가 k보다 커지면, 가장 낮은 점수를 Collections.min으로 찾아내어 제거한다.
4. kNums에서 가장 낮은 점수를 answer에 넣는다.


```java
import java.util.ArrayList;
import java.util.Collections;

public class Solution {
    public int[] solution(int k, int[] score) {
        int[] answer = new int[score.length];

        ArrayList <Integer> kNums = new ArrayList<>();

        for (int i = 0; i < score.length; i++) {
            kNums.add(score[i]);

            // kNums의 크기가 k보다 커지면 가장 낮은 점수 제거
            if (kNums.size() > k) {
                kNums.remove(Collections.min(kNums));
            }

            answer[i] = Collections.min(kNums);
        }
        return answer;
    }
}
```