---
title : "jquery fadeIn 대신에 css transition 사용하기, css로 토글 만들기"
date : 2020-08-04
categories : jQuery fadeIn fadeOut css transition
---

자연스러운 인터렉션을 위해 주로 제이쿼리의 fadeIn, fadeOut, slideUp, slideDown등을 사용해왔다면   
앞으로는 css3의 transtion을 활용해보자.   
더 부드럽고, 더 유연하고, 더 자연스러운 인터렉션이 가능해진다.   
   
css의 transition은 여러가지 속성을 가지고 있으나   
필자가 주로 사용하는 것은 아래와 같다.   
그 이유인 즉슨 제일 적당한 속도에 깔끔함을 제공하기 때문이다.   
(휘황찬란한 인터렉션은 오히려 사용자로 하여금 거부감을 느끼게 한다.)   
```css
div{opacity: 0; transition: 0.2s all;}
div:hover{opacity:1;}
```
여기서 0.2s는 트랜지션 진행하는 속도, all은 트랜지션을 적용하는 범위를 말한다.   
한가지 유의해야할 것은 'display'는 transition이 안먹힌다.
엘리먼트를 없앴다 나타내고 싶다면 opacity를 활용하도록 한다.
만약 여기서 fadeIn/Out이 아닌 SlideUp/Down을 구현하고 싶다면
```css
div{width: 100px; height: 0; overflow:hidden; transition: 0.2s all;}
div:hover{height: 100px;}
```
이렇게 진행하면 된다.    
응용방법으로는 position을 활용하여 top,bottom,right,left값을 조절하여 사용할수도 있다.   
또 제이쿼리의 addClass() / removeClass()를 활용하여 토글이 가능하게도 할 수 있다.   
예제는 아래와 같다.   

<p class="codepen" data-height="265" data-theme-id="dark" data-default-tab="js,result" data-user="bomee" data-slug-hash="PoNYxge" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="css toggle">
  <span>See the Pen <a href="https://codepen.io/bomee/pen/PoNYxge">
  css toggle</a> by bomee (<a href="https://codepen.io/bomee">@bomee</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>


