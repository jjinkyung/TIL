### REACT STUDY_03

---

>  unit converter

- 단위 변환기라고 생각하면 될 듯

  

###### <시간-분 단위 변환기> script 부분

```html
<script type="text/babel">
    const root = document.getElementById("root")
    function App() {
      const [amount, setAmount] =React.useState()
      const [flipped, setFlipped] = React.useState(false) // 기본을 false로 잡고 플립 버튼을 누를 때마다 바꾸기 위한 state
      const onChange = (event) => {
        setAmount(event.target.value)
      }
      const reset = () => setAmount(0) // 리셋하는 함수 setMinutes의 값을 0으로 바꿔줌
      const onFlip = () => {
        reset() // flipped됐을 때는 0으로 리셋해주기
        setFlipped((current) => !current) // 현재의 값에서 반대로 바꾼 값을 setFlipped로 넣어줌
      }
      return (
        <div>
          <h1>Super Converter</h1>
          <div>
            <label htmlFor="minutes">Minutes</label>
            <input // 분 단위 입력받는 부분
              // flipped가 true일 때 시간을 분 단위로 변경한 값을 보여주고 false일 때 입력받는 값을 보여줌
              value={flipped ? amount*60 : amount} // 어디서든 input의 value를 수정 가능
              id="minutes" 
              placeholder="minutes" 
              type="number"
              onChange={onChange} // 사용자가 input에 새로운 값을 입력할 때마다 state를 업데이트하는 함수
              disabled={flipped} // flipped가 true일 때 비활성화
              />
          </div>
          
          <div>
            <label htmlFor="hours">Hours</label>
            <input // 시간 단위 입력받는 부분
              // flipped가 true일 때 입력받는 값을 보여주고 false일 땐 분을 시간 단위로 변경한 값을 보여줌
              value={flipped ? amount : Math.round(amount/60)} 
              id="hours" 
              placeholder="hours" 
              type="number"
              disabled={!flipped} // flipped가 false일 때 비활성화
              onChange={onChange}
              />
          </div>
          <button onClick={reset}>Reset</button>
          <button onClick={onFlip}>{flipped ? "Turn back" : "Invert"}</button>
        </div>
      )
    } 
    ReactDOM.render(<App />, root) // 사용자에게 보여준다
 </script>
```



###### <여러 옵션들 중 선택할 수 있는 것> script 부분

```html
<script type="text/babel">
    const root = document.getElementById("root")
    function MinutesToHours() {
      const [amount, setAmount] =React.useState()
      const [flipped, setFlipped] = React.useState(false) // 기본을 false로 잡고 플립 버튼을 누를 때마다 바꾸기 위한 state
      const onChange = (event) => {
        setAmount(event.target.value)
      }
      const reset = () => setAmount(0) // 리셋하는 함수 setMinutes의 값을 0으로 바꿔줌
      const onFlip = () => {
        reset() // flipped됐을 때는 0으로 리셋해주기
        setFlipped((current) => !current) // 현재의 값에서 반대로 바꾼 값을 setFlipped로 넣어줌
      }
      return (
        <div>
          <div>
            <label htmlFor="minutes">Minutes</label>
            <input // 분 단위 입력받는 부분
              // flipped가 true일 때 시간을 분 단위로 변경한 값을 보여주고 false일 때 입력받는 값을 보여줌
              value={flipped ? amount*60 : amount} // 어디서든 input의 value를 수정 가능
              id="minutes" 
              placeholder="minutes" 
              type="number"
              onChange={onChange} // 사용자가 input에 새로운 값을 입력할 때마다 state를 업데이트하는 함수
              disabled={flipped} // flipped가 true일 때 비활성화
              />
          </div>
          
          <div>
            <label htmlFor="hours">Hours</label>
            <input // 시간 단위 입력받는 부분
              // flipped가 true일 때 입력받는 값을 보여주고 false일 땐 분을 시간 단위로 변경한 값을 보여줌
              value={flipped ? amount : Math.round(amount/60)} 
              id="hours" 
              placeholder="hours" 
              type="number"
              disabled={!flipped} // flipped가 false일 때 비활성화
              onChange={onChange}
              />
          </div>
          <button onClick={reset}>Reset</button>
          <button onClick={onFlip}>{flipped ? "Turn back" : "Invert"}</button>
        </div>
      )
    } 
    
    function KmToMiles() {
      return <h3>Km to Miles</h3>
    }

    function App() {
      const [index, setIndex] = React.useState("xx") // default값은 xx
      const onSelect = (event) => {
        setIndex(event.target.value)
      }
      return (
        <div>
          <h1>Super Converter</h1>
          <select value={index} onChange={onSelect}>
            <option value="xx">Select your units</option>
            <option value="0">Minutes & Hours</option>
            <option value="1">Km & Miles</option>
          </select>
          <hr/>
          {index === "xx" ? "Please select your units" : null}
          {index === "0" ? <MinutesToHours/> : null}
          {index === "1" ? <KmToMiles/> : null}
        </div>
      )
    } 
    ReactDOM.render(<App />, root) // 사용자에게 보여준다
 </script>
```

