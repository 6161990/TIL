#### :pushpin: TABLE
* ##### CREATE TABLE 테이블명(컬럼명 자료형 제약조건, 컬럼명 자료형 제약조건)
* ##### CHAR(SIZE) : 고정 길이 문자열 타입
* ##### VARCHAR2(SIZE) : 가변 길이 문자열 타입
* ##### NUMBER : 최고 40자리까지 저장할 수 있는 숫자 타입
* ##### DATE : 날짜
* ##### LONG : 가변 길이 문자열 타입, 최대 2Gbyte

<br>

```

CREATE TABLE EMP (
    EMPNO NUMBER(10) CONSTRAINT EMPNO_PK PRIMARY KEY,
    ENAME VARCHAR2(20),
    JOB VARCHAR2(20),
    MGR NUMBER(10),
    HIREDATE DATE default sysdate,
    SAL NUMBER(10),
    COMM NUMBER(10),
    DEPTNO NUMBER(10)
);
```

<img width="329" alt="20210510084039" src="https://user-images.githubusercontent.com/74708028/117590932-c3883500-b16c-11eb-9e04-5415680d1316.png">

<br>

  #### :round_pushpin: 서브쿼리로 테이블 만들기
        CREATE TABLE 테이블명 
        AS 
        서브쿼리
  
  
 <br>
  
```
--서브쿼리로 테이블 구조 복사해 테이블 만들기 
CREATE TABLE EMP02 AS SELECT EMPNO, ENAME, JOB FROM EMP01 WHERE 1=0;
SELECT * FROM EMP02;
--테이블 데이터 복사 (컬럼이름이 같지 않아도됨, 순서만 지켜주면 OK)
INSERT INTO EMP02(EMPNO, ENAME, JOB) SELECT EMPNO, ENAME, JOB FROM EMP;
SELECT * FROM EMP02;
```
  
  <img width="398" alt="20210510084238" src="https://user-images.githubusercontent.com/74708028/117590951-d569d800-b16c-11eb-9fab-edf14200410e.png">

 <br>
  
```
--30번 부서에 근무하고 있는 사원들의 사원번호, 이름, 근무부서 이름을 가지고 있는 테이블을 생성한다
CREATE TABLE EMP03
AS
SELECT A1.EMPNO, A1.ENAME, A2.DNAME
FROM EMP A1, DEPT A2
WHERE A1.DEPTNO = A2. DEPTNO AND A1.DEPTNO =30;
```

<img width="490" alt="20210510085115" src="https://user-images.githubusercontent.com/74708028/117590973-eca8c580-b16c-11eb-9911-603ae890975e.png">



 <br>
  
```
--각 부서별 급여 총합, 평균, 최고액, 최저액, 사원수를 가지고 있는 테이블을 생성하시오
--ERROR. WHY? 그룹함수를 통해 DATA를 가져왔지만 그 DATA를 저장할 컬럼이 없기 때문에 테이블 생성 불가
CREATE TABLE EMP 04
AS
SELECT SUM(SAL), TRUNC(AVG(SAL)), MAX(SAL), MIN(SAL), COUNT(SAL)
FROM EMP
GROUP BY DEPTNO;

--별칭을 부여해야한다
CREATE TABLE EMP 04
AS
SELECT SUM(SAL) AS SUM, TRUNC(AVG(SAL)) AS AVG, 
       MAX(SAL) AS MAX, MIN(SAL) AS MIN, COUNT(SAL) AS COUNT
FROM EMP
GROUP BY DEPTNO;
```

<img width="504" alt="20210511082347" src="https://user-images.githubusercontent.com/74708028/117736320-41fada80-b232-11eb-8ec7-7ec9d36972b9.png">

<br>

  #### :round_pushpin: 테이블 구조 변경하기 
  * ##### ALTER 구문을 이용하면 테이블 구조를 변경할 수 있다.
  * ##### ALTER TABLE[테이블명] ADD (컬럼명 자료형 제약조건)
  * ##### ALTER TABLE[테이블명] MODIFY (컬럼명 자료형 제약조건)
  * ##### ALTER TABLE[테이블명] RENAME TO [테이블명]
  * ##### ALTER TABLE[테이블명] RENAME COLUMN 컬럼명1 TO 컬럼명2
  * ##### ALTER TABLE[테이블명] DROP COLUMN 컬럼명
  * ##### DROP TABLE[테이블명]
  
  
```
CREATE TABLE TEST_TABLE20(
    DATA1 NUMBER NOT NULL,
    DATA2 NUMBER NOT NULL
);
--컬럼 추가
ALTER TABLE TEST_TABLE1 ADD(DATA3 NUMBER NOT NULL);

--컬럼의 데이터 타입 변경
ALTER TABLE TEST_TABLE1 MODIFY (DATA3 VARCHAR2(100));

--테이블 이름 변경
ALTER TABLE TEST_TABLE1 RENAME TO TEST_TABLE2;

--컬럼 이름 변경
ALTER TABLE TEST_TABLE1 RENAME RENAME COLUMN DATA3 TO DATA4;

--컬럼 삭제
ALTER TABLE TEST_TABLE1 DROP COLUMN DATA4;

--테이블 삭제
DROP TABLE TEST_TABLE1;
```

<img width="368" alt="20210511140645" src="https://user-images.githubusercontent.com/74708028/117761336-227ba600-b262-11eb-8ef3-1888e8e9ab0c.png">

