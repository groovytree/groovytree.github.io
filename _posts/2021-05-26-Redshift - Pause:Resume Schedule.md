---
layout: post
title: Redshift - Pause/Resume Schedule
subtitle: Crontab으로 스케줄 조정하기 
categories: AWS
tags: [Docs, AWS Redshift]
---

## Situation:
클러스터 운영 시간에 따라 자동 시작/중지 시간을 설정하고자 한다.
Stop: 20시
Start: 6시 30분

## Solution:
redshift-pause: 0 19 ? * MON-FRI *
redshift-resume: 30 21 ? * MON-FRI *

Cron식으로 KST 에서 -9 하여 UTC 로 표현.