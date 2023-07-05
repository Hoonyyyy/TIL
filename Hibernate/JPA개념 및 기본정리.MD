# JPA
- VO(Value Object) 클래스와 테이블 관계
```
사용자가 입력한 데이터나 비즈니스 로직 수행 결과로 얻은 데이터를 재사용할 수 있도록 데이터베이스에 저장한다.

자바 객체와 데이터베이스의 테이블 사이를 매핑하기 위해 많은 SQL 구문과 자바 코드가 필요할 수 밖에 없다.
```

## Object (VO 객체) Relation (Table) Mapping
![img](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbpFSaF%2FbtrjKOucyGt%2FXkIRcsFemfkciXKUXxtp10%2Fimg.png)

```
ORM은 정확히 일치하지 않는 자바 객체와 테이블 사이를 매핑해준다.

다시 말해, ORM은 자바 객체에 저장된 데이터를 테이블의 ROW 정보로 저장하고, 반대로 테이블에 저장된 ROW를 자바 객체로
매핑해준다.

이 과정에서 사용되는 SQL구문과 자바 코드는 ORM 프레임워크가 자동으로 만들어준다.

DB 연동 기술을 사용할 때 SQL 명령어를 XML 파일에 작성해야 했지만, ORM 이용시 필요한 SQL 자동 생성

또한 DBMS가 변경될때는 DBMS 환경설정만 조금 수정해주면 된다.
```

## JPA (Java Persistence API)
```
EJB의 EntityBean (가장 처음 등장한 것) : 완성도가 높지 않아서 성능이나 복잡한 구현 등의 문제가 있음

Hebernate 프레임워크 (그 다음으로 등장한 것) : 완벽한 ORM 프레임워크로서 자바 객체와 테이블의 ROW를
매핑하는 역할을 수행한다. 오랜 시간을 거치며 기능도 추가되고 성능도 향상되어 ORM의 대표적인 프레임워크가 됨 

TopLink나 Cocobase :  Hebernate 이후 하나씩 등장하기 시작한 프레임워크들

- 이러한 ORM 프레임워크들에 대한 표준화 작업 끝에 그 결과로 JPA가 나오게 되었다.
```

## JDBC와 JPA 공통점
![img](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbaCz4X%2FbtrjLkfh8pW%2FBaDvkKE3Yn8lUX9IkAB3w1%2Fimg.png)
```
JPA(Java Persistence API)는 모든 ORM 구현체들의 공통 인터페이스를 제공함

JDBC는 DB 연동 로직을 구현할 떄, JDBC API의 인터페이스들을 이용하면
실질적인 DB 연동 처리는 해당 DBMS의 드라이버 클래스들이 담당

따라서 DBMS가 변경될 때도 드라이버만 변경하면 JDBC API를 이용하는 애플리케이션 수정x
```

### JPA특징
![img](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F3MAJG%2FbtrjPtb3dcO%2FJe92lhnWYZkeL8z9Q2t3dK%2Fimg.jpg)
```
얘도 쉽게 TopLink 등으로 변환 가능
```

### JPA 단점
- JPA는 복잡한 업무 시스템에서느 쿼리가 많아지고 JOIN이 복잡해져서 사용하기 불편함
- 쓰이는 예 : 프로토타입이나 솔루션 예시



출처 : https://moonhy7.tistory.com/entry/Spring-4%EC%9E%A5-JPA-%EA%B0%9C%EB%85%90-JPA-%ED%8A%B9%EC%A7%95%EA%B3%BC-%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8-%EC%83%9D%EC%84%B1-%EB%B0%8F-%EB%9D%BC%EC%9D%B4%EB%B8%8C%EB%9F%AC%EB%A6%AC-%EB%82%B4%EB%A0%A4%EB%B0%9B%EA%B8%B0
