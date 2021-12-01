---
layout: post
title: MySQL - Connect to Custom Driver
subtitle: Custom Driver 셋팅하여 인터넷 불가 환경에서 DB 접속하기
categories: DB
tags: [DB, MySQL, Docs]
---

## Situation:
- 서버 접속시 필요한 드라이버 환경을 인터넷으로 자동 다운로드하여 접속하게 되는 경우가 많다. 인터넷이 안 되는 환경일 때, jar 파일을 이용해서 손수 드라이버 셋팅을 한다.
- 환경: MySQL Server 8.0
- JAR File: mysql-connector-java-8.0.17.jar, protobuf-java-3.6.1.jar

## Solution:
1. 드라이버 필요파일을 C:Users > Username > AppData > Roaming > DBeaverData > drivers > maven > maven-central > mysql > version 폴더 내 위치로 붙여넣는다.
2. dbeaver 에서 데이터베이스 > 드라이버 관리자 를 선택
3. MySQL 데이터베이스를 선택, New 로 Custom 드라이버를 생성한다. driver name, class name, url template 등은 기존 MySQL 설정과 동일하게 해주고 나머지는 연결하고자 하는 DB 세팅으로 확인한다.
4. 새 데이터베이스 연결에서 방금 생성한 custom driver 를 연결한다. 