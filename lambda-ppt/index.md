---
theme: uncover
marp: true
style: |
    .columns {
        display: grid;
        grid-template-columns: repeat(2, minmax(0, 1fr));
        gap: 1rem;
    }
    fieldset {
        border: 2px solid black;
    }
    @font-face {
        font-family: 'Freesentation';
        src: url('https://fastly.jsdelivr.net/gh/projectnoonnu/2404@1.0/Freesentation-4Regular.woff2') format('woff2');
        font-weight: 400;
        font-style: normal;
    }
    @font-face {
        font-family: 'Freesentation';
        src: url('https://fastly.jsdelivr.net/gh/projectnoonnu/2404@1.0/Freesentation-7Bold.woff2') format('woff2');
        font-weight: 700;
        font-style: bold;
    }
    section {
        display: flex;
        flex-direction: column;
    }
    section * {
        font-family: 'Freesentation', sans-serif;
    }
    section .body {
        flex-grow: 100;
        display: flex;
        flex-direction: column;
        justify-content: center;
    }
    .muted {
        opacity: 0.7;
    }
    .size {
        font-size: var(--size);
    }
    .all-center {
        display: grid;
        place-items: center;
    }
    .hide-bullet ul {
        list-style: none;
        padding-left: unset;
    }
    .rm-p-margin p {
        margin-bottom: 0;
    }
    .white img {
        filter: invert(1);
    }
---

# <!--fit-->&lambda;-Calculus - 연산의 구현

<small> by 10315 이도이 </small>

---

<!--paginate: true-->
<!--footer: <span class="muted"><strong>&lambda;-Calculus - 연산의 구현</strong></span>-->
<!--header: <span class="muted">λ-Calculus, 람다 대수란?</span>-->


# &lambda;-Calculus, 람다 대수란?

**: 기반적인 함수적 이론**
아래의 <u>**문법과 연산만으로**</u> 모든 수학적, 컴퓨터적 연산을 구현할 수 있다.

<div class="body">

<br/>

<div class="columns">

<fieldset>
<legend>문법</legend>

1. **변수**
2. **&lambda;-Abstraction(람다 추상화)**
3. **적용**
 
</fieldset>

<fieldset>
<legend>연산</legend>

1. **$\alpha$-conversion($\alpha$-변환)**
2. **$\beta$-reduction($\beta$-축약)**

</fieldset>
</div>
</div>


---

## 문법

<div class="body">

1. $x$ : **변수**, 함수에서 쓰이는 매계변수를 표현
<br/>
2. $(\lambda x . M[x])$ : **람다 추상화**, 함수를 정의. $x$를 변수로 받아서 $M[x]$을 반환
    <span class="muted">＊$M[x]$: $x$를 포함하는 식 $M$</span>

3. $(\lambda x . M[x]) N$ : **적용**, $M$에 $N$을 적용 (이후 $\beta$-축약으로 이용)

</div>

---

## 연산

<div class="body">

1. $(\lambda x.M[x]) \longrightarrow (\lambda y.M[y])$ : **$\alpha$-conversion($\alpha$-변환)**,
    이때 $(\lambda x.M[x])$, $(\lambda y.M[y])$를 **$\alpha$-equivalent($\alpha$-동치)** 라고 함
<br/>

2. $(\lambda x.M[x])N \longrightarrow_{\beta} M[x:=N]$ : **$\beta$-reduction($\beta$-축약)**, $M$의 $x$를 $N$으로 대체

</div>

---

## 예시

<div class="body">
<div class="columns">
<div class="all-center size" style="--size: 2em;">

$x \longmapsto x^2$

$\Downarrow$

$\lambda x.x^2$

<span class="muted size" style="--size: 0.5em;">＊$\lambda x.x^2 \Longleftrightarrow_{\alpha} \lambda y.y^2$</span>

</div>
<div class="all-center">

$$
\begin{align}

& (\lambda x.\underbrace{x^2}_{M[x]})\,\underbrace{3}_{N}\rightarrow_{\beta} (x^2)\,[x:=3]\\\\
& = \underbrace{3 ^ 2}_{M[x:=3]}  \\\\
& = 9

