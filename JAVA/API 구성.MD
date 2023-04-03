## API 구성
모듈
- ***여러 패키지와 이미지 등의 자원을 모아 놓은 컨테이너***
- JDK 9부터 자바 API의 모든 클래스들(자바 실행 환경)을 패키지 기반에서 모듈들로 완전히 재구성
- 응용프로그램 역시 여러 개의 모듈로 분할하여 작성 가능

>> 클래스들은 패키지로 만들고, 다시 패키지를 모듈로 만듦

패키지
- 서로 관련된 클래스와 인터페이스의 컴파일 된 클래스 파일들을 하나의 디렉터리에 묶어 놓은 것

패키지명과 클래스의 경로명
- ***점(.)으로 연결***
- Project.FileIO.Tools.class  , ProjectUI.Tools.class
 
주요패키지
- ***java.lang***
1) 자바 language 패키지 ( 스트링, 수학함수, 입출력 등 자바 프로그래밍에 필요한 기본적인 클래스와 인터페이스)
2) 자동으로 import, import 문 필요 없음
- java.util
1) 자바 유틸리티 패키지 (날짜, 시간, 백터, 해시맵 등과 같은 다양한 유틸리티 클래스와 인터페이스 제공)

- java.io
1) 키보드, 모니터, 프린터, 디스크 등에 입출력을 할 수 있는 클래스와 인터페이스 제공

- java.awt
1) 자바 GUI 프로그래밍을 위한 클래스와 인터페이스 제공

-javax.swing
1) 자바 GUI 프로그래밍을 위한 스윙 패키지


## Object 클래스
- java.lang 패키지
- ***모든 클래스의 슈퍼 클래스***
1) 모든 클래스에 강제 상속
2) 모든 객체가 공통으로 가지는 객체의 속성을 나타내는 메서드 보유
메서드 : (boolean equals(Object obj)), (Class getClass()), (int hashCode()), (String toString())
(void notify()), (void notifyAll()), (void wait())


### object
```java
package object;

class Rect {
	// 너비, 높이
	// 생성자로 초기화시킨다
	
	// equals(Object obj) 이용해서 
	//  너비*높이  == obj.width * obj.height 같다면 true, 다르면 false
	
	int width;
	int height;
	
	Rect(int width, int height) {
		this.width = width;
		this.height = height;
	}
	
	public boolean equals(Rect r) {
		if(width == r.width && height == r.height)
			return true;
		else
			return false;
	}
}

public class Obj4 {
	public static void main(String[] args) {
		
		Rect a = new Rect(10, 20);
		Rect b = new Rect(10, 20);
		Rect c = new Rect(10, 30);
		
		if(a.equals(b)) {
			System.out.println("a와 b는 같다");
		} else {
			System.out.println("a와 b는 다르다");
		}
		
		if(a.equals(c)) {
			System.out.println("a와 c는 같다");
		} else {
			System.out.println("a와 c는 다르다");
		}	
	}
}
```

## Wrapper 클래스
- 이름이 Wrapper인 클래스는 존재하지않음 (Byte Short Integer Long 등등등 같은것)
- 용도
1) 기본타입의 값을 객체로 다룰 수 있게 함

## String 클래스
- 스트링 객체는 수정 불가능 스트링
- 비교 시 반드시 equals()를 사용 - equals()는 내용을 비교하기 때문

방법1: 스트링 리터럴로 스트링 객체 생성
```java
String str1 = "abcd";
```

방법2: String 클래스의 생성자를 이용하여 스트링 생성
```java
char data[] = {'a','b','c','d'};
String str2 = new String(data);
String str3 = new String("abcd");
```


## StringBuffer클래스
가변 크기의 문자열 저장 클래스

## StringTokenizer클래스
- java.util.StringTokenizer
1) 하나의 문자열을 여러 문자열로 분리
2) 문자열을 분리할 때 사용되는 기준 문자: 구분 문자(delimiter)
- ***토큰***(tokne) : 구분 문자로 분리된 문자

```java
package stringtokenizer;

import java.util.StringTokenizer;

public class Token1 {
	public static void main(String[] args) {
		
		String query = "name=홍길동&address=신촌&age=21";
		
		StringTokenizer st = new StringTokenizer(query, "&");
		
		int n = st.countTokens();
		System.out.println("분리된 토큰은 몇개인가? " + n + "개");
		
		for(int i=0;i<n;i++) {
			String token = st.nextToken();
			System.out.println(token);
		}
		
	}
}

```

## Math클래스
난수 발생
- static double random()
1) 산술 연산 메서드 제공 java.lang.Math
2) 모든 메서드는 static 타입 : 클래스 이름으로 바로 호출해야 


## Calendar 클래스
Calendar 클래스의 특징
- java.util 패키지
- 시간과 날짜 정보 저장 관리
1) 년, 월, 일, 요일, 시간, 분, 초, 밀리초, 오전, 오후 등
2) Calendar 클래스의 각 시간 요소를 설정하거나 알아내기 위한 필드


- 어쩌다 알게된건데 AM_PM을 HOUR ( AM_PM + HOUR을 객체로 넣으면 ) +1이 돼서 출력됨
```java
package calendar;

import java.util.Calendar;

public class Calendar1 {
	public static void main(String[] args) {
		
		Calendar now = Calendar.getInstance(); // 싱글톤
		int yy = now.get(Calendar.YEAR);
		int mm = now.get(Calendar.MONTH)+1; // 0부터 시작이기에 +1 해줘야함
		int dd = now.get(Calendar.DATE);
		int ampm = now.get(Calendar.AM_PM);
		int hour = now.get(Calendar.HOUR);
//		int hourofday = now.get(Calendar.HOUR_OF_DAY);
		int min = now.get(Calendar.MINUTE);
		int sec = now.get(Calendar.SECOND);
		
		
		
		System.out.print(yy + "년" + mm + "월" + dd + "일 ");
		
		int week = now.get(Calendar.DAY_OF_WEEK); // 일요일: 1
		
		switch(week) {
		case 1: System.out.print("일요일"); break;
		case 2: System.out.print("월요일"); break;
		case 3: System.out.print("화요일"); break;
		case 4: System.out.print("수요일"); break;
		case 5: System.out.print("목요일"); break;
		case 6: System.out.print("금요일"); break;
		case 7: System.out.print("토요일"); break;
		}
		
		System.out.println(hour+"시 "+min+"분 "+sec+"초");
	}
}

```
