---
layout  : wiki
title   : Rust 배워보기 (1) 
summary :  
date    : 2023-03-07 16:49:03 +0900
updated : 2023-03-07 22:27:50 +0900
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

그리고 어째선지 내가 즐겨 보는 블로그들에서 Rust를 소개하는 글들이 많아졌는데, .

## Day 1

## 들어가기 전에 
Rust 공부를 시작하면 Cargo를 만나게 된다. Rust Ecosystem에서 Rust 어플리케이션을 빌드하고 실행하는 표준 도구다. 여기서 Rust Ecosystem은 몇 가지 툴로 이루어져있는데, `rustc` 라는 Rust 컴파일러와 dependency manager인 `cargo`, Rust toolchain installer & updater인 `rustup` 이다.

## Rust?
Rust는 2015년에 1.0 버전을 출시한 새로운 프로그래밍 언어다. Rust는..

- C++와 비슷한 역할을 하는 정적 컴파일 언어.
- LLVM을 백엔드로 사용한다.
- 다양한 플랫폼과 아키테거를 지원한다.
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


### Resources
- [Comprehensive rust](https://github.com/google/comprehensive-rust)
- [파이썬 개발자를 위한 Rust](https://indosaram.github.io/rust-python-book/)

