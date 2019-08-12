# 트리

* 비선형 구조(트리 모양)
* 1:n 관계를 가지는 자료구조
* 노드 중 최상위 노드를 루트(root)라 한다
* 형제간의 간선은 없다

### 이진트리

---

* 모든 노드들이 2개의 서브트리를 갖는 형태
* 레벨 i 에서의 노드의 초대 개수는 2^i 개 
* 높이가 h인 이진 트리가 가질 수 있는 노드의 최소 개수는 (h+1)개
* 최대 개수는 2^(h+1) - 1 개 이다

#### 포화 이진 트리(Full Binary Tree)

* 모든 레벨에 노드가 포화상태로 차 있는 이진 트리

#### 완전 이진 트리(Complete Binary Tree)

* 포화가 아닌 이진 트리
* 빈곳 없이 왼쪽부터 채운다

#### 편향 이진 트리(Skewed Binary Tree)

* 한쪽 방향의 자식 노드 만을 가진 이진 트리



#### 이진트리 - 순회(Traversal)

---

* 전위순회 : VLR
  * 부모노드 방문 후 , 자식노드를 좌,우 순서로 방문
* 중위순회 : LVR
  * 왼쪽 자식노드, 부모노드, 오른쪽 자식노드 순으로 방문
* 후위순회 : LRV
  * 자식노드를 좌우 순서로 방문한 후, 부모노드로 방문

```java
public class TreeNode {
	Object data;
	TreeNode left, right;

	public TreeNode(Object data) {
		this.data = data;
	}

	public TreeNode(TreeNode left, Object data, TreeNode right) {
		super();
		this.left = left;
		this.data = data;
		this.right = right;
	}

}
/////////////////////////////////////////////////////////////////
	public void makeTree(String postExpression) {
		Stack<TreeNode> stack = new Stack<TreeNode>();
		int length = postExpression.length();
		
		for(int i=0; i<length;++i) {
			char c = postExpression.charAt(i);
			TreeNode node = new TreeNode(c);
			switch(c) {
			case '+':case'-':case'*':case'/':
				node.right = stack.pop();
				node.left = stack.pop();
				break;
			}
			stack.push(node);
		}
		root = stack.pop();
	}

public void printByPreOrder() {
		printByPreOrder(root);
		System.out.println();
	}

	private void printByPreOrder(TreeNode current) {
		if (current != null) {
			System.out.print(current.data + " ");
			printByPreOrder(current.left);
			printByPreOrder(current.right);
		}
	}
	
	public void printByInOrder() {
		printByInOrder(root);
		System.out.println();
	}
	
	private void printByInOrder(TreeNode current) {
		if (current != null) {
			printByInOrder(current.left);
			System.out.print(current.data + " ");
			printByInOrder(current.right);
		}
	}
	
	public void printByPostOrder() {
		printByPostOrder(root);
		System.out.println();
	}
	
	private void printByPostOrder(TreeNode current) {
		if (current != null) {
			printByPostOrder(current.left);
			printByPostOrder(current.right);
			System.out.print(current.data + " ");
		}
	}
```