\end{align}
$$

</div>
</div>
</div>

---

## 변수가 2개 이상인 람다 함수

***함수를 값으로써 반환 가능함** 

$f(x,y)=x+y \Longrightarrow \lambda x.\lambda y.x+y$

<div class="body">

<div class="hide-bullet">



* $\quad\underline{(\lambda x. \lambda y. x + y)\,3}\, 4$
* $= ((\lambda x. \lambda y. x + y)\, 3)\, 4 \rightarrow_{\beta} (\lambda y. x + y)\,4\, [x:=3]\\$ 
* $= \underline{(\lambda y. 3 + y)}\, 4 \rightarrow_{\beta} (3+y)[y:=4]$
* $= 3 + 4$
    $= 7$

</div>
</div>
</div>

---

<!--
이제 함수 그 차제가 값으로 반환 될 수 있다는 사실을 알게 되었으니,
더욱 심화 단계의 람다 대수에 진입할 수 있습니다.


-->

# Church Numeral - 숫자의 구현

<div class="body">
<div class="columns">
<div class="all-center">

$$
\begin{align}
\overline{n} & = \lambda f. \lambda x. f^n \ x \quad (n \in \mathbb{N}\cup\{0\})\\
& = \lambda f. \lambda x. \underbrace{f\,f\,f\,...\,f}_{n} \,x \\
\end{align}
$$

</div>

<div class="hide-bullet">

* 
    <div class="all-center">
    
    $$
    \begin{align}
    & \overline{0} = \lambda f. \lambda x. f^0 \ x = \lambda f. \lambda x.x \\
    \\
    & \overline{1} = \lambda f. \lambda x. f^1 \ x = \lambda f. \lambda x.\underbrace{f}_{1}\ x \\
    & \overline{2} = \lambda f. \lambda x. f^2 \ x = \lambda f. \lambda x.\underbrace{f\ f}_{2}\ x \\
    \end{align}
    $$
    $\vdots$</div>

</div>

</div>
</div>

