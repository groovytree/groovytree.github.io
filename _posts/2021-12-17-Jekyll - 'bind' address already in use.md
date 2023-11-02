---
layout: post
title: Jekyll Blog - 'bind' address already in use eaddrinuse
subtitle: 깃허브 블로그 서버구동시 에러
categories: Web
tags: [Troubleshooting, Jekyll]
---

## Error
```bash
'bind' address already in use eaddrinuse 
```
블로그 서버를 로컬로 실행하고 Ctrl + C 로 정상종료되지 않았을 때, 서버를 재실행하면 위 에러가 발생한다.

## Solution
```bash
lsof -i TCP:4000
```
해당 포트로 연결되어 있는 프로세스를 리스트화하여 
ruby 로 실행되고 있고, 확실하게 종료되지 않은 프로세스를 제대로 종료한다.

```bash
kill -9 (PID)
```

재실행하면 서버가 잘 구동된다
```bash
bundle exec jekyll serve --trace
```


## 4. Error

```bash
>> bundle exec jekyll serve --trace
bundler: command not found: jekyll
Install missing gem executables with `bundle install`
```

## Solutions


