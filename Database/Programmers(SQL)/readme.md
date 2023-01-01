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

