## 💻[Error/React] useRoutes() may be used only in the context of a < Router> component.
- ```useRouter```를 ```<Router>```라는 컴포넌트에 감싸지 않았을 때 발생하는 에러
- react-router-dom 라이브러리를 사용할 때 index.js파일에 ```<BrowserRouter>``` 컴포넌트를 추가하는 걸 까먹으면 발생하는 에러

👉🏻 설치방법 참고 : [내 포스팅 : [React] Router (React-Router-Dom, URL파라미터)](https://velog.io/@keynene/ReactReact-Router-Dom) 

* * *

## 📝에러해결
index.js파일에 ```<BrowserRouter>``` import 후 ```<App />```감싸고 사용
```javascript
/* index.js */
import { BrowserRouter } from 'react-router-dom'; //사용을 위해 import 해주고

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <BrowserRouter> //이 컴포넌트만 추가해주면 에러 해결
    <React.StrictMode>
      <App />
    </React.StrictMode>
  </BrowserRouter>
);

/* 사용할 곳 */
import { Routes, Route } from 'react-router-dom';

function 컴포넌트(){
  return(
    <div>
      <Routes>
        <Route path="경로" element={ 실행코드 } />
      </Routes>
    </div>
  )
}
```

* * *

## 📚정리
1. react-router-dom 사용 시 index.js에 ```<BrowswerRouter>```컴포넌트 추가
<br>
2. import 해주는거 까먹지 말기




