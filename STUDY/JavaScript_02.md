DOM 관련 객체의 상속 구조

- EventTarget : Event Listener를 가질 수 있는 객체가 구현하는 DOM 인터페이스
- Node : 여러가지 DOM 타입들이 상속하는 인터페이스
- Element :  부모ㅇ



DOM 조작

- document.querySelector(selector)
- document.querySelectorAll(selecytor)
- document.creatElement()
- Element.append()
- Node.appendChild()
- Node.innerText()
- Element.innerHTML
- ChildNode.remove()
- Node.removeChild()
- Element.setAttribute(name, value)
- Element.getAttribute(name, value)



Event

- EventTarget.addEventListener()

- target.addEventListener()(type, listener)

  ```
  btn.addEventListener('click', event => {
  	alert('버튼이 클릭되었습니다.')
  })
  
  myTextInput.addEventListener('input', event => {
  	myPtag.innerText = event.target.value // 입력된 값 그대로 다시 나타내기
  	h2Tag.style.color = event.target.value // 입력된 값의 색깔로 나타내기
  })
  ```

- event.preventDefault()
