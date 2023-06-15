---
layout  : wiki
title   : json.dumps 할 때 한글 깨짐 
summary : 또 잊어버리느니 기록해두자. 
date    : 2023-06-14 17:19:21 +0900
updated : 2023-06-15 17:56:11 +0900
tag     : 
resource: 60/54A84D-0A12-485B-9DC7-ED258C4ED80B
toc     : true
public  : true
parent  : [[/python]] 
latex   : false
---
* TOC
{:toc}

# 좋은 친구 파이썬
파이썬은 간단한 작업을 할 때 매우 유용한 도구다. 쉽고 빠르고 간편하다. 인터넷 세상에 레퍼런스가 가득해서 하고자 하는 것을 웬만해서는 찾을 수 있다.
나도 업무 내, 외적으로 파이썬을 자주 사용했는데, 주로 배치작업이나 간단한 API 호출 스크립트, 문서 파싱 등에 사용했다.

## import json
파이썬에서 JSON을 다루기 위해서 import하는 모듈. 개인적으로는 loads와 dumps 밖에 사용하지 않는다(...)
문제는 dumps, 그러니까 파이썬의 dictionary 객체를 json 포맷으로 변환할 때 한글이 유니코드로 찍히는 현상이 있었다.

사실 동일한 문제를 여러번 겪었지만 메인으로 사용하는 언어도 아니고 그때그때 찾아보면 되니까 찾아보고 넘어가고, 또 찾아보고 넘어가곤 했는데 이번에는 어쩐지 이런 내 모습에 부아가 치밀어서(...) 그냥 정리해두려고 한다.


```python
import json

data = {
    "status": "success",
    "body": "안녕하세요. 한글을 출력하면 이상하게 나온다면서요?"
}

# {"status": "success", "body": "\uc548\ub155\ud558\uc138\uc694. \ud55c\uae00\uc744 \ucd9c\ub825\ud558\uba74 \uc774\uc0c1\ud558\uac8c \ub098\uc628\ub2e4\uba74\uc11c\uc694?"}
json.dumps(data)
```

이런 경우에, dumps 메소드의 named parameter로 ensure_ascii=False 를 같이 넘겨주면..

```python
import json

data = {
    "status": "success",
    "body": "안녕하세요. 한글을 출력하면 이상하게 나온다면서요?"
}

# '{"status": "success", "body": "안녕하세요. 한글을 출력하면 이상하게 나온다면서요?"}'
json.dumps(data, ensure_ascii=False)
```

이렇게 한글을 제대로 표현한다. 참고로 ensure_ascii 옵션에 대한 [공식문서](https://docs.python.org/ko/3.7/library/json.html)의 설명은 다음과 같다.

```
ensure_ascii가 참(기본값)이면, 출력에서 모든 비 ASCII 문자가 이스케이프 되도록 보장됩니다. 
ensure_ascii가 거짓이면, 그 문자들은 있는 그대로 출력됩니다.
```

기본값은 True이고, 이 경우 ASCII 문자에 속하지 않는 문자를 모두 이스케이프해서 출력한다는 뜻이다. 그래서 첫번째 경우 유니코드로 이스케이프되어 출력되었던 것이다. 반대로 False라면 문자 그대로 출력..

아무튼 ensure_ascii 옵션을 이제는 기억하도록 하자..
