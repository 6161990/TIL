#### :pushpin: DML(Data Manipulation Language(데이터 조작어))
* ##### SELECT : 데이터 베이스에 저장된 데이터를 가져오는 명령문 , 다양한 상황이나 조건에 맞는 데이터를 빠르고 쉽게 가져올 수 있음

<br>

  ##### :round_pushpin: 테이블의 모든 컬럼 : SELECT [*] FROM [테이블명] 
```
-- [게시판]의 모든(*) 정보를 가져오기

SELECT * FROM [BOARD];
```
<img width="499" alt="20210507122624" src="https://user-images.githubusercontent.com/74708028/117394152-90f1f880-af30-11eb-90a4-27b43f111a59.png">

<br>

  ##### :round_pushpin: 테이블의 특정 컬럼 : SELECT [가져올 컬럼명] FROM [테이블명]
```
--특정 컬럼의 데이터 가져오기
SELECT [WRITER] FROM [BOARD];
SELECT [WRITER], SUBJECT FROM [BOARD];
```
<img width="266" alt="20210507130128" src="https://user-images.githubusercontent.com/74708028/117396162-5d18d200-af34-11eb-86db-e601629bbe85.png">


<br>

  ##### :round_pushpin: DML 연산 : SELECT [연산할 컬럼1 (+,-,*,/) 연산할 컬럼2)] FROM [테이블명]
```
-- 각 사원들의 급여액과 급여액에서 1000을 더한 값, 200을 뺀 값 등 산술연산
SELECT SAL, SAL +1000, SAL- 200, SAL *2, SAL/2  FROM EMP;
```
<img width="404" alt="20210507125507" src="https://user-images.githubusercontent.com/74708028/117396060-2a6ed980-af34-11eb-949c-5cbc6cc37d89.png">

<br>

  ##### :round_pushpin: DML 연산 NULL 값 처리
```
-- 각 사원의 급여액, 커미션, 급여+ 커미션 액수 산술연산
SELECT SAL, COMM, SAL+COMM  FROM EMP;
```
  <img width="305" alt="20210507125615" src="https://user-images.githubusercontent.com/74708028/117396115-43778a80-af34-11eb-8fdc-a14a415f8b7c.png">

 #### :triangular_flag_on_post: NVL의 이용
 ##### => 데이터 베이스의 정보를 저장하게 되면 row 단위로 저장이 된다. 일부 컬럼은 값을 저장하지 못하는 경우가 발생할 수 있는데, 이 때는 NULL 값이 들어간다. 
 ##### NULL은 '무한대' 또는 '무의미'의 값을 뜻한다. 보통 지금 당장 넣을 값이 없을 때 이용한다. 
 ##### 그러나 연산시 주의할 점은 어떤 값과 NULL을 연산하면 결과는 NULL이 나오게 된다. 
  #####따라서 연산이 필요할 것 같은 경우 NULL을 0으로 사용하고 싶을 때, **NVL** 을 이용한다. 
```
-- NVL을 이용한 커미션, 급여+ 커미션 액수 산술연산 
SELECT SAL, NVL(COMM,0), SAL+NVL(COMM,0) FROM EMP;
=> NVL(COMM,0) : 'COMM' 컬럼에 NULL이 들어가 있으면 '0'을 사용하겠다 
```
<img width="320" alt="20210507130821" src="https://user-images.githubusercontent.com/74708028/117396703-80904c80-af35-11eb-8338-1d75d2b47fdd.png">

<br>

  ##### :round_pushpin: ConCat 연산자를 사용하면 문자열과 컬럼의 값을 연결하여 하나의 문자열로 가져올 수 있다. 
```
-- 문자열 || 컬럼 || 문자열 || 컬럼
--사원들의 이름과 직무를 다음 양식으로 가져온다.
-- 000사원의 담당 직무는 XXX입니다.
SELECT ENAME || '사원의 담당 직무는 ' || JOB || '입니다' FROM EMP;
```
<img width="380" alt="20210507131250" src="https://user-images.githubusercontent.com/74708028/117397202-905c6080-af36-11eb-9e58-f24f182f1107.png">

<br>

  ##### :round_pushpin: Distinct를 사용하면 가져온 로우들 중 중복된 로우를 제거하여 가져올 수 있다.
```
-- SELECT DISTINCT [컬럼명] FROM [테이블명]
--사원들이 근무하고 있는 근무 부서의 번호를 가져온다.
SELECT DEPTNO FROM EMP;
SELECT DISTINCT DEPTNO FROM EMP;
```
<img width="289" alt="20210507131445" src="https://user-images.githubusercontent.com/74708028/117397282-b71a9700-af36-11eb-9863-b7a911f0e9a7.png">
<img width="294" alt="20210507131436" src="https://user-images.githubusercontent.com/74708028/117397284-b84bc400-af36-11eb-89c3-afb76e770276.png">
