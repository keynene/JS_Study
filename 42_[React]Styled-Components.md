## 📖Styled-Components
- React에서 스타일을 적용할 수 있는 라이브러리
- 사용이 필요한 경우
  1. class 중복해서 만든 경우
  2. 컴포넌트에 원하지 않는 스타일이 적용되는 경우
  3. CSS 파일이 너무 길어져서 수정이 어려울 경우
  
* * *

### 💻Styled-Components 설치방법
Styled-Components는 React와 같이 라이브러리이기 때문에 설치해서 사용해야 함

1. 설치하고자 하는 React파일 실행
2. 터미널에서 ```npm install styled-components``` 입력
   (설치하고자 하는 경로가 맞는지 확인 필수)
3. 사용하고자 하는 js파일에 아래와 같이 정의
   ```import styled from 'styled-components'```

* * *

### 📝구현방법
#### <mark style='background-color:#FFF5B1'>✏️styled-components 사용방법</mark>
```
let 컴포넌트명 = styled.요소명`
  //1. 일반적인 방법
  속성1 : 속성1값;   
  
  //2. 속성 지정
  속성2 : ${ props => props.작명 }   
  
  //3. 속성 조건 지정
  속성3 : ${ props => props.작명 == '조건' ? '참인경우 속성깂' : '거짓인경우 속성값' }
`
```
* * *

### 📜예제
#### <mark style='background-color:#E7DDBE'>📌styled-components로 스타일 적용하는 예제</mark>
```javascript
let Btn = styled.button`
  //1. 일반적인방법
  padding : 10px;  

  //2. 속성지정 (react html코드에서 "bg"라는 속성을 이용해 요소 변경하여 여러 개 만드는 방법)
  background : ${ props => props.bg };

  //3. 속성조건지정 (if문 등 다양한 js문법 활용하여 만드는 방법
  color : ${ props => props.bg == 'blue' ? 'white' : 'black' };
           👉🏻bg가 blue인경우 글자색 white, bg가 blue가 아니면 글자색 black
`

function App(){
  return(
  	// 패딩:10px, 배경색:yellow, 글자색:black
  	<Btn bg="yellow">노란버튼</Btn> 
  	// 패딩:10px, 배경색:blue, 글자색:white
  	<Btn bg="blue">파란버튼</Btn>
  )
}
```
* * *

### 📕styled-components 장단점
#### ⭕장점
```
  1. CSS 파일 오픈할 필요없이 JS 파일에서 바로 스타일을 넣을 수 있음
  2. 하나의 JS파일에 입력한 스타일이 다른 JS파일로 오염되지 않음
     : ※원래 React에서는 다 오염됨 → 방지하는법:파일명을 "컴포넌트명.module.css"로 저장
  3. 페이지 로딩시간이 단축됨 
```

#### ❌단점
```
  1. JS 파일이 매우 복잡해짐 
     : 스타일 지정해야 되므로 코드 길어짐 + 컴포넌트가 style인지 일반 컴포넌트인지 구분어려움
  2. JS 파일 간 중복 디자인이 많으면 CSS랑 별반 차이가 없음
     : 다른파일에서 사용하고 싶은 경우 import 해야하기 때문에 CSS랑 동일
  3. 협업 시 불편
     : CSS담당자가 있는 경우 의사전달 어려워짐
```