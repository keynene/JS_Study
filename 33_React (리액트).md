## 📖REACT (리액트)
- 웹페이지, 사용자 인터페이스 중 화면에 표시되는 뷰 부분의 개발에 사용되는 자바스크립트의 컴포넌트 기반의 라이브러리
- 기존의 복잡한 DOM구조에서 일부 수정/추가가 필요할 경우 해당 부분만 가상의 DOM(컴포넌트)를 만들어 렌더링하게 하여 불필요한 자원소모를 줄이고 웹 앱 성능을 향상시킴
- SPA(Single Page Application)을 구현하기 위해 사용 (리로드 없이 동작)
- JSX(JavaScript XML)라는 HTML과 유사한 마크업 형태로 구성되어 가독성이 높고 직관적이며, 컴포넌트 객체 기반으로 UI를 관리할 수 있음

* * * 

### 💻React 설치/실행 방법
1. React 작업용 폴더 없으면 : 폴더 생성 > shift+우클릭 > powershell열기
   폴더 있으면 터미널 열기 (경로 확인 필수)
2. 터미널/powershell에 ```npm create-react-app 프로젝트명``` 입력
3. ide에서 폴더 열고 터미널 > ```npm start```입력

>만약, PWA(Progressive Web App : 웹을 앱처럼 동작시키게 함) 기능을 추가할꺼면
```npx create-react-app 프로젝트명 --template cra-template-pwa``` 입력하여 설치
>
#### 👉🏻 PWA 기능이 추가될 뿐, 나머지 기능들은 react만 설치했을 때와 동일함