## 📖Redux (리덕스)
- JavaScript 상태관리 라이브러리 (Node.js 모듈)
- **props 없이** 컴포넌트 간 state를 공유할 수 있게 도와줌
- [Context API](https://velog.io/@keynene/React-Context-API)를 개선한 라이브러리
- Context API와 마찬가지로 컴포넌트가 수없이 많아질 수록 용이

* * *

### ❗Redux 동작원리
1. Redux 라이브러리(toolkit)설치 ```npm install @reduxjs/toolkit react-redux```
2. store.js 파일 분리 (state 저장소 분리) : state 관리가 수월해짐
3. redux 사용 설정
   : store.js와 store.js 내 state를 사용할 파일에 redux import, index.js Provider 세팅
4. store.js에 ```createSlice()```로 state를 생성
5. ```createSlice()```의 ```reducer```에 state변경 함수(**action**) 생성
   : 1개의 state(createSlice())안에 여러 개 state변경 함수 생성 가능
6. store.js에 ```configureStore()```선언 후 ```reducer```에 통해 state등록 후 **export**
   : redux를 **import** 및 ```useSelector()```한 파일에서는 해당 state를 언제/어디서든 사용/변경 가능
7. action도 JS 디스트럭쳐링 문법으로 **export**하면 언제/어디서든 사용/변경 가능
   : ex ) ```export let { export할 action들 여러 개 등록 가능 } = state명.actions``` 
8. state를 사용할 파일에서 ```useSelector()```와 ```useDispatch()```를 이용하여 state 사용

* * *
   
### 📌주요함수
#### store.js에서 사용하는 함수
- createSlice() : store.js에 state생성해주는 함수 / reducer : 해당 state 변경해주는 action 생성
- configureStore() reducer : store.js에 있는 모든 state 저장 및 등록 (export하면 여러 곳에서 사용가능)

#### state 사용할 파일에서 사용하는 함수
- useSelector() : store.js에 저장되어 있는 state 가져오기 (주로 변수에 저장해서 사용)
   ```let state = useSelector((state)=>{ return state })```
- useDispatch() : useSelector()로 가져온 state의 action(변경함수)들을 호출 (변수에 저장 후 사용)
   ```let dispatch = useDispatch()```
   ```dispatch(action명(state.state명))```

* * *

### 📝Redux 3가지 원칙

#### 1. Single source of truth
- 동일한 데이터는 항상 같은 곳에서 가지고 온다
- **스토어**라는 하나뿐인 데이터 공간이 존재함

#### 2. State is read-only
- React에서는 setState 메소드를 활용해야만 상태 변경 가능함
- Redux에서도 **액션**이라는 객체를 통해서만 상태 변경이 가능함

#### 3. Change are made with pure functions
- 변경은 순수함수로만 가능
- reducer와 연관되는 개념임
- Store(스토어)-Action(액션)-Reducer(리듀서)

