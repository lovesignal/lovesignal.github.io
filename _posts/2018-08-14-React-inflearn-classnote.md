---
layout: post
date: 2018-08-14
title: "[React] 중요 내용 정리"
excerpt: "React ClassNote"
categories: programming
comments: true
tags: [clonecoding, react, javascript]
comments: true
---





# 자식 컴포넌트가 부모한테 값 전달하기

## 배열 데이터 삽입하기

<img src="https://raw.githubusercontent.com/lifeisgouda/img/master/programming/javascript/values.png">

<br>

자식 컴포넌트가 부모한테 값 전달하기 위해서는 App 컴포넌트 내부에서 handleCreate라는 메소드를 만든다. 만든 메소드를 자식컴포넌트에게  `<PhoneForm onCreate={this.handleCreate} />` props로 전달해주고, props로 전달한 함수 `onCreate={...}` 를 호출시켜서 data 값이 App.js 로 들어간다.

<br>

```javascript
// App.js
import React, { Component } from "react";
import "./App.css";
import PhoneForm from "./components/PhoneForm";

class App extends Component {
  id = 0; // id는 렌더링 되는 값이 아니기 때문에 state 값 안에 넣어줄 필요 없음

  state = {
    information: []
  };
  handleCreate = data => {
    const { information } = this.state; // 비구조 할당

    // 불변성 유지. 기존것 기반으로 값 주입. concat
    this.setState({
      information: information.concat({
        ...data,
        id: this.id++

        /* 또는 다른 방법1: 
        name: data.name,
        phone: data.phone,
        id: this.id++

      방법2:
        .concat(Object.assign( {}, data, {
          id: this.id++
        }))
        
      */
      })
      // 비구조할당 안쓰면 this.state.information.concat(data)가 된다.
    });
  };

  render() {
    return (
      <div>
        <PhoneForm onCreate={this.handleCreate} />
        {JSON.stringify(this.state.information)}
      </div>
    );
  }
}

export default App;

```

<br>

```javascript
// PhoneForm.js
import React, { Component } from "react";

class PhoneForm extends Component {
  state = {
    name: "",
    phone: ""
  };

  handleChange = e => {
    this.setState({
      [e.target.name]: e.target.value
    });
  };

  handleSumbit = e => {
    e.preventDefault();
    this.props.onCreate({
      name: this.state.name,
      phone: this.state.phone
    });
    this.setState({
      name: "",
      phone: ""
    });
  };

  render() {
    return (
      <form onSubmit={this.handleSumbit}>
        <input
          name="name"
          placeholder="name"
          onChange={this.handleChange}
          value={this.state.name}
        />
        <input
          name="phone"
          placeholder="phone number"
          onChange={this.handleChange}
          value={this.state.phone}
        />
        <button type="submit">submit</button>
      </form>
    );
  }
}

export default PhoneForm;

```

<br>

<br>

# 베열 렌더링하기

## JavaScript 배열 내장함수 map()

### map()

```javascript
const numbers = [1, 2, 3, 4, 5];
const squared = numbers.map(n => n * n);
console.log(squared); // [1, 4, 9, 16, 25]
```

<br>

### PhoneInfoList 에 적용

```javascript
// App.js
import React, { Component } from "react";
import "./App.css";
import PhoneForm from "./components/PhoneForm";
import PhoneInfo from "./components/PhoneInfo";
import PhoneInfoList from "./components/PhoneInfoList";

class App extends Component {
  id = 0;

  state = {
    information: []
  };
  handleCreate = data => {
    const { information } = this.state; // 비구조 할당

    // 불변성 유지. 기존것 기반으로 값 주입. concat
    this.setState({
      information: information.concat(
        Object.assign({}, data, {
          id: this.id++
        })
      )
    });
  };

  render() {
    return (
      <div>
        <PhoneForm onCreate={this.handleCreate} />
        <PhoneInfoList data={this.state.information} />
      </div>
    );
  }
}

export default App;
```

<br>

