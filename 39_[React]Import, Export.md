## 📖Import,Export
- React에서 외부 라이브러리나 Component 등을 불러오거나(import) 내보낼 때(export) 사용
- 하나의 컴포넌트로 만들어 export 할 경우 여러 곳에서 import 하여 **재사용**할 수 있다는 장점이 있음

* * *

### 📝import/export

#### ✏️Import : 불러오기
```javascript
/*사용방법*/
import 데이터 from 위치;
//데이터 : 변수, 컴포넌트, 데이터 등
//위치 : 데이터가 저장되어 있는 위치나 라이브러리 등

//data.js에 있는 data 가져오기
import data from './data./js' 

//react-router-dom에 있는 Routes, Route 컴포넌트 가져오기
import { Routes, Route } from 'react-router-dom' 

//img폴더에 있는 bg.png이미지를 bg라는 변수로 가져오기
import bg from './img/bg.png' 
```

#### ✏️Export : 내보내기
```javascript
/*사용방법*/
export default 데이터;
//데이터 : 컴포넌트, 변수, 함수 등 (※함수 바깥에서 사용해야함)

//Detail.js에서 Detail이라는 컴포넌트 내보내기
function Detail(){
  <div>Detail Component</div>
}
export default Detail;

/*
이렇게 내보내진 컴포넌트는 다른 js파일에서 
import Detail from './Detail.js'로 불러올 수 있음
*/
```