# IoT Spark Processor
IoT Spark Processor is a Maven application for processing IoT Data streams using Apache Spark. Processed data is persisted in to Cassandra Database. This project requires following tools and technologies.

- JDK - 1.8
- Maven - 3.3.9
- ZooKeeper - 3.4.8
- Kafka - 2.10-0.10.0.0
- Cassandra - 2.2.6
- Spark - 1.6.2 Pre-built for Hadoop 2.6

Please refer "IoTData.cql" file to create Keyspace and Tables in Cassandra Database, which are required by this application.

You can build and run this application using below commands. Please check resources/iot-spark.properties for configuration details.

```sh
mvn package
spark-submit --class "com.iot.app.spark.processor.IoTDataProcessor” iot-spark-processor-1.0.0.jar
```



----------------------------------------
1. setup cassandra cluster

Last login: Mon Aug 14 22:51:13 CST 2017 on pts/3
[hadoop@data-srv001 ~]$ cqlsh
Connected to Test Cluster at 127.0.0.1:9042.
[cqlsh 5.0.1 | Cassandra 3.11.0 | CQL spec 3.4.4 | Native protocol v4]
Use HELP for help.
cqlsh> 

查看keyspaces
cqlsh>  DESCRIBE KEYSPACES

system_traces  system_schema  system_auth  system  system_distributed

cqlsh> describe traffickeyspace;

CREATE KEYSPACE traffickeyspace WITH replication = {'class': 'SimpleStrategy', 'replication_factor': '1'}  AND durable_writes = true;

CREATE TABLE traffickeyspace.window_traffic (
    routeid text,
    recorddate text,
    vehicletype text,
    timestamp timestamp,
    totalcount bigint,
    PRIMARY KEY (routeid, recorddate, vehicletype)
) WITH CLUSTERING ORDER BY (recorddate ASC, vehicletype ASC)
    AND bloom_filter_fp_chance = 0.01
    AND caching = {'keys': 'ALL', 'rows_per_partition': 'NONE'}
    AND comment = ''
    AND compaction = {'class': 'org.apache.cassandra.db.compaction.SizeTieredCompactionStrategy', 'max_threshold': '32', 'min_threshold': '4'}
    AND compression = {'chunk_length_in_
    
    
    调整dependency 到最新版本后，出现如下错误：
    The method function(Function3<KeyType,Optional<ValueType>,State<StateType>,MappedType>) in the type StateSpec is not applicable for the arguments (Function3<AggregateKey,Optional<Long>,State<Long>,Tuple2<AggregateKey,Long>>)
    
    https://stackoverflow.com/questions/40976502/problems-with-the-state-functions-in-spark-streaming
    
    
    change the import 

