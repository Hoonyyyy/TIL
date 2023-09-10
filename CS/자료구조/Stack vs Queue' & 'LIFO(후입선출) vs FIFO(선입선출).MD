# Stack vs Queue' & 'LIFO(후입선출) vs FIFO(선입선출)

# Stack & LIFO (후입선출)

<img src="https://velog.velcdn.com/images/baekgom/post/93d37e6f-ca85-475f-b839-5c7f07ba5dd2/image.png">

- 가장 최근에 요청된 것을 가장 먼저 처리, 가장 처음에 들어온 요청은 최후에 처리
  - 같은 구조와 크기의 자료를 정해진 방향으로만 쌓을 수 있다.
  - top으로 정한 곳을 통해서만 접근 가능해서, 거기서 데이터의 추가/삭제가 이뤄진다.
- 자료 구조 中 stack에 들어 있는 프로그램의 작업요청을 처리하는 방식
  - top을 통해 삽입하는 연산 = 'push'
  - top을 통해 삭제하는 연산 = 'pop'
- 활용예시
  - 웹 브라우저의 앞/뒤로 가기
    - 가장 나중에 열린 페이지부터 다시 보여줌
  - 수식 계산
  - 수식 괄호 검사
    -연산자 우선순위 표현을 위한 괄호 검사
  - 워드프로세서의 undo/redo


### 사용법 예시1
~~~ java
public class StackQueue {
	public static void main (String[] args) {
    	Stack<String> st = new Stack<String>();
    
    	st.push("0");
        st.push("1");
        st.push("2");
    
    	System.out.println("--- Stack ---")
		While(!st.isEmpty()) {
        	System.out.println(st.pop());
        }
    }
}

/* 출력 결과
2
1
0
*/
~~~

### 사용법 예시2
- empty()
  - stack이 비어 있는지 확인 (비어있으면 true, 없으면 false)
- peek()
  - 스택의 맨 위에 저장된 객체를 반환
  - pop()과 달리, 객체를 반환 후 삭제 하지는 X(즉, 스택에서 객체를 꺼내지 않음)
  - 비었을 때 EmptyStackException을 반환
- pop()
  - 스택의 맨 위에 저장된 객체를 반환하고 삭제
  - 비었을 때 EmptyStackException을 반환
- push()
  - 스택에 객체를 저장(위에서 삽입)
- search()
  - 스택에서 주어진 객체를 찾아서 그 위치를 반환
  - 해당 객체가 있다면 1, 없으면 -1을 반환
  - 위치는 1부터 시작(배열은 0부터 시작함!!!)
~~~ java
import java.util.Stack;

public class Col1 {
    public static void main(String[] args) {
        Stack<Integer> intStack = new Stack<Integer>();     // 선언 및 생성

        intStack.push(1);
        intStack.push(2);
        intStack.push(3);

        // 다 지워질때까지 출력
        while (!intStack.isEmpty()) {
            System.out.println(intStack.pop());     // 3,2,1 출력
        }

        // 다시 추가
        intStack.push(1);
        intStack.push(2);
        intStack.push(3);

        // peek() vs pop()
        // 1. peek()
        System.out.println(intStack.peek()); 	// 3 출력
        System.out.println(intStack.size()); 	// 3 출력 (peek() 할때 삭제 안됬음)

        // 2. pop()
        System.out.println(intStack.pop()); 	// 3 출력
        System.out.println(intStack.size()); 	// 2 출력 (pop() 할때 삭제 됬음)

        System.out.println(intStack.pop()); 	// 2 출력
        System.out.println(intStack.size()); 	// 1 출력 (pop() 할때 삭제 됬음)

        // 다 지워질때까지 출력
        while (!intStack.isEmpty()) {
            System.out.println(intStack.pop());     // 1 출력 (마지막 남은거 하나)
        }
    }
}

/* 출력 결과
3
2
1
3
3
3
2
2
1
1
*/
~~~


