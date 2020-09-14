---
title: "[패스트캠퍼스 수강 후기] 프론트엔드 인강 100% 환급 챌린지 37회차 미션 - 31강 styled components로 Button의 다양한 props 추가하기"
date: 2020-09-15
categories: fastcampus
tags: fastcampus all-in-one-challenge day37 react styled-components
---

# size props 만들기

크기에 해당하는 부분을 props로 받아와서 해당 사이즈로 나올 수 있게끔 Button을 수정해보자.

> Button.js

```javascript
import React from "react";
import styled, { css } from "styled-components";
import { darken, lighten } from "polished";

const colorStyles = css`
  /* 색상 */
  ${({ theme, color }) => {
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
//size 상수 추가
const sizeStyles = css`
  /* 크기 */
  ${(props) =>
    props.size === "large" &&
    css`
      height: 3rem;
      font-size: 1.25rem;
    `}
  ${(props) =>
    props.size === "medium" &&
    css`
      height: 2.25rem;
      font-size: 1rem;
    `}
    ${(props) =>
    props.size === "small" &&
    css`
      height: 1.75rem;
      font-size: 0.875rem;
    `}
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
  ${sizeStyles}

  /* 색상 */
  ${colorStyles}

  /* 기타 */
  & + & {
    margin-left: 1rem;
  }
`;

function Button({ children, color, size, ...rest }) {
  //size도 받아와준다.
  return (
    <StyledButton
      color={color}
      size={size} //size 추가.
      {...rest}
    >
      {children}
    </StyledButton>
  );
}

Button.defaultProps = {
  color: "blue",
  size: "medium", //size의 default값 추가.
};

export default Button;
```

이제 App.js에서 확인해보자.

> App.js

```javascript
import React from "react";
import styled, { ThemeProvider } from "styled-components";
import Button from "./components/Button";

const AppBlock = styled.div`
  width: 512px;
  margin: 0 auto;
  margin-top: 4rem;
  border: 1px solid #000;
  padding: 1rem;
`;

const ButtonGroup = styled.div`
  & + & {
    margin-top: 1rem;
  }
`;

const palette = {
  blue: "#228be6",
  gray: "#505566",
  pink: "#f06595",
};

function App() {
  return (
    <ThemeProvider
      theme={{
        palette,
      }}
    >
      <AppBlock>
        <ButtonGroup>
          <Button size="large">BUTTON</Button>
          <Button color="pink">BUTTON</Button>
          <Button color="gray" size="small">
            BUTTON
          </Button>
        </ButtonGroup>
      </AppBlock>
    </ThemeProvider>
  );
}

export default App;
```

위와 같이 쓰고 나면 아래 화면처럼 잘 나오는 것을 볼 수 있다.
![리액트화면](/images/200915-1.png)
이제 그러면 Button.js를 조금 리팩토링 해보도록 하자. 아까 작성했던 버튼 사이즈 코드를 아래와 같이 리팩토링 해본다.

> Button.js 에서 /_ 크기 _/에 해당하는 코드

```javascript
const sizes = {
  large: {
    height: "3rem",
    fontSize: "1.25rem",
  },
  medium: {
    height: "2.25rem",
    fontSize: "1rem",
  },
  small: {
    height: "1.75rem",
    fontSize: "0.875rem",
  },
};
const sizeStyles = css`
  ${({ size }) => css`
    height: ${sizes[size].height};
    font-size: ${sizes[size].fontSize};
  `}
`;
```

이렇게 작성하면 좀 더 유지보수 시 빨리 찾아 볼 수 있다고 한다. 하지만 개인취향이기때문에 원하는대로 하면 된다. 그럼 다음으로 Button의 outline과 fullWidth props를 마저 만들어보자.

# outline props 추가하기

Button.js의 색상에 관련된 부분만 따로 outline에 대한 속성을 추가해보도록 하자.

> Button.js 의 const colorStyle부분

```javascript
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
      ${(props) =>
        props.ouline &&
        css`
          color: ${selectedColor};
          background: none;
          border: 1px solid ${selectedColor};
          &:hover {
            background: ${selectedColor};
            color: #fff;
          }
        `}
    `;
  }}
`;
```

이제 App.js와서 ButtonGroup을 복사해서 outline속성을 추가해보자.

> App.js 에서 ButtonGroup 추가되는 부분

```javascript
<ButtonGroup>
  <Button size="large" outline>
    BUTTON
  </Button>
  <Button color="pink" outline>
    BUTTON
  </Button>
  <Button color="gray" size="small" outline>
    BUTTON
  </Button>
</ButtonGroup>
```

아래와 같이 outline style이 잘 나오는 것을 볼 수 있다.  
![리액트화면](/images/200915-2.png)

# fullWidth props 추가하기

outline과 똑같은 방식이다. 전체 코드를 참고하도록 하자.

> Button.js

```javascript
import React from "react";
import styled, { css } from "styled-components";
import { darken, lighten } from "polished";

const colorStyles = css`
  /* 색상 */
  ${({ theme, color }) => {
    const selectedColor = theme.palette[color];
    return css`
      background: ${selectedColor};
      &:hover {
        background: ${lighten(0.1, selectedColor)};
      }
      &:active {
        background: ${darken(0.1, selectedColor)};
      }
      ${(props) =>
        props.outline &&
        css`
          color: ${selectedColor};
          background: none;
          border: 1px solid ${selectedColor};
          &:hover {
            background: ${selectedColor};
            color: #fff;
          }
        `}
    `;
  }}
`;

const sizes = {
  large: {
    height: "3rem",
    fontSize: "1.25rem",
  },
  medium: {
    height: "2.25rem",
    fontSize: "1rem",
  },
  small: {
    height: "1.75rem",
    fontSize: "0.875rem",
  },
};
const sizeStyles = css`
  ${({ size }) => css`
    height: ${sizes[size].height};
    font-size: ${sizes[size].fontSize};
  `}
`;

const fullWidthStyle = css`
  ${(props) =>
    props.fullWidth &&
    css`
      width: 100%;
      justify-content: center;
      margin-left: 0 !important;
      & + & {
        margin-top: 1rem;
      }
    `}
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
  /* 기타 */
  & + & {
    margin-left: 1rem;
  }

  ${sizeStyles}
  ${colorStyles}
  ${fullWidthStyle}
`;

function Button({ children, color, size, outline, fullWidth, ...rest }) {
  return (
    <StyledButton
      color={color}
      size={size}
      outline={outline}
      fullWidth={fullWidth}
      {...rest}
    >
      {children}
    </StyledButton>
  );
}

Button.defaultProps = {
  color: "blue",
  size: "medium",
};

export default Button;
```

> App.js

```javascript
import React from "react";
import styled, { ThemeProvider } from "styled-components";
import Button from "./components/Button";

const AppBlock = styled.div`
  width: 512px;
  margin: 0 auto;
  margin-top: 4rem;
  border: 1px solid #000;
  padding: 1rem;
`;

const ButtonGroup = styled.div`
  & + & {
    margin-top: 1rem;
  }
`;

const palette = {
  blue: "#228be6",
  gray: "#505566",
  pink: "#f06595",
};

function App() {
  return (
    <ThemeProvider
      theme={{
        palette,
      }}
    >
      <AppBlock>
        <ButtonGroup>
          <Button size="large">BUTTON</Button>
          <Button color="pink">BUTTON</Button>
          <Button color="gray" size="small">
            BUTTON
          </Button>
        </ButtonGroup>
        <ButtonGroup>
          <Button size="large" outline>
            BUTTON
          </Button>
          <Button color="pink" outline>
            BUTTON
          </Button>
          <Button color="gray" size="small" outline>
            BUTTON
          </Button>
        </ButtonGroup>
        <ButtonGroup>
          <Button size="large" fullWidth>
            BUTTON
          </Button>
          <Button color="pink" size="large" fullWidth>
            BUTTON
          </Button>
          <Button color="gray" size="large" fullWidth>
            BUTTON
          </Button>
        </ButtonGroup>
      </AppBlock>
    </ThemeProvider>
  );
}

export default App;
```

위와 같이 수정하고나면 아래와 같은 화면을 볼 수 있다. 아, 참고로 fullWidth안에서의 &+&이 작동이 잘 안되더라.. 일단 !important핵을 사용하여 마무리 해놓았다.  
![리액트화면](/images/200915-3.png)
오늘은 여기까지..  
시청 영상 31강 11~12까지

![수강인증이미지](/images/200915-4.jpeg)
프론트엔드 개발 올인원 패키지 with React Online. 👉 https://bit.ly/31Cf1hp
