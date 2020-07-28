---
title: "css로 형광펜 효과 만들기 (highlight효과)"
date: 2020-07-20
categories: css highlight
---
요즘은 css로 약간의 아날로그 감성을 나타내는게 대세인듯 하다.  
<img src="https://bomee88.github.io//images/200727_1.png" alt="highlight 이미지"/>   
이런식으로 노트에 형광펜을 그은 듯한 시안을 많이 받는다.   
css로 밑줄을 넣는 방법은 크게 두가지이다.
      
1. box-shadow 형식   
첫번째로는 위의 이미지와도 같이 긴 글, 그리고 반응형이여서 글이      
밑으로 떨어질 수 있는 경우에 적합한 방법이다.
   
```css
.highlight{
  display: inline;
  box-shadow: box-shadow: inset 0 -20px 0 #D9FCDB; /*-20px은 highlight의 두께*/
}
```
   
위와같이 css에 .highlight 클래스를 만들어주고   
html에서 원하는 부분에 span으로 감싸 highlight 클래스를 줘보자.   
위의 사진과 같은 효과를 볼 수 있을 것이다.

> <a href='https://codepen.io/bomee/pen/PoZgxer'>codepen으로 바로보기</a>
   
2. :after 형식
두번째로는 가상셀렉터인 after를 활용해서 넣는 방법이다.   
이 방법은 제목글이나 짧은 문구에 highlight를 할때 유용하다.
   
```css
.highlight:after{
  content:"";
  width: 0;
  height: 10px;
  display: inline-block;
  background: #D9FCDB;
}
```
여기까지는 정적으로 밑줄을 만들어 내는 css이다.
아까 위에 소스가 훨씬 간단한데 이렇게 가상셀렉터로 쓰는 이유는 따로 있다.
여기에 몇가지만 더하면 마우스 오버 시 형광펜을 치는 모션을 만들어 낼 수 있기 때문이다.
   
```html
<div>
  사람들은 희망보다는 절망에 더 익숙하다. <br>
  그래서 대개는 <span class="highlight">희망적인 메시지</span>보다는<br>
  <span class="highlight">부정적인 메시지</span>에 훨씬 쉽게 그리고 즉각적으로 반응한다. 
</div>
```
    
저 div에 마우스를 넣으면   
highlight에 밑줄이 쳐지게 해보자.

```css
div{cursor: pointer;}
div:hover .highlight:after{
  width:100%;
}
.highlight{
  display: inline-block; 
  position: relative;
}
.highlight:after{
  content:"";
  width: 0;
  height: 10px;
  display: inline-block;
  background: #D9FCDB;
  position: absolute;
  bottom:0;
  left:0;
  z-index:-1;
  transition: 0.2s all;
}
```
   
<p class="codepen" data-height="265" data-theme-id="light" data-default-tab="css,result" data-user="bomee" data-slug-hash="PoZgxer" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="css-highlight-2">
  <span>See the Pen <a href="https://codepen.io/bomee/pen/PoZgxer">
  css-highlight-2</a> by bomee (<a href="https://codepen.io/bomee">@bomee</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

이렇게 써주면 css만으로도 마우스 올렸을 때 인터렉티브한 모션을 만들 수 있다.    
잘 안된다면 아래 첨부한 코드펜 소스를 뜯어보도록 하자.   
오늘은 여기까지, 그럼 안녕🙋‍♀️
