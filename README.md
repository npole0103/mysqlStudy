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

DDL(Data Definition Language)  
- CREATE : 테이블 생성
- DROP : 테이블 제거
- ALTER : 테이블 변경
- truncate : 데이터 삭제

DQL(Data Query Language)  
- SELECT : 테이블 내용 검색

DML(Data Manipulation Language)
- INSERT : 테이블 내용 삽입
- DELETE : 테이블 내용 삭제
- UPDATE : 테이블 내용 수정

---
### ALTER TABLE

`ALTER TABLE 테이블명 ADD 새로운컬럼 VARCHAR(20) NULL;` : NULL 값을 허용하며, VARCHAR(20)인 컬럼을 추가함.

`ALTER TABLE 테이블명 DROP COLUMN 컬럼이름;` : 칼럼을 삭제함.

`ALTER TABLE 테이블명 ADD COLUMN 칼럼이름 DECIMAL(5, 2);` : 기존 VARCHAR(20)이었던 데이터 타입을 DECIMAL 형태로 변경


---
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
SELECT id, title, created, author FROM topic WHERE author="npole0103" ORDER BY id ACS;
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

평균 구하는 법 : `SELECT AVG (author_id) AS authorAVG FROM topic;`

똑같은 테이블을 만들어 모든 내용 복사
``` sql
DROP TABLE CustomersNew;

CREATE TABLE CustomersNew
(
  cust_id      char(10 )  NOT NULL ,
  cust_name    char(50 )  NOT NULL ,
  cust_address char( 50)  NULL ,
  cust_city    char(50 )  NULL ,
  cust_state   char(5 )   NULL ,
  cust_zip     char(10 )  NULL ,
  cust_country char( 50)  NULL ,
  cust_contact char( 50)  NULL ,
  cust_email   char(255 ) NULL
);

INSERT INTO CustomersNew
SELECT *
FROM Customers;

SELECT *
FROM CustomersNew;
```

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

### LEFT JOIN, RIGHT JOIN, FULL JOIN

[stack overflow](https://stackoverflow.com/questions/5706437/whats-the-difference-between-inner-join-left-join-right-join-and-full-join)

INNER JOIN : 두 테이블에 일치하는 항목이 있으면 행을 반환.

LEFT JOIN : 오른쪽 테이블에 일치하는 항복이 없더라도 왼쪽 테이블의 모든 행을 반환.

RIGHT JOIN : 왼쪽 테이블에 일치하는 항목이 없더라도 오른쪽 테이블 모든 행 반환.

FULL JOIN : 왼쪽과 오른쪽 OUTER JOIN의 결과를 결합.

+ LEFT OUTER JOIN == LEFT JOIN
+ INNER JOIN == JOIN

---
## Midterm Exam

``` sql

```

### Chap 2
1. Select
``` sql
SELECT * FROM department
```
2. Project
``` sql
SELECT id, name FROM instructor
```
3. Cartiesian Product
``` sql
SELECT * FROM instructor, teaches
```
4. Union & Set intersection
``` sql
SELECT course_id FROM section WHERE semester="Fall" and year="2017" union SELECT course_id FROM section WHERE semester="Spring" and year="2018"

SELECT course_id FROM section WHERE semester="Fall" and year="2017" intersect SELECT course_id FROM section WHERE semester="Spring" and year="2018"
```
5. Set Difference
``` sql
SELECT course_id FROM section WHERE semester="Fall" and year="2017" EXCEPT SELECT course_id FROM section WHERE semester="Spring" and year="2018"
```
6. The Assignment

---
### Chap 3

도메인 타입들
- char(n) : 고정 길이의 스트링 ex) char(5)에 ABC 저장하면 ‘ABC  ’로 저장됨
- varchar(n) : 가변 길이의 스트링 ex) varchar(5)에 ABC 저장하면 ‘ABC’로 저장됨
- int : 각 머신에 의존적이다 64bit 32bit
- smallint : 스몰 인트 동일하게 머신에 의존적
- numeric(p, d) : precision 유효숫자, digit 소숫점 몇까지 볼 것이냐
ex) numeric(3, 1) allows 44.5 to be stores exactly, but not 444.5, 0.32
- real, double precision : real = float, double = double로 보면 됨.
- float(n) : 부동 소수점 최소한의 숫자.

