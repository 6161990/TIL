#### :pushpin: DML(Data Manipulation Language(데이터 조작어)) 
* ##### SELECT : 데이터 베이스에 저장된 데이터를 가져오는 명령문 , 다양한 상황이나 조건에 맞는 데이터를 빠르고 쉽게 가져올 수 있음

<br>

  #### :round_pushpin: 정렬
  * ##### SELECT 문을 통해 얻어온 결과를 특정 컬럼을 기준으로 오름차순 혹은 내림차순으로 정렬할 수 있다.
  * ##### 숫자, 문자열, 날짜 등 모든 타입의 데이터를 정렬할 수 있다.
  * ##### SELECT [컬럼명] FROM [테이블명] WHERE (조건절) ORDER BY [컬럼명] (ASC|DESC)
       * ###### ASC : 오름차순 , 생략가능
       * ###### DESC : 내림차순

<br>

```
--사원의 이름, 사원번호, 급여를 급여 기준으로 오름차순 정렬한다.
SELECT ENAME, EMPNO , SAL FROM EMP ORDER BY SAL ASC; 
SELECT ENAME, EMPNO , SAL FROM EMP ORDER BY SAL; --오름차순은 ASC 생략가능 
```
