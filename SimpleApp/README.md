
http://spark.apache.org/docs/latest/quick-start.html

在hdfs上创建文件

[root@data-srv001 opt]# sudo -u hdfs hadoop fs -mkdir /spark/
[root@data-srv001 opt]# sudo -u hdfs hadoop fs -mkdir /spark/demo

[root@data-srv001 spark]# ls
bin  conf  data  examples  jars  LICENSE  licenses  NOTICE  python  R  README.md  RELEASE  sbin  yarn
[root@data-srv001 spark]# sudo -u hdfs hadoop fs -put README.md /spark/demo

[root@data-srv001 spark]# su  - demo
Last login: Mon Aug 14 21:41:35 CST 2017 on pts/3
[demo@data-srv001 ~]$ hadoop fs -cat /spark/demo/README.md


[demo@data-srv001 SimpleApp]$  spark-submit --class SimpleApp --master local[4] target/SimpleApp-0.0.1-SNAPSHOT.jar 
Lines with a: 62, lines with b: 30
[demo@data-srv001 SimpleApp]$ 

spark-submit --class SimpleApp --master yarn --deploy-mode cluster target/SimpleApp-0.0.1-SNAPSHOT.jar

[demo@data-srv001 SimpleApp]$ spark-submit --class SimpleApp --master yarn --deploy-mode cluster target/SimpleApp-0.0.1-SNAPSHOT.jar

Exception in thread "main" org.apache.hadoop.security.AccessControlException: Permission denied: user=demo, access=WRITE, inode="/user/demo/.sparkStaging/application_1500793305465_0021":hdfs:hadoop:drwxr-xr-x
	at org.apache.hadoop.hdfs.server.namenode.FSPermissionChecker.check(FSPermissionChecker.java:319)
	at org.apache.hadoop.hdfs.server.namenode.FSPermissionChecker.check(FSPermissionChecker.java:292)
	at org.apache.hadoop.hdfs.server.namenode.FSPermissionChecker.checkPermission(FSPermissionChecker.java:213)
	at org.apache.hadoop.hdfs.server.namenode.FSPermissionChecker.checkPermission(FSPermissionChecker.java:190)
	at org.apache.hadoop.hdfs.server.namenode.FSDirectory.checkPermission(FSDirectory.java:1728)
	at org.apache.hadoop.hdfs.server.namenode.FSDirectory.checkPermission(FSDirectory.java:1712)
	at org.apache.hadoop.hdfs.server.namenode.FSDirectory.checkAncestorAccess(FSDirectory.java:1695)
	at org.apache.hadoop.hdfs.server.namenode.FSDirMkdirOp.mkdirs(FSDirMkdirOp.java:71)
	at org.apache.hadoop.hdfs.server.namenode.FSNamesystem.mkdirs(FSNamesystem.java:3896)
	at org.apache.hadoop.hdfs.server.namenode.NameNodeRpcServer.mkdirs(NameNodeRpcServer.java:984)
	at org.apache.hadoop.hdfs.protocolPB.ClientNamenodeProtocolServerSideTranslatorPB.mkdirs(ClientNamenodeProtocolServerSideTranslatorPB.java:622)
	at org.apache.hadoop.hdfs.protocol.proto.ClientNamenodeProtocolProtos$ClientNamenodeProtocol$2.callBlockingMethod(ClientNamenodeProtocolProtos.java)


[root@data-srv001 spark]# sudo -u hdfs hadoop fs -mkdir /user/demo
[root@data-srv001 spark]# sudo -u hdfs hadoop fs -chown demo:hadoop /user/demo
[root@data-srv001 spark]# sudo -u hdfs hadoop fs -ls /user
Found 6 items
drwxr-xr-x   - demo    hadoop          0 2017-08-14 22:31 /user/demo
drwxr-xr-x   - hdfs    hadoop          0 2017-07-14 00:29 /user/hdfs
drwxrwxrwx   - hive    hadoop          0 2017-07-16 15:46 /user/hive
drwxr-xr-x   - hue     hue             0 2017-07-11 15:49 /user/hue
drwxr-xr-x   - oozie   oozie           0 2017-07-11 23:34 /user/oozie
drwxr-xr-x   - user001 hadoop          0 2017-07-22 23:11 /user/user001


然后通过application 控制台能查看输出日志。

http://data-srv005:8042/node/containerlogs/container_1500793305465_0023_01_000001/demo/stdout/?start=-4096


Logs for container_1500793305465_0023_01_000001
ResourceManager

    RM Home 

NodeManager
Tools
	

Lines with a: 62, lines with b: 30



	