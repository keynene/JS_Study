## 📖Transition
- 지금까지 로드/페이지이동 등 기능 구현 시 이벤트가 딱히 없었음
- React에서 이벤트를 구현하는 방법을 소개할 예정임
  1. Tab(탭) 기능 구현
  2. Tab 클릭 시 fade-in 되는 이벤트 구현

* * *
### 📜예제
### 📌Tab(탭) 기능 구현 - 3가지 탭
1. React-Bootstrap 이용하여 nav로 원하는 탭모양의 html을 가져옴
2. Nav 클릭 시 원하는 탭 순서의 내용이 배치되어야 하므로 <span style="color:red">컴포넌트</span>를 이용하여 내용페이지 구현
3. 탭순서에 맞게 내용페이지 연결 (탭1 클릭 > 내용1페이지 출력)

#### ✏️1. Bootstrap 이용하여 원하는 탭모양 가져오기
```javascript
//원하는 탭 클릭 시 탭 기능 구현되어야 하고, 
//내용페이지를 연동할꺼니까 state로 탭 상태 정의
let [tab,setTab] = useState(0) //기존 탭0으로 고정

/* 탭 nav 구현 */
// 원하는 탭 클릭 시 tab변경해줘야 하므로 setTab 이용
<Nav variant="tabs" defaultActiveKey="link0" >
  <Nav.Item>
    <Nav.Link eventKey="link0" onClick={()=>{ setTab(0) }}>탭0</Nav.Link>
  </Nav.Item>
  <Nav.Item>
    <Nav.Link eventKey="link1" onClick={()=>{ setTab(1) }}>탭1</Nav.Link>
  </Nav.Item>
  <Nav.Item>
    <Nav.Link eventKey="link2" onClick={()=>{ setTab(2) }}>탭2</Nav.Link>
  </Nav.Item>
</Nav>
<TabContent tab={tab} /> //내용페이지 (컴포넌트로 구현하는 이유는 아래에 설명)
```

#### ✏️2. 내용페이지 컴포넌트 구현
```javascript
//위의 탭 클릭 시 각각의 탭의 내용페이지가 연동되어야 함
//삼항연산자로 구현하면 되지않나? 👉🏻탭은 3가지인데 삼항연산자는 2가지만 구현가능
//또한, JSX에는 if, for문 등 기능을 사용할 수 없으므로 "컴포넌트"로 생성

❓ if문 사용 = 가능하지만 너무 지저분해보임
function TabContent(props){
  return (
    if (props.tab == 0){
      <div>내용0</div>
  	}
    if (props.tab == 1){
      <div>내용1</div>
  	}
    if (props.tab == 2){
      <div>내용2</div>
  	}
  )
}

❗ 위 코드랑 똑같이 짧게 구현
function TabContent(props){
  return ({[<div>내용0</div>,<div>내용1</div>,<div>내용2</div>][props.tab]})
}
```

#### ✏️3. 탭 순서에 맞게 내용페이지 구현
- 위 예제까지 구현했으면 자동으로 완성되었을 것임

* * *
### 📌탭 클릭할 때마다 내용페이지 fade-in 기능 구현
1. css를 이용하여 fade-in 기능 붙이기
2. 탭이 클릭될 때마다(탭의상태가 변경될 때마다) 내용페이지 fade-in 기능이 실행될 것이므로 <code>state</code>로 만들기
3. 탭이 랜더링 될 때마다 실행해야하므로 <code>useEffect</code>로 구현
4. 만들어뒀던 css 붙이기
* * *

