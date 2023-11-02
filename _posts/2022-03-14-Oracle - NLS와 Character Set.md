---
layout: post
title: Oracle - NLS와 Character Set
subtitle: Error:Not a valid month
categories: DB
tags: [Troubleshooting, Oracle]
---

### Situation
- Oracle8
- Oracle11

### Error
```sql
SELECT to_date('07-JUN-16','DD-MON-RR') FROM DUAL ;
```

위 sql을 사용할 경우 아래와 같은 에러가 발생.

```bash
Not a valid month
```
: 지정한 월이 부족합니다



'DD-MON-RR'은 day, 축약된 문자 월, 2자리로 표현되는 년도수 이다.<br> 
그런데 왜 위 같은 에러가 보일까?<br>

찾아보니 language에 대한 DB 셋팅에서 display 되는 문자와 실제 저장되는 데이터 문자가 다르게 설정되어 있을 경우 dd-mon-rr 에서 오류가 발생한다고 한다.<br> 
mon 으로 축약된 문자를 읽어들이는 데 이를 한국어로 인식하기 때문이다. <br>

![Foo](/assets/images/posts/2022-03-14/1.png)

검색해서 이것저것 찾아보니 character set 과 language set 이란 용어도 있고 개념에 대해 알 필요가 있겠다 싶어 이에 대해 정리해보려고 한다.

### Solution

https://docs.oracle.com/cd/A87860_01/doc/server.817/a76966/ch1.htm

Oracle8.1.7 의 NLS(Nature Languagee Support) 문서에 따르면, <br>
ORA_NLS Environment Variable 을 설정하여 data 디렉토리에 multilingual DB 데이터에 대한 조각들이 각각 저장된다. 데이터는 다양한 언어를 포괄적으로 저장할 수 있고, 이 데이터의 처리와 함수사용, 사용자가 원하는 방식으로 출력되는 것이 가능하게 하는 것은 NLS 라이브러리의 지원이 있기 때문이라는 뜻이다.

오라클의 클라이언트/서버가 통신할 때는 DB에 저장되는 텍스트 데이터를 지정하는 character set, language, territory 와 같은 파라미터를 서로 체크해서 데이터를 이동하거나 저장하게 된다. 

저장되는 데이터는 character set 설정 때문에 가능합니다. DBMS 는 오라클 서버 설치시에 이를 잘 선택해야 한다. 캐릭터셋 설정 값이 중간에 바뀌면, 이전에 저장된 데이터는 그 이전 버전으로, 이후에 저장되는 데이터는 변경값으로 저장된다.

Character set 은 AL32UTF8(UTF-8) 로도 변경이 가능하다. 대부분의 경우는 오라클 인스톨러(OUI)에 의해 자동으로 설정되고, unix, linux 몇가지 ms 플랫폼은 utf-8 캐릭터셋 선택이 불가능하다. AMERICAN 으로 캐릭터셋이 설정되는 것이 default 인데 이 경우 default date format 도 'DD-MON-RR' 이다.

* nls_language 를 변경할 때 
```sql
alter session set nls_language = AMERICAN ;
```