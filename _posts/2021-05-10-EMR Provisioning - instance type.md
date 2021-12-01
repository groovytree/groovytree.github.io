---
layout: post
title: EMR Provisioning - instance type
subtitle: c4.large type 서울 리전 지원
categories: AWS
tags: [AWS, EMR, Troubleshooting]
---

## Error Code:
```
The requested instance type c4.large is not supported in the requested availability zone. Learn more at https://docs.aws.amazon.com/console/elasticmapreduce/ERROR_noinstancetype
```

## Solution:
가용영역을 ap-northeast-2a 로 지정한 subnet 생성 후 재연결
