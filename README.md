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

| 바닐라 JS                                                    | 리액트 JS |
| ------------------------------------------------------------ | --------- |
| ![image-20220329165228649](C:\Users\SSAFY\AppData\Roaming\Typora\typora-user-images\image-20220329165228649.png) |           |



### 2. 좋은 방법으로 사용하기

#### setState() 함수로 count 기능 구현하기

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
    function App() {
      /* 1. counter와 counter의 modify 함수 선언 */
      const [counter, setCounter] = React.useState(0);
      /* 2. countUp 함수 선언 */
      const countUp = () => {
        // setCounter(counter + 1);
        setCounter((current) => current + 1);
      };
      return (
      	<div>
      	  <h3>Total clicks: {counter}</h3>
      	  <button onClick={countUp}>Click me</button>
      	</div>
      );
    }
    ReactDOM.render(<App />, root);
  </script>
</html>
```

#### 정리

* React.useState() 함수는 인자를 1개를 받아서 [인자, 인자 정의함수]를 반환하는 함수임
* useState를 이용해서 만들어진 함수에는 인자를 변환시키는 부분과 렌더를 하는 부분을 포함하고 있음
* 관례적으로 `const [variableName, setVariableName] = React.useState(0)`과 같은 식으로 정의함
* `set함수`를 사용할 때 직전의 값을 사용하고 싶다면 `setCounter(counter + 1)` 보다는 `setCounter(current => current + 1)`로 사용하는 것이 더 정확한 결과를 얻을 수 있음
  * `set함수`의 첫번째 인자는 set 하기 전의 값을 받아 옴
  * 관례적으로 첫번째 인자를 괄호로 감싸서 `setCounter((current) => current + 1)` 과 같이 작성


### 3. input과 같이 사용하기

#### 시간/분 converter 만들기

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
    function MinutesToHours() {
      const [minutes, setMinutes] = React.useState(0);
      const onChange = (event) => {
        console.log(event);
        setMinutes(event.target.value);
      };
      const reset = () => setMinutes(0);
      return (
        <>
          <div>
            <label htmlFor="minutes">Minutes</label>
            <input
              value={minutes}
              id="minutes"
              placeholder="Minutes"
              type="number"
              onChange={onChange}
            />
          </div>
          <div>
            <label htmlFor="hours">Hours</label>
            <input
              value={Math.round(minutes / 60)}
              id="hours"
              placeholder="Hours"
              type="number"
              disabled
            />
          </div>
          <button onClick={reset}>Reset</button>
        </>
      );
    }
    function App() {
      return (
        <div>
          <h1>Super Converter</h1>
          <MinutesToHours />
        </div>
      );
    }
    ReactDOM.render(<App />, root);
  </script>
</html>
```

#### 정리

* JSX에서는 html tag의 프로퍼티 중 클래스를 정해주는 class와  id와 묶어주는 for를 사용하면 안 되고 className과 htmlFor를 사용해야함 이렇게 작성된 코드는 알아서 번역되어 html 상에서는 class, for 로 나타나게 됨
  * `class -> className`/ `for -> htmlFor`
* input 태그에 값을 표현할 때는 value 속성에 값을 넣어서, 바뀔 때를 감지할 때는 onChange 속성에 함수를 넣어 사용함
* onChange 속성에서 불러오는 함수에는 event 인자를 첫 인자로 사용하면 event 객체가 들어가며 `SyntheticBaseEvent`를 반환함
  * `SyntehticBaseEvent`는 한글로 번역하면 합성 이벤트로, 어떤 한 방식으로 최적화된 일종의 가짜 이벤트임
  * 진짜 이벤트를 보고 싶으면 `SyntheticBaseEvent`내부에 존재하는 `nativeEvent` 속성을 확인하면 됨

* 해당 이벤트에서 target에 들어가면 onChange 속성을 갖고 있는 태그의 여러 속성을 확인할 수 있고 value에 접근할 수 있음
* input 태그를 사용하려면
  * onChange 속성에 함수가 들어있어야 input에 입력하는 내용을 저장할 수 있음
  * 저장된 내용을 실시간으로 화면에 반영하기(렌더하기) 위해서 value에 useState로 정의한 변수가 있어야 함
    * onChange 함수가 없으면 input에 입력을 하려고 해도 useState에서 초기 설정한 값 그대로 고정이됨(useState에 초기 설정 값이 없으면 화면상에는 type에 맞는 값이 입력이 되지만 변수에는 저장이 되지 않음)

