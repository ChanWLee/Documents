# Kafka
LinkedIn 에서 개발된 Distributed Messaging System
producer, broker, consumer로 구성

- 분산/복제 구성을 손쉽게 할 수 있다.
- 기존 메세징 시스템  -저장->  메모리,<br />
  kafka  -저장->  파일시스템
- 다수메시지 : batch형태 -> brokcer
> 한번에 전달,<br />
  TCP/IP 라운드 트립 횟수를 줄일 수 있다.
- _producer_ 는 broker 에게 _data를 기록_
- _consumer_ 는 broker 로 부터 _data를 읽음_
- data 는 _topic 에 저장_
- topic 은 partition 에 _분할, 복제_ 되어 있음


### kafka 다운
```shell
$ wget http://mirror.apache-kr.org/kafka/0.10.0.1/kafka_2.11-0.10.0.1.tgz
$ tar -xzf kafka_2.11-0.10.0.1.tgz
$ cd kafka_2.11-0.10.0.1.tgz
```

### zookeeper 구동
```shell
$ bin/zookeeper-server-start.sh config/zookeeper.properties
```

### Topic 생성
```shell
$ bin/kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic test
```

### Topic 확인
```shell
$ bin/kafka-topics.sh --list --zookeeper localhost:2181
```

### Topic 에 메세지 보내기
```shell
$ bin/kafka-console-producer.sh --broker-list localhost:9092 --topic test
This is a message
This is another message
```

### Consumer 로 메세지 가져오기
```shell
$ bin/kafka-console-consumer.sh --zookeeper localhost:2181 --topic test --from-beginning
```
