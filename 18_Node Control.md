### 문자열로 노드 제어
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <title>Document</title>
</head>
<body>
    <ul id="target">
        <li>HTML</li>
        <li>CSS</li>
    </ul>
    <input type="button" onclick="get_in();" value="get_in" />
    <input type="button" onclick="set_in();" value="set_in" />
    <input type="button" onclick="get_out();" value="get_out" />
    <input type="button" onclick="set_out();" value="set_out" />
    <input type="button" onclick="get_innerText();" value="get_innerText" />
    <input type="button" onclick="set_innerText();" value="set_innerText" />

    <input type="button" onclick="beforebegin();" value="beforebegin" />
    <input type="button" onclick="afterbegin();" value="afterbegin" />
    <input type="button" onclick="beforeend();" value="beforeend" />
    <input type="button" onclick="afterend();" value="afterend" />
```
※ 상기 html 코드를 모든 예제에 적용

#### innerHTML : 사용 객체의 하위 엘리먼트들만 반환 (하위 엘리먼트에만 접근 가능)
```javascript
function get_in(){
    var target = document.getElementById('target');
    alert(target.innerHTML);  
    // id값이 target인 엘리먼트의 HTML코드가 그대로 출력됨 
}
function set_in(){
    var target = document.getElementById('target');
    target.innerHTML = "<li>JavaScript Core</li><li>BOM</li><li>DOM</li>"; 
    // id값이 target인 엘리먼트 내 코드 변경
}
```

#### outerHTML : 사용 객체의 자기자신을 포함한 전체 엘리먼트들 반환
```javascript
function get_out(){
    var target = document.getElementById('target');
    alert(target.outerHTML);
}
function set_out(){
    var target = document.getElementById('target');
    target.outerHTML = "<ol id='target'><li>JavaScript Core</li><li>BOM</li><li>DOM</li></ol>";
}
```

#### innerText : 사용 객체의 텍스트값 제어
```javascript
function get_innerText(){
    var target = document.getElementById('target');
    alert(target.innerText);  
    // 해당 엘리먼트의 텍스트만 출력
}
function set_innerText(){
    var target = document.getElementById('target');
    target.innerText = "<li>JavaScript Core</li><li>BOM</li><li>DOM</li>";  
    //해당 엘리먼트의 텍스트값을 변경
}
```

#### insertAdjacentHTML : 원하는 위치에 코드 추가
```javascript
function beforebegin(){  // target 이전 해당코드 추가
    var target = document.getElementById('target');
    target.insertAdjacentHTML('beforebegin','<h1>Client Side</h1>');
}
function afterbegin(){  // target 안쪽 내용 앞에 해당코드 추가
    var target = document.getElementById('target');
    target.insertAdjacentHTML('afterbegin','<li>HTML</li>');
}
function beforeend(){  // target 안쪽 내용 뒤에 해당코드 추가
    var target = document.getElementById('target');
    target.insertAdjacentHTML('beforeend','<li>JavaScript</li>');
}
function afterend(){  // target 이후 해당코드 추가
    var target = document.getElementById('target');
    target.insertAdjacentHTML('afterend','<h1>Server Side</h1>');
}
```