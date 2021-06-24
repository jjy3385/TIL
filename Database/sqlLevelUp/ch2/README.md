# 2장.SQL 기초

## 6강. SELECT구문

### GROUP BY 구

자르기와 집약이라는 두 개의 기능으로 분리할 수 있음

테이블의 데이터를 나누고 집계 함수로 집계하는 연산을 할 수 있음

### HAVING 구

GROUP BY 결과 집합에 대한 조건을 걸어 선택하는 기능을 하는 구문

## 7강.조건 분기,집합 연산,윈도우 함수,갱신

### 1.조건분기 : CASE식

조건에 따라 결과를 분기하는 구문으로 식이기 때문에 SELECT,WHERE,GROUP BY,HAVING,ORDER BY 구 어디든 적을 수 있음

```mssql
CASE WHEN [평가식] THEN [식]
	 WHEN [평가식] THEN [식]
	 ELSE [식]
 END 
```

### 2.SQL 집합 연산

합집합 : UNION

교집합 : INTERSECT

차집합 : EXCEPT

### 3.윈도우 함수

GROUP BY 처럼 데이터를 자르긴 하지만 집약하지 않음 따라서 출력 결과가의 레코드 수가 입력되는 테이블의 레코드 수와 같음(PARTITION BY)

```mssql
SELECT address,
       COUNT(*) OVER(PARTITION BY address)
  FROM Address;
-- Address 테이블에 입력된 데이터 수만큼 결과가 출력됨
```











