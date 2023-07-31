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

### Stack 간단 코드 ( 그림은 아래 출처 참조하기 )
- 6 나
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

## Heap
- 긴 생명주기를 가진 데이터들이 저장됨(대부분의 오브젝트는 크기가 크고, 서로 다른 코드블럭에서 공우되는 경우가 많음)
- 애플리케이션의 모든 메모리 중 stack에 있는 데이터를 제외한 부분
- 모든 Object타입 (Integer, String, ArrayList, ...)은 heap 영역에 생성됨
- 몇개의 스레드가 존재하든 상관없이 단 하나의 heap영역만 존재함
- Heap 영역에 있는 오브젝트들을 가르키는 레퍼런스 변수가 stack에 올라감

### println값이 hello world가 아닌 hello가 나온 이유
- main() 메서드의 s 변수가 참조하는 "hello" 오브젝트를 param에 복사하면서 changeString() 메서드가 시작
- param += "world"; 를 실행하는 것은 heap에 "hello world"라는 스트링 오브젝트가 새롭게 할당되는 작업임
- 기존에 "hello" 오브젝트를 참조하고 있던 param으로 새롭게 생성된 스트링 오브젝트인 "hello world"를 참조하도록 만드는것
- changeString() 함수가 종료되면, 새롭게 생성된 "hello world" 오브젝트를 참조하는 param이라는 변수는 스택에서 pop 되므로 어느것도 레퍼런스 안한 상태 됨
- "hello world" 오브젝트는 garbage로 분류됨
``` java
public class Main {
    public static void main(String[] args) {
        String s = "hello";
        changeString(s);
        System.out.println(s);
    }
    public static void changeString(String param) {
        param += " world";
    }
}
```




https://yaboong.github.io/java/2018/05/26/java-memory-management/
