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
