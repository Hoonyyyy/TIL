# 스프링 컨테이너 기본흐름(AbstractApplicationContext).MD

## 객체(클래스 생성) -> bean 생성 -> AbstractApplication Context으로 bean 가져오기

- 스프링은 객체를 생성하고 각각의 객체를 연결해주는 조립기 역할을 함
- 여기에 있는 GenericXmlApplication Context 객체가 조립기 기능을 구현한 클래스.
- 조립기에 생성할 객체가 무엇이고, 각 객체를 어떻게 연결하는 지에 대한 정보는 xml에
- Generic~ 에서 xml파일에 정의된 설정 정보 읽고 객체 생성, 각각 객체를 연결한 뒤 내부 보관
- xml을 이용해 생성할 객체를 지정하기 위해 (bean) 태그를 사용
- 스프링 컨테이너가 생성해서 보관하는 객체를 스트링 빈(bean) 객체라고 부르며 일반적으로 자바 객체와 동일
- 빈 객체를 <이름, 빈 객체> 쌍으로 보관함
- 스프링 컨테이너가 보관하고 있는 객체를 사용하고 싶은 경우 빈 객체와 연결되어 있는 이름을 이용해 객체 참조

## 스프링 컨테이너 종류

- BeanFactory
```
스프링은 단순한 DI를 위한것이 아니라 (트랜잭션, 자바 코드 기반 스프링 설정, 어노테이션 이용한 빈설정
, 스프링을 이용한 웹 개발 등
을 이용하기 위해서인데 부가적인 기능을 사용하기 위해서는 보통 ApplicationContext를 사용함	
```
- AbstractApplicationContext
```
컨테이너 종료(close)와 같은 기능을 제공해 주는객체
```

- GenericXmlApplicationContext
```
AbstractApplicationContext 객체를 상속 받아 만드는 클래스. xml 파일에서 스프링 빈 설정 정보를 
읽어오는 역할.

GenericXmlApplicationContext 객체를 생성할 때 파라미터 값으로 xml의 경로를 전달하여 설정 파일로 사용함.

GenericXmlApplicationContext 객체는 전달받은 xml 파일에서 설정 정보를 읽어와서 스프링 빈 객체를
생성하고 프로퍼티 값을 설정함.

생성된 스프링 빈 객체는 getBean() 이라는 메서드를 사용해서 구현함.

getBean() 메서드의 첫번쨰 파라미터는 구현하고자 하는 스프링 빈 객체의 고유한 id이름이며,
두번째 파라미터는 그 객체의 타입을 의미함.
```

### AbstractApplicationContext (실행페이지)
```java
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

### applicationContext
```java
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd"
	xmlns:p="http://www.springframework.org/schema/p">
	
	
	<bean id="aMo" class="study2.Amonitor"/>
	<bean id="aS" class="study2.AppleSpeaker"/>	
	<bean id="samsung" class="study2.SamsungComputer" p:monitor-ref="aMo" p:speaker-ref="aS"/>
	
	<bean id="bMo" class="study2.Bmonitor"/>
	<bean id="sS" class="study2.SonySpeaker"/>	
	<bean id="lg" class="study2.LgComputer" p:monitor-ref="bMo" p:speaker-ref="sS"/>
	
	
</beans>

```






참조 : https://october-east-sea.tistory.com/157
