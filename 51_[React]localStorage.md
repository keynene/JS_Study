## 📖localStorage
- React에서 state는 새로고침하면 모두 리셋됨 (state장점이자 단점)
- state를 영구적으로 보관하고 싶을 때 **서버(DB)**에 저장하거나 **localStorage**라는
   웹 스토리지를 사용하는 방법이 있음
- 단, localStorage를 포함한 web storage는 **동일한 컴퓨터, 동일한 브라우저에 한해서만 
데이터를 저장해주고, 오직 문자형(string)데이터 타입만 지원함**
- array/object 자료는 JSON형태로 데이터를 변환하여 저장함

* * *

### ❓ Web storage란
- 웹 상에서 데이터를 서버(DB)를 사용하지 않고, 
- 새로고침해도 리셋되지 않게 영구적으로 데이터를 브라우저에 보관할 때 사용함
- 동일한 컴퓨터에서 동일한 브라우저를 사용할 때만 해당됨
- **세션 스토리지(sessonStorage)**와 **로컬 스토리지(localStorage)**로 구분됨

1. **세션 스토리지(sessonStorage)**
   : 웹 페이지의 세션이 끝날 때 저장된 데이터가 지워짐 (세션 유지중엔 데이터 보존)
   : 브라우저에서 같은 웹 사이트를 여러 탭이나 창에 띄울 경우 여러 개의 세션 스토리지에 **데이터가 격리되며, 각 탭이나 창이 닫힐 때 데이터도 함께 소멸함**<br>
2. **로컬 스토리지(localStorage)**
   : 세션이 끝나더라도 데이터가 지워지지 않고 영구 보존됨
   : 여러 탭이나 창 간 **데이터가 서로 공유되며, 탭이나 창을 닫아도 데이터는 브라우저에 남아있음**
![](https://velog.velcdn.com/images/keynene/post/06d5069e-19d2-4cc5-a7cf-ee668fd200b1/image.png)
👉🏻 localStorage에 저장된 data라는 객체와 watched라는 배열
❓ 문자형(string)자료만 저장한다면서?   👉🏻 아래 사용방법에서 설명하겠음
 
   
* * *

### 📝localStorage 사용방법
#### ✏️localStorage 문법
개발자도구 Application탭 > localStorage 에서 확인가능
```javascript
// 1. 저장
localStorage.setItem('data명', '저장할data'); //string만 저장가능

// 2. 읽기
localStorage.getItem('data명');

// 3. 삭제
localStorage.removeItem('data명')
```
👉🏻 localStorage는 **수정이 불가**하므로 **삭제→다시 저장**과정을 통해 수정해야 함!

* * * 

#### ✏️localStorage에 array/object자료 저장하기

👉🏻 localStorage는 문자형(string)으로만 데이터를 저장하기 때문에, 
array/object자료를 저장할 때 JSON으로 변환하여 저장해야 함

저장 : string → JSON 변환하여 저장 ```JSON.stringify()```
읽기 : JSON → string 변환하여 읽기 ```JSON.parse()```

```javascript
// 1. array/object 저장
localStorage.setItem('data명', JSON.stringify({ name : noi }))

// 2. array/object 읽기
let data변수명1 = localStorage.getItem('data명') // 저장해둔 데이터를 data변수명1에 저장
let data변수명2 = JSON.parse(data변수명1)   //data변수명2에 array/object자료 저장됨
                                          //data변수명1에 똑같이 저장해도 상관없음
```

* * *

### 📜쇼핑몰 최근 본 상품 기능 구현
#### ✏️제품상세페이지(Detail.js)에 접속하면 해당 상품 id를 localStorage에 저장하는 기능<br>

1. 메인페이지에 접속하면 빈껍데기 배열을 localStorage에 저장
   : ```useEffect()```를 통해 메인페이지에 접속할 때마다 최근 본 상품이 있는지 없는지 검사하고
   최근 본 상품이 없으면 'watched'로 껍데기 배열([])을 localStorage에 저장해주고,
   최근 본 상품이 있으면 저장할 필요 없음 (저장하면 state와 똑같이 동작하게 됨🤦🏻‍♀️)
   <br>
2. 상세페이지(Detail.js)에 접속하면 해당 제품의 id를 localStorage에 저장
   : ```useEffect()```를 통해 메인페이지에서 만들어놓은 localStorage의 현재 'watched'를 
   ```getItem()``` 을 통해 가져온 후 변수(watchedData)에 저장, 
   watchedData에 해당 제품 id를 ```push()```하여 다시 ```setItem()```을 통해 localStorage에 저장
   
   
   
```javascript
/* App.js (메인페이지) */

function App(){
  useEffect(()=>{
    // 현재 localStorage의 watched에 데이터가 없을때만 초기화 배열 [] 저장
    if (localStorage.getItem('watched').length <= 0){
      localStorage.setItem('watched', JSON.stringify( [] ))
    }
  }, [])
}


/* Detail.js (제품상세페이지) */

function Detail(props){
  (중략)
  // useParams : URL파라미터에 입력한 값 가져와줌 (파라미터 사용하기)
  // product에 URL파라미터 id와 제품 고유의 id가 일치하는 값 저장
  // 관련 포스팅은 아래 참고
  let {id} = useParams(); 
  let product = props.shoes.find((x)=>{ return x.id == id });
  
  useEffect(()=>{
    // localStorage는 수정이 불가하므로 데이터 가져와서 업데이트 후 다시 저장해야 함
    let watchedData = localStorage.getItem('watched') //현재 watched 가져오기
    watchedData = JSON.parse(watchedData)   //읽기 : JSON → string
    watchedData.push(product.id)   // 현 제품 id 업데이트
    
   	//중복제거하기
    watchedData = new Set(watchedData) //집합으로 만들었다가(중복제거)
    watchedData = Array.from(watchedData) //배열로 바꾸기
    
    //중복제거된 업데이트 배열 재저장
    localStorage.setItem('watched', JSON.stringify(watchedData))   
  }, [])
}
```
👉🏻 [내 포스팅(URL파라미터 관련) : [React] Router (React-Router-Dom, URL파라미터)](https://velog.io/@keynene/ReactReact-Router-Dom#url-%ED%8C%8C%EB%9D%BC%EB%AF%B8%ED%84%B0%EB%A1%9C-%ED%8E%98%EC%9D%B4%EC%A7%80-%EB%B6%84%EB%A6%AC)

* * *

### 📚정리
1. **서버(DB)없이 웹 페이지의 사용자 자료/정보를 저장하려면 web storage를 사용**
   세션 스토리지(sessonStorage) : 세션 동안의 정보만 저장 (탭/창 격리)
   로컬 스토리지(localStorage) : 세션 이후 정보도 영구 저장 (탭/창 공유)
   로컬/세션 공통점 : 동일 컴퓨터, 동일 브라우저에서만 저장
   <br>
2. **문자형(string)으로만 정보 저장**
   array/object 저장 : string → JSON ```JSON.stringify()```
   array/object 읽기 : JSON → string ```JSON.parse()```
   <br>
3. **수정이 불가** (가져와서 가공 후 재저장)
   가져오기 : ```getItem('자료명')``` 로 가져와서 가공하여 변수에 저장
   저장하기 : ```setItem('변수명',변수)``` 로 변수에 저장된 내용 재저장
  