```javascript
// PhoneForm.js
import React, { Component } from "react";

class PhoneForm extends Component {
  state = {
    name: "",
    phone: ""
  };

  handleChange = e => {
    this.setState({
      [e.target.name]: e.target.value
    });
  };

  handleSumbit = e => {
    e.preventDefault();
    this.props.onCreate({
      name: this.state.name,
      phone: this.state.phone
    });
    this.setState({
      name: "",
      phone: ""
    });
  };

  render() {
    return (
      <form onSubmit={this.handleSumbit}>
        <input
          name="name"
          placeholder="name"
          onChange={this.handleChange}
          value={this.state.name}
        />
        <input
          name="phone"
          placeholder="phone number"
          onChange={this.handleChange}
          value={this.state.phone}
        />
        <button type="submit">submit</button>
      </form>
    );
  }
}

export default PhoneForm;
```

<br>

```javascript
// PhoneInfo.js
import React, { Component } from "react";

class PhoneInfo extends Component {
  render() {
    const { name, phone, id } = this.props.info;

    const style = {
      border: "1px solid black",
      padding: "8px",
      margin: "8px"
    };

    return (
      <div style={style}>
        <div>
          <b>{name}</b>
        </div>
        <div>{phone}</div>
      </div>
    );
  }
}

export default PhoneInfo;
```

<br>

```javascript
// PhoneInfoList.js 
import React, { Component } from "react";
import PhoneInfo from "./PhoneInfo";

class PhoneInfoList extends Component {
  static defaultProps = {
    data: []
  };
  render() {
    const { data } = this.props;

    const list = data.map(info => <PhoneInfo info={info} key={info.id} />);
    return <div>{list}</div>;
  }
}

export default PhoneInfoList;
```

<br>

### 배열 렌더링, key

#### key가 없다면?

key가 없으면 순차적으로 모든 값이 바뀌게 된다. <u>key가 있으면 해당 값만 사이에 끼어들거나 삭제되게 된다.</u> 

<br>

<br>

## 배열 데이터 삭제하기

불변성 유지하면서 작업 처리 필요. `.slice`, `.filter` 사용.

<br>

### .slice

기존의 배열 건드리지 않음( 불변성 지킴 )

```javascript
const numbers = [1, 2, 3, 4, 5];
numbers.slice(0, 2);
// [1, 2]     기존의 numbers 배열은 건드리지 않음

numbers.slice(0, 2).concat(numbers.slice(3, 5))
// [1, 2, 4, 5]   3을 제외한 값 출력 가능

[
    ...numbers.slice(0, 2),
    10,
    ...numbers.slice(3, 5)
]
// [1, 2, 10, 4, 5]
```

<br>

### .filter

기존의 배열 건드리지 않음( 불변성 지킴 )

```javascript
const numbers = [1, 2, 3, 4, 5];
numbers.filter(n => n > 3);
// [4, 5]

numbers.filter(n => n !== 3);
// [1, 2, 4, 5]
```

<br>

### 적용 : 데이터 삭제

```javascript
// App.js
import React, { Component } from "react";
import "./App.css";
import PhoneForm from "./components/PhoneForm";
import PhoneInfo from "./components/PhoneInfo";
import PhoneInfoList from "./components/PhoneInfoList";

class App extends Component {
  id = 0;

  state = {
    information: []
  };
  handleCreate = data => {
    const { information } = this.state; // 비구조 할당

    // 불변성 유지. 기존것 기반으로 값 주입. concat
    this.setState({
      information: information.concat(
        Object.assign({}, data, {
          id: this.id++
        })
      )
    });
  };

  handleRemove = (id) => {
    const { information } = this.state;
    this.setState({
      information: information.filter(info => info.id !== id)
    });
  }

  render() {
    return (
      <div>
        <PhoneForm onCreate={this.handleCreate} />
        <PhoneInfoList 
          data={this.state.information} 
          onRemove={this.handleRemove}
        />

      </div>
    );
  }
}

export default App;
```

<br>

