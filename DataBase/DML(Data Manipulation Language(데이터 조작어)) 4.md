#### :pushpin: DML(Data Manipulation Language(데이터 조작어)) 
* ##### SELECT : 데이터 베이스에 저장된 데이터를 가져오는 명령문 , 다양한 상황이나 조건에 맞는 데이터를 빠르고 쉽게 가져올 수 있음

<br>

  #### :round_pushpin: 그룹함수, SELECT 문을 통해 가져올 결과를 그룹으로 묵고 그룹 내에서 지정된 컬럼의 총합, 평균 등을 구할 수 있는 함수
  * ##### SUM : 총합
  * ##### AVG : 평균
  * ##### COUNT : 로우의 수
  * ##### MAX : 최대값
  * ##### MIN : 최소값

<br>

```
--사원들의 급여 총합을 구한다.
SELECT SUM(SAL) FROM EMP;
--그룹함수(1줄) 다른 컬럼(1줄이상 나옴) 을 묵는 것은 ERROR 'NOT A SINGLE-GROUP FUNCTION'
SELECT EMPNO, SUM(SAL) FROM EMP; --ERROR
```

<img width="451" alt="20210509092947" src="https://user-images.githubusercontent.com/74708028/117557234-dbe44b00-b0ab-11eb-8fb6-62b037db87d6.png">


<br>

```
--급여가 500 이상인 사원들의 급여 총합을 구한다.
SELECT SUM(SAL) FROM EMP WHERE SAL >= 500; --520

--연극팀에 근무하고 있는 사원들의 급여 총합을 구한다.
SELECT SUM(SAL) FROM EMP WHERE JOB='연극팀';
```

<img width="290" alt="20210509093318" src="https://user-images.githubusercontent.com/74708028/117557237-e0a8ff00-b0ab-11eb-9c39-9442e109226a.png">

<br>

```
--전 사원의 급여 평균을 구한다.
SELECT AVG(SAL) FROM EMP;
SELECT TRUNC(AVG(SAL)) FROM EMP; --소수점버리기
```

<img width="259" alt="20210509093530" src="https://user-images.githubusercontent.com/74708028/117557240-e4d51c80-b0ab-11eb-83f6-bb96e5a773fe.png">

<br>

```
--커미션을 받는 사원들의 커미션 평균을 구한다. 
--( 커미션 받는 사원 9명, 그룹함수에서 NULL(4명)은 빠지고 계산된다)
SELECT COMM FROM EMP;
SELECT TRUNC(AVG(COMM)) FROM EMP;
```

<img width="339" alt="20210509094048" src="https://user-images.githubusercontent.com/74708028/117557242-eb639400-b0ab-11eb-9408-6c9fb6ab7e80.png">


<br>

```
-- 전 사원의 커미션의 평균을 구한다. 전 사원 13명 
SELECT TRUNC(AVG(NVL(COMM,0))) FROM EMP;
```

<img width="248" alt="20210509094101" src="https://user-images.githubusercontent.com/74708028/117557243-edc5ee00-b0ab-11eb-9679-89592f0debe4.png">


<br>

```
-- 커미션을 받는 사원들의 급여 평균을 구한다.
SELECT TRUNC(AVG(SAL)) FROM EMP WHERE COMM IS NOT NULL;
```

<img width="300" alt="20210509094201" src="https://user-images.githubusercontent.com/74708028/117557246-f1f20b80-b0ab-11eb-998b-addc6aeac12f.png">



<br>

```
--사원들의 총 수를 가져온다. 두 결과는 같음
SELECT COUNT(EMPNO) FROM EMP;
SELECT COUNT(*) FROM EMP;
```

<img width="221" alt="20210509094526" src="https://user-images.githubusercontent.com/74708028/117557248-f4ecfc00-b0ab-11eb-8b80-b18b10f2753b.png">


<br>

```
--사원들의 급여 최대, 최소값을 가져온다.
SELECT MAX(SAL), MIN(sAL) FROM EMP;
```

<img width="208" alt="20210509094609" src="https://user-images.githubusercontent.com/74708028/117557251-fae2dd00-b0ab-11eb-90d5-50ae141048f1.png">


<br>

  #### :round_pushpin: GROUP BY, 그룹함수를 사용할 경우, SELECT ~ FROM ~ WHERE 절까지 모두 수행하여 가져온 결과를 하나의 그룹으로 묶어 총합, 평균 등을 구할 수 있다.
  * ##### GROUP BY 절을 사용하면 SELECT문을 수행하여 가져온 하나의 결과를 여러 그룹으로 나눠 그룹 각각의 총합과 평균 등을 구할 수 있다.
  * ##### SELECT 컬럼명 FROM 테이블명 WHERE 조건절 GROUP BY 그룹기준 ORDER BY 정렬기준

<br>

```
-- 각 부서별 사원들의 급여 평균을 구한다.
SELECT JOB, SUM(SAL) FROM EMP GROUP BY JOB;

```


<img width="270" alt="20210509165019" src="https://user-images.githubusercontent.com/74708028/117564602-d147a700-b0e7-11eb-9689-50853f9b2621.png">

<br>

```
--300 이상 급여를 받는 사원들의 부서별 급여 평균을 구한다.
SELECT DEPTNO, AVG(SAL) FROM EMP WHERE SAL >= 300 GROUP BY DEPTNO;
```


<img width="381" alt="20210509165535" src="https://user-images.githubusercontent.com/74708028/117564598-cd1b8980-b0e7-11eb-9b2f-9971b8b9e3c4.png">




<br>

  #### :round_pushpin: HAVING
  * ##### GROUP BY로 묶인 각 그룹들 중에 실제 가져올 그룹을 선택할 조건을 HAVING 절에 작성한다.
  * ##### HAVING은 GROUP BY 절의 조건이 된다. 
  * ##### WHERE은 ROW의 조건, HAVING은 GROUP BY의 조건


<br>

```
--부서별 평균 급여가 400이상인 부서의 급여 평균을 가져온다.
SELECT DEPTNO, AVG(SAL) FROM EMP GROUP BY DEPTNO HAVING AVG(SAL) >= 400; 
```

<img width="397" alt="20210509170325" src="https://user-images.githubusercontent.com/74708028/117564952-d0177980-b0e9-11eb-8afa-eca1567969b3.png">

<br>

```
--부서별 최대 급여액이 300이하인 부서의 급여 총합을 가져온다.
SELECT SUM(SAL) FROM EMP GROUP BY DEPTNO HAVING MAX(SAL) >= 300;
```

<img width="379" alt="20210509170450" src="https://user-images.githubusercontent.com/74708028/117564954-d279d380-b0e9-11eb-96e1-6dd705f91944.png">

<br>

```
--부서별 최소 급여액이 300이하인 부서에서 직무가 마케팅팀인 사원들의 급여 총합을 구한다.
SELECT SUM(SAL) FROM EMP WHERE JOB='마케팅팀' GROUP BY DEPTNO HAVING MIN(SAL) <=300;
```

<img width="460" alt="20210509171018" src="https://user-images.githubusercontent.com/74708028/117564956-d574c400-b0e9-11eb-90e5-ca653e085b61.png">
