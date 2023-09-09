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
- 인덱스는 한 테이블당 보통 3~5개 정도가 적당함
-




출처

https://www.youtube.com/watch?v=iNvYsGKelYs&t=338s

https://yurimkoo.github.io/db/2020/03/14/db-index.html
