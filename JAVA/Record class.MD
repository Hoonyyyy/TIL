# Record class

- 불변(immutable) 데이터 객체를 쉽게 생성할 수 있도록 하는 새로운 유형의 클래스
- JDK14에서 preview로 등장하여 JDK16에서 정식 스펙으로 등록
- 일반 class와 다르게 생성자, getter, hashCode(), equals(), toString()를 제공한다.
- 물론 커스텀이 필요하다면 record 안에 정의해서 사용할 수 있다.

## 특징
- 생성자는 모든 field를 포함한다.
- toString()도 모든 field를 포함한다.
- equals(), hashCode() 메서드는 invokedynamic based mechanism을 사용한다.
- getter는 field 이름과 유사한 이름으로 생성된다 ex) id(), email()...
- 기본적으로 java.lang.Record class를 상속받기 때문에 다른 class를 상속받을 수 없다.
- class가 final이기 때문에 다른 subclass를 생성할 수 없다.
- 모든 field는 불변이기 때문에 setter는 제공하지 않음

## 사용
- DTO or domain modell에 사용
- 일시적인 데이터 저장
- 데이터 저장하고 싶으나 긴 코드 작성하고 싶지 않을때
- 불변적인 데이터를 저장할때

### 기존 불변 데이터 객체
``` java
public class Person {
    private final String name;
    private final int age;
    
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

### 레코드를 이용한 불변 객체
- 생성자 작성하지 않아도 되고 toString, equals, hashCode 메서드에 대한 구현을 자동으로 제공
``` java
public record Person(Strong name, int age) {}
```

### 레코드 이용한것 사용 예시
``` java
public class RecordDemo {
    public static void main(String[] args){
        Person person = new Person("Ted", 100);
        System.out.println("이름:"+ person.name() + " 나이:"+person.age());
        System.out.println("객체 정보:"+person.toString());
        Person person2 = new Person("Ted", 100);
        Person person3 = new Person("Dean", 200);
        
        if (person.equals(person2)) System.out.println("person, person2는 같은 사람");
        else System.out.println("person, person2는 다른 사람");
        
        if (person.equals(person3)) System.out.println("person, person3는 같은 사람");
        else System.out.println("person, person3는 다른 사람");
    }
}
```


출처

https://scshim.tistory.com/372

https://velog.io/@rmswjdtn/JAVA-%EB%AC%B8%EB%B2%95-Record-Class
