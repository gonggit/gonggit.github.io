---
layout  : wiki
title   : object literal? 
summary : 타입스크립트 뉴비의 좌충우돌 공부 
date    : 2023-09-15 18:30:35 +0900
updated : 2023-09-22 20:06:10 +0900
tag     : 
resource: 72/0FE31D-A207-40F8-986A-7AB5E5956AD6
toc     : true
public  : true
parent  : [[/typescript]]
latex   : false
---
* TOC
{:toc}

# 그 미묘함에 대하여 
메인 프레임워크를 정함에 따라 타입스크립트를 공부해야 할 때가 되었다. 사실 한 가지 언어를 오래 사용하다 보면 다른 언어를 새로 배우는 것이 제로베이스에서 시작하는 것과는 사뭇 난이도가 달라지는 것 같다. 많은 고수준 언어들이 기본적으로 갖는 특성들이 정해져있기 때문에 숙련도 문제를 제외하면 어떤 언어로 시작하더라도 단순한 기능을 구현하는 것에는 큰 무리가 없다.

그래서 타입스크립트를 처음 시작하는 것도 크게 무리는 없었다. 자바스크립트를 배워보려는 시도를 한 적이 몇 번인가 있었는데 적응하지 못했던 이유는 강타입 컴파일 언어에 익숙해져 스크립트 언어에 잘 적응이 되지 않았다(개념적으로 반대인 것은 아니지만). 그래도 타입스크립트를 이전 회사에서 찍어 먹어보고 자바스크립트와는 꽤 다른 인상을 받았고, 이거 하나만 제대로 해도 앞으로 먹고 사는 데 큰 지장이 없을 것 같아 새로이 시작하게 되었다!

## 무서운 이야기 

그렇게 타입스크립트를 기초로 Next.js 어플리케이션을 개발할 때 있었던 일이다. 아래와 같은 코드를 작성하고 있었는데, 

```typescript
interface ElementProps {
  title: string;
  description: string;
  price: number;
}

function createElement(props: ElementProps): string {
  // blah blah..
  return 'element'
}

createElement({
  title: "춘식이 스퀴즈볼",
  description: "귀여운 춘식이 볼을 조물락",
  price: 10000,
  discountRate: 5, // 에러!
});
```

위 코드에서는 아래와 같은 에러가 발생한다.

```
Argument of type '{ title: string; description: string; price: number; discountRate: number; }' is not assignable to parameter of type 'ElementProps'.
Object literal may only specify known properties, and 'discountRate' does not exist in type 'ElementProps'. (tsserver 2345)
```

바로 ElementProps 인터페이스에 존재하지 않는 discountRate 라는 키를 가진 Object literal을 파라미터로 넘겼기때문에 문제가 된다는 것이다.

사실 코드상으로 보면 문제가 없어보이는데, 이는 특별히 객체 리터럴(Object Literal)에만 적용되는 `Excess Property Check` 때문이다.

## Excess Property Check?

직관적으로는 초과 프로퍼티가 있는지 체크한다는 말이다. ElementProps 인터페이스에 존재하지 않는 discountRate 라는 키가 담긴 객체 리터럴을 넘겼기때문에 문제가 생긴다는 것이다. 
어쨌든 넘겨준 객체 리터럴이 ElementProps 인터페이스의 슈퍼셋인데 왜 안되는 것일까?  

오직 객체 리터럴민이 다른 변수에 할당되거나 함수 파라미터(매개변수)로 넘겨질 때 적용되는 특별한 규칙이 있는데, 그것이 바로 이 Excess Property Check, 그러니까 타겟 타입에 없는 프로퍼티를 객체 리터럴이 가지고 있는 것을 잠재적인 버그 상황이라고 보고 오류를 발생시키는 것이다.

이를 피하기 위한 방법으로 몇 가지 방법을 제시하는데 다음과 같다.

```typescript
// 강제 형변환
createElement({
  title: "춘식이 스퀴즈볼",
  description: "귀여운 춘식이 볼을 조물락",
  price: 10000,
  discountRate: 5,
} as ElementProps);
```

 혹은
 
```typescript
const parameter = {
  title: "춘식이 스퀴즈볼",
  description: "귀여운 춘식이 볼을 조물락",
  price: 10000,
  discountRate: 5,
}

// 별도의 변수로 분리한 후 넘긴다.
// 하지만 최소 하나의 공통 프로퍼티가 있어야 오류가 발생하지 않는다.
createElement(parameter);
```

혹은

```typescript
interface ElementProps {
  [propName: string]: any;
  price: number;
}

function createElement(props: ElementProps): string {
  // blah blah..
  return 'element'
}

createElement({
  title: "춘식이 스퀴즈볼",
  description: "귀여운 춘식이 볼을 조물락",
  price: 10000,
  discountRate: 5,
});
```

이렇게 우회할 수 있는 방법이 있음에도 불구하고, 이런 상황(우회해야하는 상황)이 발생하는 것 자체가 잠재적인 버그일 수 있다. 이런 경우에는 ElementProps 인터페이스가 Excess property를 정의하도록 수정하는 것이 가장 좋은 방법이다.


### 참고 문서
[object literal에 관한 공식 문서](https://www.typescriptlang.org/docs/handbook/2/objects.html#excess-property-checks)

