# 스프링 컨테이너 기본흐름(AbstractApplicationContext).MD

```
package study2;

import org.springframework.context.support.AbstractApplicationContext;
import org.springframework.context.support.GenericXmlApplicationContext;

public class ComputerUser {
	
	public static void main(String[] args) {
		
		AbstractApplicationContext aac
			= new GenericXmlApplicationContext("applicationContext2.xml");
		
		Computer cp = (Computer)aac.getBean("samsung");
		
		cp.buyComputer();
		cp.monitorChoice();
		cp.speakerChoice();
		cp.sellComputer();
		
		System.out.println("----------------------------");
		
		
		Computer cp2 = (Computer)aac.getBean("lg");
		
		cp2.buyComputer();
		cp2.monitorChoice();
		cp2.speakerChoice();
		cp2.sellComputer();
		
	}
	
}
```

### 객체(클래스 생성) -> bean 생성 -> AbstractApplication Context으로 bean 가져오기

- 스프링은 객체를 생성하고 각각의 객체를 연결해주는 조립기 역할을 함
- 여기에 있는 GenericXmlApplication Context 객체가 조립기 기능을 구현한 클래스.
- 조립기에 생성할 객체가 무엇이고, 각 객체를 어떻게 연결하는 지에 대한 정보는 xml에
- Generic~ 에서 xml파일에 정의된 설정 정보 읽고 객체 생성, 각각 객체를 연결한 뒤 내부 보관
- xml을 이용해 생성할 객체를 지정하기 위해 (bean) 태그를 사용
- 스프링 컨테이너가 생성해서 보관하는 객체를 스트링 빈(bean) 객체라고 부르며 일반적으로 자바 객체와 동일
- 빈 객체를 <이름, 빈 객체> 쌍으로 보관함
- 스프링 컨테이너가 보관하고 있는 객체를 사용하고 싶은 경우 빈 객체와 연결되어 있는 이름을 이용해 객체 참조

### 스프링 컨테이너 종류















참조 : https://october-east-sea.tistory.com/157
