## prepareStatement와 statement의 차이

둘의 차이를 알기전에 '캐시'를 먼저 알야아한다.

## 캐시?
- 데이터나 명령어를 임시로 저장하는 고속 메모리이다.
- 데이터나 명령어에 빠르게 접근할 수 있도록 도와준다.
- 일반적으로 캐시는 CPU코어와 주 메모리 사이에서 동작하며, 주 메모리보다 빠른 접근 시간을 제공함
- 캐시는 시스템 성능을 향상시키고 응용 프로그램의 실행 속도를 향상시키는 데 중요한 역할을 함


## Statement
- Statement 인터페이스는 정적인  SQL문을 실행하기 위한 메서드를 제공함
- Statement를 사용하면 SQL 문을 실행할 때마다 데이터베이스 서버에 해당 SQL문을 컴파일하고 실행함
- 따라서 SQL문을 반복해서 실행할 때마다 데이터베이스 서버에 재컴파일 비용이 발생함
- 캐시를 사용하지 않기 때문에 반복 실행 시 성능 저하가 발생할 수 있다.

## prepareStatement
- prepareStatement는 동적인 SQL문을 실행하기 위한 메서드를 제공한다.
- prepareStatement를 사용하면 SQL문을 미리 컴파일하여 데이터베이스 서버에 보관함
- SQL문을 실행할 때마다 컴파일하는 대신, 이미 컴파일된 SQL 문을 재사용함
- 이렇게 함으로써 데이터베이스 서버에 재컴파일 비용을 절약하고 성능을 향상시킬 수 있음
- 캐시를 사용하기 때문에 동일한 SQL문을 반복 실행할 떄 성능이 향상됨

## 예시
```java
// Statement 사용 예시
Statement statement = connection.createStatement();
ResultSet resultSet = Statement.executeQuery("SELECT * FROM users");

// prepareStatement 사용 예시
PreparedStatement preparedStatement = connection.prepareStatement("SELECT * FROM users WHERE age > ?");
preparedStatement.setInt(1, 18);
ResultSet resultSet = preparedStatement.executeQuery();
```

- 예시에서 Statement를 사용할 경우 매번 SQL문을 데이터 베이스에 서버에 보내고 실행함
- 반면 prepareStatement를 사용할 경우, SQL문이 컴파일되고 데이터베이스 서버에 캐시되어 재사용됨
- 그러므로 prepareStatement를 사용하면 성능상의 이점이 있다.

### prepareStatement는 매개변수화된 쿼리를 사용할 수 있어 SQL 인젝션 공격을 방지하는데 도움됨
- 예시
```jsp
String name = "John";
int age = 25;

// Statement 사용 예시
String query = "SELECT * FROM users WHERE name='" + name + "' AND age=" + age;
Statement statement = connection.createStatement();
ResultSet resultSet = statement.executeQuery(query);

// prepareStatement 사용 예시
String query = "SELECT * FROM users WHERE name=? AND age=?";
PreparedStatement preparedStatement = connection.prepareStatement(query);
preparedStatement.setString(1, name);
preparedStatement.setInt(2, age);
ResultSet resultSet = preparedStatement.executeQuery();
```

- 예시에서 Statement는 문자열 연결을 하기에 SQL 인젝션 공격을 할 수 있음
- 반면에 prepareStatement를 사용하면 쿼리문에 매개변수를 사용하여 값을 전달함
- 이는 쿼리문의 컴파일된 버전과 함께 전달되어 보안상 안전한 방식으로 작업할 수 있다. 따라서
- prepareStatement를 사용하면 SQL 인젝션 공격을 예방할 수 있다.

### 그러나 무조건적으로 prepareState가 좋다는것은 아니다.
---------------------------------------------------------------------------------------

## Statement 장점
- 단순함 : 문자열을 직접 작성하기에
- 쿼리유형 : 정적쿼리 및 단순한 쿼리에는 더 간단하게 사용가능
- 기능제약없음 : 특정 데이터베이스 기능이나 문법을 사용해야 할 때에는 Statement를 선택할 수 있다.

## prepareStatement 장점
- 성능 개선 : 쿼리를 미리 컴파일하고 캐시에 저장하기 때문에 반복적인 쿼리 실행에서 성능 향상이 있다.
- 보안 강화 : 매개변수화된 쿼리를 사용하여 SQL 인젝션 공격을 방지할 수 있다.
- 가독성 : 쿼리문에 매개변수를 사용하기 때문에 가독성이 좋아짐
- 유연성 : 매개변수를동적으로 변경하여 다양한 쿼리를 실행할 수 있다.









