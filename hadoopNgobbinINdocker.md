# hadoop, gobblin 도커에서 사용하기
  설치환경
  docker image : ubuntu:latest<br/>
  hadoop<br/>
  gobblin<br/>
  kafka<br/>
  java<br/>

  1. [docker 에 하둡설치 / 기본셋팅](hadoop_in_docker.md)
  1. 컨테이너 내부
    1. 설치
      1. kafka 설치
      ```shell
      $ wget http://mirror.apache-kr.org/kafka/0.10.0.1/kafka_2.11-0.10.0.1.tgz
      $ tar -xzf kafka_2.11-0.10.0.1.tgz
      $ cd kafka_2.11-0.10.0.1
      ```
      1. gobblin 설치
    1. 셋팅
      1. gobblin 셋팅
        - pull 파일에 job.jars 추가
        ```pull
        job.jars=/home/gobblin-dist/lib/fbingestor.jar,/home/gobblin-dist/lib/*.jar
        ```
        - gobblin-mapreduce.properties 수정
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
      export HADOOP_BIN_DIR=/home/hadoop-2.7.3/bin
      ```
    1. 실행
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
      $ bin/zookeeper-server-start.sh config/zookeeper.property
      ```
      1. kafka 실행
      ```shell
      $ cd /home/kafka_2.11-0.10.0.1
      $ bin/kafka-server-start.sh config/server.property
      ```
      1. gobblin 실행
      ```shell
      $ cd /home/gobblin-dist
      $ bin/gobblin-mapreduce.sh --conf job-config-bpu/wikipedia.pull
      ```