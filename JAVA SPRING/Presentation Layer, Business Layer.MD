# Presentation Layer, Business Layer

여기 정리하는것은 언제나 변경될 수 있음 그때그때마다 쓰는것

### Presentation Layer
- 사용자와 커뮤니케이션을 담당하는 화면

### Business Layer
- 사용자의 요청에 대한 비즈니스 로직 처리를 담당

#### 이 구조에 핵심 요소는 Controller, ServiceImpl, DAO 클래스
- Controller 클래스는 사용자의 요청을 제어하고,
- ServiceImpl 클래스는 실질적인 비즈니스 로직을 처리함
- DAO 클래스는 실질적인 데이터 베이스 연동을 담당한다.

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbylxl5%2FbtrVVQ3cPit%2FfMMcWCLcwMKXqaYeK3Z920%2Fimg.jpg">
