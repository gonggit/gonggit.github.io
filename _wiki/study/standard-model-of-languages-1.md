---
layout  : wiki
title   : SMoL, 프로그래밍 언어에 대해서 (1)
summary : 
date    : 2024-04-15 16:32:30 +0900
updated : 2024-04-17 17:36:11 +0900
tag     : 
resource: B6/6BD3DC-3812-4E2B-8269-72C3C1AD5692
toc     : true
public  : true
parent  : 
latex   : false
---
* TOC
{:toc}

# Standard Model of Laugnages
여러 언어를 다루어 본 사람이라면, 혹은 한 가지 언어를 쭉 사용하다가 다른 언어를 배워야 하는 상황에 처한 사람이라면 '어, 내가 주로 쓰는 언어와 크게 다르지 않은데?' 라는 인상을 받을 때가 있다. 사실 어느 정도 연차가 쌓인 개발자들이 새로운 언어를 사용해야 하는 환경에 대한 걱정을 크게 하지 않는 이유가 바로 그 때문이다. 여러가지 현대 프로그래밍 언어가 공유하는 중요한 특성들이 있기 때문에 새로운 언어에 적응하는 것도 그 언어만의 특수한 문법 정도에 익숙해지는 것 정도가 되는 것이다.

이러한 특성들에 대해 정리하고, 많은 프로그래머들이 여러가지 이유로 오해하고 있는 특성에 대해 정리한 블로그 및 교육 자료가 있어 정리해두고자 한다.

# Semantic Cores

블로그에는 몇 가지 특성을 SMoL로 정의하고 있다.

- variables are lexically scoped
  - 변수는 lexical scope 안에서 정의된다. 
- scope can be nested
  - 스코프는 중첩될 수 있다.
- evaluation is eager
  - 평가(Evaluation)는 즉시 발생한다.
- evaluation is sequential (per “thread”)
  - 평가(Evaluation)은 순차적이다(스레드별)
- variables are mutable, but first-order
  - 변수는 변경 가능하고, 1급이다.
- structures (e.g., vectors/arrays and objects) are mutable, and first-class
  - 구조체는 변경 가능하고, 1급이다.
- functions can be higher-order, and close over lexical bindings
  - 함수는 고차함수일 수 있고, lexical binding 밖에서 닫힌다. 
- memory is managed automatically (e.g., garbage collection)
  - 메모리는 자동으로 관리된다.
  
이런 특성을 잘 기억한다면, 아래와 같은 이점을 가질 수 있다.

# SMoL에 대해 제대로 알면, 
- 여러 언어들의 핵심 기능을 잘 다룰 수 있게 된다.
- 다른 언어들을 배울 때 기존의 지식을 적용할 수 있고, 공통점을 발견할 수 있게 된다. 따라서 새로운 언어를 배우는 것이 쉬워진다. 
- 다른 언어들 사이의 차이점에 대해 더 뚜렷하게 구분할 수 있게 된다.
- 언어의 문법 이면에 모든 언어들이 공유하는 'Best Practice'를 알 수 있다.

# 그래서, 이 프로그램은..
[SMoL Tutor](https://smol-tutor.xyz/) 에서는 프로그래밍 경험이 어느 정도 있는 학생 혹은 직업인을 대상으로 잘못 이해하고있는 개념을 찾아서 고쳐준다. 여러 섹션의 개념과 문제로 이루어진 과정에서, 학생들은 오개념을 바로잡고 SMoL의 전문가로 거듭날 수 있게 된다!
