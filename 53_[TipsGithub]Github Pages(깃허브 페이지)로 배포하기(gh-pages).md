## 📖Github Pages(깃허브 페이지)란?
- 무료 티어 사용자가 퍼블릭 레포지토리에서 무료로 호스팅을 이용할 수 있는 서비스
   (Pro 티어 사용자는 private 레포지토리에서도 사용 가능)
- HTML/CSS/JavaScript로 구성된 파일을 구동하고 배포해 Static 웹 사이트를 호스팅 할 수 있게 해주는 서비스
- 기본적으로 github.io라는 도메인을 사용하게 됨 (커스텀 도메인도 사용 가능)

#### 📚공식문서 : [https://docs.github.com/en/pages/getting-started-with-github-pages](https://docs.github.com/en/pages/getting-started-with-github-pages)

* * *

## 💎Github Pages(깃허브 페이지) 만들기
※ 아래에 깃허브페이지를 만들고 배포하기 위한 방법을 순서대로 게시해놨는데,
우선 깃허브페이지를 제작하기 전에 index.js 파일의 ```<BrowserRouter />```컴포넌트에 
```basename``` 속성을 사용하고 있는지 확인해보자

앞으로 발생할 많은 에러를 미리 해결해주므로 꼭 확인해보자🙆🏻‍♀️
```javascript
/* index.js */

(중략)
<BrowserRouter basename={process.env.PUBLIC_URL}> 
  (중략)
</BrowserRouter>
(중략)
```
>
>#### ❓ basename 이란
>   : ```<BrowserRouter />```컴포넌트로 라우팅 시 모든 경로의 **기본 URL을 설정**해주는 속성
>
>   깃허브페이지는 일반적으로 homepage주소를 github 레포지토리로 지정하는데,
>   이 때, 메인페이지 경로를 ("/")로 지정하고, 깃헙페이지를 배포해버리면
>   <span style="color:red">**error 404** </span>또는 <span style="color:red">**빈페이지**</span>만 출력하게 된다.
>
>   이러한 문제를 해결하기 위해  public 주소를 기본경로로 지정해두면
>   로컬 작업에도, 깃헙페이지 배포 후에도 정상적으로 작동하게 된다.
>
>   📝 [basename 관련 문서](https://v5.reactrouter.com/web/api/BrowserRouter)

* * *

### 1. 레포지토리 생성
이제 본격적으로 깃허브페이지를 생성/배포 해보자

깃허브 실행 > Repositories > New 에서 레포지토리 생성 후 배포할 파일 업로드/커밋
![](https://velog.velcdn.com/images/keynene/post/2fef70c3-af3b-48f0-8320-ca83d6d97a1b/image.png)

* * *

### 2. Github와 로컬 프로젝트 연결 / Github Pages URL 확인
업로드/커밋 완료한 Github 레포지토리에 접속 > [Setting]
![](https://velog.velcdn.com/images/keynene/post/50efbcbb-f190-4f0c-a516-3501925726fd/image.png)

[Setting] > [Pages] > Branch : main으로 변경 후 Save
![](https://velog.velcdn.com/images/keynene/post/47d2f0a9-dd6e-4c50-a53f-b3a475ddb04d/image.png)

Save 완료하면 published되었다는 안내와 함께 URL을 안내해줌

![](https://velog.velcdn.com/images/keynene/post/a07d2b3c-6176-4955-9f70-7a076943ee9e/image.png)

❗❗❗ 현재는 내 페이지와 연동이 되지 않았기 때문에 error 404 페이지가 뜸 ❗❗❗

* * *

### 3. React 프로젝트에 gh-pages 설치
👉🏻 gh-pages : React 프로젝트를 쉽게 배포할 수 있는 라이브러리
해당 파일의 터미널 > ```npm install gh-pages --save-dev``` 입력

(해당폴더 우클릭 > vsc열기 > [Terminal] > new terminal > ```npm install gh-pages --save-dev``` 입력)

* * *

### 4. package.json 설정
React 프로젝트 폴더에서 package.json 실행 > homepage, predeploy, deploy 추가

**homepage** : package.json 제일 아래에 아래 문구 추가 (윗 줄에 콤마(,) 붙여서 입력)
```"homepage": "https://깃허브ID.github.io/레포지토리이름/",```
![](https://velog.velcdn.com/images/keynene/post/ddf181cd-eaf7-4647-901c-ae897b941b24/image.png)

**predeploy, deploy** : package.json "scripts"에 아래 문구 그대로 추가
                          (콤마로 구분되니까 이에 유의할 것!)
                          
```"predeploy": "npm run build",```
```"deploy": "gh-pages -d build"```
![](https://velog.velcdn.com/images/keynene/post/7d394973-1af1-47b4-9253-0bd5fd9e3a14/image.png)

* * *

### 5. npm run deploy
package.json까지 설정 완료했으면 터미널을 실행하여 아래와 같이 입력
```npm run deploy```

별다른 에러가 안 뜨면? 성공🎉


![](https://velog.velcdn.com/images/keynene/post/4121b291-beeb-450a-b925-736751b27181/image.png)



👉🏻 ```npm run deploy``` 입력하면?
이전에 package.json에서 설정해줬던
```"predeploy" : "npm run build"```가 실행되어 자동으로 빌드되고,
```"deploy" : "gh-pages -d build"```가 실행되어 Github 원격 저장소에 배포에 필요한 파일을 보내줌
<br>
>#### 🤦🏻‍♀️만약 터미널에 Published가 아닌, 에러가 뜬다면?..
**<span style="color : red">errno : -4058</span>** : **Git** 새로 설치하기..
나는 소스트리를 이용해서 commit 해왔기 때문에 Git 설치가 따로 필요하지 않았는데,
Git 버전이 낮거나 설치되어 있지 않으면 원격 저장소에 파일을 보내줄 수가 없으므로 발생한 에러였음
소스트리는 Git cli를 로컬이 아닌 다른 경로로 실행해주는 듯...?


* * *

### 6. 레포지토리 재설정
deploy까지 완료하면 다시 Github의 [Setting] > [Pages]에 접속
Branch main → **gh-pages**로 변경 후 Save

**❗❕ 5번까지의 과정이 완료되어야지만 gh-pages 브랜치가 추가됨 ❕❗**
![](https://velog.velcdn.com/images/keynene/post/1aea466c-8de8-4c62-bab3-f0965fb613d6/image.png)

* * *

### 7. 배포된 페이지 확인!
2번에서 확인한 URL로 접속하여 내 페이지가 뜨는지 확인!
**⏳ 원래 3~10분정도 걸리니까 조급해하지 말자 ⌛**
![](https://velog.velcdn.com/images/keynene/post/d984e5e5-fa88-47b2-aecd-9c38d53ff38c/image.png)

#### 🎉성 공🎉
앞으로 프로젝트 소스코드를 수정하거나, 업데이트가 필요할 경우
git 레포지토리에 커밋 후 터미널에 ```npm run deploy``` 를 입력하여 자동빌드/배포를 하면 끝👏🏻

* * * 

## ❓빌드까지 성공했는데 에러가 난다😥
#### 🙅🏻‍♀️에러종류
1. error 404
2. README
3. 빈 페이지
4. 개발자가 지정해놓은 디폴트 페이지

에러 종류도 알고싶지 않았지만... 다음에 다시 만날 상황을 대비해서 추후 포스팅에서 다루겠음^^...







