---
layout  : wiki
title   : 나도 해보자 AI 
summary : 커밋 메세지를 어떻게 써줄까? 
date    : 2023-02-16 23:24:36 +0900
updated : 2023-02-16 23:34:38 +0900
tag     : 
resource: 7F/463669-2E04-4753-BF4A-1D266B0C80B0
toc     : true
public  : true
parent  : [[/hobby]] 
latex   : true 
---
* TOC
{:toc}

# 대 AI 시대

ChatGPT가 열어제낀 대 AI시대를 맞아 나름 IT 업계 종사자이며 개발자인 내가 이를 외면할 수는 없다.

## 자동으로 생성된 커밋 메세지?
세팅은 간단하다. npm으로 aicommits를 설치하고, OpenAI에 가입한 후 인증키를 발급받아 스크립트 세팅을 한 후, 레파지토리에서 `aicommits` 명령어를 수행하기만 하면 된다는 것이다!

## 이 포스트부터
과연 이 포스트를 커밋하면 어떤 메세지가 생성될까? 

> Add files for hobby and ai-commit-test in wiki directory, add metadata and total-document-url-list entries for hobby and ai-commit-test.

세상에! 정말 직관적이고 단순한 형태의 메세지다. 

## 어떤 원리
공식 레파지토리의 설명에 따르면 `git diff` 명령어를 수행한 후 최신 코드 변경점을 OpenAI의 GPT-3 으로 전송해 그 결과값을 사용한다는 것이다.
사실상 `aicommits`의 역할은 로컬 리파지토리와  GPT-3 사이의 가교 정도인 것 같다.

## 앞으로
마찬가지로 공식 레파지토리의 설명에 앞으로 업데이트 될 기능 목록이 명시되어 있는데, 프로젝트 특성상 사용성이나 UX 개선 정도가 예정되어 있는 것 같다. 

## 참고
[aicommits 공식 리파지토리](https://github.com/Nutlope/aicommits)
