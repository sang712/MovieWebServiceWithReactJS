# The Basics of React
## 1. 바닐라 자바스크립트로 카운터 버튼 만들기
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
