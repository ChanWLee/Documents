1. hadoop 이미지 만들기
  1. 먼저 ubuntu 이미지로 컨테이너 생성
  ```shell
  $ docker run -i -t --name hadoop ubuntu:latest
  ```
  1. 컨테이너 안에서 실행
  ```shell
  $ apt-get update
  $ apt-get install openjdk-8-jdk
  $ java -version
  ```
  1. wget, vim 설치
  ```shell
  $ apt-get install wget
  $ apt-get install vim
  ```
  1. etc/hadoop/hadoop-env.sh 수정
  ```shell
  export JAVA_HOME="/usr/lib/jvm/java-8-openjdk-amd64"
  export HADOOP_HOME="/root/hadoop-2.7.3"
  ```
  1. etc/hadoop/core-site.xml 수정
  ```xml
  <configuration>
    <property>
        <name>fs.defaultFS</name>
        <value>hdfs://localhost:9000</value>
    </property>
    <property>
        <name>hadoop.tmp.dir</name>
        <value>/root/hadoop-2.7.3/tmp</value>
    </property>
  </configuration>
  ```
  1. etc/hadoop/hdfs-site.xml 수정
  ```xml
  <configuration>
    <property>
        <name>dfs.replication</name>
        <value>1</value>
    </property>
  </configuration>
  ```
  1. etc/hadoop/yarn-site.xml 수정 (yarn 을 위한 설정)
  ```xml
  <configuration>
    <property>
        <name>yarn.nodemanager.aux-services</name>
        <value>mapreduce_shuffle</value>
    </property>
  </configuration>
  ```
  1. 다른 노드에 연결하기 위한 ssh 설치
  ```shell
  $ apt-get install ssh
  ```
  1. ssh 를 위한 키파일 생성
  ```shell
  $ cd ~/
  $ ssh-keygen -t rsa -P '' -f ~/.ssh/id_dsa
  $ cd .ssh
  $ cat id_dsa.pub >> authorized_keys
  ```
  1. namenode 포맷
  ```shell
  $ bin/hadoop namenode -format
  ```
  1. `Ctrl + P + Q` 로 컨테이너에서 이탈
  1. 지금까지 작업한 컨테이너를 이미지로 commit
  ```shell
  $ docker commit hadoop dockerhubid/hadoop:0.1
  ```  
1. hadoop word count 테스트

  매우 유명한 하둡 예제인 wordcount를 테스트로 실행해본다.
  1. 컨테이너 접속
  ```shell
  $ docker attach hadoop
  ```
  1. hadoop 디렉토리로 이동해서 모든 노드를 시작
  ```shell
  $ sbin/start-all.sh
  ```
  1. ssh 접속 문제 생기면
  ```shell
  $ service ssh restart
  ```
  1. 노드확인
  ```shell
  $ jps
  ```
  1. 텍스트 파일 넣을 디렉토리 생성
  ```shell
  $ bin/hadoop fs -mkdir -p /home/input
  $ bin/haddop fs -ls /home/
  ```
  1. LISENCE.txt 파일을 input 디렉토리에 넣기
  ```shell
  $ bin/hadoop fs -put LISENCE.txt /home/input
  ```
  1. wordcount.jar 파일 실행
  ```shell
  $ bin/hadoop jar share/hadoop/mapreduce/hadoop-mapreduce-examples-2.7.3.jar wordcount /home/input /home/output
  ```
  1. 결과확인
  ```shell
  $ hadoop fs -cat /home/output/*
  ```
