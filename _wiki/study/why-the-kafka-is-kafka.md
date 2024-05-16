---
layout  : wiki
title   : 카프카는 왜 카프카가 되었나? 
summary : 
date    : 2024-05-10 17:33:59 +0900
updated : 2024-05-14 18:22:08 +0900
tag     : kakfa 
resource: B5/768432-64B7-4DEB-9583-85B77A11CD06
toc     : true
public  : true
parent  : [[/kafka]] 
latex   : false
---
* TOC
{:toc}

# Apache Kafka, Franz Kafka
아파치 카프카의 이름이 세계적 소설가 프란츠 카프카의 이름으로부터 유래했다는 사실은 저명한 사실이다. 다만 왜 프란츠 카프카의 이름을 차용했는가에 대해서는 항상 의문을 갖고 있었다.

# 카프카는 왜 카프카일까?

정설이라고 해야할까, 현 Confluent의 CEO이자 코파운더 그리고 아파치 카프카의 커미터인 [Jay Kreps](https://www.linkedin.com/in/jaykreps/){:target="_blank"}가 [Quora](https://www.quora.com/What-is-the-relation-between-Kafka-the-writer-and-Apache-Kafka-the-distributed-messaging-system/answer/Jay-Kreps){:target="_blank"}에 남긴 답변에 따르면 그 이유는 아래와 같다.

>I thought that since Kafka was a system optimized for writing using a writer's name would make sense. I had taken a lot of lit classes in college and liked Franz Kafka. Plus the name sounded cool for an open source project.
>
> So basically there is not much of a relationship.

> 카프카는 쓰기에 최적화된 시스템이었기 때문에 작가의 이름을 사용하는 것이 일맥상통해 보였다. 대학시절 문학 강좌를 여럿 수강했고, 그 중 프란츠 카프카를 좋아했다. 게다가 그 이름이 오픈소스로 사용하기에 멋져보이기도 했다.
>
> 그러니까 근본적으로는 그리 큰 연관은 없다고 볼 수 있다.

어쨌든 카프카의 근본인 이벤트 스트리밍 시스템, 그러니까 이벤트를 읽고 쓰는 것이 가장 기본적이고 근본적인 목적이었기 때문에 작가의 이름을 쓰는 것이 괜찮아보였다는 것이다. 어쩐지 김 빠지는 이유인 것 같기도 한걸..

# 그 외

이름의 기원에 대한 이야기 외 몇 가지의 재미있는 이모저모를 더 찾을 수 있었다.

1. 옥스포드 대학에서 현대 독일 문학을 연구하는 교수 Karen Leeder에 따르면, 프란츠 카프카는 생전 엄청난 양의 편지를 썼고 이 편지들이 제대로 전달되었는지에 대해 편집증적인 모습을 보였다고 한다. 아파치 카프카가 이벤트의 읽기/쓰기에 높은 수준의 신뢰도를 보장하는 것과는 대조되는 모습이다. [^kafka-reference-1]
2. 카프카는 살아 생전 아버지와의 관계가 매우 좋지 않기로 유명했다(문학계에서 카프카의 아버지는 아버지라는 지위의 폭력성이 언급될 때 자주 거론된다고 한다). 카프카는 아버지와 직접 대화하는 것을 극도로 꺼려했고 할 말이 있으면 50장 분량의 편지를 쓴 적도 있다고 한다. 아파치 카프카가 지향하는 `효율적인 메세징 시스템` 과 비교되는 모습이다.[^kafka-reference-2]
3. 그마저도 아버지에게 직접 편지를 전달하지 않고 어머니를 통해 전달했고, 어머니는 편지를 먼저 읽어본 후 아버지에게 전달할지 말지 고민했다고 한다. 신뢰성 높은 메세지 전달을 추구하는 아파치 카프카 시스템과 또 한 번 대조되는 모습이다.
4. 프란츠 카프카의 작품 «황제의 전갈» 에서 마지막 문장은 다음과 같다. *그런데도 그대는 창가에 앉아 저녁이 오면 그 전갈을 꿈꾼다.*

# 출처

[^kafka-reference-1]: https://hackernoon.com/the-missing-introduction-to-kafka-85f8627f8153
[^kafka-reference-2]: https://www.quora.com/What-is-the-relation-between-Kafka-the-writer-and-Apache-Kafka-the-distributed-messaging-system/answer/Jay-Kreps
