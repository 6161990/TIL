#### :pushpin: DML(Data Manipulation Language(데이터 조작어)) 
* ##### SELECT : 데이터 베이스에 저장된 데이터를 가져오는 명령문 , 다양한 상황이나 조건에 맞는 데이터를 빠르고 쉽게 가져올 수 있음

<br>

  #### :round_pushpin: 날짜함수
  * ##### 오라클은 날짜 데이터를 제어할 수 있는 함수를 제공한다.
  * ##### SYSDATE : 현재 날짜와 시간을 반환한다.
  * ##### MONTHS_BETWEEN : 두 날짜간의 개월 수를 구한다.
  * ##### ADD_MONTHS : 주어진 개월 수 만큼 더한다.

<br>

```
--현재 날짜 구하기 
SELECT SYSDATE FROM DUAL; --(21/05/08)
```

<img width="220" alt="20210508194345" src="https://user-images.githubusercontent.com/74708028/117537929-d6045080-b03e-11eb-9ae0-187af1ce2e96.png">

<br>

```
--날짜 데이터 연산 (10000일)
SELECT SYSDATE, SYSDATE-10000, SYSDATE+10000 FROM DUAL;
```

<img width="305" alt="20210508194408" src="https://user-images.githubusercontent.com/74708028/117537935-db619b00-b03e-11eb-86cb-df0c680626ff.png">


<br>

```
--각 사원이 입사한 날짜로부터 1000일 후가 되는 날짜를 가져온다.
SELECT HIREDATE, HIREDATE+1000 FROM EMP;
```

<img width="315" alt="20210508194428" src="https://user-images.githubusercontent.com/74708028/117537941-e288a900-b03e-11eb-8c04-d398d081a1eb.png">

<br>

```
--직무가 연극팀인 사원의 입사일 100일전 날짜를 구한다.
SELECT JOB, HIREDATE, HIREDATE-100 FROM EMP WHERE JOB = '연극팀';
```

<img width="362" alt="20210508194647" src="https://user-images.githubusercontent.com/74708028/117537944-e87e8a00-b03e-11eb-9070-94cca53b0f9a.png">

<br>

```
-- 전 사원의 근무일을 가져온다. (소수점은 버린다)
SELECT TRUNC(SYSDATE-HIREDATE) FROM EMP;
```

<img width="249" alt="20210508194811" src="https://user-images.githubusercontent.com/74708028/117537947-efa59800-b03e-11eb-8775-4b417a76f1a1.png">

<br>

```
--반올림 
SELECT SYSDATE, ROUND(SYSDATE,'CC') AS "년도두자리", 
    ROUND(SYSDATE,'YYYY') AS "월기준", --월을 기준으로 년도를 올림할것이냐 현재 4월이면 올림, 8월이면 내림
    ROUND(SYSDATE,'DDD') AS "시기준",  -- 현재 시를 기준으로 날짜를 올림할것이냐 오후면 올림 오전이면 내림
    ROUND(SYSDATE, 'HH') AS "분기준", --현재 분을 기준으로 시를 올림할 것이냐 30분 이후면 올림, 이전이면 내림
    ROUND(SYSDATE,'MM') AS "일기준", --현재 일을 기준으로 월을 올림할 것이냐 15일 이후면 올림, 이전이면 내림
    ROUND(SYSDATE, 'DAY') AS "주기준", -- 현재 주를 기준으로 요일을 올림할 것이냐 일주일의 절반 이상 지나갔다면(목금) 올림, 이전이면 내림
    ROUND(SYSDATE,'MI') AS "초기준" --현재 초를 기준으로 분을 올림할 것이냐 
    FROM DUAL;
```

<img width="670" alt="20210508201210" src="https://user-images.githubusercontent.com/74708028/117537951-f6340f80-b03e-11eb-9407-8667d5afb99e.png">

<br>

```
--버림
SELECT SYSDATE, TRUNC(SYSDATE,'CC') AS "년도두자리" ,
    TRUNC(SYSDATE,'YYYY') AS "월기준", 
    TRUNC(SYSDATE,'DDD') AS "시기준",  
    TRUNC(SYSDATE, 'HH') AS "분기준", 
    TRUNC(SYSDATE,'MM') AS "일기준", 
    TRUNC(SYSDATE, 'DAY') AS "주기준", 
    TRUNC(SYSDATE,'MI') AS "초기준" 
    FROM DUAL;
```

<img width="419" alt="20210508201225" src="https://user-images.githubusercontent.com/74708028/117537956-f9c79680-b03e-11eb-822e-965e59d1568d.png">

<br>


```
-- 2021년에 입사한 사원들의 사원이름, 급여, 입사일을 가져온다.
SELECT EMPNO, ENAME, HIREDATE FROM EMP WHERE HIREDATE BETWEEN '21/01/01' AND '21/12/31';
SELECT ENAME, SAL, HIREDATE FROM EMP WHERE TRUNC(HIREDATE, 'YYYY') = '2021/01/01';
```

<img width="477" alt="20210508201928" src="https://user-images.githubusercontent.com/74708028/117537963-00eea480-b03f-11eb-9546-6616e7f3107e.png">

<br>


```
-- 모든 사원이 근무한 개월 수를 구한다. 
SELECT MONTHS_BETWEEN(SYSDATE, HIREDATE) FROM EMP;
SELECT TRUNC(MONTHS_BETWEEN(SYSDATE, HIREDATE)) FROM EMP; --소수점 버리기
```

<img width="386" alt="20210508202747" src="https://user-images.githubusercontent.com/74708028/117537974-0815b280-b03f-11eb-9c16-6012299b9c94.png">

