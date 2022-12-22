## 📖Component
- 리액트로 만들어진 웹 페이지의 화면을 이루는 최소한의 단위 (가상 DOM)
- 데이터(props)를 입력받아 View(state)상태에 따라 DOM Node를 출력하는 함수

**👉🏻 많은 div들을 한 단어로 줄이기**

* * *

### 📝Component 사용하기 좋을 때
1. 반복적인 html 축약할 때
2. 큰 페이지들
3. 자주변경되는 것들
4. 다른 페이지 제작할 때 그 페이지의 html내용을 하나의 컴포넌트로 제작
5. 협업 시 웹페이지를 컴포넌트 단위로 나눠서 작업 분배

* * *

### 😥Component 단점
- State 가져다 쓸 때 문제가 생김
 : 기본적으로 JS는 function scope에 준하기 때문에 다른 함수의 변수, state를 가져다 쓸 수 없음 (undefined 발생)
 
**👉🏻 동적인 UI / Props 등으로 극복 가능!**
[내 포스팅 : [React] 동적인UI](https://velog.io/@keynene/React%EB%8F%99%EC%A0%81%EC%9D%B8UI)
[내 포스팅 : [React] Map(data,i)](https://velog.io/@keynene/ReactMapdatai)
 
 * * *

### 📝Component 사용방법
- 컴포넌트 이름은 항상 대문자로 시작 (ex. Header, Article, Nav)
- UI를 재사용 가능한 개별적인 컴포넌트로 나누어 관리 
- JSX구문해 render()/return 안에 하나의 태그로 구분
  (컴포넌트 하나를 만들어 재사용(반복)하는 것이 react의 주 목적이기 때문)
  
  * * *

### 📚Component 종류
**1. 함수형 컴포넌트**
```javascript
function Header(){
  return <header>
    <h1><a href="/">WEB</a></h1>
  </header>
}
```
**2. 클래스형 컴포넌트**
```javascript
class Header extends Component {
  render(){
    <header>
      <h1><a href="/">WEB</a></h1>
  	</header>
  }
}
```