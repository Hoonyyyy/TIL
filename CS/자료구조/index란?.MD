# index
- 저장 공간을 조금 더 활용해서 데이터베이스 테이블의 검색 속도를 향상시키기 위한 주료구조

## index의 특징
- index는 where 절에서 효과가 있다.
- 인덱스 설정하기 좋은 컬럼
  - 조회시 자주 사용하고
  - 고유값 위주로
- DML(DATA Manipulation Language) 영향
  - UPDATE, DELETE는 WHERE 절에 잘 설정된 인덱스로 조건을 붙여주면 조회할 때 성능은 크게 저하 안됨
  - INSERT의 경우, 새로운 데이터가 추가되면서 -> 기존 인덱스 페이지에 저장되어 있던 탐색 위치가 수정되어야 하므로 효율이 좋지 않음
  - 즉, 인덱스는 원하는 데이터를 빠르게 찾을 때 빛을 발휘함

## 어떤 컬럼에 인덱스를 설정하는게 좋은지?
- 크기가 충분히 큰 테이블
- Insert, Delete, Update가 자주 발생하지 않는 컬럼
- Join, where Order by(Index가 정렬되어 있기 때문에 성능이 향상될 수 있다.)를 자주 사용하는 컬럼
- 인덱스는 한 테이블당 보통 3~5개 정도가 적당함
- 효율적으로 쓰기 위한 4가지
  - 카디널리티 (Cardinality)
  - 선택도 (Selectivity)
  - 활용도
  - 중복도


### 카디널리티 (Cardinality)
- 카디널리티가 높을 수록 인덱스 설정에 좋은 컬럼이다.
  - 한 컬럼이 갖고 있는 중복 정도가 낮을 수록 좋다.
- 컬럼에 사용되는 값의 다양성 정도, 즉 중복 수치를 나타내는 지표
~~~
'학번' 은 학생마다 부여 받으므로 10 값 모두 고유함
  - 중복 정도가 낮으므로 카디널리티가 낮다.
'이름' 은 동명이인이 있을 수 있으니 1~10개 사이의 값을 가진다.
  - 중복 정도가 '학번' 에 비해 높으므로 카디널리티가 높다고 표현할 수 있다.
~~~

### 선택도 (Selectivity)
- 선택도가 낮을 수록 인덱스 설정에 좋은 컬럼이다. ( 5~10% 정도가 적당함)
- 데이터에서 특정 값을 얼마나 잘 선택할 수 있는지에 대한 지표
- 선택도 계산 방법
~~~
= 컬럼의 특정 값의 row 수 / 테이블의 총 row수 * 100
= 컬럼의 값들의 평균 row 수 / 테이블의 총 row수 * 100
~~~
- 예를 들어, 10개 rows를 가지는 '학생' 테이블에 '학번', '이름', '성별' 컬럼이 있다고 할때
- 학번은 고유하고, 이름은 2명씩 같고, 성별은 남녀 5:5 비율이다.
  - '학번'의 선택도 = 1/10*100 = 10%
    - select count(1) from '학생' where '학번; = 1; (모두 고유하므로 특정 값 : 1)
  - '이름'의 선택도 = 2/10*100 = 20%
    - select count(1) from '학생' where '이름' = "김철수"; (2명씩 같으므로 특정 값 : 2)
  - '성별'의 선택도 = 5/10*100 = 50%
    select count(1) from '학생' where '성별' = M; (5명씩 같으므로 특정 값 : 5)

### 활용도
- 활용도가 높을 수록 인덱스 설정에 좋은 컬럼이다.
- 해당 컬럼이 실제 작업에서 얼마나 활용되는지에 대한 값

### 중복도
- 중복도가 없을 수록 인덱스 설정에 좋은 컬럼



## B+Tree 구조
- 예시이지만 제일 아래에서도 오른쪽으로 가는 구조를 가짐
- 노드에 Key만 두고, data는 담아두지 않음
- 오직 리프 노드에만 Key와 data를 담아서 저장함, 리프 노드들은 Linked List로 연결
- 하나의 노드에 더 많은 Key값을 담을 수 있기에 트리의 높이가 낮아짐(더 빠르게 검색 가능)
<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fc4C7d8%2Fbtq6YlQ5tHI%2FZAT45PnENpIctErdeIcD6K%2Fimg.png">

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FrnQnX%2FbtrCkgFoKo3%2FVQfHcWds7kmFfk3bLaPdtk%2Fimg.png">


# Spring Entity indexa 설정하기
~~~ java
@Entity
@NoArgsConstructor(access = AccessLevel.PROTECTED)
@Getter
@ToString(exclude = {"team"})
@Table(indexes = {@Index(name = "member_index",columnList = "member_id")})
public class Member{
 
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    @Column(name = "member_id")
    private Long id;
 
    @Column(name = "name",unique = true)
    private String name;
 
    @Column(name = "age")
    private int age;
 
    @Builder
    public Member(String name, int age){
        this.name=name;
        this.age=age;
    }
 
    @ManyToOne(fetch = FetchType.LAZY)
    @JoinColumn(name = "team_id")
    private Team team;
 
    public void changeAge(int age){
        this.age=age;
    }
 
    public void addTeam(Team team){
        team.getMembers().add(this);
        this.team=team;
    }
}
~~~




출처

https://www.youtube.com/watch?v=iNvYsGKelYs&t=338s

https://yurimkoo.github.io/db/2020/03/14/db-index.html