Create Table
``` sql
CREATE TABLE instructor(
  ID char(5),
  name varchar(20) not null,
  dept_name varchar(20),
  salary numeric(8,2),
  primary key(ID),
  foreign key(dept_name) references department
);
```
department 릴레이션의 기본키를 dept_name에 참조하라.

Insert
``` sql
INSERT INTO instructor values ('10211', 'Smith', 'Biology', 66000);
```

Delete : 모든 튜플들을 지움
``` sql
DELETE FROM student
```
Drop Table : 테이블 삭제
``` sql
DROP TABLE R
```
Alter : 컬럼 추가, 컬럼 삭제
``` sql
ALTER TABLE R ADD 어트리뷰트명 타입

ALTER TABLE R DROP 어트리뷰트명
```

Distinct 중복제거
``` sql
SELECT DISTINCT dept_name FROM instructor
```

Select 문자열 / 사칙연산
``` sql
SELECT 'abc' FROM instructor

SELECT ID, name, salary/12 FROM instructor
```

전산학과 교수보다 연봉이 높으면 선택 중복없이
``` sql
SELECT DISTINCT T.name FROM instructor as T, instructor as S WHERE T.salary > S.salary and S.dept_name="Comp. Sci."
```

1. Intro로 시작하는 단어 : Intro%
2. 앞 뒤에 무엇이 있든 Comp를 포함하는 단어 : %Comp%
3. 길이 3의 문자열 : '___'
4. 길이 3이상의 문자열 : '___%'
``` sql
SELECT name FROM instructor WHERE name like '%dar%'
```
정렬 - 오름차순 / 내림차순
``` sql
SELECT DISTINCT name FROM instructor ORDER BY name;
SELECT DISTINCT name FROM instructor ORDER BY name ASC; 

SELECT DISTINCT name FROM instructor ORDER BY name DESC;
```

NULL / NOT NULL : NOT NULL이면 값이 들어있는 값 전부 출력
``` sql
SELECT name FROM instructor WHERE salary is null
SELECT name FROM instructor WHERE salary is not null
```

집계함수
``` sql
SELECT avg(salary) FROM instrutor WHERE dept_name="Comp. Sci."

SELECT count (DISTINCT ID) FROM teaches WHERE semester="Spring" and year="2018"

SELECT count(*) FROM course

SELECT dept_name, avg(salary) as avg_salary FROM instructor GROUP BY dept_name
집계함수 쓰지 않은 어트리뷰트는 전부 GROUP BY 에 넣어줘야함

SELECT dept_name, avg(salary) as avg_salary FROM instructor GROUP BY dept_name HAVING avg(salary) > 42000
```
1. 컴퓨터 사이언스 학과 교수들의 평균 연봉
2. Spring 2018에 수업을 담당하는 교원이 몇명인지
3. course 릴레이션의 모든 튜플의 갯수
4. 각 학과의 평균 연봉
5. 각 학과의 평균 연봉 > 42000 이상

Nested Subqueries 종복된 서브쿼리

서브쿼리 내에 있는 course_id에 해당하는 값만 보겠다는 것임
``` sql
SELECT DISTINCT course_id FROM section WHERE semester="Fall" AND year=2017 AND course_id IN (SELECT course_id FROM section WHERE semester="Spring" and year=2018)
```

some은 해당하는 서브쿼리 내에 있는 어떠한 값보다도 커야함.
만약 10000/9000/8000이 있으면 가장 낮은 8000보다 커야함 하나라도 만족하면 true반환

all은 일부가 아닌 전체이기 때문에 제일 최고 연봉자와 비교해서 제일 커야함.
``` sql
SELECT name FROM instructor WHERE salary > some(SELECT salary FROM instructor WHERE dept_name="Biology")
```

