### jQuery Node API
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <title>Document</title>
</head>
<body>
    <div class="target" id="target1">
        target 1
    </div>
    <div class="target" id="target2">
        target 2
    </div>
    <div id="source">source</div>

    <input type="button" value="remove target 1" id="btn1" />
    <input type="button" value="empty target 2" id="btn2" />
    <input type="button" value="replaceAll target 1" id="btn3" />
    <input type="button" value="replaceWith target 2" id="btn4" />
    <input type="button" value="clone replaceAll target 1" id="btn5" />
    <input type="button" value="clone replaceWith target 2" id="btn6" />
    <input type="button" value="append source to target 1" id="btn7" />
  
    <script src="https://code.jquery.com/jquery-1.12.4.js"></script>
```
※ 상기 html 코드를 모든 예제에 적용

#### 내용추가 : 원하는 위치에 html코드 추가
```javascript
$('.target').before('<div>before</div>');  //target div 앞에 추가
$('.target').after('<div>after</div>');  //target div 뒤에 추가
$('.target').prepend('<div>prepend</div>');  //target div 안쪽에서 내용 앞에 추가
$('.target').append('<div>append</div>');  //target div 안쪽에서 내용 뒤에 추가
```

#### 내용삭제 : 원하는 id값을 가진 html코드 삭제
```javascript
$('#btn1').click(function(){
    $('#target1').remove();  // 태그와 내용 다 삭제
})
$('#btn2').click(function(){
    $('#target2').empty();  // 태그는 그대로고 내용만 삭제
})
```

#### 내용변경
```javascript
$('#btn3').click(function(){
    $('<div>replaceAll</div>').replaceAll('#target1');  
    // id값이 target1인 엘리먼트를 <div>replaceAll</div>로 변경
})
$('#btn4').click(function(){
    $('#target2').replaceWith('<div>replaceWith</div>');    
    //<div>replaceWith</div>로 id값이 target2인 엘리먼트를 변경
})
```
- replaceAll : 지정한 코드로 엘리먼트에 해당하는 내용 변경
- replaceWith : 엘리먼트를 지정하여 원하는 코드로 변경
※ 주체가 다름

#### 내용복사
```javascript
$('#btn5').click(function(){
    $('#source').clone().replaceAll('#target1');  
    // id값이 source인 엘리먼트 복사 후 target1엘리먼트를 replaceAll함
})
$('#btn6').click(function(){
    $('#target2').replaceWith($('#source').clone());  
    // id값이 target2인 엘리먼트를 source를 복사 후 교체
})
```

#### 노드이동
```javascript
$('#btn7').click(function(){
    $('#target1').append($('#source'));  
    // id값이 target1엘리먼트에 source에 append
})
```
