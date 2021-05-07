###  :pushpin: 오라클 데이터 베이스 Oracle SQL DataBase

<br>

<img src="https://user-images.githubusercontent.com/74708028/117399494-a9b3db80-af3b-11eb-9271-503cd03616f1.jpg" width="400" height="200">

SQL용어 | 관계형데이터베이스용어 | 설명 
 -- | -- | --
 로우 | 튜플 또는 레코드 | 하나의 항목을 대표하는 데이터
 컬럼 | 속성(Attribute) 또는 필드 | 튜플의 이름 요소 (예:"주소","태어난 날짜")
 테이블 |관계 또는 기초 관계 변수 | 같은 속성을 공유하는 튜플의 모임(컬럼이나 로우의 모임)
* #### 데이터 딕셔너리 : 시스템 카탈로그라고 부르기도 하며 사용 가능한 데이터 베이스 및 테이블의 정보를 가지고 있는 시스템 테이블
* #### DBMS 만이 추가, 수정, 삭제가 가능하며 사용자는 조회만 가능함.

<br>

* #### 테이블 목록 조회 
  #####  : 현재 접속한 데이터 베이스 내의 테이블을 조회
```
 SELECT * FROM TAB;
```
<img width="278" alt="20210423085720" src="https://user-images.githubusercontent.com/74708028/117389835-fab9d480-af27-11eb-81e7-30187f89ee24.png">

<br>

* #### 테이블 정보 조회 
  #####  : 원하는 테이블의 구조를 조회
```
 DESC [테이블명];
```
<img width="223" alt="20210507113223" src="https://user-images.githubusercontent.com/74708028/117389841-fdb4c500-af27-11eb-9df1-bb13345bf66c.png">


<br>

#### :round_pushpin: SQL 명령문
* ##### 관계형 데이터 베이스 관리 시스템에서 데이터를 관리하기 위해 설계된 특수 목적의 프로그래밍 언어
* ##### SQL 문은 표준 언어와 비표준 언어로 나뉘며 표준 언어는 모든 RDBMS 제품군들이 지원하고 비 표준 언어는 특정 RDBMS에서만 지원됨

<br>

#### :triangular_flag_on_post: DDL(Data Definition Language(데이터 정의어))
* ##### 테이블과 인덱스의 구조를 관리하는 언어
* ##### create, drop, alter 등

<br>

#### :triangular_flag_on_post: DML(Data Manipulation Language(데이터 조작어))
###### * 참고: [DML, 기본 쿼리문 및 SELECT](https://github.com/6161990/TIL/blob/main/DataBase/DML(Data%20Manipulation%20Language(%EB%8D%B0%EC%9D%B4%ED%84%B0%20%EC%A1%B0%EC%9E%91%EC%96%B4)).md)
* ##### 테이블 등에 데이터를 저장, 수정, 삭제, 추출 등을 처리하는 언어
* ##### insert, update, delete, select 등

<br>

#### :triangular_flag_on_post: DCL(Data Control Language(데이터 제어어))
* ##### 사용자 권한, 작업의 취소 등을 처리할 수 있는 언어 
* ##### grant, revoke, commit, rollback 등
