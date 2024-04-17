
---
title : "docker compose kafka"
---

### docker compose 설정파일
    - kafka-compose.yml 파일을 만든다
    - 
      ~~~
      version: '2'
      
      services:
        zookeeper:
          image: confluentinc/cp-zookeeper:latest
          environment:
            ZOOKEEPER_SERVER_ID: 1
            ZOOKEEPER_CLIENT_PORT: 2181
            ZOOKEEPER_TICK_TIME: 2000
            ZOOKEEPER_INIT_LIMIT: 5
            ZOOKEEPER_SYNC_LIMIT: 2
          ports:
            - "22181:2181"
      
        kafka:
          image: confluentinc/cp-kafka:latest
          depends_on:
            - zookeeper
          ports:
            - "29092:29092"
          environment:
            KAFKA_BROKER_ID: 1
            KAFKA_ZOOKEEPER_CONNECT: 'zookeeper:2181'
            KAFKA_ADVERTISED_LISTENERS: PLAINTEXT://kafka:9092,PLAINTEXT_HOST://localhost:29092
            KAFKA_LISTENER_SECURITY_PROTOCOL_MAP: PLAINTEXT:PLAINTEXT,PLAINTEXT_HOST:PLAINTEXT
            KAFKA_INTER_BROKER_LISTENER_NAME: PLAINTEXT
            KAFKA_OFFSETS_TOPIC_REPLICATION_FACTOR: 1
            KAFKA_GROUP_INITIAL_REBALANCE_DELAY_MS: 0
      ~~~

### docker compose 실행
  ~~~
  % docker-compose -f kafka-compose.yml up -d
  ~~~
  - -f : 뒤에 위에서 작성한 kafka-compose.yml 파일 경로
  - up : 실행
  - -d : detach 모드. background 로 실행
 
 
### docker 상태 확인
  ~~~
  % docker ps

  CONTAINER ID   IMAGE                              COMMAND                   CREATED          STATUS          PORTS                                        NAMES
  1e22c148a154   confluentinc/cp-kafka:latest       "/etc/confluent/dock…"   13 minutes ago   Up 13 minutes   0.0.0.0:9092->9092/tcp                       kafka-kafka-1
  72ac23bde699   confluentinc/cp-zookeeper:latest   "/etc/confluent/dock…"   13 minutes ago   Up 13 minutes   2888/tcp, 0.0.0.0:2181->2181/tcp, 3888/tcp   kafka-zookeeper-1
  ~~~
  
  - 컨테이너 로그 확인
    ~~~
    % docker logs 1e22c148a154
    ~~~

### topic 생성
  ~~~
  $ docker-compose -f kafka-compose.yml exec kafka kafka-topics --create --topic my-topic --bootstrap-server kafka:9092 --replication-factor 1 --partitions 1
  ~~~
