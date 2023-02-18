## 💻[Error/React] export 'Join' (imported as 'Join') was not found in './routes/Join.js' (possible exports: default)
![](https://velog.velcdn.com/images/keynene/post/478b5c3e-e049-4507-9c61-9f3fd83fffd8/image.png)

- 외부파일 컴포넌트 import/export 시 발생하는 문법 에러
- 보통 컴포넌트 import나 export의 문법을 잘못 작성하여 발생함
- 라이브러리 컴포넌트 import문법과 외부js파일 컴포넌트 import 문법은 약간 차이가 있음
  (라이브러리는 import 시 컴포넌트명에 {중괄호}가 붙고 외부js는 안붙음)
<br>

나는 Join이라는 컴포넌트의 코드가 길어질 것 같아, App과 분리하여 외부 컴포넌트js파일로 관리하기 위해 src폴더에 routes라는 폴더를 생성하여 Join.js이라는 파일을 import하는 부분에서 에러가 발생했다.

Redux, react-router-dom 등 라이브러리와 같이 ```import { 컴포넌트명 } from '라이브러리명';``` 문법으로 import 했는데, 여기서 문제가 발생했다.
아무도 이 원인으로 에러가 발생한 사람이 없나보다... 에러 해결하는데 한참 걸렸다😥

**👉🏻결론적으로 외부 파일 컴포넌트를 import할 때는 {중괄호}를 떼야 한다.**
<br>




* * *


## 📝에러 해결 및 import/export Tips
### 1. 외부js파일 import 시 컴포넌트 명에 {중괄호}를 뗄 것 (에러해결)
<br>

**❓외부컴포넌트js파일에 ~~{중괄호}~~가 안붙는 이유**
: react는 일반적으로 한 파일 당 하나의 export만 존재한다.
: 👉🏻 import 할 때도 **단 1개의 컴포넌트만 import** 한다는 소리임
: 👉🏻👉🏻 {중괄호}넣어서 컴포넌트를 여러개 import 할 수가 없으니 필요 없을 수밖에..
<br>

**❓그럼 라이브러리에는 {중괄호}가 붙는 이유**
  : 라이브러리에는 수많은 컴포넌트가 있고, 여러 컴포넌트를 한 번에 import 하기위해 {중괄호}를 사용함
  : ex) ```import { Route, Routes, useNavigate } from 'react-router-dom';```


```javascript
/* 외부js파일 컴포넌트 import */
import  {Join}  from './routes/Join.js';  //이러면 에러남
import  Join  from './routes/Join.js';    //이게 맞는 문법

/* 라이브러리 컴포넌트 import */
import { Route, Routes, useNavigate } from 'react-router-dom';
```
* * *

### 2. 간혹 react-router-dom 라이브러리 버전 문제인 사람도 있었음 (에러해결)
package.json에서 react-router-dom 버전을 확인해보고 v5라면 다시 설치해보자
(v6 이상이어야 정상 작동하는 것 같음)
![](https://velog.velcdn.com/images/keynene/post/48cb791c-9832-4c70-9521-fba964490b6a/image.png)



* * *


### 3. 외부 컴포넌트는 무조건 defualt속성을 사용하여 export
```javascript
/* App.js */
import 자식컴포넌트명 from '자식컴포넌트가 저장된 파일.js';

function App(){
  return(
    <div>
      <자식컴포넌트 /> //이렇게 상위에서 하위 컴포넌트를 import할 때는
    </div>
  )
}

/* 자식컴포넌트가 저장된 파일.js */
function 자식컴포넌트(){
  (중략)
}

export default 자식컴포넌트;  //이렇게 하위에서 default 속성을 이용하여 export 해야함
```

* * *

## 📚정리
1. **외부js파일 컴포넌트 import 시 ~~{중괄호}~~ 떼기**
   ```import  컴포넌트명  from '경로';```
   <br>
2. **라이브러리 컴포넌트 import 시 {중괄호} 붙이기**
   ```import  {컴포넌트명1, 컴포넌트명2 ...}  from '라이브러리명';```
   <br>
2. **외부js파일에서 컴포넌트 export 시 default 속성 무조건 사용**
   ```export default 컴포넌트명;```
   <br>







