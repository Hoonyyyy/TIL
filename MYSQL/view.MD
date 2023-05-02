## view
```mysql
/*
	뷰(view)
		- 필요한 정보만 추출하여 가상테이블 형태(view)로 제공한다.
        - 복잡한 질의문을 간소화
        - 작업결과를 임시로 보관
        - 뷰를 기초로 다른 뷰를 생성할 수도 있다.
        - 관리자로 부터 테이블에 대한 접근권한과 생성권한을 부여받아야 한다.
        
	목적
		- 데이터 노출로부터 데이터베이스를 보호
        - 데이터의 독립성
        - 다양한 구조의 테이블 사용효과
        - 작업의 단순화
        
	생성
		CREATE VIEW 이름 as
			select ~~~~~~
            
	수정 ALTER VIEW 이름(컬럼,컬럼...) AS
    
*/
```


### view 이용
```mysql
# 학과평균나이 뷰를 생성하시오.
# 학생테이블 소속학과를 기준으로 학과의 평균나이를 출력해준다.

CREATE VIEW 학과평균나이 AS
SELECT truncate(AVG(나이), 0) AS 평균나이
FROM 학생
GROUP BY 소속학과;
```

### INSET INTO는 하기 힘드나, UPDATE SET은 쉽게 가능함
```mysql
# 컴퓨터과학과 C303교수의 주소를 경기도 의정부로 수정하시오.
UPDATE 컴퓨터과학과교수
set 주소 = '경기도 의정부'
where 교수번호 = 'C303';
```

### mysql 여러가지
```mysql
# 사번 이름 부양가족수, 총급여(본봉+수당-공제액+상여금),평균소득(총급여/부양가족수)을 
# 오름차순으로 출력되는
# 부양가족별 평균소득 뷰를 작성하시오.


CREATE VIEW 부양가족별_평균소득 AS
SELECT 
신상테이블.사번,
신상테이블.성명,
신상테이블.부양가족수,
(본봉+수당-공제액+상여금) AS 총급여,
truncate(((본봉+수당-공제액+상여금) / 신상테이블.부양가족수),0) AS 평균소득
FROM 급여테이블
INNER JOIN 신상테이블
	ON 급여테이블.사번 = 신상테이블.사번
ORDER BY 부양가족수 asc, 평균소득 asc;

SELECT *
FROM 부양가족별_평균소득;


# 사원 김인수 씨의 생일까지 남은 일수를 산출하시오

SELECT DATEDIFF(CONCAT(YEAR(NOW()),'-',MONTH(생년월일),'-',DAY(생년월일)), NOW()) AS '김인수 생일까지 남은 일수'
FROM 신상테이블
WHERE 성명 = '김인수';
```

### mysql 여러가지2
```mysql
# 직급이 사원에 해당하는 사원들의 사번, 이름, 직급, 수당, 부양가족수를 구할 수 있는 뷰를 생성하시오
CREATE VIEW 사원뷰 AS
SELECT 신상테이블.사번, 신상테이블.성명, 급여테이블.직급, 급여테이블.수당, 신상테이블.부양가족수
FROM 신상테이블 INNER JOIN 급여테이블
	ON 신상테이블.사번 = 급여테이블.사번
WHERE 급여테이블.직급 REGEXP '^사원';

SELECT *
FROM 사원뷰;

# 급여내역을 직급별 평균본봉, 평균수당, 평균공제액, 평근상여금, 직급별사원이름을 조회할 수 있는 급여내역 뷰를 작성하시오
CREATE VIEW 급여내역뷰 AS
SELECT 급여테이블.직급 AS 직급 ,truncate(AVG(본봉),0) AS 평균본봉, truncate(AVG(수당),0) AS 평균수당, 
		truncate(AVG(공제액),0) AS 평균공제액, group_concat(성명) AS 이름
FROM 급여테이블 INNER JOIN 신상테이블
	ON 급여테이블.사번 = 신상테이블.사번
GROUP BY 직급;
```
