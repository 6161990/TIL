#### :pushpin: DML(Data Manipulation Language(데이터 조작어)) 
* ##### INSERT : 테이블에 새로운 로우를 추가하는 구문

      INSERT INTO 테이블명 (컬럼명) VALUES (값)

<br>

```
INSERT INTO EMP01 (EMPNO, ENAME, JOB) VALUES(222,'김제니','개발');
INSERT INTO EMP01 (EMPNO, ENAME, JOB) VALUES(223,'로제','인사');
INSERT INTO EMP01 (EMPNO, ENAME, JOB) VALUES(224,'지수','생산');

--컬럼목록을 생략하는 경우 (모든 컬럼에 DATA 넣을때만!)
INSERT INTO EMP01 VALUES(225,'리사','개발');
```

<img width="356" alt="20210510072020" src="https://user-images.githubusercontent.com/74708028/117589320-b87cd700-b163-11eb-867d-086d973ee38e.png">

<br>

```
--컬럼 목록에 모든 컬럼에 있지 않을 경우 (JOB에 NULL 값이 들어감)
INSERT INTO EMP01 (EMPNO,ENAME) VALUES (226,'사나');
```

<img width="327" alt="20210510072040" src="https://user-images.githubusercontent.com/74708028/117589323-bfa3e500-b163-11eb-9879-60134f125b15.png">


<br>

```
--NULL을 명시적으로 저장할 수도 있음
INSERT INTO EMP01 (EMPNO, ENAME, JOB) VALUES (227,'나연', NULL);
```

<img width="368" alt="20210510072143" src="https://user-images.githubusercontent.com/74708028/117589324-c4689900-b163-11eb-95cc-c562452ea326.png">

<br>

  #### :round_pushpin: 테이블 구조와 데이터 복사

<br>

```
--테이블 구조 복사
CREATE TABLE EMP02 AS SELECT EMPNO, ENAME, JOB FROM EMP01 WHERE 1=0;
SELECT * FROM EMP02;

--테이블 데이터 복사 (컬럼이름이 같지 않아도됨, 순서만 지켜주면 OK)
INSERT INTO EMP02(EMPNO, ENAME, JOB) SELECT EMPNO, ENAME, JOB FROM EMP;
SELECT * FROM EMP02;

--모든 컬럼 복사시 명시 X 도 가능
INSERT INTO EMP02 SELECT EMPNO, ENAME, JOB FROM EMP01;
SELECT * FROM EMP02;
```

<img width="377" alt="20210510072442" src="https://user-images.githubusercontent.com/74708028/117589332-ce8a9780-b163-11eb-9ded-c6e01b4a80e3.png">
<img width="401" alt="20210510072523" src="https://user-images.githubusercontent.com/74708028/117589346-e06c3a80-b163-11eb-8ba7-6c8d51611961.png">

<img width="315" alt="20210510072741" src="https://user-images.githubusercontent.com/74708028/117589352-e6fab200-b163-11eb-8cf8-d274cfae5689.png">


<br>

  #### :round_pushpin: 서브쿼리로 데이터 저장하기
      INSERT INTO 테이블명 서브쿼리
      INSERT ALL INTO 테이블명 (컬럼명) VALUES (컬럼명) 
                 INTO 테이블명(컬럼명) VALUES(컬럼명)
             서브쿼리

<br>

```
--서브쿼리 이용해 한꺼번에 DATA 삽입
INSERT ALL 
INTO EMP03 ( EMPNO, ENAME, JOB) VALUES (EMPNO, ENAME, JOB) 
INTO EMP04 ( EMPNO, ENAME, HIREDATE) VALUES (EMPNO, ENAME, HIREDATE)
SELECT EMPNO, ENAME, JOB, HIREDATE FROM EMP;

SELECT * FROM EMP03;
SELECT * FROM EMP04;
```

<img width="411" alt="20210510073322" src="https://user-images.githubusercontent.com/74708028/117589358-ec57fc80-b163-11eb-80eb-8118ab1dc9db.png">


<br>

  #### :round_pushpin: UPDATE, 로우 내의 컬럼 값을 수정하는 구문
      UPDATE 테이블명 SET 컬럼 = 값, 컬럼 = 값.. WHERE 조건문
 
 
<br>

