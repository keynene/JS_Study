### 정규표현식
- 특정한 규칙을 가진 문자열의 집합을 표현하는 데 사용하는 형식 언어. 문자열의 검색(추출)과 치환을 위해 지원함.
ex) 어떠한 정보 속에서 url 추출 등

#### [검색]

1. 원하는 정보 추출
String.exec()
>var pattern = /a/;    
console.log(pattern.exec('abcde'));  →a반환
var pattern = /a./;    
console.log(pattern.exec('abcde'));  →ab반환  
var pattern = /a/;    
console.log(pattern.exec('bcdef'));  →null (찾고자하는 결과가 없음)

2. 원하는 정보 존재유무 테스트[true/false]
String.test()
>var pattern = /a/;    
console.log(pattern.test('abcde'));  →true
var pattern = /a/;    
console.log(pattern.test('bcde'));  →false

3. 원하는 문자 검색 후 반환
String.match()
>var pattern = /a/;
var str = 'abcdef';
console.log(str.match(pattern));  →a반환
var str = 'bcdef';
console.log(str.match(pattern));  →null



#### [치환]
1. 원하는 문자열 검색 후 치환(변경)
String.replace()
>var pattern = /a/;
var str = 'abcdef';
console.log(str.replace(pattern, 'A'));  →Abcdef 반환

#### [옵션]
1. "i"옵션 - 대소문자 구분하지 않게해줌
>var xi = /a/;
var oi = /a/i;
console.log("Abcde".match(xi));  //null
console.log("Abcde".match(oi));  //A 반환

2. "g"옵션 - 중복 문자도 검색 가능
>var xg = /a/;
var og = /a/g;
console.log("abcdea".match(xg));  //a 반환
console.log("abcdea".match(og));  //a, a 반환
