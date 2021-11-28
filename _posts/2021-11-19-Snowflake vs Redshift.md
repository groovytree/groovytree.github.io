---
layout: post
title: Database - Snowflake vs Redshift
subtitle: Difference on Cloud Computing
categories: Redshift
tags: [AWS, DB, Snowflake, Redshift, Docs]
---

1. 데이터베이스 성능 비교의 중점은

2. Computing, Storage, 기능, 가격

3. json 데이터를 다루는 측면에서의 비교
반구조화 데이터(semi-structured data); 
- 중첩된 데이터 구조와 고정된 스키마가 없다는 점이 특징
- 같은 클래스 내의 엔터티는 함께 그룹화되어도 속성이 다를 수 있으며, 속성의 순서도 중요하지 않다
- flat 테이블, 스프레드시트 등의 구현이 가능한 구조화 데이터와 달리 반구조화 데이터는 중첩된 정보를 n 수준의 계층으로 다양하게 표현될 수 있다
* snowflake 에서 지원되는 반구조 데이터
- json, avro, ORC, Parquet, XML
* redshift 에서 지원되는 반구조 데이터 
SUPER 데이터 유형;
스키마 없는 데이터를 배열/구조를 저장할 수 있는 Redshift 만의 데이터 유형


3. 공통점
두 개의 데이터베이스 모두 MPP(Massively Parellel Processing), 대규모 병렬처리가 가능한 비공유 아키텍처(Shared Nothing) 이며, 이에 대한 장/단점을 그대로 가지고 있다. 
- 성능과 확장성: RDB로서 ACID를 보장하며 노드를 선형적으로 확장할 수 있음
- 메모리와 운영체제를 공유하지 않기 때문에 데이터 병목현상이 없고 노드를 추가하기 쉽다
- 각 노드에 데이터가 분할되어 관리되기 때문에 읽기/쓰기에 대한 처리 시 경합이 줄어든다
- 모든 노드에서 쓰기가 가능하여 전통 RDB에서 지니던 쓰기 확장성이 가능하다 -> Scale Out

External Table 로딩 기술 (대용량 데이터 로딩 기술) 

4. Redshift 는 OLAP 전용으로 설계되었으나, computing engine 이 OLTP (Postgres) 
- OLTP는 전통적으로 행 기반으로 데이터를 저장.
- redshift는 최적 메모리 사용 및 디스크 I/O를 위한 특수 데이터 압축 인코딩을 사용하여 데이터를 열에 저장. 보조 인덱스, 단일 행 데이터 조작 작업 등의 OLTP 기능상의 이점은 redshift 에서는 생략되었음

* Scale Up/Down: 더 높은 성능의 장비로 교체하는 것. 관리/운영 비용은 큰 차이가 없음. 한 대 서버의 집중도가 높아 장애 시 처리가 어려울 수 있음.
* Scale Out/In: 장비를 여러 대 추가하여 나눠서 일할 수 있도록 수평 확장. 지속적 확장함. 대수가 늘어날수록 운영 비용이 증가한다. 읽기/쓰기가 여러 대 서버에 분산되어 장애 처리가 용이할 수 있다.

Reference:
https://docs.aws.amazon.com/ko_kr/redshift/latest/dg/c_redshift-and-postgres-sql.html