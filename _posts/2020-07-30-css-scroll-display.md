---
title: "css로 스크롤바 없애기"
date: 2020-07-30
categories: css scroll display 
---

```css
div{overflow: scroll; -ms-overflow-style: none;} /*for ie*/
div::-webkit-scrollbar{display:none;} /*for chrome, safari, firefox*/
```
   
본론부터 말하면 위와 같다.   
익스플로러를 위한 -ms-용 코드는 스크롤이 없어지는 div안에 써주고   
표준을 위한 -webkit-은 밖에 써준다.   
자 이제 모바일, 웹에서 깨끗하게 지워진 스크롤을 확인할 수 있다.
   
오늘은 여기까지!
질문은 댓글로!
