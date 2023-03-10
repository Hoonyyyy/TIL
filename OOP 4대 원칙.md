
# 객체지향 4대원칙

## 캡슐화
[모델링 / 정보 은닉 / 데이터 캡슐화]

- 연관이 있는 속성과 메서드를 “하나의 클래스”로 묶어서 활용한다는 개념
- 묶을 때, 객체는 자신이 맡은 역할을 수행하기 위한  하나의 목적을 가진 실체라는 관점에서 접근해야함
- 은닉화 (Information Hiding) : 캡슐화 하면, 접근 제어자(private, public 등) 사용해  객체 외부에서  내부데이터의 접근 통제가 가능해짐

## 속성
[재사용 / 확장]

- 부모클래스의 속성과 메서드를 자식클래스에서 그대로 물려받는 개념
- 상속을 통해, 코드가 재활용 되기 때문에 생산성이 높아짐(클래스의 재사용과 확장을 위해 상속이 사용됨)
- 객체지향의 개념에서, **클래스**가 다른 타입과 구별되는 결정적인 차이점

## 추상화
[모델링]

- 추상화란 실생활에서의 구체적인 것을 관찰자가 관심있는 부분만 가지고 재조합 하는 것
- 실체들에서 관심있고, 공통적인 특성을 뽑아내서 하나의 분류(class)로 만든 것(모델링)
- 객체지향의 관점에서, 실체들의 공통적 특성을 뽑아내서 클래스의 정의하는 것 자체가 추상화의 개념
- ex) 도서관리 프로그램 → 제목 / 저자 / 출판사 / 총페이지 / 가격 등

## 다형성
[사용편의 / 동적바인딩]

- 하나의 객체가 여러가지 타입의 형태로 저장 될 수 있고, 다양한 메서드의 형태로 동작 가능함을 의미 (하나의 객체는 부모의 타입으로도 저장이 가능하고, 프로토콜 타입으로도 저장이 가능)
- 하나의 객체는 다양한 방식으로 동적 가능(동적 바인딩 / Method Dispatch)
