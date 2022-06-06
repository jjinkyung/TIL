### REACT STUDY_04

---

> Props

- 부모 컴포넌트로부터 자식 컴포넌트에 데이터를 보낼 수 있게 해주는 방법



###### 함수형 컴포넌트_함수들을 불러내기

```html
 <script type="text/babel">
    const root = document.getElementById("root")
    
    function SaveBtn() {
      return <button>Save Changes</button>
    }
    function ConfirmBtn() {
      return <button>Confirm</button>
    }
    function App() {
      return (
        <div>
          <SaveBtn/>
          <ConfirmBtn/>
        </div>
      )
    } 
    ReactDOM.render(<App />, root) // 사용자에게 보여준다
 </script>
```



###### 버튼의 컴포넌트 하나로 설정값 다르게 하기

```html
 <script type="text/babel">
    const root = document.getElementById("root")
    
  
    function Btn({ banana, big }) {
      return (
        <button
          style={{
            backgroundColor: "tomato",
            color: "white",
            padding: "10px 20px",
            border: 0,
            borderRadius: 10,
            fontSize: big ? 18 : 16 // 받아온 big의 값에 따라 다른 글자 크기
          }}
        >{banana}</button>)
    }
    // 컴포넌트 이름은 맘대로 해도 됨, 여기선 banana로 한 것처럼
    function App() {
      return (
        <div>
          <Btn banana="Save Change" big={true}/>
          <Btn banana="Continue" big={false}/>
        </div>
      )
    } 
    ReactDOM.render(<App />, root) // 사용자에게 보여준다
 </script>
```



###### memo를 사용하여 부모의 바뀐 부분만 리렌더링하기

```html
  <script type="text/babel">
    const root = document.getElementById("root")
    
  
    function Btn({ banana, onClick }) { // prop를 가져와서 적용 시키는 부분
      return (
        <button
          onClick={onClick}
          style={{
            backgroundColor: "tomato",
            color: "white",
            padding: "10px 20px",
            border: 0,
            borderRadius: 10,
          }}
        >{banana}</button>)
    }
    const MemorizedBtn = React.memo(Btn)
    function App() { // 만약 부모 state가 변경되면 모든 자식들은 다시 렌더링됨 그걸 막기 위해 위의 memo를 사용
      const [value, setvalue] = React.useState("Save Change")
      const changeValue = () => setvalue("Revert Change")
      return (
        <div>
          <MemorizedBtn // 이것을 사용함으로써 첫번째 버튼을 눌렀을 때 첫번째 버튼만 렌더링됨
            banana={value} // 컴포넌트 이름은 맘대로 해도 됨, 여기선 banana로 한 것처럼
            onClick={changeValue} // 이 부분의 onClick은 이벤트 리스너가 아님 그냥 prop의 이름일 뿐, 위에서 적용시켜야 함
          />
          <MemorizedBtn banana="Continue"/>
        </div>
      )
    } 
    ReactDOM.render(<App />, root) // 사용자에게 보여준다
 </script>
```



###### prop을 사용할 때 오류가 난 걸 react js는 알려주지 않음, 그래서 PropTypes을 사용하여 console에 경고문 띄우기

```html
<script type="text/babel">
    const root = document.getElementById("root")
  
    function Btn({ text, fontSize = 16 }) { // prop를 가져와서 적용 시키는 부분, fontSize = 14를 넣는 것은 default 값
      return (
        <button
          style={{
            backgroundColor: "tomato",
            color: "white",
            padding: "10px 20px",
            border: 0,
            borderRadius: 10,
            fontSize
          }}
        >{text}</button>)
    }
    // props의 타입이 뭐고 어떤 모양이어야 하는지 설명
    // 이것을 해주면 type 오류가 생겼을 때 console 창에 에러를 보여줄 수 있음
    Btn.propTypes = {
      text: PropTypes.string.isRequired, // isRequired는 입력을 필수로 해야할 때 사용
      fontSize: PropTypes.number
    }
    function App() {
      return (
        <div>
          <Btn text="Save Changes" fontSize={18} />
          <Btn fontSize={"Continue"} />
        </div>
      )
    } 
    ReactDOM.render(<App />, root) // 사용자에게 보여준다
 </script>
```

