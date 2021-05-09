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



<br>

  #### :round_pushpin: JOIN
  * ##### 두 개 이상의 테이블에 있는 컬럼의 값을 한번에 가져오기위해 사용하는 것이 조인이다.
  * ##### SELECT 컬럼명 FROM 테이블 1, 테이블 2 ; 
  * ##### 두 개 이상의 테이블을 조인하게 되면 다대다의 관계로 가져오기 때문에 테이블 1의 로우의 수 X 테이블 2의 로우이 수 만큼 로우를 가져오게 된다.
  * ##### 조건 : 두 개 이상의 테이블에서 가져온 결과 중에 정확한 결과면 가져오기 위해 공통부 부분을 이용한 조건문이 반드시 필요하다


<br>

```
--공통부 DEPTNO
SELECT * FROM EMP, DEPT WHERE EMP.DEPTNO = DEPT.DEPTNO;
SELECT * FROM EMP A1, DEPT A2 WHERE A1.DEPTNO = A2.DEPTNO; --별칭사용
```

<img width="419" alt="20210509175507" src="https://user-images.githubusercontent.com/74708028/117566127-c729a680-b0ef-11eb-8cb5-e0e827052546.png">

<br>

```
--사원의 사원번호, 이름, 근무부서 이름을 가져온다.
SELECT A1.EMPNO, AL.ENAME, A2.DNAME FROM EMP A1, DEPT A2 WHERE A1.DEPTNO = A2.DEPTNO;
```

<img width="462" alt="20210509175514" src="https://user-images.githubusercontent.com/74708028/117566129-c98c0080-b0ef-11eb-8001-ba5ce659ab71.png">


<br>

```
--DALLAS에 근무하고 있는 사원들의 사원번호, 이름, 직무를 가져온다.
SELECT A1.EMPNO, AL.ENAME, A1.JOB FROM EMP A1, DEPT A2 WHERE A1.DEPTNO = A2.DEPTNO AND A2.LOC = 'DALLAS';
```

<img width="568" alt="20210509175527" src="https://user-images.githubusercontent.com/74708028/117566132-cb55c400-b0ef-11eb-9e33-3d8955c89e38.png">


<br>

```
--각 사원들의 사원번호, 이름, 급여, 급여등급을 가져온다.
SELECT A1.EMPNO, A1.ENAME, A1.SAL, A2.GRADE FROM EMP A1, SALGRADE A2 
       WHERE A1.SAL BETWEEN A2.LOSAL AND A2.HISAL;

```

<img width="370" alt="20210509175534" src="https://user-images.githubusercontent.com/74708028/117566135-cd1f8780-b0ef-11eb-9b48-71be3ce0d452.png">


<br>

```
--SALES 부서에 근무하고 있는 사원의 사원번호, 이름, 급여등급을 가져온다.
SELECT A1.EMPNO, A1.ENAME, A2.GRADE FROM EMP A1, SALGRADE A2, DEPT A3
       WHERE A1.SAL BETWEEN A2.LOSAL AND A2.HISAL AND A1.DEPTNO = A3.DEPTNO
       AND A3.DNAME ='SALES';
```

<img width="412" alt="20210509175539" src="https://user-images.githubusercontent.com/74708028/117566136-d01a7800-b0ef-11eb-92a4-bdf4906c9253.png">



<br>

  #### :round_pushpin: SELF JOIN , 같은 테이블을 두 번 이상 조인하는 것. 

<br>

```
--SMITH 사원의 사원번호, 이름, 직속상관 이름을 가져온다.
-- A1 ; SMITH 사원의 정보
-- A2 ; 직속상관의 정보
SELECT A1.EMPNO, A1.ENAME, A2.ENAME FROM EMP A1, EMP A2 WHERE A1.MGR = A2.EMPNO AND A1.ENAME='SMITH';
```

  <img width="554" alt="20210509180712" src="https://user-images.githubusercontent.com/74708028/117566471-b843f380-b0f1-11eb-9536-c84dea9a87ba.png">

  

<br>

```
--FORD 사원 밑에서 일하는 사원들의 사원번호, 이름 , 직무를 가져온다.
-- A1 ; FORD 의 정보
-- A2 ; 부하 직원의 정보
SELECT A2.EMPNO, A2.ENAME, A2.JOB FROM EMP A1, EMP A2 WHERE A1.EMPNO = A2.MGR AND A1.ENAME='FORD';
```

<img width="549" alt="20210509180717" src="https://user-images.githubusercontent.com/74708028/117566477-b9752080-b0f1-11eb-916a-6c72313cce6f.png">


<br>

#### :round_pushpin:  OUTER JOIN : 조인 조건에 해당하지 않기 때문에 결과에 포함되지 않는 로우까지 가져오는 조인


```
--각 사원의 이름, 사원번호, 직장상사 이름을 가져온다. 단 직속 상관이 없는 사원도 가져온다.
-- A1 ; 각 사원의 정보
-- A2 ; 직장상사의 정보 
SELECT A1.ENAME, A1.EMPNO, A2.ENAME FROM EMP A1, EMP A2 WHERE A1.MGR = A2.EMPNO(+); --직속상관이 없는 쪽(NULL)에 +
```

<img width="615" alt="20210509180723" src="https://user-images.githubusercontent.com/74708028/117566480-c09c2e80-b0f1-11eb-8887-52e1e7c51e3b.png">
<img width="197" alt="20210509180407" src="https://user-images.githubusercontent.com/74708028/117566486-c560e280-b0f1-11eb-9823-f2d6c66d4de1.png">



