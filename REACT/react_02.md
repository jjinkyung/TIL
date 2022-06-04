### REACT STUDY_02

---

> 모든 것을 렌더링하지 않고 변하는 부분만 렌더링하기

- **state가 바뀌면 리렌더링이 일어남**
- vanilla js를 대체했음
- html 요소를 생성하거나 찾을 필요 없음
- 이벤트 리스너를 더해줄 필요 없음
- UI 업데이트 해줄 필요 없음



**바로 html을 만들고 이벤트 리스너를 더해줌, UI를 업데이트하면 자동으로 리렌더링**

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
    function App() {
      // state: 데이터가 저장되는 곳, React.useState(0): 초기값인 0과 이 data의 값을 바꿀 수 있는 함수가 들어있는 배열
      // setCount로 새로운 값을 가진 것을 재생성(리렌더링) 하고 있음, state가 바뀌면 리렌더링
      let [count, setCount] = React.useState(0)
      const onClick = () => {
        setCount(count +1) // 원래 count에서 setCount로 바꿔서 보여줌, 자동 리렌더링
      }
      // 사용자가 보게될 컴포넌트
      return (
        <div>
          <h2>Click : {count}</h2>
          <button onClick={onClick}>click me</button>
        </div>
      )
    } 
    ReactDOM.render(<App />, root) // 사용자에게 보여준다
 </script>
</html>
```

