---
layout: post
title: Datawarehouse - Snowflake
subtitle: Snowflake key capabilities
categories: DB
tags: [DB, Snowflake, Docs]
---

## Key capabilities
1. 전통DB에서 처리하는 Relational DB, 관계형DB가 아니다.
2. PK/FK (Primary Key/Foreign Key) 제약이 없습니다.
2. No indexing / No performance tuninig / no partitioning / no physical storage design

## Architecture
- Cloud service layer
	- 메타데이터를 관리, 자동성능최적화, 보안, 트랜잭션관리, 동시확장성 관리
	- query 의 que 부하에 따라 scale up/down 을 결정한다
	- snowflake 의 brain 영역이다
	- Database, schema, table, view 등의 logical model 개념이 사용된다
	- Data processing 에 있어서 sql database 모델에 적용되었던 익숙한 것들이 그대로 사용된다 
- Virtual Warehouse - compute only layer
	- Database Layer (using DDL), dml?
	- 테이블 데이터를 로딩하는 것, 데이터베이스 생성, 스키마 생성, 테이블 생성 등의 작업이 S3 에 저장된 데이터를 기반으로 하고, snowflake는 computing layer 와 storage layer (S3) 가 완벽하게 구분되어 있기 때문에 위의 작업 중에는 compute cost 가 들지 않는다. (비용, 시간, 성능)
	- |end user ->|Amazon EC2 / Pay per use for Compute ->|Aamzon S3 / Pay per use for Storage|
	- |Virtual Machine -> Virtual Warehouse| 완전한 클라우드 기반의 virtual warehouse (VW) 명명. 
	- VW의 다양한 사이즈와 노드개수
	- VW 러닝 중에만 compute cost 할당
	- VW 의 concurrency scale up/down 
	- 데이터 로드/ 사용/ BI/ 시각화 툴 모두 각각의 WL를 가지고 VW를 따로 띄워서 작업하므로 I/O Competency가 거의 없다고 봐도 무방.
- Storage layer
	- 블럭 스토리지로서, 확장성이 높다
	- 데이터 로드시에 자동으로 암호화, 메타데이터 관리를 진행한다(micro-partitioning)

## 데이터 로드
1. 데이터를 클라우드에 스테이징한다
- 데이터를 클라우드 스토리지의 여러 개 버킷에 나누어 넣는다
2. 데이터를 로드할 SQL 명령어를 실행하여 로드한다
- 이 과정에 ETL/ELT 툴을 사용(alteryx, BimlFlex, ATTUNITY, WhereScape, MATILLION, Fivetran, talend, informatica)
3. 실시간 데이터 수집기 연결 기능도 제공한다, snowpipe
- Spark streaming, kafka, amazon Kinesis 

## 데이터 사용
- BI/ 시각화 툴 사용
- ODBC/JDBC 를 사용하여 연결 
- MicroStrategy, looker, tableau
- Spark, R, Python .. 
- 데이터 연동 및 사용에 대하여 challenge 가 있을 수 있다

## 비용
- architecture 에서 compute, storage 양에 따른 비용이 대부분이다.
- VW를 실시간/ 동적으로 활용할 수 있으며, WL 때문에 Scale의 사이즈를 조정하여 VW을 조정할 때에도 워크로드를 중지하거나 사용자를 차단하는 일이 없다. VW를 8배로 늘리게 되었을 때, 1대로 처리해야 하는 시간이 8배로 단축되고, 또 이에 대한 사용료도 1대로 처리할 때와 8대로 8배 빠른 속도로 처리될 때의 비용이 동일하다. (computing 과 storage 가 완벽하게 분리되어서 가능함)

## 반정형 데이터 처리
- variant data type으로 반정형 데이터 핸들링

## 처리 속도
- xlarge computing type으로 1억1천건 정도의 데이터 핸들링이 52초 정도 소요

## 그 외
- Data Protection, replication & time travel (43:22)
- zero copy cloning (DevOps)
	- production 환경의 변화없이 개발환경을 쉽게 복제하여 연결/ 사용할 수 있음
	- create or replace database dev clone prd; (-- make a copy of our current state PRD database to use as DEV). 추가 스토리지/ 비용이 들지 않음. meta data에서 실행하기 때문에 속도도 빠름
	- 개발환경을 다 이용한 후 production화 할 수 있음
