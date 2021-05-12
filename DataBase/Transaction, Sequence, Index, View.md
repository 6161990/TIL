  #### :pushpin: 트랜잭션 Transaction
   * ##### 최종 결과를 내기까지 하나의 작업 단위를 의미.
   * ##### Oracle DataBase는 개발자가 전달한 insert, update, delete 문을 메모리상에서만 수행하고 디스크에 반영하지 않음(테이블생성,삭제는 자동 디스크 반영됨)
     #####  => 실수로 인한 데이터의 유실을 막기 위함.
   * ##### 데이터 베이스를 조작하는 작업이 완료되고 모두 정상적으로 되었아면 이를 디스크에 반영해야함.
   * ##### 작업이 시작되고 디스크에 반영될 때까지의 작업의 단위 = 트랜잭션.
        * ##### COMMIT : 트랜잭션을 완료하고 디스크에 반영. 복구 불가 
        * ##### ROLLBACK : 트랜잭션을 취소
        * ##### SAVEPOINT : RALLBACK의 단위를 지정. 지정 시, SAVEPOINT [세이브포인트이름] / 호출 시, ROLLBACK TO [세이브포인트이름]
      
 <br>
 
  #### :round_pushpin: 시퀀스
   * ##### 테이블 내의 컬럼중 PRIMARY KEY를 지정하기 애매한 경우, 1부터 1씩 증가되는 값을 저장하는 컬럼을 추가하여 사용하는 경우, 시퀀스 필요
     ######  => 1부터 1씩 증가되는 값을 구하기 위해 시퀀스 이용
   * ##### [문법]
       * ##### 시퀀스 CREATE SEQUENCE 시퀀스 이름
       * ##### START WITH 숫자  : 시작 값, 시작 값은 절대 최소 값보다 작을 수 없음
       * ##### INCREMENT BY 숫자 : 증가시킬 값
       * ##### MAXVALUE 숫자 OR NOMAXVALUE : 시퀀스가 가질 수 있는 최대값. 생략하거나 NOMAXVALUE일 경우 10의 27승.
       * ##### MINVALUE 숫자 OR NOMINVALUE : 시퀀스가 가질 수 있는 최소값. 생략하거나 NOMINVALUE일 경우 1.
       * ##### CYCLE OR NOCYCLE : 최대 혹은 최소값까지 갈 경우 다시 최소값부터 순환한다.
       * ##### CACHE 숫자 OR NOCACHE : 시퀀스를 메모리상에서 관리할 수 있도록 설정하는 것. (메모리상에서 관리하기 때문에 속도가 향상됨)
       * ##### NEXTVAL : 다음 시퀀스 값
       * ##### CURRVAL : 현재 시퀀스 값 
    
   <br>
   
 ```
--테이블 생성
CREATE TABLE TEST_TABLE20(
    IDX NUMBER CONSTRAINT TEST_TABLE20_IDX_PK PRIMARY KEY,
    NUMBER_DATA NUMBER NOT NULL
);

--시퀀스 생성
CREATE SEQUENCE TEST_SEQ1
START WITH 1
INCREMENT BY 1
MINVALUE 0;

--DATA INSERT
INSERT INTO TEST_TABLE20(IDX, NUMBER_DATA) VALUES(TEST_SEQ1.NEXTVAL,100);
INSERT INTO TEST_TABLE20(IDX, NUMBER_DATA) VALUES(TEST_SEQ1.NEXTVAL,200);

SELECT * FROM TEST_TABLE20;

--시퀀스 제거 시, DROP
DROP SEQUENCE TEST_SEQ1;
 ```
   
   <img width="434" alt="20210512085332" src="https://user-images.githubusercontent.com/74708028/117898339-bbacca00-b2ff-11eb-8b3d-cc7afe167156.png">

  <br>
     
```
--현재 시퀀스 값 가져오기
SELECT TEST_SEQ1.CURRVAL FROM DUAL;
```

<img width="218" alt="20210512085144" src="https://user-images.githubusercontent.com/74708028/117898380-d2532100-b2ff-11eb-80f2-a6ec06f6e958.png">