```javascript
// PhoneForm.js
import React, { Component } from "react";

class PhoneForm extends Component {
  state = {
    name: "",
    phone: ""
  };

  handleChange = e => {
    this.setState({
      [e.target.name]: e.target.value
    });
  };

  handleSumbit = e => {
    e.preventDefault();
    this.props.onCreate({
      name: this.state.name,
      phone: this.state.phone
    });
    this.setState({
      name: "",
      phone: ""
    });
  };

  render() {
    return (
      <form onSubmit={this.handleSumbit}>
        <input
          name="name"
          placeholder="name"
          onChange={this.handleChange}
          value={this.state.name}
        />
        <input
          name="phone"
          placeholder="phone number"
          onChange={this.handleChange}
          value={this.state.phone}
        />
        <button type="submit">submit</button>
      </form>
    );
  }
}

export default PhoneForm;
```

<br>

```javascript
// PhoneInfo.js
import React, { Component } from "react";

class PhoneInfo extends Component {

    handleRemove = () => {
        const { info, onRemove } = this.props;
        onRemove(info.id);
    }
  render() {
    const { name, phone } = this.props.info;

    const style = {
      border: "1px solid black",
      padding: "8px",
      margin: "8px"
    };

    return (
      <div style={style}>
        <div><b>{name}</b></div>
        <div>{phone}</div>
        <button onClick={this.handleRemove}>삭제</button>
      </div>
    );
  }
}

export default PhoneInfo;
```

<br>

```javascript
// PhoneInfoList.js
import React, { Component } from "react";
import PhoneInfo from "./PhoneInfo";

class PhoneInfoList extends Component {
  static defaultProps = {
    data: []
  };
  render() {
    const { data, onRemove } = this.props;

    const list = data.map(info => (
      <PhoneInfo 
        onRemove={onRemove} 
        info={info} 
        key={info.id} 
      />
    ));
    return <div>{list}</div>;
  }
}

export default PhoneInfoList;
```

<br>

<br>

## 배열 안의 데이터 수정하기

배열 안의 데이터 수정할 때는 `.slice` , `.map` 을 사용할 수 있다.

<br>

### .slice

```javascript
const numbers = [1, 2, 3, 4, 5];
[
    ...numbers.slice(0, 2),
    9,
    ...numbers.slice(3, 5)
]
```

<br>

### .map

```javascript
const numbers = [1, 2, 3, 4, 5];
numbers.map(n => {
    if(n === 3) {
        return 9;
    } return n;
});
```

<br>

### 적용

```javascript
// App.js
import React, { Component } from "react";
import "./App.css";
import PhoneForm from "./components/PhoneForm";
import PhoneInfo from "./components/PhoneInfo";
import PhoneInfoList from "./components/PhoneInfoList";

class App extends Component {
  id = 0;

  state = {
    information: []
  };
  handleCreate = data => {
    const { information } = this.state; // 비구조 할당

    // 불변성 유지. 기존것 기반으로 값 주입. concat
    this.setState({
      information: information.concat(
        Object.assign({}, data, {
          id: this.id++
        })
      )
    });
  };

  handleRemove = (id) => {
    const { information } = this.state;
    this.setState({
      information: information.filter(info => info.id !== id)
    });
  }

  handleUpdate = (id, data) => {
    const { information } = this.state; // 비구조화 할당 통해서 information에 대한 레퍼런스 가져옴
    this.setState({
      information: information.map(
        info => {
          if(info.id === id) {
            return {
              id,
              ...data,
            };
          }
          return info;
        }
      )
    })
  }

  render() {
    return (
      <div>
        <PhoneForm onCreate={this.handleCreate} />
        <PhoneInfoList 
          data={this.state.information} 
          onRemove={this.handleRemove}
          onUpdate={this.handleUpdate}
        />

      </div>
    );
  }
}

export default App;

```

<br>

