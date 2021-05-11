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
<br>

  #### :round_pushpin: 제약조건, 테이블의 데이터를 저장 혹은 수정할 때 컬럼의 값에 대한 조건을 설정하는 것,
   ####   설정된 조건에 위배되는 값을 컬럼에 저장할 수 없으며 데이터의 무결성을 위한 구문
   * ###### 참고 : NOT NULL 오류시에는 정확한 오류 원인을 알 수 있지만, 그 외 제약조건에서 오류가 발생하면 불분명하다.
     ######       제약조건이 만들어질때 DB안에서 랜덤으로 이름이 만들어지기 때문에 
     ######       개발자는 오류발생시 그 이름을 보고 어떤 제약조건에서 발생한 오류인지 파악하기 힘들다.
     ######       따라서 NOT NULL 제약조건 이외의 제약조건을 만들때, 반드시 이름을 붙여줘야한다.
     
                  * 제약조건쿼리
                  컬럼명 데이터타입 CONSTRAINT (제약조건명) 제약조건
                  
                  * 제약조건명
                  [테이블명]_[컬럼명]_[제약조건약어] 

  <br>
  
  * #### NOT NULL: 컬럼에 NULL을 허용하지 않음


 <br>

```
--NOT NULL: 해당 컬럼에 NULL을 저장할 수 없다.
CREATE TABLE TEST_TABLE1(
    DATA1 NUMBER,
    DATA2 NUMBER NOT NULL
);

--ERROR, DATA2는 NOT NULL 제약조건이 걸려있기 때문에 INSERT시 DATA2 데이터를 반드시 넣어야한다.
INSERT INTO TEST_TABLE(DATA1) VALUES(200); 
INSERT INTO TEST_TABLE(DATA2) VALUES(201);  --DATA2만 넣으면 오류 없음. DATA1은 NULL을 허용하기때문
```

<br>



  * #### UNIQUE: 중복된 값을 허용하지 않음, NULL은 무한대로 저장할 수 있음

 <br>

```
--UNIQUE :중복된 값을 허용하지 않고 NULL은 무한대로 허용한다.

CREATE TAVLE TEST_TABLE2(
    DATA1 NUMBER,
    DATA2 NUMBER CONSTRAINT TEST_TABLE2_DATA2_UK UNIQUE
);
```

<br>

  * #### PRIMARY KEY: 중복된 값을 허용하지 않으며 NULL 값을 허용하지 않음. 각 로우를 구분하기 위한 유일한 값을 저장하기 위해 사용함.

 <br>

```
--PRIMARY KEY : UNIQUE + NOT NULL , 유일한 값을 저장하기 위해 사용
CREATE TABLE TEST_TABLE3(
    DATA1 NUMBER,
    DATE2 NUMBER CONSTRAINT TEST_TABLE_DATA3_PK PRIMARY KEY
);
```


<br>

  * #### FOREIGN KEY: 다른 테이블 혹은 같은 테이블의 컬럼을 참조하는 제약조건. 
  
     * ##### 참조하는 컬럼에 저장되어 있는 값만 컬럼에 저장할 수 있음. 
     * ##### 일반적으로 PRIMARY KEY 제약조건이 설정된 컬럼을 참조.



 <br>

```
--FOREIGN KEY: 특정 테이블의 컬럼을 참조하는 제약조건
--중복과 NULL을 허용
CREATE TABLE TEST_TABLE4(
    DATA1 NUMBER CONSTRAINT TEST_TABLE4_PK PRIMARY KEY,
    DATA2 NUMBER NOT NULL
);

CREATE TABLE TEST_TABLE5(
    DATA3 NUMBER NOT NULL,
    DATA4 NUMBER CONSTRAINT TEST_TABLE5_FK REFERENCES TEST_TABLE4(DATA1)
);
```

<br>


  * #### CHECK : 조건에 만족할 경우 컬럼에 저장할 수 있도록 함.


 <br>

```
--CHECK 제약조건 : 컬럼에 저장될 값을 지정한다.
--중복, NULL허용
CREATE TABLE TEST_TABLE6(
DATA1 NUMBER CONSTRAINT TEST_TABLE6_DATA1_CK CHECK (DATA1 BETWEEN 1 AND 10),
DATA2 NUMBER CONSTRAINT TEST_TABLE6_DATA2_CK CHECK (DATA2 IN (10,20,30))
);
```
