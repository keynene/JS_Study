## 📖JSX (JavaScript XML)
- React에서 UI구현 시 사용하는 JavaScript 확장문법 (JS안에 HTML이 포함되어 있음)
- React에서 JSX사용이 필수는 아니지만, SPA(Single Page Application)방식을 따르는 React 특성상 JSX를 사용하면 <span style="color:red">가독성을 높이고 코드를 간결화</span>한다는 장점이있음
- JSX사용에 앞서 React는 렌더링 로직과 UI로직의 연결관계를 이해할 필요가 있음

>1. 이벤트가 처리되는 방식
>2. 시간에 따라 state가 변하는 방식
>3. 화면에 표시하기 위해 데이터가 준비되는 방식

* * *

### 📝JSX표현식
#### ✏️JSX문법 1. HTML에 class 넣을 땐 className
일반적으로 JSX는 HTML과 사용방식이 비슷하지만 문법에 살짝 차이점이 있음
(JSX는 JavaScript 기반이기 때문)
```javascript
//html
class = ""

//JSX
className = ""

//Ex
function App(){
  return (
    <div className="App"> </div>
  )
}
```

* * *

#### ✏️JSX문법 2. 변수를 HTML에 넣을 때는 {중괄호} - 데이터바인딩
JSX는 HTML과 달리 하드코딩이 아니라, 중괄호를 이용하면 변수에 저장된 값을 출력/저장할 수 있음

**1. div안에 변수값 출력**
```javascript
function App(){
  
  let post = '변수에 저장될 내용'
  return (
    <div className="App">
      <div>{post}</div>  //div안에 '변수에 저장될 내용'이 출력됨
    </div>
  )
}
```

**2. className에 변수값 저장**
```javascript
function App(){
  
  var data = 'className에 저장할 class/id값'
  return (
    <div className="App">
      <div className={data}>이런식으로 사용 가능</div>
  )
}
```

👉🏻위 예제들 뿐 아니라 **href, id, className, src** 등 다양한 HTML 속성들에도 데이터바인딩 가능

* * *

#### ✏️JSX문법 3. HTML에 style 속성 넣고싶으면 {{쌍중괄호}}
JSX 상에서는 ```style={} 안에 {}자료형```으로 넣어야 함
👉🏻style에 데이터바인딩을 할껀데, {}자료형으로 넣어야하니까 쌍중괄호

> - {속성명 : '속성값'}
> - 대쉬기호 사용 불가능 (font-size → fontSize) 카멜케이스화