* useState()에 값 배정을 하지 않고 setState() 함수로 값을 변경하려고 하면 워닝 메시지가 뜸
  * `> Warning: A component is changing an uncontrolled input to be controlled. This is likely caused by the value changing from undefined to a defined value, which should not happen. Decide between using a controlled or uncontrolled input element for the lifetime of the component. More info: https://reactjs.org/link/controlled-components`
* input 속성에 `disabled`를 추가하면 입력이 되지 않도록 만들 수 있음

#### 추가 내용

* react와 reactDOM을 import하는 script 태그에서 production대신 development를 사용하면 배포 모드에서 개발모드로 전환이 됨

  ```jsx
  <script src="https://unpkg.com/react@17.0.2/umd/react.development.js"></script>
    <script src="https://unpkg.com/react-dom@17.0.2/umd/react-dom.development.js"></script>
  ```

* 개발모드에서는 작성된 코드 중에 버그로 이어질 수 있는 요소들을 미리 경고하는 검증 코드가 포함되어 있음

### 3-2. boolean 변수 관리하기

#### switch 기능 구현하기

1. switch 버튼 생성
2. switch 정보를 담을 bool 변수 선언
3. bool 변수를 switch 하는 함수 선언
4. switch 적용

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
    function MinutesToHours() {
      const [amount, setAmount] = React.useState(0);
      /* 2. switch 정보를 담을 boolean 변수 선언 */
      const [flipped, setFlipped] = React.useState(false);
      const onChange = (event) => {
        console.log(event);
        setAmount(event.target.value);
      };
      const reset = () => setAmount(0);
      /* 3. bool 변수를 switch 하는 함수 선언 */ 
      const onFlip = () => {
        reset();
        setFlipped((current) => !current);
      };
      return (
        <>
          <div>
            <label htmlFor="minutes">Minutes</label>
            <input
              /* 5. switch에 따른 값 변경 */
              value={flipped ? amount * 60 : amount}
              id="minutes"
              placeholder="Minutes"
              type="number"
              onChange={onChange}
              /* 4. switch 적용 */
              disabled={flipped}
            />
          </div>
          <div>
            <label htmlFor="hours">Hours</label>
            <input
              /* 5. switch에 따른 값 변경 */
              value={Math.round(flipped ? amount : amount / 60)}
              id="hours"
              placeholder="Hours"
              type="number"
              onChange={onChange}
              /* 4. switch 적용 */
              disabled={!flipped}
            />
          </div>
          <button onClick={reset}>Reset</button>
          /* 1. switch 버튼 생성 */
          <button onClick={onFlip}>Flip</button>
        </>
      );
    }
    function App() {
      return (
        <div>
          <h1>Super Converter</h1>
          <MinutesToHours />
        </div>
      );
    }
    ReactDOM.render(<App />, root);
  </script>
</html>
```

* boolean 변수를 사용할 때 변수의 이름에 whether의 의미를 포함하고 있다면 `variable === true` (`~이라면`), `variable === false` (`~가 아니라면`)과 같이 표현하는 것이 눈으로 이해하기에는 좋음

* switch 변수 `flipped`에 따라 변하는 값을 3항 연산자 `<조건> ? <true일 때 값> : <false일 때 값>` 으로 표현함
* Minutes와 Hours 동일한 State를 공유하고 있으므로 기존에 있는 값을 초기화해주는 reset 함수를 만들어 사용하였음

### 4. State 총 정리

#### 세팅하기

1. select, option 선언
2. select에 사용할 index 선언
3. select에 사용할 onChange 함수 선언
4. index에 따라 보여줄 컴포넌트 설정

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
    function MinutesToHours() {...}
    function KilometerToMiles() {
      return <h3>Kilometer To Miles</h3>;
    }
    function App() {
      /* 2. select에 사용할 index 선언 */
      const [index, setIndex] = React.useState("0");
      /* 3. select에 사용할 onChange 함수 선언 */
      const onSelect = (event) => {
        setIndex(event.target.value);
      };
      return (
        <div>
          <h1>Super Converter</h1>
          /* 1. select, option 선언 */
          <select value={index} onChange={onSelect}>
            <option value="0">Minutes & Hours</option>
            <option value="1">Kilometers & Miles</option>
          </select>
          <hr />
          /* 4. index에 따라 보여줄 컴포넌트 설정 */
          {index === "0" ? <MinutesToHours /> : null}
          {index === "1" ? <KilometerToMiles /> : null}
        </div>
      );
    }
    const root = document.getElementById("root");
    ReactDOM.render(<App />, root);
  </script>
</html>
```

* value 값을 설정할 때 number 값인지, string 값인지 잘 보고 통일해야함
  * `const [index, setIndex] = React.useState("0");`에서 숫자로 사용하면 첫 화면에서 원하는 부분이 나오지 않음

