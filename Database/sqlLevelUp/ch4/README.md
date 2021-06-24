# 4장.집약과 자르기

SQL의 특징적인 사고방식 중 하나는 레코드 단위가 아닌 레코드의 집합 단위로 처리하는 기술이다.

## 12강.집약(aggregate)

CASE 와 GROUP BY

```mssql
SELECT id,
	   MAX(CASE WHEN data_type = 'A' THEN data_1 ELSE NULL END) AS data_1,
	   MAX(CASE WHEN data_type = 'A' THEN data_2 ELSE NULL END) AS data_2,
	   MAX(CASE WHEN data_type = 'B' THEN data_3 ELSE NULL END) AS data_3,	   
	   MAX(CASE WHEN data_type = 'B' THEN data_4 ELSE NULL END) AS data_4,
	   MAX(CASE WHEN data_type = 'B' THEN data_5 ELSE NULL END) AS data_5,
	   MAX(CASE WHEN data_type = 'C' THEN data_6 ELSE NULL END) AS data_6
  FROM NonAggTbl
 GROUP BY id;
 //GROUP BY 구에 없는 필드는 MAX() 절등 집약함수를 사용하여 집약!
```

### 집약,해시,정렬

GROUP BY 시 해시 알고리즘이 사용됨(SORT도 있지만 요즘은 해시)

#### 해시 알고리즘

 GROUP BY 구에 지정되어 있는 필드를 해시 함수를 사용해서 해시키로 변환하고, 같은 해시 키를 가진 그룹을 모아 집약하는 방법

### 합쳐서 하나

PriceByAge(연령별 가격) 테이블

| reserve_id(예약 ID) | low_age(대상 연령의 하한) | high_age(대상 연령의 상항) | price(가격) |
| ------------------- | ------------------------- | -------------------------- | ----------- |
| 제품1               | 0                         | 50                         | 2000        |
| 제품1               | 51                        | 100                        | 3000        |
| 제품2               | 0                         | 100                        | 4200        |
| 제품3               | 0                         | 20                         | 500         |
| 제품3               | 31                        | 70                         | 800         |
| 제품3               | 71                        | 100                        | 1000        |
| 제품4               | 0                         | 99                         | 8900        |

질문: 각 제품별로 0~100세까지 모든 연령을 커버하지 제대로 커버하고 있는 제품이 찾는 쿼리를 작성하라

```mssql
SELECT product_id
  FROM PriceByAge
 GROUP BY product_id
 HAVING SUM(high_age - low_age + 1) = 101;
```

> 제품3를 예로 들면
>
> (20 - 0 + 1) +(70-31 + 1) + (100-71 + 1)  = 21 + 40 + 30 = 91 이므로 HAVING 구의 식이 참이 아니다
>
> 따라서 제품 3은 위의 SELECT문에서 제외됨

## 13장.자르기

GROUP BY 는 집약뿐만 아니라 **자르기**라는 기능도 있다.

모집합인 테이블을 작은 부분집합들로 자르는 것을 말함

```mssql
SELECT CASE WHEN age < 20 THEN '어린이'
			WHEN age BETWEEN 20 AND 69 THEN '성인'
			WHEN age >= 70 THEN '노인'
			ELSE NULL END AS age_class,
	   count(*)
  FROM Persons
 GROUP BY CASE WHEN age < 20 THEN '어린이'
			WHEN age BETWEEN 20 AND 69 THEN '성인'
			WHEN age >= 70 THEN '노인'
			ELSE NULL END AS age_class
```

위의 코드를 보면 자르기의 기준이 되는 키를 CASE 식으로 작성할 수도 있다

### PARTITION BY 구를 사용한 자르기

📌GROUP BY 구에서 집약 기능을 제외하고 자르는 기능만 남긴 것이 윈도우 함수 PARTITION BY 구 이다

즉, 원본테이블의 레코드를 그대로 유지한다

```mssql
SELECT name,
       age,
	   CASE WHEN age < 20 THEN '어린이'
			WHEN age BETWEEN 20 AND 69 THEN '성인'
			WHEN age >= 70 THEN '노인'
			ELSE NULL END AS age_class,
	   RANK() OVER(PARTITION BY CASE WHEN age < 20 THEN '어린이'
									 WHEN age BETWEEN 20 AND 69 THEN '성인'
								     WHEN age >= 70 THEN '노인'
			                         ELSE NULL END
				   ORDER BY age) AS age_rank_in_class
  FROM Persons
 ORDER BY age_class,age_rank_in_class
```

실행 결과

![](D:\GitRepository\TIL\Database\sqlLevelUp\ch4\image\result1.png)

전체 레코드수가 5개로 GROUP BY CASE 식을 했다면 3행의 레코드가 표시됐을 것이다.

PARTIOTION BY 구는 집약을 하지 않으므로 레드코갯수대로 5개가 표시되고 단지, 각 레코드의 RANK()만 보여주고 있음

