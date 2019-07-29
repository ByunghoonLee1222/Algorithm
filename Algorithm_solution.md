```java
package algorithm;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

import java.util.Stack;
import java.util.StringTokenizer;

public class Solution {
	private static int T;
	private static char []s;
	public static void main(String[] args) throws NumberFormatException, IOException {
		Stack<Character> stack = new Stack<Character>();
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		T = Integer.parseInt(br.readLine());
		
		for(int i=0; i<T;++i) {
			StringTokenizer st = new StringTokenizer(br.readLine());
			s = st.nextToken().toCharArray();
		}
		
		System.out.println(s[0]);
		
	}

}
```

