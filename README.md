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

테이블 명 변경.
`RENAME TABLE '기존 테이블 이름' TO '새로운 이름';`

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

※ WHERE 을 넣지 않으면 모든 행이 변경하고자 하는 열 값으로 변경됨.

---
### DELETE
id값이 5인 행을 삭제.
``` sql
DELETE FROM topic WHERE id=5;
```

---

### JOIN

관계형 데이터베이스에서 가장 중요시 되는 개념.

``` sql

전체 출력
SELECT * FROM topic LEFT JOIN author ON topic.author_id=author.id;


author_id와 author.id 제외하고 출력
SELECT topic.id, title, description, created, name, profile FROM topic LEFT JOIN author ON topic.author_id=author.id;

topic의 id값을 topic_id로 변경 'AS'사용
SELECT topic.id AS topic_id, title, description, created, name, profile FROM topic LEFT JOIN author ON topic.author_id=author.id;

```

[INNER JOIN, LEFT JOIN, RIGHT JOIN, FULL JOIN](https://stackoverflow.com/questions/5706437/whats-the-difference-between-inner-join-left-join-right-join-and-full-join)

---
### 인터넷과 데이터베이스의 관계

Client - Server 
클라이언트에선 request를 서버에 보내고 서버는 response를 클라이언트에 보냄.

MySQL monitor가 Database의 client이며, 명령어로 조작하는 프로그램임.

MySQL workbench도 Client이며, GUI기반의 프로그램임.

수많은 클라이언트가 하나의 데이터베이스 서버를 이용해서 정보를 주고 받는 것이 가능해 짐.

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

관계형 데이터베이스가 필요한 이유 : 중복의 발생 시키지 않으면서, 유지보수가 훨씬 쉬워짐. 저장은 분산되게 하며 결과는 합쳐서 보여주는 것이 요구됨.

`./mysql -uroot -p -h127.0.0.1` : 원하는 IP에 있는 MySQL 서버로 접속가능.

다만 -h를 생략하면 Default로 Monitor(Client)가 설치되어있는 MySQL Server를 가르킴.

데이터가 많아지면 데이터를 관리하기 힘들기 때문에 처음부터 정리정돈을 잘해야 함.

INDEX(색인) : 데이터가 많아지면 Index(색인) 기능을 활용하면 미리 읽어놨던(많이 접근하기에 미리 뽑아놓은) 데이터를 빠르게 읽어올 수 있다.

Modeling(모델링) : 테이블 설계를 효율적으로 중복없이 더 좋은 성능으로 하는 것.

Backup(백업) : 백업의 기본적인 원리는 데이터를 복제해서 보관. 키워드 : mysqldump, binary log

Cloud(클라우드) : 큰 회사들이 운영하고 있는 인프라 위에 있는 컴퓨터를 사용하는 것이 클라우드컴퓨팅 기술임. 원격제어를 통해 다룸. AWS RDS, Google Cloud SQL for MySQL, AZURE Database for MySQL

프로그래밍 : Python mysql api, PHP mysql api, Java mysql api

---