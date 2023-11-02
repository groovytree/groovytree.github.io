---
layout: post
title: Python - HTTP
subtitle: Network and Sockets
categories: Network
tags: [Docs, Network, Python]
---

## Start: 

HTTP(HyperTextTransperProtocol) 개발자는 http:// 에 // 가 멋있어보여서 그냥 넣었다고 했다. 밀림의 왕자인 호랑이가 하는 거짓말은 아무리 간사한 여우라도 따라야 하는 법이다. 인터넷이라고 하는 멋진 곳에서 서버와 클라이이언트가 정보를 주고 받는 데에는 http, 프로토콜 등에 대한 배경 지식이 필요하다. python에서도 인터넷과 마찬가지로 built-in 으로 내장된 socket을 통해 데이터를 주고 받으면서 인터넷의 데이터를 쉽게 parse하고 이용할 수 있다.

![Foo](/assets/images/posts/2023-11-01/1.png)

사용될 application의 각 앞에 socket이 있는데, 이를 통해 네트워크간 통신이 가능하다. 소켓 하나에는 두 가지 기능이 있는데, 하나는 read 이고 다른 하나는 write 다. 그림의 1번 과정을 통해 내가 write한 데이터를 다른 소켓으로 전송한다. 2번 과정을 통해 내가 read 하는 데이터들은 다른 소켓으로부터 받아온 데이터임을 알 수 있다. 

![Foo](/assets/images/posts/2023-11-01/2.png)

내 소켓이 계속 waiting 상태에 있다면 상대 소켓에서 데이터가 보내진 게 확실한지 확인해야 한다. python으로 프로그램을 짤 때, 두 개의 소켓이 계속해서 대기 상태를 지속하지 않도록 정밀하게 프로토콜을 짜야 한다. 프로토콜에는 정보를 보낸 자가 누구인지, 어떻게 언제 보냈는지 등의 정보를 기록할 수 있다.

## References:
Python for Everybody 








