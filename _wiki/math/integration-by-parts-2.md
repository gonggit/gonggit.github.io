---
layout  : wiki
title   : 부분적분 2 
summary : 
date    : 2025-04-07 23:47:16 +0900
updated : 2025-04-07 23:51:25 +0900
tag     : 적분,부분적분,integration  
resource: F6/284968-EAFF-4D41-BE40-A79C634F07F2
toc     : true
public  : true
parent  : [[/math]] 
latex   : true 
---
* TOC
{:toc}


부분적분 예제 정리.

---

## 예제 1. $$ \int x \cos x \, dx $$

$$
u = x,\quad dv = \cos x \, dx \\
du = dx,\quad v = \sin x
$$

$$
\int x \cos x \, dx = x \sin x - \int \sin x \, dx \\
= x \sin x + \cos x + C
$$

---

## 예제 2. $$ \int x^2 e^x \, dx $$

반복 적용 필요.

### 1차 적용:

$$
u = x^2,\quad dv = e^x \, dx \\
du = 2x \, dx,\quad v = e^x
$$

$$
\int x^2 e^x \, dx = x^2 e^x - \int 2x e^x \, dx
$$

### 2차 적용:

$$
u = 2x,\quad dv = e^x \, dx \\
du = 2 \, dx,\quad v = e^x
$$

$$
\int 2x e^x \, dx = 2x e^x - \int 2 e^x \, dx = 2x e^x - 2e^x
$$

최종 정리:

$$
\int x^2 e^x \, dx = x^2 e^x - 2x e^x + 2e^x + C
$$

---

## 예제 3. 수능 기출 변형 – $$ \int \ln x \, dx $$

표면적으로는 곱 형태가 아니지만, 다음처럼 처리:

$$
\int \ln x \cdot 1 \, dx
$$

$$
u = \ln x,\quad dv = dx \\
du = \frac{1}{x} dx,\quad v = x
$$

$$
\int \ln x \, dx = x \ln x - \int x \cdot \frac{1}{x} dx = x \ln x - \int 1 \, dx = x \ln x - x + C
$$

---

## 메모

- $$ \int x^n e^x \, dx $$ 꼴은 n만큼 반복 적용
- $$ \int \ln x \, dx $$ 같은 로그 단독 적분도 부분적분 활용
- 근데 손으로 직접 써보지 않으면 또 금방 까먹을거 같다
