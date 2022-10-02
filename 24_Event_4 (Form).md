### Event(Form)
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <title>Document</title>
</head>
<body>
    <p>1. submit</p>
    <form id="target" action="result.html">
        <label for="name">name</label> <input id="name" type="name" />
        <input type="submit" />
    </form>
    <br />

    <p>2. change</p>
    <p id="result"></p>
    <input id="target2" type="name" />
    <br />

    <p>3. blur/focus</p>
    <input id="target3" type="name" />
```
※ 상기 html코드를 모든 예제에 적용

#### submit form
```javascript
var t = document.getElementById('target');
t.addEventListener('submit', function(event){
    if(document.getElementById('name').value.length === 0){ // 입력값이 없을 경우
        alert('Name 필드의 값이 누락되었습니다.');
        event.preventDefault();  //이벤트종료
    }
})
```
- submit : form 입력값을 서버로 전달
- 입력값이 없을 경우 event.preventDefault()(기본이벤트 취소)함수로 종료

#### change form
```javascript
var t2 = document.getElementById('target2');
t2.addEventListener('change', function(event){
    document.getElementById('result').innerHTML = event.target.value;
});
```
- change : form값으로 원하는 요소 밸류값 변경
- result 값을 가진 p태그의 텍스트를 target2 값으로 변경

#### focus/blur form
```javascript
var t3 = document.getElementById('target3');
/* focus */
t3.addEventListener('focus', function(event){
    console.log('focus');
});
/* blur */
t3.addEventListener('blur', function(event){
    console.log('blur');
});
```
- focus : form영역 안쪽을 클릭할 경우 발동
- blur : form영역에 잇던 커서를 바깥으로 클릭할 경우 발동