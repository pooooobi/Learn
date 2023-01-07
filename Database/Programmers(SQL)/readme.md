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

    -- NULL 처리하기
    SELECT ANIMAL_TYPE, IFNULL(NAME, 'No name') as NAME, SEX_UPON_INTAKE
    FROM ANIMAL_INS

    -- 이름이 있는 동물의 아이디
    SELECT ANIMAL_ID
    FROM ANIMAL_INS
    WHERE NAME IS NOT NULL
    ORDER BY ANIMAL_ID ASC

    -- 이름이 없는 동물의 아이디
    SELECT ANIMAL_ID
    FROM ANIMAL_INS
    WHERE NAME IS NULL
    ORDER BY ANIMAL_ID ASC

    -- 최댓값 구하기
    SELECT MAX(DATETIME)
    FROM ANIMAL_INS

    -- 최솟값 구하기
    SELECT MIN(DATETIME)
    FROM ANIMAL_INS

    -- 동물 수 구하기
    SELECT COUNT(*)
    FROM ANIMAL_INS
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

- 경기도에 위치한 식품창고 목록 출력하기
    ```sql
    SELECT WAREHOUSE_ID, WAREHOUSE_NAME, ADDRESS, IFNULL(FREEZER_YN, 'N') as FREEZER_YN
    FROM FOOD_WAREHOUSE
    WHERE ADDRESS like '경기도%'
    ORDER BY WAREHOUSE_ID ASC
    ```

- 나이 정보가 없는 회원 수 구하기
    ```sql
    SELECT COUNT(*) USERS
    FROM USER_INFO
    WHERE AGE IS NULL
    ```

- 12세 이하인 여자 환자 목록 출력하기
    ```sql
    SELECT PT_NAME, PT_NO, GEND_CD, AGE, IFNULL(TLNO, 'NONE') as TLNO
    FROM PATIENT
    WHERE AGE <= 12 AND GEND_CD = 'W'
    ORDER BY AGE DESC, PT_NAME ASC
    ```

- 서울에 위치한 식당 목록 출력하기
    ```sql
    SELECT a.REST_ID, a.REST_NAME, a.FOOD_TYPE, a.FAVORITES, a.ADDRESS, ROUND(AVG(b.REVIEW_SCORE), 2) as SCORE
    FROM REST_INFO a
        INNER JOIN REST_REVIEW as b
        ON a.REST_ID = b.REST_ID
    WHERE a.ADDRESS LIKE '서울%'
    GROUP BY a.REST_NAME
    ORDER BY SCORE DESC, a.FAVORITES DESC
    ```

- 강원도에 위치한 생산공장 목록 출력하기
    ```sql
    SELECT FACTORY_ID, FACTORY_NAME, ADDRESS
    FROM FOOD_FACTORY
    WHERE ADDRESS LIKE '강원도%'
    ORDER BY FACTORY_ID ASC
    ```

- 인기있는 아이스크림
    ```sql
    SELECT FLAVOR
    FROM FIRST_HALF
    ORDER BY TOTAL_ORDER DESC, SHIPMENT_ID ASC
    ```

- 가격이 제일 비싼 식품의 정보 출력하기
    ```sql
    SELECT *
    FROM FOOD_PRODUCT
    ORDER BY PRICE DESC LIMIT 1
    ```

- 중복 제거하기
    ```sql
    SELECT COUNT(DISTINCT(NAME))
    FROM ANIMAL_INS
    WHERE NAME IS NOT NULL
    ```

- 조건에 맞는 도서와 저자 리스트 출력하기
    ```sql
    SELECT a.BOOK_ID, b.AUTHOR_NAME, DATE_FORMAT(a.PUBLISHED_DATE, '%Y-%m-%d') as PUBLISHED_DATE
    FROM BOOK as a
        INNER JOIN AUTHOR as b
        ON a.AUTHOR_ID = b.AUTHOR_ID
    WHERE a.CATEGORY = '경제'
    ORDER BY PUBLISHED_DATE ASC
    ```

- 5월 식품들의 총매출 조회하기
    ```sql
    SELECT a.PRODUCT_ID, a.PRODUCT_NAME, (a.PRICE * SUM(b.AMOUNT)) as TOTAL_SALES
    FROM FOOD_PRODUCT as a
        INNER JOIN FOOD_ORDER as b
        ON a.PRODUCT_ID = b.PRODUCT_ID
    WHERE b.PRODUCE_DATE LIKE '%2022-05-%'
    GROUP BY PRODUCT_ID
    ORDER BY TOTAL_SALES DESC, PRODUCT_ID ASC
    ```

- 주문량이 많은 아이스크림들 조회하기
    ```sql
    SELECT a.FLAVOR
    FROM FIRST_HALF as a
        INNER JOIN JULY as b
        ON a.FLAVOR = b.FLAVOR
    GROUP BY a.FLAVOR
    ORDER BY (SUM(a.TOTAL_ORDER) + SUM(b.TOTAL_ORDER)) DESC LIMIT 3
    ```