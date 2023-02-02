## 📖Context API
- 일반적으로 React는 **상위→하위(상속) 컴포넌트**로만 props를 전달할 수 있음
   (자식→자식(근친), 자식→부모(패륜) 불가능 하다고 했음!)
   [내 포스팅 : [React] Props,State](https://velog.io/@keynene/ReactProps)
- **context API**를 이용하면 각 단계마다 명시적으로 props를 넘겨주지 않아도 자식 컴포넌트들이 state 등 값 공유할 수 있음
- 즉, React 컴포넌트 트리 안에서 전역적(global)이라고 볼 수 있는 데이터를 공유할 수 있도록 고안된 방법임

ex) 1노드에 있는 state를 5노드에서 필요로 하면 2,3,4 노드에도 props 전달해줘야 하는 문제를 개선한 API

* * *

### 📝Context API 사용방법
#### ✏️전달하기 (상위컴포넌트)
```javascript
/* 상위컴포넌트 */
import {createContext} from 'react';
//Context 선언 및 다른 컴포넌트가 사용할 수 있게 export
export let Context명 = React.createContext();

function 상위컴포넌트(){
  let [state명, setState명] = useState(전달할데이터);
  
  return(
    <Context명.Provider value={{ state명 }}>  //전달할 state여러 개 입력 가능
      <하위컴포넌트 state명={state명} />
    </Context명.Provider>
  )
}
```
#### ✏️전달받기 (하위컴포넌트)
```javascript
/* 하위컴포넌트 */
import {useContext} from 'react';
import {Context명} from '경로'; //상위에서 export한 Context명 그대로 들고오기

function 하위컴포넌트(){
  let {state명} = useContext(Context명) //상위에서 선언한 state,Context 그대로 입력
  
  return(
    //state사용하면 됨
  )
}
```

* * *

### 📜App.js에서 생성한 state를 Detail 컴포넌트로 전달하기
```javascript
/* App.js */
import {createContext} from 'react';
export let stockContext = createContext();  //state(stock)담을 context생성

function App(){
  let [stock, setStock] = useState([10,11,12]);  //전달할 state(stock)
  
  (중략)
  
  <stockContext.Provider value={{ stock }}>
    <Detail stock={stock} />  //state(stock) 전달완료
  </stockContext.Provider>
}


/* detail.js (Detail컴포넌트) */
import {stockContext} from './../App.js'

function Detail(){
  let {stock} = useContext(stockContext);
  
  return (
    {stock} //stock에 들어있는 데이터 출력함
  )
}
```

* * *

### 💡Context API 장단점
#### 장점
1. 중첩해서 사용한 컴포넌트가 많을 때 props 전달이 편리함
2. 여러 개 props(state)들을 한꺼번에 전송 가능함
3. 말단노드로 전달 시 그 전의 컴포넌트들에 일일이 명시해주지 않아도 됨

#### 단점
1. state 변경 시 Context를 사용한 컴포넌트 전체가 재렌더링이 됨
   (변경된 state를 사용하지 않는 컴포넌트라도 무조건 재렌더링 되기 때문에 성능이슈 발생)
2. ```useContext()```를 사용하고 있는 컴포넌트는 다른 파일에서 재사용할 때 Context를 import해야하므로 더 귀찮아 질 수도 있음...
3. 컴포넌트가 많이 없을 때 props보다 불편함

👉🏻 Context API 대체제 : **Redux**같은 외부 라이브러리
다음 포스팅 [[React] Redux](https://velog.io/@keynene/React-Redux) 에서 확인 가능
   