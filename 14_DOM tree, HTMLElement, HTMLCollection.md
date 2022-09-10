### DOM Tree
- 문서노드 > 요소노드 > 어트리뷰트노드 > 텍스트노트 순으로 구성된 중첩관계

#### 요소저장
```javascript
var li = document.getElementById('active');
console.log(li.constructor.name); 
//HTMLElement : 엘리먼트(단수) 단수이므로 li에 값 저장
var lis = document.getElementsByTagName('li');
console.log(lis.constructor.name); 
//HTMLCollection : 유사배열(복수) 복수이므로 lis에 유사배열 형태로 저장
```

#### 요소검사/삭제
```javascript
/*before 그룹*/
console.group('before');
var lis = document.getElementsByTagName('li');
for(var i=0; i<lis.length; i++){
    console.log(lis[i]);
}
console.groupEnd();
//li라는 태그를 가진 요소들 전부 lis라는 유사배열에 저장

/*after 그룹*/
console.group('after');
lis[1].parentNode.removeChild(lis[1]); // lis[1] : <li>CSS</li> 삭제
for(var i=0; i<lis.length; i++){
    console.log(lis[i]);
}
console.groupEnd();
//lis에서 lis[1]에 해당하는 인자 삭제
```
- conole.group : groupEnd()함수 전까지 그룹을 가시적으로 출력해줌
- removeChild() : 해당 배열/값의 노드 삭제