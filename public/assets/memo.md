# React-JSX

## JSX 쓰고 안쓰고의 차이

Jsx를 꼭 사용하지 않아도 되긴하는데 
리액트의 빌드 프로세스는 이론상으로는 JSX의 도움 없이 앱을 빌드 할 수 있다.
빌드 과정이 필요치 않은 플젝이라면 더더욱 JSX를 사용할 필요가 없다.
JSX로 코드로 작성하면 가동성이 좋아진다.

- Requires build process & code transformation
    easy to read & understand
```js
// JSX
<div id= "content">
    <p> hello world!</p>
<div/>
```
- Work without special build process & transformation
    Pretty verbose & not necessarily intuive
```js
// none JSX
React.createElement(
    'div'
    {id: 'content'},
    React.createElement(
        'p',
        null,
        'hello world'
    )
);
```

---
### index.jsx
```js
//index.jsx
import ReactDOM from "react-dom/client";

import App from "./App";
import "./index.css";

const entryPoint = document.getElementById("root");
ReactDOM.createRoot(entryPoint).render(<App />);
```

->

```js
//index.jsx
import React from "react";

import App from "./App";
import "./index.css";

const entryPoint = document.getElementById("root");
ReactDOM.createRoot(entryPoint).render(React.createElement(App));
```



## Fragment 사용법
     == <> <content / > </>
App.jsx에서 App()의 return문은 최초에 `<div>`,`<>`로 감싸져 있다.
그걸 지워보면 에러가 나고 JSX는 부모 요소가 하나 있어야 한다는 안내가 나옴.
이게 쉽게 생각하면 되는게,
원래 함수는 하나의 값을 반환해야하는데
최상위 부모 요소이자 `<div>` 감싸진걸 지우면 반환되는 값이 여러개가 되는거.
App()의 반환값은 하나의 요소여야 한단거는 즉 이 말임. 쉽고 당연한 이치임.

## 컴포넌트를 분리할 때는 언제인가?
컴포넌트를 분리하는 이유 👍
- (가독성 개선, 책임 분리, 협업, 버그 수정과 기능 확장 등) 을 위해.
1. 코드 재사용성이 필요할 때.
- 여러 곳에서 동일한 UI나 로직이 반복되는 경우 (ex.Button,InputField,Card 등의 공통 UI요소들)

2. 컴포넌트가 너무 커질때( 복잡도 관리 ) 
- 파일이 200-300 줄이 넘어가면서 가독성이이 구려질 때
- 한 컴포넌트가 많은 책임을 가질 때

3. 로직이 명확히 구분 될 때
- 특정 기능이나 관심사가 독립적으로 분리된다면 나누는게 좋다. (ex.데이터 필터링,폼 검증, 차트 표시 등)

4. 성능 최적화가 필요할 때
- 특정 부분만 재렌더링하고 싶을 때
- React.memo 나 useMemo를 효과적으로 사용하고 싶을 때

5. 테스트 용이성
- 독립적으로 테스트가 필요한 로직이 있을 떄
- 단위 테스트를 쉽게 작성하기 위해.

     과도한 컴포넌트 분리는 오히려 복잡도를 높힐 수 있으며 적절한 균형을 찾는게 중요하다.


