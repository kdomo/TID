## 1-2.Queue vs Stack

---

### 1-2-1. Queue는 무슨 자료구조 인가요?

queue는 선입선출 FIFO(First In First Out)의 자료구조입니다. 시간복잡도는 enqueue O(1), dequeue O(1) 입니다. 활용 예시는 Cache구현, 프로세스 관리, 너비우선탐색(BFS) 등이있습니다.

**구현방식**

- Array-Based: enqueue와 dequeue 과정에서 남는 메모리가 생깁니다. 따라서 메모리의 낭비를 줄이기 위해 주로 Circular Queue형식으로 구현합니다.
- List-Based: 재할당이나 메모리 낭비의 걱정을 할 필요가 없어집니다.

**확장 & 활용**

queue의 개념에서 조금 확장한 자료구조들로는 양쪽에서 enqueue와 dequeue가 가능한 **deque**와 시간순서가 아닌 우선순위가 높은 순서로 dequeue할 수 있는 **priority queue**가 있습니다.

활용 예시로는 하나의 자원을 공유하는 프린터나, CPU Task Scheduling, Cache구현, 너비우선탐색(BFS)등이 있습니다.

### 1-2-1 꼬꼬무. Array-Based와 List-Based의 경우 어떤 차이가 있나요?

Array-Base의 경우 queue는 circular queue로 구현하는 것이 일반적입니다. 이는 메모리를 효율적으로 사용하기 위함입니다. 또한, enqueue가 계속 발생하면 fixed size를 넘어서게 되기 때문에, dynamic array와 같은 방법으로 Array의 size를 확장시켜야 합니다. 그럼에도 enqueue의 시간복잡도는 (amortized)O(1)를 유지할 수 있습니다.

 List-Base의 경우 보통 singly-lilnked list로 구현을 합니다. enqueue는 단순히 singly-lilnked list에서 append를 하는 것으로 구현되고, 이 때 시간복잡도는 O(1)입니다. dequeue는 맨 앞의 원소를 삭제하고 first head를 변경하면 되기 때문에 이 연산도 O(1)의 시간이 걸립니다.

 요약하자면, 두 가지 종류의 자료구조로 queue를 구현을 하더라도 enqueue와 dequeue는 모두 O(1)의 시간복잡도를 갖습니다. Array-Base의 경우 전반적으로 performance가 더 좋지만, worst case의 경우에는 훨씬 더 느릴 수 있습니다(resize). List-Base의 경우에는 enqueue를 할 때마다 memory allocation을 해야 하기 때문에 전반적인 runtime이 느릴 수 있습니다.

### 1-2-2. Stack은 어떤 자료구조 인가요?

Stack은 후입선출 LIFO(Last In First Out)의 자료구조 입니다. 시간복잡도는 Push O(1), Pop O(1)입니다.

활용 예시는 후위 표기법,  괄호 유효성 검사, 웹 브라우저 방문기록(뒤로 가기), 깊이 우선 탐색(DFS)가 있습니다.

### 1-2-3. Stack 두 개를 이용하여 Queue를 구현해 보세요.

```java
public class Queue {
	public Stack<Integer> inStack = new Stack<>();
	public Stack<Integer> outStack = new Stack<>();

	public void enqueue(int n) {
		inStack.push(n);
	}
        
	public int dequeue() {
			if (outStack.isEmpty()) {
					while (!inStack.isEmpty()) {
							outStack.push(inStack.pop());
					}
			}
			return outStack.pop();
	}
}

public class Main {
	public static void main(String[] args) {
		Queue queue = new Queue();
		queue.enqueue(1);
		System.out.println(queue.dequeue());
	}
}
```

### 1-2-3 꼬꼬무. 그럼 시간복잡도는 어떻게 되는지 설명해주세요.

