## 📖Ajax (Asynchronous JavaScript And XML)
- 서버란, 유저가 데이터를 요청하면 데이터를 보내주는 프로그램임
- 데이터 요청 규격에 맞춰 요청해야 함
  1. 어떠한 데이터인지 (url 형식)
  2. 어떤 방법으로 요청할지 (GET/POST)
- Ajax란, 서버에 GET/POST를 요청할 때 <span style="color:red">새로고침 없이</span> 데이터를 주고받을 수 있게 도와주는 브라우저 기능

* * *
### 📝Ajax 데이터 요청 방법
1. XMLHttpRequest : 옛날문법
2. fetch() : 최신문법 (json 명명해줘야 함)
3. <span style="color:red">axios : 외부 라이브러리 (json→문자로 자동으로 변경해줘서 일반적으로 많이 씀)</span>
4. 응답은 <code>json</code>형태로 넘어옴

* * *
### 💻Axios 설치방법
1. 터미널에 아래와 같이 입력하여 설치 후 사용
   <code>npm install axios</code>
2. import로 선언하여 사용
   <code>import axios from 'axios';</code>
   
* * *

### 📝Axios 구현방법
서버로부터 데이터를 받아올 때 : ```axios.get('url').then()```

#### ✏️.get('url')
해당 url로부터 데이터 GET요청

```javascript
axios.get('url') //url에 GET(데이터 보내주세요~) 요청한 상태
```
   
#### ✏️.then()
비동기 통신이 성공했을 경우,
```.then()```은 데이터를 인자로 받아 결과값을 처리할 수 있음
가져온 데이터는 ```.data```안에 들어있음

```javascript
axios.get('url').then((변수)=>{
  console.log(변수) //데이터 가져오기 성공여부, 데이터 등 출력
                   //(config, data, header, request 등....)
  console.log(변수.data) //온전한 '데이터'만을 출력해줌
                        //(서버로부터 가져온 데이터 형식 그대로)
})
```

#### ✏️.catch()
axios는 <code>.catch()</code>를 통해 오류를 처리함
<code>error</code>객체를 이용해 오류에 대한 주요 정보를 학인할 수 있음
에러 처리 문서 참고자료 : https://axios-http.com/docs/handling_errors
ex) 
  <code>error.response.statue</code> : 응답 상태코드 정보
  <code>error.response.headers</code> : 응답 헤더 정보

#### ✏️여러 데이터 한 번에 get 요청하기
```javascript
Promise.all([ axios.get('url1'), axios.get('url2') ])
.then(()=>{ 기존 then과 동일 })
.catch(()=>{ 기존 catch와 동일 })
```

* * * 
  
#### ✏️axios를 이용하여 정보 받아오기
```javascript
import axios from 'axios';

function App(){
  return (
  	<button onClick={()=>{
    
      /*axios로 데이터 받기*/
  	  axios.get('/url')
      .then((result)=>{  
        데이터 수신 성공 시 실행할 코드
        //받아올 데이터를 변수(result-작명)에 저장함
        //result = 데이터의 config, data, header 등 모든정보 저장
        //result.data = 순수 데이터만을 저장

      })
      .catch(()=>{
      	데이터 수신 실패 시 실행할 코드
        //주로 에러메세지 띄움
      })
    
    
      /*n개의 url에서 데이터 가져오기*/
      Promise.all([ axios.get('/url1'), axios.get('/url2') ])
      .then(()=>{ 실행할 코드 })
    
    
      /* axios로 데이터 보내기 */
      axios.post('/url', {data}) 
      // ex) axios.post('/url', {name : 'noi'})
      //json 형태로 서버로 {name:'noi'}라는 데이터 보냄
      //새로운 리소스를 생성함(create)  ex. 로그인, 회원가입 정보 전달
    
    }} >axios예시</button>
  )
}
```

* * *

### 📜예제
#### 📌버튼 클릭 시 서버로부터 데이터 받아와서 갯수만큼 상품카드 추가하기
```javascript
( 기존코드는 shoes에 data라는 데이터 3개를 저장해놓고 상품카드를 출력해주는 코드임 )
let [shoes, setShoes] = useState(data);

(중략)

<button onClick={()=>{
  /* 데이터 받아오기 */
  axios.get('데이터가 저장되어있는 url')
  
  /* 전송 성공 시 */
  .then((result)=>{
    /* 기존의 shoes와 result에 저장된 data를 한꺼번에 copy 에 저장 */
    //array데이터는 쉼표로 구분하여 중복하여 저장 가능
    let copy = [...shoes, ...result.data]; 
    setShoes(copy); 
  })
  /* 전송 실패 시 */
  .catch(()=>{ console.log('실패함 ㅅㄱ') }) //예외코드
}} >more</button>

```

* * *
### 📕주의할 점
❕❗ axios 사용 시 JSX문 사용 불가❗❕
👉🏻 for, if, map 등 함수 사용불가
```javascript
※위 예제풀이 중 에러발생상황
"🤷🏻‍♀️ 이미 있는 state shoes를 copy하여 map을 이용해서 result.data를 push하면 되지 않을까?"
(중략)

.then((result)=>{
  let copy = [...shoes];
//1. result.data가 기존의 shoes의 data와 같은 형태의 data임을 확인한 상황임
//2. result.data가 3개이며 result.data[0]은 0번째의 배열요소를 나타냄을 확인한 상황임
  result.data.map((data, i)=>{
    return copy.push(result.data[i]);
  })
  setShoes(copy);
})
.catch(()=>{ console.log('실패햇음 ㅠㅠ') })

/* 결과 */
"실패했음 ㅠㅠ" 출력됨
```
#### ❓ catch문으로 빠진 이유?
🙅🏻‍♀️ axios에는 JSX 문구 사용이 불가능함. for, if, map 등 함수 사용불가!
👉🏻promise를 이용하여 반복문 구현 (async/await 이용)

* * *

### 📝Fetch 구현방법
```fetch('url').then(결과 => 결과.json()).then((결과)=>{ console.log(결과) })```

기본적인 ```.then, .catch``` 등 사용법은 axios와 동일함

#### ❓Axios와 차이점
Axios는 json → object / array 자동으로 변경해주지만,
fetch는 json을 직접적으로 object / array 자료로 변환해야 함