# Scope, Static

## 스코프?
- 사용할 수 있는 범위를 나타낸다

### 전역변수(Global Variable)
- 어디서든 사용 가능함    * 전역 : 클래스 내의 모든 장소에서 사용할 수 있기 때문

### 지역변수(Locale Variable)
- 메서드 안에서만 사용이 가능

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
