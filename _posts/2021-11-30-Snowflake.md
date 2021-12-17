---
layout: post
title: Database - Snowflake
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
- Virtual Warehouse - compute only layer
	- Database Layer (using DDL), dml?
	- 테이블 데이터를 로딩하는 것, 데이터베이스 생성, 스키마 생성, 테이블 생성 등의 작업이 S3 에 저장된 데이터를 기반으로 하고, snowflake는 computing layer 와 storage layer (S3) 가 완벽하게 구분되어 있기 때문에 위의 작업 중에는 compute cost 가 들지 않는다. (비용, 시간, 성능)
	- |end user ->|Amazon EC2 / Pay per use for Compute ->|Aamzon S3 / Pay per use for Storage|
	- |Virtual Machine -> Virtual Warehouse| 완전한 클라우드 기반의 virtual warehouse (VW) 명명. 
	- VW의 다양한 사이즈와 노드개수
	- VW 러닝 중에만 compute cost 할당
	- VW 의 concurrency scale up/down 

## 비용
- architecture 에서 compute, storage 양에 따른 비용이 대부분이다.


## 참고
![](//www.youtube.com/watch?v=dxrEHqMFUWI)


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