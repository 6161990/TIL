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



<br>

  #### :round_pushpin: 숫자함수
  * ##### 컬럼에 저장되어 있는 숫자 값에 대해 처리를 하여 값을 가져올 수 있는 함수들을 의미한다.
  * ##### 가상테이블 **DUAL**
  ```
  --가상의 테이블 ( 어떤 테이블을 적기 애매할 때 데려다 쓰는 DUAL TABLE)
  SELECT 10+10 FROM DUAL;
  ```

<img width="367" alt="20210508103652" src="https://user-images.githubusercontent.com/74708028/117522162-b93f2d00-afec-11eb-9742-1787671e01e3.png">

  * ##### 절대값 구하기
  ```
  --절대값 구하기 ABS
  SELECT -10, ABS(-10) FROM DUAL;
  ```
  
  <img width="214" alt="20210508103741" src="https://user-images.githubusercontent.com/74708028/117522180-d247de00-afec-11eb-89c0-66549746c92e.png">

<br>

 * ##### 기타

```
--전직원의 급여를 300 삭감하고 삭감한 급여액의 절대값을 구한다.
SELECT SAL, SAL -300, ABS(SAL-300) FROM EMP;
```

<img width="327" alt="20210508104003" src="https://user-images.githubusercontent.com/74708028/117522269-526e4380-afed-11eb-8b71-bbd735cf1a1b.png">

<br>

```
--소수점 이하 버림
SELECT 12.3456, FLOOR(12.3456) FROM DUAL; --12
--소수점 이하 버림 , 자리수 지정 
SELECT 1223.3456, TRUNC(1223.3456),TRUNC(1223.3456, 2),TRUNC(1223.3456,-2) FROM DUAL;
```

<img width="483" alt="20210508105755" src="https://user-images.githubusercontent.com/74708028/117522253-3ec2dd00-afed-11eb-8849-0a6f99c93591.png">

<br>

```
--급여가 300이상인 사원의 급여를 15% 삭감한다. 단 소수점 이하는 버린다.
SELECT ENAME ,SAL, SAL*0.85, FLOOR(SAL * 0.85) FROM EMP WHERE SAL >= 300;
```

<img width="441" alt="20210508104556" src="https://user-images.githubusercontent.com/74708028/117522274-5b5f1500-afed-11eb-9461-17fdc29d5b2b.png">

<br>

```
--반올림
SELECT 12.8888, ROUND (12.8888) FROM DUAL;
-- 반올림 자리수 지정 (소수점 이하)
SELECT 12.8888, ROUND (12.8888), ROUND(12.8888, 3) FROM DUAL;
```

<img width="340" alt="20210508105128" src="https://user-images.githubusercontent.com/74708028/117522276-5e5a0580-afed-11eb-8375-74cb1db8b70e.png">

<br>

```
-- 반올림 자리수 지정 (소수점 이상)
SELECT 777.8888, ROUND (777.8888), ROUND(777.8888, -2) FROM DUAL;
```

<img width="367" alt="20210508105147" src="https://user-images.githubusercontent.com/74708028/117522278-6023c900-afed-11eb-93c4-fa9728dd534a.png">


<br>

```
--급여가 400이하인 사원들의 급여를 20%씩 인상한다. 단 1의 자리를 기준으로 반올림한다.
SELECT ENAME, SAL, SAL*1.2, ROUND(SAL*1.2, -1) FROM EMP WHERE SAL <=400;
```

<img width="437" alt="20210508105500" src="https://user-images.githubusercontent.com/74708028/117522281-62862300-afed-11eb-9d71-930def0b0135.png">

<br>

```
--나머지 구하기
SELECT MOD(10,3), MOD(10,4) FROM DUAL;
```

<img width="258" alt="20210508105841" src="https://user-images.githubusercontent.com/74708028/117522312-97927580-afed-11eb-98d7-60975d7a5e4d.png">

<br>

  #### :round_pushpin: 문자열함수
  * ##### 컬럼에 저장되어 있는 문자열에 대해 처리를 하여 값을 가져올 수 있는 함수들을 의미한다.

<br>

```
-- 대문자를 소문자로
SELECT 'ABcdEF', lower('ABcdEF') FROM DUAL;
```

<img width="258" alt="20210508175011" src="https://user-images.githubusercontent.com/74708028/117534861-2cb55e80-b02e-11eb-8145-edc83ddd21a7.png">

<br>

```
--소문자를 대문자로
SELECT 'abcdef', UPPER ('abcdef') FROM DUAL;
```

<img width="264" alt="20210508174929" src="https://user-images.githubusercontent.com/74708028/117534867-30e17c00-b02e-11eb-8b31-023f43fbd7c2.png">

<br>

