## System 클래스
- 자바는 JVM 위에서 실행되므로 운영체제의 모든 기능을 자바코드로 직접 접근하기 어렵다.
- 하지만, java.lang.System클래스를 이용하면 일부기능을 이용할 수 있다.

- 가능한 일들 : 프로그램종료, 키보드로 입력, 모니터로 출력, 메모리 정리, 현재시간읽기, 시스템프로퍼티 읽기, 환경변수 읽기

- exit() : 현재 실행되고 있는 프로세스를 강제종료 시킨다. 정상종료 0, 비정상종료 1 을 매개변수 값으로 지정한다.
- gc() : 가비지컬렉션을 호출해서 사용하지 않는 객체를 제거한다. 하지만, 자바는 JVM이 자동으로 가비지컬렉션을 수행한다.
- currentTimeMills(().nanoTime() : 컴퓨터 시계로부터 현재시간을 밀리세컨드 단위와 나노세컨드 단위로 long값을 리턴한다.
- getProperty/(String key) : JVM이 시작할 때 자동으로 설정되는 시스템의 속성값을 말함 키와 value로 구성


### Sytem.in.read()
```java
package system;

import java.io.IOException;

public class S2_PrintStream {
	public static void main(String[] args) throws IOException {
		
		char in = 0;
		System.out.println("여러개의 영문자를 입력하세요>>");
		while(true) {
			in = (char)System.in.read();
			if(in==13 || in == 10) {
				continue; // 엔터값을 받아줌
			}
			if(in=='q') {
				break;
			}
			System.out.println("입력받은 문자들은 : ");
			System.out.println(in);
		}
	}
}
```

### Class
```java
/*
	Class클래스
		. 클래스와 인터페이스의 메타데이터(클래스이름, 생성자/필드/메서드 정보)를 
		java.lang.Class로 자바는 관리한다.
		. forName()		- 클래스의 정보객체를 생성한다.
		. newInstance() - 동적으로 객체를 생성한다.
		
		. Class<?> getClass() : Object
	

*/

class Student {
	String name;
	int age;
	void introduce() {
		System.out.println(name + "님은 " + age + "살 입니다.");
	}
}

class Person {
	String name;
	String address;
	int age;
	void introduce() {
		System.out.println(name + "은 " + address + "에 살고 " + age + "살 입니다.");
	}
}

public class C1_ClassEx {
	public static void main(String[] args) {
		
		// 1.객체생성
		Student st1 = new Student();
		st1.name = "홍길동";
		st1.age = 25;
		st1.introduce();
		
		System.out.println("**********************");
		
		// 2. getClass() 활용
		
//		Student st2 = new Student();
//		
//		Class cl = st2.getClass();
//		System.out.println(cl.getName());
//		System.out.println(cl.getSimpleName());
//		System.out.println(cl.getPackageName());
//		
//		// 값이 없음을 대비해서 그에 알맞는 오류처리를 해줘야함
//		try {
//			Object obj = Class.forName(cl.getName());
//			Student st3 = (Student)obj; // 다운캐스팅
//			st3.name = "김길동";
//			st3.age = 30;
//			st3.introduce();
//		} catch (ClassNotFoundException e) {
//			System.out.println("클래스를 찾을 수 없습니다.");
//		} catch (ClassCastException e) {
//			System.out.println("클래스 형변환에 오류가 있습니다.");
//		} 
		
		
		// 3. forName()
		try {
			Class cl2 = Class.forName("Class.Student");
			Object obj = cl2.newInstance();
			Student st4 = (Student)obj;
			st4.name = "이길동";
			st4.age = 15;
			st4.introduce();
			
		} catch (ClassNotFoundException e) {
			System.out.println("클래스를 찾을 수 없습니다.");
		} catch (InstantiationException e) {
			System.out.println("객체를 생성할 수 없습니다.");
		} catch (IllegalAccessException e) {
			System.out.println("접근할 수 없습니다.");
		}
```
