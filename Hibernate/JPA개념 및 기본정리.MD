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
- EJB의 EntityBean (가장 처음 등장한 것) : 완성도가 높지 않아서 성능이나 복잡한 구현 등의 문제가 있음

- Hebernate 프레임워크 (그 다음으로 등장한 것) : 완벽한 ORM 프레임워크로서 자바 객체와 테이블의 ROW를 매핑하는 역할을 수행한다. 오랜 시간을 거치며 기능도 추가되고 성능도 향상되어 ORM의 대표적인 프레임워크가 됨 

- TopLink나 Cocobase :  Hebernate 이후 하나씩 등장하기 시작한 프레임워크들

- 이러한 ORM 프레임워크들에 대한 표준화 작업 끝에 그 결과로 JPA가 나오게 되었다.
```

## JDBC와 JPA 공통점
![img](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbaCz4X%2FbtrjLkfh8pW%2FBaDvkKE3Yn8lUX9IkAB3w1%2Fimg.png)


