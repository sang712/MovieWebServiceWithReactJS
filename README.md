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

