# 빈 생명주기 콜백(@PostConstruct, @PreDestroy)

## 빈 생명주기 콜백 시작
- 데이터베이스 커넥션 풀이나, 네트워크 소켓처럼 애플리케이션 시작 시점에 필요한 연결을 미리 해두고,
- 애플리케이션 종료 시점에 연결을 모두 종료하는 작업을 진행하려면, 객체의 초기화와 종료 작업이 필요하다.

## 스프링 빈의 라이프사이클
- 객체 생성 -> 의존관계 주입
- 스프링 빈은 객체를 생성하고, 의존관계 주입이 다 끝난 다음에야 필요한 데이터를 사용할 수 있는 준비가 완료된다.
- 따라서 초기화 작업은 의존관계 주입이 모두 완료되고 난 다음에 호출해야 한다.
- 그렇지만 개발자가 의존관계 주입이 모두 완료된 시점을 아는 방법은 무엇일까?
  - 스프링은 의존관계 주입이 완료되면 스프링 빈에게 콜백 메서드를 통해서 초기화 시점을 알려주는 기능을 제공한다.
  - 또한 스프링은 스프링 컨테이너가 종료되기 직전에 소멸 콜백을 준다.
  - 따라서 안전하게 종료 작업을 진행 할 수 있다.

## 스프링 빈의 이벤트 라이프 사이클
1. 스프링 컨테이너 생성
2. 스프링 빈 생성
3. 의존관계 주입
4. 초기화 콜백
5. 사용
6. 소멸전 콜백
7. 스프링 종료
- 초기화 콜백 : 빈이 생성되고, 빈의 의존관계 주입이 완료된 후 호출
- 소멸전 콜백 : 빈이 소멸되기 직전에 호출

## 객체의 생성과 초기화를 분리하자
- 생성자
  - 필수 정보(파라미터)를 받고, 메모리를 할당해서 객체를 생성하는 책임을 가진다.
- 초기화
  - 이렇게 생성된 값들을 활용해서 외부 커넥션을 연결하는 등 무거운 동작을 수행함
- 따라서 생성자 안에서 무거운 초기화 작업을 함께 하는 것 보다는 객체를 생성하는 부분과 초기화 하는 부분을 명확하게 나누는 것이 유지보수 관점에서 좋음
- 약간 변경 정도는.. 생성자에서 한번에 하는게 나을수도 있음

### 생성 초기화 분리 전 코드
``` java
public class MemberService {
    private String username;
    private String password;
    private Connection databaseConnection;

    public MemberService(String username, String password) {
        // 생성자에서 초기화와 무거운 작업을 함께 처리
        this.username = username;
        this.password = password;
        // 데이터베이스 연결 등 무거운 초기화 작업 수행
        this.databaseConnection = connectToDatabase();
    }
}
```

### 생성 초기화 분리 후 코드
``` java
public class MemberService {
    private String username;
    private String password;
    private Connection databaseConnection;

    public MemberService(String username, String password) {
        // 생성자에서 필수 정보만 받아서 할당
        this.username = username;
        this.password = password;
    }

    public void initialize() {
        // 초기화 메서드에서 무거운 작업 수행
        this.databaseConnection = connectToDatabase();
    }
}
```


# 한번만 등록할때!!!


## @PostConstruct
- 객체의 초기화 부분
- 객체가 생성된 후 별도의 초기화 작업을 위해 실행하는 매더를 선언
- @PostConstruct 어노테이션을 설정해놓은