- data sharing
	- 데이터 추출, 이동 없이 당사자에게 권한을 부여하고 실시간 액세스 권한을 관리할 수 있음
	- 데이터 제공자가 변경하면 실시간으로 양수인에게 공유됨

## 웨비나 
### 데이터 로드 
- 데이터가 Azure 에 있어도 snowflake AWS 에서도 연결해서 데이터를 적재할 수 있음. 
- @ 외부버킷 로케이터 

### 데이터 로딩
- copy into 명령어 사용. 대량 데이터 로딩시 배치성 데이터, 벌크 로딩. 실시간, 스트리밍이라면 snow파일 사용. 24시간~~ .. 23:35 
- 컴퓨팅 파워 필요. 멀티클러스터 컴퓨팅 영역. 버츄어 웨어하우스. EC2 영역. 

### 웨어하우스
- warehouse 설명 25:12 minimum 60초 40초 사용시 60초 과금. Maximum clusters 최소/최대 지정.
- scaling policy. 어느 순간 복제하느냐. 
	- 큐잉 걸리는 걸 감지했을 때, 바로바로 한다: standard, 
	- economy는 6분 기다림. 일시성 부하를 기다림. 스파이크. 잠시 기다려보는 세팅.
	- auto suspend 잠드는 기능. 5분.(300 밀리세컨드) 
	- auto resume 체크. 알아서 일어나는 기능. 
- 하나의 노드는 8개의 virtual cpu로 구성. 4-xl 는 노드 128개도 가능. 클러스터 동시성 기능 때문에 *10 하여 1280개까지 가능. 슈퍼 컴퓨터급.
- 오토리쥼, 오토서스펜드 잘 사용할 것! 월요일 리포트 부하 많을 때 예제 기억할 것

### 웨어하우스 생성  분석용
- 컴퓨트 웨어하우스 경합이 필요 없음 

### 캐싱
- 24시간 보유, 30일 지속

### 클론 
- 데이터 자체가 아니라 논리적 복제

### 반정형 
- 완전비정형 데이터(오디오 등)도 핸들링. 메타데이터를 저장, 메타데이터에 링크걸 수 있음. 예로 이미지파일이 있고 image recognition 을 분석 가능. 외부 function , recognition 펑션을 외부에서 불러서 내부 데이터를 대상으로 쿼리할 수 있음 
- variant: 반정형 데이터 적재

### 히스토리
- 마켓, 게임 산업에서 스노우플레이크 도입 빠르게 됨. 그게 반정형 데이터에 대한 장점 때문. 2015년 출시시. 웹 로그, 클릭 스트림 등의 데이터 핸들링 굿. 
- dot notation: , :: : casting, []: array

## 타임트래블
- change data capture

## 9.RBAC 
- accountadmin: 사용료 볼 수 있음 
- 워크쉬트의 컨택스트 실행 관리와 로그인된 관리가 별개임

## 10.마켓플레이스
- 데이터 모니타이제이션
- 외부 데이터를 가져오고 스토리지에 저장해서 변환하고 조인하는 게 아니라, 마켓에서 쿼리당 데이터 소비비용으로 가는 추세. 
- 관리/업데이트할 필요 없이 바로 가져와서 사용만 하는 추세

### 데이터 1:1 공유 
아웃바운드: 내가 데이터 외부로 공유 
doemzjstbaj: snrndhk rhddb
애드 컨슈머: 누구와 공유할지 
실시간으로 공유하게 됨.

### 마켓플레이스
- 어카운트 어드민 선택 

## 궁금사항
1. zero copy cloning, 메타데이터를 복제하여 사용하는 방식일 때, VW의 computing 에 영향(속도/ 비용)이 드는지?
1-1. 메타데이터를 사용하는 cloud service layer 의 사용시, compute/ storage cost 가 전혀 안 드는지?
1-2. zero copy cloning 에서 변경사항이 생길 경우 메타데이터에서 이 변화도 감지하여 관리하는지?
1-3. zero copy cloning 을 사용할 수 있는 사용자/ 용량 제한은?
1-4. prd 환경의 일부만 복제하는 것도 가능한지?


## 참고
![](//www.youtube.com/watch?v=dxrEHqMFUWI)
https://resources.snowflake.com
