---
layout  : wiki
title   : backoff 설정 한 번 봐 주세요. 
summary : 얼마만큼더기다리는거에요? 
date    : 2025-03-26 00:14:42 +0900
updated : 2025-03-26 00:35:58 +0900
tag     : 
resource: D8/DEF49B-56C0-4443-9DDE-54205861E9EC
toc     : true
public  : true
parent  : [[/developer]]
latex   : false
---
* TOC
{:toc}

# Backoff?
처음 Backoff를 접하는 것은 보통 데이터통신 같은 전공수업 때일 것이다. 전송제어 등을 배울 때 실패한 전송을 어떻게 재처리 할 것인가 등의 내용에 등장하는 것이 바로 이 backoff 이다.

소프트웨어 엔지니어링에서 **Backoff**는 **재시도(retry) 전략**의 일환으로, 실패한 요청을 일정 시간 대기 후 다시 시도하는 방식이다.  

**과부하 방지, 네트워크 안정성 개선, 트래픽 급증 완화** 등의 목적으로 사용되며, **Kafka, RabbitMQ, Redis** 같은 메시징 시스템 및 분산 시스템에서도 활용된다.

그러니까 대상이 연결을 받아줄 수 없는 장애 상황에 무작정 계속해서 연결을 시도하는 것 보다는, 일정 주기 혹은 증가하는 주기로 시도하여 연결을 시도 혹은 받아주는 양쪽 모두의 부하를 줄여주는 방법인 것이다.

---

## 📌 Backoff 유형

### 1. Fixed Backoff (고정된 대기시간)
- 일정한 간격으로 재시도.
- 예: `100ms → 100ms → 100ms`

### 2. Linear Backoff (선형 증가)
- 재시도할 때마다 대기시간이 일정한 값만큼 증가.
- 예: `100ms → 200ms → 300ms → 400ms`

### 3. Exponential Backoff (지수형 증가)
- 대기시간이 `2^n` 또는 `base^n` 형태로 증가.
- 네트워크 트래픽이 급증했을 때 서버 보호를 위해 사용됨.
- 예: `100ms → 200ms → 400ms → 800ms`

### 4. Exponential Backoff with Jitter (지터 포함)
- 지수형 증가 방식에 난수를 추가하여 **부하 집중을 방지**.
- 예: `100ms → 210ms → 430ms → 870ms (랜덤 값 포함)`

---

## 📌 실제 사용 예시

### ✅ Kafka Backoff 설정
Kafka에서는 메시지 전송 실패 시 재시도(backoff)를 위해 `retry.backoff.ms`, `reconnect.backoff.ms` 같은 설정을 사용한다.

```properties
# Producer에서 메시지 전송 실패 시 재시도 간격 (기본값: 100ms)
retry.backoff.ms=200

# Broker와의 재연결 시도 간격 (기본값: 50ms)
reconnect.backoff.ms=300
```
참고 : retry.backoff.ms[^id], reconnect.backoff.ms[^id2]


## 📌 결론

Backoff는 분산 시스템 및 메시지 브로커에서 재시도 요청을 제어하여 네트워크 안정성과 성능을 보장하는 중요한 전략이며, 여러 시스템에서도 이를 활용하여 과부하를 방지하고 안정적인 연결을 유지할 수 있게 된다.

실무에서 제반 인프라(카프카 등)와 커넥션 에러가 계속해서 발생할 때 자신감 있게 말하자. 

> 이거 backoff 어떻게 설정되어 있어요? 다음 시도까지 너무 오래 걸리면 그냥 재배포 하시죠!

## 참고
[^id]: [retry.backoff.ms 설정](https://docs.confluent.io/platform/current/installation/configuration/producer-configs.html#retry-backoff-ms){:target="_blank"}
[^id2]: [reconnect.backoff.ms 설정](https://docs.confluent.io/platform/current/installation/configuration/producer-configs.html#reconnect-backoff-ms){:target="_blank"}

