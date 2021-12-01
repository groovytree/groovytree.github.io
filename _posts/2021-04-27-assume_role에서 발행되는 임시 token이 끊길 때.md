---
layout: post
title: assume_role 에서 발행되는 임시 token이 끊길 때
subtitle: The provided token has expired
categories: Amazon Web Services
tags: [AWS, SDK, Role Switching, boto3, Troubleshooting]
---

## Error Code:
```
raise error_class(parsed_response, operation_name)
botocore.exceptions.ClientError: An error occurred (ExpiredToken) when calling the ListObjects operation: The provided token has expired.
```

## Situation:
역할전환을 위해 사용한 assume_role 은 계정에 1시간에 해당하는 temporary token을 발급한다. 때문에 1시간이 넘는 시간 동안 boto3로 연결하여 스크립트가 실행될 경우, 에러가 발생한다.

## Reference:
https://stackoverflow.com/questions/35685729/the-security-token-included-in-the-request-is-expired

## Solutions:
https://medium.com/@li.chastina/auto-refresh-aws-tokens-using-iam-role-and-boto3-afd3c52fd8c7
https://feeney.mba/refreshable-aws-boto-credentials.html
