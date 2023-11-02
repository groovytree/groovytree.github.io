---
layout: post
title: AWS EMR - Provisioning
subtitle: availability zone 
categories: AWS
tags: [Troubleshooting, AWS EMR, region, c4.large]
---

## Error Code:
```
The requested instance type c4.large is not supported in the requested availability zone. Learn more at https://docs.aws.amazon.com/console/elasticmapreduce/ERROR_noinstancetype
```

## Solution:
가용영역을 ap-northeast-2a 로 지정한 subnet 생성 후 재연결 성공함
