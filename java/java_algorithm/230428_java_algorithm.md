# 카드 뭉치

https://school.programmers.co.kr/learn/courses/30/lessons/159994

1. goal의 배열을 반복문으로 하나씩 돌면서 cards1와 cards2의 단어와 일치하는지 판단
2. cards1과 cards2를 돌면서 일치 시에 그 카드를 제외하고 돌아야 하기 때문에, cards1num과 cards2num을 초기 설정 0으로 지정하여 일치 시에만 ++되게 하고, cards1[i]가 아닌 cards1[cards1num]으로 비교한다.
```java
package org.example;

import java.util.*;

public class Solution {
    public String solution(String[] cards1, String[] cards2, String[] goal) {
        String answer = "";
        int cards1num = 0;
        int cards2num = 0;
        for (int i = 0; i < goal.length; i++) {
            System.out.println("----" + goal[i]);
            if (cards1[cards1num].equals(goal[i])) {
                System.out.println("cards1 : " + cards1[cards1num]);
                System.out.println("yes");
                cards1num++;
                System.out.println("cards1num : " + cards1num);
                System.out.println("----------------");
            } else if (cards2[cards2num].equals(goal[i])) {
                System.out.println("cards2 : " + cards2[cards2num]);
                System.out.println("yes");
                cards2num++;
                System.out.println("cards2num : " + cards2num);
                System.out.println("----------------");
            } else {
                break;
            }
        }
        if (cards1num + cards2num == goal.length) {
            answer = "Yes";
        } else {
            answer = "No";
        }
        System.out.println(answer);
        return answer;
    }
}
```
나오는 숫자들을 다 테스트 해보면서 처음 만든 코드인데, 

No가 result로 나오는 두 번째 예시를 넣어서 실행 시켜봤더니

Exception in thread "main" java.lang.ArrayIndexOutOfBoundsException: Index 2 out of bounds for length 2

에러를 뱉었다.
배열의 길이를 넘는 인덱스를 호출해서 생긴 모양인데 실행이 잘 되는 위치와 디버깅을 통해서 21번째 줄 cards2num++에서 뭔가 이상하다는 것을 알았다.

want, to가 goal의 문자와 모두 일치하여 cards2num이 총 2가 되는데, cards2배열은 인덱스1이 끝이기 때문에 에러가 난 것이다.

cards2num이 cards2의 배열 길이를 넘지 않도록 조치를 해줬다.

여기서 중요한 것이, 에러가 걸리를 부분이 
```agsl
if (cards2[cards2num].equals(goal[i]))
```
이 부분이기 때문에, 길이 체크 if문이 위의 if문을 감싸는 형태가 되어야한다. (이걸 캐치 못해서 조금 헤맸다.)

```java
package org.example;

public class Solution {
    public String solution(String[] cards1, String[] cards2, String[] goal) {
        String answer = "";
        int cards1num = 0;
        int cards2num = 0;
        for (int i = 0; i < goal.length; i++) {
            System.out.println("----" + goal[i]);
            if (cards1num < cards1.length) {
                if (cards1[cards1num].equals(goal[i])) {
                    cards1num++;
                }
            }
            if (cards2num < cards2.length) {
                if (cards2[cards2num].equals(goal[i])) {
                    cards2num++;
                }
            }
        }
        if (cards1num + cards2num == goal.length) {
            answer = "Yes";
        } else {
            answer = "No";
        }
        return answer;
    }
}
```