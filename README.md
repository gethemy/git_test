# 1. github 기본 활용

## 1.0 github 토큰 생성

### 1.0.1 Token
<br>github에서 Token을 생성한다.<br>
![alt text](image-4.png)
![alt text](image-5.png)
![alt text](image-6.png)
![alt text](image-7.png)
![alt text](image-8.png)
<br>설명 및 만료일 설정(필요한 기간 만큼)<br>
![alt text](image-9.png)
<br>토큰 보관 (다시 확인할 수 없음)<br>
<br>

## 1.1. git bash

### 1.1.0. 토큰 글로벌 설정
![alt text](image-14.png)
<br>토큰 글로벌 설정(username, email, Token)<br>
![alt text](image-12.png)
<br><span style="color:red">Public profile에 있는 name이 아님!!</span><br>
<br>토큰 글로벌 설정은 로컬 단위로 최초 1회만 진행하면 됨<br>

### 1.1.1. github repository 생성
github에서 repository 생성하기
![alt text](image.png)
![alt text](image-1.png)

### 1.1.2. github repository clone
<br>github에서 `https` copy <br>
![alt text](image-2.png)
<br>git bash 에서 `git clone (레포지터리.git)`<br>
![alt text](image-10.png)
<br>`cd git_test`<br>
![alt text](image-13.png)
<br>브랜치명(main)이 잘 뜨는지 / 폴더에 .git 폴더가 생성되었는지 확인<br>

### 1.1.3. push 과정
우선 인증 이력을 캐시에 저장하도록 설정한다.
`git config --global credential.helper store`
![alt text](image-28.png)
그러면 처음 push할 때만 1회 로그인후 그 이후는 로그인할 필요 없다
`git add .`
`git commit -m "작업내용을 적는 커밋 메시지"`
`git push`
![alt text](image-29.png)


## 1.2. sourcetree

### 1.2.0. 토큰 설정
도구 - 옵션 - 인증 - 추가
![alt text](image-16.png)
![alt text](image-17.png)
![alt text](image-18.png)
<br>호스팅 서비스 : GitHub<br>
<br>선호 프로토콜 : HTTPS<br>
<br>인증 : OAuth<br>
<br>OAuth 토큰 새로고침<br>
![alt text](image-21.png)
![alt text](image-22.png)
![alt text](image-23.png)
<br>인증 성공<br>
![alt text](image-24.png)

### 1.2.1. 클론
클론은 빈 폴더에서 진행
![alt text](image-25.png)
소스 경로 / URL:(레포지터리.git)
목적지 경로:로컬 디렉터리 경로
이름:이름
![alt text](image-27.png)
![alt text](image-26.png)

### 1.2.2. push 과정
디렉터리 내에서 작업하게 되면 스테이지에 올라가지 않은 파일이 생긴다.
![alt text](image-30.png)
스테이지에 파일을 올리면 커밋이 가능해진다.
![alt text](image-31.png)
커밋을 누르면 커밋 메세지를 작성할 수 있고 커밋하면 Push가 가능해진다.
![alt text](image-32.png)
![alt text](image-33.png)
![alt text](image-34.png)