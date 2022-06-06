### REACT STUDY_06

---

> useEffect function

- 원하는 코드는 딱 한 번만 실행될 수 있도록 보호해줌
- ex) api를 불러올 때 다른 것들은 계속 렌더링하지만 api를 불러오는 것은 최초에 딱 한 번만 하면 됨



###### useEffect를 사용하여 한 번만 호출하기

```html
import { useState, useEffect } from "react"

function App() {
  const [counter, setValue] = useState(0)
  const onClick = () => setValue((prev) => prev + 1)
  console.log("i run all the time")
  useEffect(() => {
    console.log("i run only once")
  }, [])
  return (
    <div>
      <h1>{counter}</h1>
      <button onClick={onClick}>click me</button>
    </div>
  );
}
export default App;
```





###### search keyword에 변화가 있을 때만 검색하기, 다른 버튼을 누른다고 계속 해서 검색하지 않게 하기

```html
import { useState, useEffect } from "react"

function App() {
  const [counter, setValue] = useState(0)
  const onClick = () => setValue((prev) => prev + 1)
  console.log("i run all the time")
  useEffect(() => {
    console.log("i run only once")
  }, [])
  return (
    <div>
      <h1>{counter}</h1>
      <button onClick={onClick}>click me</button>
    </div>
  );
}
export default App;
```



###### 특정 데이터가 변화할 때 실행하기(위의 것에서 추가)

```html
import { useState, useEffect } from "react"

function App() {
  const [counter, setValue] = useState(0)
  const [keyword, setKeyword] = useState("")
  const onClick = () => setValue((prev) => prev + 1)
  const onChange = (event) => setKeyword(event.target.value)

  // useEffect의 첫번째 요소는 우리가 실행시키고 싶은 코드, 두번째 요소는 react.js가 지켜보다가 변화할 때 코드 실행
  useEffect(() => {
    console.log("I run only once")
  }, []) // [] 빈 array는 딱 한 번만 실행한다는 뜻
  useEffect(() => {
    console.log("I run when 'keyword' changes.");
  }, [keyword]); // [keyword]는 keyword가 변화할 때만 코드를 실행한다는 것
  useEffect(() => {
    console.log("I run when 'counter' changes.");
  }, [counter]) // counter기 변화할 때만 실행
  useEffect(() => {
    console.log("I run when keyword & counter change");
  }, [keyword, counter]) // 둘 중 하나라도 변화할 때 실행
  return (
    <div>
      <input
        value={keyword}
        onChange={onChange}
        type="text"
        placeholder="Search here..."
      />
      <h1>{counter}</h1>
      <button onClick={onClick}>click me</button>
    </div>
  );
}
export default App;
```

