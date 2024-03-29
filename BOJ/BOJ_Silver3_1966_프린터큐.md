# 프린터 큐

날짜: 2023년 2월 28일
레벨: Silver3
분류: 구현
언어: Java
출제기관: 백준

## 문제

[1966번: 프린터 큐](https://www.acmicpc.net/problem/1966)

## 내 풀이

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.LinkedList;
import java.util.StringTokenizer;

public class BOJ_Silver3_1966_프린터큐 {

	public static void main(String[] args) throws NumberFormatException, IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		int T = Integer.parseInt(br.readLine());

		for (int t = 0; t < T; t++) {
			StringTokenizer st = new StringTokenizer(br.readLine());
			int N = Integer.parseInt(st.nextToken()); // 문서 개수
			int M = Integer.parseInt(st.nextToken()); // 몇번째

			LinkedList<Paper> queue = new LinkedList<>();
			st = new StringTokenizer(br.readLine());
			int max = 0; // 문서 중 최대 중요도
			for (int i = 0; i < N; i++) {
				int level = Integer.parseInt(st.nextToken());
				queue.add(new Paper(i, level));
				max = Math.max(max, level);
			}

			int cnt = 1;
			while (true) {
				Paper now = queue.poll();
				if (now.level == max) { // 현재 문서의 중요도가 최대일 경우
					if (now.index == M) { // 찾는 문서라면
						System.out.println(cnt);
						break;
					} else { // 찾는 문서가 아니라면 최대 중요도 갱신
						max = searchMax(queue);
					}
					cnt++; // 인쇄했으니 증가
				} else { // 다시 맨 뒤로 재배치
					queue.add(new Paper(now.index, now.level));
				}
			}

		}

	}

	static int searchMax(LinkedList<Paper> queue) {
		int max = 0;
		for (int i = 0; i < queue.size(); i++) {
			max = Math.max(max, queue.get(i).level);
		}
		return max;
	}

	static class Paper {
		int index, level;

		public Paper(int index, int level) {
			super();
			this.index = index;
			this.level = level;
		}
	}
}
```

- 조건에 맞게 수행해주면 되는 문제
- 중요도와 문서의 인덱스를 같이 저장하기 위해 Paper 클래스를 생성해서 풀이