#### 킬로미터/마일 converter 만들기

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
    function MinutesToHours() {
      const [minutes, setMinutes] = React.useState(0);
      const [hours, setHours] = React.useState(0);
      const onMinutesChange = (event) => {
        console.log(event);
        setMinutes(event.target.value);
        setHours(event.target.value / 60);
      };
      const onHoursChange = (event) => {
        setMinutes(event.target.value * 60);
        setHours(event.target.value);
      };
      return (
        <>
          <div>
            <label htmlFor="minutes">Minutes </label>
            <input value={minutes} id="minutes" placeholder="Minutes" type="number" onChange={onMinutesChange} />
            <span>m</span>
          </div>
          <div>
            <label htmlFor="hours">Hours </label>
            <input value={hours} id="hours" placeholder="Hours" type="number" onChange={onHoursChange} />
            <span>h</span>
          </div>
        </>
      );
    }
    function KilometerToMiles() {
      const [kilometer, setKilometer] = React.useState(0);
      const [mile, setMile] = React.useState(0);
      const onKilometerChange = (event) => {
        const kilo = event.target.value;
        setKilometer(kilo);
        setMile(kilo / 1.609);
      };
      const onMileChange = (event) => {
        const mile = event.target.value;
        setMile(mile);
        setKilometer(mile * 1.609);
      };
      return (
        <>
          <div>
            <label for="kilometer">Kilometer </label>
            <input value={kilometer} id="kilometer" placeholder="Kilometer" type="number" onChange={onKilometerChange} />
            <span>km</span>
          </div>
          <div>
            <label for="mile">Mile </label>
            <input value={mile} id="mile" placerholder="Mile" type="number" onChange={onMileChange} />
            <span>mi</span>
          </div>
        </>
      );
    }
    function App() {
      const [index, setIndex] = React.useState("0");
      const onSelect = (event) => {
        setIndex(event.target.value);
      };
      return (
        <div>
          <h1>Super Converter</h1>
          <select value={index} onChange={onSelect}>
            <option value="0">Minutes & Hours</option>
            <option value="1">Kilometers & Miles</option>
          </select>
          <hr />
          {index === "0" ? <MinutesToHours /> : null}
          {index === "1" ? <KilometerToMiles /> : null}
        </div>
      );
    }
    ReactDOM.render(<App />, root);
  </script>
</html>
```

#### 정리

* `MinutesToHours`와 `KilometersToMiles`를 통해 컴포넌트를 따로 분리하는 방법을 배웠는데 이는 코드 격리(code isolation) 또는 캡슐화(encapsulation)라고 함
* 이는 분할 정복(문제를 작은 단위로 쪼개서 해결하는 방법)과도 연관이 있는데 기능들을 컴포넌트로 쪼개서 구현하고 합치는 과정으로 분할 정복과 같은(흡사한?) 과정이라고 할 수 있음

## 5. Props

부모 컴포넌트로부터 자식 컴포넌트에 데이터를 보낼 수 있게 해주는 방법

#### 예시

* 똑같은 스타일이 적용된 2개의 버튼, 다만 안의 텍스트 내용만 다름

```jsx
    function SaveBtn() {
      return <button style={{ backgrounColar: "gold", color: "white", padding: "10px 20px", border: 0, borderRadius: 10 }}>Save Changes</button>;
      }
    function ConfirmBtn() {
      return <button style={{ backgrounColar: "gold", color: "white", padding: "10px 20px", border: 0, borderRadius: 10 }}>Confirm</button>;
      }    
    function App() { 
      return (
        <div>
          <SaveBtn />
          <ConfirmBtn />
        </div>
      );
    }
    const root = document.getElementById("root");
    ReactDOM.render(<App />, root);
```

* 스타일을 통일하기 위해서 하나의 컴포넌트로 만들고 text만 바꾸는 예시

```jsx
    function Btn(props) {
      return <button style={{ backgroundColor: "gold", color: "white", padding: "10px 20px", border: 0, borderRadius: 10 }}>{props.something}</button>;
    }
    function App() {
      return (
        <div>
          <Btn something="Save Changes" />
          <Btn something="Confirm" />
        </div>
      );
    }
    const root = document.getElementById("root");
    ReactDOM.render(<App />, root);
//--------------------------------------------------------//
    function Btn(something) {
      return <button style={{ backgroundColor: "gold", color: "white", padding: "10px 20px", border: 0, borderRadius: 10 }}>{something}</button>;
    }
    function App() {
      return (
        <div>
          <Btn something="Save Changes" />
          <Btn something="Confirm" />
        </div>
      );
    }
    const root = document.getElementById("root");
    ReactDOM.render(<App />, root);

