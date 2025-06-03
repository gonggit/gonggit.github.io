---
layout  : wiki
title   : cursor로 jq 학습 사이트 만들기 
summary : 
date    : 2025-05-30 23:29:22 +0900
updated : 2025-06-03 23:09:29 +0900
tag     : jq cursor ai 
resource: D7/063ECA-60CA-4064-95A8-8FBF88D1B572
toc     : true
public  : true
parent  : [[/developer]]
latex   : false
---
* TOC
{:toc}

# Cursor로 무엇을 할 수 있을까?
처음 cursor를 사용하기로 마음먹고 무엇을 해보면 좋을까? 하고 생각해 보았을 때 가장 먼저 떠올랐던 것이 바로 학습 도구였다. 내가 새로운 것을 접할 때 가장 효과적이었던 예시와 반복 연습을 통한 학습법을 이용해 일상적으로 사용하고 있지만 제대로는 알지 못했던 것들을 스스로 연습할 수 있는 학습장을 만들어보면 어떨까? 하는 것이었다. 그렇다면 어떤 것을 주제로 할까? 했을 때 가장 먼저 떠올랐던 것들 중 하나가 바로 `jq` 명령어였다.

## jq
>jq is like sed for JSON data - you can use it to slice and filter and map and transform structured data with the same ease that sed, awk, grep and friends let you play with text.

> jq는 JSON 데이터를 위한 sed같은 명령어입니다. sed, awk, grep과 같은 친구들처럼 jq를 이용해 JSON 데이터를 쉽게 자르거나 추출하거나 매핑, 그리고 변형할 수 있습니다.  

그러니까 어떤 JSON 데이터를 봐야 할 때, 예를 들어 API 응답을 확인해본다거나 JSON으로 저장한 데이터를 보아야 할 때는 항상 jq를 이용하는 것이 좋은 경우가 많다. 실제로 API 응답을 볼 때 `curl https://json-data-url | jq .` 처럼 사용한다든가 하면 raw json을 beautify한 형태로 확인할 수 있다는 것이다.

## jq-academy
그래서 cursor와 두시간 정도 아웅다웅 한 후 [jq-academy](https://jq-academy.vercel.app/stage/0) 를 만들었다. 사실 아직 UX도 조잡하고 데이터도 완전하지 않지만 Cursor를 이용하여 그래도 유의미한(?) 결과를 냈다는 것에 만족한다. 자세한 사용기에 대해서는 몇 번 더 써보고 정리할 수 있을 것 같다.

