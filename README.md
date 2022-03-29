# The Basics of React
## 1. 바닐라 JS로 카운터 버튼 만들기
### 기본 구조 만들기

1. 버튼 html 엘레먼트 생성
2. 버튼을 자바스크립트로 가져오기
3. 버튼이 클릭 됨을 감지하는 이벤트 리스너 작성
4. 이벤트 리스너에서 호출할 함수 생성

```html
<!DOCTYPE html>
<html>
  <body>
    <!-- 1.버튼 html 엘레먼트 생성-->
    <button id="btn">Click me</button>
  </body>
  <script>
    // 2.버튼을 자바스크립트로 가져오기  
    const button = document.getElementById("btn"); 
    // 4.이벤트 리스너에서 호출할 함수 생성
    function hadleClick() { 
      console.log("I have been clicked");
    }
    // 3.버튼이 클릭 됨을 감지하는 이벤트 리스너 작성
    button.addEventListner("click"), handleClick);
  </script>
</html>
```

* 2번 querySelector를 쓰지 않는 이유는 버튼이 여러개일 수 있기 때문에 button 태그에 id를 부여하고 해당 id로 엘레먼트를 가져오은 getElementById를 사용함.
* 3번 버튼 엘레먼트에서 click이라는 이벤트가 발생하면 handleClick이라는 함수를 호출함. 만약 호출하는 함수가 없으면 콘솔에 에러남

### 카운터 만들기

1. span HTML 엘레먼트 생성

2. 자바 스크립트에서 counter 변수 생성

3. 버튼이 클릭되면 호출되는 함수에서 카운터를 1 증가시킴

   3-1. 스크립트 내에서 카운터가 올라가더라도 HTML를 새로고침 해주지 않기 때문에 화면에선 변화가 없음

4. span 태그를 자바스크립트로 가져오기
5. 버튼이 클릭되면 호출되는 함수에서 span의 innerText를 변경하기

```html
<!DOCTYPE html>
<html>
  <body>
    <!-- 1. 스팬 html 엘레먼트 생성 -->
    <span>Total clicks: 0</span>
    <button id="btn">Click me</button>
  </body>
  <script>
    // 2. 자바 스크립트에서 counter 변수 생성
    let counter = 0;
    const button = document.getElementById("btn");
    // 4. span 태그를 자바스크립트로 가져오기
    const span = document.querySelector("span");
    function handleClick() {
      // 3. 버튼이 클릭되면 호출되는 함수에서 카운터를 1 증가시킴
      counter = counter + 1;
      // 5. 버튼이 클릭되면 호출되는 함수에서 span의 innerText를 변경하기
      span.innerText = `Total clicks: ${counter}`;
      console.log("I have been clicked");
    }
    button.addEventListener("click", handleClick);
  </script>
</html>
```

* 5번 innerText를 변경하는 부분에서 \`\` 백틱으로 묶어서 `${}`에 변수를 입력하여 사용할 수 있음

### 정리

자바스크립트에서 동작을 하는 버튼을 만들기 위해서는

1. HTML을 만들고
2.  JavaScript에서 HTML을 가져오고
3. event를 감지해서
4. 데이터를 업데이트하고
5. HTML을 업데이트 한다

**React.JS에서는 더 간편한 방법으로 같은 기능을 구현할 수 있다**

## 2. 리액트 JS로 카운터 버튼 만들기

### 0. 시작하기

React를 다운 받아야 하므로 CDN을 추가하여 다운로드를 대신 하자

```html
<!DOCTYPE html>
<html>
  <body></body>
  <script src="https://unpkg.com/react@17.0.2/umd/react.development.js"></script>
  <script src="https://unpkg.com/react-dom@17.0.2/umd/react-dom.development.js"></script>
  <script></script>