```

* 함수형 컴포넌트의 첫번째 인자는 컴포넌트를 사용하는 부분에서 전달된 값들을 받아오는 객체(props), 만약 사용하지 않는다면 `_` 로 위치만 표시하기도 함

* 지난시간에 이용했던 함수를 만들 때 이벤트를 첫 인자로 받아온 것과 유사함. 단, 함수와 함수 컴포넌트는 다름

* props를 받아올 때 props객체로 받아오는 대신, 중괄호를 이용해 props 객체를 풀어서 받아올 수 있음. 단 이 때의 받아오는 변수의 이름은 전달되는 변수의 이름과 같아야함. 덕분에 풀어서 가져올 때 순서는 바뀌어도 상관없음

  `function name({ something }) return <span>{something}</span>`

* 보통 풀어서 가져오는 것을 선호함

#### Memo

```jsx
function Btn({ text, changeValue }) {
      return (
        <button onClick={changeValue} style={{ backgroundColor: "gold", color: "white", padding: "10px 20px", border: 0, borderRadius: 10 }}>
          {text}
        </button>
      );
    }
	const MemorisedBtn = React.memo(Btn);
    function App() {
      const [value, setValue] = React.useState("Save Changes");
      const changeValue = () => setValue("Revert Changes");
      return (
        <div>
          <MemorisedBtn text={value} changeValue={changeValue} />
          <MemorisedBtn text="Confirm" />
        </div>
      );
    }
    const root = document.getElementById("root");
    ReactDOM.render(<App />, root);
```

* 부모-자식 컴포넌트에서 부모 컴포넌트에 state를 선언해 놓고 자식 컴포넌트에서 해당값을 변경하면 부모의 state가 변경된 것이므로 부모 전체가 re-render됨
* 이것을 막기 위해 React.memo 를 사용함
* 꼭 사용할 필요는 없음
* `onst MemorisedBtn = React.memo(Btn);`와 같이 선언하고 기존 태그 대신`<MemorisedBtn text="Confirm" />`와 같이 대체해서 사용하면 됨

#### Prop Types

* 부모 컴포넌트에서 전달되는 prop의 타입을 지정해주어서 잘못 전달된 값을을 쉽게 캐치할 수 있게 해주는 패키지
* `<script src="https://unpkg.com/prop-types@15.7.2/prop-types.js"></script>`로 CDN을 작성하여 설치가능
* 패키지를 설치하고 html 파일을 실행하면 콘솔창에서 `propTypes`오브젝트에 접근할 수 있고 해당 오브젝트가 갖는 타입을 확인할 수 있음
* 다음과 같이 컴포넌트를 선언한 뒤에 `.propTypes`로 정의 할 수 있고 해당 내용에는 `PropTypes.<타입>` 형태로 작성할 수 있음

```jsx
    function Btn({ text, changeValue, fontSize }) {
      return (
        <button onClick={changeValue} style={{ backgroundColor: "gold", color: "white", padding: "10px 20px", border: 0, borderRadius: 10, fontSize }}>
          {text}
        </button>
      );
    }
    Btn.propTypes = {
      text: PropTypes.string,
      fontSize: PropTypes.number,
    };
```

* 타입이 맞지 않는다면 `Failed prop type: Invalid prop 'fontSize' of type 'string' supplied to 'Btn', expected 'number'.`  과 같이 경고 메시지가 뜸

* 참고: [PropTypes와 함께 하는 타입 검사 – React (reactjs.org)](https://ko.reactjs.org/docs/typechecking-with-proptypes.html)



## 6. Create React App

Create React App을 이용하면 하나의 css파일안에 style 정보를 몰아 넣을 필요없이 각 컴포넌트 별로 css를 나눠서 설정할 수 있음

예시로

```directory
folder
┬-App.js
└-App.module.css
```

이렇게 설정한 module.css를 사용하고자하는 js파일에서 import하여 사용할 수 있고

import한 이름에 프로퍼티 접근하듯이 사용할 수 있음

```js
import myStyle from "./App.module.css"

function App() {
    return (
        // 중략
        <div className={styles.id}>id에는 module.css에서 정의한 id</div>
    );
}
```

이렇게 되면 개발자도구상에서는 {module.css의 이름}-{id의 이름}-{random한 문자열} 형태로 id가 따로 지정이 되며 다른 컴포넌트와 id가 겹칠일이 없어 css도 겹칠일이 없어지게 됨
