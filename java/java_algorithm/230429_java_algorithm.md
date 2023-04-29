# 덧칠하기
1. 반복문으로 n을 돌면서 인덱스 i가 section의 수와 일치하는지 비교
2. section의 숫자 사이의 거리가 m을 넘는지 안넘는지 판단 - count 변수 : section이 시작되는 곳에서부터 1씩 증가하고, m과 수가 같아지면 0으로 초기화
3. 1번에서, count가 0일때만 count와 answer이 ++되도록 함 (section 길이만큼 도는 if문 안에 있기 때문에 증가가 중복되지 않기 위함)

```java
public class Solution {
    public int solution(int n, int m, int[] section) {
        int answer = 0;
        int count = 0;

        // n과 section의 숫자 비교
        for (int i = 1; i <= n; i++) {
            for (int j = 0; j < section.length; j++) {
                // i 와 section j 일치 시 카운트 시작, 첫 카운트일 시 answer ++
                if(i == section[j]) {
                    if(count == 0) {
                        answer ++;
                        count ++;
                    }
                }
            }

            // 카운트가 m에 도달할 시 초기화
            if (count == m) {
                count = 0;
            }
            else if (count > 0) {
                // 카운트 시작 후 계속 진행
                count++;
            }
        }
        return answer;
    }
}
```