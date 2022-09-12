### Node API
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <title>Document</title>
</head>
<body>
    <ul id="target">
        <li id="remove">HTML</li>
        <li id="replace">CSS</li>
    </ul>
    <input type="button" onclick="callAppendChild();" value="appendChild()" />
    <input type="button" onclick="callInsertBefore();" value="callInsertBefore()" />
    <input type="button" onclick="callRemoveChild();" value="callRemoveChild()" />
    <input type="button" onclick="callReplaceChild();" value="callReplaceChild()" />
```
※ 상기 html을 모든 예제에 적용
#### appendChild() : 노드추가
```javascript
/* 뒤쪽에 추가 */
function callAppendChild(){
    var target = document.getElementById('target'); // id가 target인 객체 저장
    var li = document.createElement('li') // li 노드추가
    var text = document.createTextNode('JavaScript'); // 텍스트 노드 추가
    li.appendChild(text); // li객체에 text를 자식으로 넣음 <li>JavaScript</li>
    target.appendChild(li); //생성한 li를 target객체에 자식으로 뒤쪽에 추가
}
```
- ```<li>JavaScript</li>```가 target 제일 뒤에 (CSS뒤에) 추가됨
- 추가하려는 객체 ```<li>JavaScript</li>```의 부모노드가 무엇인지 파악해야 함
※ appendChild는 자식으로만 추가 가능

```javascript
/* 앞쪽에 추가 */
function callInsertBefore(){ // 앞에추가
    var target = document.getElementById('target');
    var li = document.createElement('li');
    var text = document.createTextNode('jQuery');
    li.appendChild(text);
    target.insertBefore(li, target.firstChild); //target객체에 target의 firstChild 앞에 추가
}
```
- ```<li>jQuery</li>```가 firstChild 앞에 추가됨 (제일 앞쪽)

#### removeChild() : 노드삭제
```javascript
function callRemoveChild(){
    var remove = document.getElementById('remove');
    remove.parentNode.removeChild(remove); //부모노드에서 삭제할 노드 선택 (부모노드에서만 자식을 삭제 가능, 본인삭제 불가능)
}
```
- 부모노드에서만 자식노드 선택하여 삭제 가능 (객체 본인 스스로 삭제할 수 없음!)

#### replaceChild() : 노드변경
```javascript
/* 태그를 텍스트 → 링크로 바꾸는 함수 */
function callReplaceChild(){
    var a = document.createElement('a');   //a태그 생성
    a.setAttribute('href','https://github.com/keynene');  //속성 추가
    a.appendChild(document.createTextNode('Web browser JavaScript'));  //a태그에 텍스트 추가

    var replace = document.getElementById('replace');
    replace.replaceChild(a, replace.firstChild);
}
```

※ Node API는 대체적으로 Child함수를 이용해 '자식'으로 추가/삭제/변경할 수 있음 (부모노드가 무엇인지 파악하는 것이 관건)