<br>


```
--개월 수를 더한다. (디폴트는 '일'기준 )
SELECT SYSDATE+100, ADD_MONTHS(SYSDATE,100) FROM DUAL;
```

<img width="318" alt="20210508203102" src="https://user-images.githubusercontent.com/74708028/117537984-119f1a80-b03f-11eb-98b5-959fbdbb4be1.png">

<br>


```
--각 사원들의 입사일 후 100개월 되는 날짜를 구한다.
SELECT HIREDATE, ADD_MONTHS(HIREDATE,100) FROM EMP;
```

<img width="308" alt="20210508205328" src="https://user-images.githubusercontent.com/74708028/117538096-7e1a1980-b03f-11eb-8b5a-5fa6cd8faef9.png">

<br>


```
--지정된 날짜를 기준으로 지정된 다음 요일이 몇일인지 구한다.
SELECT SYSDATE, NEXT_DAY(SYSDATE, '월요일') FROM DUAL;
```

<img width="294" alt="20210508203404" src="https://user-images.githubusercontent.com/74708028/117538019-2a0f3500-b03f-11eb-9bc1-9ea0778d30cc.png">

<br>


```
--지정된 날짜를 기준으로 월의 마지막 날짜를 구한다.
SELECT SYSDATE, LAST_dAY(SYSDATE) FROM DUAL;
```

<img width="276" alt="20210508203527" src="https://user-images.githubusercontent.com/74708028/117538028-33989d00-b03f-11eb-9945-505fa30fc56b.png">

<br>


```
-- TO_CHAR : 오라클 DB의 날짜 -> 프로그램 날짜 형식으로 문자열로 변환
SELECT SYSDATE, TO_CHAR(SYSDATE, 'YYYY-MM-DD HH:MI:SS AM') FROM DUAL;
```

<img width="384" alt="20210508205311" src="https://user-images.githubusercontent.com/74708028/117538088-79edfc00-b03f-11eb-9cc5-e56574050b39.png">


<br>


```
--TO_DATE : 프로그램 -> 오라클 DB 날짜
SELECT TO_DATE('2018-04-30 03:39:20 오후', 'YYYY-MM-DD HH:MI:SS AM') FROM DUAL;
```

<img width="429" alt="20210508204038" src="https://user-images.githubusercontent.com/74708028/117538051-51fe9880-b03f-11eb-9dde-096e0b684b38.png">


<br>

  #### :round_pushpin: DECODE
  * ##### 값에 따라 반환값이 결정되는 구문
  * ##### DECODE(컬럼명, 값1, 반환값1, 값2, 반환값2, 값3, 반환값3)


```
--각 사원의 부서 이름을 가져온다.
SELECT EMPNO, ENAME, 
       DECODE(DEPTNO, 301,'예술팀', 
                      302,'공연팀', 
                      303,'연극팀', 
                      305,'마케팅팀',
                      309,'해외개발팀',
                      310,'페스티벌팀')
FROM EMP;
```

<img width="235" alt="20210509085937" src="https://user-images.githubusercontent.com/74708028/117556817-ed2b5880-b0a7-11eb-9d3d-7212d1d38202.png">

<br>


```
--업무에 따라 인상된 급여액을 가져온다.
--예술팀 : 5%
--공연팀 : 10%
--연극팀 : 15%
--마케팅팀 : 5%
--해외개발팀 : 5%
--페스티벌팀 : 8%

SELECT EMPNO, ENAME, JOB,
       DECODE(JOB,'예술팀', SAL * 1.05, 
                      '공연팀', SAL * 1.1, 
                      '연극팀', SAL * 1.15, 
                      '마케팅팀', SAL * 1.05,
                      '해외개발팀', SAL * 1.05,
                      '페스티벌팀', SAL * 1.08)
FROM EMP;
```
<img width="558" alt="20210509090647" src="https://user-images.githubusercontent.com/74708028/117556827-ffa59200-b0a7-11eb-8298-c78c04642944.png">




<br>

  #### :round_pushpin: CASE
  * ##### 조건에 따라 반환값이 결정되는 구문
  * ##### CASE WHEN 조건식1 THEN 반환값1
         ##### WHEN 조건식2 THEN 반환값2
    ##### END
    
<br>
    
```
--급여액 별 등급을 가져온다.
-- 300 미만 : C등급
-- 300 이상, 500미만 : B등급
-- 500 이상 : A등급
SELECT EMPNO, ENAME, CASE WHEN SAL < 300 THEN 'C등급'
                          WHEN SAL >= 300 AND SAL < 500 THEN 'B등금'
                          WHEN SAL >= 500 THEN 'A등급'
                     END
FROM EMP;
```

 <img width="376" alt="20210509091240" src="https://user-images.githubusercontent.com/74708028/117556829-02a08280-b0a8-11eb-8a4f-efc80a5b12f9.png">
   
<br>
    
```
--직원들의 급여를 다음과 같이 인상한다.
-- 300 미만 : 100%
-- 300 이상, 500미만 : 20%
-- 500 이상 : 10%
SELECT EMPNO, ENAME, 
       CASE WHEN SAL <= 300 THEN SAL * 2
            WHEN SAL > 300 AND SAL <= 500 THEN SAL *1.02
            WHEN SAL >= 500 THEN SAL * 1.01
        END
FROM EMP;
```

<img width="442" alt="20210509091807" src="https://user-images.githubusercontent.com/74708028/117556831-059b7300-b0a8-11eb-9f27-4e0ed9027dfb.png">
