

  #### :pushpin: CONSTRAINT 제약조건 :테이블의 데이터를 저장 혹은 수정할 때 컬럼의 값에 대한 조건을 설정하는 것,
   * ##### 설정된 조건에 위배되는 값을 컬럼에 저장할 수 없으며 데이터의 무결성을 위한 구문
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

<img width="517" alt="20210511091833" src="https://user-images.githubusercontent.com/74708028/117739783-019f5a80-b23a-11eb-8f3b-026d49d06fde.png">

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

<img width="322" alt="20210511091849" src="https://user-images.githubusercontent.com/74708028/117739789-049a4b00-b23a-11eb-9396-0acb191ab2db.png">

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

<img width="352" alt="20210511091854" src="https://user-images.githubusercontent.com/74708028/117739796-07953b80-b23a-11eb-9082-7c2fe7138057.png">

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

<img width="411" alt="20210511091906" src="https://user-images.githubusercontent.com/74708028/117739823-1845b180-b23a-11eb-9ee2-0d7700ffb3f3.png">

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

<img width="411" alt="20210511091920" src="https://user-images.githubusercontent.com/74708028/117739826-1aa80b80-b23a-11eb-9cbd-e8b6c13574cb.png">

<br>

  #### :round_pushpin: 테이블 레벨 제약조건
   * ##### 제약 조건을 설정할 때 각 컬럼마다 지정할 수도 있지만 하단 부분에 몰아서 지정할 수도 있다.
   * ##### 컬럼명 옆에 기술하는 것을 컬럼 레벨, 하단에 몰아서 기술하는 것을 테이블 레벨 제약 조건이라고 부른다.
 
<br>

```
--컬럼 레벨 제약조건
CREATE TABLE TEST_TABLE10(
    DATA1 NUMBER CONSTRAINT TEST_TABLE10_DATA1_PK PRIMARY KEY,
    DATA2 NUMBER NOT NULL CONSTRAINT TEST_TABLE10_DATA2_UK UNIQUE,
    DATA3 NUMBER NOT NULL CONSTRAINT TEST_TABLE10_DATA3_FK
                           REFERENCES EMP(EMPNO),
    DATA4 NUMBER NOT NULL CONSTRAINT TEST_TABLE10_DATA4_CK  CHECK (DATA4 BETWEEN 1 AND 10),
    DATA5 NUMBER NOT NULL CONSTRAINT TEST_TABLE10_DATA5_CK CHECK (DATA5 IN (10,20,30))
);

``` 
  
  <img width="492" alt="20210511092652" src="https://user-images.githubusercontent.com/74708028/117740792-2399dc80-b23c-11eb-8cd5-dc086ec2ceb4.png">

<br>


```
--테이블 레벨 제약조건
CREATE TABLE TEST_TABLE10(
    DATA1 NUMBER ,
    DATA2 NUMBER NOT NULL,
    DATA3 NUMBER NOT NULL,
    DATA4 NUMBER NOT NULL,
    DATA5 NUMBER NOT NULL,
    
    CONSTRAINT TEST_TABLE10_DATA1_PK PRIMARY KEY(DATA1),
    CONSTRAINT TEST_TABLE10_DATA2_UK UNIQUE (DATA2),
    CONSTRAINT TEST_TABLE10_DATA3_FK FOREIGN KEY (DATA3) REFERENCES EMP(EMPNO),
    CONSTRAINT TEST_TABLE10_DATA4_CK CHECK (DATA4 BETWEEN 1 AND 10),
    CONSTRAINT TEST_TABLE10_DATA5_CK CHECK (DATA5 IN (10,20,30))
);
```

<img width="431" alt="20210511092659" src="https://user-images.githubusercontent.com/74708028/117740797-25fc3680-b23c-11eb-9fe3-950f2f21ec4f.png">

<br>

  #### :round_pushpin: 복합키
   * ##### 테이블 레벨 제약조건을 설정할 때 하나이상의 컬럼을 하나의 PRIMARY KEY로 묶어서 사용할 수 있다. 
   * ##### 복합키의 경우 각 컬럼에 중복된 데이터가 허용이 되지만, 한 로우의 모든 복합키 컬럼이 중복되는 것은 허용하지 않는다.


```
--DATA1과 DATA1의 데이터 삽입시 같은 값 같이 넣을 수 없음. 
-- EX) ...(100,100) -> X
-- EX) ...(100,200) AND 또다시 (100,200) -> O
CREATE TABLE TEST_TABLE11(
    DATA1 NUMBER ,
    DATA2 NUMBER ,
    CONSTRAINT TEST_TABLE11_COMBO_PK PRIMARY KEY(DATA1, DATA2)
);
```

<img width="355" alt="20210511093027" src="https://user-images.githubusercontent.com/74708028/117740802-2a285400-b23c-11eb-9bb4-8fcb2d3272fd.png">


<br>

  #### :round_pushpin: 제약조건추가, 제거 
   * ##### 테이블을 생성한 후 제약 조건을 추가하거나 제거하고 싶다면 ALTER 구문을 이용.
   * ##### 추가 : ALTER TABLE [테이블명] ADD [제약조건]
   * ##### 제거 : ALTER TABLE [테이블명] DROP [제약조건]

<br>

