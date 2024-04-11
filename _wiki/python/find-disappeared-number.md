---
layout  : wiki
title   : 배열에 없는 숫자 찾기  
summary : Leetcode 448 
date    : 2024-03-28 18:43:15 +0900
updated : 2024-03-28 23:44:43 +0900
tag     : 
resource: 92/8EE47A-6706-4F65-B2A5-956FA6A84AD3
toc     : true
public  : true
parent  : 
latex   : false
---
* TOC
{:toc}

# 문제

> Given an array nums of n integers where nums[i] is in the range [1, n], return an array of all the integers in the range [1, n] that do not appear in nums.<br />
[1, n] 범위의 정수 n개로 이루어진 배열 `nums`가 있다. [1, n] 범위 내 모든 정수 중 `nums` 에 없는 숫자들을 모두 반환하라.

Example 1.

Input: nums = [4,3,2,7,8,2,3,1]
Output: [5,6]

Example 2:

Input: nums = [1,1]
Output: [2]

# 생각해보기

가장 간단한 방법은 Counter를 이용해서 각 element를 키로 갖는 HashSet을 만들고 1부터 n까지 반복하면서 키가 없는 요소를 반환하면 간-단.
공간복잡도가 O(n), 시간복잡도는 O(n)

어차피 배열을 한 번 순회해야 하는 것은 명백하니 공간복잡도를 줄일 수 있는 방법이 있을까?

이 때 유효한 조건이 배열 속 정수의 범위가 [1, n] 이라는 것. => 배열의 각 요소를 배열의 index로 가정할 수 있다.
그러니까 배열의 요소를 index (정확히는 index - 1)로 가정하고, 해당 요소를 음수 혹은 구별할 수 있는 값으로 바꾼다.

변환 과정 후 다시 배열을 순회하면서 구별값이 아닌 경우 그 index (정확히는 index + 1)가 없는 정수이므로 결과 배열에 추가.

```python
class Solution:
    def findDisappearedNumbers(self, nums: List[int]) -> List[int]:
        for n in nums:
            i = abs(n) - 1 # 각 요소(n)을 배열의 인덱스로 변경한다.
            nums[i] = -1 * abs(nums[i]) # 해당 인덱스의 값을 음수로 변경한다.
        
        return [i + 1 for i in range(len(nums)) if nums[i] > 0] # 배열을 순회하며 변경되지 않은 엘리먼트의 인덱스를 반환
```
