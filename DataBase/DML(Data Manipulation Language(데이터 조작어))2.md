#### :pushpin: DML(Data Manipulation Language(데이터 조작어)) 
* ##### SELECT : 데이터 베이스에 저장된 데이터를 가져오는 명령문 , 다양한 상황이나 조건에 맞는 데이터를 빠르고 쉽게 가져올 수 있음

<br>

  ##### :round_pushpin: 정렬
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

<img width="419" alt="20210508101017" src="https://user-images.githubusercontent.com/74708028/117521373-695e6700-afe8-11eb-8133-b79a7acd6de7.png">

<br>

```
--사원의 이름, 사원번호, 급여를 급여 기준으로 내림차순 정렬한다.
SELECT ENAME, EMPNO , SAL FROM EMP ORDER BY SAL DESC; 
```

<img width="332" alt="20210508101048" src="https://user-images.githubusercontent.com/74708028/117521377-6e231b00-afe8-11eb-94e3-d7d1d3f86f87.png">

<br>

```
--사원의 이름, 사원번호를 이름 기준으로 오름차순 정렬한다.
SELECT ENAME, EMPNO FROM EMP ORDER BY ENAME ASC; 
SELECT ENAME, EMPNO  FROM EMP ORDER BY ENAME; --오름차순은 ASC 생략가능 
```

<img width="416" alt="20210508101215" src="https://user-images.githubusercontent.com/74708028/117521384-77ac8300-afe8-11eb-970d-b86f6710ea8a.png">

<br>

```
--사원의 이름, 사원번호, 입사일을 입사일 기준으로 내림차순 정렬한다.
SELECT ENAME, EMPNO, HIREDATE FROM EMP ORDER BY HIREDATE DESC; 
```

<img width="360" alt="20210508101409" src="https://user-images.githubusercontent.com/74708028/117521393-7e3afa80-afe8-11eb-84fd-11a2c815a986.png">

<br>

```
--2021년에 입사한 사원들의 사원번호, 이름, 입사일을 사원 번호를 기준으로 내림차순 정렬한다.
SELECT EMPNO, ENAME, HIREDATE FROM EMP WHERE HIREDATE BETWEEN '21/01/01' AND '21/12/31'
ORDER BY EMPNO DESC;
```

<img width="496" alt="20210508101833" src="https://user-images.githubusercontent.com/74708028/117521399-885cf900-afe8-11eb-91c2-391fad9b6bf0.png">

<br>

```
-- 사원의 이름, 급여, 커미션을 커미션 기준으로 오름차순 정렬한다. 
-- NULL값은 다 뒤로몰림, 무한대의미로 제일 큰 값이기 때문에
SELECT ENAME, EMPNO , SAL, COMM FROM EMP ORDER BY COMM;
```

<img width="339" alt="20210508102114" src="https://user-images.githubusercontent.com/74708028/117521408-914dca80-afe8-11eb-955a-89e33abbe7f8.png">

<br>

```
--사원의 이름, 사원번호, 급여를 급여 기준으로 내림차순 정렬하고, 값이 같으면 이름을 기준으로 오름차순 정렬한다.
-- 선우정아와 안소희 
SELECT ENAME, EMPNO , SAL FROM EMP ORDER BY SAL DESC, ENAME ASC; 
```

<img width="550" alt="20210508102347" src="https://user-images.githubusercontent.com/74708028/117521413-9a3e9c00-afe8-11eb-97dc-6e248d30ffbe.png">
