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

