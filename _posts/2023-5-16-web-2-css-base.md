---
title: "[웹 프로그래밍 - 2] CSS 기본"
date: 2023-05-17 15:40:00 +0900
categories: [웹 프로그래밍, Frontend]
tags: [devrunner, web, frontend, css]
---

## **UX, UI와 CSS**

---

**UX(User Experience)** 는 유저가 서비스와 상호작용하면서 갖게 되는 전반적인 경험을 의미한다.
**UI(User Interface)** 는 사용자가 서비스와 상호 작용할 수 있도록 하는 그래픽 요소 및 디자인을 의미한다.
**CSS**는 이러한 웹의 UX, UI를 향상시키기 위한 디자인을 위해 사용된다.

## **적용 방법**

---

html에 css를 적용하는 방법 3가지는 다음과 같다.

1. html 파일의 `<head>` 태그 내의 `<style>` 활용

2. `<link>`로 외부 참조

3. 태그 내의 `style` 속성 활용(inline 방식)

<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="bGmxwEb" data-user="Baejw0111" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/Baejw0111/pen/bGmxwEb">
  Using CSS</a> by Baejw0111 (<a href="https://codepen.io/Baejw0111">@Baejw0111</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

## **선택자**

---

CSS에서는 선택자로 규칙을 적용할 요소를 지정한다.

### **전체 선택자**

`*`를 사용하며, 모든 태그에 적용된다.

### **유형 선택자**

태그명을 사용하며, 해당 태그에만 적용된다.

### **class 선택자**

`.`은 class임을 나타내며, 해당 class를 가지는 모든 요소들에 적용된다.

### **id 선택자**

`#`은 id임을 타나태며, 해당 id를 가지는 모든 요소들에 적용된다.

<p class="codepen" data-height="300" data-default-tab="css,result" data-slug-hash="NWOLRrW" data-user="Baejw0111" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/Baejw0111/pen/NWOLRrW">
  선택자</a> by Baejw0111 (<a href="https://codepen.io/Baejw0111">@Baejw0111</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

## **디자인 요소**

---

### **폰트**

- `font-weight`: 폰트의 굵기 설정

- `font-family`: 글꼴 설정

<p class="codepen" data-height="300" data-default-tab="css,result" data-slug-hash="GRYXjWL" data-user="Baejw0111" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/Baejw0111/pen/GRYXjWL">
  폰트</a> by Baejw0111 (<a href="https://codepen.io/Baejw0111">@Baejw0111</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

### **텍스트 정렬**

`text-align`으로 텍스트 정렬을 설정할 수 있다.

<p class="codepen" data-height="300" data-default-tab="css,result" data-slug-hash="jOevMLr" data-user="Baejw0111" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/Baejw0111/pen/jOevMLr">
  텍스트 정렬</a> by Baejw0111 (<a href="https://codepen.io/Baejw0111">@Baejw0111</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

### **테두리**

`border`로 테두리의 굵기와 스타일을 설정할 수 있다.

<p class="codepen" data-height="300" data-default-tab="css,result" data-slug-hash="VwEGKMV" data-user="Baejw0111" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/Baejw0111/pen/VwEGKMV">
  Untitled</a> by Baejw0111 (<a href="https://codepen.io/Baejw0111">@Baejw0111</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

### **배경**

- `background-color`: 배경색 설정

<p class="codepen" data-height="300" data-default-tab="css,result" data-slug-hash="XWxPjzz" data-user="Baejw0111" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/Baejw0111/pen/XWxPjzz">
  Untitled</a> by Baejw0111 (<a href="https://codepen.io/Baejw0111">@Baejw0111</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

- `background-image`: 이미지의 url을 링크해 박스의 배경에 이미지 삽입

- `background-repeat`: 이미지가 배경을 꽉 채우지 못할 경우에 배경 이미지의 반복 여부를 설정

- `background-size`: 이미지를 배경에 어떻게 채울 지 설정

<p class="codepen" data-height="300" data-default-tab="css,result" data-slug-hash="poxOEaR" data-user="Baejw0111" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/Baejw0111/pen/poxOEaR">
  배경 이미지</a> by Baejw0111 (<a href="https://codepen.io/Baejw0111">@Baejw0111</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

위의 설정들에 대해서는 여러가지 옵션들이 존재한다.
에디터의 자동완성 기능과 docs로 알아서 찾아보도록 하자.

### **길이, 너비 등등**

- `width`: 박스의 너비 설정

- `height`: 박스의 높이 설정

- `border-radius`: 박스 꼭짓점의 둥근 정도 설정

<p class="codepen" data-height="300" data-default-tab="css,result" data-slug-hash="ZEqMpxJ" data-user="Baejw0111" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/Baejw0111/pen/ZEqMpxJ">
  Untitled</a> by Baejw0111 (<a href="https://codepen.io/Baejw0111">@Baejw0111</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

### **margin, padding**

- margin: 레이아웃 바깥쪽 여백을 설정

- padding: 레이아웃 안쪽 여백을 설정

위 설정들은 `left`, `right`, `top`, `bottom`으로 디테일하게 방향 별로 설정이 가능하며, `auto`로 픽셀 자동 조정을 할수 있다.

<p class="codepen" data-height="300" data-default-tab="css,result" data-slug-hash="BaqOLxN" data-user="Baejw0111" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/Baejw0111/pen/BaqOLxN">
  Untitled</a> by Baejw0111 (<a href="https://codepen.io/Baejw0111">@Baejw0111</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

<p class="codepen" data-height="300" data-default-tab="css,result" data-slug-hash="eYPLdKG" data-user="Baejw0111" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/Baejw0111/pen/eYPLdKG">
  Untitled</a> by Baejw0111 (<a href="https://codepen.io/Baejw0111">@Baejw0111</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

### **상속**

특정 CSS 요소(`text-align`,`font-size`,`color` 등)는 부모 태그로부터 상속받는다.

<p class="codepen" data-height="300" data-default-tab="css,result" data-slug-hash="abRamjK" data-user="Baejw0111" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/Baejw0111/pen/abRamjK">
  Untitled</a> by Baejw0111 (<a href="https://codepen.io/Baejw0111">@Baejw0111</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

### **box shadow**

`box-shadow`로 박스에 그림자 효과를 넣을 수 있다.

<p class="codepen" data-height="300" data-default-tab="css,result" data-slug-hash="VwEGKGR" data-user="Baejw0111" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/Baejw0111/pen/VwEGKGR">
  Untitled</a> by Baejw0111 (<a href="https://codepen.io/Baejw0111">@Baejw0111</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>
