---
title : "jQuery로 top값 찾기"
date : 2020-08-03
categories : jQuery offset position scrollTop
---

jQuery를 사용하면서 자주 사용하는 top값 찾는 방법

```javascript
$("p").position().top;
$("p").offset().top;
$("div").scrollTop();
```
position과 offset은 둘다 똑같이 한 영역 안에서의 top값을 가져온다.   
예를 들어 div 안에 p가 있다고 가정하면   
div안에서의 p가 위치한 top값을 가져온다.  
scrollTop은 div에게 overflow: scroll을 주었을 경우   
현재의 스크롤탑 값을 반환한다.   
보통은 그래서 get상태보다 set상태로 많이 쓰는데   
아래를 참고하도록 한다.

```javascript
var target = $("p").offset().top;
$("div").scrollTop(target);
```
이런식으로 많이 쓴다.
특정 버튼을 눌렀을 시 animate가 되면서 이동하게 하려면
아래와 같이 활용해볼 수 있다.

```javascript
var target = $("p").offset().top;
$("button").click(function(){
  $("div").animate({scrollTop : target},400);
});
```