```javascript
// PhoneForm.js
import React, { Component } from "react";

class PhoneForm extends Component {
  state = {
    name: "",
    phone: ""
  };

  handleChange = e => {
    this.setState({
      [e.target.name]: e.target.value
    });
  };

  handleSumbit = e => {
    e.preventDefault();
    this.props.onCreate({
      name: this.state.name,
      phone: this.state.phone
    });
    this.setState({
      name: "",
      phone: ""
    });
  };

  render() {
    return (
      <form onSubmit={this.handleSumbit}>
        <input
          name="name"
          placeholder="name"
          onChange={this.handleChange}
          value={this.state.name}
        />
        <input
          name="phone"
          placeholder="phone number"
          onChange={this.handleChange}
          value={this.state.phone}
        />
        <button type="submit">submit</button>
      </form>
    );
  }
}

export default PhoneForm;
```

<br>

```javascript
// PhoneInfo.js
import React, { Component, Fragment } from "react";

class PhoneInfo extends Component {

    state = {
        editing: false,
        name: '',
        phone: '',
    }

    handleRemove = () => {
        const { info, onRemove } = this.props;
        onRemove(info.id);
    }

    handleToggleEdit = () => { // editing 값을 반전시킴. f -> t, t -> f
        // true -> false
          // onUpdate
        // false -> true
          // state에 info 값들 넣어주기
        const { info, onUpdate } = this.props;
        if (this.state.editing) {
            onUpdate(info.id, {
                name: this.state.name,
                phone: this.state.phone
            });
        } else {
            this.setState({
                name: info.name,
                phone: info.phone,
            });
        }

        this.setState({
            editing: !this.state.editing,
        })
    }

    handleChange = (e) => {
        this.setState({
            [e.target.name]: e.target.value
        })
    }

  render() {
    const { name, phone } = this.props.info;
    const { editing } = this.state;

    const style = {
      border: "1px solid black",
      padding: "8px",
      margin: "8px"
    };

    return (
      <div style={style}>
        {
            editing ? (
                <Fragment>
                  <div>
                      <input
                        name="name"
                        onChange={this.handleChange} 
                        value={this.state.name}
                      />
                  </div>
                  <div>
                      <input
                        name="phone"
                        onChange={this.handleChange} 
                        value={this.state.phone}
                      />
                  </div>
                </Fragment>
            ) : (
                <Fragment>
                  <div><b>{name}</b></div>
                  <div>{phone}</div>
                </Fragment>
            )
        }
        <button onClick={this.handleRemove}>삭제</button>
        <button onClick={this.handleToggleEdit}>
          { editing ? '적용' : '수정' }
        </button>
      </div>

    );
  }
}

export default PhoneInfo;
```

<br>

```javascript
// PhoneInfoList.js
import React, { Component } from "react";
import PhoneInfo from "./PhoneInfo";

class PhoneInfoList extends Component {
  static defaultProps = {
    data: []
  };
  render() {
    const { data, onRemove, onUpdate } = this.props;

    const list = data.map(info => (
      <PhoneInfo 
        onRemove={onRemove} 
        onUpdate={onUpdate}
        info={info} 
        key={info.id} 
      />
    ));
    return <div>{list}</div>;
  }
}

export default PhoneInfoList;
```

<br>

<br>

# 최적화, 활용, Ref

## shouldComponentUpdate를 통한 최적화. 불변성을 왜 유지하는가

### 불변성을 왜 유지하는가?

불필요한 렌더링을 막아서 최적화 시킬 수 있다. `shouldComponentUpdate` 를 통해서 업데이트가 불필요할 때는 업데이트를 하지 않도록 해줘야 한다. 이 경우 `PhoneInfo.js` 에 `shouldComponentUpdate` 를 구현한다. 

<br>

### 컴포넌트 업데이트 성능 최적화

현재의 props와 nextProps의 값을 비교해서 다를 때 업데이트 하게 만든다.

```javascript
// PhoneInfo.js
(...)
 
shouldComponentUpdate(nextProps, nextState) {
    if (this.state !== nextState) {   // 현재의 props와 nextProps의 값을 비교
        return true;
    }
    return this.props.info !== nextProps.info; // 동일하면 렌더함수 다시 호출 안함
}

(...)
```

<br>

<br>

## 이름으로 전화번호 찾기

