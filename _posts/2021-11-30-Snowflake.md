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