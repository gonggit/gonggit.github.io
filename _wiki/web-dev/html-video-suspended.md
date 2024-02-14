---
layout  : wiki
title   : 멈춰버린 비디오 
summary : 그런데 다른 곳에서는 잘 재생되는 
date    : 2023-10-25 16:15:22 +0900
updated : 2023-10-26 20:40:02 +0900
tag     : HTML, VIDEO 
resource: E4/27B2FD-12DC-4E3B-8814-35ACC2678910
toc     : true
public  : true
parent  : [[/web-dev]] 
latex   : false
---
* TOC
{:toc}

## 이상하다 이상해
같은 페이지 안에 두 개의 비디오 소스(같은 확장자, 다른 길이)가 있었다. `<video>` 태그를 이용해서 비디오를 임베드했고, 자동재생을 걸어두었다. 차이가 있다면 재생되는 비디오는 메인에(보통 히어로 영역이라고 부르는), 두번째 비디오는 스크롤을 한 window size만큼 내려야하는, 그러니까 다음 화면에 들어가있는 것이었다.

두번째 비디오는 아예 재생되지 않거나 1초 정도 재생되고 멈추는 등 일관성 없는 동작을 보였다. video element의 이벤트를 다 로깅해보았지만 별다른 이상이 보이지 않았다. 영상 순서를 바꾸어서 (히어로 <-> 다음 화면) 재생해 보니 둘 다 재생이 잘 됐다! 도대체 왜? 특이한 것은 다 그런 것은 아니고, 특정 윈도우 디바이스에서만 발생하고 있었다. 도대체 왜!

결론만 말하자면 mp4 비디오를 webm 비디오로 변환하니 잘 되었다. 대략 12MB -> 2MB로 줄었는데, 이게 로딩을 빨리 끝내줘서 그런건진 모르겠다. 그런데 히어로 영역에 있는 비디오가 더 큰 비디오인데 다음 화면에서도 재생 잘됐는데...

아무튼 이렇게 해결(...) 아래는 mp4 영상을 webm으로 변환한 cli command이다. ffmpeg을 설치한 후 사용해야 한다.


```
ffmpeg -i input.mp4 -c:v libvpx-vp9 -crf 30 -b:v 0 -b:a 128k -c:a libopus output.webm
```