[하나몬님 블로그 참고](https://hanamon.kr/redux%EB%9E%80-%EB%A6%AC%EB%8D%95%EC%8A%A4-%EC%83%81%ED%83%9C-%EA%B4%80%EB%A6%AC-%EB%9D%BC%EC%9D%B4%EB%B8%8C%EB%9F%AC%EB%A6%AC/)

* * *

### 💻Redux 설치방법
Redux는 React와 같이 라이브러리이기 때문에 설치해서 사용해야 함

1. 설치하고자 하는 React파일 실행
2. 터미널에서 ```npm install @reduxjs/toolkit react-redux``` 입력
   설치 전 package.json 파일 실행해서 "react", "react-dom"이 18.1 버전 이상인지 확인
```
   "react": "^18.1.0",
   "react-dom": "^18.1.0", ...
```
3. 설치완료 후 index.js파일에서
  ```<BrowswerRouter>```컴포넌트를 ```<Provider>```컴포넌트로 감싸기
  (```<BrowswerRouter>```없으면 ```<App>```컴포넌트 감싸기)
```javascript
  /* index.js */
  import {Provider} from 'react-redux'; //Provier컴포넌트 import 필요
  import store from './store.js'; //store.js 파일 만들어놓고 import
  
  <Provider store={store}>
    <BroswerRouter>
      <App />
    </BroswerRouter>
  </Provider>
```
   
* * *

### 📝Redux 사용방법1 (state)
#### ✏️store.js 파일 만들기 (state들을 보관하는 파일)
####  : createSlice()/configureStore()/useSelector())
```javascript
/* store.js : state들 생성 및 등록 */
import {configureStore, createSlice} from '@reduxjs/toolkit';

//state생성
let state명 = createSlice({
  name : 'state명',
  initialState : 'state값'
})

//state등록
export default configureStore({
  reducer: {
    //이곳에 등록할 state들 모두 입력
    state명 : state명.reducer
  }
})
```

#### ✏️Redux store에 있던 state 사용하기
```javascript
/* state사용할 컴포넌트가 있는 파일 */
import {useSelector} from "react-redux";

function 컴포넌트명(){
  let state사용할이름 = useSelector((state)=>{ return state })
  //let state사용할이름 = useSelector((state) => state) : 위와 같은 문법
  //let state사용할이름 = useSelector((state) => state.특정state명)
  // : store에서 특정 state만 꺼내서 'state사용할이름' 에 저장
  
  return(
    console.log(state사용할이름) //store에 저장되어있는 state 모두 출력
    console.log(state사용할이름.특정state명) //특정 state만 출력
  )
}
```


* * *

### 📝Redux 사용방법2 (action)
#### ✏️store.js 파일 만들기 (state들을 보관하는 파일)
#### useDispatch()
```javascript
/* store.js : state/action 생성 및 등록 */
import {configureStore, createSlice} from '@reduxjs/toolkit';

let state명 = createSlice({
  name : 'state명',
  initialState : 'state값',
  
  reducers : {
    //이곳에 현재 state와 관련된 모든 변경 함수(action) 생성
    action명(state, action){
      //state : 주로 state라고 작명, 해당 state 자체를 가리킴 (객체 느낌)
      //action : 주로 action이라고 작명, 일반 함수에서의 파라미터 역할을 담당
      
      //이곳에 state를 변경할 코드 작성
      state.name = '변경할 state이름' //이런식으로 사용
      state.name = action.payload //action을 사용한 예시
                                  //action사용 시 무조건 .payload를 붙임
    },
    
    action2명(state, action){
      //이렇게 action은 여러 개 선언 가능 (setState보다 더 세세한 기능 구현 가능)
    }
  }
})

```

#### ✏️Redux store에 있던 action 사용하기
```javascript
import { useDispatch, useSelector } from "react-redux";
import { 사용할 action명 } from "../store.js";

function 사용할컴포넌트(){
  (중략)
  let state = useSelector((state)=>{ return state }) // state 가져오기
  let dispatch = useDispatch() //주로 dispatch로 작명한 변수에 저장해서 사용
  
  //dispatch()를 통해 action를 호출
  dispatch(action명(파라미터)) 
  //파라미터는 위에서 생성한 action의 "action"변수를 뜻함
  //"state" 파라미터는 넘기지 않음
}

```
👉🏻 컴포넌트에서 직접 ```setState()```로 변경하는 것이 아니라, store.js에 저장되어 있는
action을 직접 호출함으로써 사용! 
<span style="color:red">== 문제가 생기면 store.js에 저장된 action함수만 고치면 된다는 뜻!</span>

* * *

### 📜장바구니 데이터 state/action 생성/사용하기
#### ✏️store.js에 장바구니 데이터 저장하기
#### cart state의 count를 증가시키는 state 구현해보자
```javascript
/* stroe.js */
import {configureStore, createSlice} from '@reduxjs/toolkit';

//state생성
let cart = createSlice({
  name : 'cart',
  initialState : [
    {id : 0, name : '첫번째상품', count : 2},
    {id : 2, name : '두번째상품', count : 1}
  ],
  //state가 리스트 형식이면 initialState(값저장)에 리스트 그대로 저장!
  
  //action생성 (count 증가 함수)
  reducer : {
    addCount(state, action){
      let index = state.findIndex((x)=> x.id == action.payload )
      //❓findIndex쓰는이유 : 아래 참고
      state[index].count++
    }
  }
})

//cart를 사용하는 파일에 addCount() action export
export let { addCount } = cart.actions 
//state 등록 및 export
export default configureStore({
  reducer: {
    cart : cart.reducer //다른 곳에서 cart로 사용함
  }
})
```
👉🏻 ```createSlice()```로 state를 생성하고, ```configureStore()```의 ```reducer```를 통해 state등록

#### ❓findIndex쓰는이유 
 : 정렬 등으로 인해 state 값이 변경될 경우, 정렬된 데이터의 id값이 아닌 state에 저장되어 있는
   고유의 id값을 가진 index를 찾기 위함

#### ✏️Cart.js에서 store 데이터 불러오기, action 사용하기
```javascript
/* Cart.js */
import {useSelector} from "react-redux";

function Cart(){
  //state라는 변수에 store 저장
  let state = useSelector((state) => { return state })
  
  //map을 이용하여 리스트 자료 개수만큼 출력하기
  return(
    {
      state.cart.map((a,i)=>{
        return(
          <tbody>
            <tr>
              <td>{(i+1)}</td>
  			  //state 사용하기 (출력)
  			  <td>{state.cart[i].name}</td>
			  <td>{state.cart[i].count}</td>

			  //action 사용하기 (변경 : 버튼 클릭 시 count값 증가)
			  <td>
                <button onClick={()=>{ dispatch(addCount(state.cart[i].id)) }}>+</button>
			  </td>
            </tr>
          </tbody>
        )
      })
    }
  )
}
```
👉🏻 ```useSelector()```를 통해 변수에 store를 저장하고, ```변수.state명``` state 출력
👉🏻 map 사용법은 [내 포스팅 : [React] Map(data,i)](https://velog.io/@keynene/ReactMapdatai) ← 여기서 확인!
👉🏻 ```useDispatch()```를 통해 변수에 action을 저장하고, ```dispatch(action명(파라미터))```으로 사용

* * *

### 💡Redux 장단점
#### 장점
1. 중첩해서 사용한 컴포넌트가 많을 때 **props전달 없이** 깔끔하게 store에서 state사용
2. 공유할 state를 store에서 한 번에 확인 및 사용 가능 (관리가 편함)
3. store에 state들이 아무리 많이 쌓여도 props들보다 가시적임
4. state를 변경하는 함수(action)를 다양하게, 여러 개 생성 및 공유할 수 있음

#### 단점
1. 간단한 프로그램이나 컴포넌트가 많이 없을 경우 props가 더 간결함
2. ```useSelector(), configureStore(), createSlice()``` 등 다양한 세팅이 필요함
3. 라이브러리 설치가 필요함
4. action을 호출할 때마다 ```useDispatch()```를 저장한 변수로 호출해야 함