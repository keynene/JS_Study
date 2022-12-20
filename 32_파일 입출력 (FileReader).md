# 📖FileReader
- type이 file인 input태그 ```<input type="file" />``` 또는 API 요청과 같은 File 또는 Blob 객체를 편리하게 처리할 수 있는 방법을 제공하는 객체
- ```abort, load, error```와 같은 이벤트에서 발생한 프로세스를 처리하는데 주로 사용됨
- File 또는 Blob 객체를 읽어서 result 속성에 저장 (result 속성을 통해 데이터를 접근가능)
- **비동기적**으로 동작함

* * *

## 📌비동기로 동작하는 FileReader
- React의  AJAX 요청(API 요청)처럼 잠재적으로 시간이 소모되는 작업은 HTML 페이지 렌더링에 영향을 줄 수 있으므로 동기가 아닌 **비동기**로 동작함
  (비동기로 동작하면 HTML 페이지 렌더링 차단을 피하므로 HTML 페이지 렌더링에 영향을 주지 않음)
- FileReader도 비동기로 동작함
> type이 file인 input 태그 ```<input type="file" />```에서 대용량 파일을 선택하고 파일 정보를 result 속성에 저장하는 과정이 동기식으로 동작한다면, 
파일 정보를 result 속성에 저장할 때까지 HTML 렌더링에 영향을 줄 수 있음
👉🏻그렇기 때문에 FileReader는 비동기 방식으로 동작함

* * *

## 📝FileReader 문법
### new 연산자를 사용하여 FileReader 객체 생성
```const reader = new FileReader();```

파일의 내용은 result 속성에는 문자열 값으로 들어감
우리는 이 result 속성을 이용하여 아래의 4가지 방식으로 파일을 읽을 수 있음

### result 속성의 4가지 방식으로 파일 읽기

1. **readAsText()** : 파일 객체의 내용을 텍스트로 읽음 
2. **readAsDataURL()** : 파일 객체를 읽은 후 데이터 URL으로 변환
3. **readAsArrayBuffer()** : 파일 객체의 내용을 배열 버퍼로 읽음
4. **readAsBinaryString()** : 파일 객체의 내용일 비트 문자열로 읽음 
<br>

### 사용 예제
```javascript
const reader = new FileReader();

// 1. 텍스트
reader.readAsText(File 또는 Blob);

// 2. 데이터를 URL로 변환
reader.readAsDataURL(File 또는 Blob);

// 3. 배열 버퍼
reader.readAsArrayBuffer(File 또는 Blob);

// 4. 비트 문자열
reader.readAsBinaryString(File 또는 Blob);
```

* * *

## 📝File 또는 Blob로 읽는방법
위의 4가지 방식으로 File 또는 Blob로 읽을 수 있는데,
File 또는 Blob으로 읽은 결과를 처리하기 위한 과정도 함께 고려해야 함

주로 ```load, abort, error, progress``` 이벤트에서 FileReader 객체를 사용하여 결과를 확인하거나 처리함

1. **load** : 파일 읽기 작업이 완료되면 작동
2. **error** : 에러로 인해 파일을 읽을 수 없을 때 동작
3. **abort** : abort() 함수를 호출하여 파일 읽기 작업이 취소될 때 동작
4. **progress** : 파일을 읽는 동안 일정한 간격으로 동작

* * *

## 📝FileReadr 객체의 주요 속성
1. **result** : 파일 읽은 결과 또는 null 값 (이 값으로 읽은 파일을 원하는 방식으로 처리함)
2. **error** : 읽기 작업에서 발생한 오류를 설명하는 Error 객체 또는 null 값 (예외처리)
3. **readyStat e** : 객체의 상태를 숫자로 관리함
   - 0은 비어있음(Empty) : FileReader 객체에서 읽기 작업이 수행되지 않았음을 의미
   - 1은 로딩 중(Loading) : 파일을 읽는 중을 의미
   - 2는 완료(Done) : 파일 읽기 작업이 완료되었음을 의미
   
* * *

## 📜이미지 파일 불러와서 미리보기로 보여주기
### React에서 .readAsDataURL() 사용하기
```javascript
//불러온 파일 임시저장할 state (초기값 : 빈상태)
const [attachment, setAttachment] = useState(); 

const onFileChange = (e) => {
  const {
    target: {files},
  } = e;
  const theFile = files[0]; //우선 1개만 보여줄꺼니까 크기 1로 지정
  
  //FileReader 객체 생성
  const reader = new FileReader();  
  
  //로드될 때 result 가져오기
  reader.onloaded = (finishedEvent) => {
    const {
      currentTarget: {result},
    } = finistedEvent;
    //불러온 결과(이미지)를 attachment에 넣기
    setAttachment(result);
  }
  //파일 데이터를 URL로 변환하기
  reader.readAsDataURL(theFile);
}

return(
  (생략)
  
  //파일 선택할 input창 (image파일만 불러오기)
  <input type="file" accept="image/*" onChange={ onFileChange } />

  //파일이 존재할 때만 미리보기 보여주기
  { attachment && <img src={ attachment } width="50px" height="50px" /> }
)
```