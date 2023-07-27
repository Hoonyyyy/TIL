# Presentation Layer, Business Layer

여기 정리하는것은 언제나 변경될 수 있음 그때그때마다 쓰는것

### Presentation Layer
- 사용자와 커뮤니케이션을 담당하는 화면

### Business Layer
- 사용자의 요청에 대한 비즈니스 로직 처리를 담당

#### 이 구조에 핵심 요소는 Controller, ServiceImpl, DAO 클래스
- Controller 클래스는 사용자의 요청을 제어하고,
- ServiceImpl 클래스는 실질적인 비즈니스 로직을 처리함
- DAO 클래스는 실질적인 데이터 베이스 연동을 담당한다.

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbylxl5%2FbtrVVQ3cPit%2FfMMcWCLcwMKXqaYeK3Z920%2Fimg.jpg">


- @Component 어노테이션은 스프링컨테이너가 해당 클래스 객체를 생성하도록 설정할 수 있다.
- 그렇지만 시스템을 구성하는 이 모든 클래스에 @Component를 할당하면
- 어떤 클래스가 어떤 역할을 수행하는지 파악하기 어렵다.
- 스프링 프레임워크는 이런 클래스들을 분류하기 위해 @Component를 상속하여 다음과 같이 3개 어노테이션을 추가로 제공한다.
```
@Service    -  비즈니스 로직을 처리하는 Service 클래스
@Repository -  데이터베이스 연동을 처리하는 DAO
@Controller -  사용자 요청을 제어하는 Controller
```

### 리스너를 등록하여 비즈니스 컴포넌트 호출 설정
(web.xml에 ContextLoaderListener 적용하기)
- DispatcherServlet이 생성한 스프링 컨테이너는 Controller 객체들만 생성함
- 하지만 Controller 객체들이 생성되기 전에 누군가 먼저 resource소스 폴더에 있는 ~.xml파일 들을
- 읽어 비즈니스 컴포넌트들을 메모리에 생성해야 한다.
- 이때 사용하는 클래스가 스프링에서 제공하는 ContextLoaderListener임
- 사용예시
- web.xml
``` xml
	<!-- 리스너 -->
	<context-param>
		<param-name>contextConfigLocation</param-name>
		<param-value>classpath:applicationContext.xml</param-value>
	</context-param>

	<listener>
		<listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
	</listener>
	
	
	<servlet>
		<servlet-name>action</servlet-name>
		<servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
		<init-param>
			<param-name>contextConfigLocation</param-name>
			<param-value>/WEB-INF/config/presentation-layer.xml</param-value>
		</init-param>
		<load-on-startup>1</load-on-startup>
	</servlet>
	<servlet-mapping>
		<servlet-name>action</servlet-name>
		<url-pattern>/</url-pattern>
	</servlet-mapping>
	
	<welcome-file-list>
  		<welcome-file>start.jsp</welcome-file>
  	</welcome-file-list>
```

- presentation-layer.xml (controller와 클라이언트에 관한것들)
```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xmlns:context="http://www.springframework.org/schema/context"
	xmlns:mvc="http://www.springframework.org/schema/mvc"
	xsi:schemaLocation="http://www.springframework.org/schema/mvc http://www.springframework.org/schema/mvc/spring-mvc-4.3.xsd
		http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
		http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context-4.3.xsd">
	
	<context:component-scan base-package="com.traveltogether.view"/>
	<context:component-scan base-package="com.traveltogether.biz.chat"/>



	<!-- 파일 업로드 처리 -->
	<bean id="multipartResolver" class="org.springframework.web.multipart.commons.CommonsMultipartResolver">
		<property name="maxUploadSize" value="1000000000"/>
		<property name="maxInMemorySize" value="1000000000"></property>
	</bean>
	
	<!-- 예외처리 -->
	<mvc:annotation-driven/>
	<mvc:default-servlet-handler/>
	
   <bean id="exceptionResolver" class="org.springframework.web.servlet.handler.SimpleMappingExceptionResolver">
      <property name="defaultErrorView" value="common/error.jsp"></property>      
   </bean>	
	
	
		 
</beans>
```

