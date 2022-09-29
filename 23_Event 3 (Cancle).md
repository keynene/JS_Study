### Event Cancle
- 자바스크립트의 내장 evnet의 진행을 중단할 경우 사용
- event 진행을 무시하고 코드 작성 가능
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <title>Document</title>
</head>
<body>
    <p>
        <label>prevent event on</label><input id="prevent" type="checkbox" name="eventprevent" value="on" />
    </p>
    <p>
        <a href="https://github.com/keynene" onclick="if(document.getElementById('prevent').checked) return false;">keynene</a>
    </p>
    <p>
        <form action="https://github.com/keynene" onsubmit="if(document.getElementById('prevent').checked) return false;">
            <input type="submit" />
        </form>
    </p>
</body>
```
※ 상기 html 코드를 모든 예제에 적용

#### property 방식 event cancle
```javascript
document.querySelector('a').onclick = function(event){
    if(document.getElementById('prevent').checked){
        return false;
    }
};
document.querySelector('form').onclick = function(event){
    if(document.getElementById('prev5ent').checked){
        return false;
    }
};
```

#### addEventListener 방식 event cancle
```javascript
document.querySelector('a').addEventListener('click', function(event){
    if(document.getElementById('prevent').checked){
        event.preventDefault();
    }
})
document.querySelector('form').addEventListener('submit', function(event){
    if(document.getElementById('prevent').checked){
        event.preventDefault();
    }
})
```