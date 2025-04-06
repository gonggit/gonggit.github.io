---
layout  : wiki
title   : 부분적분 1
summary : 매번 생각이 안나는 
date    : 2025-04-06 23:32:36 +0900
updated : 2025-04-07 00:00:26 +0900
tag     : 적분,부분적분 
resource: 80/020229-39B1-49ED-9CC7-33DEFCCC240A
toc     : true
public  : true
parent  : [[/math]] 
latex   : true
comment : true
---
* TOC
{:toc}


# 부분적분법
두 함수의 곱 형태 적분에서 사용하는 방법.  
기본 공식:

$$
\int u \, dv = uv - \int v \, du
$$

---

## 적용 조건

- 적분 대상이 두 함수의 곱 형태
- u는 미분하면 단순해지는 함수
- dv는 적분이 가능한 함수

---

## 예제 1

$$
\int x e^x \, dx
$$

- $$ u = x $$, $$ dv = e^x dx $$ 
- $$ du = dx $$, $$ v = e^x $$ 

공식에 대입:

$$
\int x e^x \, dx = x e^x - \int e^x dx = x e^x - e^x + C
$$

---

## u 선택 기준 (LIATE 순서)

1. Logarithmic – $$ \ln x $$
2. Inverse trig – $$ \arctan x $$, $$ \arcsin x $$ 등
3. Algebraic – $$ x, x^2 $$ 등
4. Trig – $$ \sin x, \cos x $$ 등
5. Exponential – $$ e^x $$, $$ a^x $$ 등

위에 있을수록 u로 먼저 선택.

---

## 예제 2

$$
\int x \ln x \, dx
$$

- $$ u = \ln x $$, $$ dv = x dx $$
- $$ du = \frac{1}{x} dx $$, $$ v = \frac{1}{2}x^2 $$

공식에 대입:

$$
= \ln x \cdot \frac{1}{2}x^2 - \int \frac{1}{2}x^2 \cdot \frac{1}{x} dx \\
= \frac{1}{2}x^2 \ln x - \frac{1}{2} \int x \, dx \\
= \frac{1}{2}x^2 \ln x - \frac{1}{4}x^2 + C
$$

---

## 메모

- 곱 형태가 아니더라도 강제로 곱처럼 만들어서 쓰는 경우도 있음 (ex: $$ \int \ln x \, dx $$)
- 반복 적용이 필요한 경우도 있음 (ex: $$ \int x^2 e^x dx $$)
- u, v를 정하는 방법을 항상 잊어버린다.