Exists 존재하는지 여부
``` sql
SELECT course_id FROM section as S WHERE semester="Fall" and year=2017 and 
exists(SELECT * FROM section as T 
WHERE semester="Spring" and year=2018 and S.course_id = T.course_id)
```

Exists 공집합이여야 트루가 됨. 생물학과에서 들어야하는 모든 강의를 수강한 것.
``` sql
SELECT DISTINCT S.ID S.name FROM student as S WHERE not exists(
  (SELECT course_id FROM course WHERE dept_name="Biology") except
  (SELECT T.course_id FROM takes as T WHERE S.ID = T.ID)
)
```

Unique : 튜플에 중복값 있는지 없는지 테스트 / 봄 가을에 둘 다 개설되었던 과목은 중복으로 나타나서 false처리 되고 봄 혹은 가을에 한번만 계설되었던 것들만 출력됨.
``` sql
SELECT T.course_id FROM course as T WHERE unique(SELECT R.course_id FROM section as R WHERE T.course_id = R.course_id and R.year=2017)
```

Subqueries in the from : FROM절 안에 중복된 서브 쿼리
``` sql
SELECT dept_name , avg_salary FROM
(
  SELECT dept_name , avg (salary) as avg_salary FROM instructor
GROUP BY dept_name
) WHERE avg_salary > 42000
```

With절 : 쿼리에서 사용될 임시 릴레이션을 만들어 줌
``` sql
with max_budget(value) as (SELECT max(budget) FROM department)
SELECT dept_name FROM department, max_budget WHERE department.budget = max_budget.value;
```

UPDATE
``` sql
UPDATE instructor SET salary = salary * 1.03 WHERE salary > 100000
```

### Chap 4

- Natural Join : 두 테이블의 같은 컬럼 기준으로 조인함. 그래서 정보 손실이 일어날 수 있음.
- Left Outer Join : 왼쪽 테이블을 기준으로 조인
- Right Outer Join : 오른쪽 테이블을 기준으로 조인
- Full Outer Join : 양 테이블 모두를 고려해서 조인
- Inner Join : 둘 다 매칭하는 쪽에 대해서만 조인 Inner는 생략가능

Views : 일종의 가상 릴레이션
뷰는 생성하는 것이 아닌 쿼리문 자체를 객체화 시킴
``` sql
CREATE view faculty as SELECT ID, name, dept_name FROM instructor
```
v1이라는 뷰를 만들 때 v2를 사용했다면 depend directly라고 말함.
직접/간접 둘 다를 표현할 때는 depend on이라고 표현함.

뷰를 정의할 때 쓰였던 쿼리(수식)로 치환됨!!!
이유는 뷰를 저장하게 되면 뷰가 참조하는 테이블에서 변경사항이 일어났을 때 그 데이터를 누락하게 된다. 이때 뷰가 수식으로 참조를 한다면 테이블 변경사항이 업데이트 된 테이블을 참조하게 되므로 데이터 손실이 없다. 그래서 물리적으로 저장하지 않고 쿼리(수식)으로 치환하는 것.

View에서 Update를 허용하는 4가지 경우
1. FROM절에 단 하나의 릴레이션만 존재하는 경우
2. SELECT 문에서는 오로지 어트리뷰트의 이름만 나와야함. (사칙연산, 집계함수 DISTINCT)X
3. SELECT 문에서 등장하지 않은 것들은 NULL로 표시될 수 있어야한다.
4. GROUP BY와 HAVING 문을 사용할 수 없다. (당연함 집계함수를 안 썼으니)

트렌젝션
Commit : 트렌젝션 시작할 때부터 끝날 때까지 실행됐던 쿼리문을 영구적으로 업데이트 하는 것.
Rollback : 트렌젝션 시작할 때부터 끝날 때까지 실행됐던 쿼리문을 취소하는 것. 데이터베이스에 저장되지 않도록 롤백

무결성 조건 : 데이터 베이스에 잘못된 값이 들어와서 데이터베이스가 망가지는 것을 방지해 줌.

- NOT NULL : NULL 값을 허용하지 않는다.
- PRIMARY KEY : 튜플들 구분할 때
- UNIQUE : 유일해야한다. 중복이 없어야 한다.
- CHECK(P), 식을 체크하라

