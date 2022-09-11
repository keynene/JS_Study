### Element
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <title>Document</title>
</head>
<body>
    <a id="target" href="https://github.com/keynene" title="keynene">keynene github</a>
    <ul>
        <li class="marked">HTML</li>
        <li>CSS</li>
        <li id="active" class="important current">JavaScript</li>
        <ul>
            <li>JavaScript Core</li>
            <li class="marked">DOM</li>
            <li class="marked">BOM</li>
        </ul>
    </ul>
</body>
```
※ 상기 html코드를 아래 예제들에 적용

#### 식별자API
```javascript
for(var i=0; i<active.classList.length; i++){
    console.log(active.classList[i]);  // [0]important, [1]current 차례로 반환
}
```
- classList : 객체가 가지고 있는 클래스 이름을 " "(공백) 단위로 구분하여 유사배열로 저장
- active라는 id의 클래스들을 " "(공백) 단위로 출력하는 예제

#### 조회API
```javascript
/* document그룹 */
var list = document.getElementsByClassName('marked');
console.group('document');
for(var i=0; i<list.length; i++){
    console.log(list[i].textContent);  // HTML, DOM, BOM
}
console.groupEnd();
```
- .textContent : 객체/배열에 저장되어있는 요소를 반환
- class가 marked에 해당하는 객체들을 list라는 변수에 유사배열 형태로 저장하여 textContent를 이용하여 출력하는 예제

```javascript
/* active그룹 */
console.group('active');
var active = document.getElementById('active');
var list = active.getElementsByClassName('marked');
for(var i=0; i<list.length; i++){
    console.log(list[i].textContent);  // DOM, BOM
}
console.groupEnd();
```
- getElementsByCalssName의 대상을 document가 아닌 id(active) 값으로 할 경우, active의 엘리먼트만 조회함
- active라는 변수에 active라는 id를 가진 객체를 저장하고,
  list라는 변수에 active id 안의 marked라는 class를 가진 객체를 저장하여 list를 출력하는 예제

#### 속성API
```javascript
var t = document.getElementById('target');
console.log(t.getAttribute('href'));
t.setAttribute('href','https://github.com/keynene/javascript');
t.hasAttribute('title'); // title이라는 속성을 가지고 있는지 확인
```
- .getAttribute() : 객체가 가지고있는 속성값을 선택하여 가져옴 
(변수에 저장하는 등 활용가능)
- .setAttribute() : 객체가 가지고있는 속성값을 선택하여 변경



### jQuery Element
#### jQueyr를 이용하여 속성변경
```javascript
var t = $('#target');
console.log(t.attr('href'));
t.attr('title','github.com/keynene'); // title추가 (setAttribute)
t.removeAttr('title'); //title삭제 (removeAttribute)
```
#### jQuery 조회범위 제한
```javascript
$(".marked","#active").css("background-color","red"); 
//active의 marked만 배경색 레드

$("#active .marked").css("background-color","red"); 
//위와 동일

$('#active').find('.marked').css("backgound-color","red"); 
//find 사용

$('#active').css('color','blue').find('.marked').css('background-color','red');
//active 글자색 블루, marked 배경색 레드
```