# Queue & FIFO (선입선출)
<img src="https://velog.velcdn.com/images/baekgom/post/7adeaf61-f416-4a0d-a986-b55a5db7eafa/image.png">

<img src="https://velog.velcdn.com/images/baekgom/post/658ffc21-5435-4d71-a4f1-07c2525eff5b/image.png">

- 가장 오래된 요청(가장 먼저 요처된)을 가장 먼저 처리
	- 한쪽 끝에서 삽입 작업, 다른 쪽 끝에서 삭제 작업이 양쪽으로 이루어진다.
		- 프론트(front) : 삭제 연산만 수행되는 곳 -> 디큐(Dequeue) : front에서 이루어지는 삭제 연산
		-	리어(rear) : 삽입 연산만 수행되는 곳 -> 인큐(Enqueue) : rear에서 이루어지는 삽입 연산
- 자료 구조 中 큐에 들어있는 프로그램의 작업요청을 처리하는 방식
	- "Queue" : (무엇을 기다리는 사람, 자동차 등의) 줄, 혹은 줄을 서서 기다리는 것
	- 스택과 달리(new Stack), 생성자가 없는 인터페이스
		- Queue는 생성자가 없는 껍데기라서 바로 생성은 x
		- 생성자가 존재하는 클래스인 LinkedList를 사용하여 Queue를 생성해서 받을 수 있다.
		- Queue 를 사용하기 위해선 java.util.LinkedList; 와 import java.util.Queue; 를 추가해야한다.
- 데이터를 꺼낼 때, 항상 첫 번째 저장된 데이터를 삭제!!!
	- 따라서 Queue는 데이터의 추가/삭제가 쉬운 컬렉션 프레임워크가 적합함
- 활용 예시
	- 주로 데이터가 입력된 시간 순서대로 처리해야 할 필요가 있는 상황
		- 1. 인쇄 작업 대기 목록
		- 버퍼(Buffer)
		- 우선순위가 같은 작업 예약
		- 은행 업무
		- 프로세스 관리
		- 캐시 구현
		- 선착순 티켓 판매

### 예시 1
- Java에서는 큐를 Queue 인터페이스로만 정의해둬서, 별도의 클래스 제공은 x
	- 따라서, Queue 인터페이스를 구현한 클래스들 중 하나를 사용하면 된다.
~~~ java
public class StackQueue {
	public static void main (String[] args) {
        Queue<String> q = new LinkedList<String>();		// LinkedList 클래스로 객체 생성
    
    	q.offer("0");
        q.offer("1");
        q.offer("2");
    
    	System.out.println("--- Queue ---")
		While(!q.isEmpty()) {
        	System.out.println(q.pop());
        }
    }
}

/* 출력 결과
0
1
2
*/
~~~

### 예시 2 : 메서드
- add()
	- 지정된 객체를 큐에 추가
	- 성공하면 ture, 실패하면 false를 반환
	- 저장 공간이 부족하면 IllegalException 발생
- offer()
	- Queue에 데이터 저장
	- 성공 ture, 실패 false
- remove()
	- 큐에서 객체를 꺼내 반환
	- 비어있으면 NoSuchElementException 발생
- element()
	- 삭제 없이 저장된 요소 읽어옴
	- peek()와 달리, 큐가 비었을ㄷ 때 NoSuchElementExceptiond을 발생 (peek()는 null)
- peek()
	- 삭제 없이 저장된 요소(맨 앞(front)가 가리키는 값)을 읽어옴
	- 큐가 비었을 때 null을 반환
- poll()
	- 큐에서 객체(맨 앞(front)가 가리키는 값)를 꺼내서 반환
	- 큐가 비어 있으면 null 반환
- clear()
	- 큐에 저장된 데이터들을 삭제하고 초기화
- enqueue()
	- 큐의 마지막 위치에 데이터를 추가하는 메서드
- dequeue()
	- 큐의 첫 번째 위치에 있는 데이터를 반환하고 삭제하는 메서드
~~~
Java에서 Queue 인터페이스로 선언하여 라이브러리를 사용할 경우, back()과 같은 역할을 하는 메서드가 없다.
(맨 앞의 원소를 반환하는 peek() 메서드는 있음)
~~~