``` sql
check(semester in ('Fall', 'Winter', 'Spring', 'Summer'))
```

참조 무결성
``` sql
foreign key(dept_name) references department (dept_name)
on delete cascade
on update cascade
```
맨 뒤에 dept_name 안 쓰면 department 릴레이션의 기본키가 참조됨.
cascade 옵션을 추가하면 참조 무결성을 깨는 것을 허용함.
참조하고 있는 값을 지워버리면 그 참조 당하는 튜플도 지워짐.

권한 주기/뺏기
``` sql
grant select on department to Amit, Satoshi

revoke select on student from Amit, Satoshi
```
참고 : 뷰에 권한을 줬다고 해서 뷰가 기반으로 하는 테이블에는 아무 권한이 없음

유저별로 역할 설정
``` sql
create role instructor
grant instructor to Amit
```
instructor 라는 역할을 만들고 Amit에게 그 역할을 주라는 뜻.

이외의 권한들
``` sql
grant reference 어트리뷰트명 on 테이블명 to 유저이름
grant select on department to Amit with grant option
revoke select on department from Amit, Satoshi cascade
revoke select on department from Amit, Satoshi restrict
```
1. 외래키를 줄 수 있는 권한을 줌
2. 누군가에게 자신과 똑같은 권한을 부여할 수 있음.
3. cascade를 쓰면 해당 유저 권한 뿐만 아니라 해당 유저가 권한을 준 유저들의 권한도 뺏음
4. restrict을 붙이면 해당 유저가 권한을 준 사람이 없을 때만 revoke를 실행하게 됨.
---
### Chap 5

다이나믹 SQL : 대부분의 쿼리를 스트링으로 저장, 컴파일러는 스트링의 내용을 보진 않음. 런타임을 통해서야 확인이 가능. 컴파일러 입장에서는 쿼리는 그냥 스트링일 뿐. JDBC가 여기 속함.

임베디드 SQL : 다이나믹 SQL과 다르게 컴파일 과정에서 SQL 명령어가 번역이 됨. 런타임시에는 SQL이 수행이 됨.

JDBC
1. Connection을 Open
2. Statement Object 만들기 – 실행하고 싶은 명령어 statement에 저장
3. 스테이트 먼트 오브젝트르 실행해서 결과를 받아옴.
4. 쿼리를 가지고 오다가 에러가 발생하면 예외를 처리하기 위한 매커니즘을 만들어야함.

``` java
Connection conn = DriverManager.getConnection("jdbc:oracle:thin:@db.kw.edu:2000:univdb", userid, passwd);

Statement stmt = conn.createStatement();

stmt.executeUpdate("insert into instructor values('77987', 'Kim', 'Physics', 98000)");

ResultSet set = stmt.executeQuery("SELECT dept_name, avg(salary) FROM instructor GROUP BY dept_name")

while(rset.next())
{
  System.out.println(rest.getString("dept_name") + " " + rset.getFloat(2));
}

stmt.close();
conn.colse();
```
인덱스 넘버가 0번부터 시작하는 것이 아닌 1번부터 시작한다. 어트리뷰트 1번부터 시작

널 값을 처리할 때 NULL이어도 0을 리턴하고, 0이어도 0을 리턴하기 때문에 NULL인지 0인지 알 수 없는데 이때 `rs.wasNull()`함수를 사용하여 NULL을 처리.


SQL 인젝션을 방지하기 위해 PreparedStatement를 사용해야함.
``` java
PreparedStatement pStmt = conn.prepareStatement("insert into instructor value(?,?,?,?)");

pStmt.setString(1, "88877");
pStmt.setString(2, "Perry");
pStmt.setString(3, "Finance");
pStmt.setInt(4, 125000);
pStmt.executeUpdate();
pStmt.setString(1, "88878");
pStmt.executeUpdate();
```

SQL 인젝션
데이터를 입력해야하는 상황에 예를 들어
`X' or 'Y' = 'Y`라는 값을 넣게 되면 쿼리문은 조건을 참으로 인식하여 의도치 않은 상황을 만들게 할 수 있음.

