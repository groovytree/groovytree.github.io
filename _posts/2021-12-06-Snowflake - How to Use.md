---
layout: post
title: Snowflake - How to Use
subtitle: Snowflake key capabilities
categories: DB
tags: [DB, Snowflake, Docs]
---

## Create Warehouse
- Auto Suspend: 아무 activity가 없을 경우 해당 초/ 분 기다린 후, 자동으로 suspend 되어 비용 청구가 되지 않음
- Auto Resume: check. suspend가 되어 있어도 다음 쿼리가 들어오면 자동 resume 되는 기능. 

## Data handling
- 외부 버킷에 데이터가 스테이징 되어 있고, create table 을 통해서 데이터를 DB 에 저장한다. 이후 copy 명령문으로 데이터를 로드하여 사용함

## 명령문
### Zero copy cloning
- 생성
```sql
-- make a copy of our current state PRD db to use as DEV 
create or replace database dev clone prd;
-- also make a DEV warehouse so our DEV queries are isolated from PRD
create warehouse if not exists dev_wh warehouse_size = 'medium' auto_suspend = 300 initially_suspended=true;
```

- 삭제
```sql
drop database dev;
drop warehouse dev_wh;
use schemas prd;
use warehouse load_wh;
```

### 데이터 로드
- 외부 S3 스테이징 데이터 리스트 조회
```sql
list @citibike.public.weather/;
```

- 반정형 데이터 조회
```sql
select $1 from @citibike.public.weather/2019/ limit 20;
```

## 참고
https://resources.snowflake.com/
