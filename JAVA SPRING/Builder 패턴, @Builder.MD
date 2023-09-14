# Builder 패턴, @Builder

# Builder Pattern
- 빌더 패턴(Builder Pattern)은 복잡한 객체의 생성 과정 표현 방법을 분리하여 다양한 구성의 인스턴스를 만드는 생성 패턴이다.
- 생성자에 들어갈 매개 변수를 메서드로 하나하나 받아들이고 마지막에 통합 빌드해서 객체를 생성하는 방식이다.
- 서브웨이 생각하기
  - 내가 원하는대로 다양한 타입의 야채, 소스 넣고 만드는 과정
  - 다양한 타입의 인스턴스를 생성할 수 있어, 클래스의 선택적 매개변수가 많은 상황에서 유용하게 사용된다.

## 점층적 생성자패턴
- Telescoping Constructor Pattern은 필수 매개변수와 함께 서택 매개변수를 0개, 1개, 2개 .. 받는 형태로, 우리가 다양한 매개변수를 입력받아 인스턴스를 생성하고 싶을때
- 사용하던 생성자를 오버로딩 하는 방식
- 하지만 이런 방식은 인스턴스 필드들이 많으면 많아질수록 생성자에 들어갈 인자의 수가 늘어나 몇번째 인자가 어떤 필드였는지 헷갈림
- 그리고 일정한 순서에 따라 생성해야 하기에 몇번째가 양상추인지, 몇번째가 토마토인지 다 알고 있어야함
- 또한 매개변수 특성상 필요없는 부분은 파라미터에 0을 전달해야하는데 매우 불편함
- 가독성 및 유지보수 측면에서 좋지 않음
~~~ java
class Hamburger {
    // 필수 매개변수
    private int bun;
    private int patty;

    // 선택 매개변수
    private int cheese;
    private int lettuce;
    private int tomato;
    private int bacon;

    public Hamburger(int bun, int patty, int cheese, int lettuce, int tomato, int bacon) {
        this.bun = bun;
        this.patty = patty;
        this.cheese = cheese;
        this.lettuce = lettuce;
        this.tomato = tomato;
        this.bacon = bacon;
    }

    public Hamburger(int bun, int patty, int cheese, int lettuce, int tomato) {
        this.bun = bun;
        this.patty = patty;
        this.cheese = cheese;
        this.lettuce = lettuce;
        this.tomato = tomato;
    }
    

    public Hamburger(int bun, int patty, int cheese, int lettuce) {
        this.bun = bun;
        this.patty = patty;
        this.cheese = cheese;
        this.lettuce = lettuce;
    }

    public Hamburger(int bun, int patty, int cheese) {
        this.bun = bun;
        this.patty = patty;
        this.cheese = cheese;
    }
~~~

~~~ java
public static void main(String[] args) {
    // 모든 재료가 있는 햄버거
    Hamburger hamburger1 = new Hamburger(2, 1, 2, 4, 6, 8);

    // 빵과 패티 치즈만 있는 햄버거
    Hamburger hamburger2 = new Hamburger(2, 1, 1);

    // 빵과 패티 베이컨만 있는 햄버거
    Hamburger hamburger3 = new Hamburger(2, 0, 0, 0, 0, 6);
}
~~~

## 자바 빈(Java Beans) 패턴
- 이러한 단점을 보완하기 위해 Setter 메서드를 사용한 자바 빈(Bean) 패턴이 고안 되었다.
- 매개변수가 없는 생성자로 객체 생성후 Setter 메서드를 이용해 클래스 필드의 초깃값을 설정하는 방식
- 기존 생성자 오버로딩에서 나타났던 가독성 문제점이 사라지고 선택적인 파라미터에 대해 해당되는 Setter메서드를 호출함으로써 유연젹으로 객체 생성이 가능해짐
- 그러나 객체 생성 시점에 모든 값들을 주입 하지 않아 일관성(consistency) 문제와 불변성(immutable) 문제가 나타남
- 일관성 문제
  - 필수 매개변수란 객체가 초기화될 때 반드시 설정되어야 하는 값
  - 하지만 개발자가 깜빡하고 setter 하나 빼먹고 나중에 넣어버리려 하면? 일관성이 무너짐
  - 객체가 유효하지 않게 됨, 만일 다른 곳에서 햄버거 인스턴스를 사용하게 된다면 런타임 예외가 발생할 수도 있다.
  - 물론 생성자와 결합하여 극복은 되겠지만 불변성 문제 때문에 자바 빈즈 패턴은 지양해야함
- 불변성 문제
  - 자바 빈즈 패턴의 Setter 메서드는 객체를 처음 생성할 때 필드값을 설정하기 위해 존재하는 메서드
  - 하지만 객체를 생성했음에도 여전히 외부적으로 Setter 메서드를 노출하고 있으므로, 협업 과정에서 언제 어디서나 누군가 Setter 조작 가능!!!
  - 이는 불변성을 위배함

~~~ java
class Hamburger {
    // 필수 매개변수
    private int bun;
    private int patty;

