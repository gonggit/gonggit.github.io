---
layout  : wiki
title   : Rust 배워보기 (1) 
summary :  
date    : 2023-03-07 16:49:03 +0900
updated : 2023-03-09 11:13:42 +0900
tag     : 
resource: 6E/3ADAA7-F19C-4AFF-ABD0-08DF8EC8F2E3
toc     : true
public  : true
parent  : [[/study]] 
comment : true
latex   : true 
---
* TOC
{:toc}

# 무료한 회사 생활, 즐거운 배움!
막바지를 향해가는 회사생활(?)에 새로운 자극이 필요한 차에 Rust를 배워보고 싶어졌다! 사실 이와 별개로 나의 접을 수 없는 FE 욕심에 Flutter를 공부하고 있긴 한데, 이것만 하긴 좀 심심하기도 해서 세계인이 사랑하는 언어 Rust를 함께 공부해보고 싶어졌다! 

그리고 어째선지 내가 즐겨 보는 블로그들에서 Rust를 소개하는 글들이 많아졌는데, 마침 새로운 배울거리를 원하던 나에게 딱 걸려버린것.. 

## Day 1

## 들어가기 전에 
Rust 공부를 시작하면 Cargo를 만나게 된다. Rust Ecosystem에서 Rust 어플리케이션을 빌드하고 실행하는 표준 도구다. 여기서 Rust Ecosystem은 몇 가지 툴로 이루어져있는데, `rustc` 라는 Rust 컴파일러와 dependency manager인 `cargo`, Rust toolchain installer & updater인 `rustup` 이다.

## Rust?
Rust는 2015년에 1.0 버전을 출시한 새로운 프로그래밍 언어다. Rust는..

- C++와 비슷한 역할을 하는 정적 컴파일 언어.
- LLVM을 백엔드로 사용한다.
- 다양한 플랫폼과 아키텍처를 지원한다.
- 펌웨어와 부트로더, 스마트 디스플레이, 휴대전화, 데스크톱, 서버 등 많은 장치에 이용된다.

## 왜 Rust?

- 컴파일 타임 memory safety
- 정의되지 않은 런타임 동작이 적음.
- 현대적인 언어 특성들.

### 컴파일 타임에 보장되는 것들
- 초기화되지 않은 변수 없음
- 메모리 누수 없음 (거의)
- double free 없음
- use-after-free 없음
- null pointer 없음
- 잊혀진 locked mutexes 없음
- 스레드간 data races 없음
- iterator invalidation 없음

가능한가..?

### 런타임에 보장되는 것들
- 배열 접근이 바운드 확인.
- Integer overflow 정의됨.

가능한가..?

### 현대적인 특성들
- 언어 특성
  - 열거형(Enums)과 패턴 매칭
  - 제네릭
  - No overhead FFI (모르겠음)
  - Zero-cost abstraction (모르겠음)

- 툴
  - 훌륭한 컴파일러 에러 
  - 빌트인 의존성 매니저
  - 빌트인 테스트 지원
  - 훌륭한 서버 프로토콜 지원

### 메모리 관리
전통적으로 메모리 관리하는 두 가지 방식이 있다.
- 직접 관리하는 방식: C, C++, Pascal..
- 런타임에 자동으로 관리하는 방식: Java, Python, Go, Haskell, ..

Rust는? 컴파일 타임에 올바른 메모리 관리를 강요함으로서 완전한 제어와 안정성을 확보한다.

### Stack vs Heap

- Stack
  - 컴파일 타임에 고정된 크기를 가짐.
  - 엄청 빠름 (스택 포인터를 옮기기만 하면 되니까)
  - 관리하기 쉬움 (function call 따라가기)
  - 뛰어난 메모리 지역성 (locality)
- Heap
  - 런타임에 유동적인 크기
  - 스택보다 조금 느림.
  - 메모리 지역성 보장 없음

### Ownership of Rust
```rust
fn say_hello(name: String) {
    println!("Hello {name}")
}

fn main() {
    let name = String::from("Alice");
    say_hello(name); // 최초로 say_hello를 호출하는 순간 main은 name에 대한 ownership을 포기한다.
    // say_hello(name); // 주석을 해제하면 compile error!
    // 이를 피하려면 say_hello 함수의 시그니쳐를 call by reference 형태로 변경하고 name의 reference(&name)을 넘기거거나, 명시적으로 .clone()을 이용해야 함.
}
```

### Borrowing
함수를 호출할 때 ownership을 전달하는 방법 대신, 값을 빌려줄(borrwoing) 수 있다.
```rust
#[derive(Debug)]
struct Point(i32, i32);

fn add(p1: &Point, p2: &Point) -> Point {
    Point(p1.0 + p2.0, p1.1 + p2.1)
}

fn main() {
    let p1 = Point(3, 4);
    let p2 = Point(10, 20);
    let p3 = add(&p1, &p2); // add function이 두 Point를 빌려받아 새로운 Point를 반환한다.
    println!("{p1:?} + {p2:?} = {p3:?}");
}
```

Rust에서 borrow 제약 조건

어떤 값(T)에 대해
- 동시에 하나 이상의 `&T` 값들 혹은
- 동시에 하나의 `&mut T` 값
만 가질 수 있다. (위 두 조건은 mutual exclusive)

```rust
fn main() {
    let mut a: i32 = 10;
    let b: &i32 = &a;
    
    // println!("b: {b}"); // 아래 print문을 위로 옮기면 b는 c가 존재하는 시점에 useless 하다는 것을 컴파일러가 알기때문에 에러 없음. 
    {
        let c: &mut i32 = &mut a;
        *c = 20;
    }

    println!("a: {a}");
    println!("b: {b}"); // compile error! c가 mut a를 빌려갔기 때문에 규칙에 위배!
}
```

빌려온 값은 수명이 있다.
- 수명은 생략될 수 있음.
- 명시할 수도 있음(`&'a Point`)
- `&'a Point`는 최소 a의 수명만큼 유효한 빌려온 Point라고 해석.
- 수명은 항상 컴파일러에 의해 추론되고, 직접 할당할 수 없음(할당과 명시는 다름).
- 수명은 제약 조건을 생성하며, 컴파일러가 유효한 솔루션을 확인한다. 


## Resources
[[-]] [Comprehensive rust](https://github.com/google/comprehensive-rust)
- [파이썬 개발자를 위한 Rust](https://indosaram.github.io/rust-python-book/)

