---
layout: post
title: No route to any external sources dextected in Route Table for Subnet
subtitle: EMR 띄우는 과정 중 발생 에러
categories: AWS
tags: [Troubleshooting, AWS EMR, Network, route]
---

## Situation:
AWS EMR을 띄우는 도중 에러 코드 발생하여 네트워크 세팅 전반을 다시 살펴봄

## Error Code:
```
No route to any external sources detected in Route Table for Subnet
오류로 종료 상태 The VPC/subnet configuration was invalid: No route to any external sources detected in Route Table for Subnet: subnet-xxxxxxx for VPC: vpc-xxxxxxx
```

## Solution:
라우팅 테이블에 인터넷 게이트웨이 연결
라우팅 편집에서 대상을 인터넷 게이트웨이로 선택하여 ICDR 생성