</html>
```

### 1. 리액트를 어려운 방법으로 사용하기 - (1)

#### 리액트로 엘레멘트 생성하기

1. React로 엘레멘트를 하나 생성함
2. ReactDOM으로 렌더를 하면 되는데

   2-1. 렌더를 할 곳을 정해줘야함

3. body 태그에 root라는 id로 div 태그를 하나 생성하고

4. JS에서 엘레멘트를 가져옴
5. ReactDOM으로 렌더함
6. createElement의 두번째 인자를 딕셔너리 형태로 넣으면 property를 설정할 수 있음
7. createElement의 세번째 인자에는 content가 들어감

```html
<!DOCTYPE html>
<html>
  <body>
    <!-- 3. body 태그에 root라는 id로 div 태그를 하나 생성함 -->
    <div id="root"></div>
  </body>
  <script src="https://unpkg.com/react@17.0.2/umd/react.development.js"></script>
  <script src="https://unpkg.com/react-dom@17.0.2/umd/react-dom.development.js"></script>
  <script>
    // 4. JS에서 엘레멘트를 가져옴
    const root = document.getElementById("root");
    // 1. 6. 7. React.createElement(<str:html이름>, {스타일}, <str:컨텐츠>)
    const span = React.createElement(
      "span",
      { id: "my-span", style: { color: "red" } },
      "Hello, I'm a span"
    );
    // 2. 5. ReactDOM으로 렌더함 ReactDOM.render(<렌더할 객체>, <렌더될 공간>)
    ReactDOM.render(span, root);
  </script>
</html>
```

* React.createElement를 사용할 때 앞의 변수 명은 상관 없지만 함수 내부에 사용된 이름은 HTML 태그와 같아야 함.

#### 정리

* 바닐라 JS에서는 HTML을 생성하고 이것을 JS로 가져와서 조작하는 것이고
* 리액트 JS에서는 JS에서 HTML을 생성해 조작하고, 필요한 것이 있으면 HTML로 가서 따로 생성하는 것이다.



### 2. 리액트를 어려운 방법으로 사용하기 - (2)

#### 리액트로 이벤트 다루기

1. 버튼 하나 생성, 프로퍼티 없이(null로), content로는 Click me라는 글씨
2. ReactDOM으로 버튼과 버튼이 들어간 root를 렌더 함
3. 아까 사용한 span태그도 한번에 렌더 하려면
4. div태그를 새로 만들고
5. 그 div 태그에 span태그와 버튼을 넣고
6. 해당 div 태그를 렌더하면 됨
7. 버튼을 누르면 변화하게 하고 싶다면 onClick 함수를 화살표 함수로 property에 넣어서 사용하면 됨
8. 위의 span 태그에도 마우스를 호버하면 반응하도록 onMouseEnter 함수를 사용함

```html
<!DOCTYPE html>
<html>
  <body>
    <div id="root"></div>
  </body>
  <script src="https://unpkg.com/react@17.0.2/umd/react.development.js"></script>
  <script src="https://unpkg.com/react-dom@17.0.2/umd/react-dom.development.js"></script>
  <script>
    const root = document.getElementById("root");
    // 3. 아까 사용한 span태그 수정
    const h3 = React.createElement(
      "h3",
      {
        id: "title",
        // 8. 마우스 호버 이벤트리스너 추가
        onMouseEnter: () => console.log("Mouse entered"),
      },
      "Hello, I'm a span"
    );
    // 1. 버튼 하나 생성, 프로퍼티 없이(null로), content로는 Click me라는 글씨
    const btn = React.createElement(
      "button",
      {
        // 7. 버튼 클릭 이벤트리스너 추가
        onClick: () => console.log("I'm clicked"),
        style: {
          backgroundColor: "tomato",
        },
      },
      "Click me"
    );
    // 4. 5. div태그를 새로 만들기
    const container = React.createElement("div", null, [h3, btn]);
    // 2. 6. ReactDOM으로 버튼과 타이틀이 들어간 div를 root에 넣어 렌더 함
    ReactDOM.render(container, root);
  </script>
