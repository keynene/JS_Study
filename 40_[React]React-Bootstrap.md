## 📖React-Bootstrap
- html, css를 React의 컴포넌트로 저장하여 언제든 재사용할 수 있게 만들어놓은 도구
- Nav, Grid, Routes 등 자주쓰이는 여러 컴포넌트들 사용 가능
- React-Bootstrap 공식 사이트에서 검색 후 옵션 조절하여 사용
- 가져다 쓰기만 하면 된다는 장점이 있지만, css변경 시 옵션이 충돌될 수 있으므로 사용시 주의
[React-Bootstrap 공식 사이트](https://react-bootstrap.github.io/getting-started/introduction/)

* * *

### 💻React-Bootstrap 설치방법
React-Bootstrap은 React와 같이 라이브러리이기 때문에 설치해서 사용해야 함

❗❕ 설치명령어/import방법 등은 자주 바뀌니까 [React-Bootstrap 공식사이트](https://react-bootstrap.github.io/getting-started/introduction/)에서 확인 후 입력

1. 설치하고자 하는 React파일 실행
2. 터미널에서 ```npm install react-bootstrap bootstrap```입력
   (공식사이트 확인 필수)
3. css파일도 App.js에 import 또는 index.html head태그 안에 넣기
   App.js : ```import 'bootstrap/dist/css/bootstrap.min.css';```
   index.html : [React-Bootstrap 공식사이트](https://react-bootstrap.github.io/getting-started/introduction/) 확인하기
4. 설치완료 후 사용할 파일에 import 후 사용
   ex) ```import { Button } from 'react-bootstrap';```


* * * 

### 📝React-Bootstrap 사용방법
1. 일반 Bootstrap과 동일하게 [React-Bootstrap 공식사이트](https://react-bootstrap.github.io/getting-started/introduction/)에서 원하는 디자인을 검색 후 코드 복사/붙여넣기 하면 끝
2. 단, **컴포넌트**형식은 **import 하여 사용**
3. 일부 css요소 커스터마이징도 가능 (주로 검색 후 최하단에 API 설명이 있음)
```javascript
import { Button } from 'react-bootstrap';

function App(){
  return (
    <div>
      <Button variant="primary">버튼</Button>
    </div>
  )
}
```

* * *

### 📜React-Bootstrap 사용예제
```javascript
import { Navbar, Container, Nav, Row, Col } from 'react-bootstrap';

function App() {
  return (
    <div className="App">
      <Navbar className="nav">  
        <Container>
          <Navbar.Brand href="/">NOI ·_· NARA</Navbar.Brand>
          <Nav className="me-auto">
            <Nav.Link onClick={()=>{ navigate('/') }} href="#home" >Home</Nav.Link>
            <Nav.Link onClick={()=>{ navigate('/detail') }} href="#detail" >Detail</Nav.Link>
            <Nav.Link href="#new">New</Nav.Link>
            <Nav.Link href="#cart">Cart</Nav.Link>
            <Nav.Link href="#sale">Sale</Nav.Link>
          </Nav>
        </Container>
      </Navbar>
	</div>
)}
```

  기존에는 위와 같은 코드를 html, css로 직접 입력을 했어야 했지만,
  React-Bootstrap 사이트 등 여러 유저가 만들어놓은 부트스트랩을 사용하면
  이미 React로 만들어놓은 html, css를 언제든지 가져다 쓸 수 있음🙆🏻‍♀️
