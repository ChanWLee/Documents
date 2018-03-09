# 개발환경 셋팅

## fedora 설치

## password 수정

## 필수 프로그램 설치

jdk, git, gradle, docker, nodejs 설치

### jdk 설치

```bash
  $ sudo yum -y install java-1.8.0-openjdk-devel.x86_64
  $ javac -version
```

- java 위치확인

  ```bash
  $ which javac
  $ readlink -f /usr/bin/javac
  ```

- /etc/profile 에 export~ 내용 추가

  ```bash
  $ vi /etc/profile
  ```

  ```batch
  export JAVA_HOME /usr/lib/jvm/java-1.8.0-openjdk-1.8.0.141-1.b16.fc24.x86_64
  ```

- 재접속/재로그인 후 확인

  ```bash
  $ echo $JAVA_HOME
  ```

### gradle 설치

```bash
  $ wget https://downloads.gradle.org/distributions/gradle-4.0.1-bin.zip
  $ sudo mkdir /opt/gradle
  $ unzip -d /opt/gradle gradle-4.0.1-bin.zip
```

[install manual url](https://gradle.org/install/)

### sshd booting시 자동시작

```bash
  systemctl enable sshd.service
```

### docker 설치

#### docker start without sudo

$USER : 현재 사용유저아이디 docker 그룹생성, 현재 사용유저 docker 그룹에 추가, docker서비스 재시작

```bash
  $ sudo groupadd docker && sudo gpasswd -a $USER docker && sudo systemctl restart docker
  $ newgrp docker
```

## IDE 설치

### IntelliJ 설치

IntelliJ 실행

```bash
$ bin/idea.sh
```

- plugin

  1. grep console
  2. idea-gitignore
  3. makdown support
  4. sonarlint
  5. bash support
  6. advanced java folding

#### toolbar 수정

- git : Settings > Menus and Toolbars > Navigation Bar Toolbar > NavBarVcsGroup > VcsNavBarToobarActions

#### shotcut

- change view : Ctrl + ` > 4 > 2

#### keymap

- window > editor tabs > close

  - `Ctrl + w`

## 용량 삭제

### clean PackageKit cache

```bash
$ sudo pkcon refresh force -c -1
$ sudo vi /etc/PackageKit/PackageKit.conf
```

```config
# Keep the packages after they have been downloaded
KeepCache=false
```

## keyring 문제

- System Tool > Passwords and Keys
- new Password Keyring
- set password as empty
- delete 'Login' Keyring
- Right-click the new keyring, and 'set as a default'
