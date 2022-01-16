---
title:  "[SQL] UNION과 JOIN"
excerpt: "union과 join"

categories:
  - SQL
tags:
  - [sql]

toc: true
toc_sticky: true

date: 2022-01-16
last_modified_at: 2022-01-16
layout: single
---

### UNION, UNION ALL
- 여러 개의 SQL문을 합쳐 하나의 SQL문으로 만들어 준다.
- UNION : 각 쿼리의 결과를 반환하는 합집합 (중복제거)
- UNION ALL : 각 쿼리의 모든 결과를 포함한 합집합 (중복 제거 안함)
```SQL

SELECT 'S'         AS SAL_TYPE,
				A.JOB      AS JOB,
				SUM(A.SAL) AS TOTAL_SAL
FROM EMP1 A
GROUP BY A.JOB

UNION ALL

SELECT 'C'          AS SAL_TYPE,
				A.JOB       AS JOB,
				SUM(A.COMM) AS TOTAL_COMM
FROM EMP A
GROUP BY A.JOB

ORDER BY JOB, SAL_TYPE DESC

```
- 사용 시 주의사항
  * 각 쿼리의 컬럼의 개수와 데이터 타입이 일치해야 한다.
  * 첫 번째 쿼리의 컬럼 별칭으로 결과가 반환되므로 두 번째 쿼리부터는 별칭을 생략할 수 있다.
    + 위의 쿼리문의 경우 세번째 컬럼명은 'TOTAL_SAL'로만 나온다.
  * ORDER BY 는 마지막에 한번만 사용할 수 있으며, 합쳐진 모든 결과를 정렬한다.
  * 중복 제거가 필요한 상황이 아니라면 UNION ALL 사용 권장.

### UNION과 JOIN
- JOIN : 새로운 열로 결합(수평결합)


![image](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/3ad73b52-7ea7-4b0c-bd27-60a46f6f0412/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220113%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220113T034822Z&X-Amz-Expires=86400&X-Amz-Signature=146a26f83ceaab811a312cf37a67cbb686274df0d77b51847d63543d50af57fe&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22&x-id=GetObject)

- UNION : 새로운 행으로 결합 (수직결합)


![image](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/ef41d8d6-d350-4efe-b8ff-3d62d674150f/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220113%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220113T034922Z&X-Amz-Expires=86400&X-Amz-Signature=beeab442a5c0515442b38369de35a7e2d2de243904b4ab28f7153e3100d03f49&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22&x-id=GetObject)
