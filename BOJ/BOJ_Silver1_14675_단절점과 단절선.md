# 단절점과 단절선

날짜: 2023년 1월 30일
레벨: Silver1
분류: 그래프
언어: Java
출제기관: 백준

## 문제

[14675번: 단절점과 단절선](https://www.acmicpc.net/problem/14675)

## 내 풀이

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.ArrayList;
import java.util.StringTokenizer;

public class BOJ_14675_단절점과단절선 {

	public static void main(String[] args) throws NumberFormatException, IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		int N = Integer.parseInt(br.readLine()); // 트리 정점 개수
		StringTokenizer st = null;

		ArrayList<Integer>[] list = new ArrayList[N + 1];
		for (int i = 1; i <= N; i++) {
			list[i] = new ArrayList<Integer>();
		}

		for (int i = 0; i < N - 1; i++) {
			st = new StringTokenizer(br.readLine());
			int a = Integer.parseInt(st.nextToken());
			int b = Integer.parseInt(st.nextToken());
			list[a].add(b);
			list[b].add(a);
		}

		StringBuilder sb = new StringBuilder();
		int q = Integer.parseInt(br.readLine());
		for (int i = 0; i < q; i++) {
			st = new StringTokenizer(br.readLine());
			int t = Integer.parseInt(st.nextToken());
			int k = Integer.parseInt(st.nextToken());
			if (t == 1 && list[k].size() < 2) { // 자식이 1개일때는 단절점이 무조건 아님
				sb.append("no\n");
			} else { // 단절선, 자식이 2개인 단절점
				sb.append("yes\n");
			}
		}
		System.out.println(sb.toString());
	}
}
```

- 단절점일때 자식이 1개밖에 없다면 그래프가 2개 이상으로 나눠지지 않음
- 예제 입력에서 정점 1이 단절점인지 묻는것을 보고 생각해냄