~~~ java
import java.util.LinkedList;
import java.util.Queue;

public class Main {
	public static void main(String[] args) {
		Queue<Integer> intQueue = new LinkedList<>(); 		// 선언 및 생성

		intQueue.add(1);
		intQueue.add(2);
		intQueue.add(3);

		// 다 지워질때까지 출력
		while (!intQueue.isEmpty()) {
			System.out.println(intQueue.poll()); 		// 1,2,3 출력
		}

		// 다시 추가
		intQueue.add(1);
		intQueue.add(2);
		intQueue.add(3);

		// peek() vs pop()
		// 1. peek()
		System.out.println(intQueue.peek()); 	// 1 출력 (맨먼저 들어간값이 1 이라서)
		System.out.println(intQueue.size()); 	// 3 출력 (peek() 할때 삭제 안됐음)

		// 2. poll()
		System.out.println(intQueue.poll()); 	// 1 출력
		System.out.println(intQueue.size()); 	// 2 출력 (poll() 할때 삭제 됐음)

		System.out.println(intQueue.poll()); 	// 2 출력
		System.out.println(intQueue.size()); 	// 1 출력 (poll() 할때 삭제 됐음)

		// 다 지워질때까지 출력
		while (!intQueue.isEmpty()) { 
			System.out.println(intQueue.poll()); 		// 3 출력 (마지막 남은거 하나)
		}
	}
}
~~~

### PriorityQueue
- 우선 순위에 따라 객체를 처리할 때 사용
	- 선입선출을 기본으로 허ㅏ지만, 우선 순위에 따라 먼저 처리해야할 것이 있다면, 우선 순위 힙(heap)을 기반으로 처리
- 숫자가 작을수록 우선순위가 높음(오름차순)
~~~ java
class GfG {
    public static void main(String args[]) {
    
        // 우선순위 큐 선언
        PriorityQueue<Integer> pQueue = new PriorityQueue<Integer>();
  
        // 데이터 입력
        pQueue.add(10);
        pQueue.add(20);
        pQueue.add(15);
  
        // 첫 번째 데이터 결과 출력
        System.out.println(pQueue.peek());
  
        // 오름차순하여 데이터 출력 -> 출력한 데이터는 제거된다
        System.out.println(pQueue.poll());
  
        // 두 번째 데이터 15 출력
        System.out.println(pQueue.peek());
    }
}

/* 출력 결과
10 
10 
15
*/
~~~

### Deque

<img src="https://velog.velcdn.com/images/baekgom/post/93d37e6f-ca85-475f-b839-5c7f07ba5dd2/image.png">

- 큐 데이터 구조의 변형
- "양방향 큐"
	- 양쪽 끝에서 요소를 추가/제거할 수 있는 구조
- ArrayDeque
~~~ java
public class ArrayDequeDemo {
    public static void main(String[] args) {
    
        // Deque 선언
        ArrayDeque<Integer> de_que = new ArrayDeque<Integer>(10);
  
        // 값 입력
        de_que.add(10);
        de_que.add(20);
        de_que.add(30);
        de_que.add(40);
        de_que.add(50);
  
  		// 결과 출력
        System.out.println(de_que);
  
        // deque초기화
        de_que.clear();
  
        // 첫 번째에 데이터 입력
        de_que.addFirst(564);
        de_que.addFirst(291);
  
        // 마지막에 데이터 입력
        de_que.addLast(24);
        de_que.addLast(14);
  
  		// 결과 출력
        System.out.println(de_que);
    }
}

/* 출력 결과
[10, 20, 30, 40, 50] 
[291, 564, 24, 14]
*/
~~~



https://velog.io/@baekgom/LIFO-%EC%84%A0%EC%9E%85%EC%84%A0%EC%B6%9C-FIFO-%ED%9B%84%EC%9E%85%EC%84%A0%EC%B6%9C

https://swk3169.tistory.com/283