그렇기 때문에  Prepared Statement를 사용해야함. escape character를 사용하여 SQL 공격을 차단할 수 있기 때문.

메타데이터를 가져오는 방법도 있음.
``` java
ResultSet rs;
ResultSetMetaData rsmd = rs.getMetaData();
for(int i = 1 ; i <= rsmd.getColumnCount(); i++)
{
  System.out.println(rsmd.getColumnName(i));
  System.out.println(rsmd.getColumnTypeName(i));
}
```
Security with External Lauguage Routines
외부 functions에 오류가 있다면 DB시스템을 망칠 수 있음. 이러한 것을 방지하기 위해
Sandbox라는 테크닉이 존재함. 외부 데이터베이스 메모리에 접근이 불가능 하도록 공간을 따로 두어서 거기서만 작업하게 됨. 내부 루틴들을 별도의 프로세스로 실행을 해서 DB프로세스에 접근 못하게.
Sandbox를 쓰거나 별도의 프로세스를 써도 오버헤드가 발생하는 건 같음. 공유메모리가 아니기에. 오버헤드 때문에 일부 DB에서는 공유메모리를 쓰는 법도 지원함

Triggers : DB에 변경사항이 생겼을 때 자동으로 실행되도록 되어있는 명령어.

---
### Chap 6

ER - Model
데이터베이스를 새로 구축하거나 DBA가 되면 스키마를 어떻게 디자인하는지 알아야 함.

1. 데이터베이스 사용자가 어떤 데이트를 요구하는가
2. 데이터 모델을 사용해서 스키마로 변환
3. 실제로 데이터베이스를 구현하는 단계

논리적 디자인 : 데이터베이스 스키마 결정
- 데이터베이스 디자이너 : 좋은 테이블
- 비즈니스 결정자 : 어떠한 어트리뷰트
- 컴퓨터 사이언스 관점 : 어느 테이블에 적절히 분배

조심해야할 것
중복된 정보 피하기 : 저장공간의 제약, 버그 유발 가능
불안전한 스키마 사용x : 데이터베이스 스키마를 잘못만들어서 작업을 못할 때

객체 관계 모델
Entitiy Relationship Model
Entity는 어트리뷰트들로 묘사됨. 교원이나 학생을 구분하기 위해선 아이디 교원 번호 학과등의 어트리뷰트들이 필요함. 개체는 사람이라고 보면됨 사람을 구별하기 위해 어트리뷰트가 필요한 것임
Relationship은 객체들 사이에서 발생하는 관계

Derived : 파생된 어트리뷰트. 무언가가 주어졌을 때 계산될 수 있는 속성 ex) 생년월일 주어지면 나이 계산 가능
Domain : 각 어트리뷰트가 가질 수 있는 허용된 값들의 집합.

**제약조건**  
One to One : 하나에 하나만 대응  
One to Many / Many to One : One인 쪽은 선 여러 개 가능. Many 쪽은 하나의 선만 가짐  
Many to Many : 선을 하나만 갖거나 여러개 동시에 가질 수 있음.

**Weak Entity Sets**  
Weak entity는 기본키로 식별을 할 수 없고, identifying entity랑 discriminator라는 약한 엔티티가 가지고 있는 어트리뷰트들이 필요함.
모든 weak entity는 identifying entity랑 연관이 되어 있다. 식별해주는 엔티티 집합에 의존하여 존재한다.
식별해주는 개체 집합은 그것이 식별하는 약한 엔티티 집합을 가지고 있다.
Weak entity set은 두줄로 된 사각형으로 나타낸다. Discriminator는 점선으로 나타낸다.

Compostie 어트리뷰트를 스키마로 표현할 때는 가장 하위 항목들만 저장하라.

Total : 반드시 하나 이상의 관계를 가져야할 때 Total임. 더블라인으로 표시

Partial : 관계를 꼭 형성하지 않아도 되는 것은 한줄로 그으면 됨. 

