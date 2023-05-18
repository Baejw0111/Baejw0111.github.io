---
title: "[웹 프로그래밍 - CSS] 2. CSS Layout"
date: 2023-05-17 17:40:00 +0900
categories: [웹 프로그래밍, CSS]
tags: [devrunner, web, frontend, css]
---

## **display**

---

### **inline**

- 대표적인 inline 태그: `<span>, <a>`

- `width`, `height`, `margin` 모두 제대로 동작하지 않는다.
  `padding`은 작동한다.

<p class="codepen" data-height="300" data-default-tab="css,result" data-slug-hash="GRYXLRX" data-user="Baejw0111" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
<span>See the Pen <a href="https://codepen.io/Baejw0111/pen/GRYXLRX">
display inline</a> by Baejw0111 (<a href="https://codepen.io/Baejw0111">@Baejw0111</a>)
on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

### **block**

- 대표적인 block 태그: `<div>`, `<p>`, `<h>`

- block 요소는 기본적으로 줄바꿈이 일어난다(한 줄 차지)

- `margin`,`padding`이 적용됨

<p class="codepen" data-height="300" data-default-tab="css,result" data-slug-hash="PoydgwX" data-user="Baejw0111" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/Baejw0111/pen/PoydgwX">
  Untitled</a> by Baejw0111 (<a href="https://codepen.io/Baejw0111">@Baejw0111</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

### **inline-block**

- 대표적인 inline-block 태그: `<button>`, `<select>`, `<input>`

- 줄바꿈없이 나란히 배치되나 `width`, `heihgt`, `margin`, `padding` 속성이 적용됨

<p class="codepen" data-height="300" data-default-tab="css,result" data-slug-hash="bGmxJVy" data-user="Baejw0111" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/Baejw0111/pen/bGmxJVy">
  display inline-block</a> by Baejw0111 (<a href="https://codepen.io/Baejw0111">@Baejw0111</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

### **none**

요소의 `display` 속성을 `none`으로 설정하면 해당 요소는 보이지 않는다.

<p class="codepen" data-height="300" data-default-tab="css,result" data-slug-hash="OJBoGrJ" data-user="Baejw0111" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/Baejw0111/pen/OJBoGrJ">
  display none</a> by Baejw0111 (<a href="https://codepen.io/Baejw0111">@Baejw0111</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

### **flex**

css 레이아웃 디자인에 있어서 가장 중요한 기능으로, 웬만한 레이아웃 디자인은 이걸로 다 구현 가능하다.
메인 축을 기반으로 정렬을 진행하며, 하나의 flex-container(부모 요소)와 flex-item(부모 요소)으로 구성된다.

- `justify-content`: 주축 기준 정렬

- `align-items`: 교차축 기준 정렬

- `flex-direction`: 주축 정의

<p class="codepen" data-height="300" data-default-tab="css,result" data-slug-hash="JjmaqLq" data-user="Baejw0111" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/Baejw0111/pen/JjmaqLq">
  flex 1</a> by Baejw0111 (<a href="https://codepen.io/Baejw0111">@Baejw0111</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

- `flex`: 비율 조정. 자식 속성으로 넣어 활용한다.

- `flex-wrap`: 컨테이너가 한줄에 담을 여유공간이 없을 때 아이템에 대한 줄바꿈을 결정

<p class="codepen" data-height="300" data-default-tab="css,result" data-slug-hash="qBJMGYe" data-user="Baejw0111" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/Baejw0111/pen/qBJMGYe">
  flex 2</a> by Baejw0111 (<a href="https://codepen.io/Baejw0111">@Baejw0111</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

### **display 명시**

display의 속성을 명시적으로 적용하고 싶다면 아래와 같이 하면 된다.

```css
* {
  display: inline;
  /*
    display: block;
    display: inline-block;
    display: flex;
    */
}
```

## **position**

---

display가 2차원적으로만 동작했다면, **position**은 3차원적으로 동작한다.
`top`, `left`, `right`, `bottom`으로 위치 설정을 할 수 있으며, 기준에 따라 다음 세가지로 나뉜다.

### **fixed**

상위 요소에 영향을 받지 않고 레이아웃을 고정시키며, 브라우저의 전체화면을 기준으로 요소를 배치한다.
상단 메뉴와 같이 스크롤을 내려도 고정된 위치에 나타내야 할 요소를 배치할 때 사용한다.

주의해야할 점은 width를 따로 지정하지 않으면 inline처럼 width가 최소값으로 설정된다.

<p class="codepen" data-height="300" data-default-tab="css,result" data-slug-hash="GRYXaBj" data-user="Baejw0111" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/Baejw0111/pen/GRYXaBj">
  position fixed</a> by Baejw0111 (<a href="https://codepen.io/Baejw0111">@Baejw0111</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

### **relative**

최상위 태그의 위치를 기준점으로 배치된다.

<p class="codepen" data-height="300" data-default-tab="css,result" data-slug-hash="vYVzwzL" data-user="Baejw0111" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/Baejw0111/pen/vYVzwzL">
  position relative</a> by Baejw0111 (<a href="https://codepen.io/Baejw0111">@Baejw0111</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

### **absolute**

기준점은 선택적이다. 부모 태그에 position이 있다면 해당 태그가 기준점이 되고, 없다면 그 상위 태그로 계속 올라가게 된다.
선언시 width가 inline 형태로 줄어든다.

<p class="codepen" data-height="300" data-default-tab="css,result" data-slug-hash="abRarar" data-user="Baejw0111" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/Baejw0111/pen/abRarar">
  position absolute</a> by Baejw0111 (<a href="https://codepen.io/Baejw0111">@Baejw0111</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

- z-index: 요소들에 대해 3차원 방향의 순서를 부여하며, 큰 값을 부여할수록 우선 순위가 높다.

<p class="codepen" data-height="300" data-default-tab="css,result" data-slug-hash="jOevodx" data-user="Baejw0111" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/Baejw0111/pen/jOevodx">
  position z-index</a> by Baejw0111 (<a href="https://codepen.io/Baejw0111">@Baejw0111</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>
