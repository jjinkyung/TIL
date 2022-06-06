### REACT STUDY_05

---

> create-react-app(리액트 어플리케이션을 만드는 방식)

- node.js 설치
- npx create-react-app 앱이름
- npm start
- npm i prop-types



###### 컴포넌트와 스타일을 독립적이게 유지시키키

- App.js

```html
import Button from "./Button" // 버튼 불러오기
import styles from "./App.module.css"

function App() {
  return (
    <div>
      <h1 className={styles.title}>Welcome back!</h1>
      <Button text={"Continue"}/> // 컴포넌트 넣어줌
    </div>
  );
}

export default App;

```



- App.module.css

```html
.title {
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  font-size: 18px;
}
```



- Button.js

```html
import PropTypes from "prop-types"
import styles from "./Button.module.css"

function Button({ text }) {
  return <button className={styles.btn}>{text}</button>
}
Button.propTypes ={
  text: PropTypes.string.isRequired,
}
export default Button
```



- Button.module.css

```html
.btn {
  color: white;
  background-color: tomato;
}
```