</html>
```

* 엘레멘트를 생성할 때 앞의 함수명은 JS에서 불릴 이름이고 함수의 인자로 사용되는 것은 HTML의 태그와 같아야 함
* property에 `style: {}`과 같이 eventLIstener도 `onClick: () => ` 으로 넣을 수 있음

#### 정리

* 지금까지의 과정은 사용자들과 구성요소간의 상호작용들을 위한 작업이며, event로 감지해서 동작을 시킴
* 이 과정을 바닐라JS에서는 4단계 과정을 거쳐야하지만 리액트에서는 한줄의 코드로 줄여서 개발할 수 있음

## 3. JSX 사용하기

위에서 작성한 React 어렵게 사용하기에서 만든 엘레멘트들을 JSX 문법으로 만들어서 비교를 할 예정

단 JSX를 사용하면 브라우저가 못 알아듣기 때문에 이를 번역해주기(React.createElement로)위해 Babel을 사용함

### 시작하기

Babel CDN을 추가

`<script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>` 

하단에 작성된 script 태그의 타입을 지정해 주어야 함 

`<script>`태그를 `<script type="text/babel">` 로 수정

```html
<!DOCTYPE html>
<html>
  <body>
    <div id="root"></div>
  </body>
  <script src="https://unpkg.com/react@17.0.2/umd/react.development.js"></script>
  <script src="https://unpkg.com/react-dom@17.0.2/umd/react-dom.development.js"></script>
  <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
  <script type="text/babel">
    /*
    중략
    */
  </script>
</html>
```

### JSX 문법 사용하기 - 컴포넌트 선언

JSX문법이라고 크게 달라진 것은 없음

* 바로 <>로 태그형식으로 선언할 수 있음 
* 내부에 작성했던 프로퍼티를 `:`으로 관계를 설정하는 것이 아니라 `=`으로 관계를 설정하고`{}`로 우항을 잘 감싸주면 됨
* 각각의 프로퍼티는 `,`로 구분하는 것이 아니라 `공백`으로 구분됨

```js
//JS 문법으로 엘레멘트 생성
const h3 = React.createElement(
  "h3",
  {
    id: "title",
    onMouseEnter: () => console.log("Mouse entered"),
  },
  "Hello, I'm a span"
); 
```

```jsx
//JSX 문법으로 컴포넌트 선언
const Title = () => (
  <h3 id="title" onMouseEnter={() => console.log("Mouse entered")}>
    "Hello, I'm a span"
  </h3>
);
```





엘레멘트를 컨테이너 안에 넣은 채로 createElement하면 됐지만 JSX로 안에 넣으려면 엘레멘트를 함수 형식으로 선언해야함

그래서 화살표함수나 그냥 함수 형태로 선언해야함

### 화살표함수와 일반 함수 형태의 비교

화살표 함수의 형태는 `const Name = () => ();` 꼴이며 화살표 이후의 `();` 안에 html 형식으로 작성함

일반 함수의 형태는 `function name() {}` 꼴이며 function의 `{}` 안에는 `return(내용물);` 로 작성이 됨(세미 콜론으로 끝내야 함)

```jsx
// 화살표 함수
const Title = () => (
  <h3 id="title" onMouseEnter={() => console.log("Mouse entered")}>
    "Hello, I'm a span"
  </h3>
);
```

```jsx
// 함수
function Title() {
  return (
    <h3 id="title" onMouseEnter={() => console.log("Mouse entered")}>
      "Hello, I'm a span"
    </h3>
  );
}
```



### 정리

```jsx
<!DOCTYPE html>
<html>
  <body>
    <div id="root"></div>
  </body>
  <script src="https://unpkg.com/react@17.0.2/umd/react.development.js"></script>
  <script src="https://unpkg.com/react-dom@17.0.2/umd/react-dom.development.js"></script>
  <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
  <script type="text/babel">
    const root = document.getElementById("root");
    // 화살표 함수형 선언
    const Title = () => (
      <h3 id="title" onMouseEnter={() => console.log("Mouse entered")}>
        "Hello, I'm a span"
      </h3>
    );
    /* 기본 함수형 선언
    function Title() {
      return (
        <h3 id="title" onMouseEnter={() => console.log("Mouse entered")}>
          "Hello, I'm a span"
        </h3>
      );
    } 
    */
    /* 바닐라 JS 형태
    const h3 = React.createElement(
      "h3",
      {
        id: "title",
        onMouseEnter: () => console.log("Mouse entered"),
      },
      "Hello, I'm a span"
    ); 
    */
    const Button = () => (
      <button
        style={{ backgroundColor: "tomato" }}
        onClick={() => console.log("I'm clicked")}
      >
        "Click me"
      </button>
    );
    /* 
    const btn = React.createElement(
      "button",
      {
        onClick: () => console.log("I'm clicked"),
        style: {
          backgroundColor: "tomato",
        },
      },
      "Click me"
    ); 
    */
    // 화살표 함수형 중첩 컴포넌트 선언
    const Container = () => (
      <div>
        <Title />
        <Button />
      </div>
    );
    /* 기존 함수형 중첩 엘레멘트 선언
    const container = React.createElement("div", null, [Title, Button]); 
    */
    // 버튼과 타이틀이 들어간 Container를 root에 넣어 렌더 함
    ReactDOM.render(<Container />, root);
  </script>
