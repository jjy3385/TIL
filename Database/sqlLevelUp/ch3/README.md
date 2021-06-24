# 3장.SQL의 조건분기

## 8강. UNION을 사용한 쓸데없이 긴 표현

UNION을 사용한 조건 분기

```mssql
SELECT item_name,year,price_tax_ex as price
  FROM Items	
 WHERE year <= 2001
 UNION ALL
SELECT item_name,year,price_tax_in as price
  FROM Items	
 WHERE year >= 2002 
```

쓸데없이 테이블에 2회 접근하며 그만큼 I/O 비용이 증가한다

아래와 같이 수정하면 TABLE ACESS FULL 을 1회로 줄일 수 있다.

```mssql
SELECT item_name,year,
	   CASE WHEN year <= 2001 THEN Price_tax_ex
	        WHEN year >= 2002 THEN price_tax_in END AS price
  FROM Items;
```

## 10강. 그래도 UNION이 필요한 경우

1. SELECT 구문에 사용하는 테이블이 다른 경우엔 UNION 을 사용할 수 밖에 없음

2. 인덱스 관련해서 UNION 사용하는 것이 성능이 더 좋은 경우가 있음

그래도 몇 가지 경우를 제외하곤 UNION을 사용하지 않는 것이 성능이나 가독성 면에서 더 좋다

SQL의 성능은 저장소의 I/O 를 얼마나 감소시키는지가 가장 중요하다



