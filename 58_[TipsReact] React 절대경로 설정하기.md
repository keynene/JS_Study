## 📖절대경로로 지정하는 이유?
- React로 작업 시 프로젝트 규모가 점점 커지고 import할 파일이 많아지면 상대경로 지정이 어려워짐
- 결론 : ```import component from "../../../component/component...``` 이렇게 쓰기 싫어서임.

* * *

## 📝절대경로 지정하기
### 1. 절대경로 기본값 폴더에 jsconfig.json 파일 만들기
src폴더 말고 그냥 기본 폴더에 만들면 됨
![](https://velog.velcdn.com/images/keynene/post/1bd015df-070d-428f-ae17-639ada0684c4/image.png)

* * *

### 2. jsconfig.json 파일에코드 작성하기
![](https://velog.velcdn.com/images/keynene/post/194953a9-9289-4148-b7b5-7b0c59195972/image.png)

※ 복사하자
```javascript
{
  "compilerOptions": {
    "baseUrl": "src"
  },
  "include": ["src"]
}
```

* * *

### 3. 절대경로로 import 하기
![](https://velog.velcdn.com/images/keynene/post/475402bd-adb1-4aec-a31f-f499054ae5e7/image.png)

* * *

## 📚정리
1. 폴더 개수가 몇 개 없고 파일이 많은 경우 유용하다
2. 라우팅이 수월해지고 가시적이다.