---
marp: true
style: |
  .columns {
      display: grid;
      grid-template-columns: repeat(2, minmax(0, 1fr));
      gap: 1rem;
  }
  .rows {
      display: grid;
      grid-template-rows: repeat(2, minmax(0, 1fr));
      gap: 1rem;
  }
  fieldset {
      border: 2px solid black;
  }
  @font-face {
      font-family: 'Freesentation';
      src: url('https://fastly.jsdelivr.net/gh/projectnoonnu/2404@1.0/Freesentation-4Regular.woff2') format('woff2');
      font-weight: 300;
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
  .smaller {
      font-size: 0.5em;
  }
  .all-center {
      display: grid;
      place-items: center;
  }
  .hide-bullet * ul {
      list-style: none;
      padding-left: unset;
  }
  .rm-p-margin p {
      margin-bottom: 0;
  }
  .morph {
      display: inline-block;
      view-transition-name: var(--morph-name);
      contain: layout;
      vertical-align: top;
  }
  img {
    display: block;
    object-fit: contain;
    background-color: transparent;
  }
  .scroll {
    display: block;
    overflow-y: scroll;
    height: 100%;
    background-color: transparent;
    width: fit-content;
  }
---

# <!--fit-->인류의 집단생활의 원인 탐구, <br/>시뮬레이션 프로그래밍을 통한 분석

by 10315 이도이

---

## 이전 연구

**<인류 집단생활 원인에 대한 가설, 모델을 통한 시뮬레이션으로 검증하기>**

<div class="body">
<div class="columns">
<div class="scroll smaller">

구현

1.  피식자와 포식자는 최초에 개체 수만큼 생성되며, 난수를 생성하여 개체의 비율에 비교해 포식자와 피식자를 정하고, 환경의 랜덤한 위치, 랜덤한 방향을 바라본다. 각 피식자는 0.0~0.5의 난수 값의 공격력을 갖고, 포식자는 0.5~1.0의 난수 값의 공격력을 갖는다.
2.  모든 개체는 자신이 바라보는 방향으로 초당 개체의 이동속도만큼 이동한다.
3.  모든 개체는 자신의 상호작용 범위 내에 있는 동족의 개체와 멀어지는 방향으로 자신의 방향을 조정한다.
4.  포식자는 개체 공격 쿨다운 만큼 시간이 지난 후, 포식 활동을 한다.
5.  포식자는 포식 활동을 할 때 가장 가까운 피식자의 방향으로 조향한다.
6.  피식자는 인식 범위 내에 있는 가장 가까운 포식자로부터 멀어지는 방향으로 조향한다.
7.  피식자는 공격 쿨다운이 0인 포식자와 접촉했을 때, 인식 범위 내에 있는 동족(피식자)의 공격력을 총합해서 포식자와 비교한다. 만약 공격력의 총합이 포식자의 것보다 크다면 포식자는 죽고 반대라면 접촉한 피식자는 죽는다.
8.  (1.) 아래의 단계를 한 종류의 종족만 남을 때까지 반복한다.


</div>
<div class="all-center">

<img height="430px" src="./assets/prev-sim.gif"/>

</div>
</div>
</div>

---

## 이전 연구

**<인류 집단생활 원인에 대한 가설, 모델을 통한 시뮬레이션으로 검증하기>**

<div class="body">
<div class="columns">
<div class="size" style="--size: .9em;">

문제점

- 개체 모델링이 미흡 $\rightarrow$ 특정 종의 승률이 $0\%$, 분석 X
- 개체 간 교배 X $\rightarrow$ 유전적 차이 X $\rightarrow$ 연구 목적과 괴리
- 시뮬레이션 자연환경 X
- 프로그래밍 언어의 성능 문제  $\downarrow$

</div>
<div class="all-center">

<img height="430px" src="./assets/prev-result.png"/>

</div>
</div>
</div>

---

### 이전 연구 - Source Code

<div class="scroll">

<script src="https://gist.github.com/ywbird/f3d7fbfa56f5560c643b9753032c2262.js"></script>

</div>

---

## 핵심 기능 - QuadTree

<div class="body">
<div class="columns">
<div class="">
  
정의

- 공간을 $4$개의 하위 노드(셀)로 분해 $\rightarrow$ 버킷(셀)
- 각 버킷(셀)에 최대 용량이 존재 (이 경우 $4$)
- 트리 구조의 공간 분해

이점

- 더욱 효율적인 공간 탐색
  $100 * 100 \rightarrow 100 * n$

</div>
<div>
  
<video height="470px" src="./assets/quad-tree.webm" type="video/webm" controls />

</div>
</div>
</div>

---

### QuadTree - Source Code

<div class="scroll">

<script src="https://gist.github.com/ywbird/9ebaad98e2385b8f954a87548d5ee0a0.js"></script>

</div>

---

## 시뮬레이션 구현

<div class="body">
<div class="columns">
<div class="all-center size" style="--size: .9em;">

- 매 프레임마타 QuadTree 새로 구축
- 매 개체마다 자신 주위 개체를 QuadTree로 부터 얻음
- 피식자(파랑)은 먹이로 향해서 먹이를 먹음
- 포식자(빨강)은 피식자로 향함

</div>
<div class="all-center">
<video height="470px" src="./assets/sim.webm" type="video/webm" controls />

</div>
</div>
</div>

---

### 시뮬레이션 - Source Code

<div class="scroll">

<script src="https://gist.github.com/ywbird/9fe37cf54589fbe12917bd0e75237974.js"></script>
</div>
