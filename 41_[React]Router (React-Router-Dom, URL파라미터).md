## 📖Router (React-Router-Dom, URL파라미터)
- **React-Router-Dom**이란 React에서 페이지를 나눌 때 쓰는 외부라이브러리임
- 기본적으로 React는 **SPA** 방식이므로 **한페이지**로만 구성되어있음
- 그러나 React로 여러페이지를 구성하는 방법이 여러가지가 있는데 그 중 하나가 **React-router-dom**을 사용하는 것임
- Routes, Route, Link, useNavigate, Outlet 등이 있고, nested route등을 구현할 수 있음
- Routes 로도 구현 못 할 만큼 여러 페이지를 구현해야 하는 경우, **URL 파라미터**를 사용

* * *

### ❓기존 HTML과 React-Router_Dom의 차이점
#### HTML에서 페이지 나누는 법 (React미사용)
1. HTML파일 만들어서 새로운 페이지 내용 새로 하드코딩
2. 새로운 페이지 url로 접속하면 1번에서 만든 HTML파일 보내줌
(여러 개의 HTML파일 관리)
3. 페이지를 이동할 때마다 **로딩필요**

#### React에서 페이지 나누는 법 (React-Router-Dom)
1. 컴포넌트로 새로운 페이지 내용 일부 코딩
2. 새로운 페이지 url로 접속하면 **현재 HTML파일에서 로딩없이** 1번에서 만든 컴포넌트를 보여줌
(HTML파일은 1개만 관리)
3. **리로드 없이** 페이지 이동 가능

#### ※ React에서는 SPA이므로 HTML파일은 index.html파일 하나밖에 사용하지 않기 때문!

* * *

### 💻React-Router_Dom 설치방법
React-Router-Dom은 React와 같이 라이브러리이기 때문에 설치해서 사용해야 함

1. 설치하고자 하는 React파일 실행
2. 터미널에서 ```npm install react-router-dom@6``` 입력
   (설치하고자 하는 경로가 맞는지 확인 필수)
3. 설치완료 후 index.js 파일에서 
```import {BrowserRouter} from "react-router-dom"```입력
4. index.js 파일에서
```<App />```컴포넌트를 ```<BrowserRouter>```컴포넌트로 감싸기 (아래참고)

```
<BrowserRouter>
  <App />
</BrowserRouter>
```

* * *

### 📝페이지분리 구현 (Navigate/Route)
#### ✏️useNavigate() 훅을 이용한 페이지 이동 구현
navbar에서 원하는 카테고리 클릭 시 페이지 이동
```javascript
//useNavigate는 훅이기 때문에 변수에 저장해야 함
import { Link } from 'react-router-dom'
let navigate = useNavigate();

//(중략)
<Nav.Link onClick={()=>{ navigate('/detail') }} href="#detail" >Detail</Nav.Link>
//Detail이라는 nav요소를 누르면 '/detail' url로 페이지 이동
```
👉🏻 기존의 href요소와 navigate 훅의 차이점
href : 로딩이 발생하여 페이지 이동 지연됨
navigate : 로딩 없이 페이지 이동, 클릭 이외 다른 이벤트로도 구현 가능

* * *

#### ✏️Routes, Route, Outlet을 이용한 nested route
url마다 보여지는 페이지가 달라지게 구현 (라우팅)
```javascript
/**사용방법**/
import { Routes, Route } from 'react-router-dom'

<Routes>
  /*일반적 route*/
  <Route path="/url주소" element={실행코드} />
    // path : 페이지의 url. (그냥 "/"는 메인페이지를 의미함)
    // element={} : 페이지에 구성될 요소를 나타냄 (컴포넌트 삽입가능)
    
  /*nested routes*/
  <Route path="/상위url" element={<div>상위코드</div><Outlet />}>
    <Route path="하위url" element={<div>하위코드</div>} />
  </Route>
    //<div>상위코드</div><div>하위코드</div> 이렇게 배치됨
    //Outlet : 하위코드가 노출될 위치
</Routes>
```

```javascript
/**구현**/
<Routes>
  /*일반적 route*/
  <Route path="/" element={
    <div>메인페이지입니다.</div>
  } ></Route>
  
  /*nested routes*/
  <Route path="/about" element={<About />}>
    //nested routes의 path는 상위 path를 포함함 (member == /about/member)
	<Route path="member" element={<div>멤버임</div>} />
    <Route path="location" element={<div>위치정보임</div>} />
  </Route>
</Routes>
                                
(중략)

} //App컴포넌트 종료

function About(){
  return(
    <h4>회사정보임</h4>
    <Outlet />  
    //Outlet : 상단 nested routes에서 member, location 이 노출될 자리
    // 👉🏻/about/member 접속 시 
    // <h4>회사정보임</h4><div>멤버임</div> 이렇게 노출될 것임
  )
}
```
💡 예제풀이

url에 **/about/member**를 입력하면 실행되는 코드
: ```<About><div>멤버임</div></About>```
**/about/location**을 입력하면 입력하면 실행되는 코드
: ```<About><div>위치정보임</div></About>```

이렇게 member와 location이 ```<About>```컴포넌트 내용을 노출해야 하는 것처럼
비슷한 구성을 띄고있는 웹페이지를 구상할 때, 
**nested routes**를 사용하면 원하는대로 url구현이 가능하다
(기존 웹페이지의 탭기능과 비슷)

* * *

#### ✏️Error404 페이지 출력 (예외처리 페이지)
```javascript
/*사용방법*/
<Route path="*" element={<div>예외처리 페이지 구현</div>} />
```