[:arrow_backward: Slide 2](#2)

---

## 더하기

<div class="body">
<div class="columns">
<div class="all-center">

처치 숫자에 $\overline{1}$을 더하는 함수인 $\text{SUCC}$<small>(successor)</small>

<div class="rm-p-margin all-center">

$\text{SUCC}(n) = n+1$

$\Downarrow$

$\text{SUCC} := \lambda n. \lambda f. \lambda x.f\ (n\ f\ x)$

</div>
</div>

<div class="hide-bullet">

*
    $\text{SUCC}$를 이용해 $\overline{0}+\overline{1}=\overline{1
    }$ 을 계산
    $$
    \begin{align}
    & \text{SUCC}\ \overline{0} \qquad (\overline{0} := \lambda f. \lambda x.x \Leftrightarrow_{\alpha} \lambda p. \lambda q.q)\\\\
    & = \big(\lambda n. \lambda f. \lambda x.f\ (n\ f\ x)\big)\ \overline{0} \rightarrow_{\beta}\ \lambda f. \lambda x.f\ (\overline{0}\ f\ x) \\\\
    & = \lambda f. \lambda x.f\ (\underbrace{(\lambda p. \lambda q.q)}_{\overline{0}}\ f\ x) \rightarrow_{\beta}\ \lambda f. \lambda x.f\ x \\
    & = \overline{1}
    \end{align}
    $$

</div>
</div>
</div>

---

## 더하기

<div class="body">
<div class="columns">
<div class="all-center">

$\text{SUCC}$를 이용해 $\text{{ADD}}$<small>(addition)</small>을 구현

<div class="rm-p-margin all-center">

$\text{ADD}(x, y) = x+y$

$\Downarrow$

$\text{ADD} := \lambda x. \lambda y. x\ \text{SUCC}\ y$

</div>

</div>
<div class="hide-bullet">

*
    $\text{ADD}$을 이용해 $\overline{2}+\overline{3}=\overline{5}$를 계산
    $$
    \begin{align}
    & \text{ADD}\,\overline{2}\,\overline{3} \\
    & = \big(\lambda x. \lambda y. x\ \text{SUCC}\ y\big)\ \overline{2}\,\overline{3}\rightarrow_{\beta}\ \overline{2}\,
    \text{SUCC}\ \overline{3} \\
    & = \big(\lambda f. \lambda x. f^2 \ x\big)\ \text{SUCC}\ \overline{3} \rightarrow_{\beta}\ \text{SUCC}^2\ \overline{3} \\
    & = \overline{3} + 1 + 1 \\
    & = \overline{5}
    \end{align}
    $$

</div>
</div>
</div>

---

## 곱하기

<div class="body">
<div class="columns">
<div class="all-center">

$\text{ADD}$를 이용해 $\text{MULT}$<small>(multiplication)</small>을 구현

<div class="rm-p-margin all-center">

$\text{MULT}(x, y) = x\times y$

$\Downarrow$

$\text{MULT} := \lambda x. \lambda y. x\ (ADD\ y)\,\overline{0}$

</div>

</div>
<div class="hide-bullet">

*
    $\text{MULT}$을 이용해 $\overline{2}\times \overline{3}=\overline{6}$을 계산
    $$
    \begin{align}
    & \text{MULT}\ \overline{2}\,\overline{3} \\
    & = \big(\lambda x. \lambda y. x\ (ADD\ y)\ \overline{0}\big)\ \overline{2}\,\overline{3} \rightarrow_{\beta}\ \overline{2}\ (\text{ADD}\ \overline{3})\ \overline{0} \\
    & = \big(\lambda f. \lambda x. f^2 \ x\big)\ (\text{ADD}\ \overline{3})\ \overline{0} \rightarrow_{\beta}\ (\text{ADD}\ 3)^2\ \overline{0} \\
    & = (\text{ADD}\ \overline{3})\ (\text{ADD}\ \overline{3})\ \overline{0} \\
    & = \overline{0} + \overline{3} + \overline{3} \\
    & = \overline{6}
    \end{align}
    $$

</div>
</div>
</div>

---

<!--header: <span class="muted">Church Numeral - 숫자의 구현</span>-->
## 이외의 연산

앞과 비슷한 방법으로 아래의 연산을 구현

<div class="body">

* $\text{PRED}$<small>(predecessor)</small>: $-1$ 연산 함수
<br/>
* $\text{SUB}$<small>(subtraction)</small>: 빼기 연산 함수
    <span class="muted">＊처치 숫자의 구현 범위가 $\mathbb{N}\cup\{0\}$이므로 값의 결과가 음수면 처치 숫자에서는 $0$이 됨.<span>
<br/>    
* $\text{DIV}$<small>(division)</small>: 나누기 연산 함수

</div>


---

<!--header: <span class="muted">진리 연산</span>-->
# 진리 연산

<div class="body">

$$
\begin{align}
\text{True} := \lambda x.\lambda y.x \\\\
\text{False} := \lambda x.\lambda y.y
\end{align}
$$

</div>

[:arrow_backward: Slide 7](#7)

---

## $\text{AND}(\land)$

<div class="body">
<div class="columns">
<div>

$$
\text{AND} := \lambda x. \lambda y. x\ y\ x
$$
<br/>

|      $x$       |      $y$       |   $x\land y$   | $\text{AND} \ x\  y$ |
| :------------: | :------------: | :------------: | :------------------: |
| $\text{False}$ | $\text{False}$ | $\text{False}$ | $\text{False}$       |
| $\text{False}$ | $\text{True}$  | $\text{False}$ | $\text{False}$       |
| $\text{True}$  | $\text{False}$ | $\text{False}$ | $\text{False}$       |
| $\text{True}$  | $\text{True}$  | $\text{True}$  | $\text{True}$        |
</div>

<div class="hide-bullet">

*
    <div class="all-center">

    **두번째 행 예시**
    <br/>

    $$
    \begin{align}
    & \text{AND} \ \text{False}\  \text{True} \\
    & = (\lambda x. \lambda y. x\ y\ x) \ \text{False}\  \text{True} \\
    & \rightarrow_{\beta}\  \text{False}\ \text{True}\ \text{False}  \\
    & = \underbrace{(\lambda x.\lambda y.y)}_{\text{False}}\ \text{True}\ \text{False} \\
    & \rightarrow_{\beta}\ \text{False}
    \end{align}
    $$

    </div>

</div>

</div>
</div>

---

## $\text{OR}(\lor)$, $\text{NOT}(\lnot)$

<div class="body">

$$
\begin{align}
& \text{OR} := \lambda x. \lambda y. x\ x\ y \\
\\
& \text{NOT} := \lambda x. x\ \text{False}\ \text{True}
\end{align}
$$

</div>

---

## $\text{IF}$

$\text{IF}:=\lambda c. \lambda x. \lambda y. c\ x\ y$ 
    **:** $c$ 는 조건, $x$ 는 참일때($\text{if}$) 실행, $y$ 는 거짓일때($\text{else}$) 실행

<div class="body">

**$c$ 가 참일때 1을, 거짓일때 2를 뱉는 함수**

<div class="columns">

$$
\begin{align}
& \text{IF}\,c\,1\,2 \\
& = (\lambda c. \lambda x. \lambda y. c\ x\ y)\,c\,1\,2 \\
\end{align}
$$
</div>

<div class="columns">
<div class="hide-bullet">

*
    $$
    \begin{align}
    & \text{i)}\,c=\text{True} \\
    & (\lambda c. \lambda x. \lambda y. c\ x\ y)\,\text{True}\,1\,2 \\
    & \rightarrow_{\beta}\,\text{True}\,1\,2\,\rightarrow_{\beta}\,1 \\
    \end{align}
    $$

</div>

<div class="hide-bullet">

*
    $$
    \begin{align}
    & \text{ii)}\,c=\text{False} \\
    & (\lambda c. \lambda x. \lambda y. c\ x\ y)\,\text{False}\,1\,2 \\
    & \rightarrow_{\beta}\,\text{False}\,1\,2\,\rightarrow_{\beta}\,2 \\
    \end{align}
    $$

