# Builder 패턴, @Builder

# Builder Pattern
- 빌더 패턴(Builder Pattern)은 복잡한 객체의 생성 과저오가 표현 방법을 분리하여 다양한 구성의 인스턴스를 만드는 생성 패턴이다.
- 생성자에 들어갈 매개 변수를 메서드로 하나하나 받아들이고 마지막에 통합 빌드해서 객체를 생성하는 방식이다.
- 서브웨이 생각하기
  - 내가 원하는대로 다양한 타입의 야채, 소스 넣고 만드는 과정
  - 다양한 타입의 인스턴스를 생성할 수 있어, 클래스의 선택적 매개변수가 많은 상황에서 유용하게 사용된다.

## 점층적 생성자패턴
- Telescoping Constructor Pattern은 필수 매개변수와 함께 서택 매개변수를 0개, 1개, 2개 .. 받는 형태로, 우리가 다양한 매개변수를 입력받아 인스턴스를 생성하고 싶을때
- 사용하던 생성자를 오버로딩 하는 방식
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



https://inpa.tistory.com/entry/GOF-%F0%9F%92%A0-%EB%B9%8C%EB%8D%94Builder-%ED%8C%A8%ED%84%B4-%EB%81%9D%ED%8C%90%EC%99%95-%EC%A0%95%EB%A6%AC
https://esoongan.tistory.com/82
https://pamyferret.tistory.com/67
