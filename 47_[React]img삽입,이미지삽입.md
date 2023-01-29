## 📖Img삽입
- React는 기존 HTML과 이미지 삽입하는 방법이 다름
- 방법은 다양한데 일단 일반 ```<img src="상대 or 절대경로" />```는 안됨
>React에서 이미지 삽입하기
>1. css
>2. html(import)  : 기존 html과 다름
>3. public폴더사용 등

* * *

## 📝이미지 삽입하기
### ✏️1. css에서 이미지 삽입하기
```css
/*App.js에 이미지가 들어갈 div 만들어주기*/
<div className="main-bg"></div>

/*App.css에서 main-bg에 이미지 넣기*/
.main-bg {
  height: 300px;
  background-image: url('./img/bg.png')  /*이미지 경로*/
  background-size: cover;  /*cover : 크기에 맞게 이미지 확대/축소 (가로세로비율유지)*/
  background-position: center;
}
```

* * *

### ✏️2. html(import)에서 이미지 삽입하기
```javascript
/*App.js에서 실행*/
import bg from './img/bg.png'  //이미지 경로

function App(){
  return (
    <div>
      //bg는 import해온 "변수"이므로 
      //JS에서 문자와 변수를 같이 써줄 때 사용하는 '+'연산자가 필요
      <div className="main-bg" style={{ backgroundImage: 'url('+ bg +')' }}></div>
    </div>
  )
}
```

* * *

### ✏️3. public폴더 활용하여 이미지 삽입하기
>리액트로 개발 끝내면 모든 코드를 한 파일로 압축하는 build 작업을 하게 된다.
>src폴더에 css,html,js등 모든 파일이 다 압축되는데 public폴더는 그대로 보존된다.
>img, txt, json 등 수정이 필요없고 그대로 보존하고 싶은 파일은 public에 보관하면 된다.


```javascript
/*App.js 등 js파일에서 실행*/
//1. 간단한방법 - 그냥 '/이미지경로'사용
<img src="/bg.png" />
  
//2. 권장되는방법
<img src={process.env.PUBLIC_URL + '/bg.png'} /> 
```

* * *

## 📚정리
1. 사실 **css**에서 이미지 파일을 가져오는 것이 가장 쉽다.
 : 그러나 이미지 파일이 수백-수천가지인 경우 한계가 있다.
 
2. 그래서 React 공식사이트에서는 **public폴더**를 이용한 이미지 삽입 방법을 권장하는 것이다.

3. 또한, 리액트로 만든 html페이지를 배포할 때 깔끔한 경로로 배포하지 않고,
```"velog.com/~~~/~"```과 같은 경로로 배포할 때가 있을 수 있다.
이럴 때 public폴더를 이용하기 위해 ```<img src="/bg.png" />```이런식으로 사용하면 파일을 찾을 수 없다고 에러가 뜰 수가 있다.
4. 그러므로 public폴더를 사용하여 이미지를 가져올 경우 웬만하면 **권장되는 방법**을 사용하도록 하자.