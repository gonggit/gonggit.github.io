---
layout  : wiki
title   : CSS CHALLENGE 3 
summary : 
date    : 2023-09-27 20:54:13 +0900
updated : 2023-09-27 21:01:58 +0900
tag     : 
resource: 1A/110EF6-A354-43D2-8B38-4998099C1261
toc     : true
public  : true
parent  : 
latex   : false
---
* TOC
{:toc}

# 너무 어렵다!
진짜 중간에 너무 포기하고싶었다. 그래서 마지막에 피라미드 그림자는 답을 베꼈다. 그렇게라도 하지 않으면 도저히 오늘 마무리 할 수 없을 것 같아서..

어제 챌린지랑 비슷하게 animation 쓰는 거였고, 역시나 몇 가지 병목 지점이 있었다.

# 배운 점
- 세모 만들기! 피라미드의 앞, 뒤를 각각 세모로 만들어야했는데, ChatGPT에 물어보니 width, height가 모두 0이고 border를 이용해서 만들라고 하더라. 이게 편법인것 같은데 정확히 원리를 이해를 못했다.
- 태양이 빙글 도는 것은 태양을 감싸는 네모를 하나 상상하고, 네모 안에 동그라미를 하나 집어넣은 다음 네모의 우측 하단 모서리를 기준으로 회전시킨다고 생각했다.
- 피라미드의 양 면은위에서 언급했던 border를 이용해서 만들었고, 그러다보니 양 면 사이에 빈틈이 조금 보이는 것 같았다.
- 그림자는 답을 베꼈고, clip-path에 대해서 공부해야 겠다. 애니메이션은 scaleY와 clip-path의 polygon을 이용했다.

# 결과물
<iframe height="300" style="width: 100%;" scrolling="no" title="CHALLENGE #3" src="https://codepen.io/sunghyuk/embed/ExGLbJm?default-tab=result" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href="https://codepen.io/sunghyuk/pen/ExGLbJm">
  CHALLENGE #3</a> by sunghyuk (<a href="https://codepen.io/sunghyuk">@sunghyuk</a>)
  on <a href="https://codepen.io">CodePen</a>.
</iframe>
