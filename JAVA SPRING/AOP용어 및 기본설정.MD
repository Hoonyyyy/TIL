# AOP용어 및 기본설정

### 설정 까먹지 말기
```xml
<!-- AOP라이브러리 추가 -->
		<dependency>
			<groupId>org.aspectj</groupId>
			<artifactId>aspectjrt</artifactId>		
			<version>${org.aspect-version}</version>
		</dependency>
		<dependency>
			<groupId>org.aspectj</groupId>
			<artifactId>aspectjweaver</artifactId>
			<version>1.8.8</version>
		</dependency>
		
		<!-- AspectJ -->
		<dependency>
			<groupId>org.aspectj</groupId>
			<artifactId>aspectjrt</artifactId>
			<version>${org.aspectj-version}</version>
		</dependency>	
```


```
<!-- 
	AOP용어 및 기본설정
		1. 조인트 포인트(Jointpoint)
			- 클라이언트가 호출하는 모든 비즈니스 메서드
			- 포인트컷의 후보가 된다.
			
		2. 포인트컷(pointcut)
			- 조인트 포인트 중에서 필터링된 메서드
			- 우리가 원하는 특정 메서드에서만 횡단 관심에 해당하는 공통기능을
				수행하기 위해 포인트컷으로 필터한다.
				
			- expression
				* | com.mycompany.biz.. |*impl| *(..)
				* | com.mycompany.biz.. |*impl|get*(..)
				1)			2)			3)		4)
				
			1) 리턴타입	
				*		모든 리턴타입 적용
				void	리턴타입이 void인 메서드
				!void	리터타입이 void가 아닌 메서드
				
			2) 패키지 경로
				com.mycompany.biz	해당하는 패키지만 선택
				com.mycompany.biz..	biz패키지로 시작하는 모든 패키지
				com.mycompany..impl	com.mycompany로 시작하면서,, 마지막 패키지 이름이 impl로 끝나는 패키지
					
			3) 클래스명
				BoardServiceimpl	해당 클래스
				* impl				클래스 이름이 impl로 끝나는 모든 클래스만 선택
				BoardService + 		해당 클래스에서 파생된 모든 자식클래스 선택 (인터페이스 동일)
				
			4) 메서드명
				*(..)				모든 메서드 선택
				get(..)				메서드 이름이 get으로 시작하는 모든 메서드 선택
				
			5) 매개변수
				(..)				기본설정, 매개변수의 개수 타입의 제약이 없다.
				(*)					반드시 1개 이상의 매개변수를 갖고 있는 메서드만 선택
				(com.mycompany.user.UserVO)	UserVO를 가지고 있는 메서드만 선택(패키지명까지 필수 기입)
				(!com.mycompany.user.UserVO) "		가지지 않는 메서드만 선택
				(Integer...)		한 개 이상의 매개변수이고 첫번째 매개변수가 Integer타입의 메서드만 선택
				(Integer,*)			반드시 두 개 이상의 매개변수이고, 시작은 Integer타입인 메서드만 선택
				
		3. 어드바이스(Advice)
			- 횡단관심에 해당하는 공통기능의 코드를 의미
			- 수행시점
				. before
				. after
					- after returning 	: 비즈니스 메서드가 성공적으로 실행되고나서 그 결과로 생성된 데이터가 리턴되면 동작
					- after throwing 	: 비즈니스 메서드가 실행중 예외가 발생되면 동작 (try~catch에서 catch 해당)
					- after				: 비즈니스 메서드 실행후 무조건 실행 (finally에 해당)
					
				. around

 -->
```


### XML설정
```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xmlns:context="http://www.springframework.org/schema/context"
	xmlns:p="http://www.springframework.org/schema/p"
	xmlns:aop="http://www.springframework.org/schema/aop"
	xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
		http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context-4.3.xsd
		http://www.springframework.org/schema/aop http://www.springframework.org/schema/aop/spring-aop-4.3.xsd">
<!-- 
	Spring Annotation
		. @AutoWired
		. @Qualifier
		. @Injection
		. @Resource
		
		. @Service		: 비즈니스 로직처리한 서비스클래스
		. @Respository	: 데이터베이스 연동 DAO
		. @Controller	: 사용자 요청을 제어하는 컨트롤러
 -->
 <context:component-scan base-package="com.mycompany.biz"/>
 
 <bean id="logA" class="com.mycompany.biz.common.LogAdvice"></bean>
 <bean id="logB" class="com.mycompany.biz.common.Log4jAdvice"></bean>
 
 <aop:config>
 	<aop:pointcut id="allPointcut" expression="execution(* com.mycompany.biz..*impl.*(..))" />
 	<aop:aspect ref="logB">
 		<aop:before pointcut-ref="allPointcut" method="printLogging"/>
 	</aop:aspect>
 
 </aop:config>
</beans>
```

