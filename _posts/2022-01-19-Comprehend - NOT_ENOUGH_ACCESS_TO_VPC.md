---
layout: post
title: AWS Comprehend - NOT_ENOUGH_ACCESS_TO_VPC
subtitle: 에러 해결방법
categories: AWS
tags: [Troubleshooting, AWS Comprehend]
---

![Foo](/assets/images/posts/2022-01-19/1.png)

## Error
```bash
NOT_ENOUGH_ACCESS_TO_VPC: The provided data access role does not have ec2:DescribeSecurityGroups permission.
```

## Solution
```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "ec2:DescribeInstances",
                "ec2:DescribeImages",
                "ec2:DescribeKeyPairs",
                "ec2:DescribeVpcs",
                "ec2:DescribeSubnets",
                "ec2:DescribeSecurityGroups"
            ],
            "Resource": "*"
        }
    ]
}
```

위 policy를 comprehend job을 수행하는 role 의 정책으로 추가한다
ec2: DescribeInstances, ... 외 몇 가지 정책은 추가하지 않으면 같은 에러로 다시 발생한다.


정책 수정 후에도 ec2:DescribeSubnets 에러가 계속 발생할 경우 선택 VPC 내 subnet-a, b, c 를 모두 포함한다.
