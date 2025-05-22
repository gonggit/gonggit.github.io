---
layout  : wiki
title   : ZRANGEBYSCORE는 왜 사라졌을까?
summary : 
date    : 2025-04-19 00:16:29 +0900
updated : 2025-05-22 23:24:30 +0900
tag     : redis xrange deprecated 
resource: 8E/4EA5F3-9794-4CB3-A125-2A2787433C79
toc     : true
public  : true
parent  : [[/study]]
latex   : false
---
* TOC
{:toc}

# XRANGE

Redis를 쓰다 보면 정렬된 집합(Sorted Set)에서 값들을 조회할 일이 종종 생긴다.  
예전에는 score 범위로 조회할 땐 `ZRANGEBYSCORE`, 사전식 범위로 조회할 땐 `ZRANGEBYLEX`를 썼다.  
근데 Redis 6.2부터 이 명령어들이 deprecated 되었다. 더 이상 권장하지 않는다는 이야기다.

처음엔 조금 당황스러웠다. 익숙한 명령어들이 하나둘씩 사라지면 괜히 마음이 불편하다.  
하지만 그 속사정을 알고 나니, 나름대로 이해가 된다.

---

## 명령어가 너무 많았다

Redis는 점점 기능이 많아지면서 명령어도 많아졌다.  
`ZRANGE`, `ZREVRANGE`, `ZRANGEBYSCORE`, `ZREVRANGEBYSCORE`, `ZRANGEBYLEX`, `ZREVRANGEBYLEX`...  
같은 동작을 하는데 정렬 순서나 기준만 달라진다고 명령어가 죄다 따로따로였다.

이걸 Redis 6.2부터 하나로 통합한 것이다. 바로 `ZRANGE`라는 명령어로.

---

## ZRANGE 하나로 통합

Redis 6.2부터는 `ZRANGE`가 훨씬 강력해졌다.  
다양한 옵션이 추가되었고, 이제 이 하나로 대부분의 조회 작업이 가능하다.

| 옵션         | 설명                              | 대체하는 명령어                          |
|--------------|-----------------------------------|-------------------------------------------|
| `BYSCORE`    | score 기준으로 범위 조회          | `ZRANGEBYSCORE`, `ZREVRANGEBYSCORE`      |
| `BYLEX`      | 사전식 기준으로 범위 조회         | `ZRANGEBYLEX`, `ZREVRANGEBYLEX`          |
| `REV`        | 결과를 내림차순으로 정렬          | `ZREVRANGE` 계열                         |
| `WITHSCORES` | score 값을 함께 반환              | 기존과 동일                              |
| `LIMIT`      | offset, count 설정 (페이징 용도) | 기존과 동일                              |

이제는 `ZRANGEBYSCORE` 대신 `ZRANGE ... BYSCORE`를 쓰면 되고, `ZRANGEBYLEX`도 마찬가지다.

---

## 예제로 비교해 보기

### 1. ZRANGEBYSCORE → ZRANGE

```bash
# 예전 방식 (Deprecated)
ZRANGEBYSCORE myset 100 200 WITHSCORES LIMIT 0 10

# 새로운 방식
ZRANGE myset 100 200 BYSCORE WITHSCORES LIMIT 0 10
```

### 2. ZREVRANGEBYSCORE → ZRANGE + REV
```
# 예전 방식
ZREVRANGEBYSCORE myset 200 100 WITHSCORES LIMIT 0 10

# 새로운 방식
ZRANGE myset 200 100 BYSCORE REV WITHSCORES LIMIT 0 10
```

## 그래서 앞으로는 어떻게 해야 할까

이제 Redis에서 정렬된 집합을 다룰 땐 무조건 ZRANGE를 떠올리는 게 좋다.
예전 명령어들도 아직 작동은 하지만, 언젠가는 사라질 수 있다.
그리고 지금도 문서에선 명확히 deprecated로 표시되고 있다.

개발하면서 뭔가 명령어가 너무 많고 복잡하다고 느껴졌다면, 이 변화가 오히려 반갑게 느껴질지도 모르겠다.
하나로 통일된 명령어는 기억하기도 쉽고, 코드도 더 깔끔해진다.

--- 

## 참고 링크
- [Redis ZRANGE 공식 문서](https://redis.io/commands/zrange/)
