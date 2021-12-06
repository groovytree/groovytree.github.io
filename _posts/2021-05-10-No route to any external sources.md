---
layout: post
title: Routing setting for EMR
subtitle: EMR 띄우는 과정 중 발생 에러
categories: AWS
tags: [AWS, EMR, Troubleshooting]
---

## Error Code:
```
No route to any external sources detected in Route Table for Subnet
오류로 종료 상태 The VPC/subnet configuration was invalid: No route to any external sources detected in Route Table for Subnet: subnet-xxxxxxx for VPC: vpc-xxxxxxx
```

## Solution:
라우팅 테이블에 인터넷 게이트웨이 연결
라우팅 편집에서 대상을 인터넷 게이트웨이로 선택하여 ICDR 생성
