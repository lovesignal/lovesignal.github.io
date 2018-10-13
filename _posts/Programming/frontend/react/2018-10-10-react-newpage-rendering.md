---
key: 20181010
title: "[React] 새 페이지 렌더링 시 상단에서 시작하기"
excerpt: "리액트는 새 페이지를 렌더링한 후 스크롤을 맨 위로 올려주지 않는다. 그래서 별도로 컴포넌트를 만들어서 설정해주어야 한다."
categories: programming
tag : [react, programming, javascript]
---

리액트는 새 페이지를 렌더링한 후 스크롤을 맨 위로 올려주지 않는다. 그래서 별도로 컴포넌트를 만들어서 설정해주어야 한다.

먼저 `ScrollToTop.js` 컴포넌트를 만든다.

```javascript
import React, { Component } from 'react';
import { withRouter } from 'react-router';

class ScrollToTop extends Component {
  componentDidUpdate(prevProps) {
    if (this.props.location !== prevProps.location) {
      window.scrollTo(0, 0)
    }
  }

  render() {
    return this.props.children
  }
}

export default withRouter(ScrollToTop)
```


`App.js` 파일에 `ScrollToTop` 컴포넌트를 끼워 넣는다. 나의 경우는 아래와 같이 했다.

```javascript
import React from 'react';
import { Switch, Route, Router } from 'react-router-dom';
import { Home, RefundPage, ChatbotPage, NotFoundPage } from '../pages';
import ScrollToTop from './ScrollToTop';
const App = () => {
    return (
        <div>
          <ScrollToTop>  // ScrollToTop으로 각 페이지를 감쌓다.
            <Switch>
                <Route exact path="/" component={Home}/>
                <Route path="/refund" component={RefundPage} />
                <Route path="/refund/:Chatbot?" component={ChatbotPage} />
                <Route component={NotFoundPage} />
            </Switch>
          </ScrollToTop>
        </div>
    );
};

export default App;
```

