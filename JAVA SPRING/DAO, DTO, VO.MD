# DAO, DTO, VO


### DAO (Data Access Object)
- 실제로 DB의 data에 접근하기 위한 객체
- 실제로 DB에 접근하여  CRUD 기능을 수행
- Service와 DB를 연결하는 고리 역할


### DTO (Data Transfer ObjecT)
#### Layer간 통신 용도로 오고가는 객체(getter, setter)
- 계층 간 데이터 교환을 하기 위해 사용하는 객체
- 로직을 가지지 않는 순수한 데이터 객체(Java Beans)
- getter/setter 메서드만 가진 클래스를 의미함
- DB에서 데이터를 얻어서 Service와 Controlloer 등으로 보낼때 사용한다.
- 즉 엔티티를 DTO 형태로 변환 후 사용함

### VO(value Object)
#### 특정한 비즈니스 값을 담는 객체(VO)
- DTO와 달리 Read-Only 속성을 지닌 값 오브젝트입니다.
- DTO는 setter를 가지고 있어서 값이 변할 수 있지만,
- VO의 경우에는 getter만 가지고 있어 수정이 불가능하다.
```
DTO와 VO의 차이점은 DTO는 인스턴스 개념이고, VO는 리터럴 값 개념이다.
VO는 값들에 대해 Read-Only를 보장해줘야 존재의 신뢰성이 확보되지만, DTO의 경우에는 단지 데이터를 담는 그릇의
역할일 뿐 값은 그저 전달되어야 할 대상일 뿐이다.
따라서 값 자체에 의미가 있는 VO와 전달될 데이터를 보존해야 하는 DTO의 특성상 개념이 다르다.

따라서 VO의 핵심은 두 객체의 모든 필드 값들이 동일하다면 두 객체는 같다.
따라서 완전히 값 자체 표현 용도로만 사용하는 게 목적이라면, 두 객체의 모든 필드 값들이
모두 같으면 같은 객체이도록 만드는 것(equals() 와 hashCode()의 오버라이딩)이 중요하지,
메소드는 어떤 메소드가 있든 말든 상관 없습니다.
```


|종류|용도|동등 결정|가변 / 불변|로직|
|------|---|---|---|---|
|DTO|계층 간 데이터 전달|속성값이 모두 같아도 같은 객체가 아닐수 있음|setter존재 시 가변, 비 존재시 불변|getter/setter 불 필요|
|VO|값 자체를 표현|값 자체를 표현|불변|getter/setter 이외의 로직을 가질 수 있음|


https://kbwplace.tistory.com/162

