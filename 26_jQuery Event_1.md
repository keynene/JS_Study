### jQuery Event
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <title>Document</title>
</head>
<body>
    <input type="button" id="pure" value="pure" />
    <input type="button" id="jquery" value="jQuery" />
    <script src="https://code.jquery.com/jquery-1.12.4.js"></script>
```
※ 상기 html 코드를 모든 예제에 적용

#### Pure (jQuery 사용x)
```javascript
var target = document.getElementById('pure');
if(target.addEventListener){
    target.addEventListener('click', function(event){
        alert('pure');
    });
} 
```
- 일반적인 이벤트 사용 기법인 addEventListener를 사용하여 event 실행

#### jQuery Event
```javascript
$('#jquery').on('click', function(event){
    alert('jQuery');
})
```
- jQuery 내장함수 중 ".on"을 사용하여 이벤트 실행