### 오류 처리
- board에 0번글은 등록할 수 없다고 해놓았을때
- 오류 처리 문법 적어두기
- applicationContext.xml에 오류처리할 메서드 적어두기

```java
	@Override
	public void insertBoard(BoardVO vo) {
		
		
		// 오류발생 추가
		if(vo.getSeq()==0) {
			throw new IllegalArgumentException("0번 글은 등록할 수 없습니다.");
		}
		boardDAO.insertBoard(vo);
		System.out.println(">>>>>>>> insert 로직 수행");
	}
```

```java
package com.mycompany.biz.common;

import org.aspectj.lang.JoinPoint;

public class AfterThrowingJoinPoint {
	
	// 비즈니스 메서드가 실행중 예외가 발생되면 동작하는 어드바이스
	public void exceptionLog(JoinPoint jp, Exception exceptObj) {
		
		// 클라이언트가 요청한 메서드 이름
		String method = jp.getSignature().getName(); 
		System.out.println("[예외처리]" + method + "()메서드 수행중 발생된 예외메시지 : " + exceptObj.getMessage());
		
		if(exceptObj instanceof IllegalArgumentException) {
			System.out.println("부적합한 값이 입력되었습니다.");
		} else if(exceptObj instanceof NumberFormatException) {
			System.out.println("숫자 형식의 값이 아닙니다.");
		} else if(exceptObj instanceof Exception) {
			System.out.println("문제가 발생되었습니다.");
		}
		
	}
	
}

```

```xml
 <bean id="logA" class="com.mycompany.biz.common.LogAdvice"></bean>
 <bean id="logB" class="com.mycompany.biz.common.Log4jAdvice"></bean>
 <bean id="afterThrowing" class="com.mycompany.biz.common.AfterThrowingJoinPoint"></bean>
 
 <aop:config>
 	<aop:pointcut id="allPointcut" expression="execution(* com.mycompany.biz..*impl.*(..))" />
 	
 	<aop:aspect ref="afterThrowing">
 		<aop:after-throwing pointcut-ref="allPointcut" method="exceptionLog" throwing="exceptObj"/>
 	</aop:aspect>
 
 </aop:config>
```

### 오류처리
- 0번은 등록할수 없을때 오류처리

```
package com.mycompany.biz.user;

import java.util.ArrayList;

import org.springframework.context.support.AbstractApplicationContext;
import org.springframework.context.support.GenericXmlApplicationContext;

import com.mycompany.biz.board.BoardVO;
import com.mycompany.biz.board.impl.BoardService;
import com.mycompany.biz.user.impl.UserService;

public class UserServiceClient {

	public static void main(String[] args) {
		
		AbstractApplicationContext container = new GenericXmlApplicationContext("applicationContext.xml");
		UserService userService = (UserService)container.getBean("userService");
		
		UserVO vo = new UserVO();
		vo.setId("admin");
		vo.setPassword("1234");
		
		UserVO user = (UserVO)userService.getUser(vo);
		
		BoardService boardService = (BoardService)container.getBean("boardService");
		
		if(user != null) {
			System.out.println(user.getName()+"님 환영합니다.");
		} else {
			System.out.println("로그인 실패");
		}
		
		//userService.deleteUser(user);
		
		
		System.out.println("ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ");
		
		ArrayList<UserVO> userList = (ArrayList<UserVO>) userService.getUserList();
		
		for(UserVO users : userList) {
			System.out.println(users.toString());
		}
		
		// 게시판 글추가
		BoardVO board = new BoardVO();
		board.setSeq(0);
		board.setTitle("월요일");
		board.setWriter("글쓴이 미상");
		board.setContent("내용없음.....");
		
		boardService.insertBoard(board);
		
		ArrayList<BoardVO> boardList = (ArrayList<BoardVO>) boardService.getBoardList();
		
		for(int i=0; i<boardList.size();i++) {
			board = (BoardVO)boardList.get(i);
			System.out.println(board.toString());
		}
		
		
		container.close();
		
	}
	
}

```

