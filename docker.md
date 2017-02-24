# Docker 명령어
* Docker Hub 에서 image 검색
```shell
$ docker search ubuntu
```
* image 다운받기
```shell
docker pull ubuntu:latest
```
* 로컬 image 목록확인
```shell
docker images
```
* 컨테이너 생성/실행
```shell
$ docker run -i -t --name hello ubuntu
```
> -i : interactive
-t : Rseudo-tty
; bash shell 로 접속
--name <컨테이너 이름 지정> <image 이름>
* 컨테이너 목록 확인
```shell
$ docker ps //동작하고 있는 컨테이너
$ docker ps -a // 정지한 컨테이너도
```