**Specialization(전문화)** : 상위 수준 엔티티가 여러 하위 수준 엔티티로 분할되는 햐항식 접근방식을 말함. Top-Down 방식임.  
Overlapping : 어떠한 개체가 전문화를 여러게 동시에할 수 있는 것 ex) employee, student  
Disjoint : 둘 중 하나만 선택해야 하는 경우 ex) instructor, secretary  

방법 1  
하위 레벨의 개체 집합은 상위 레벨 개체 집합의 기본키를 포함해야한다.  
만약 학생의 이름을 알고 싶다면 person과 student를 조인 시켜야함.  

방법 2  
상위 레벨 개체 집합 속성까지 모조리 하위 레벨 개체 집합에 저장한다.  
단점 : 정보의 중복저장, 저장공간의 낭비, 데이터 불일치의 문제  

**Generalization(일반화)** : 전문화의 반대 개념. Bottom-Up 방식 아래에서 위로 올라가는 방식.  
전문화와 일반화는 서로 역의 개념이다. 하지만 그려지는 건 똑같기 때문에 엄격하게 구분하진 않음.

total : 무조건 하위 레벨 엔티티 셋에 속해야 함.  
partial : 속하지 않고 그 상태로 머물러도 됨.  

**Aggregation**  
데이터 중복을 막아준다.  
1. 여기서 관계를 어떤 추상적인 개체로 취급함.  
2. 관계와 관계가 관계를 형성할 수 있도록  

**E-R Design Decisions : E-R 모델에서 디자인을 할 때 결정해야하는 사안.**
- 전화번호와 같은 것은 별도의 엔티티셋으로 표현할지 아니면 어트리뷰트로 지니고 있을지
- 학생이 어떠한 분반을 수강하는 것을 관계로 나타낼지, 별도의 개체집합으로 나타낼지
- Binary 쓸지 Non-binary쓸지
- 혼자 식별이 불가능한 약한 게체집합을 형성할지 말지
- 전문화와 일반화를 사용할지 말지
- Aggregation을 사용할지 말지(관계를 통째로 하나의 개체로 취급)

---

Chap 7

**Normalization 데이터베이스 정규화**, 데이터베이스의 구조화를 수행하는 작업

제1정규화 : 모든 값은 atomic 해야한다. 각 Col별로 값이 하나만 있어야 한다.

제2정규화 : 제1정규형을 만족해야하며, 후보키의 진 부분집합만 가지고 다른 항목이 결정되면 안된다.

**함수적 종속성**  
Functional Dependencies  
ID -> name, ID -> address처럼 함수적 종속성이 존재  
ID -> dpet도 성립, dept -> building, dept -> budget도 성립  

**Closure of a Set of Functional Dependencies**  
어떠한 함수적 종속성이 여러 개 있는 set F에서 추론해낼 수 있는 모든 규칙을 끄집어 낸 것을 Closure. F+로 표현

**Trivial Functional Dependencies(사소한 함수적 종속성)**  
ID, NAME이 같으면 ID가 같다. ID, NAME -> ID  
NAME -> NAME

Lossless Decomposition : 무손실 분해를 함수적 종속성을 이용해서 나타내 줌.

Dependency Preservation (함수적 종속성의 보존) : 판별하는데 도음을 주는 조건들

**Boyce-Codd 정규형(1974)** : 제3정규형보다 조건은 간단한데 더 엄격한 정규형  
a -> B 일 때,  
1) a -> B 가 trivial이다(a가 B를 포함하는 더 큰 집합이어야 함.)  
2) a가 슈퍼키이면 된다. (모든 튜플들을 구분할 수 있기 때문에)  
Boyce-Codd 정규형은 정보의 반복을 싫어함.  
Boyce-Codd 정규형은 중복을 싫어하기 때문에 릴레이션을 분해하는데 dependency preserving은 유지되지 않음. 함수의 종속성이 깨짐. 대신 정보 중복의 문제는 해결

