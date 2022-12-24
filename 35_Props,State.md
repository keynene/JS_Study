## 📖Props, State
### 📝Props
- 프로퍼티(properties)의 줄임말
- 컴포넌트에게 어떠한 값을 전달할 때 props를 사용
- props를 전달받은 함수가 내부동작한 return값이 새로운 UI가 됨
- 부모 → 자식 (상속)으로만 전송 가능함 
※ 자식 → 부모 (패륜), 자식 → 자식 (근친) 불가능!

* * *

#### ✏️ Props 사용 전
```javascript
  function Header(){
  	return <header>
  	  <h1><a herf="/">WEB</a></h1>  //여기를 수정해야 함
  	</header>
  }
  
  function App(){
  	return (
      <div>
        <Header /> //WEB
        <Header /> //WEB
      </div>
    )
  }

```
```
위 코드대로도 실행은 가능하나, Header 컴포넌트 안에 HTML 태그를 하드코딩해줘야 함은 변함이 없음 
ex. 1."WEB"을 수정한다고 가정하면 Header안을 수정해줘야 함. 
    2.위 코드처럼 Header 태그를 여러개 사용한 경우, 똑같이 "WEB"이라는 값만 공유하게 됨
    (수정 시 한꺼번에 똑같은 값으로 수정됨)
```

* * *
#### ✏️ Props 사용방법
1. 자식컴포넌트 사용 시 **<자식컴포넌트 작명={state이름} />**
```보통 state명과 동일하게 작명함```
```ex) <자식컴포넌트 test={test} />```
```👉🏻 test라는 state를 test라는 파라미터로 전달한다는 뜻```
2. 자식컴포넌트 function에 매개변수(파라미터) 등록 후 **props.작명**으로 사용
```ex) 위와같이 test라는 state를 파라미터명을 test로 작명해서 전달하면 ```
```자식컴포넌트에서는 <h4>{props.test}</h4>로 사용할 수 있음```
```*아래 예제 참고```

```javascript
function App(){
  //자식컴포넌트에서 사용할 state 생성
  let [test, setTest] = useState(['A','B','C'])
  return (
    <div>
      //자식컴포넌트에 전달 <자식컴포넌트명 props명={state이름} />
      <ChildTest test={test}></ChildTest>
	</div>
  )
}

//대부분 "props"단어로 파라미터 전달 (변경해도 상관없음)
function ChildTest(props){ 
  return (
    <div className="ctest">
      //사용 시 {파라미터명.스테이트명} 여기선 test[0]이므로 "A"만 출력
      <h4>{ props.test[0] }</h4>
    </div>
  )
}
```

* * *



#### ✏️ Props 사용하여 Header h1에 title 넣기
```javascript
  function Header(props){
  	return (
      <header>
  	    <h1><a herf="/">{props.title}</a></h1>
  	  </header>
	)
  }
  
  function App(){
  	return (
      <div>
      	// 아래의 title 값을 수정하면 컴포넌트마다 다른 값 출력가능
        <Header title="WEB"/>  //WEB
        <Header title="APP"/>  //APP
      </div>
    )
  }

```

```
Header()는 APP()의 Header태그 안의 title 값만을 props로 가져옴으로써 
WEB, APP 등 여러 값으로 변경하면서 재사용이 가능해짐

※ App(부모)에서 Header(자식)으로만 상속가능 (반대는불가함)
※ Props는 웹, 앱에서 각 컴포넌트의 속성(properties)값을 가져와,
   해당 컴포넌트 함수/클래스 에 적용 가능하게 함
```

* * *

### 📝State
- 컴포넌트를 다시 실행시켜 새로운 return 값을 만들어주는 데이터
- 리로드 없이 컴포넌트를 재실행
- setState를 할 때마다 컴포넌트를 재실행하여 기본변수를 저장하지 않으므로, setState를 통해 변수 지정하는 것에 익숙해져야 함

**👉🏻 자주 변경될 것 같은 HTML은 State로 만들어두기**

* * *

#### ✏️ State 사용방법
```javascript
import {useState} from 'react';
const [State, setState] = useState('초기값')
  : [0] > 현재 상태 (값)
  : [1] > 상태를 바꾸어주는 함수
useState : 배열생성, 0=값, 1=상태의 값을 변경할 떄 사용
setState : state를 업데이트하여 새로고침없이 component를 리랜더링 해줌
```

* * *

#### ✏️ 1. State 사용하여 클릭 시 1씩 더하는 예제 구현
```javascript
function App(){
  let [따봉, 따봉더하기] = useState(0); //초기값 0
  return (
    <h4><span onClick={ ()=>{ 따봉더하기(따봉+1) } }>👍🏻</span> { 따봉 }</h4>
  )
}
```

```
👉🏻 '👍🏻'이라는 이모티콘을 누르면 '따봉'이 1씩 증가함

※ onClick 사용방법
  onClick={실행할함수}
```

* * *

#### ✏️ 2. Array, Object State 변경하기
👉🏻 copy라는 변수에 array/object를 ```[...저장할변수]``` 를 이용하여 저장

**button 클릭 시 B → C로 변경해주는 함수 구현**
```javascript
function App(){
  let [arr, setArr] = useState(['A','B']) //초기 arr = ['A','B']
  
  return (
    <button onClick={()=>{
  	  let copy = [...arr]  //arr를 copy에 저장
      copy[1] = 'C' // copy = ['A','C']가 됨
      setArr(copy)  // arr의 state를 copy로 저장
  	} }> 수정버튼 </button>
  )
}
```

* * *

#### 📜 3. 심화 > Nav 태그 클릭 시 출력내용이 로드없이 Article 내용이 변경되는 예제
```javascript
function App(){
  const [mode, setMode] = useState('WELCOME'); //0번쨰 인자는 'WELCOME'저장, 1번쨰 인자는 함수로 사용
  const [id, setId] = useState(null);
  const topics = [
    {id:1, title:'html', body:'html is ...'},
    {id:2, title:'css', body:'css is ...'},
    {id:3, title:'js', body:'javascript is ...'}
  ];
  /* html, css, javascript 중에 어떤것을 선택했는지 확인하여 해당 값을 전달 */
  let content = null;
  if(mode === 'WELCOME'){
    content = <Article title="Welcome" body="Hello, WEB"></Article>;
  } else if(mode === 'READ'){
    let title, body = null;
    for(let i=0; i<topics.length; i++){
      if(topics[i].id === id){ 
       //topics의 id에 저장된 값과 nav에서 클릭하여 setId를 통해 변경된 상태의 (_id)값을 비교하여 동일한 값 찾아 
        //topics에 저장된 topics[i].title과 topics[i].body값을 각 변수(title, body)에 저장
        title = topics[i].title;
        body = topics[i].body;
      }
    }
    content = <Article title={title} body={body}></Article>;
  }
  return (
    <div>
      <Header title="WEB" onChangeMode={()=>{
        setMode('WELCOME'); //setMode를 통해 상태값이 'WELCOME'으로 바뀜
      }}></Header>
      <Nav topics={topics} onChangeMode={(_id)=>{
        setMode('READ'); //setMode를 통해 상태값이 'READ'로 바뀜
        setId(_id);
      }}></Nav>
      {content}
      {/* <Article title="Welcome" body="Hello, WEB"></Article> */}
    </div>
  );
}
```


* * *

#### Props, State 공통점
```
props, state 모두 값이 변경되면 새로운 return 값을 통해 UI를 바꿈
```

#### Props, State 차이점
```
Props : component를 사용하는 외부자를 위한 데이터
State : component를 만드는 내부자를 위한 데이터
```
