# Docker 명령어
* Docker Hub 에서 image 검색
```shell
$ docker search ubuntu
```

* image 다운받기
```shell
$ docker pull ubuntu:latest
```

* 로컬 image 목록확인
```shell
$ docker images
```

* 컨테이너 생성/실행
```shell
$ docker run -i -t --name hello ubuntu
```
```shell
$ docker run -d -p 80:80 -v /root/data:/data --name hello-nginx hello:0.1
```
> -i : interactive, 컨테이너와 상호적으로 주고받겠다.<br/>
-t : Rseudo-tty<br/>
-i -t : 터미널 환경 조성<br/>
-d : 백그라운드 실행<br/>
-p 80:80 : port 연결, 앞이 host, 뒤가 컨테이너<br/>
-v /root/data:/data : 디렉토리 연결, 앞이 host, 뒤가 컨테이너<br/>
--name (컨테이너 이름 지정) (image 이름)

* 컨테이너 목록 확인
```shell
$ docker ps //동작하고 있는 컨테이너만 출력
$ docker ps -a // 정지한 컨테이너도 출력
```

* 컨테이너에 접속
```shell
$ docker attach hello
```

* 컨테이너 exit
`Ctrl + P and Ctrl + Q, 순서대로`

* 외부에서 컨테이너 내부 명령어 실행
```shell
$ docker exec hello pwd
```

* 컨테이너 삭제
```shell
$ docker rm hello
```

* 이미지 삭제
```shell
$ docker rmi ubuntu:latest
```

* 컨테이너가 실행되면서 바뀐 내용 출력
```shell
$ docker diff hello
```
> Add, Change, Delete

* 이미지 생성
```shell
$ docker build --tag hello:0.1
```
```shell
$ docker commit hello chan/hadoop:0.1
```
> hello : 컨테이너 이름,<br/> chan/haddop : 이미지 이름,<br/> 0.1 : tag

* docker hub 에 push
```shell
$ docker push chan/hadoop:0.1
```
> chan : dockerhub ID,<br/> chan/hadoop : 이미지 이름,<br/> 0.1 : tag