</html>
```

* JSX 문법으로 Babel한테 코드를 넘겨주면 Babel이 헤드에서 브라우저가 읽을 수있는 코드로 변환하여 헤드에 담아둠
* 함수 안에 태그로 만든 것을 `엘레멘트`, 해당 함수를 `컴포넌트`로 보면 됨 다시말해 이 과정은 createElement()로 생성했던 `엘레멘트`를 함수에 넣어 만들었고, 얼마든지 재사용이 가능하므로 `컴포넌트`로 볼 수 있음
* 단, 이 컴포넌트는 **반드시 대문자로 시작**해야 함, 그렇지 않으면 JSX 태그가 아니라 HTML 태그라고 인식하기 때문
* 컴포넌트를 불러와서 사용하기 위해서는 `<Title />`과 같은 형식으로 추가하면 됨

## 4. State

데이터가 저장되는 곳

### 1. 별로 좋지 않은 방법으로 사용하기

#### count 기능 추가하기

1. counter 선언

2. 선언한 변수를 `{변수명}` 형태로 작성하여 사용하기

3. count 함수 선언

4. 이벤트 리스너 추가

   4-1. 이 과정에서 count는 올라가지만 UI 업데이트가(화면에 렌더)가 되지 않아 0으로 유지되는 상태가 됨

   4-2. `ReactDOM.render(<Container />, root);` 함수가 렌더를 해주는 부분이지만  처음 페이지가 로드될 때만 딱 1번만 호출이 되어 업데이트가 되지 않는 것임

5. count 함수에 다시 렌더하는 구문을 추가함

```jsx
<!DOCTYPE html>
<html>
  <body>
    <div id="root"></div>
  </body>
  <script src="https://unpkg.com/react@17.0.2/umd/react.development.js"></script>
  <script src="https://unpkg.com/react-dom@17.0.2/umd/react-dom.development.js"></script>
  <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
  <script type="text/babel">
    const root = document.getElementById("root");
    /* 1. counter 선언 */
    let counter = 0;
    /* 3. count 함수 선언 */
    function countUp() {
      counter = counter + 1;
      /* 5. 다시 렌더하는 함수를 정의해서 추가 */
      render();
    }
    function render() {
      ReactDOM.render(<Container />, root);
    }
    const Container = () => (
      <div>
        {/* 태그 내에서 주석을 하려면 주석을 {} 감싸줘야함 */}
        {/* 2. 선언한 변수를 사용하려면 그냥 태그 내에서 {변수명} 으로 작성하면 됨 */}
        <h3>Total clicks: {counter}</h3>
        {/* 4. 이벤트 리스너 추가 */}
        <button onClick={countUp}>Click me</button>
      </div>
    );
    render();
  </script>
</html>
```

#### 정리

* 이벤트 콜백 함수에 화면을 렌더해주는 함수를 넣어 그때 그때마다 렌더함
* 리액트는 렌더를 할 때 직전화면과 변하는 화면을 비교하여 변하는 딱 그 부분만 업데이트 함, 그래서 인터액티브한 서비스를 만들기 좋고, 개발자도구 요소창에서도 바뀌는 부분만 확인 할 수 있어 보기 편함

| 바닐라 JS                                                    | 리액트 JS                                                    |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| ![image-20220329165228649](C:\Users\SSAFY\AppData\Roaming\Typora\typora-user-images\image-20220329165228649.png) | ![image-20220329165317889](C:\Users\SSAFY\AppData\Roaming\Typora\typora-user-images\image-20220329165317889.png) |