```
--제약조건 없이 테이블생성
CREATE TABLE TEST_TABLE20(
    DATA1 NUMBER ,
    DATA2 NUMBER ,
    DATA3 NUMBER ,
    DATA4 NUMBER ,
    DATA5 NUMBER 
);

--NOT NULL 제약조건 추가
ALTER TABLE TEST_TABLE20 
MODIFY DATA1 NOT NULL;

INSERT INTO TEST_TABLE20 (DATA1) VALUES (NULL); --ERROR


--NOT NULL제약조건 제거(NULL 허용하는 컬럼으로 수정)
ALTER TABLE TEST_TABLE20 
MODIFY DATA1 NULL;

```

<img width="308" alt="20210511124939" src="https://user-images.githubusercontent.com/74708028/117755579-71700e00-b257-11eb-8085-8ea3a2581750.png">

<br>

```
--PRIMARY KEY 제약조건 추가
ALTER TABLE TEST_TABLE20
ADD CONSTRAINT TEST_TABLE20_DATA2_PK PRIMARY KEY(DATA2);


--PRIMARY KEY 제약조건 제거
ALTER TABLE TEST_TABLE20 
DROP CONSTRAINT TEST_TABLE20_DATA2_PK;
```

<img width="294" alt="20210511124946" src="https://user-images.githubusercontent.com/74708028/117755589-7634c200-b257-11eb-943f-59179a4e5e77.png">

<br>

```
--FOREIGN KEY 제약조건 추가
ALTER TABLE TEST_TABLE20
ADD CONSTRAINT TEST_TABLE20_DATA3_FK FOREIGN KEY(DATA3)
               REFERENCES EMP(EMPNO);
               
        
--FOREIGN KEY 제약조건 제거
ALTER TABLE TEST_TABLE20 
DROP CONSTRAINT TEST_TABLE20_DATA3_FK;
```

<img width="332" alt="20210511124951" src="https://user-images.githubusercontent.com/74708028/117755594-78971c00-b257-11eb-9020-fb310d5271f4.png">

<br>

```
--UNIQUE 제약조건 추가
ALTER TABLE TEST_TABLE20
ADD CONSTRAINT TEST_TABLE20_DATA4_UK UNIQUE(DATA4);

--UNIQUE 제약조건 제거
ALTER TABLE TEST_TABLE20 
DROP CONSTRAINT TEST_TABLE20_DATA4_UK;

```

<img width="293" alt="20210511124957" src="https://user-images.githubusercontent.com/74708028/117755604-7c2aa300-b257-11eb-9c39-af2185f1ac2b.png">

<br>



```
--CHECK 제약조건 추가
ALTER TABLE TEST_TABLE20
ADD CONSTRAINT TEST_TABLE20_DATA5_CK CHECK(DATA5 BETWEEN 1 AND 10);

--CHECK 제약조건 제거
ALTER TABLE TEST_TABLE20 
DROP CONSTRAINT TEST_TABLE20_DATA5_CK;

```

<img width="406" alt="20210511125007" src="https://user-images.githubusercontent.com/74708028/117755610-7f259380-b257-11eb-93da-2c2e6a86ce18.png">




<br>

  #### :round_pushpin: 제약조건활성/ 비활성
   * ##### DISABLE을 사용하면 제약조건이 비활성화되고 ENABLE을 사용하면 제약조건이 활성화된다.
        * ALTER TABLE [테이블명] ENABLE [제약조건]
        * ALTER TABLE [테이블명] DISABLE [제약조건]
   * ###### 주의: 제약조건의 비활성으로 변경 한 뒤 데이터를 삽입/수정하고 다시 제약조건을 활성화 시킬경우, 다시 전에 데이터들을 제약조건에 맞춰 검사한다. 이때 제약조건에 위배되는 데이터가 있을 경우 활성화가 불가능하다. 
<img width="425" alt="20210511125759" src="https://user-images.githubusercontent.com/74708028/117756272-d6783380-b258-11eb-9a4a-e04715254a71.png">


<br>



```
CREATE TABLE TEST_TABLE40(
    DATA1 NUMBER CONSTRAINT TEST_TABLE40_DATA1_PK PRIMARY KEY,
);

INSERT INTO TEST_TABLE40 (DATA1) VALUES (100);
INSERT INTO TEST_TABLE40 (DATA1) VALUES (100); --ERROR : PRIMARY KEY, 중복불가능

--제약조건 비활성 
ALTER TABLE TEST_TABLE40 
DISABLE CONSTRAINT TEST_TABLE40_DATA1_PK; 

INSERT INTO TEST_TABLE40 (DATA1) VALUES (100); --중복가능해짐

--제약조건 다시 활성화 
ALTER TABLE TEST_TABLE40 
ENABLE CONSTRAINT TEST_TABLE40_DATA1_PK;  --다시 활성화 불가능.

--테이블 내의 데이터 삭제 후 다시 데이터 삽입
DELETE FROM TEST_TABLE40;

INSERT INTO TEST_TABLE40 (DATA1) VALUES (100);
INSERT INTO TEST_TABLE40 (DATA1) VALUES (200); 

ALTER TABLE TEST_TABLE40 
ENABLE CONSTRAINT TEST_TABLE40_DATA1_PK;  

INSERT INTO TEST_TABLE40 (DATA1) VALUES (200); --ERROR : PRIMAEY KEY가 활성화되었으므로, 중복불가
```
<img width="475" alt="20210511130053" src="https://user-images.githubusercontent.com/74708028/117756415-13442a80-b259-11eb-95e6-8b1d413ce1a6.png">

