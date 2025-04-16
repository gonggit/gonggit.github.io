---
layout  : wiki
title   : 배열에서 조건을 만족하는 첫번째 요소 찾기 
summary : first or None 
date    : 2025-04-17 00:34:34 +0900
updated : 2025-04-17 00:40:33 +0900
tag     : python 
resource: 51/6346CD-3CD7-4B2A-BC08-678F2941E658
toc     : true
public  : true
parent  : [[/python]] 
latex   : false
---
* TOC
{:toc}

# 배열에서 바늘찾기 

코틀린에서 `firstOrNull`, `first` 같은 함수를 사용하는 것에 익숙하다면 파이썬에도 이런 게 있지 않을까? 싶은 생각이 든다.

이건 별개의 이야기인데, 파이썬에서 리스트를 조작하는 방법은 영 익숙해지지가 않는다. list(filter(lambda)) 혹은 list(map(filter(lambda))) 등등..

```python
def first_or_none(iterable, predicate):
    return next((x for x in iterable if predicate(x)), None)
```

사용 예시로는
```python
my_list = [2, 4, 6, 8]

result = first_or_none(my_list, lambda x: x > 10)
print(result)  # 출력: None
```

요 `next`란 함수가 무엇이냐? iterator에서 다음 요소를 꺼내는 함수이다. `next(generator, default)` 형식으로 사용하면 된다.
