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
  - 스택이 비어 있는지 확인 (비어있으면 true, 없으면 false)
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






https://velog.io/@baekgom/LIFO-%EC%84%A0%EC%9E%85%EC%84%A0%EC%B6%9C-FIFO-%ED%9B%84%EC%9E%85%EC%84%A0%EC%B6%9C

https://swk3169.tistory.com/283
