### DOM
- 웹페이지를 자바스크립트로 제어하기 위한 객체모델
- 자바스크립트에서 html 엘리먼트 호출 가능
- Window : 창 / Document : 윈도우에 로드된 문서

#### 문법
1. document.getElementsByTagName()
2. document.getElementsByClassName()
3. document.getElementById()
4. document.guerySelector() : 선택된 인자 하나만을 가리킴
5. document.guerySelectorAll() : 선택된 인자의 모든 속성을 가리킴

#### 사용예제
```javascript
var lis = document.getElementsByClassName('.active');
for(var i=0; i<lis.length; i++){
		lis[i].style.color='red';
}
```
- 'active'라는 class를 가지는 엘리먼트 를 lis에 유사배열 형태로 저장한 후 반복문을 통해 css에 접근하여 color를 red로 변경함

### jQuery
- 상기 DOM을 이용하기 쉽게 적용한 자바스크립트 라이브러리

#### 문법
- $('css선택자').변경속성('인자','변경할 값')

#### 사용예제
1. $('li').css('color', 'red'); → 위 getElementsByClassName 예제 jQuery로 변환
2. $('.active').css('color','red');