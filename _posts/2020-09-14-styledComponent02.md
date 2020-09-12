---
title: "[패스트캠퍼스 수강 후기] 프론트엔드 인강 100% 환급 챌린지 35회차 미션 - 31강 styled components, Polished"
date: 2020-09-13
categories: fastcampus
tags: fastcampus all-in-one-challenge day35 react styled-components Polished
---

# styled compoenets로 Button 만들기

재사용성 높은 버튼을 만들어보자. 먼저 src안에 components 폴더를 만들고 그 안에 Button.js를 만들자.

> Button.js

```javascript
import React, { Children } from "react";
import styled from "styled-components";

const StyledButton = styled.button`
  /* 공통스타일 */
  display: inline-flex;
  justify-content: center;
  align-items: center;
  outline: none;
  border: none;
  border-radius: 4px;
  color: #fff;
  font-weight: bold;
  cursor: pointer;
  padding-left: 1rem;
  padding-right: 1rem;

  /* 크기 */
  height: 2.25rem;
  font-size: 1rem;

  /* 색상 */
  background: #228be6;
  &:hover {
    background: #339af0;
  }
  &:active {
    background: #1c7ed6;
  }

  /* 기타 */
  & + & {
    margin-left: 1rem;
  }
`;

function Button({ children, ...rest }) {
  return <StyledButton {...rest}>{children}</StyledButton>;
}

export default Button;
```

> App.js

```javascript
import React from "react";
import styled from "styled-components"; // css추가
import Button from "./components/Button"; //Button.js연결

const AppBlock = styled.div`
  width: 512px;
  margin: 0 auto;
  margin-top: 4rem;
  border: 1px solid #000;
  padding: 1rem;
`;

function App() {
  return (
    <AppBlock>
      <Button>BUTTON</Button>
    </AppBlock>
  );
}

export default App;
```

이렇게 App.js까지 수정하고 나면 아래와 같이 잘 나온다.  
![리액트화면](/images/200914-1.png)

# Polished 스타일유틸함수 사용하기

