---
title: "[패스트캠퍼스 수강 후기] 프론트엔드 인강 100% 환급 챌린지 35회차 미션 - 31강 css modules, styled components"
date: 2020-09-13
categories: fastcampus
tags: fastcampus all-in-one-challenge day35 react styled-components
---

# css modules

css클래스명이 중복되는 것을 방지하는 라이브러리이다. 리액트에 기본으로 깔려있기때문에 추가적인 설치는 필요없다. 사용법은 css파일명에 'box.module.css'이런식으로 만들어주는 것이다. 그리고 사용할 리액트 컴포넌트에 아래와 같이 써주면 고유화된 클래스명으로 자동으로 변환되어 출력한다.

![css module](/images/200913-4.png)  
![css module](/images/200913-5.png)

css modules은 아래와 같은 상황에서 주로 많이 사용한다.

1. 레거시 프로젝트에 리액트를 도입할 때
2. CSS 클래스 네이밍 규칙 만들기 귀찮을 때

이럴때 사용하는 것이므로 이번에는 영상만 시청하고 직접 실습은 나중에 필요할때 찾아서 해보는 것으로 하자.

# styled compoenets

styled components는 스타일은 js형태로 넣는 것이다. 이런 형태를 css-in-js라고 하는데 이런 형태로 이루어진 css가 이것만 있는 것은 아니다.
![캡처](/images/200913-1.png)  
emotion도 많이 쓰이고 있긴 하다고 한다. 무튼 우리는 styled component를 배워볼 것인데 아래와 같은 형태로 이루어져 있다.
![캡처](/images/200913-2.png)  
Tagged Template Literal방식으로 이루어져있는데 주로 백틱을 이용하여 쓰는 아래와 같은 형식은 많이 접했을 것이다. 이것은 Template Literal 방식이다.

```javascript
const name = "react";
const message = `hello ${name}`;
console.log(message); //hello react 출력
```

문자열 안에 특정 자바스크립트 값을 넣어서 쓸때 백틱을 사용해서 쉽게 쓸 수 있는 방식을 말했다.

```javascript
const red = "빨간색";
const blue = "파란색";

function favoritColors(text, ...values) {
  console.log(texts);
  console.log(values);
}
favoriteColors`제가 좋아하는 색은 ${red}와 ${blue}입니다.`;
```

이런식으로 백틱을 사용해서 함수에 택스트와 벨류로 각각 찍어보면 텍스트는 텍스트대로 모아서 배열로 갖게되고 나머지 values에는 red와 blue가 각각 담겨있는 것을 볼 수 있다.  
아무튼 우리가 여기에서 알아야할 것은 styled components를 쓸때 props를 설정하게 됐을 때 props를 읽기 위하여 tagged template literal을 사용한다는 정도만 알고 넘어가자.  
새로운 리액트를 만들어보자. 이름은 styling-with-styled-components로 한다. 그리고 styled-components를 설치해준다.

```
yarn add styled-components
```

다 깔았으면 App.js로 가보자.

> App.js

```javascript
import React from "react";
import styled from "styled-components"; //styleed-components 연결해주기

const Circle = styled.div`
  width: 5rem;
  height: 5rem;
  background: ${(props) => props.color}; /*컬러를 props로 받아오려면*/
  border-radius: 50%;
`;

function App() {
  return (
    <div>
      <Circle
        // 컬러를 props로 전달 하려면
        color="blue"
      />
    </div>
  );
}

export default App;
```

이번에는 huge라는 true or false조건의 props를 추가해보자.

```javascript
import React from "react";
import styled, { css } from "styled-components"; // 4. css추가

const Circle = styled.div`
  width: 5rem;
  height: 5rem;
  background: ${(props) => props.color || "black"};
  border-radius: 50%;
  ${(
    props // 2. huge가 true일때
  ) =>
    props.huge &&
    css`
      /* 3. css추가 */
      width: 10rem;
      height: 10rem;
    `}
`;

function App() {
  return (
    <div>
      <Circle color="blue" />
      <Circle
        // 1. props 추가
        huge
      />
    </div>
  );
}

export default App;
```

huge가 ture일때 && 이하의 css속성을 가져오게끔 해야되는데 저부분에서 css를 써주지 않으면 그냥 template literal방식이다. 이것을 tagged template literal방식으로 써주려면 앞에 css라고 불여줘야 한다. 그래야지만 나중에 다른 props들도 추가로 더 만들어 줄 수 있다.  
그리고 추가적으로 background에 color값을 주지 않았을 때 default로 black이 나오게끔 하고 싶어서 위와 같이 ||연산자를 사용해봤는데 잘 나온다. (잘한거 맞겠지?ㅎ)  
그럼 여기까지 하고 리액트를 구현해보자. 아래와 같이 잘 나올 것이다.
![리액트화면](/images/200913-3.png)

오늘은 여기까지..  
시청 영상 31강 07~08까지

![수강인증이미지](/images/200913-6.jpeg)

프론트엔드 개발 올인원 패키지 with React Online. 👉 https://bit.ly/31Cf1hp
