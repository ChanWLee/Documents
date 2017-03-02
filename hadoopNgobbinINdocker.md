# hadoop, gobblin 도커에서 사용하기
  설치환경
  docker image : ubuntu:latest<br/>
  hadoop<br/>
  gobblin<br/>
  kafka<br/>
  java<br/>

## docker 에 하둡설치 / 기본셋팅
  link: [haddop in docker](hadoop_in_docker.md)
#### gobblin에서 hadoop 2.3.0 이 필요함
아래 환경 변수 셋팅할 때 `HADOOP_BIN_DIR` 를 `2.3.0/bin`으로 셋팅
```shell
$ wget https://archive.apache.org/dist/hadoop/core/hadoop-2.3.0/hadoop-2.3.0.tar.gz
$ tar -xzf hadoop-2.3.0.tar.gz
```
---

## 컨테이너 내부 설치/셋팅/실행
#### 설치
  1. kafka 설치
  ```shell
  $ wget http://mirror.apache-kr.org/kafka/0.10.0.1/kafka_2.11-0.10.0.1.tgz
  $ tar -xzf kafka_2.11-0.10.0.1.tgz
  $ cd kafka_2.11-0.10.0.1
  ```
  1. gobblin 설치

---
#### 셋팅
  1. gobblin 셋팅
  ###### pull 파일에 job.jars 추가
  ```pull
  job.jars=/home/gobblin-dist/lib/fbingestor.jar,/home/gobblin-dist/lib/*.jar
  ```
  ###### gobblin-mapreduce.properties 수정<br/>
  기본 8020으로 되어 있는 port를 HDFS의 셋팅값으로 수정
  ```properties
  fs-uri=hdfs://localhost:9000
  ```
  1. 환경변수 셋팅
  `~/.bashrc` 에 추가
  ```shell
  export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
  export GOBBLIN_WORK_DIR=/home/gobblin-dist/working-dir
  export HADOOP_HOME=/home/hadoop-2.7.3
  export HADOOP_BIN_DIR=/home/hadoop-2.3.0/bin
  ```
---
#### 실행
  1. ssh 실행
  ```shell
  $ service ssh restart
  ```
  1. hadoop 실행
  ```shell
  $ cd /home/hadoop-2.7.3
  $ sbin/start-all.sh
  ```
  1. directory 만들고 복사, 확인
  ```shell
  $ bin/hadoop fs -mkdir -p /home/gobblin-dist
  $ bin/hadoop fs -put /home/gobblin-dist /home
  $ bin/hadoop fs -ls /home/gobblin-dist
  ```
  1. zookeeper 실행
  ```shell
  $ cd /home/kafka_2.11-0.10.0.1
  $ bin/zookeeper-server-start.sh config/zookeeper.properties
  ```
  1. kafka 실행
  ```shell
  $ cd /home/kafka_2.11-0.10.0.1
  $ bin/kafka-server-start.sh config/server.properties
  ```
  1. gobblin 실행
  ```shell
  $ cd /home/gobblin-dist
  $ bin/gobblin-mapreduce.sh --conf job-config-bpu/wikipedia.pull --workdir working-dir
  ```
---
#### master, slave1, slave2 구성
  1. 각 docker 실행
  ```shell
  $ docker run -i -t -h master --name master -p 50070:50070 dockerhubid/hadoop:0.1
  $ docker run -i -t -h slave1 --name slave1 --link master:master dockerhubid/hadoop:0.1
  $ docker run -i -t -h slave2 --name slave2 --link master:master dockerhubid/hadoop:0.1
  ```
  1. slave1, 2 의 virtual IP를 확인
  <br/>보통 `172.17.0.xxx` 형태를 띈다.
  1. master 에서 hosts, slaves 파일을 수정
  ```shell
  $ docker attach master
  $ vi /etc/hosts
  ```
  ```
  172.17.0.3 slave1
  172.17.0.4 slave2
  ```
  ```shell
  $ vi hadoop-2.3.0/etc/hadoop/slaves
  ```
  ```
  slave1
  slave2
  master
  ```
  ```shell
  $ hadoop-2.3.0/sbin/start-all.sh
  ```
  ```shell
  namenode, datanode 연결 관련된 질문
  yes 엔터
  yes 엔터
  yes 엔터
  yes 엔터
  ...
  ```
  ###### slave 컨테이너에 접속해, `$ jps`로 slave에 nodemanager, datanode가 돌아가는지 확인
  ###### master 에서 확인하는 방법
  ```shell
  $ hadoop-2.3.0/bin/hadoop dfsadmin -report
  ```
  datanode가 총 3개 돌아가고 있는지 확인
  ```shell
  ...
  Live datanodes (3) :
  ...
  ```
