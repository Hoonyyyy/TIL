# JNDI
```java
/*
	JNDI ?
		- Java Naming and Directory Interface	API
		- 디렉터리 서비스에 접근하는 필요한 API이다.
		- 애플리케이션은 API를 통해서 자원(서버나 메시징시스템등)을 찾을 수 있다.
		- JDBC를 특히 데이터소스라 한다.
		- 자원을 서버에 등록할때 고유한 JNDI이름을 붙인다.

		- 서버에서 자원을 찾을때 기본 JNDI이름
			java:comp/env		-	응용프로그램 환경항목
			java:comp/env/jdbc	-	jdbc데이터소스 
				~~~
*/
```

## jndi 설치
```
https://commons.apache.org/



DBCP
왼쪽 download
Binaries 위에꺼 다운 ( 반디집 필요 )

Pool
이하 동문

lib에 jar 넣기

```

### Datasource
```java
DataSource ds = (DataSource)initialContext.lookup("java:comp/env/jdbc/myDB");
// DataSource(JDBC자원)
//	- 컨넥션 풀의 connection을 관리하기 위한 객체이다.
//	- DataSOurce객체를 통해서 Connection을 획득, 반납등의 작업을 한다.
```

### tomcat context.xml
```xml
	<Resource
		name="jdbc/myDB"
		auth="Container"
		type="javax.sql.DataSource"
		maxActive="10" maxIdle="3" maxWait="10000"
		username="root"
		password="mysql"
		driveClassName="com.mysql.jdbc.Driver"
		url="jdbc:mysql://localhost:3306/studyDB"
		closeMethod="close">
	</Resource>
	<!-- 
		. name : JDBC이름
		. auth : 자원관리자 - Container
		. type : 자원의 리소스이름 - DataSource클래스 (패키지이름까지 포함)
		. maxActive : 최대 연결가능한 connection수(기본 20개)
		. maxIdle : 사용가능한 컨넥션이 없을때 회수대기시간
	 -->
```

### web.xml
```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://xmlns.jcp.org/xml/ns/javaee" xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_3_1.xsd" version="3.1">
  <display-name>Ch23</display-name>
	
	<resource-ref>
		<res-ref-name>jdbc/myDB</res-ref-name>
		<res-type>javax.sql.DataSource</res-type>
		<res-auth>Container</res-auth>
	</resource-ref>
	
	<!-- 리스너 배치 -->
<!-- 	<listener>
		<listener-class>study.listeners.ContextLoaderListener</listener-class>
	</listener> -->
	
	<servlet>
		<servlet-name>AppInitServlet</servlet-name>
		<servlet-class>study.servlets.AppInitServlet</servlet-class>
		<load-on-startup>1</load-on-startup>
	</servlet>
  
  <welcome-file-list>
    <welcome-file>index.html</welcome-file>

  </welcome-file-list>
</web-app>
```
