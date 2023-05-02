# 문자열 나누기

https://school.programmers.co.kr/learn/courses/30/lessons/140108

1. 문자 s를 각각 나누어 arrayList에 넣는다
2. x와 같은 숫자(count1), x와 다른 숫자(count2)를 세는 변수 생성
3. 첫 문자일 때, 또는 첫 문자와 같은 문자일 때 count1 증가
4. 첫 문자와 비교 문자가 다를 때 count2 증가. 이 때, 첫 문자는 인덱스 0이 아닐 수도 있으므로 (ex: banana 에서 ba문자를 만든 뒤에는 n은 인덱스 0은 아니지만 첫 문자가 됨) num이라는 변수에 첫 문자의 인덱스를 저장하게 함
5. count들의 수가 같아질 때 sArr2에 만들어진 문자를 넣고, 초기화
6. for문의 마지막 인덱스(i == sArr.size() - 1)에서 나머지 만들어진 문자를 집어넣음


```java
import java.util.ArrayList;

public class Solution {
    public int solution(String s) {
        int answer = 0;

        // arrayList에 s 쪼개서 넣기
        ArrayList<String> sArr = new ArrayList<>();
        for (int i = 0; i < s.length(); i++) {
            sArr.add(s.substring(i, i + 1));
        }

        // x와 같을 때 증가
        int count1 = 0;
        // x와 다를 때 증가
        int count2 = 0;
        String tempString = "";
        // 만들어진 문자를 집어넣을 빈 배열
        ArrayList<String> sArr2 = new ArrayList<>();
        // 첫 문자의 인덱스를 저장
        int num = 0;

        for (int i = 0; i < sArr.size(); i++) {
            // 첫 문자일 때, 또는 첫 문자와 같은 문자일 때
            if(count1 == 0 ) {
                count1 ++;
                tempString += sArr.get(i);
                num = i;
            } else if (sArr.get(i).equals(sArr.get(num))) {
                tempString += sArr.get(i);
                count1 ++;
            }

            // 첫 문자와 비교 문자가 다를 때 count2 증가
            if (!sArr.get(i).equals(sArr.get(num))) {
                tempString += sArr.get(i);
                count2 ++;
            }
            
            // count들의 수가 같아질 때 빈 arrayList에 만들어진 문자를 넣고, 초기화
            if (count1 == count2) {
                sArr2.add(tempString);
                count1 = 0;
                count2 = 0;
                tempString = "";
            } else if (i == sArr.size() - 1) {
                // for문의 마지막 인덱스에서 나머지 만들어진 문자를 집어넣음
                sArr2.add(tempString);
            }
        }
        answer = sArr2.size();
        return answer;
    }
}
```