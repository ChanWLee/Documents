# Git 저장소 이동, 복사
git clone, git remote, git push...

## 새로운 디렉토리에 받아서, 올리기

1. git 기존 저장소 내려받기(commit, tags, branches..)
```shell
$ git clone --mirror https://bitbucket.org/user/example.git
```
1. git 새 저장소 등록
```shell
$ cd example
$ git remote set-url --push origin https://github.com/user/mirrored
```
1. 소스(데이터) 올리기
```shell
$ git push --mirror
```

## 사용중인 git 소스디렉토리에서 저장소 등록

1. 기존 저장소 바꾸기
```shell
$ git remote rename origin old_bitbucket
```
1. 새 저장소 등록
```shell
$ git remote add origin https://github.com/user/new-repo.git
```
1. 소스(데이터) 올리기
```shell
$ git push origin master
```
1. 기존 저장소 삭제
```shell
$ git remote rm old_bitbucket
```