- applicationContext.xml(비즈니스로직과 관련된것)
``` xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
   xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
   xmlns:context="http://www.springframework.org/schema/context"
   xmlns:aop="http://www.springframework.org/schema/aop"
   xmlns:tx="http://www.springframework.org/schema/tx"
   xmlns:mvc="http://www.springframework.org/schema/mvc"
   xmlns:c="http://www.springframework.org/schema/c"
   xmlns:mybatis-spring="http://mybatis.org/schema/mybatis-spring"
   xsi:schemaLocation="http://www.springframework.org/schema/mvc http://www.springframework.org/schema/mvc/spring-mvc-4.3.xsd
      http://mybatis.org/schema/mybatis-spring http://mybatis.org/schema/mybatis-spring-1.2.xsd
      http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
      http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context-4.2.xsd
      http://www.springframework.org/schema/aop http://www.springframework.org/schema/aop/spring-aop-4.2.xsd
      http://www.springframework.org/schema/tx http://www.springframework.org/schema/tx/spring-tx-3.2.xsd">

   <context:component-scan base-package="com.traveltogether.biz" />
   
   
   
   <aop:aspectj-autoproxy></aop:aspectj-autoproxy>



   <!-- DataSource 설정 -->
   <context:property-placeholder location="classpath:config/database.properties" />
   
   <bean id="dataSource" class="org.apache.commons.dbcp.BasicDataSource" destroy-method="close">
      <property name="driverClassName" value="${jdbc.driver}" />
      <property name="url" value="${jdbc.url}" />
      <property name="username" value="${jdbc.username}" />
      <property name="password" value="${jdbc.password}" />
   </bean>

	<bean id="sqlSession" class="org.mybatis.spring.SqlSessionFactoryBean">
		<property name="dataSource" ref="dataSource"/>
		<property name="configLocation" value="classpath:sql-map-config.xml"/>
	</bean>

	<bean class="org.mybatis.spring.SqlSessionTemplate">
		<constructor-arg ref="sqlSession"></constructor-arg>
	</bean>
  

	<!-- MyBatis 트랜잭션 매니저 설정 -->
	<bean id="transactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
	    <property name="dataSource" ref="dataSource" />
	</bean>
	
	<!-- 트랜잭션 어드바이스 설정 -->
	<tx:advice id="txAdvice" transaction-manager="transactionManager">
	    <tx:attributes>
	        <tx:method name="get*" read-only="true" />
	        <tx:method name="*" />
	    </tx:attributes>
	</tx:advice>
	
	<!-- AOP 설정 -->
	<aop:config>
	    <aop:pointcut id="txPointcut" expression="execution(* com.traveltogether.biz..*.*(..))" />
	    <aop:advisor pointcut-ref="txPointcut" advice-ref="txAdvice" />
	</aop:config>
   
   
   <!-- Spring과 JPA 연동 설정 -->
   <!-- 
      . HibernateJpaVendorAdapter : JPA 벤더(Database) 지정할 때 사용하는 하이버네이트의 클래스
      . LocalContainerEntityManagerFactoryBean : EntityManager객체를 가져오는 클래스
                              - 여기에  japVendorAdapter를 의존주입하면 된다.    
    -->
<!--    <bean id="jpaVendorAdapter"
      class="org.springframework.orm.jpa.vendor.HibernateJpaVendorAdapter"></bean>
   <bean id="entityManagerFactory"
      class="org.springframework.orm.jpa.LocalContainerEntityManagerFactoryBean">
      <property name="dataSource" ref="dataSource"></property>
      <property name="jpaVendorAdapter" ref="jpaVendorAdapter"></property>
      <property name="packagesToScan" value="com.mycompany.biz.board"></property>
      <property name="jpaProperties">
         <props>
            <prop key="hibernate.dialect">org.hibernate.dialect.MySQLDialect</prop>
            <prop key="hibernate.show_sql">true</prop>
            <prop key="hibernate.format_sql">true</prop>
            <prop key="hibernate.use_sql_comments">true</prop>
            <prop key="hibernate.id.new_generator_mappings">true</prop>
            <prop key="hibernate.hbm2ddl.auto">update</prop>    중요: create/update등... 
         </props>
      </property>
   </bean> -->

   
   
</beans>
```
