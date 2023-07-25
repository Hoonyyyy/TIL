# DI, IOC


## IOC란?
- Inversion of Control ( 의역하면 제어의 역전 )
- 이전에 제어는 개발자가 구현했어야 했다.

#### 예시
- "A객체는 B객체에게 의존하고 있어" 라고 개발자가 직접 표현해주고 있다.
- 제어를 개발자가 관리하고 있다.
```java
public class A {
 private B b;
 public A(){
   b = new B(); 
 } 
}

```
  
- 그러나 SPRING에서는
- B라는 객체가 스프링 컨테이너에게 관리되고 있는 Bean이라면 @Autowired를 통해 객체를 주입받을 수 있게 된다.
- 이것이 스프링 컨테이너에서 직접(제어) 객체를 생성하여 해당 객체에 주입 시켜준 것
- 개발자가 해야 할 제어를 스프링 컨테이너에서 대신 해주고 있다.
- 이것이 IoC라는 개념
```java
public class A {

  @Autowired
  private B b;

}
```

### 장점 ( IoC 적용시 미리 생성해놓은 객체를 주이받아 사용하기만 하면 
- 객체 간 결합도를 낮춘다.
- 유연한 코드 작성
- 가독성 증진
- 코드 중복 방지
- 유지 보수 용이

## DI
- 아래에서 DI는 이런 의존성을 외부에서 주입한다고 한다. 여기서 외부는 "스프링 컨테이너" 를 의미함
```
A클래스 내부에서 B, C 클래스의 메서드를 활용한다고 할때,
유지 보수 과정에서 B,C클래스의 응답형식이 변경된다면 A클래스도 변경되어야 한다.
A클래스 로직이 변경되어 B, C클래스로 보내는 객체가 변경된다면 기존과 같게 변경하는 로직을 추가해야 합니다.
이렇게 B, C클래스에 의존도가 높은 코드는 결합도가 높은 코드라고 말함
```

### DI방식

#### 필드, 수정자 방식은 런타임에서도 의존성을 주입하기 때문에 의존성을 주입하지 않아도 객체가 생성될 수 있다.

- Field Injection(필드 주입)
- 주입받으려는 빈의 생성자를 호출하여 빈을 찾거나 빈 팩토리에 등록
- 생성자 인자에 사용하는 빈을 찾거나 만듦
- 필드에 주입
```java
// Field Injection은 의존성을 주입하고 싶은 필드에 @Autowired 어노테이션을 붙여주면 의존성이 주입됨

@RestController
public class PostController {

    @Autowired
    private PostService postService;

}
```

- Setter Injection(수정자 주입)
- 주입받으려는 빈의 생성자를 호출하여 빈을 찾거나 빈 팩토리에 등록
- 생성자 인자에 사용하는 빈을 찾거나 만듦
- 주입하려는 빈 객체의 수정자를 호출하여 주입
```java
@RestController
public class PostController {
    private PostService postService;

    @Autowired
    private void setPostService(PostService postService){
        this.postService = postService;

    }

}
```

- Constructor Injection(생성자 주입) (추천!)
- 객체가 생성되는 시점에 빈을 주입한다.
- 생성자의 인자에 사용되는 빈을 찾거나빈 팩토리에서 만든다.
- 찾은 인자 빈으로 주입하려는 생성자를 호출한다.
- NullPointerException의 발생을 막는다 (객체가 생성되는 시점에 빈을 주입한다.)
- 불변성을 활용할 수 있다.(final로 선언 가능하다.)
- SRP(단일 책임 원칙)을 지킬 수 있도록 유도한다. 
```java
@RestController
public class PostController {
    private PostService postService;

    @Autowired
    public void PostController(PostService postService) {
        this.postService = postService;
    }
}
```


https://isoomni.tistory.com/entry/TISPRING-IOC-DI-%EC%A0%95%EC%9D%98-%EC%9E%A5%EC%A0%90
https://marrrang.tistory.com/58



## AOP