**Third Normal Form 제3정규형 (3NF)**  
위 3개중 최소 하나를 따름.  
1) a -> B is trivial (B가 a에 속하느냐)  
2) a is a superkey for R  
3) B – a (베타에만 있는 어트리뷰트들이) 후보키에 속해있다면, 각 어트리뷰트는 서로 다른 후보키에 속해있을 수 있다. 하나하나의 어트리뷰트가 각각의 후보키에만 속해있으면 된다.  

**3NF VS BCNF**  
3NF : 정보손실을 깨지 않고 3NF을 만족시킬 수 있다. 단 중복성이 발생  
BCNF : 중복이 없다. 단 Decomposition(함수적 종속성 깨질 수 있음)이 생기기 때문에 정보손실이 생길 수도 있다.  

둘 다 Lossless Decomposition이 가능하다.  
제3정규형은 함수적 종속성을 보장하지만, BCNF는 보존이 안 될 수도 있다.  

제3정규형에선 NULL값이 등장함, 테이블을 안 나누다보니까, 정보의 반복이 나옴

**Goals of Normalization : 정규화의 목표가 무엇인지**

R을 스미카, F를 함수적 종속성의 집합이라고 할 때, R이 좋은 형태인지 판단해주는 것

만약 좋은 R이 아니라면? 분해를 해야하고 분해한 것들은  
1) 좋은 형태가 되어야함.  
2) 무손실 분해가 되어야 함.3) 가급적이면 함수적 종속성이 안 깨지면 좋다.  

제3정규형도 만약 함수적 종속성이 3조건 중 하나도 만족하지 못한다면 테이블 분해함.

BCNF면 좋고  
Lossless join이며  
함수적 종속성 유지하면 좋다.  

위 3개가 만족할 수 없다면  
1) 함수적 종속성 만족 안된 상태로 BCNF 가던가  
2) 정보를 중복해서 저장해서 3NF로 가서 함수적 종속성을 유지하자.  

SQL에서는 함수적 종속성을 테스트할 수 있는 기능이 없다.  
FDs라는 것이 있긴한데 계산하기가 까다롭다.  
기본키로 설정을 한다면 함수적 종속성을 만족할 수 있다.  
함수적 종속성을 만족하는 것을 썼다고 해도, 그것을 테스트 하는 것이 어렵다.  

나중에 확실히 문제가 될 것이 보인다, JOIN을 엄청 많이 해야할 거 같다면?  
JOIN할 데이터가 엄청 많은 경우 BCNF를 포기하고 제3정규형을 쓰는 것이 좋음.  

---

#### Chap 15 Query Processing
사용자가 쿼리를 작성해서 입력을 하면 Parser가 쿼리를 분석하여 관계대수 형태로 변형을 함. Optimizer는 이 수식을 어떻게 해야 효율적으로 실행할 수 있을지 분석하게 됨.
또한 Statistics about data를 가지고 Execution Plan을 만들어 냄. eveluation engine을 통해 어떤 결과를 사용자에게 보냄.

사용자가 문법을 어겼을 수도 있으니 Parser가 문법을 체크함

**리니어 서치는 효율적이지 않지만 좋은점 3가지**
1. 셀렉션 조건을 어떻게 써줘도 처음부터 끝까지 하나씩 읽음.  
2. 어떠한 순서로 튜플이 저장되어 있어도 다 체크 가능  
3. 인덱스가 있던지 없던지 적용이 가능함.  

**Selection Search 대신 바이너리 서치를 쓰면 안될까?**
1. 데이터가 정렬된 상태가 아니기 때문에 적용 불가
2. 바이너리서치는 Seek를 계속하게 되는데 Seek가 시간이 크기 때문에, 좋지 않다.

**Join**  
Nested-loop Join : 가장 쉬움 For문을 두 번 돌리는 것.

Block Nested Loop Join : 블록 단위로 모든 조합에 대해서 조인을 할지 말지 결정해 줌.

Indexed Nested Loop Join : 전체를 다 볼 필요 없이 색인만 보면 된다. 안쪽에 있는 for루프에서 Index가 있다고 하면 Index 특정 값을 찾을 수 있다.

Hash-Join : 해쉬 함수를 이용하여 Join 하는 것

---

