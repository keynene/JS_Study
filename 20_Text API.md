### Text API
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <title>Document</title>
</head>
<body>
<p id="target">Cording everybody!</p>
<p> data : <input type="text" id="data" value="JavaScript" /></p>
<p> start : <input type="text" id="start" value="5" /></p>
<p> end : <input type="text" id="end" value="5" /></p>
<p>
    <input type="button" value="appendData(data)" onclick="callAppendData()" />
    <input type="button" value="deleteData(start, end)" onclick="callDeleteData()" />
    <input type="button" value="insertData(start, data)" onclick="callInsertData()" />
    <input type="button" value="replaceData(start, end, data)" onclick="callReplaceData()" />
    <input type="button" value="substringData(start, end)" onclick="callSubstringData()" />
</p>
</body>
```


#### Text API
- 텍스트를 추출하여 편집
```javascript
var target = document.getElementById('target').firstChild; 
//Cording everybody! 라는 텍스트를 의미 
//(target이라는 id값을 가진 p태그의 자식이니까)
var data = document.getElementById('data');
var start = document.getElementById('start');
var end = document.getElementById('end');

function callAppendData(){
    target.appendData(data.value); 
    // target 뒤에 data 삽입
  	// cording everbody!JavaScript
}
function callDeleteData(){
    target.deleteData(start.value, end.value);
  	// start.value(0부터 세므로 0~5, 6번째)값에서 시작하여 end.value(5개)값만큼 삭제
  	// Cordierybody! (ng ev삭제)
}
function callInsertData(){
    target.insertData(start.value, data.value);
  	// start.value(6번째)에 data삽입
    // CordiJavaScriptng everybody!
}
function callReplaceData(){
    target.replaceData(start.value, end.value, data.value);
  	// start.value(6번쨰)부터 end.value(5개)까지의 값을 data로 변경
    // CordiJavaScripterybody!
}
function callSubstringData(){
    alert(target.substringData(start.value, end.value));
    // start.value(6번째)부터 end.value(5개)까지 값 추출
  	// ng ev
}
```