- enqueue() : instack.push()를 한번만 하면 되기 때문에 시간복잡도 O(1)입니다.
- dequeue() : 두 가지 경우를 따져봐야 합니다. worst case는 outstack이 비어있는 경우입니다. 이 때는 instack에 있는 n개의 데이터를 instack.pop()을 한 이후에 outstack.push()를 해줘야 합니다. 따라서 총 2*n 번의 operation이 실행되어야 하므로 O(n)의 시간복잡도를 갖습니다.
    
    하지만 outstack이 비어있지 않는 경우에는 outstack.pop()만 해주면 됩니다. 이는 O(1)의 시간복잡도를 갖습니다. 이를 종합했을 때, amortized O(1)의 시간복잡도를 갖는다고 할 수 있습니다. 
    

### 1-2-4. Queue 두 개를 이용하여 Stack을 구현해 보세요.

```java
class Stack {
	public Queue<Integer> q1 = new LinkedList<>();
	public Queue<Integer> q2 = new LinkedList<>();

	public void push(int n) {
		q1.offer(n);
	}

	public int pop() {
		while (q1.size() != 1) {
			q2.offer(q1.poll());
		}

		Queue<Integer> temp = q2;
		q2 = q1;
		q1 = temp;

		return q2.poll();
	}
}
```

편의상 push()에 사용할 queue는 q1이라고 부르고 pop()에 사용할 queue를 q2라고 칭하겠습니다. 두 개의 queue로 stack을 구현하는 방법은 다음과 같습니다.

1. push() :: q1으로 enqueue()를 하여 데이터를 저장합니다.
2. pop() :: 
    1. q1에 저장된 데이터의 갯수가 1 이하로 남을 때까지 dequeue()를 한 후, 추출된 데이터를 q2에 enqueue()합니다. 결과적으로 가장 최근에 들어온 데이터를 제외한 모든 데이터는 q2로 옮겨진다.
    2. q1에 남아 있는 하나의 데이터를 dequeue()해서 가장 최근에 저장된 데이터를 반환한다.(LIFO)
    3. 다음에 진행될 pop()을 위와 같은 알고리즘으로 진행하기 위해 q1과 q2의 이름을 swap한다.
    

### 1-2-4 꼬꼬무. 그럼 시간복잡도는 어떻게 되는지 설명해주세요.

- push() : q1.enqueue()를 한번만 하면 되기 때문에 O(1)의 시간복잡도를 갖습니다.
- pop() :  q1에 저장되어 있는 n개의 원소중에 n-1개를 q2로 옮겨야 하므로 O(n)이 됩니다.

### 1-2-5. ⭐️Queue vs Priority Queue를 비교하여 설명해주세요.

Heap은 그 자체로 우선순위 큐(Priority Queue)의 구현과 일치합니다.

Heap은 완전이진트리 구조입니다. Heap이 되기 위한 조건은 다음과 같습니다.

- Max Heap → 각 Node에 저장된 값은 Child Node들에 저장 된 값보다 크거나 같다.
- Min Heap → 각 Node에 저장된 값은 Child Node들에 저장 된 값보다 작거나 같다.

**Heap 구현**

Tree는 보통 Linked List로 구현합니다. 하지만 Heap은 Tree임에도 불구하고 Array를 기반으로 구현해야 합니다. 그 이유는 새로운 Node를 힙의 ‘마지막 위치’에 추가해야 하는데,이 때 Array를 기반으로 구현해야 이 과정이 수월해 지기 때문입니다.

구현의 편의를 위해 0번째 인덱스는 사용하지 않습니다.

완전이진트리의 특성을 활용하여 Array의 Index만으로 부모 자식간의 관계를 정의합니다.

- n번째 Node의 Left Child Node = 2n
- n번째 Node의 Right Child Node = 2n+1
- n번째 Node의 Parent Node = n/2

**Heap push -  O(logn)**

heap tree의 높이는 logN입니다.

`push()` 를 했을 때, swap하는 과정이 최대  logN번 반복되기 때문에 시간복잡도는  O(logn)입니다.


**Heap pop - O(logn)**

`pop()`을 했을 때, swap하는 과정이 최대  logN번 반복되기 때문에 시간복잡도는  O(logn)입니다.

- 각 node에 저장된 값은 child node들에 저장된 값보다 크거나 같다(max heap)
    
    ⇒ root node에 저장된 값이 가장 큰 값이 된다.