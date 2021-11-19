---
layout: post
title: Database - Snowflake vs Redshift
subtitle: Difference on Cloud Computing
categories: DB, AWS, Snowflake, Redshift
tags: [AWS, DB, Snowflake, Redshift, Docs]
---

1. 데이터베이스 성능 비교의 중점은

2. Computing, Storage, 기능, 가격

json 데이터를 다루는 측면에서의 비교
동시확장성 기능(Concurrency scaling)에 대하여 


두 개의 데이터베이스 모두 MPP(Massively Parellel Processing), 대규모 병렬처리가 가능한 비공유 아키텍처(Shared Nothing) 이며, 이에 대한 장/단점을 그대로 가지고 있다. 
- 성능과 확장성 
- 메모리와 운영체제를 공유하지 않기 때문에 데이터 병목현상이 없고 노드를 추가하기 쉽다

External Table 로딩 기술 (대용량 데이터 로딩 기술) 