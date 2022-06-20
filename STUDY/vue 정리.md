SPA(Single Page Application) 단일 페이지 어플리케이션

- 페이지를 동적으로 렌더링
- 단일 페이지



CSR(Client Side Rendering) 서버에서 화면을 구성하는 SSR 방식과 달리 클라이언트에서 화면을 구성

- 처음엔 뼈대만 받고 브라우저에서 동적으로 DOM을 그림
- SPA가 사용하는 렌더링 방식
- 장점
  - 서버와 클라이언트 간 트래픽 감소
  - 사용자 경험(UX) 향상
- 단점
  - SSR에 비해 전체 페이지 최종 렌더링 시점이 느림
  - SEO(검색 엔진 최적화)에 어려움이 있음



SSR(Server Side Rendering) 서버에서 클라이언트에게 보여줄 페이지를 모두 구성하여 전달

- 장점
  - 초기 구동 속도가 빠름
  - SEO(검색 엔진 최적화)에 적합
- 단점
  - 모든 요청마다 새로운 페이지를 구성하여 전달



Vue.js

MVVM

- Model
  - Plain JavaScript Object
  - 화면에 표현되는 내용, 데이터
- View
  - DOM
  - 사용자가 보는 화면
- ViewModel
  - View에서 표시할 데이터가 추상화 되는 곳, Model과 상호작용하여 데이터를 주고받음
  - View에서 View Model의 특정 데이터를 참조하여 화면에 표시하도록 정의하고, 
    View Model의 데이터가 바뀌면 그대로 화면에 반영
  - View Model은 데이터만 바꿀 뿐 View와의 직접적 교류는 X



**화살표 함수를 메서드 정의하는 데 사용하면 안 됨, 화살표 함수가 부모 컨텍스트를 바인딩하기 때문에 this는 Vue 인스턴스가 아님**

**임의로 사용자로부터 입력 받은 내용은 v-html에 절대 사용 금지**

v-show : 요소는 항상 렌더링 되고 DOM에 남아있음, 실제로 렌더링은 되지만 눈에 보이지 않는 것이기 때문에 딱 한 번만 렌더링 되는 경우라면 v-if에 비해 상대적으로 렌더링 비용이 높음, 자주 변경되는 요소라면 토글 비용이 적음

iv-if : 전달인자가 false인 경우 렌더링 되지 않음, 화면에 보이지 않을 뿐 아니라 렌더링 자체가 되지 않기 때문에 렌더링 비용이 낮음, 자주 변경되는 요소의 경우 비용 증가

v-if와 함께 사용하는 경우 v-for가 우선순위가 더 높음

computed

- 종속된 데이터가 변경될 때만 함수를 실행
- 반드시 반환 값이 있어야 함
- 데이터를 기반으로 하는 계산된 속성



computed(선언형 프로그래밍 방식 : 계산해야 하는 목표 데이터를 정의) vs methods

- computed는 종속된 대상이 변경되지 않는 한 computed에 작성된 함수를 여러 번 호출해도 계산을 다시하지 않고 계산되어 있던 결과를 반환
- methods를 호출하면 렌더링을 다시 할 때마다 항상 함수를 실행



watch(명령형 프로그래밍 방식 : 데이터가 바뀌면 특저어 함수를 실행해!) : 데이터에 변화가 일어났을 때 실행되는 함수



부모는 props를 통해 자식에게 '데이터'를 전달하고 자식은 events를 통해 부모에게 '메시지'를 보냄

부모는 pass props, 자식은 emit event



컴포넌트 등록 3단계 : 불러오기(import), 등록하기(register), 보여주기(show)



카멜케이스 : 선언할 때

케밥케이스 : template 내



모든 props는 단방향 바인딩을 형성, 부모의 속성이 변경되면 자식 속성에게 전달되지만 반대는 안 됨

![image-20220516022437096](C:\Users\Owner\AppData\Roaming\Typora\typora-user-images\image-20220516022437096.png)부모

![image-20220516022501191](C:\Users\Owner\AppData\Roaming\Typora\typora-user-images\image-20220516022501191.png)자식



![image-20220516022521703](C:\Users\Owner\AppData\Roaming\Typora\typora-user-images\image-20220516022521703.png)자식

![image-20220516022535486](C:\Users\Owner\AppData\Roaming\Typora\typora-user-images\image-20220516022535486.png)부모



![image-20220516023005024](C:\Users\Owner\AppData\Roaming\Typora\typora-user-images\image-20220516023005024.png)router1

![image-20220516023046279](C:\Users\Owner\AppData\Roaming\Typora\typora-user-images\image-20220516023046279.png)router2



SPA 등장 이전 : 서버가 모든 라우팅을 통제, 요청 경로에 맞는 HTML을 제공

SPA 등장 이후 : 서버는 index.html 하나만 제공, 요청에 대한 처리를 더이상 서버가 하지 않음



state : data이며 해당 어플리케이션의 핵심이 되는 요소, 중앙에서 관리하는 모든 상태 정보

mutation 실제로 state를 변경하는 유일한 방법, 동기적이어야 함, 첫번째 인자 항상 state, actions에서 commit 메서드에 의해 호출

actions : state를 변경하는 대신 mutations를 호출해서 실행, context 객체 인자를 받음, 컴포넌트에서 dipatch 메서드에 의해 호출

getter : state를 변경하지 않고 활용하여 계산을 수행(computed)와 유사, state를 변경하지 않음, 계산된 값을 가져옴







npm i vuex-persistedstate

createPersistedState









