---
layout: post
title: CodeCommit - Slack App Alarm
subtitle: 코드업데이트 시 슬랙으로 알람 설정하기
categories: AWS
tags: [Docs, AWS CICD]
---

ci-cd 파이프라인을 사용하여 코드관리와 배포를 한 번에 처리하면서, 알람을 설정하여 여러 사람에게 공유될 수 있도록 설정합니다.
Codecommit 에서 branch 상태변화에 대하여 알람하는 방법을 알아봅니다.

AWS Chatbot 에서 APP으로 연결된 슬랙용 클라이언트를 구성합니다.

![Foo](/assets/images/posts/2021-12-17/1.png)

알람을 받을 슬랙에 로그인하면 권한 요청을 위한 액세스 질문이 나오고 이를 허용합니다.

슬랙 워크스페이스의 이름으로 챗봇에 클라이언트가 구성되고 
알람을 받을 채널을 설정해줍니다.

![Foo](/assets/images/posts/2021-12-17/3.png)


코드커밋 서비스에서 사용하는 repository 하단에 setting - notification, Create notification rule 을 구성합니다.
branch 에 변경이 있을 때 앱에 알람이 오도록 설정하고 싶습니다.
Target 에는 SNS Topic/ AWS Chatbot 이 가능하며, 저는 다이렉트로 chatbot 에 알람이 오도록 합니다.

![Foo](/assets/images/posts/2021-12-17/4.png)


테스트로 코드커밋에서 코드를 임의로 수정하여 커밋해보니, 

![Foo](/assets/images/posts/2021-12-17/6.png)

알람이 잘 작동합니다.



