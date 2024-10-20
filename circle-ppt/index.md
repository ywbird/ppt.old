---
marp: true
theme: uncover
math: latex
style: |
    .columns {
        display: grid;
        grid-template-columns: repeat(2, minmax(0, 1fr));
        gap: 1.5rem;
    }
    .all-center {
        display: grid;
        place-items: center;
    }
    @font-face {
    font-family: 'Cafe24Ssurround';
    src: url('https://fastly.jsdelivr.net/gh/projectnoonnu/noonfonts_2105_2@1.0/Cafe24Ssurround.woff') format('woff');
    font-weight: normal;
    font-style: normal;
    }
    .title {
        font-family: 'Cafe24Ssurround', san-serif;
        font-weight: 400;
        display: inline-block;
    }
    h1 {
        padding-inline: 3rem;
        padding-block: 0.1rem;
    }
    h1,h2,h3,h4 {
    font-family: "Black Han Sans", sans-serif;
    font-weight: 400;
    font-style: normal;
    }
    .rainbow {
        background: linear-gradient(270deg, rgb(221, 2, 3) 0.00%, rgb(251, 137, 2) 20.00%, rgb(248, 235, 5) 40.00%, rgb(0, 127, 38) 60.00%, rgb(5, 75, 249) 80.00%, rgb(114, 6, 130) 100.00%);
                -webkit-background-clip: text;
                background-clip: text;
                color: transparent;
        font-weight: bold;
    }
---

<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Black+Han+Sans&display=swap" rel="stylesheet">


# <span class="rainbow title"><!--fit-->동글동글</span>

## - 원의 방정식의 다양한 표현 방법 -

by $10315$이도이, $10303$곽대호

---

## 원의 방정식의 표준형


<div class="columns" >

<div>
    
**중심 $C(a,b)$, 반지름 $r$**
<br/>
- 표준형 :
    $(x-a)^2+(y-b)^2=r^2$
    <br/>
- 일반형 :
    $x^2+y^2+Ax+By+C=0$

</div>

<iframe src="https://www.desmos.com/calculator/6efspejoab?embed" width="500" height="500" style="border: 1px solid #ccc" frameborder=0></iframe>

</div>

---

## 함수 꼴의 원의 방정식

<div class="columns" >

<div>

**중심 $C(a,b)$, 반지름 $r$**
<br/>

- $y$에 대해정리 $\rightarrow$ $y=f(x)$

<br/>

$f(x)=\pm\sqrt{r^2-(x-a)^2}+b$

</div>

<!--DESMOS 함수꼴 원방-->
<iframe src="https://www.desmos.com/calculator/uil4iud31t?embed" width="500" height="500" style="border: 1px solid #ccc" frameborder=0></iframe>

</div>

---

## 삼각비를 이용한 원의 방정식


<div class="columns" >

<div>

<small>$\cos\theta$, $\sin\theta$ 형태로 표현</small>

<div class="all-center">

1) $x=a+r\cos\theta$
    $y=b+r\sin\theta$

2) $t\equiv\tan\frac{\theta}{2}$ 일때,

3) $x=a+r(\frac{1-t^2}{1+t^2})$
    $y=b+r(\frac{2t}{1+t^2})$

</div>

</div>

<iframe src="https://www.desmos.com/calculator/llj5nczktr?embed" width="500" height="500" style="border: 1px solid #ccc" frameborder=0></iframe>

</div>

---

## 극좌표계를 이용한 원의 방정식

<div class="columns">

<div>

 **극좌표계란?**
 
 - 원점으로부터의 거리($r$)
 - $x$축에 대한 각($\theta$)
<br/>
 - $(r,\theta)$로 표현

</div>

<!--DESMOS 이미지 넣기-->
<iframe src="https://www.desmos.com/calculator/ar5gzfdf56?embed" width="500" height="500" style="border: 1px solid #ccc" frameborder=0></iframe>

</div>

---

### 극좌표계 변환

* 데카르트 좌표계(평면좌표) $\rightarrow$ 극좌표계
    
    $D(A)=(\sqrt{A.x^2+A.y^2},\arctan(\frac{A.y}{A.x}))$
<br/>
* 극좌표계 $\rightarrow$ 데카르트 좌표계(평면좌표)
    
    $P(A)=(A.x\cdot \cos(A.y),A.x\cdot \sin(A.y))$

---

### 극좌표계에서의 원

<div class="columns">

<div class="all-center">

**원의 중심 : $O(0,0)$**

$$
r=1
$$

</div>

<!--DESMOS 극좌표계 원-->
<iframe src="https://www.desmos.com/calculator/dy4pntuih3?embed" width="500" height="500" style="border: 1px solid #ccc" frameborder=0></iframe>


</div>

---

### 극좌표계에서의 원

<div class="columns">

<div class="all-center">

**중심 : $(r_1,\theta_1)$, 반지름 : $r$**

 - [$\cos$ 법칙](#9)을 사용

$$
r^2=r_0^2+r_1^2-2r_1r_0\cos(\theta-\theta_1)
$$

</div>

<iframe src="https://www.desmos.com/calculator/ogg9spxliu?embed" width="500" height="500" style="border: 1px solid #ccc" frameborder=0></iframe>

</div>

---

### $\cos$ 법칙이란?

<div class="columns">
<div align="left">


<div>

<span align="center">$\overline{AH} = c\sin B$</span>
<span align="center">$\overline{HC} = a - c\cos B$</span>
<span align="center">$\overline{AC} = b$</span>


</div>

<div align="left">

$$
\begin{equation}
\begin{aligned}
b^2 &= (c\sin B)^2 + (a - c\cos B)^2 \\
    &= c^2 \sin^2 B+ c^2  \cos^2 B  +a^2-2ac\cos B \\
    &= c^2 ( \sin^2 B+ \cos^2 B ) +a^2-2ac\cos B
\end{aligned}
\end{equation}
$$

</div>

<br/>

$\therefore b^2 = c^2+a^2-2ac\cos B$
$(\because \sin^2 B+ \cos^2 B=1)$

</div>

<iframe src="https://www.desmos.com/calculator/2plpidfimm?embed" width="500" height="500" style="border: 1px solid #ccc" frameborder=0></iframe>

</div>


---

# 마무리

<div class="columns">

<div class="all-center">

사용 도구 : Desmos

PPT : <span class="rainbow">이도이</span>

발표 : <span class="rainbow">곽대호</span>

</div>

<iframe src="https://www.desmos.com/calculator/phshrg2sne?embed" width="500" height="500" style="border: 1px solid #ccc" frameborder=0></iframe>

</div>
