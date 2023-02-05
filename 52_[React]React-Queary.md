## 📖React-Queary
- 서버의 값을 클라이언트에게 가져오거나, 캐싱, 값 업데이트, 에러핸들링 등 Ajax(비동기 요청)과정을 편하게 해주는 라이브러리
  ※캐싱 : 미리 하드에 저장해놓는 작업
- React 개발하다 보면 store 내부에 클라이언트 데이터와 서버 데이터가 공존하며 상호작용을 하게 되는 현상을 예방할 수 있음
- **실시간으로 Ajax 요청을 할 때실시간 데이터 요청 시 기능들을 사용하려면 아래와 같이 사용
발생하는 문제들을 손쉽게 다룰 수 있게 해줌**

>### react-query가 필요한 경우?
1. 일정기간 자동으로 데이터 갱신이 필요한 경우
2. Ajax 요청 실패 시, 재시도가 필요한 경우 (재시도 간격 설정 가능)
3. 다음 페이지를 미리 가져올 때
4. Ajax 성공/실패/로딩중 시 각각 다른 html을 보여줄 때
5. 즉, 실시간 데이터 요청 성공/실패/재요청 상황에 즉각적인 대처가 필요한 사이트

* * *

### 💻React-query 설치방법
React-query는 React와 같이 라이브러리이기 때문에 설치해서 사용해야 함

1. 설치하고자 하는 React파일 실행
2. 터미널에서 ```npm install @tanstack/react-query``` 입력
   (```npm install react-query```와 비슷하나 tanstack버전이 최신버전임)
3. 설치완료 후 index.js파일에서
   ```<App>```컴포넌트를 ```<QueryClientProvider>```컴포넌트로 감싸기
   (import 하고 사용 해야함)

```javascript
import { QueryClient, QueryClientProvider, useQuery } from '@tanstack/react-query'  //1번
const queryClient = new QueryClient()   //2번

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <QueryClientProvider client={queryClient}>  //3번
    <Provider store={store}>     //Redux 컴포넌트인데 미사용 시 생략 가능
      <BrowserRouter>            //Router 컴포넌트인데 미사용 시 생략 가능
        <App />
      </BrowserRouter>
    </Provider>
  </QueryClientProvider>
); 
```

* * *

### 📝React-query 사용방법
#### ✏️React-query로 Ajax 요청하기
일반 ajax로 요청해도 되는데, 실시간 데이터 요청 시 기능들을 사용하려면 아래와 같이 사용
```javascript
import { useQuery } from '@tanstack/react-query';

function App(){
  let 변수명 = useQuery(['쿼리변수명'],()=>{
    return (
      //axios 문법과 동일 (axios 한 것을 useQuery로 감싸서 변수에 저장하는 것이 핵심)
      axios.get('url명')
      .then((결과데이터명)=>{ return 결과데이터명.data })
    )
  })
}
```
👉🏻 ```useQuery()```를 제외한 나머지는 axios 문법이므로 아래 포스팅 확인!
[내 포스팅 : [React] Ajax, Axios, Fetch](https://velog.io/@keynene/ReactAjax)

* * *

#### ✏️ajax 요청 성공/실패/로딩중 상태 기능구현
```javascript
import { useQuery } from '@tanstack/react-query';

function App(){
  let result = useQuery(['querydata'],()=>{
    return(
      axios.get('url')
      .then((axios_result)=>{ 
        return axios_result.data
      })
    )
  })
  
  return (
    <div>
      //로딩중 : 'now lodaing...' 출력
      { result.isLoading && 'now lodaing...' }  
    
      //실패 : 'error' 출력
      { result.error && 'error' }  

      //성공 : axios로 받아온 데이터 출력
      { result.data && result.data }  
    </div>
  )
}
```
👉🏻 그냥 axios만 사용했을 때는 성공/실패 시 상황을 직접 state를 만들어 하드코딩 해줘야 했는데, ```.isLoading, .error, .data```요소를 사용하여 가시적이고 편리하게 구분 가능

* * *

### 💡React-query 장단점
#### 장점
1. ajax 요청 성공/실패/로딩중 상태 쉽게 파악 및 가시적 구현 가능
2. 알아서 ajax 재요청 해줌 (재요청 간격조절 가능)
3. 실패 시 재시도 알아서 해줌 (4, 5번 자동 재시도)
4. ajax로 가져온 결과는 state공유 안 해도 여러 컴포넌트에서 사용 가능

#### 단점
1. 실시간 데이터 요청이 중요한 페이지가 아니면 그닥....

