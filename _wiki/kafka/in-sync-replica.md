---
layout  : wiki
title   : In Sync Replication in Kafka
summary : Kafka 
date    : 2024-12-21 11:54:25 +0900
updated : 2025-01-02 00:08:18 +0900
tag     : 
resource: CE/9C1EFF-0283-426C-B931-124108F3894E
toc     : true
public  : true
parent  : [[/kafka]]
latex   : false
---
* TOC
{:toc}

# Kafka ISR 과 복제본 관리
카프카는 토픽의 파티션에 대해 복제본간 동기화를 위해 최선을 다한다. 이와 관련해 In Sync Replication (이하 ISR) 이라는 개념이 있는데 말 그대로 리더를 잘 복제하고 있는 팔로워를 말한다.

이 ISR 이라는 것은 굉장히 중요한 개념인데 리더 혹은 팔로워 파티션이 있는 브로커가 장애로 빠지게 된다든지 하는 상황에 언제든 그 파티션을 대체할 수 있는 후보가 있어야 Durable한 서비스를 할 수 있기 때문이다.

## 동기화
그렇다면 잘 동기화되고 있다는 것은 구체적으로 어떤 상태를 말하는 것일까? 이는 몇 가지 조건을 만족하는 것을 의미한다. `replica.lag.time.max.ms` 값 이내에 동기화가 수행되었는가(i.e. 팔로워가 제한시간 안에 리더에 fetch 요청을 보냈는가), 그리고 팔로워의 offset이 리더보다 `replica.lag.max.messages` 만큼 뒤쳐져있지 않은가이다.  둘 중 하나의 조건이라도 만족하지 못하는 경우 해당 팔로워는 `비 ISR(Non-ISR)` 상태가 된다.


### 토픽 생성

아래와 명령어는 파티션이 3개, 각 파티션의 replica 개수가 5개인 파티션을 생성하는 명령어다. 물론 이 경우 브로커의 개수가 5개 이상임을 가정한다. (브로커의 개수보다 많은 수의 복제본을 생성할 수는 없다)

이 때, `min.insync.replicas` 를 3으로 설정했는데, 이는 `ack` 옵션이 `all` 로 설정된 프로듀서가 성공적으로 메세지를 발행하기 위해 최소 3개의 ISR 상태의 replica가 있어야 한다는 의미이다. 반대로 프로듀서의 `ack` 옵션이 `all`이 아니라면 이 설정은 별다른 의미를 갖지 않는다.

```bash
# topic-level 설정
kafka-topics.sh --create \
--bootstrap-server localhost:9092 \
--topic example-topic \
--partitions 3 \
--replication-factor 5 \
--config min.insync.replicas=3
```
