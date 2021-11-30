---
layout: post
title: MySQL - Communication Link Failure
subtitle: MySQL 서버 통신 오류 에러
categories: MySQL
tags: [DB, MySQL, Error, Troubleshooting]
---

## Error Code:
```
Connection timed out connect:
Communications link failure
The last packet sent successfully to the server was 0 milliseconds ago. The driver has not received any packets from the server.
	Connection timed out: connect
```

## Solution:
1. 연결하려는 서버 정보가 올바르게 기재되어있는지 다시 확인. db endpoint, pot, user, pw, connection driver settings ..
2. 연결 서버에 ping 으로 확인한다
3. Driver properties 설정 변경
- serverTimezone -> UTC 
- autoReconnect=true
- tcpKeepalive=true
4. meta temp값을 날리고 재접속
- C:Users > username > AppData > Roaming > DBeaverData > workspace6 > .metadata metadata 폴더를 백업한 후, 본 위치에서 날리고 dbeaver에 재접속한다.
5. MySQL 서버가 설치되어있는 경우, 서버 설정값을 변경한다
- C:ProgramData > MySQL > MySQL Server x.0 > my.ini 설정 파일 
- mawait_timeout, interactive_timeout 값을 초 단위로 8시간 이상으로 설정. 설정 시간 동안 연결을 유지함

순서대로 해볼 수 있는 경우의 수를 작성하였다. mysql 서버, connector 재설치 다 해보았지만 결국 서버 정보를 잘못 입력 ㅋㅋ 삽질의 기록..