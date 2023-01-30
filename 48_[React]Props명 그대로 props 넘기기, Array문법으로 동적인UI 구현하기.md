## 📖Props명 그대로 props 넘기기
- React에서 하위 컴포넌트에 state값을 전달할 때 props라는 변수를 사용함
- 하위 컴포넌트에서 props를 사용할 때마다 ```props.props명```으로 사용해왔는데, props명 그대로 사용하는 방법이 있음

👉🏻 하위 컴포넌트에서 매개변수란에 ```{props명}```입력하기
```javascript
function 하위컴포넌트({props명1, props명2, ...}){
  return (
    console.log(props명1, props명2) //으로 사용가능
  )
}
```

* * *

### 📝Props 전달 기존문법
```javascript
/* 상위 컴포넌트 */
function App(){
  let [test, setTest] = useState(0);
  return (
    (중략)
    //Test라는 컴포넌트로 test라는 state 전달하기
    <Test test={test} />
  )
}
  
/* 하위 컴포넌트(Test) */
function Test(props){
  return (
    console.log(props.test)
    //props.props명 즉, props.test를 입력해야 값 출력이 가능했음
  )
}
```

👉🏻매번 ```props.props명```을 입력하자니 매우 귀찮다

* * *

### 📝Props 전달 개선문법
```javascript
/* 상위 컴포넌트 */
function App(){
  let [best, setBest] = useState(0)
  return (
  	(중략)
  	<Best best={best} />
  )
}

/* 하위 컴포넌트(Test) */
function Best({best}){
  //여러 개면 {best, test, etc...} 가능
  return (
    console.log(best)
    //props명을 그대로 가져올 수 있다 !
  )
}
```

* * *

### 💡Props 전달 개선문법 장단점
#### 장점
1. 각각 props 구분이 쉬워짐 (현업에서 유용하게 쓰일듯? ...아님말고..)
2. 코드가 짧아짐

#### 단점
1. 전달할 props가 많으면 많을수록 매개변수란이 길어짐
2. 하위 컴포넌트 내 변수/함수와 props의 구분이 어려워질듯

* * *

## 📖삼항연산자/조건문 대신 array문법으로 동적인UI 구현하기
- React에서 동적인UI 구현할 때 **삼항연산자**를 사용하거나, **컴포넌트를 분리해서 조건문**을 주로 씀
(JSX에서는 js의 일반 조건문인 if/else 사용이 불가능하기 때문)
- ```[array자료][array명]```으로 조건문처럼 동적인UI 구현 가능
- 삼항연산자는 2가지 조건만을 필요로 하는데, 조건식이 2보다 많을 경우 array문법을 사용

* * *

### 📙protab state에 따라 결과가 변하는 UI구현
### 📝컴포넌트 분리 후 조건문으로 동적인UI 구현

```javascript
function App(){
  let [protab, setProtab] = useState(0)
  return (
    (중략 / 버튼 클릭할 때마다 proptab 상태 변하는 코드가 있다고 치자)
    <TabContent protab={protab} />
  )
}

/* 조건문으로 동적UI구현 */
function TabContent({protab}){
  if (protab == 0){
    return <div>0일때 코드</div>
  }
  else if (protab == 1){
    return <div>1일때 코드</div>
  }
  ......
}
```
👉🏻 protab이 추가될 때마다 ```else if``` 열어줘야 하고, ```return```을 계속 쓰자니 귀찮다 ...

* * *

### 📝Array문법으로 동적인UI 구현
```javascript
/* App내용은 동일 */
function App(){
  let [protab, setProtab] = useState(0)
  return (
    (중략 / 버튼 클릭할 때마다 proptab 상태 변하는 코드가 있다고 치자)
    <ArrayContent protab={protab} />
  )
}

function ArrayContent({protab}){
  return [<div>0일때 코드</div>,<div>1일때 코드</div>, ...][protab]
  //이 짧은 한 줄로 코드 구현 끝!
}
```

* * *

### 💡Array문법으로 동적UI구현 장단점
#### 장점
1. ```return```최소화
2. 한줄로도 조건문처럼 구현 가능 (코드가 짧아짐)
3. array 요소가 계속 추가되어도 ```.append```등을 이용하여 수정 용이

#### 단점
1. 조건문에 비해 비가시적임 (코드 길어지면 구분이 잘 안됨)
2. array 크기를 벗어나면 예외처리 하기 힘들 것 같음