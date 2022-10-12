### jQuery Event 2
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <title>Document</title>
</head>
<textarea>
    <p>on속성 - selector</p>
    <ul>
        <li><a href="#">HTML</a></li>
        <li><a href="#">CSS</a></li>
        <li><a href="#">JavaScript</a></li>
    </ul>
    <br />

    <p>다중 바인딩</p>
    <input type="text" id="target" />
    <p id="status"></p>

    <p>이벤트 제거</p>
    <input type="text" id="target2"></textarea>
    <input id="remove" type="button" value="remove" />
    <p id = status2></p>

    <script src="https://code.jquery.com/jquery-1.12.4.js"></script>
```
※ 상기 html 코드를 모든 예제에 적용

#### on()의 2번째 속성 - selector (필터링/생략가능)
```javascript
/* .on속성 - selector : 필터링 */
// ul속성 안의 a, li 클릭 시 이벤트 발생
$('ul').on('click','a, li', function(event){
    console.log(this.tagName);
})
```
- on의 2번째 속성 selector : 2번째 속성값에 해당 이벤트를 발생
- a, li 태그 클릭 시 이벤트 발생하는 예제 (ul부분 클릭하면 이벤트 발생하지 않음 / 필터링)
- a, li 생략할 경우 ul태그를 포함한 모든 부분 클릭 시 이벤트 발생

#### 다중바인딩
```javascript
/* 다중바인딩 - focus/blur 2중으로 적용 */
$('#target').on('focus blur', function(e){
    $('#status').html(e.type);
})
```
- on의 1번째 속성에 ' '(공백)을 이용하여 여러 이벤트 적용 가능
- target이라는 id값을 가진 요소에 focus와 blur의 모든 이벤트를 적용하는 예제
- .type : 객체에 해당하는 이벤트를 status라는 id를 가진 요소에 전달 (focus/blur 전달)

#### Event Cancle
```javascript
var handler = function(e){
    $('#status2').text(e.type+Math.random());
    // 이벤트 타입 + 랜덤변수 반환
};
$('#target2').on('focus blur', handler)
$('#target2').on('focus', function(e){
    alert(1);
    // focus : handler함수, 1출력 함수 (2개)
    // blur : handler함수
});
$('#remove').on('click', function(e){
    // 1. focus의 handler이벤트만 제거
    $('#target2').off('focus', handler);
    // 2. focus의 이벤트 2개 다 제거
    $('#target2').off('focus');
    // 3. focus, blur의 모든 이벤트 제거
    $('#target2').off('focus blur');

})
```
- jQuery의 .off()함수를 이용하여 해당 객체에 부여되어있는 이벤트중 원하는 이벤트를 일부/전체 삭제 가능