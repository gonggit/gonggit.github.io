---
layout  : wiki
title   : Redis 이모저모 (2) Keys 
summary :  
date    : 2024-05-09 11:07:50 +0900
updated : 2024-05-10 17:33:44 +0900
tag     : REDIS 
resource: 8A/4694E4-1242-4468-8B7A-2BF618124647
toc     : true
public  : false
parent  : [[/study]] 
latex   : false
---
* TOC
{:toc}

# Keys

- Syntax
```
KEYS pattern
```
- 사용 가능한 버전 : 1.0.0 ~
- 시간 복잡도 : O(N). N은 레디스에 저장된 키의 개수. (레디스에 저장된 키들의 이름과 패턴의 길이가 유한하다는 가정 하에) 


## 전가의 보도
레디스를 운영하다 보면 반드시 할 수 밖에 없는 일이 있다. 바로 저장된 데이터를 찾는 것이다. Key-Value 저장소인 레디스에서는 당연히 키를 기준으로 값을 찾게 되는데, 이 때 사용하는 명령어가 바로 Keys 이다.