<br>
      
  #### :round_pushpin: 인덱스
   * ##### 데이터베이스에서 검색속도를 빠르게 하기 위해 사용하는 기능
   * ##### 시스템의 부하를 줄여 성능을 향상시킴
   * ##### 단점 : 추가적인 기억공간이 필요, 인덱스 생성시간이 오래걸림 , 
     #####  INSERT, UPDATE, DELETE와 같은 변경작업이 자주 일어나면 오히려 성능 저하를 가져올 수 있음
   * ##### Oracle DataBase는 테이블 내의 PRIMARY KEY 생성시, 자동으로 인덱스가 세팅됨
   * ##### SO, 검색시 PRIMARY KEY 를 이용하면 속도가 높아짐
   * ##### WHERE 조건절로 자주 검색하는 컬럼이 있다면 그 컬럼에 인덱스를 생성해주면 검색 속도 더 향상된다.

```
--인덱스 조회하기 
SELECT INDEX_NAME, TABLE_NAME, COLUMN_NAME FROM USER_IND_COLUMNS;
```

<img width="430" alt="20210512090446" src="https://user-images.githubusercontent.com/74708028/117899182-8bfec180-b301-11eb-90d5-2a463d2f8cb0.png">

 <br>
 
   #### :round_pushpin: 뷰
   * ##### 데이터 베이스에서 제공하는 가상의 테이블
   * ##### 뷰를 만들 때 사용한 쿼리문을 저장해두고 뷰를 조회할 때 그 쿼리문이 동작하게 되는 원리.
   * ##### 뷰를 사용하면 복잡한 쿼리문을 대신할 수 있기 때문에 개발의 용이성을 가질 수 있음
   * ##### 주의 : 한 개 이상의 테이블을 JOIN 해서 VIEW를 생성할 경우, VIEW로 데이터를 INSERT 할 수 없음. 
      #####    VIEW로 데이터를 INSERT, UPDATE, DELETE할 경우 , 해당 VIEW가 하나의 테이블로 구성되어있어야함.
   * ##### 뷰 생성 권한 설정 : 일반 계정의 경우 뷰를 생성할 수 있는 권한이 없기 때문에 뷰 생성 권한을 설정해줘야함.
      #####     시스템계정으로 DB에 접속한 후, GRANT CREATE VIEW TO [계정이름]
      
![KakaoTalk_20210512_094533195](https://user-images.githubusercontent.com/74708028/117901756-041bb600-b307-11eb-865b-5bd8798b3e13.jpg)

![KakaoTalk_20210512_094533555](https://user-images.githubusercontent.com/74708028/117901772-0aaa2d80-b307-11eb-90f8-dcfb07486397.jpg)

<br>

 
```
--뷰 생성하기
CREATE VIEW [뷰이름] AS [서브쿼리]

--사원의 사원번호, 이름, 급여, 근무부서이름, 근무지역을 가지고 있는 뷰를 생성한다.
CREATE VIEW EMP_DEPT_VIEW
AS 
SELECT A1.EMPNO, A1.ENAME, A2.DNAME, A2.LOC
FROM EMP A1, DEPT A2
WHERE A1.DEPTNO = A2.DEPTNO;


--뷰 조회하기
SELECT * FROM EMP_DEPT_VIEW;
```

<img width="413" alt="20210512094225" src="https://user-images.githubusercontent.com/74708028/117901487-67f1af00-b306-11eb-9752-d2aaeccf086d.png">

<br>

```
--뷰로 데이터 삽입
--뷰로 데이터를 INSERT, UPDATE, DELETE할 경우 , 해당 VIEW가 하나의 테이블로 구성되어있어야함.
CREATE VIEW EMP200_VIEW 
AS
SELECT EMPNO, ENAME, SAL
FROM EMP100;

INSERT INTO EMP200_VIEW (EMPNO, ENAME, SAL) VALUES (7000, '제니', 2000);
```

<img width="419" alt="20210512094230" src="https://user-images.githubusercontent.com/74708028/117901496-6c1dcc80-b306-11eb-8d99-ea52f30b04d7.png">
