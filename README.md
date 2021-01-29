# mysqlStudy
MySQLStudy

---
## 실행

1. CMD(윈도우 + R)
2. cd C:\Bitnami\wampstack-7.4.14-0\mysql\bin
3. mysql -uroot -p
4. Enter password

---
## 개념

표(table) : 관계형데이터베이스에서 데이터가 저장되는 공간

스키마(schema) : 연관된 표들을 그루핑 해놓은 일종의 폴더 개념.

데이터베이스 서버 : 스키마가 존재하는 공간을 뜻함.

SQL : Structured Query Language

행 : row, record

열 : column

PRIMARY KEY : 중복을 방지한다라는 의미를 가짐.

---

## 스키마

디비 생성 : `CREATE DATABASE 디비이름;`

디비 삭제 : `DROP DATABASE 디비이름;`

디비 목록 : `SHOW DATABASES;`

디비 사용(스키마 선택) : `USE 디비이름;`

Clear : `system cls;`

---

## 문법

### CREATE TABLE

``` sql
CREATE TABLE topic(
    id INT(11) NOT NULL AUTO_INCREMENT,
    title VARCHAR(100) NOT NULL,
    description TEXT NULL,
    created DATETIME NOT NULL,
    author VARCHAR(30) NULL,
    profile VARCHAR(100) NULL,
    PRIMARY KEY(id));
```

`INT(11)`에서 11에 의미는 데이터를 얼마나 노출할 것이냐 라는 뜻이다. 관행적으로 11을 많이 씀.

`NULL`은 값이 없는 것을 허용한다는 의미.

`NOT NULL`의 의미는 값이 없는 경우를 배제한다는 뜻이다. 공백을 허용하지 않는다라는 의미.

`AUTO_INCREMENT`를 설정하면 데이터가 추가될 때 이전 행의 숫자보다 하나 더 높은 숫자로 자동 설절된다.

`VARCHAR(size)` : size로 설정된 값보다 더 많은 값이 입력되면 초과된 만큼 지워버린다.

`DESC 테이블명;` : Describe table. 테이블의 구조가 나옴.

---
### INSERT TABLE

``` sql
INSERT INTO topic (title, description, created, author, profile) VALUES('MySQL', 'MySQL is....', NOW(), 'npole0103', 'developer');
```

### SELECT

테이블에 들어있는 모든 값 확인

``` sql
SELECT * FROM topic;
```
'*' 기호는 ALL의 의미를 가짐.

테이블에서 특정 열만 확인
``` sql
SELECT id, title, created, author FROM topic;
```

특정 값이 존재하는 행만 읽어오기
```sql
SELECT id, title, created, author FROM topic WHERE author="npole0103";
```

특정 값을 기준으로 정렬하기
``` sql
SELECT id, title, created, author FROM topic WHERE author="npole0103" ORDER BY id DESC;
```

원하는 갯수 만큼만 데이터 확인
``` sql
SELECT id, title, created, author FROM topic WHERE author="npole0103" ORDER BY id DESC LIMIT 2;
```
`LIMIT 2`는 상위 데이터 2개만 보여달라는 것을 나타냄.

---
### UPDATE

``` sql
UPDATE 테이블명 SET  column_name="변경할 내용" WHERE column_name="어떤 열의 값을 바꿀 것인지에 대한 기준값";

UPDATE topic SET description="Oracle is....", title="Oracle" WHERE id=2;
```

### DELETE

---
## etc

### DATABASE 1
데이터를 가공해서 다양한 일을 할 수 있음.

데이터를 저장하고 꺼낼 수 있는 것이 파일. 하지만 파일은 보안이나 성능에 한계를 갖고 있음. 이를 보완한 전문화된 소프트웨어가 데이터베이스임.

CRUD : CREATE READ UPDATE DELETE

데이터 베이스에서 어떻게 데이터를 입력(CREATE UPDATE DELETE)하고 출력(READ)하는지를 알아야 함.

구조적으로 데이터를 저장했을 때 우리가 얻을 수 있는 효과가 큼. 가공력 증대.

데이터 베이스 시장의 절대 강자는 Relational DBMS이다.

MongoDB는 Document store이다.

MySQL은 오픈소스이면서 무료이다.

---
### DATABASE 2

파일 형식의 데이터 관리법에서 정리정돈과 가공하기 용이한 데이터베이스 시스템을 고안해 냄.

1970 IBM에서 Relational Database를 출시.

DBMS를 이용하면 데이터를 표로 정돈할 수 있으며, 정렬 검색과 같은 기능을 안전하고 빠르게 할 수 있다.

스웨덴에서 개발된 MySQL

DBMS와 스프레드 시트의 공통점은 데이터를 표의 형태로 표현해준다.

유저에 따라 권한을 부여하는 것이 가능함.

---




---