    // 선택 매개변수
    private int cheese;
    private int lettuce;
    private int tomato;
    private int bacon;
    
    public Hamburger() {}

    public void setBun(int bun) {
        this.bun = bun;
    }

    public void setPatty(int patty) {
        this.patty = patty;
    }

    public void setCheese(int cheese) {
        this.cheese = cheese;
    }

    public void setLettuce(int lettuce) {
        this.lettuce = lettuce;
    }

    public void setTomato(int tomato) {
        this.tomato = tomato;
    }

    public void setBacon(int bacon) {
        this.bacon = bacon;
    }
}
~~~

~~~ java
public static void main(String[] args) {
    // 모든 재료가 있는 햄버거
    Hamburger hamburger1 = new Hamburger();
    hamburger1.setBun(2);
    hamburger1.setPatty(1);
    hamburger1.setCheese(2);
    hamburger1.setLettuce(4);
    hamburger1.setTomato(6);
    hamburger1.setBacon(8);

    // 빵과 패티 치즈만 있는 햄버거
    Hamburger hamburger2 = new Hamburger();
    hamburger2.setBun(2);
    hamburger2.setPatty(1);
    hamburger2.setCheese(2);

    // 빵과 패티 베이컨만 있는 햄버거
    Hamburger hamburger3 = new Hamburger();
    hamburger3.setBun(2);
    hamburger2.setPatty(1);
    hamburger3.setBacon(8);
}
~~~

## 빌더(Builder 패턴)
- 별도의 Builder 클래스를 만들어 step-by-step으로 값을 입력받은 후에 최종적으로 build() 메서드로 하나의 인스턴스를 생성하여 리턴하는 패턴
- 아래 코드에서 주목할 부분은 "return this" 부분이다. 여기서 this란 StudentBuilder 객체 자신을 말한다.
- 빌더 객체 자신을 리턴함으로써 메서드 호출 후 연속적으로 빌더 메서드들을 체이닝(Chaining) 하여 호출할 수 있게 된다.
- ex) new StudentBuilder().id(값).name(값)
~~~ java
class StudentBuilder {
    private int id;
    private String name;
    private String grade;
    private String phoneNumber;

    public StudentBuilder id(int id) {
        this.id = id;
        return this;
    }

    public StudentBuilder name(String name) {
        this.name = name;
        return this;
    }

    public StudentBuilder grade(String grade) {
        this.grade = grade;
        return this;
    }

    public StudentBuilder phoneNumber(String phoneNumber) {
        this.phoneNumber = phoneNumber;
        return this;
    }
}
~~~

~~~ java
public static void main(String[] args) {

    Student student = new StudentBuilder()
                .id(2016120091)
                .name("임꺽정")
                .grade("Senior")
                .phoneNumber("010-5555-5555")
                .build();

    System.out.println(student);
}
~~~

## 빌더 패턴 장점

### 객체 생성 과정을 일관된 프로세스로 표현
- 생성자 방식은 클래스 변수가 4개 이상만 되어도 각 인자 순서 마다 이 값이 어떤 멤버에 해당되는지 바로 파악이 힘듬
- 그러나 빌더 패턴을 적용하면 직관적으로 어떤 데이터에 어떤 값이 설정되는지 한눈에 파악할 수 있게 된다.
~~~ java
// 생성자 방식
Student student1 = new Student(2016120091, "홍길동", "freshman", "010-5555-5555");

// 빌더 방식
Student student2 = new StudentBuilder()
            .id(2016120091)
            .name("임꺽정")
            .grade("Senior")
            .phoneNumber("010-5555-5555")
            .build();
~~~

### 디폴트 매개변수 생략을 간접적으로 지원
- 디폴트 매개변수가 설정된 필드를 설정하는 메서드를 호출하지 않는 방식으로 마치 디폴트 매개변수를 생략하고 호출하는 효과를 간접적으로 구현할 수 있음
~~~ java
class Student {
    private int id;
    private String name;
    private String grade = "freshman"; // 디폴트 매개변수 역할
    private String phoneNumber;

