---
marp: true
theme: uncover
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
---



# <!--fit-->&lambda;-Calculus - 연산의 구현

<small> by 10315 이도이 </small>

---

<!--paginate: true-->
<!--footer: <span class="muted">&lambda;-Calculus - 연산의 구현</span>-->

# &lambda;-Calculus, 람다 대수란?

**: 기반적인 함수적 이론**

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

1. $\alpha$-conversion($\alpha$-변환)
2. $\beta$-reduction($\beta$-축약)

</fieldset>

</div>
</div>

---

# 문법

<div class="body">

1. $x$ : **변수**, 함수에서 쓰이는 매계변수를 표현

2. $(\lambda x . M[x])$ : **람다 추상화**, 함수를 정의. $x$를 변수로 받아서 $M[x]$을 반환
    <span class="muted">＊$M[x]$: $x$를 포함하는 식 $M$</span>

3. $(\lambda x . M[x]) N$ : **적용**, $M$에 $N$을 적용 (이후 $\beta$-축약으로 이용)

</div>

---

# 연산

<div class="body">

1. $(\lambda x.M[x]) \longrightarrow (\lambda y.M[y])$ : **$\alpha$-conversion($\alpha$-변환)**,
    이때 $(\lambda x.M[x])$, $(\lambda y.M[y])$를 **$\alpha$-equivalent($\alpha$-동치)** 라고 함
<br/>

2. $(\lambda x.M[x])N \longrightarrow M[x:=N]$ : **$\beta$-reduction($\beta$-축약)**, $M$의 $x$를 $N$으로 대체

</div>

---

# 예시

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

& (\lambda x.x^2)\space3 \rightarrow_{\beta} (x^2)[x:=3]\\
& = 3 ^ 2 \\
& = 9

\end{align}
$$

</div>
</div>
</div>

---

# 변수가 2개 이상인 람다 함수

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