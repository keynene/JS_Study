### Event
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <title>Document</title>
</head>
<body>
    <style>
        html{border:5px solid red; padding:30px;}
        body{border:5px solid green; padding:30px;}
        fieldset{border:5px solid blue; padding:30px;}
        input{border:5px solid black; padding:30px;}
    </style>
</body>
<fieldset>
    <legend>event propagation</legend>
    <input type="button" id="target" value="target" />
</fieldset>
```
※ 상기 html코드를 모든 예제에 적용

#### Event Target (Bubbling/Capturing)
- event가 여러 태그에서 중복하여 발생 시 호출되는 시점에서 가장 안쪽부터 진행할 것인지, 가장 바깥쪽부터 진행할 것인지 순서 정의 필요
- addEventListener('event 요소', '함수', '캡처링 여부')
  캡처링 false : bubbling
  캡처링 true : capturing 
- bubbling / capturing 은 상반된 개념

#### Bubbling
- event 중복 발생 시 호출되는 시점의 태그에서 "안쪽부터 바깥쪽으로" event 진행하는 방법
- ex) 위 html예제에서 input에서 진행할 경우
     input → fieldset → body → html 순으로 진행
```javascript
function handler(event){
    var phases = ['capturing', 'target', 'bubbling'];
    console.log(event.target.nodeName, this.nodeName, phases[event.eventPhase-1]);
    //.eventPhase : event 함수 호출 시 상태의 값. (1=capturing, 2=target, 3=bubbling)
}

/* bubbling */
document.getElementById('target').addEventListener('click', handler, false);
document.querySelector('fieldset').addEventListener('click', handler, false);
document.querySelector('body').addEventListener('click', handler, false);
document.querySelector('html').addEventListener('click', handler, false);
```

#### Capturing
- event 중복 발생 시 "가장 바깥쪽 태그부터 함수가 호출된 가장 안쪽 태그" 순서로 진행
- ex) 위 html예제에서 input에서 진행할 경우
     html → body → fieldset → input 순으로 진행
```javascript
function handler(event){
    var phases = ['capturing', 'target', 'bubbling'];
    console.log(event.target.nodeName, this.nodeName, phases[event.eventPhase-1]);
    //.eventPhase : event 함수 호출 시 상태의 값. (1=capturing, 2=target, 3=bubbling)
}

/* capturing */
document.getElementById('target').addEventListener('click', handler, true);
document.querySelector('fieldset').addEventListener('click', handler, true);
document.querySelector('body').addEventListener('click', handler, true);
document.querySelector('html').addEventListener('click', handler, true);
```

#### Event 중단
- bubbling/capturing에 모두 적용 가능하며, event 진행 시 중단해야 할 경우 사용
```javascript
function stopHandler(event){
    var phases = ['capturing', 'target', 'bubbling'];
    console.log(event.target.nodeName, this.nodeName, phases[event.eventPhase-1]);
    event.stopPropagation(); 
    // stopPropagation() : event capturing/bubbling을 호출 단계에서 마무리할 떄 사용
}

document.getElementById('target').addEventListener('click', handler, false);
document.querySelector('fieldset').addEventListener('click', handler, false);
document.querySelector('body').addEventListener('click', stopHandler, false);
document.querySelector('html').addEventListener('click', handler, false);
```