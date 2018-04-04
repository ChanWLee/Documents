# docker upgrade

## docker old versions remove

docker를 삭제해도 docker image는 그대로 보존된다

```
# dnf remove -y docker docker-common container-selinux docker-selinux docker-engine
```

## docker ce repository 추가

```
# curl -o /etc/yum.repos.d/docker-ce.repo https://download.docker.com/linux/fedora/docker-ce.repo
```

## install docker ce

```
# dnf -y install docker-ce
```

## docker image, container, volume 들과 사용자 설정파일 위치

`/var/lib/docker`
