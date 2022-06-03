### REACT STUDY_01

---

>  기존의 vanilla js의 코드

```html
<!DOCTYPE html>
<head>
</head>
  <body>
    <span>Click : </span>
    <button id = "btn">Click me</button>
  </body>
  <script>
    let count = 0;
    const button = document.getElementById("btn");
    const span = document.querySelector("span");
    function Click() {
      count = count + 1;
      span.innerText = `Click : ${count}`;
    }
    button.addEventListener("click", Click);
  </script>
</html>
```



> react js를 활용한 코드_ 어려운 버전

```html
<!DOCTYPE html>
<head>
</head>
  <body>
    <div id="root"></div>
  </body>
  <script src="https://unpkg.com/react@17.0.2/umd/react.production.min.js"></script>

  <!-- 모든 react element들을 html body에 둘 수 있도록 함 -->
  <script src="https://unpkg.com/react-dom@17.0.2/umd/react-dom.production.min.js"></script> 
  
  <script>
    const root = document.getElementById("root")
    const h2 = React.createElement("h2", { 
      id: "sexy-span", style: { color: "red" }, onMouseEnter: () => console.log("mouse enter")
    }, "hello") //  첫번째 h2은 html 태그와 같지 않아도 되지만 두번째 h2은 html태그와 똑같은 이름이어야함
    const btn = React.createElement("button", {
      onClick: () => console.log("im clicked")
    }, "click me")
    const container = React.createElement("container", null, [h2, btn])
    ReactDOM.render(container, root) // 사용자에게 보여준다
 </script>
</html>
```



>  react js를 활용한 코드_ JSX로 코드 간편화

```html
<!DOCTYPE html>
<head>
</head>
  <body>
    <div id="root"></div>
  </body>
  <script src="https://unpkg.com/react@17.0.2/umd/react.production.min.js"></script>

  <!-- 모든 react element들을 html body에 둘 수 있도록 함 -->
  <script src="https://unpkg.com/react-dom@17.0.2/umd/react-dom.production.min.js"></script>
  
  <!-- 이 방식은 느림 -->
  <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
  
  <script type="text/babel">
    const root = document.getElementById("root")
    // jsx 코드로 하기, 브라우저가 알 수 있도록 코드 변환을 위해 babel 사용
    function Title() {
      return (
        <h2 id="title" onMouseEnter={() => console.log("mouse enter")}>hello</h2>
      )
    }
    function Button() {
      return (
        <button onClick={() => console.log("im clicked")}>click me</button>
      )
    }
    // 컴포넌트의 글자는 첫글자를 대문자로하기, 소문자면 html 태그라고 생각할 것임
    function Container() {
      return (
        <div>
          <Title />
          <Button />
        </div>
      )
    } 
    ReactDOM.render(<Container />, root) // 사용자에게 보여준다
 </script>
</html>
```