```javascript
// App.js
state = {
  (...)
  keyword: '',      // keyword 생성
};

handleChange = (e) => {     // hadleChange 함수 구현
  this.setState({
    keyword: e.target.value,
  })
}
(...)
render() {
  return (
    <div>
      (...)
      <input        // Serach 만들고 연결
        value={this.state.keyword}
        onChange={this.handleChange}
        placeholder="Search"
      />
      <PhoneInfoList   
        data={this.state.information.filter(  // filter 구현
          info => info.name.indexOf(this.state.keyword) > -1
        )} 
        (...)
      />

    </div>
  );
}
```

<br>

<br>

## Ref를 통하여 DOM에 직접 접근하기

입력후 focus를 name에 있게 변경하기.  ref를 통해서 DOM에 직접 접근해야 한다. 

아래 코드에 직접 접근해야 한다. 이때 ref를 사용.

```javascript
// PhoneForm.js
 (...)
<input
  name="name"
  placeholder="name"
  onChange={this.handleChange}
  value={this.state.name}
/>
 (...)
```

<br>

### ref 사용 방법 두가지

#### 1. 함수 사용

`ref={ function }` 라는 값에 함수를 작성한다. 이 함수는 `ref` 를 `parameter` 로 받아서 이 컴포넌트의 멤버 변수로 `ref` 값을 넣어주는 작업을 한다.

<br>

```javascript
// PhoneForm.js
(...)
 
class PhoneForm extends Component {
  input = null;
 
 (...)

  render() {
    return (
      <form onSubmit={this.handleSumbit}>
        <input
          name="name"
          placeholder="name"
          onChange={this.handleChange}
          value={this.state.name}
          ref={ref => this.input = ref}   // ref 함수
  (...)
```

  `this.input` 은 상단의 `input` 인데 rendering 되면 `input = ref` 에 의해서  값이 `ref` 가 된다.

<br>

```javascript
// PhoneForm.js
  handleSubmit = e => {
    (...)
    this.input.focus();
  };
```

HandleSubmit 이 발생했을 때 `input` DOM에 직접적으로 접근 해서 `focus()` 를 찾는다.

<br>

#### 2. `React.createRef()` 사용

```javascript
// PhoneForm.js
(...)
 
class PhoneForm extends Component {
  input = React.createRef();   // React.createRef();

 (...)
  
    handleSubmit = e => {
     (...)
    this.input.current.focus();  // current.focus()
    };

 (...)

  render() {
    return (
        (...)
          ref={this.input}   // ref 함수
  (...)
```

`React.createRef()` 를 이용하면 `current` 를 통해서 해당 DOM에 접근 가능하다. 그러므로 `this.input.current.focus()` 로 작성한다.

<br>

<br>

# 전체코드 정리

```javascript
// App.js
import React, { Component } from "react";
import "./App.css";
import PhoneForm from "./components/PhoneForm";
import PhoneInfo from "./components/PhoneInfo";
import PhoneInfoList from "./components/PhoneInfoList";

class App extends Component {
  id = 3;

  state = {
    information: [
      {
        id: 0,
        name: 'Gouda',
        phone: '010-0000-0001'
      },
      {
        id: 1,
        name: '자두',
        phone: '010-0000-0002'
      },
      {
        id: 2,
        name: '돌돌이',
        phone: '010-0000-0003'
      }
    ],
    keyword: '',
  };

  handleChange = (e) => {
    this.setState({
      keyword: e.target.value,
    })
  }

  handleCreate = data => {
    const { information } = this.state; // 비구조 할당

    // 불변성 유지. 기존것 기반으로 값 주입. concat
    this.setState({
      information: information.concat(
        Object.assign({}, data, {
          id: this.id++
        })
      )
    });
  };

  handleRemove = (id) => {
    const { information } = this.state;
    this.setState({
      information: information.filter(info => info.id !== id)
    });
  }

  handleUpdate = (id, data) => {
    const { information } = this.state; // 비구조화 할당 통해서 information에 대한 레퍼런스 가져옴
    this.setState({
      information: information.map(
        info => {
          if(info.id === id) {
            return {
              id,
              ...data,
            };
          }
          return info;
        }
      )
    })
  }

  render() {
    return (
      <div>
        <PhoneForm onCreate={this.handleCreate} />
        <input 
          value={this.state.keyword}
          onChange={this.handleChange}
          placeholder="Search"
        />
        <PhoneInfoList 
          data={this.state.information.filter(
            info => info.name.indexOf(this.state.keyword) > -1
          )} 
          onRemove={this.handleRemove}
          onUpdate={this.handleUpdate}
        />

      </div>
    );
  }
}

export default App;
```

