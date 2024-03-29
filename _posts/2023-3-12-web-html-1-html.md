---
title: "[웹 프로그래밍 - HTML] 1. HTML 기본"
date: 2023-03-12 19:42:00 +0900
categories: [웹 프로그래밍, HTML]
tags: [devrunner, web, frontend, html]
---

## **서론**

---

이제부터 그간 싸피에서 배운 것들을 블로그에 포스팅하려고 한다.
이번 글이 그 시작으로, 먼저 HTML에 대해 다루고자 한다.

## **HTML이란?**

---

**Hyper Text Markup Language**의 약자로서, 태그 등을 이용하여 문서나 데이터의 구조를 명시하는 언어다.

## **주로 쓰이는 태그들**

---

### **`<h>` 태그**

- 글자 크기를 조절할 때 사용된다.

- 숫자가 작을수록 사이즈가 크다.

<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="rNqrQxa" data-user="Baejw0111" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/Baejw0111/pen/rNqrQxa">
  Untitled</a> by Baejw0111 (<a href="https://codepen.io/Baejw0111">@Baejw0111</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

### **`<ul>`, `<ol>`, `<li>` 태그**

- 목록을 생성하는 태그들이다.

- `<ul>`은 unordered list를 뜻함. 넘버링이 매겨지지 않는 리스트다.

- `<ol>`은 ordered list를 뜻함. 넘버링이 매겨지는 리스트다.

- `<li>`는 위 두 태그의 자식 태그다.

<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="yLRxeWz" data-user="Baejw0111" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/Baejw0111/pen/yLRxeWz">
  &lt;ul&gt;, &lt;ol&gt;, &lt;li&gt;</a> by Baejw0111 (<a href="https://codepen.io/Baejw0111">@Baejw0111</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

### **`<a>` 태그**

- 텍스트에 링크를 걸기 위한 용도의 태그다.

<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="zYmJrgL" data-user="Baejw0111" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/Baejw0111/pen/zYmJrgL">
  Untitled</a> by Baejw0111 (<a href="https://codepen.io/Baejw0111">@Baejw0111</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

### **`<p>` 태그**

- 문단을 의미하는 태그다.

- `<br>` 태그 대신 줄바꿈을 할 수 있다.

- 글의 가독성을 높여줄 수 있다.

<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="NWOLNWp" data-user="Baejw0111" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/Baejw0111/pen/NWOLNWp">
  &lt;p&gt;</a> by Baejw0111 (<a href="https://codepen.io/Baejw0111">@Baejw0111</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

### **`<input>` 태그**

- 사용자로부터 입력을 받을 수 있는 입력창을 생성할 수 있는 태그다.

- `type`: 태그의 입력 타입

- `placeholder`: 어떤 것을 입력해야 하는지에 대한 안내 문구

<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="KKGxzwX" data-user="Baejw0111" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/Baejw0111/pen/KKGxzwX">
  Untitled</a> by Baejw0111 (<a href="https://codepen.io/Baejw0111">@Baejw0111</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

### **`<form>` 태그**

- 서버 전송을 위한 양식 태그다.

<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="ZEqMWGo" data-user="Baejw0111" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/Baejw0111/pen/ZEqMWGo">
  &lt;form&gt;</a> by Baejw0111 (<a href="https://codepen.io/Baejw0111">@Baejw0111</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

### **`<select>` 태그**

- 옵션 메뉴를 제공하는 태그다.

<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="qBJMZdw" data-user="Baejw0111" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/Baejw0111/pen/qBJMZdw">
  &lt;select&gt;</a> by Baejw0111 (<a href="https://codepen.io/Baejw0111">@Baejw0111</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

### **`<iframe>` 태그**

- 현재 문서에 다른 html 페이지를 삽입하는 태그다.

<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="bGmxpVq" data-user="Baejw0111" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/Baejw0111/pen/bGmxpVq">
  Untitled</a> by Baejw0111 (<a href="https://codepen.io/Baejw0111">@Baejw0111</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

### **`<div>` 태그**

- 레이아웃을 구분하기 위해 사용하는 태그다.

- css와 함께 많이 쓰인다.

- 줄바꿈이 일어난다.

<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="YzJOqwz" data-user="Baejw0111" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/Baejw0111/pen/YzJOqwz">
  &lt;div&gt;</a> by Baejw0111 (<a href="https://codepen.io/Baejw0111">@Baejw0111</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

### **`<span>` 태그**

- 이 태그 역시 css와 함께 쓰이는 태그 중 하나다.

- 하지만 `<div>`와 달리 줄바꿈이 일어나지는 않는다.

<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="JjmaXGz" data-user="Baejw0111" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/Baejw0111/pen/JjmaXGz">
  &lt;span&gt;</a> by Baejw0111 (<a href="https://codepen.io/Baejw0111">@Baejw0111</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

### **`<img>` 태그**

- 이미지를 나타내는 태그이다.

- `src`: 이미지의 경로

- `alt`: 이미지가 제대로 표시되지 않을 경우 대신 출력될 텍스트

<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="PoydNNz" data-user="Baejw0111" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/Baejw0111/pen/PoydNNz">
  &lt;img&gt;</a> by Baejw0111 (<a href="https://codepen.io/Baejw0111">@Baejw0111</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

## **Semantic Tag**

---

![image](https://user-images.githubusercontent.com/87963766/214270662-a1838c77-311e-4ab3-8f87-68b88ee040a8.png)

### **Semantic Web**

- 기계가 읽고 처리할 수 있는 웹을 의미한다.

- 기계가 쉽게 읽을 수 있도록 **Semantic Tag**를 사용한다.

### **`<header>`**

- 문서나 특정 섹션의 헤더를 정의 할때 사용한다.

- 로고나 제목등을 표시할때 주로 사용한다.

- 문서의 정보가 요약되어 있다.

### **`<nav>`**

- 링크중에서 중요도가 높은 링크들을 구성해 둘때 사용한다.

### **`<main>`**

- 해당 문서의 메인 컨텐츠를 정의할 때 사용한다.

- 페이지당 단 하나의 `main`만 존재해야한다.

### **`<section>`**

- 독립적인 섹션을 정의 할 때 사용한다.

### **`<article>`**

- 페이지나 사이트와 독립적으로 구성할수 있는 요소를 정의 할 때 사용한다.

- ex) 블로그 , 뉴스기사등

- 내용끼리 서로 관련이 있으면 `section`

- 없는 개별의 내용인 경우 `article`

- 의미가 없고 단순히 묶어주는 용도면 `div` 를 활용

### **`<aside>`**

- 사이드바 개념으로 활용한다.

- 광고 구글 광고 게재등에 활용한다.
