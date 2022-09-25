### Event
```html
<!DOCTYPE html>
<html>
<head>
    <title>Document</title>
</head>
    <!--inline방식-->
    <p>inline방식</p>
    <input type="button" id="target" onclick="alert('Hello world, '+document.getElementById('target').value);" value="button" />
    <input type="button" onclick="alert('Hello world, '+this.value);" value="button" />
    <br/>

    <!--property방식-->
    <p>property방식</p>
    <input type="button" id="target2" value="button_property" />
    <br/>

    <!--addEventListener방식-->
    <p>addEventListener방식</p>
    <input type="button" id="target3" value="button_addEventListener" />
    <br/>

    <!--addEventListener재활용방식-->
    <p>addEventListener재활용방식</p>
    <input type="button" id="target4" value="button_add1" />
    <input type="button" id="target5" value="button_add2" />

</body>
```
※ 상기 html 코드를 모든 예제에 적용

#### inline 방식 (html에서만 구동)
```html
<input type="button" id="target" onclick="alert('Hello world, '+document.getElementById('target').value);" value="button" />
<input type="button" onclick="alert('Hello world, '+this.value);" value="button" />
```
- html 코드 내 onclick event요소에 값 전달하여 구현
- 2줄 모두 같은 inline방식의 코드이나, id값을 부여하여 .getElementById 함수여부 차이

#### property 방식 (js에서 구동, 일반적이진 않음)
```javascript
var t = document.getElementById('target2');
t.onclick = function(event){
    alert('Hello world, '+event.target.value);
}
```
- onclick event시 js코드 내에서 함수 실행

#### addEventListener 방식 (가장 일반적인 방식)
```javascript
var t = document.getElementById('target3');
t.addEventListener('click', function(event){
    alert('Hello world, '+event.target.value);
})
```
- .addEventListener('event종류', '함수') : event 시 함수 실행


#### addEventListener 재활용 (중복하여 사용가능)
```javascript
//하나의 함수로 여러객체에 이벤트 부여 가능
var t1 = document.getElementById('target4');
var t2 = document.getElementById('target5');
function btn_listener(event){
    switch(event.target.id){
        case 'target4':
            alert('add1');
            break;
        case 'target5':
            alert('add2');
            break;
    }
}
t1.addEventListener('click', btn_listener);
t2.addEventListener('click', btn_listener);

```
- js에서 하나의 btn_listner() 함수 생성하여, addEventListener로 호출 시 여러 곳에서 사용 가능