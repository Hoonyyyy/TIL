# Scope, Static

## 스코프?
- 사용할 수 있는 범위를 나타낸다

### 전역변수(Global Variable)
- 어디서든 사용 가능함    * 전역 : 클래스 내의 모든 장소에서 사용할 수 있기 때문

### 지역변수(Locale Variable)
- 메서드 안에서만 사용이 가능

### 예시
```JAVA
public class ScopeTest {
    String sClassVal = "Class Value"; // Class 영역에 선언한 변수(Global Variable)
    static String StaticVal = "Static Value"; // 스태틱은 클래스 내에서 공유되어 아무데서나 사용

    public void method1(){
        String sMethod1Val = "method Value"; // Method 영역에 선언한 변수(Local Variable)
        System.out.println(sClassVal); // Class 영역 안에 있는 메서드에서는 클래스 변수 사용 가능
    }

    public static void main(String[] args) {
        // 메인 메서드는 static 변수가 아닐 경우 객체화해야 클래스 변수 사용 가능
        System.out.println(StaticVal);
        ScopeTest sT = new ScopeTest();
        System.out.println(sT.sClassVal);

    }
}
```
------------------------------------------------------------------------------------------------

# 다른 설명
- 협업 시
- left가 왼쪽을 뜻할수도 있고, Leave과거형인 left로 사용될 수도 있음
- 유효범위(Scope)가 존재하므 이러한 명충돌을 방지할 수 있다.
``` JAVA
int left;
public void left() {}
```


- 유효범위(Scope)를 "제외" 하고 생각하면
- for문이 돌아갈 떄 메서드 a가 실행되면서 i=0이 되므로 무한으로 찍히는 경우가 발생함 바로 무한루프 발생
- 하지만 유효범위가 존재하기에 0,1,2,3,4 찍히고 죵로됨
- 메서드에서 다른메서드의 지역변수(i)를 호출한다 하더라도, 유효 범위의 우선순위는 지역변수 그다음이 메머변수임
- 또한 메서드에서 다른 메서드의 지역변수의 값은 참조 할 수 없다.
``` JAVA
public class DemoScope {
   static void a () {
      int i = 0;
   }

   public static void main(String[] args) {
      for(int i = 0; i < 5; i++) {
         a();
         System.out.println(i);
      }
   }
}
```


- 메서드 a의 i와 for문에 i가 모두 멤버변수의 값을 참조하고 있음
- 무한루프에 빠짐
- for에서 i가 증가되어도 sout(i)가 실행 전 메서드 a가 먼저 실행되기 때문에 i의 값은 계속 0이 되므로 무한루프 빠짐
``` JAVA
public class DemoScope {
    static int i;
    static void a() {
        i = 0;
    }
    public static void main(String[] args) {
        for(i = 0; i < 5; i++) {
            a();
            System.out.println(i);
        }
    }
}
```




