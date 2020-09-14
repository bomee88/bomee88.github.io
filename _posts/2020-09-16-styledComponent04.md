---
title: "[패스트캠퍼스 수강 후기] 프론트엔드 인강 100% 환급 챌린지 38회차 미션 - 31강 styled component로 Dialog, Transition 구현하기"
date: 2020-09-16
categories: fastcampus
tags: fastcampus all-in-one-challenge day38 react styled-components
---

# Dialog 만들기

아래 이미지 처럼 취소/확인 등 사용자가 클릭할 수 있는 창을 Dialog라고 한단다. 이번에는 이걸 구현해보도록 하자.

> /src/component/Dialog.js

```javascript
import React from "react";
import styled from "styled-components";
import Button from "./Button";

const DarkBackground = styled.div`
  position: fixed;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  background: rgba(0, 0, 0, 0.8);
`;
const DialogBlock = styled.div`
  width: 320px;
  padding: 1.5rem;
  background: white;
  border-radius: 2px;
  h3 {
    margin: 0;
    font-size: 1.5rem;
  }
  p {
    font-size: 1.125rem;
  }
`;
const ButtonGroup = styled.div`
  margin-top: 3rem;
  display: flex;
  justify-content: flex-end;
`;

const ShortMarginButton = styled(Button)`
  & + & {
    margin-left: 0.5rem;
  }
`;

function Dialog({
  title,
  children,
  confirmText,
  cancelText,
  visible,
  onConfirm,
  onCancel,
}) {
  if (!visible) return null;
  return (
    <DarkBackground>
      <DialogBlock>
        <h3>{title}</h3>
        <p>{children}</p>
        <ButtonGroup>
          <ShortMarginButton color="gray" onClick={onCancel}>
            {cancelText}
          </ShortMarginButton>
          <ShortMarginButton color="pink" onClick={onConfirm}>
            {confirmText}
          </ShortMarginButton>
        </ButtonGroup>
      </DialogBlock>
    </DarkBackground>
  );
}

Dialog.defaultProps = {
  cancelText: "취소",
  confirmText: "확인",
};
export default Dialog;
```

> App.js

```javascript
import React, { useState } from "react";
import styled, { ThemeProvider } from "styled-components";
import Button from "./components/Button";
import Dialog from "./components/Dialog";

const AppBlock = styled.div`
  width: 512px;
  margin: 0 auto;
  margin-top: 4rem;
  border: 1px solid #000;
  padding: 1rem;
`;

const palette = {
  blue: "#228be6",
  gray: "#505566",
  pink: "#f06595",
};

function App() {
  const [dialog, setDialog] = useState(false);
  const onClick = () => {
    setDialog(true);
  };
  const onConfirm = () => {
    console.log("확인");
    setDialog(false);
  };
  const onCancel = () => {
    console.log("취소");
    setDialog(false);
  };

  return (
    <ThemeProvider
      theme={{
        palette,
      }}
    >
      <>
        <AppBlock>
          <Button color="gray" size="small" onClick={onClick}>
            삭제
          </Button>
        </AppBlock>
        <Dialog
          title="삭제합니다."
          confirmText="삭제"
          cancelText="취소"
          onConfirm={onConfirm}
          onCancel={onCancel}
          visible={dialog}
        >
          정말로 삭제하시겠습니까?
        </Dialog>
      </>
    </ThemeProvider> // 하나의 엘리먼트만 허용함
  );
}

export default App;
```

![리액트화면](/images/200916-1.png)
위 처럼 구현이 되는 것을 볼 수 있다.

# Transition 구현하기

이제 Dialog가 부드럽게 나타났다 사라지도록 transition을 구현해보도록 하자.
styled-components에서 keyframes를 사용하려면 상단에서 불러와주고 시작해야한다.  
아래와 같이 Dialog를 수정해보자.

> Dialog.js

```javascript
import React, { useState, useEffect } from "react";
import styled, { keyframes, css } from "styled-components";
import Button from "./Button";

const fadeIn = keyframes`
    from {
        opacity: 0;
    }
    to {
        opacity: 1;
    }
`;

const fadeOut = keyframes`
    from {
        opacity: 1;
    }
    to {
        opacity: 0;
    }
`;

const slideUp = keyframes`
    from {
        transform: translateY(200px);
    }
    to {
        transform: translateY(0px);
    }
`;

const slideDown = keyframes`
    from {
        transform: translateY(0px);
    }
    to {
        transform: translateY(200px);
    }
`;

const DarkBackground = styled.div`
  position: fixed;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  background: rgba(0, 0, 0, 0.8);
  animation-duration: 0.25s;
  animation-timing-function: linear;
  animation-name: ${fadeIn};
  animation-fill-mode: forwards;
  ${(props) =>
    props.disappear &&
    css`
      animation-name: ${fadeOut};
    `}
`;
const DialogBlock = styled.div`
  width: 320px;
  padding: 1.5rem;
  background: white;
  border-radius: 2px;

  h3 {
    margin: 0;
    font-size: 1.5rem;
  }
  p {
    font-size: 1.125rem;
  }
  animation-duration: 0.25s;
  animation-timing-function: linear;
  animation-name: ${slideUp};
  animation-fill-mode: forwards;
  ${(props) =>
    props.disappear &&
    css`
      animation-name: ${slideDown};
    `}
`;
const ButtonGroup = styled.div`
  margin-top: 3rem;
  display: flex;
  justify-content: flex-end;
`;

const ShortMarginButton = styled(Button)`
  & + & {
    margin-left: 0.5rem;
  }
`;

function Dialog({
  title,
  children,
  confirmText,
  cancelText,
  visible,
  onConfirm,
  onCancel,
}) {
  const [animate, setAnimate] = useState(false);
  const [localVisible, setLocalVisible] = useState(visible);
  useEffect(() => {
    // visible true -> false
    if (localVisible && !visible) {
      setAnimate(true);
      setTimeout(() => setAnimate(false), 250);
    }
    setLocalVisible(visible);
  }, [localVisible, visible]);

  if (!localVisible && !animate) return null;
  return (
    <DarkBackground disappear={!visible}>
      <DialogBlock disappear={!visible}>
        <h3>{title}</h3>
        <p>{children}</p>
        <ButtonGroup>
          <ShortMarginButton color="gray" onClick={onCancel}>
            {cancelText}
          </ShortMarginButton>
          <ShortMarginButton color="pink" onClick={onConfirm}>
            {confirmText}
          </ShortMarginButton>
        </ButtonGroup>
      </DialogBlock>
    </DarkBackground>
  );
}

Dialog.defaultProps = {
  cancelText: "취소",
  confirmText: "확인",
};
export default Dialog;
```

이렇게 코드를 구현해주고 나면 아래와 같이 잘 구동되는 것을 볼 수 있다.  
![리액트화면](/images/200916-2.gif)  
이렇게 styled-components까지 모두 끝마쳤다. sass를 사용하든 css module을 사용하든 본인에게 편한것을 사용하면 된다. 나는 개인적으로 styled-components는 한 파일에 css와 js가 같이 있는 구조라서 그닥 좋게 안느껴진다. class명도 자기 마음대로 붙어버려서 디버깅하기도 힘들고.. 난 sass를 써야겠다 ㅎㅎ 그래도 이런게 있다는 건 알게되서 좋은 수업이였다!

오늘은 여기까지..  
시청 영상 31강 13~14까지

![수강인증이미지](/images/200916-3.jpeg)
프론트엔드 개발 올인원 패키지 with React Online. 👉 https://bit.ly/31Cf1hp