#### ✏️1. css를 이용하여 fade-in 기능 구현
App.css에서 작업
```javascript
/* class 이름이 "start"일 떈 숨기고 "start end"가 되면 보이도록 설계할 것임 */
.start {
  opacity: 0; //내용물 안보이게
}
.end {
  opacity: 0; //내용물 보이게
  transition: opacity 0.5s; //opacity 기능을 0.5초에 걸쳐서 실행
}
```
* * *
#### ✏️2. 탭 상태에 따라 fade-in 기능 구현 (state)
```javascript
/* 탭 "상태"에 따라 "내용페이지"가 이벤트 실행되는 것이므로 
"TabContent 컴포넌트"에 기능 구현 */
function TabContent(props){
  let [fade, setFade] = useState('');
  
  return (
    /*
    내용페이지 전체가 기능이 구현되어야 하므로 바깥에 class이름 변경해줄 div 생성
    fade 상태에따라 "start" 또는 "start end"가 되어야 하므로,
    className을 {}로 JSX 구현
    */
    <div className={'start ' + fade} >
      {[<div>내용0</div>,<div>내용1</div>,<div>내용2</div>][props.tab]}
    </div>
  )
}
```

하지만, 위 코드대로 실행하면 className을 "start end"로 바꿔줄 수가 없음.
tab 상태가 <span style="color:red">변경될 때마다</span> fade를 바꿔주려면???
👉🏻<span style="color:red">useEffect 이용!</span>

* * *

#### ✏️3. 탭이 변경될 때마다 className 변경 (useEffect)
이미 state로 fade 구현해놓았으니 이걸 탭 상태에 따라 useEffect로 붙이기만 하면 끝!
```javascript
function TabContent(props){
  let [fade, setFade] = useState('');
  
  //현재 fade 상태는 ''이므로 내용페이지 className은 'start'임
  //useEffect가 실행되면 fade를 'end'로 바꾸면 끝이지 않을까??
  useEffect(()=>{
  	setFade('end');
    
    //그리고 한 번 end로 바뀐 fade를 다시 ''로 되돌아오도록 구현하면 완성?!
    return ()=>{
      setFade('');
    }
  }, [props.tab]) //tab이 변경될 떄마다 useEffect 실행해야 하므로
  
  return (
    <div className={'start ' + fade} >
      {[<div>내용0</div>,<div>내용1</div>,<div>내용2</div>][props.tab]}
    </div>
  )
}
```
❌ 예상과는 다르게 className이 변경되지 않음
👉🏻 react에서 동작하려면 'start'에서 'start end'가 될때까지의 시간을 조정해줄 필요가 있음 (setTimeout을 이용해보자)

* * *

#### 👌🏻setTimeout()일 이용하여 웨이팅타임 추가
```javascript
(중략)
useEffect(()=>{
  
setTimeout(()=>{ setFade('end') }, 100) //임의로 0.1초 웨이팅

return()=>{
  setFade('');
},[props.tab])

```
❌ ...개발자도구로 봐도 동작하지 않음
👉🏻 react 18?버전부터 <span style="color:red">automatic batching</span>이라는 기능이 추가되었기 때문
```
automatic batching이란, react에서 컴포넌트가 불필요하게 랜더링된는 현상을 막기위해, 
setState가 연달아 호출될 경우 한꺼번에 실행되도록 하는 기능 
※ 따라서, useEffect의 setFade('end')와 return안이 setFade('')가
랜더링 한 번에 실행되어 setFade('')만 실행된 것처럼 동작했던 것임!!
```
❓ automatic batching를 고려하여 문제되지 않게 구현하려면?
❗ clearTimeout을 이용하여 timer처럼 동작시켜보자

* * *

#### 👌🏻automatic batching을 고려하여 다시 구현해보자
```javascript
function TabContent(props){
  let [fade, setFade] = useState('');
  
  useEffect(()=>{
    //timer로 동작하려면 return에서 clean up 해줘야하므로 변수에 넣자
  	let t= setTimeout(()=>{ setFade('end') },100);
    
    return ()=>{
      clearTimeout(t);
      setFade('');
    }
  }, [props.tab])
  
  return (
    <div className={'start ' + fade} >
      {[<div>내용0</div>,<div>내용1</div>,<div>내용2</div>][props.tab]}
    </div>
  )
}
```
⭕ 문제없이 잘 동작함