<br>

#### :round_pushpin: 서브쿼리, 쿼리문 안에 들어가는 쿼리문. 쿼리문 작성시 사용되는 값을 다른 쿼리문을 통해 구해야 할 경우 사용한다.

<br>

```
--SCOTT 사원이 근무하고 있는 부서의 이름을 가져온다.
SELECT DNAME FROM DEPT WHERE DEPTNO = (SELECT DEPTNO FROM EMP WHERE ENAME = 'SCOTT');
SELECT A2.DNAME FROM AMP A1, DEPT A2 WHERE A1.DEPTNO = A2.DEPTNO AND A1.ENAME = 'SCOTT'; --JOIN문을 이용해도됨
```

<img width="589" alt="20210509190633" src="https://user-images.githubusercontent.com/74708028/117568077-b5e59780-b0f9-11eb-9c76-65ba27b510cd.png">


<br>

```
--MARTIN과 같은 직무를 가지고 있는 사원들의 사원번호, 이름, 직무를 가져온다.
SELECT EMPNO, ENAME, JOB FROM EMP WHERE JOB =(SELECT JOB FROM EMP WHERE ENAME ='MARTIN');
```

<img width="480" alt="20210509190639" src="https://user-images.githubusercontent.com/74708028/117568080-b8e08800-b0f9-11eb-9a81-a64e1e2ec5d7.png">


<br>

```
--CHICAGO 지역에 근무하는 사원들 중 BLAKE가 직속상관인 사원들의 사원번호, 이름, 직무를 가져온다.
SELECT EMPNO, ENAME, JOB FROM EMP WHERE DEPTNO = (SELECT DEPTNO FROM DEPT WHERE LOC='CHICAGO') 
                                        AND MGR = (SELECT EMPNO FROM EMP WHERE ENAME ='BLAKE');
```

<img width="513" alt="20210509190645" src="https://user-images.githubusercontent.com/74708028/117568083-bb42e200-b0f9-11eb-965d-aea6abb3342e.png">'



<br>

#### :round_pushpin: 결과가 하나 이상인 서브쿼리 연산자 이용 : 서브쿼리를 통해 가져온 결과가 하나 이상인 경우 결과를 모두 만족하거나 결과 중 하나만 만족하거나 해야하는 경우
  * ##### IN : 서브쿼리의 결과 중 하나라도 일치하면 조건은 참이 된다.
  * ##### ANY, SOME : 서브쿼리의 결과와 하나이상 일치하면 조건은 참이된다. 
  * ##### ALL : 서브쿼리의 결과와 모두 일치해야 조건은 참이된다. 

<br>

```
-- 3000 이상의 급여를 받는 사원들과 같은 부서에 근무하고 있는 사원의 사원번호, 이름, 급여를 가져온다.
--ERROR QUERY. WHY? 뒤의 서브쿼리가 결과가 2개 이상이 나오기 때문에 그 중 어떤 하나를 기준으로 WHERE해야하는지 알 수 없기에
SELECT EMPNO, ENAME, SAL FROM EMP WHERE DEPTNO =( SELECT DEPTNO FROM EMP WHERE SAL >= 3000);
--아래와 같이 수정해야함 IN
SELECT EMPNO, ENAME, SAL FROM EMP WHERE DEPTNO IN ( SELECT DEPTNO FROM EMP WHERE SAL >= 3000);
```

<img width="606" alt="20210509194038" src="https://user-images.githubusercontent.com/74708028/117569028-7ec5b500-b0fe-11eb-88fc-f6c1f7a97a86.png">

<br>

```
--각 부서별 급여 평균보다 더 많이 받는 사원의 사원번호, 이름, 급여를 가져온다.
--각 DEPTNO의 평균 급여를 구한 후 , 모든 부서 평균보다 급여가 높은 사원을 가져와야하기 때문에 ALL
SELECT EMPNO, ENAME, SAL FROM EMP WHERE SAL > ALL (SELECT AVG(SAL) FROM EMP GROUP BY DEPTNO);
-- 즉, 모든 부서에서 최고 급여 평균 값보다 높은 사원을 구하면 되는 것이므로 MAX
SELECT EMPNO, ENAME, SAL FROM EMP WHERE SAL > (SELECT MAX(AVG(SAL)) FROM EMP GROUP BY DEPTNO);
-- 각 부서별 급여 평균보다 더 적게 받는 사원의 사원번호, 이름, 급여를 가져온다. MIN
SELECT EMPNO, ENAME, SAL FROM EMP WHERE SAL < (SELECT MIN(AVG(SAL)) FROM EMP GROUP BY DEPTNO);
```

<img width="509" alt="20210509194050" src="https://user-images.githubusercontent.com/74708028/117569030-81c0a580-b0fe-11eb-84b1-b3c892b026c9.png">

<br>

```
-- DALLAS에 근무하고 있는 사원들 중 가장 나중에 입사한 사원의 입사 날짜보다 더 먼저 입사한 사원들의 사원번호, 이름, 입사일을 가져온다.
SELECT EMPNO, ENAME, HIREDATE FROM EMP WHERE HIREDATE < ANY (SELECT HIREDATE FROM EMP WHERE DEPTNO = (SELECT DEPTNO FROM DEPT WHERE LOC='DALLAS'));
```


<img width="784" alt="20210509194057" src="https://user-images.githubusercontent.com/74708028/117569033-84bb9600-b0fe-11eb-8448-2d9773b941bf.png">
