# IoT Kafka Producer
IoT Kafka Producer is a Maven application for generating IoT Data events using Apache Kafka. This project requires following tools and technologies.

- JDK - 1.8
- Maven - 3.3.9
- ZooKeeper - 3.4.8
- Kafka - 2.10-0.10.0.0

You can build and run this application using below commands. Please check resources/iot-kafka.properties for configuration details.

```sh
mvn package
mvn exec:java -Dexec.mainClass="com.iot.app.kafka.producer.IoTDataProducer"

```

Alternate way to run this application is using the “iot-kafka-producer-1.0.0.jar” file created by maven. Open command prompt, go to target folder and execute below command.

```sh
java -jar iot-kafka-producer-1.0.0.jar


ssh root@data-srv003 "cd /data/opt/kafka; 

# Zookeeper connection string (see zookeeper docs for details).
# This is a comma separated host:port pairs, each corresponding to a zk
# server. e.g. "127.0.0.1:3000,127.0.0.1:3001,127.0.0.1:3002".
# You can also append an optional chroot string to the urls to specify the
# root directory for all kafka znodes.
zookeeper.connect=data-srv003:2181,data-srv004:2181,data-srv005:2181/kafka


ssh root@data-srv003 "cd /data/opt/kafka; bin/kafka-server-start.sh config/server.properties"
ssh root@data-srv004 "cd /data/opt/kafka; bin/kafka-server-start.sh config/server.properties"
ssh root@data-srv005 "cd /data/opt/kafka; bin/kafka-server-start.sh config/server.properties"

验证kafka是否启动成功
[root@data-srv001 data]# zkCli.sh -server data-srv003 ls /kafka/brokers/ids 
Connecting to data-srv003
2017-08-14 15:22:01,041 [myid:] - INFO  [main:Environment@100] - Client environment:zookeeper.version=3.4.10-39d3a4f269333c922ed3db283be479f9deacaa0f, built on 03/23/2017 10:13 GMT
2017-08-14 15:22:01,044 [myid:] - INFO  [main:Environment@100] - Client environment:host.name=data-srv001
2017-08-14 15:22:01,044 [myid:] - INFO  [main:Environment@100] - Client environment:java.version=1.8.0_141
2017-08-14 15:22:01,046 [myid:] - INFO  [main:Environment@100] - Client environment:java.vendor=Oracle Corporation
2017-08-14 15:22:01,046 [myid:] - INFO  [main:Environment@100] - Client environment:java.home=/data/opt/jdk1.8.0_141/jre
2017-08-14 15:22:01,046 [myid:] - INFO  [main:Environment@100] - Client environment:java.class.path=/data/opt/zookeeper/bin/../build/classes:/data/opt/zookeeper/bin/../build/lib/*.jar:/data/opt/zookeeper/bin/../lib/slf4j-log4j12-1.6.1.jar:/data/opt/zookeeper/bin/../lib/slf4j-api-1.6.1.jar:/data/opt/zookeeper/bin/../lib/netty-3.10.5.Final.jar:/data/opt/zookeeper/bin/../lib/log4j-1.2.16.jar:/data/opt/zookeeper/bin/../lib/jline-0.9.94.jar:/data/opt/zookeeper/bin/../zookeeper-3.4.10.jar:/data/opt/zookeeper/bin/../src/java/lib/*.jar:/data/opt/zookeeper/bin/../conf:
2017-08-14 15:22:01,046 [myid:] - INFO  [main:Environment@100] - Client environment:java.library.path=/usr/java/packages/lib/amd64:/usr/lib64:/lib64:/lib:/usr/lib
2017-08-14 15:22:01,047 [myid:] - INFO  [main:Environment@100] - Client environment:java.io.tmpdir=/tmp
2017-08-14 15:22:01,047 [myid:] - INFO  [main:Environment@100] - Client environment:java.compiler=<NA>
2017-08-14 15:22:01,047 [myid:] - INFO  [main:Environment@100] - Client environment:os.name=Linux
2017-08-14 15:22:01,047 [myid:] - INFO  [main:Environment@100] - Client environment:os.arch=amd64
2017-08-14 15:22:01,047 [myid:] - INFO  [main:Environment@100] - Client environment:os.version=3.10.0-229.20.1.el7.x86_64
2017-08-14 15:22:01,047 [myid:] - INFO  [main:Environment@100] - Client environment:user.name=root
2017-08-14 15:22:01,047 [myid:] - INFO  [main:Environment@100] - Client environment:user.home=/root
2017-08-14 15:22:01,047 [myid:] - INFO  [main:Environment@100] - Client environment:user.dir=/data
2017-08-14 15:22:01,048 [myid:] - INFO  [main:ZooKeeper@438] - Initiating client connection, connectString=data-srv003 sessionTimeout=30000 watcher=org.apache.zookeeper.ZooKeeperMain$MyWatcher@1a86f2f1
2017-08-14 15:22:01,084 [myid:] - INFO  [main-SendThread(data-srv003:2181):ClientCnxn$SendThread@1032] - Opening socket connection to server data-srv003/10.0.2.8:2181. Will not attempt to authenticate using SASL (unknown error)
2017-08-14 15:22:01,167 [myid:] - INFO  [main-SendThread(data-srv003:2181):ClientCnxn$SendThread@876] - Socket connection established to data-srv003/10.0.2.8:2181, initiating session
2017-08-14 15:22:01,175 [myid:] - INFO  [main-SendThread(data-srv003:2181):ClientCnxn$SendThread@1299] - Session establishment complete on server data-srv003/10.0.2.8:2181, sessionid = 0x15dc5acdceb0052, negotiated timeout = 30000

WATCHER::

WatchedEvent state:SyncConnected type:None path:null
[1, 2, 3]



Kafka-manager

kafka-manager.zkhosts="data-srv003:2181,data-srv004:2181,data-srv005:2181"
kafka-manager.zkhosts=${?ZK_HOSTS}
pinned-dispatcher.type="PinnedDispatcher"
pinned-dispatcher.executor="thread-pool-executor"
application.features=["KMClusterManagerFeature","KMTopicManagerFeature","KMPreferredReplicaElectionFeature","KMReassignPartitionsFeature"]

akka {
  loggers = ["akka.event.slf4j.Slf4jLogger"]
"conf/application.conf" line 23 of 41 --56%-- col 1


[root@data-srv001 kafka-manager-1.3.3.8]# ./bin/kafka-manager 
This application is already running (Or delete /data/opt/kafka-manager-1.3.3.8/RUNNING_PID file).
[root@data-srv001 kafka-manager-1.3.3.8]# 


http://data-srv001:9000/