의미없는 url 입력 시 **에러페이지**를 출력해주고 싶을 때 사용
(ex. ~~~/detail/123123 등 rul 입력 시 오타)

위와같이 Route 에 path를 "*"으로 주게되면 Route를 통해 url를 구현해놓은 페이지 이외의 모든 url을 다 예외처리 페이지로 출력해준다.

* * *

### 📝URL 파라미터로 페이지 분리
#### ❓ 위와 같이 Route를 이용해 페이지를 분리하려 하는데, 만약 페이지가 수백~수천개라면? (ex. 쇼핑몰 제품상세 페이지)
#### 👉🏻 URL 파라미터로 해결 가능
URL 파라미터란, url의 특정 부분에 사용자가 값을 입력하게 하고,
입력된 값을 ```useParams()```라는 훅을 이용하여 파라미터로 전송하여,
해당 URL 파라미터 값과 데이터 내 고유값이 일치하는 자료를 조회하는 방법

* * *

#### ✏️URL파라미터 사용방법
```javascript
/*파라미터 받을 때*/
<Route path='/url주소/:url파라미터변수' element={실행코드} />
👉🏻":"기호 이후 "url파라미터 변수"를 마음대로 작명하고 해당값을 "실행코드"에서 사용


/*파라미터 조회할 때*/
function 컴포넌트(){
  let {url파라미터변수} = useParams();
  return(
    <h4>{url파라미터변수}</h4>
  )
}
👉🏻useParams()라는 훅을 사용하여 "url파라미터변수"에 사용자 입력 값 저장하고,
  컴포넌트의 return()안에서 사용
  

```

아래 예제를 통해 확인해보자

* * *

#### ✏️URL파라미터로 제품상세 페이지 구현하기

```
/detail 이라는 url을 통해 쇼핑몰 제품상세 페이지를 구현하려고 함
<Detail> 컴포넌트는 detail.js에 구현해놨고, 
각 제품 당 url은 아래와 같이 구분하려 함

1번상품 = /detail/1
2번상품 = /detail/2 .....
👉🏻 여기서 "1,2,3,4 ...."이 데이터의 고유 값이므로 URL파라미터로 지정하면 될 듯
    url파라미터변수 = id,
    실행코드 = <Detail>이라는 컴포넌트로 지정해보자

```
```javascript
/*data.js (데이터 구조)*/
let data = [
  {
    id : 0,
    title : "제품이름",
    content : "제품설명",
    price : 00000
  },
  {둘째상품},
  {셋째상품}, ....
]
export default data;
//서버에서 받아온 데이터
//App.js로 전송할 데이터임 (참고)

-----------------------------------------------------------------

/*App.js (메인페이지 = 파라미터 받기)*/
import data from './data.js';
import Detail from './routes/detail.js';

function App(){
  let [shoes, setShoes] = useState(data)
  
  (중략)
  
  <Route path='/detail/:id' element={<Detail shoes={shoes} />} />
  //url파라미터 = :id
  //실행코드 = <Detail>컴포넌트
  //shoes = App에서 전달할 데이터임 (참고)

-----------------------------------------------------------------

/*detail.js (제품상세페이지, <Detail>컴포넌트 구현 = 파라미터 사용)*/
import { useParams } from "react-router-dom";

function detail(props){
  let {id} = useParams();
  let product = props.shoes.find((x)=>{
    return x.id == id
    //유저가 입력한 url파라미터와 일치하는 데이터를 찾는 함수
    //아까 App.js에서 shoes로 데이터 넘겨줬으니까
  })
  
  return(
    <div>
      <h4>{product.title}</h4> //제품이름 반환
      <p>{product.content}</p> //제품설명 반환
  	  <p>{product.price}</p> //제품가격(00000) 반환
    </div>
  //유저가 입력한 url파라미터(:id)가 1이면 1번상품, 2면 2번상품 반환해줌
  )
}
```

* * *

#### 📌URL파라미터 장점
1. 여러 개의 페이지를 하드코딩 없이 파라미터 값으로 구분하여 관리
   : 수백~수천개 데이터 관리하기 수월함
2. 페이지에서 자료가 정렬되어도 데이터의 **고유의 값**을 이용하여 조회 가능
   : 인기순/제품명순 등 정렬하여 arr의 자료 순서가 바뀌더라도
     데이터의 고유의 값을 이용하기 때문에 혼동없이 자료 조회 가능
3. 원하는 곳에 원하는 만큼 url 파라미터 삽입 가능
   : /detail/:id/part/:id2 이런거 가능

* * *

### 📚정리 
1. **React-Router-Dom**은 React에서 **페이지를 분리**할 때 사용하는 라이브러리
2. **useNavigate()**
   : 이벤트 설정 후 url을 이동하게 해주는 훅 **<span style="color:red">(리로드X)</span>**
   : 리모콘 역할, 변수에 저장하여 사용
3. **<Routes, Route, Outlet>**
   : url마다 페이지를 다르게 출력할 때 사용
   : nested route를 이용해 일부 공유하게 구현 가능
   : 컴포넌트 삽입 가능
4. **URL파라미터 & useParams()**
   : Route path에 ":url변수"로 받아서 ```useParams()```훅을 이용하여 사용
   : 여러개 페이지 한 번에 관리 수월, 데이터 오염 방지 가능
5. **navbar 등 모든페이지에 상시 공유해야하는 요소는 Route에 넣지않음**