</div>
</div>
</div>

---

<!--
두 처치 숫자가 같거나 한쪽이 큰지 알려면 한쪽에서 다른 한쪽을 뺀 뒤 $\text{IsZero}$ 함수로 연산하여 알 수 있다.
-->

## $\text{IsZero}$

$\text{IsZero} := \lambda x.x\ (\lambda y.\text{False})\ \text{True}$

<div class="body">
<div class="columns">
<div class="hide-bullet">

*
    $$
    \begin{align}
    & \text{IsZero}\ \overline{0} \\
    & = \big(\lambda x.x\ (\lambda y.\text{False})\ \text{True}\big)\ \overline{0} \\
    & \rightarrow_{\beta}\ \overline{0}\ (\lambda y.\text{False})\ \text{True}\ [\overline{0}:=\lambda f. \lambda x.x] \\
    & = (\lambda f. \lambda x.x)\ (\lambda y.\text{False})\ \text{True} \\
    & \rightarrow_{\beta}\ \text{True}
    \end{align}
    $$

</div>

<div class="hide-bullet">

*
    $$
    \begin{align}
    & \text{IsZero}\ \overline{1} \\
    & = \big(\lambda x.x\ (\lambda y.\text{False})\ \text{True}\big)\ \overline{1} \\
    & \rightarrow_{\beta}\ \overline{1}\ (\lambda y.\text{False})\ \text{True}\ [\overline{1}:=\lambda f. \lambda x.f\ x] \\
    & = (\lambda f. \lambda x.f\ x)\ (\lambda y.\text{False})\ \text{True} \\
    & \rightarrow_{\beta}\ (\lambda y.\text{False})\ \text{True} \\
    & \rightarrow_{\beta}\ \text{Fasle}
    \end{align}
    $$

