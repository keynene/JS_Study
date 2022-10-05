### Event Load
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <title>Document</title>
    <script>
        /* 문서로딩 에러 */
        var t = document.getElementById('target');
        console.log(t); //null

        /* load : 문서로딩 에러 해결 */
        window.addEventListener('DOMContentLoaded', function(){
            var t1 = document.getElementById('target');
            console.log(t1);  //Hello
        });
    </script>
</head>
<body>
    <p id="target">Hello</p>
</body>
</html>
```
- 일반적으로 html코드 이전에 script코드를 호출하는 경우가 많은데,
  상기 /* 문서로딩에러 */ 부분과 같이 html이 실행되기도 전에 상단에서 js코드로 id값이 target인 요소를 찾는 경우 값을 찾지 못하여 에러가 발생함(null)
- 이러한 문제를 해결하기 위해 내장event중 load 사용 필요