    public Student(int id, String name, String grade, String phoneNumber) {
        ...
    }
	
    // 디폴트 매개변수를 제외한 인자들을 받는 생성자 오버로딩
    public Student(int id, String name, String phoneNumber) {
        ...
    }

    @Override
    public String toString() {
        return "Student { " +
                "id='" + id + '\'' +
                ", name=" + name +
                ", grade=" + grade +
                ", phoneNumber=" + phoneNumber +
                " }";
    }
}

// 디폴트 필드인 grade를 제외하고 빌더 구성 및 인스턴스화
Student student1 = new StudentBuilder(2016120091)
        .name("홍길동")
        .phoneNumber("010-5555-5555")
        .build();

System.out.println(student1);
~~~

### 필수 멤버와 선택적 멤버를 분리 가능
~~~ java
class StudentBuilder {
    // 초기화 필수 멤버
    private int id;

    // 초기화 선택적 멤버
    private String name;
    private String grade;
    private String phoneNumber;

    // 필수 멤버는 빌더의 생성자를 통해 설정
    public StudentBuilder(int id) {
        this.id = id;
    }

    // 나머지 선택 멤버는 메서드로 설정
    public StudentBuilder name(String name) {
        this.name = name;
        return this;
    }

    public StudentBuilder grade(String grade) {
        this.grade = grade;
        return this;
    }

    public StudentBuilder phoneNumber(String phoneNumber) {
        this.phoneNumber = phoneNumber;
        return this;
    }

    public Student build() {
        return new Student(id, name, grade, phoneNumber);
    }
}


Student student1 = 
        new StudentBuilder(2016120091) // 필수 멤버
        .name("홍길동") // 선택 멤버
        .build();

Student student2 = 
        new StudentBuilder(2016120091) // 필수 멤버
        .name("임꺽정") // 선택 멤버
        .grade("freshman") // 선택 멤버
        .build();
~~~

### 객체 생성 단계를 지연할 수 있음
~~~ java
// 1. 빌더 클래스 전용 리스트 생성
List<StudentBuilder> builders = new ArrayList<>();

// 2. 객체를 최종 생성 하지말고 초깃값만 세팅한 빌더만 생성
builders.add(
    new StudentBuilder(2016120091)
    .name("홍길동")
);

builders.add(
    new StudentBuilder(2016120092)
    .name("임꺽정")
    .grade("senior")
);

builders.add(
    new StudentBuilder(2016120093)
    .name("박혁거세")
    .grade("sophomore")
    .phoneNumber("010-5555-5555")
);

// 3. 나중에 빌더 리스트를 순회하여 최종 객체 생성을 주도
for(StudentBuilder b : builders) {
    Student student = b.build();
    System.out.println(student);
}
~~~

## 빌드 패턴 단점
- 코드 복잡성 증가
- 생성자 보다는 성능이 떨어짐
- 약 4개 이하의 필드 개수를 가진느 경우는 차라리 생성자를 사용하는것이 좋음
	- 빌더 패턴의 코드가 다소 장황하기 때문
	- 다만 API는 시간이 지날수록 많은 매개변수를 갖는 경향이 있기 때문에 애초에 빌더 패턴으로 시작하는 편이 나을 수 있음

### Lombok의 @Builder
- @Builder : PersonBuilder 빌더 클래스와 이를 반환하는 builder() 메서드 생성
- @AllArgsConstruct(access = AccessLevel.PRIVATE) : @Builder 선언하면 전체 인자를 갖는 생성자를 자동으로 만드는데 이를 private로 설정
- @ToString : toString() 메서드 자동 생성
~~~ java
import lombok.AccessLevel;
import lombok.AllArgsConstructor;
import lombok.Builder;
import lombok.ToString;

@Builder
@AllArgsConstructor(access = AccessLevel.PRIVATE)
@ToString
class Person {
    private final String name;
    private final String age;
    private final String gender;
    private final String job;
    private final String birthday;
    private final String address;
}

public static void main(String[] args) {
    Person person = Person.builder()
            .name("홍길동")
            .age("26")
            .gender("man") // 선택 파라미터
            .job("Warrior")
            .birthday("1800.10.10")
            .address("조선")
            .build();
}
~~~


https://inpa.tistory.com/entry/GOF-%F0%9F%92%A0-%EB%B9%8C%EB%8D%94Builder-%ED%8C%A8%ED%84%B4-%EB%81%9D%ED%8C%90%EC%99%95-%EC%A0%95%EB%A6%AC

https://esoongan.tistory.com/82

https://pamyferret.tistory.com/67