</div>
</div>
</div>

---

<!--
알파-동치에 의해 처음 식과 베타-축약의 결과가 같으므로, 위 람다 항은 무한히 반복된다.
하지만, 위 루프는 실제로 사용할 쓸모가 없다. 단순 반복 이외에 다른 기능을 하지 못하기 때문이다.
-->

<!--header: <span class="muted">LOOP, 반복 연산</span>-->
# LOOP, 반복 연산

가장 기본적인 루프(반복문) **:** $\lambda x. (\lambda y. x\ x)\ (\lambda y. x\ x)$

<div class="body">
<div class="all-center">

$$
\begin{align}
& \lambda x. (\lambda y. x\ x)\ (\lambda y. x\ x) \Leftrightarrow_{\alpha}\ \lambda x. (\lambda y. x\ x)\ (\lambda z. x\ x)\\
& \rightarrow_{\beta}\ \lambda y. (\lambda z. x\ x)\ (\lambda z. x\ x) \\\\
& \lambda x. (\lambda y. x\ x)\ (\lambda y. x\ x) \Leftrightarrow_{\alpha}\ \lambda y. (\lambda z. x\ x)\ (\lambda z. x\ x)
\end{align}
$$

</div>
</div>

---

## $\text{Y}$-Combinator

$\text{Y} =\lambda f. (\lambda x.f(x\ x))\ (\lambda x.f(x\ x))$

<div class="body">

람다 함수 $g$를 $\text{Y}$에 대입
$$
\begin{align}
& \text{Y}\ g \\ 
& = \big(\lambda f. \big(\lambda x.f(x\ x)\big)\ \big(\lambda x.f(x\ x)\big)\big)\ g \rightarrow_{\beta}\ \big(\lambda x.g(x\ x)\big)\ \big(\lambda x.g(x\ x)\big) \\
& \rightarrow_{\beta}\ g\big(\big(\lambda x.g(x\ x)\big)\ \big(\lambda x.g(x\ x)\big)\big) \\
& = g\ (\text{Y}\ g) \\
& = g\ (g\,(\text{Y}\ g)) \\
& \qquad \vdots
\end{align}
$$

</div>

---

## Factorial, 계승

<div class="body">
<div class="all-center">

$$
\text{Fac}(n) =
\begin{cases}
1 & (n=0)\\
n\times \text{Fac}(n-1) & (n>0)
\end{cases}
$$
$\Downarrow$
$$
\begin{align}
\text{Fac} := \text{Y}\ \big(\lambda f. \lambda n.\text{IF}\ (\text{IsZero}\ n)\ 1\ (\text{Mult}\ n\ (f\ (\text{Pred}\ n)))\big)
\end{align}
$$

</div>
</div>

[:arrow_backward: Slide 11](#11)

---

<!--header: "마치면서..."-->
# 마무리

<div class="body">
<small>

합성함수에 관해 수학시간에 배우게 되었다. 나의 꿈인 프로그래밍과 관련된 컴퓨터 토픽과 함수와 관련한 내용을 탐구하던 와중, 람다 대수에 관해 알게되었고, 그중에서도 합성 함수와 비슷한 개념으로 숫자와 진리 값 등을 정의하는 등 흥미로운 부분이 많아서 
이렇게 발표하게 되었다.
고1에 들어오면서 조각적 정의로 쓰여진 함수등 복잡한 함수가 많아졌는데,
 람다 대수를 탐구하며 함수에 관련한 이해가 늘어난 것 같다.

## 출처

- WIKIPEDIA, Lambda Calculus
- Barendregt, Hendrik Pieter, Introduction to Lambda Calculus
- Cardone, Felice and Hindley, J. Roger, History of Lambda-calculus and Combinatory Logic
- Raúl Rojas, A Tutorial Introduction to the Lambda Calculus

</small>

</div>

---

<!--_paginate: skip-->
<!--_backgroundColor: black-->

# <!--fit-->&lambda;-Calculus

by 10315 이도이 <span class="white"></span>