<br>

```javascript
// PhoneForm.js
import React, { Component } from "react";

class PhoneForm extends Component {
  input = React.createRef();
  state = {
    name: "",
    phone: ""
  };

  handleChange = e => {
    this.setState({
      [e.target.name]: e.target.value
    });
  };

  handleSubmit = e => {
    e.preventDefault();
    this.props.onCreate({
      name: this.state.name,
      phone: this.state.phone
    });
    this.setState({
      name: "",
      phone: ""
    });
    this.input.current.focus();
  };

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <input
          name="name"
          placeholder="name"
          onChange={this.handleChange}
          value={this.state.name}
          ref={this.input}
        />
        <input
          name="phone"
          placeholder="phone number"
          onChange={this.handleChange}
          value={this.state.phone}
        />
        <button type="submit">submit</button>
      </form>
    );
  }
}

export default PhoneForm;
```

<br>

```javascript
// PhoneInfo.js
import React, { Component, Fragment } from "react";

class PhoneInfo extends Component {

    state = {
        editing: false,
        name: '',
        phone: '',
    }

    shouldComponentUpdate(nextProps, nextState) {
        if (this.state !== nextState) {
            return true;
        }
        return this.props.info !== nextProps.info;   
        // 동일하면 렌더함수 다시 호출 안함
    }

    handleRemove = () => {
        const { info, onRemove } = this.props;
        onRemove(info.id);
    }

    handleToggleEdit = () => { // editing 값을 반전시킴. f -> t, t -> f
        // true -> false
          // onUpdate
        // false -> true
          // state에 info 값들 넣어주기
        const { info, onUpdate } = this.props;
        if (this.state.editing) {
            onUpdate(info.id, {
                name: this.state.name,
                phone: this.state.phone
            });
        } else {
            this.setState({
                name: info.name,
                phone: info.phone,
            });
        }

        this.setState({
            editing: !this.state.editing,
        })
    }

    handleChange = (e) => {
        this.setState({
            [e.target.name]: e.target.value
        })
    }

  render() {
    const { name, phone } = this.props.info;
    const { editing } = this.state;

    const style = {
      border: "1px solid black",
      padding: "8px",
      margin: "8px"
    };

    console.log(name);

    return (
      <div style={style}>
        {
            editing ? (
                <Fragment>
                  <div>
                      <input
                        name="name"
                        onChange={this.handleChange} 
                        value={this.state.name}
                      />
                  </div>
                  <div>
                      <input
                        name="phone"
                        onChange={this.handleChange} 
                        value={this.state.phone}
                      />
                  </div>
                </Fragment>
            ) : (
                <Fragment>
                  <div><b>{name}</b></div>
                  <div>{phone}</div>
                </Fragment>
            )
        }
        <button onClick={this.handleRemove}>삭제</button>
        <button onClick={this.handleToggleEdit}>
          { editing ? '적용' : '수정' }
        </button>
      </div>

    );
  }
}

export default PhoneInfo;
```

<br>

```javascript
// PhoneInfoList.js
import React, { Component } from "react";
import PhoneInfo from "./PhoneInfo";

class PhoneInfoList extends Component {
  static defaultProps = {
    data: []
  };
  render() {
    const { data, onRemove, onUpdate } = this.props;

    console.log('rendering list');

    const list = data.map(info => (
      <PhoneInfo 
        onRemove={onRemove} 
        onUpdate={onUpdate}
        info={info} 
        key={info.id} 
      />
    ));
    return <div>{list}</div>;
  }
}

export default PhoneInfoList;
```

