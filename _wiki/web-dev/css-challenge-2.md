---
layout  : wiki
title   : CSS CHALLENGE 2
summary : 
date    : 2023-09-26 21:53:42 +0900
updated : 2023-09-26 22:15:22 +0900
tag     : 
resource: 6F/EDBCB1-91C8-48C6-A526-2E6D2F939322
toc     : true
public  : true
parent  : 
latex   : false
---
* TOC
{:toc}

# 매일 CSS 챌린지 

## CHALLENGE 2
[문제](https://100dayscss.com/days/2/)

두번째 챌린지는 일명 햄버거라고 불리는 버튼을 만드는 것이었다. 그런데 이제 애니메이션이 적절히 가미된..

사실 transform을 사용 해 본 적도 별로 없는데, 애니메이션까지 가미하려니 여간 어려운 게 아니었다. 사실 이 두번째 문제까지 보고 도망가기만 일주일 넘게 하고, 하면서도 정말 몇 번이나 도망치고 싶었는데 끝까지 해서 제출했다는 것에 의의를 두어야 겠다.

CSS나 자바스크립트를 조금 더 최적화 할 수는 있겠지만 그건 다음에!

## 배운 점

- 최초로 CodePen의 CSS를 로컬 vim 환경으로 복붙하면 frame class가 적용되지 않는 현상이 있었는데 주석을 제거하니 잘 됐다. CSS 주석은 어떻게 하는거길래? (/* */)
- @keyframes 지시자에 대해 배웠다. 애니메이션을 정의하고, 적용하는 방법을 배웠다. 따로 정리할 기회가 있을 것이다.
- html 내부에 자바스크립트를 위치시키고 실행하는 방법을 배웠다. 아무리 getElementById 해도 요소를 못찾길래 스크립트를 닫는 html 태그 바로 위에 위치시켰더니 적용됐다.
- 클릭 할 때마다 동적으로 클래스를 부여 및 박탈하면서 미리 정의된 애니메이션을 적용시켰다. 더 세련된 방법이 있을 것 같아서 답지를 한 번 볼 생각이다.

## 결과물
<iframe height="300" style="width: 100%;" scrolling="no" title="Untitled" src="https://codepen.io/sunghyuk/embed/dywmBZJ?default-tab=html%2Cresult" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href="https://codepen.io/sunghyuk/pen/dywmBZJ">
  Untitled</a> by sunghyuk (<a href="https://codepen.io/sunghyuk">@sunghyuk</a>)
  on <a href="https://codepen.io">CodePen</a>.
</iframe>
