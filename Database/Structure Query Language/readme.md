# SQL(Structure Query Language)

1. 기본 데이터베이스 지식
- varchar
    - Variable length char, 가변 길이의 문자열을 담는 공간이다.
    - varchar(50)이 선언된 컬럼에 abc만 넣는다면 47개는 공간 할당이 되지 않는 것이다.

2. DML(Data Manipulation Lanauage)
- insert
```sql
INSERT INTO tableName
(columm1, columm2, ...) -- 단, 모든 컬럼일 경우 생략할 수 있다.
VALUES(value1, value2, ...);

INSERT INTO table2
SELECT * FROM table1
WHERE condition;

INSERT INTO table2 (columm1, columm2, ...)
SELECT columm1, columm2, ... FROM table1
WHERE condition;
```


3. 참고
- 실습 테이블
    ```sql
    create table Customer(
        customerId int primary key,
        customerName varchar(50) not null,
        customerAddress varchar(200),
        customerSex bit,
        customerAge tinyint
    );
    ```