```
--사원들의 직무를 개발로 변경한다.
UPDATE EMP01 SET JOB = '개발';
SELECT * FROM EMP01;
```     

<img width="174" alt="20210510075222" src="https://user-images.githubusercontent.com/74708028/117590116-e3b5f500-b168-11eb-8dfa-d2026d634b70.png">

<br>

```
--사원들의 사원번호, 이름, 직무를 변경한다.
UPDATE EMP01 SET EMPNO = 777, ENAME ='제니' , JOB = '개발';
```   

<img width="323" alt="20210510075540" src="https://user-images.githubusercontent.com/74708028/117590127-eca6c680-b168-11eb-9d92-01ccef5ca87d.png">


<br>

```
--연극팀 부서에 근무하고 있는 사원들의 급쳐를 전체 평균 급여로 설정한다. 
UPDATE EMP SET SAL = (SELECT TRUNC(AVG(SAL)) FROM EMP) WHERE JOB='연극팀';
```   

<img width="406" alt="20210510080638" src="https://user-images.githubusercontent.com/74708028/117590149-faf4e280-b168-11eb-9146-a7c7af66bb2d.png">



<br>

```
--20번 부서에 근무하고 있는 사원들의 직속상관을 KING 으로 하고 급여를 전체 급여의 최고액으로 설정한다.
UPDATE EMP01 SET MGR = (), SAL = () WHERE DEPTNO =20; --헷갈리는 경우 이렇게 만들어놓고
    SELECT EMPNO FROM EMP01 WHERE ENAME = 'KING'; --괄호에 들어갈 정보를 하나씩 채우기
    SELECT MAX(SAL) FROM EMP01;
```   

<img width="502" alt="20210510082505" src="https://user-images.githubusercontent.com/74708028/117590211-40191480-b169-11eb-8fbd-5b372daf2529.png">


<br>

```
--직무가 CLERK 인 사원들의 직무와 급여를 최고액을 받는 사원의 직무와 급여액으로 변경한다.
--직무와 급여 따로 
UPDATE EMP01 SET JOB=(SELECT JOB FROM EMP01 WHERE SAL =(SELECT MAX(SAL) FROM EMP01)), 
                 SAL=(SELECT SAL FROM EMP01 WHERE SAL =(SELECT MAX(SAL) FROM EMP01))
WHERE JOB = 'CLERK';

--직무 급여 한꺼번에 UPDATE
UPDATE EMP01 SET(JOB,SAL) = (SELECT JOB, SAL FROM EMP01 WHERE SAL =(SELECT MAX(SAL) FROM EMP01))
        WHERE JOB ='CLERK';
```   

<img width="519" alt="20210510082033" src="https://user-images.githubusercontent.com/74708028/117590195-22e44600-b169-11eb-8394-640d0a6a274e.png">



<br>

  #### :round_pushpin: DELETE, 테이블 내의 로우를 삭제하는 구문
      DELETE FROM 테이블명 WHERE 조건문

<br>

```
--조건절을 사용하지 않으면 테이블의 모든 데이터가 삭제된다.
DELETE FROM EMP01; 
```   

<img width="303" alt="20210510083006" src="https://user-images.githubusercontent.com/74708028/117590404-42c83980-b16a-11eb-85ed-fb5a02783083.png">

<br>

```
-- 사원번호가 7499인 사원의 정보를 삭제한다.
DELETE FROM EMP01 WHERE EMPNO = 7499;
```   

<img width="291" alt="20210510082917" src="https://user-images.githubusercontent.com/74708028/117590401-3e9c1c00-b16a-11eb-8415-e5e3f1c8cd4b.png">

<br>

```
--사원의 급여가 평균 급여 이하인 사원의 정보를 삭제한다.
DELETE FROM EMP01 WHERE SAL <= (SELECT AVG(SAL) FROM EMP01);
```   

<img width="345" alt="20210510083016" src="https://user-images.githubusercontent.com/74708028/117590411-49ef4780-b16a-11eb-85b6-cc44bb2b9bed.png">

<br>

```
--커미션을 받지 않는 사원들의 정보를 삭제한다.
DELETE FROM EMP01 WHERE COMM IS NULL;
```   

<img width="233" alt="20210510083022" src="https://user-images.githubusercontent.com/74708028/117590414-4cea3800-b16a-11eb-8615-f33e08c0f7fa.png">
