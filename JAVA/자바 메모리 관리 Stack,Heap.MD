# 자바 메모리 관리 Stack,Heap

## Stack
- Heap 영역에 생성된 Object 타입의 데이터의 참조값이 할당됨
- 원시타입의 데이터가 값과 함께 할당
- 지역변수들은 scope에 따른 visibility를 가짐
- 각 Thread는 자신만의 stack을 가짐
```
Stack에는 heap영역에 생성된 Object 타입의 데이터들에 대한 참조를 위한 값들이 할당됨 또한,
원시타입(byte, short, int, long, double,float, boolean, char) 타입의 데이터들이 할당됨
이때 원시타입의 데이터들에 대해서는 참조값을저장하는 것이 아닌 실제 값을 Stack에 직접 저장함

Stack 영역에 있는 변수들은 visibility를 가짐, 변수 scope에 대한 개념임
전역변수가 아닌 foo() 함수 안에 지역변수가 stack에 할당 된 경우, 해당 지역변수는 다른 함수에 접근할 수 없음

ex. foo() 함수에서 bar() 함수 호출하고 bar() 함수의 종료되는 중괄호 }가 실행된 경우(함수가 종료된 경우),
    bar() 함수내부에서 선언된 모든 지역변수들은 stack에서 pop 되어 사라짐

```

### Stack 간단 코드
``` java
package test;

public class Test2 {
    public static void main(String[] args) {
        int argument = 4;
        System.out.println(argument = someOperation(argument));
    }
    private static int someOperation(int param){
        int tmp = param * 3;
        int result = tmp / 2;
        return result;
    }
}
```


https://yaboong.github.io/java/2018/05/26/java-memory-management/
