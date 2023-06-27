# AOP 트랜잭션
  
## 데이터 일관성과 안전한 데이터 조작을 보장하기 위해 사용됨
- 트랜잭션은 데이터베이스 상태를 변화시키는 작업의 논리적 단위
- 여러 개의 데이터베이스 작업이 하나의 트랜잭션으로 묶일 때, 이 작업은 모두 성공하거나, 모두 실패해야함

## ACID
### 원자성(Atomicty)
- 트랜잭션은 모든 작업이 완벽하게 수행되거나 아무런 작업도 수행되지 않은 상태를 보장
- 모든 단계가 성공적으로 실행되거나, 어떠한 단계에서 오류가 발생하면 이전 상태로 롤백

### 일관성(Consistency)
- 트랜잭션이 시작하기 전과 후에도 데이터베이스는 일관된 상태를 유지해야 함

### 독립성(Isolation)
- 동시에 실행 중인 여러 개의 트랜잭션으 서로 영향을 주지 않고 독립적으로 실행되는것처럼 보여야함
- 하나의 트랜잭션이 다른 트랜잭션의 작업을 간섭하지 않도록 격리 수준을 제공

### 지속성(Durability)
- 트랜잭션이 성공적으로 안료되면, 그 결과는 영구적으로 데이터에 ㅏㄴ영되어야 함
- 시스템 장애 또는 전원 손실과 같은 문제가 발생하더라도 데이터는 안전하게 보존되어야 함

### 종합
- 이렇게 트랜잭션을 사용하면 데이터의 무결성과 일관성을 보장할 수 있음
- 예기치 않은 문제가 발생했을 때도 데이터베이슬 이전의 일관된 상태로 롤백할 수 있음
- 이는 데이터베이스 시스템에서 안정성과 신뢰성을 유지하는 데 도움 됨

### 예시는 은행 입출금할때

## @Transaction을 이용한 트랜잭션 vs AOP이용한 트랜잭션

### @Transaction
- 장점 : 특별한 설정없이 쉽게 사용, 원하는 곳에서만 사용
- 단점 : 어노테이션 누락되거나 여러 메서드에 걸쳐 사용시 적용 안될수도 있음, 외부 라이브러리 x
```java
@Service
@Transactional
public class BoardServiceImpl implements BoardService {

    @Autowired
    private BoardMapper boardMapper;
    
    @Override
    public BoardDto selectBoardDetail(int boardIdx) throws Exception{
        boardMapper.updateHitCount(boardIdx); // 조회수 올리기
        int a = 10/0;
        BoardDto board = boardMapper.selectBoardDetail(boardIdx); // 게시글 보여주기

        return board;
    }

}
```

### AOP 이용한 트랜잭션
- 장점 : 공통으로 트랜잭션이 적용되기 때문에 트랜잭션이 누락될 일이 없다, 외부 라이브러리 o
- 단점 : 원하는 곳에서만 트랜잭션 적용 힘듬 ->
- 특정 비즈니스 로직에서는 에러 발생한 시점까지 데이터가 저장되어야 하는데, 이런 것까지 모두 rollback 됨
``` java
package com.example.board.board.aop;

import org.springframework.aop.Advisor;
import org.springframework.aop.aspectj.AspectJExpressionPointcut;
import org.springframework.aop.support.DefaultPointcutAdvisor;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.transaction.PlatformTransactionManager;
import org.springframework.transaction.interceptor.MatchAlwaysTransactionAttributeSource;
import org.springframework.transaction.interceptor.RollbackRuleAttribute;
import org.springframework.transaction.interceptor.RuleBasedTransactionAttribute;
import org.springframework.transaction.interceptor.TransactionInterceptor;

import java.util.Collections;

@Configuration
public class TransactionAspect {

    private static final String AOP_TRANSACTION_METHOD_NAME="*";
    private static final String AOP_TRANSACTION_EXPRESSION="execution(* board.service.*Impl.*(..))";

    @Autowired
    private PlatformTransactionManager transactionManager;

    @Bean
    public TransactionInterceptor transactionAdvice(){
        MatchAlwaysTransactionAttributeSource source = new MatchAlwaysTransactionAttributeSource();
        RuleBasedTransactionAttribute transactionAttribute = new RuleBasedTransactionAttribute();
        transactionAttribute.setName(AOP_TRANSACTION_METHOD_NAME);
        transactionAttribute.setRollbackRules(Collections.singletonList(new RollbackRuleAttribute(Exception.class)));
        source.setTransactionAttribute(transactionAttribute);

        return new TransactionInterceptor(transactionManager, source);
    }

    @Bean
    public Advisor transactionAdviceAdvisor(){
        AspectJExpressionPointcut pointcut = new AspectJExpressionPointcut();
        pointcut.setExpression(AOP_TRANSACTION_EXPRESSION);
        return new DefaultPointcutAdvisor(pointcut, transactionAdvice());
    }
}
```

### 다른 aop 예시는 xml로
```xml
	<context:component-scan base-package="com.mycompany.biz" />
	<aop:aspectj-autoproxy></aop:aspectj-autoproxy>
	
	<context:property-placeholder location="classpath:config/database.properties" />
	<bean id="dataSource" class="org.apache.commons.dbcp.BasicDataSource" destroy-method="close">
		<property name="driverClassName" value="${jdbc.driver}" />
		<property name="url" value="${jdbc.url}" />
		<property name="username" value="${jdbc.username}" />
		<property name="password" value="${jdbc.password}" />
	</bean>


	<bean id="jdbcTemplate" class="org.springframework.jdbc.core.JdbcTemplate">
		<property name="dataSource" ref="dataSource" />
	</bean>
	
	

	<bean id="txManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager"> 
		<property name="dataSource" ref="dataSource"></property>
	</bean>

	<tx:advice id="txAdvice" transaction-manager="txManager"> 
		<tx:attributes>
			<tx:method name="get*" read-only="true"/>  
			<tx:method name="*"/> 
		</tx:attributes>
	</tx:advice>
	
	<aop:config>
		<aop:pointcut id="txPointcut" expression="execution(* com.mycompany.biz..*.*(..))"/>
		<aop:advisor  pointcut-ref="txPointcut"  advice-ref="txAdvice"/> 
```




