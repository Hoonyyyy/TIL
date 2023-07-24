# 리플렉션(reflection)
- 구체적인 클래스 타입을 알지 못해도 그 클래스의 메서드, 타입, 변수들을 접근할 수 있도록 해주는 자바 API
- 컴파일 시간이 아닌 실행 시간에 동적으로 특정 클래스의 정보를 추출해낼 수 있는 프로그램기법
- 자바는 컴파일 시점에 타입을 결정하는 정적 언어인데, 동적으로 클래스를 사용해야 할떄 리플렉션 사용한다.
- 간단한걸로 말하자면
- 컴파일 할 때 그들(클래스, 필드, 메서드...)의 이름을 모를때 유용하다.

## 기능 사용
### 필드 접근하기
```java
public class Person {

    public String name;
    protected String address;
    private int age;
    String email;
}
```

#### getDeclaredFields()
```java
    public static void main(String[] args) {
        Class<Person> clazz = Person.class;
        Field[] fields = clazz.getDeclaredFields();

        for (Field field : fields){
            System.out.println(field.getName());
        }

    }

// 결과
// name, address, age, email
```


### 인스턴스 생성하기
```java
public class Person {
    private String name;
    private int age;

    public Person() {}

    public Person(String name) {
        this.name = name;
    }

    public Person(int age) {
        this.age = age;
    }

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
}
```

#### getConstructor()
- 타입을 명시하여 원하는 생성자를 조회할 수 있음
```java
Class<Person> clazz = Person.class;
try {
    Constructor<Person> constructor = clazz.getConstructor(String.class, int.class);
} catch (NoSuchMethodException e) {
    e.printStackTrace();
}
```

#### newInstance()
```java
Class<Person> clazz = Person.class;
try {
    Constructor<Person> constructor = clazz.getConstructor(String.class, int.class);
    Person newPerson = constructor.newInstance("호호맨", 20);
} catch (NoSuchMethodException | IllegalAccessException | InstantiationException | InvocationTargetException e) {
    e.printStackTrace();
}
```

### 메서드 접근하기
```java
public class Person {
    private String name;
    private int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    @Override
    public String toString() {
        return "이름 : " + this.name + ", 나이 : " + age;
    }
}
```

#### getMethod()
```java
Class<Person> clazz = Person.class;
try {
    Constructor<Person> constructor = clazz.getConstructor(String.class, int.class);
    Person newPerson = constructor.newInstance("호호맨", 20);
    Method toString = newPerson.getClass().getMethod("toString");
} catch (NoSuchMethodException | IllegalAccessException | InstantiationException | InvocationTargetException e) {
    e.printStackTrace();
}
```

#### invoke()
- invoke(Object obj, Object... args)
- 인자로 해당 클래스 타입과 해당 메서드의 인자들을 인자로 받는다.
- invoke() 메서드는 라이브러리 내부를 디버깅할 때 정말 많이 보게 되는 메서드
- 스프링을 사용하면서 디버깅을 하다보면 무조건 보게 될 메서드이다.
- invoke() 메서드가 보인다면 대부분 리플렉션을 사용한 기능들일 것임
```java
public static void main(String[] args) {
    Class<Person> clazz = Person.class;
    try {
        Constructor<Person> constructor = clazz.getConstructor(String.class, int.class);
        Person newPerson = constructor.newInstance("호호맨", 20);
        Method toString = newPerson.getClass().getDeclaredMethod("toString");
        String result = (String)toString.invoke(newPerson);
        System.out.println(result);
    } catch (NoSuchMethodException | IllegalAccessException | InstantiationException | InvocationTargetException e) {
        e.printStackTrace();
    }
}

// 결과 이름 : 호호맨, 나이 : 20
```

## 그냥 생성하면 되지 왜 어렵게 하나요?
```
Java를 사용한다면 Person person = new person(); 으로 간단하게 생성하면 될 것을 어렵게 생성했다.
스프링 프레임워크나 다른 라이브러리를 사용할 때는 구체적인 클래스를 알고 있기 떄문에 리플렉션을 사용 할 일이 적다.
하지만 직접 라이브러리를 만들어본다고 생각할때, 라이브러리를 사용하는 사용자가 어떤 클래스를 만들지 예상할 수 있나?

Jackson, hibernate는 리플렉션을 사용하고 있습니다. 객체를 json타입으로 변경해주는
jackson 라이브러리의 ObjectMapper를 사용해보겠습니다.
```

### 예시
```java
public class Person {
    private String name;
    private int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public int getAge() {
        return age;
    }
}
```

```java
ObjectMapper objectMapper = new ObjectMapper();
try {
    String result = objectMapper.writeValueAsString(new Person("호호맨", 20));
    System.out.println(result);
} catch (JsonProcessingException e) {
    e.printStackTrace();
}
```

- 결과
```
{"name":"호호맨","age":20}
```

- 라이브러리가 어떻게 "호호맨", 20이라는 데이터를 가져올 수 있었을까?
- Person이라는 클래스를 사용자가 만들 거라 예상하고 getter를 사용해 데이터를 가져왔나?
- 우리가 좀 전에 예제로 살펴본 방식으로 리플렉션 api를 사용하여 Person이라는 클래스 정보를 받아온다.
- 그다음 'get'으로 시작하는 메서드를 찾아온 뒤 필드값에 접근하여 json형식으로 데이터를 변환해주기 때문에
- 우리는 간편하게 인스턴스만 넘겨주면 된다.
