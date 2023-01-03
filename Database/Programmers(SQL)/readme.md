# Programmers SQL

1. LV 1
- 조건에 맞는 도서 리스트 출력하기
    ```sql
    SELECT BOOK_ID, DATE_FORMAT(PUBLISHED_DATE, '%Y-%m-%d') as PUBLISHED_DATE
    FROM BOOK
    WHERE PUBLISHED_DATE like '%2021%' and CATEGORY = '인문'
    ORDER BY PUBLISHED_DATE ASC
    ```

- 재구매가 일어난 상품과 회원 리스트 구하기
    ```sql
    SELECT USER_ID, PRODUCT_ID
    FROM ONLINE_SALE
    GROUP BY USER_ID, PRODUCT_ID
    HAVING COUNT(*) > 1
    ORDER BY USER_ID ASC, PRODUCT_ID DESC
    ```

- 오프라인/온라인 판매 데이터 통합하기
    ```sql
    SELECT DATE_FORMAT(SALES_DATE, "%Y-%m-%d") AS SALES_DATE, PRODUCT_ID, IFNULL(USER_ID, NULL) AS USER_ID, SALES_AMOUNT
    FROM (
        SELECT SALES_DATE, PRODUCT_ID, USER_ID, SALES_AMOUNT
        FROM ONLINE_SALE
        UNION
        SELECT SALES_DATE, PRODUCT_ID, NULL, SALES_AMOUNT
        FROM OFFLINE_SALE
        ) A
    WHERE SALES_DATE like "2022-03%"
    ORDER BY SALES_DATE ASC, PRODUCT_ID ASC, USER_ID ASC
    ```

- 동물 관련문제 통합
    ```sql
    -- 아픈 동물 찾기
    SELECT ANIMAL_ID, NAME
    FROM ANIMAL_INS
    WHERE INTAKE_CONDITION like "Sick"
    -- WHERE INTAKE_CONDITION = 'Sick'

    -- 어린 동물 찾기
    SELECT ANIMAL_ID, NAME
    FROM ANIMAL_INS
    WHERE INTAKE_CONDITION != 'Aged'

    -- 동물의 아이디와 이름
    SELECT ANIMAL_ID, NAME
    FROM ANIMAL_INS
    ORDER BY ANIMAL_ID

    -- 여러 기준으로 정렬하기
    SELECT ANIMAL_ID, NAME, DATETIME
    FROM ANIMAL_INS
    ORDER BY NAME ASC, DATETIME DESC

    -- 상위 n개 레코드
    SELECT NAME
    FROM ANIMAL_INS
    ORDER BY DATETIME ASC LIMIT 1

    -- 역순 정렬하기
    SELECT NAME, DATETIME
    FROM ANIMAL_INS
    ORDER BY ANIMAL_ID DESC

    -- 모든 레코드 조회하기
    SELECT *
    FROM ANIMAL_INS
    ORDER BY ANIMAL_ID
    ```

- 조건에 맞는 회원수 구하기
    ```sql
    SELECT COUNT(*) AS USERS
    FROM USER_INFO
    WHERE AGE between 20 AND 29
        and
        JOINED like "2021%"
    ```

- 가장 비싼 상품 구하기
    ```sql
    SELECT PRICE as MAX_PRICE
    FROM PRODUCT
    ORDER BY PRICE DESC LIMIT 1
    ```

- 과일로 만든 아이스크림 고르기
    ```sql
    SELECT a.FLAVOR
    FROM FIRST_HALF as a
        INNER JOIN ICECREAM_INFO as b
        ON a.FLAVOR = b.FLAVOR
    WHERE a.TOTAL_ORDER >= 3000 AND b.INGREDIENT_TYPE = 'fruit_based'
    ```

- 흉부외과 또는 일반외과 의사 목록 출력하기
    ```sql
    SELECT DR_NAME, DR_ID, MCDP_CD, DATE_FORMAT(HIRE_YMD, '%Y-%m-%d') as HIRE_YMD
    FROM DOCTOR
    WHERE MCDP_CD = 'CS' OR MCDP_CD = 'GS'
    ORDER BY HIRE_YMD DESC, DR_NAME ASC
    ```

- 3월에 태어난 여성 회원 목록 출력하기
    ```sql
    SELECT MEMBER_ID, MEMBER_NAME, GENDER, DATE_FORMAT(DATE_OF_BIRTH, '%Y-%m-%d') as DATE_OF_BIRTH
    FROM MEMBER_PROFILE
    WHERE TLNO IS NOT NULL AND DATE_OF_BIRTH like '%-03-%' AND GENDER = 'W'
    ORDER BY MEMBER_ID
    ```