# JPA 기본생성자,Reflection

## Reflection
- reflection은 구체적인 클래스 타입을 알지 못해도 클래스의 메서드나, 타입, 변수들에 접근할 수 있도록 해주는 api (동적생성)
- 대표 예시
  - JPA에서 객체 조회시 데이터가 들어가는 것
  - @RequestBody 사용 시 DTO 객체에 데이터가 들어가는 것
  - 테스트 케이스 작성시 private 메서드를 테스트할 때 등
- 가능한 이유?
  - 기본적으로 객체에 데이터를 넣기 위해서는 일련의 과정(new, setter 등)이 필요하고, 접근 제어자에 따라 접근 불가능한 것이맞다.
  - 하지만 reflection이 적용된다면 이러한 과정이 필요하지 않고 private 메서드의 접근도 가능하다.
  - 바로 reflection이 static 영역에 저장되어 있는 클래스 정보에 접근이 가능하기 때문이다.
  - 다만 reflection은 기본 생성자를 통해 객체를 생성하기 때문에 해당 클래스에 기본 생성자(빈 생성자)가 있어야 한다.

## Reflection은 Spring Data JPA에서도 사용되었다.
- 우리는 JPA에서 xxRepository.findById 메서드를 통해 객체를 조회할 수 있는데, 이러한 객체를 반환해주는 로직에서 reflection 적용됨

## Spring Data JPA와 기본 생성자 private이 불가능한 이유?
- Spring Data JPA에서 private 접근 제어자는 사용 불가능 한데, 이는 프록시와 관련이 있다.
- 지연로딩으로 인해 프록시 객체를 사용하는 경우 원본 엔티티를 상속한 프록시 객체를 생성하게 된다.
- 그 후 실제 사용 시점에 엔티티 정보를 조회하여 프록시 엔티티가 원본 엔티티를 참조하도록 한다.
- 그러므로 기본 생성자에 private을 사용하게 된다면 상속받은 클래스(프록시 엔티티)에서 호출이 불가능하게 되고 public이나 protected를 사용해야 한다는 오류가 발생하게 된다.

## 정리
- JPA는 Reflection API를 사용하여 객체를 생성하기 때문에 기본 생성자가 필요하고,
- 지연로딩(LAZY)으로 인해 생성된 프록시 객체를 사용하기 위해서는 private로 선언이 불가능하다.








  
https://bluemoon-clover.tistory.com/131