```
--첫 글자만 대문자로, 나머지는 소문자로
SELECT 'aBCDEF', INITCAP('aBCDEF') FROM DUAL;
```

<img width="261" alt="20210508175024" src="https://user-images.githubusercontent.com/74708028/117534903-553d5880-b02e-11eb-88c5-efc4f35e8e25.png">


<br>

```
--문자열 연결
SELECT CONCAT('ABC','DEF') FROM DUAL;
SELECT CONCAT('KKK',CONCAT('ABC','DEF')) FROM DUAL;
SELECT CONCAT(CONCAT('KKK',CONCAT('ABC','DEF')),'ZZZ') FROM DUAL;
--아래와 위 방법과 같음 취사선택
SELECT '사원들의 이름은' || '이효리' || '이다' FROM DUAL; 
```

<img width="365" alt="20210508180026" src="https://user-images.githubusercontent.com/74708028/117534912-61c1b100-b02e-11eb-8079-303fbdf2c062.png">
<img width="368" alt="20210508180313" src="https://user-images.githubusercontent.com/74708028/117534914-69815580-b02e-11eb-892d-ceaa42e6aa15.png">

<br>

```
--문자열의 길이 (LENGTHB- BYTE 수 , 한글은 2BYTE)
SELECT LENGTH('ABCD'), LENGTHB('ABCD'),LENGTH('안녕하세용'),LENGTHB('안녕하세용') FROM DUAL;
```

<img width="484" alt="20210508180459" src="https://user-images.githubusercontent.com/74708028/117534925-700fcd00-b02e-11eb-879e-a5b96c2ff2ab.png">

<br>

```
--문자열 잘라내기 (SUBSTRB- BYTE 수 , 한글은 2BYTE)
SELECT SUBSTR('ABCD',3),SUBSTRB('ABCD',3), SUBSTR('안녕하세용',3),SUBSTRB('안녕하세용',3) FROM DUAL;

SELECT SUBSTR('ABCDEFGHI',3,4), SUBSTR('동해물과 백두산이',3,4) FROM DUAL;
```

<img width="532" alt="20210508180831" src="https://user-images.githubusercontent.com/74708028/117534929-730abd80-b02e-11eb-831b-39c8ad270c5c.png">

<img width="402" alt="20210508181000" src="https://user-images.githubusercontent.com/74708028/117534947-86b62400-b02e-11eb-8174-e46a8ee85fa2.png">

<br>

```
--문자열 찾기 (인덱스번호가 나옴)
SELECT INSTR('ABCDABCDABCD','CD') FROM DUAL;
SELECT INSTR('ABCDABCDABCD','BC'), INSTR('ABCDABCDABCD','BC',3) FROM DUAL; --3번째 글자 이후의 'BC' 찾기
SELECT INSTR('ABCDABCDABCD','BC',3), INSTR('ABCDABCDABCD','BC',3,2) FROM DUAL; --3번째 글자 이후의 2번째 'BC'묶음 찾기
```

<img width="626" alt="20210508182405" src="https://user-images.githubusercontent.com/74708028/117534956-933a7c80-b02e-11eb-9aed-bc830113b5ba.png">

<br>

```
--사원의 이름 중에 'E'가 두번째 이후에 나타나는 사원의 이름을 가져온다.
SELECT ENAME, SAL  FROM EMP WHERE INSTR(ENAME,'E') >1 ;
```

<img width="383" alt="20210508182731" src="https://user-images.githubusercontent.com/74708028/117534966-9afa2100-b02e-11eb-856a-e657afef28fb.png">

<br>


```
--특정 문자여롤 채우기
SELECT '문자열', LPAD('LEFT PAD',15), RPAD('RIGHT PAD',20) FROM DUAL;
SELECT '문자열', LPAD('LEFT PAD',15,'_'), RPAD('RIGHT PAD',20) FROM DUAL;
```

<img width="399" alt="20210508183418" src="https://user-images.githubusercontent.com/74708028/117534973-a2212f00-b02e-11eb-85ba-5326e16bba68.png">
<br>

```
--공백제거
SELECT '       문자열      ', LTRIM('      LEFT TRIM       '), RTRIM('     RIGHT TRIM      '), TRIM('      TRIM   ') FROM DUAL;
```

<img width="689" alt="20210508183956" src="https://user-images.githubusercontent.com/74708028/117534979-aa796a00-b02e-11eb-9a60-3702c066887c.png">

<br>

```
--문자열 변경
SELECT '김준희', REPLACE('김준희','준','수한무거북이와') FROM DUAL;
```

<img width="348" alt="20210508184057" src="https://user-images.githubusercontent.com/74708028/117534983-aea58780-b02e-11eb-8fd7-bc2093e82129.png">

