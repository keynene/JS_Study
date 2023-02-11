## 💻[Error/React] Invalid Hook Call Warning (유효하지 않은 Hook 요청)
- [React Invalid Hook Call Warning 에러 공식 문서](https://reactjs.org/warnings/invalid-hook-call-warning.html)
- 잘못된 Hook 요청으로 인한 에러
<br>

**👇🏻 에러발생 추정 위치**
```javascript
let dispatch() = useDispatch();

function Detail(props){
  (중략)
  <button className="btn btn-danger" onClick={()=>{
    //새로운 상품이 cart state에 추가되는 기능
    dispatch(addCart(product))
  }}>장바구니</button>
}
```
```useDispatch()```라는 훅을 dispatch변수에 저장하여 사용하려고 했는데, 잘못된 곳에 훅을 호출하면서 해당 에러가 발생되는 것 같았다.
갑자기 페이지가 구동조차 되지 않으니 당황했는데, 공식 문서를 확인하니 아래 3가지 이유로 발생되는 에러인 것을 알 수 있었다.

👉🏻 ```useDispatch()```란? 
 : Redux의 store에 저장되어 있는 Action을 사용할 수 있게 하는 훅
 : [내 포스팅 : [React] Redux(리덕스)](https://velog.io/@keynene/React-Redux) 에서 확인!

* * *
## ❓에러발생이유 & 해결방법
### 1. You might have mismatching versions of React and  React DOM. <br> : React와 React DOM 버전이 16.8.0 이하일 때 발생
React 버전은 package.json에서 확인할 수 있음
![](https://velog.velcdn.com/images/keynene/post/bb23a37a-2832-457b-9c6e-9746e1fcb476/image.png)
만약 버전이 16.8.0 이하라면 React 업데이트 및 재설치 해보자
[내 포스팅 : [React] React (리액트)](https://velog.io/@keynene/React) 👈🏻설치방법참고

* * *

### 2. You might be breaking the Rules of Hooks. <br> : React의 훅 룰을 어겼을 때 발생
[React Invalid Hook Call Warning 에러 공식 문서](https://reactjs.org/warnings/invalid-hook-call-warning.html)
상위 공식 문서 페이지에 접속해보면, 상단에 아래 문구를 확인할 수 있음
![](https://velog.velcdn.com/images/keynene/post/7a95b7eb-0474-43a1-876f-6c0aaca2d214/image.png)

>Hooks can only be called inside the body of a function component.
: 훅은 **함수형 컴포넌트 바디 안**에 호출되어야 한다

<br>

### ❓훅 룰을 어긴 경우
2-1. **클래스형 컴포넌트** 아예 컴포넌트 밖에서 단독으로 호출하는 경우
```javascript
//클래스형 컴포넌트
class Err1_1 extends React.Component {
  render() {
    let dispatch = useDispatch();
  }
}

//단독호출
let dispatch = useDispatch();

function Err1_2() {
  (중략)
}
```
2-2. 함수형 컴포넌트 안의 일반적인 **{중괄호}나 이벤트 핸들러** 안에서 호출하는 경우
```javascript
function Err2() {
  return(
    //일반적 호출
    { let dispatch = useDispatch(); }
	
	//이벤트 핸들러 안 호출
	<button onClick={()=>{ let dispatch = useDispatch(); }}>버튼</button>
  )
}
```
2-3. **훅 내**에서 훅을 호출하는 경우
```javascript
function Err3() {
  let memo = useMemo(()=>{
    let dispatch = useDispatch();
  })
}
```
<br>
<br>

😅 결론적으로 나는 1번 문제(**단독호출**) 때문에 발생한 에러였고, dispatch 변수 선언 부를 컴포넌트 바디 안으로 넣어주니 해결되었다.
```javascript
/*   여기 있던 let dispatch() = useDispatch();   */

function Detail(props){
  let dispatch() = useDispatch(); //여기로 옮김
  (중략)
  <button className="btn btn-danger" onClick={()=>{
    //새로운 상품이 cart state에 추가되는 기능
    dispatch(addCart(product))
  }}>장바구니</button>
}
```

### 
* * *

### 3. You might have more than one copy of React in the same app. <br> : React나 React package가 중복 설치된 경우

#### 우선, 동일한 앱에 React는 하나만 존재해야 한다. (React 사본이 존재하면 안됨❌)

React프로젝트를 하다 보면 Redux, Styled-component, React-query 등 라이브러리나 모듈을 설치해야 하는 경우가 많은데, 이로 인해 **간혹 React가 추가로 설치되면 원본 코드에서의 import와 다른 라이브러리의 import가 중복되어 호출되면 훅 실행이 어려워질 때가 있다고 한다.**

나는 아직 해당 문제를 접해보진 않았지만 만약 앞서 소개한 에러발생이유 1,2번에 해당되지 않는다면 중복되는 react 파일을 검색하여 제거해보자!

터미널에 ```npm ls react``` 입력 > 에러나 중복표시가 있으면 해당 react 제거
![](https://velog.velcdn.com/images/keynene/post/1fa987fc-8883-4985-9b23-935bf07645f9/image.png)
뭐... 중복된 react가 없다면 이와같이 정상적으로 뜰 것이다.

* * *

## 📚정리

### Hooks can only be called inside the body of a function component.<br> : 훅은 함수형 컴포넌트 바디 안에 호출되어야 한다

❌ 클래스형 컴포넌트 안됨 ❌
❌ 단독호출 안됨 ❌
❌ 이벤트핸들러에서 호출 안됨 ❌
❌ 훅 내 호출 안됨 ❌

또 발견되면 추가하겠음✍🏻...

