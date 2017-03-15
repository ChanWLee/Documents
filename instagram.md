# Instagram accessToken 받는 방법
## 브라우저에서 입력 - auth code 구하기
accessToken 받기위한 코드, 한번 accessToken 받으면 재사용 불가능
- 최소설정:  https://api.instagram.com/oauth/authorize/?client_id=CLIENT_ID&redirect_uri=REDIRECT_URI&response_type=code
> - REDIRECT_URI : http://127.0.0.1 가능
> - CLIENT_ID : instagram 에서 발급받은 ID
> - scope=likes+public_content : 추가적으로 scope에 대한 내용을 넣어서 accessToken을 받을 수 있다. scope는 따로 권한을 승인받아야 하기에 accessToken만 받을 때는 빼고 진행한다.
> - 예시: https://api.instagram.com/oauth/authorize/?client_id=1234567890&redirect_uri=http://127.0.0.1&response_type=code

##### auth 코드 받기
브라우저 창이 리다이렉트 되면, 아래와 같은 코드를 확인할 수 있다.<br/>
http://127.0.0.1/?code=9d663931439f4045a55e42c734ade472

##### auth 코드
`9d663931439f4045a55e42c734ade472`
<br/>발급받을 때마다 코드는 달라진다.


## 터미널에서 accessToken 받기
CLIENT_ID, CLIENT_SECRET, REDIRECT_URI, code 를 사용해서 accessToken 을 받는다.
```shell
curl -d "client_id=CLIENT_ID&client_secret=CLIENT_SECRET&grant_type=authorization_code&redirect_uri=http://127.0.0.1&code=9d663931439f4045a55e42c734ade472" https://api.instagram.com/oauth/access_token
```
##### accessToken 받기 출력물
json 형태의 데이터를 받는다. CLIENT_ID 등록자의 정보와 accessToken을 확인한다.
```json
{"user": {"id": "-------", "username": "------", "website": "", "bio": "", "profile_picture": "https://ig-s-a-a.akamaihd.net/hphotos-ak-xat1/t51.2885-19/11906329_960233084022564_1448528159_a.jpg", "full_name": "-------"}, "access_token": "----------------------"}
```

### 일부 기능을 사용하기 위해서는 권한을 승인 받아야한다.
- 애플리케이션에 대한 설명을 제출 / 검토후 승인 받아야 한다.
- [플랫폼 정책](https://www.instagram.com/about/legal/terms/api/) / [권한 검토 문서](https://www.instagram.com/developer/review/)를 참조.
- [scope](https://www.instagram.com/developer/authorization/)의 종류
>  basic, comments, follower_list, likes, public_content, relationships
<br/>scope는 복수로 선택 가능하다.
