# Instagram accessToken 받는 방법
## 브라우저에서 입력 - auth code 구하기 : input
accessToken 받기위한 코드, 한번 accessToken 받으면 재사용 불가능
- REDIRECT_URI=http://127.0.0.1 가능
- CLIENT_ID=instagram 에서 발급받은 ID
- https://api.instagram.com/oauth/authorize/?client_id=CLIENT_ID&redirect_uri=REDIRECT_URI&response_type=code
> 예시: https://api.instagram.com/oauth/authorize/?client_id=CLIENT_ID&redirect_uri=http://127.0.0.1&response_type=code

##### auth 코드 받기 : ouput, getting auth code
브라우저 창이 리다이렉트 되면, 아래와 같은 코드를 확인할 수 있다.
http://127.0.0.1/?code=9d663931439f4045a55e42c734ade472

##### 코드 : using code
9d663931439f4045a55e42c734ade472

## 터미널에서 accessToken 받기 : do curl for getting accessToken in terminal
CLIENT_ID, CLIENT_SECRET, REDIRECT_URI, code 를 사용해서 accessToken 을 받는다.
```terminal
curl -d "client_id=CLIENT_ID&client_secret=CLIENT_SECRET&grant_type=authorization_code&redirect_uri=http://127.0.0.1&code=9d663931439f4045a55e42c734ade472" https://api.instagram.com/oauth/access_token
```
##### 출력물 : output
json 형태의 데이터를 받는다. CLIENT_ID 등록자의 정보와 accessToken을 확인한다.
```json
{"user": {"id": "-------", "username": "------", "website": "", "bio": "", "profile_picture": "https://ig-s-a-a.akamaihd.net/hphotos-ak-xat1/t51.2885-19/11906329_960233084022564_1448528159_a.jpg", "full_name": "-------"}, "access_token": "----------------------"}
```
