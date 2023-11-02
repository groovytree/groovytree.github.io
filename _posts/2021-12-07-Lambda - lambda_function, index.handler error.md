---
layout: post
title: Lambda - lambda_function, index.handler error
subtitle: Lambda 삽질의 기록
categories: AWS
tags: [Troubleshooting, AWS Lambda]
---

## Error Code

```
**Unable to import module 'lambda_function': No module names lambda_function**
```

```
Runtime.HandlerNotFound: idnex.handler is undefined or not exported
```

## Solutions

1. Lambda Runtime settings
2. Handler 를 Edit 
3. fileName.handlerName 으로 수정한다