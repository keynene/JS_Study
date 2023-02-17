## 💻[Error/React] Module not found: Error: You attempted to import ...
- import된 js파일의 경로 에러
- CRA(create-react-app)에서 컴파일은 **src폴더 내부에서만** 일어나기 때문에,
src폴더 외부의 파일을 import할 때 발생하는 에러임.
<br>
#### 🤷🏻‍♀️src폴더 외부 파일을 import 하려면?
   : public폴더 이용 (주로 img파일 저장)
   : public폴더는 컴파일 이후 index.html 기준으로 불러오기 때문
   : public폴더는 CRA 배포 시, 실제 서버에 배포되는 폴더임

* * *

### 😐하여튼, src폴더로 파일을 이동해주면 해결됨
#### 에러 발생 시 디렉토리
Join.js파일을 분리하여 App.js에 import 해주려고 했는데, 해당 에러 발생!
![](https://velog.velcdn.com/images/keynene/post/7e1fa040-0c99-4189-9727-3776102ed58b/image.png)
<br>

#### routes 디렉토리를 src 안으로 옮겨주자
에러해결됨 
옮기는 김에 파일명도 대문자로 수정해줬다 
(컴포넌트 파일은 대문자로 저장하는게 국룰)
![](https://velog.velcdn.com/images/keynene/post/79271d58-ee8d-495b-87e2-713287a838a7/image.png)

* * *

### 📚정리
1. react는 import할 때 **src 내부의 폴더만 참조한다**
  : public폴더에 이미지를 저장해서 불러오는 방법도 있음
  : public은 주로 이미지만 저장하고, index.html로 바로 불러온다.
  <br>
2. 컴포넌트 파일 및 컴포넌트 파일 저장 폴더는 무조건 **src폴더에 저장**하자.
<br>
3. 자꾸 까먹는데, **컴포넌트 파일명은 대문자가 국룰**이다.