Polished는 자주 사용하는 css를 미리 함수화 시켜놓은 라이브러리이다. 우리는 여기에서 lighten과 daken을 사용할 것이다. 더 많은 라이브러리의 기능들은 [polished docs](https://polished.js.org/)를 참고하자. 그럼 먼저 yarn을 사용해 아래와 같이 설치한다.

```
yarn add polished
```

그리고 아까 만들었던 Button을 수정해보자.

> Button.js

```javascript
import React from "react";
import styled from "styled-components";
import { darken, lighten } from "polished"; //1. polished 추가

const StyledButton = styled.button`
  /* 공통스타일 */
  display: inline-flex;
  justify-content: center;
  align-items: center;
  outline: none;
  border: none;
  border-radius: 4px;
  color: #fff;
  font-weight: bold;
  cursor: pointer;
  padding-left: 1rem;
  padding-right: 1rem;

  /* 크기 */
  height: 2.25rem;
  font-size: 1rem;

  /* 색상 */
  background: #228be6;
  &:hover {
    background: ${lighten(0.1, "#228be6")}; /* polished 함수추가 */
  }
  &:active {
    background: ${darken(0.1, "#228be6")}; /* polished 함수추가 */
  }

  /* 기타 */
  & + & {
    margin-left: 1rem;
  }
`;

function Button({ children, ...rest }) {
  return <StyledButton {...rest}>{children}</StyledButton>;
}

export default Button;
```

우리는 이제 버튼의 색깔을 App.js에서 전역적으로 적용할 수 있게 수정해 볼 것이다. 그러기 위해서는 styled-components의 ThemeProvider이라는 것을 사용해 줄 것인데 App.js를 아래와 같이 바꿔보도록하자.

> App.js

```javascript
import React from "react";
import styled, { ThemeProvider } from "styled-components"; // 1. ThemeProvider 추가
import Button from "./components/Button";

const AppBlock = styled.div`
  width: 512px;
  margin: 0 auto;
  margin-top: 4rem;
  border: 1px solid #000;
  padding: 1rem;
`;

const palette = {
  //3. theme 생성
  blue: "#228be6",
  gray: "#496057",
  pink: "#f06595",
};

function App() {
  return (
    <ThemeProvider
      theme={{
        palette, //4. theme 불러오기
      }}
      //2. ThemeProvider로 감싸주기
    >
      <AppBlock>
        <Button>BUTTON</Button>
      </AppBlock>
    </ThemeProvider>
  );
}

export default App;
```

이제 App에서 만들어 준 palette를 Button에 사용해보도록하자.

> Button.js 의 const StyledButton 중 색상부분

```scss
  /* 색상 */
  background: ${(props) => props.theme.palette.blue}; //props로 받아와 줌.
  &:hover {
    background: ${(props) =>
      lighten(0.1, props.theme.palette.blue)};
  }
  &:active {
    background: ${(props) =>
      darken(0.1, props.theme.palette.blue)};
  }
```

음.. 코드가 만족스럽지 못하다. props를 변수에 가져와서 전달해보자.

> Button.js

```javascript
import React from "react";
import styled, { css } from "styled-components"; //1. css 불러오기
import { darken, lighten } from "polished";

const StyledButton = styled.button`
  /* 공통스타일 */
  display: inline-flex;
  justify-content: center;
  align-items: center;
  outline: none;
  border: none;
  border-radius: 4px;
  color: #fff;
  font-weight: bold;
  cursor: pointer;
  padding-left: 1rem;
  padding-right: 1rem;

  /* 크기 */
  height: 2.25rem;
  font-size: 1rem;

  /* 색상 */
  ${(props) => {
    //2. props 안에 써줌.
    const color = props.theme.palette.blue; //3. color 변수 생성
    //4. css로 props 전달
    return css`
      background: ${color};
      &:hover {
        background: ${lighten(0.1, color)};
      }
      &:active {
        background: ${darken(0.1, color)};
      }
    `;
  }}

  /* 기타 */
  & + & {
    margin-left: 1rem;
  }
`;

function Button({ children, ...rest }) {
  return <StyledButton {...rest}>{children}</StyledButton>;
}
export default Button;
```

이제 색깔을 App에서 받아오게 할것이니까 fuction Button에 color를 받아오게, 또 defaultProps도 설정해줘보자.

```javascript
import React from "react";
import styled, { css } from "styled-components"; //1. css 불러오기
import { darken, lighten } from "polished";

const StyledButton = styled.button`
  /* 공통스타일 */
  display: inline-flex;
  justify-content: center;
  align-items: center;
  outline: none;
  border: none;
  border-radius: 4px;
  color: #fff;
  font-weight: bold;
  cursor: pointer;
  padding-left: 1rem;
  padding-right: 1rem;

  /* 크기 */
  height: 2.25rem;
  font-size: 1rem;

  /* 색상 */
  ${(props) => {
    const color = props.theme.palette[props.color]; //컬러를 받아올 부분을 배열로 감싸고 props.color로 받아와준다.
    return css`
      background: ${color};
      &:hover {
        background: ${lighten(0.1, color)};
      }
      &:active {
        background: ${darken(0.1, color)};
      }
    `;
  }}

  /* 기타 */
  & + & {
    margin-left: 1rem;
  }
`;

function Button({ children, color, ...rest }) {
  return (
    <StyledButton
      //rest로 다 받아와서 color를 굳이 설정 안해줘도 되지만 defaultProps도 설정하니까 보기 편하게 color는 따로 써줘보자.
      color={color}
      {...rest}
    >
      {children}
    </StyledButton>
  );
}

Button.defaultProps = {
  //default는 blue로 설정.
  color: "blue",
};

export default Button;
```

이제 App.js에 버튼별 컬러 props를 추가해주고 확인해보자.

> App.js

```javascript
function App() {
  return (
    <ThemeProvider
      theme={{
        palette,
      }}
    >
      <AppBlock>
        <Button>BUTTON</Button>
        <Button color="pink">BUTTON</Button>
        <Button color="gray">BUTTON</Button>
      </AppBlock>
    </ThemeProvider>
  );
}
```

![리액트화면](/images/200914-2.png)

버튼은 잘 나오는 것이 확인 됐지만 코드를 더 깔끔하게 리팩토링 해보도록 하자.

> Button.js

```javascript
import React from "react";
import styled, { css } from "styled-components";
import { darken, lighten } from "polished";

//1. 컬러에 관한 부분만 변수로 따로 빼줌.
const colorStyles = css`
  /* 색상 */
  ${({ theme, color }) => {
    //2. 객체 비구조화 할당으로 깔끔하게 정리
    const selectedColor = theme.palette[color];
    return css`
      background: ${selectedColor};
      &:hover {
        background: ${lighten(0.1, selectedColor)};
      }
      &:active {
        background: ${darken(0.1, selectedColor)};
      }
    `;
  }}
`;
const StyledButton = styled.button`
  /* 공통스타일 */
  display: inline-flex;
  justify-content: center;
  align-items: center;
  outline: none;
  border: none;
  border-radius: 4px;
  color: #fff;
  font-weight: bold;
  cursor: pointer;
  padding-left: 1rem;
  padding-right: 1rem;

  /* 크기 */
  height: 2.25rem;
  font-size: 1rem;

  /* 색상 */
  ${colorStyles}

  /* 기타 */
  & + & {
    margin-left: 1rem;
  }
`;

function Button({ children, color, ...rest }) {
  return (
    <StyledButton
      //rest로 다 받아와서 color를 굳이 설정 안해줘도 되지만 defaultProps도 설정하니까 보기 편하게 color는 따로 써줘보자.
      color={color}
      {...rest}
    >
      {children}
    </StyledButton>
  );
}

Button.defaultProps = {
  //default는 blue로 설정.
  color: "blue",
};

export default Button;
```

오늘은 여기까지..  
시청 영상 31강 09~10까지

![수강인증이미지](/images/200914-3.jpeg)

프론트엔드 개발 올인원 패키지 with React Online. 👉 https://bit.ly/31Cf1hp
