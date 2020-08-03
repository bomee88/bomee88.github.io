
---
title: "css 그라디언트로 사선 백그라운드 만들기"
date: 2020-07-30
categories: css gradient background
---
   
그라디언트는 잘 사용하면    
여러가지 효과를 낼 수 있다.   
그 중에서 오늘 해볼 것은     
아래와 같은 시안을 받았을 때 svg가 아닌 css로 만들어 보는 것이다.      
    
<img src="//images/20200730_1.png" alt="img"/>
   
그라디언트는 원래 부드럽게 두가지 색을 믹스하는 것인데    
비율을 잘 조절하면 섞이는 구간을 분리할 수 있다.   
아래와 같이 코드를 작성해보자.   
   
```css
background: linear-gradient(-45deg, #f3f5f0 50%, #dfe8eb 50%);
```
이미지와 똑같이 사선으로 배경이 그려지는 것을 볼 수 있다.
    
그라디언트의 예제를 직접 보면서   
작성해보고 싶다면 아래 링크에서    
테스트하고 만들어 보자.    
<a href="https://developer.mozilla.org/ko/docs/Web/CSS/linear-gradient">MDN Web Docs</a>
