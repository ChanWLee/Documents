#node.js 설치
## node.js 설치/설정

```shell
$ curl -O https://nodejs.org/dist/v4.4.2/node-v4.4.2-linux-x64.tar.xz
$ unxz node-v4.4.2...tar.xz
$ tar -xvf node-v4.4.2...tar
$ echo $PATH
$ vi /etc/profile
```

```vi
export PATH=$PATH:/설치경로/node-v0.10.28/bin
```

`$ source /etc/profile`

## node.js web 서버

`$ vi test.js`
```shell
var http = require('http');
http.createServer(function(req,res){
     res.writeHead(200,{'Content-Type':'text/plain'});
     res.end('Hello World\n');
}).listen(1337);
```
브라우저에서 `http://localhost:1337` 접속

## mongodb 연동

```shell
$ node test.js &
$ vi mongoTest.js
```
```vi
var MongoClient = require('mongodb').MongoClient;
var url = 'mongodb://localhost/test';
function callback(err,db){
	console.log('err:'+err+'\ndb:'+db.collection('test'));
	db.collection('test').insert({
		'ok':1
	}, function(e){
		console.log(e);
		db.close();
	});
}
MongoClient.connect(url, callback);
```
`$ node mongoTest.js`


error: cannot find module 'mongodb'
```shell
$ npm install mongodb
$ node mongoTest.js
```

mongo db에서 입력된 값 확인
```shell
mongodb> use test
mongodb> db.test.find()
```

_ _ _


### forever package 설치
node.js를 실행하다 보면 서버로 백그라운드에서 실행을 하는데도 터미널을 닫으면 프로세스가 종료가 되는 현상이 있었다.
`$ node test.js &`

그래서 설치하는 package가 forever

`$ npm install forever -g`

// test.js 실행
`$ forever start test.js`

// 실행 된 node.js 프로세스 리스트 확인
`$ forever list`

// 실행 된 node.js 프로세스 정지
`$ forever stop 프로세스번호`
`$ forever stopall`
