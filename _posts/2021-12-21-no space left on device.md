---
layout: post
title: EC2 - no space left on device
subtitle: resize volumne
categories: AWS
tags: [Troubleshooting, AWS EC2]
---

## Error Code
```bash
failed to register layer: Error processing tar file(exit status 1): write /usr/local/lib/python3.5/dist-packages/tensorflow/python/_pywrap_tensorflow_internal.so: no space left on device
```
![Foo](/assets/images/posts/2021-12-21/1.png)

도커를 pull 하는 도중에 에러가 났다. 용량이 부족했던 것 같다

## Solution

1. 현재 볼륨 상태를 확인했다

![Foo](/assets/images/posts/2021-12-21/2.png)

![Foo](/assets/images/posts/2021-12-21/3.png)


2. Elastic Volume 에서 Modify 기능으로 볼륨 사이즈를 100 G 올려서 수정했다.

![Foo](/assets/images/posts/2021-12-21/4.png)

3. 증설한 볼륨을 파티셔닝, 리사이즈 했다.

![Foo](/assets/images/posts/2021-12-21/5.png)

![Foo](/assets/images/posts/2021-12-21/6.png)

![Foo](/assets/images/posts/2021-12-21/7.png)
