# Step_01: installing kafka as stanalone
```
curl -O http://packages.confluent.io/archive/7.2/confluent-7.2.1.zip
unzip confluent-7.2.1.zip
```
#### installing java:
```
sudo apt install default-jre
```
```
cd /home/kubeadmin/kafka-old1/new-kafka/confluent-6.1.1
vim etc/kafka/zookeeper.properties
clientPort=2181

vim etc/kafka/server.properties
listeners=PLAINTEXT://192.168.6.127:9092
zookeeper.connect=localhost:2181

vim etc/schema-registry/schema-registry.properties
listeners=http://192.168.6.127:8081
kafkastore.bootstrap.servers=PLAINTEXT://192.168.6.127:9092
```
```
 Start Zookeeper:
cd /home/kubeadmin/kafka-old1/new-kafka/confluent-6.1.1
nohup bin/zookeeper-server-start etc/kafka/zookeeper.properties &

 Start the Kafka Services:
cd /home/kubeadmin/kafka-old1/new-kafka/confluent-6.1.1
nohup bin/kafka-server-start etc/kafka/server.properties & 

Start the schema registry:
cd /home/kubeadmin/kafka-old1/new-kafka/confluent-6.1.1
nohup bin/schema-registry-start etc/schema-registry/schema-registry.properties & 
```
#### Now i am going to create topics:
```
./kafka-topics --create --topic DEV3  --bootstrap-server 192.168.6.127:9092 --replication-factor 1 --partitions 4
./kafka-topics --create --topic nservice-DEV3  --bootstrap-server 192.168.6.127:9092 --replication-factor 1 --partitions 4
./kafka-topics --create --topic hiveprocessor-DEV3  --bootstrap-server 192.168.6.127:9092 --replication-factor 1 --partitions 4
./kafka-topics --create --topic ingestion-DEV3  --bootstrap-server 192.168.6.127:9092 --replication-factor 1 --partitions 4
./kafka-topics --create --topic nservice-DEV3  --bootstrap-server 192.168.6.127:9092 --replication-factor 1 --partitions 4
./kafka-topics --create --topic processparamvalues-DEV3  --bootstrap-server 192.168.6.127:9092 --replication-factor 1 --partitions 4

to list the topics run below command:

bin/kafka-topics --list  --bootstrap-server 192.168.6.127:9092

to delete the topic run below command:

./kafka-topics --delete --topic elastic-DEV3  --bootstrap-server 10.20.51.114:9092

./kafka-topics --zookeeper 10.20.51.114:2182 --delete --topic elastic-DEV3

```
#### Now i am going to create schemas:
```
curl http://192.168.6.127:8081/subjects/dlf-DEV3-value/versions -H 'Content-Type: application/json' --data-binary '{"schema":"{\"type\":\"record\",\"namespace\":\"com.verizon.oneparser.avroschemas\",\"name\":\"Logs\",\"version\":\"1\",\"fields\":[{\"name\":\"dmUser\",\"type\":[\"int\",\"null\"]},{\"name\":\"creationTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"lastLogTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"fileName\",\"type\":[\"string\",\"null\"]},{\"name\":\"size\",\"type\":[\"double\",\"null\"]},{\"name\":\"mdn\",\"type\":[\"string\",\"null\"]},{\"name\":\"imei\",\"type\":[\"string\",\"null\"]},{\"name\":\"id\",\"type\":\"long\"},{\"name\":\"firstname\",\"type\":[\"string\",\"null\"]},{\"name\":\"lastname\",\"type\":[\"string\",\"null\"]},{\"name\":\"isinbuilding\",\"type\":[\"int\",\"null\"]},{\"name\":\"hasgps\",\"type\":[\"int\",\"null\"]},{\"name\":\"emailid\",\"type\":[\"string\",\"null\"]},{\"name\":\"status\",\"type\":[\"string\",\"null\"]},{\"name\":\"modelName\",\"type\":[\"string\",\"null\"]},{\"name\":\"fileLocation\",\"type\":[\"string\",\"null\"]},{\"name\":\"esDataStatus\",\"type\":[\"string\",\"null\"]},{\"name\":\"esRecordCount\",\"type\":[\"double\",\"null\"]},{\"name\":\"importstarttime\",\"type\":[\"long\",\"null\"]},{\"name\":\"importstoptime\",\"type\":[\"long\",\"null\"]},{\"name\":\"filetype\",\"type\":[\"string\",\"null\"]},{\"name\":\"startLogTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"updatedTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"failureInfo\",\"type\":[\"string\",\"null\"]},{\"name\":\"logfilestatusforlv\",\"type\":[\"string\",\"null\"]},{\"name\":\"lvupdatedtime\",\"type\":[\"long\",\"null\"]},{\"name\":\"lverrordetails\",\"type\":[\"string\",\"null\"]},{\"name\":\"statusCsvFiles\",\"type\":[\"string\",\"null\"]},{\"name\":\"csvUpdatedTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"csvErrorDetails\",\"type\":[\"string\",\"null\"]},{\"name\":\"technology\",\"type\":[\"string\",\"null\"]},{\"name\":\"seqStartTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"seqEndTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"hiveStartTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"hiveEndTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"esStartTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"esEndTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"lvfilestarttime\",\"type\":[\"long\",\"null\"]},{\"name\":\"missingVersions\",\"type\":[\"string\",\"null\"]},{\"name\":\"lvPick\",\"type\":[\"string\",\"null\"]},{\"name\":\"lvStatus\",\"type\":[\"string\",\"null\"]},{\"name\":\"lvparseduserid\",\"type\":[\"string\",\"null\"]},{\"name\":\"lvlogfilecnt\",\"type\":[\"long\",\"null\"]},{\"name\":\"processingServer\",\"type\":[\"string\",\"null\"]},{\"name\":\"reportsHiveTblName\",\"type\":[\"string\",\"null\"]},{\"name\":\"compressionstatus\",\"type\":[\"boolean\",\"null\"]},{\"name\":\"eventsCount\",\"type\":[\"int\",\"null\"]},{\"name\":\"ftpstatus\",\"type\":[\"boolean\",\"null\"]},{\"name\":\"userPriorityTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"reprocessedBy\",\"type\":[\"int\",\"null\"]},{\"name\":\"pcapMulti\",\"type\":[\"string\",\"null\"]},{\"name\":\"pcapSingleRm\",\"type\":[\"string\",\"null\"]},{\"name\":\"pcapSingleUm\",\"type\":[\"string\",\"null\"]},{\"name\":\"cpHdfsTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"cpHdfsStartTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"cpHdfsEndTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"hiveDirEpoch\",\"type\":[\"string\",\"null\"]},{\"name\":\"ondemandBy\",\"type\":[\"int\",\"null\"]},{\"name\":\"carrierName\",\"type\":[\"string\",\"null\"]},{\"name\":\"odlvUserId\",\"type\":[\"int\",\"null\"]},{\"name\":\"odlvUpload\",\"type\":[\"boolean\",\"null\"]},{\"name\":\"odlvOnpStatus\",\"type\":[\"string\",\"null\"]},{\"name\":\"odlvLvStatus\",\"type\":[\"string\",\"null\"]},{\"name\":\"zipStartTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"zipEndTime\",\"type\":[\"long\",\"null\"]} , { \"name\": \"logcodes\", \"type\":[\"string\", \"null\"] }, { \"name\": \"triggerCount\", \"type\":[\"int\", \"null\"] } , { \"name\": \"seqRunCount\", \"type\":[\"int\", \"null\"] }, { \"name\": \"hiveRunCount\", \"type\":[\"int\", \"null\"] }, { \"name\": \"esRunCount\", \"type\":[\"int\", \"null\"] }]}"}' -i


curl http://192.168.6.127:8081/subjects/elastic-DEV3-value/versions -H 'Content-Type: application/json' --data-binary '{"schema":"{\"type\":\"record\",\"namespace\":\"com.verizon.oneparser.avroschemas\",\"name\":\"Logs\",\"version\":\"1\",\"fields\":[{\"name\":\"dmUser\",\"type\":[\"int\",\"null\"]},{\"name\":\"creationTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"lastLogTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"fileName\",\"type\":[\"string\",\"null\"]},{\"name\":\"size\",\"type\":[\"double\",\"null\"]},{\"name\":\"mdn\",\"type\":[\"string\",\"null\"]},{\"name\":\"imei\",\"type\":[\"string\",\"null\"]},{\"name\":\"id\",\"type\":\"long\"},{\"name\":\"firstname\",\"type\":[\"string\",\"null\"]},{\"name\":\"lastname\",\"type\":[\"string\",\"null\"]},{\"name\":\"isinbuilding\",\"type\":[\"int\",\"null\"]},{\"name\":\"hasgps\",\"type\":[\"int\",\"null\"]},{\"name\":\"emailid\",\"type\":[\"string\",\"null\"]},{\"name\":\"status\",\"type\":[\"string\",\"null\"]},{\"name\":\"modelName\",\"type\":[\"string\",\"null\"]},{\"name\":\"fileLocation\",\"type\":[\"string\",\"null\"]},{\"name\":\"esDataStatus\",\"type\":[\"string\",\"null\"]},{\"name\":\"esRecordCount\",\"type\":[\"double\",\"null\"]},{\"name\":\"importstarttime\",\"type\":[\"long\",\"null\"]},{\"name\":\"importstoptime\",\"type\":[\"long\",\"null\"]},{\"name\":\"filetype\",\"type\":[\"string\",\"null\"]},{\"name\":\"startLogTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"updatedTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"failureInfo\",\"type\":[\"string\",\"null\"]},{\"name\":\"logfilestatusforlv\",\"type\":[\"string\",\"null\"]},{\"name\":\"lvupdatedtime\",\"type\":[\"long\",\"null\"]},{\"name\":\"lverrordetails\",\"type\":[\"string\",\"null\"]},{\"name\":\"statusCsvFiles\",\"type\":[\"string\",\"null\"]},{\"name\":\"csvUpdatedTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"csvErrorDetails\",\"type\":[\"string\",\"null\"]},{\"name\":\"technology\",\"type\":[\"string\",\"null\"]},{\"name\":\"seqStartTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"seqEndTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"hiveStartTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"hiveEndTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"esStartTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"esEndTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"lvfilestarttime\",\"type\":[\"long\",\"null\"]},{\"name\":\"missingVersions\",\"type\":[\"string\",\"null\"]},{\"name\":\"lvPick\",\"type\":[\"string\",\"null\"]},{\"name\":\"lvStatus\",\"type\":[\"string\",\"null\"]},{\"name\":\"lvparseduserid\",\"type\":[\"string\",\"null\"]},{\"name\":\"lvlogfilecnt\",\"type\":[\"long\",\"null\"]},{\"name\":\"processingServer\",\"type\":[\"string\",\"null\"]},{\"name\":\"reportsHiveTblName\",\"type\":[\"string\",\"null\"]},{\"name\":\"compressionstatus\",\"type\":[\"boolean\",\"null\"]},{\"name\":\"eventsCount\",\"type\":[\"int\",\"null\"]},{\"name\":\"ftpstatus\",\"type\":[\"boolean\",\"null\"]},{\"name\":\"userPriorityTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"reprocessedBy\",\"type\":[\"int\",\"null\"]},{\"name\":\"pcapMulti\",\"type\":[\"string\",\"null\"]},{\"name\":\"pcapSingleRm\",\"type\":[\"string\",\"null\"]},{\"name\":\"pcapSingleUm\",\"type\":[\"string\",\"null\"]},{\"name\":\"cpHdfsTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"cpHdfsStartTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"cpHdfsEndTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"hiveDirEpoch\",\"type\":[\"string\",\"null\"]},{\"name\":\"ondemandBy\",\"type\":[\"int\",\"null\"]},{\"name\":\"carrierName\",\"type\":[\"string\",\"null\"]},{\"name\":\"odlvUserId\",\"type\":[\"int\",\"null\"]},{\"name\":\"odlvUpload\",\"type\":[\"boolean\",\"null\"]},{\"name\":\"odlvOnpStatus\",\"type\":[\"string\",\"null\"]},{\"name\":\"odlvLvStatus\",\"type\":[\"string\",\"null\"]},{\"name\":\"zipStartTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"zipEndTime\",\"type\":[\"long\",\"null\"]} , { \"name\": \"logcodes\", \"type\":[\"string\", \"null\"] }, { \"name\": \"triggerCount\", \"type\":[\"int\", \"null\"] } , { \"name\": \"seqRunCount\", \"type\":[\"int\", \"null\"] }, { \"name\": \"hiveRunCount\", \"type\":[\"int\", \"null\"] }, { \"name\": \"esRunCount\", \"type\":[\"int\", \"null\"] }]}"}' -i


curl http://192.168.6.127:8081/subjects/nservice-DEV3-value/versions -H 'Content-Type: application/json' --data-binary '{"schema":"{\"type\":\"record\",\"namespace\":\"com.verizon.oneparser.avroschemas\",\"name\":\"Logs\",\"version\":\"1\",\"fields\":[{\"name\":\"dmUser\",\"type\":[\"int\",\"null\"]},{\"name\":\"creationTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"lastLogTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"fileName\",\"type\":[\"string\",\"null\"]},{\"name\":\"size\",\"type\":[\"double\",\"null\"]},{\"name\":\"mdn\",\"type\":[\"string\",\"null\"]},{\"name\":\"imei\",\"type\":[\"string\",\"null\"]},{\"name\":\"id\",\"type\":\"long\"},{\"name\":\"firstname\",\"type\":[\"string\",\"null\"]},{\"name\":\"lastname\",\"type\":[\"string\",\"null\"]},{\"name\":\"isinbuilding\",\"type\":[\"int\",\"null\"]},{\"name\":\"hasgps\",\"type\":[\"int\",\"null\"]},{\"name\":\"emailid\",\"type\":[\"string\",\"null\"]},{\"name\":\"status\",\"type\":[\"string\",\"null\"]},{\"name\":\"modelName\",\"type\":[\"string\",\"null\"]},{\"name\":\"fileLocation\",\"type\":[\"string\",\"null\"]},{\"name\":\"esDataStatus\",\"type\":[\"string\",\"null\"]},{\"name\":\"esRecordCount\",\"type\":[\"double\",\"null\"]},{\"name\":\"importstarttime\",\"type\":[\"long\",\"null\"]},{\"name\":\"importstoptime\",\"type\":[\"long\",\"null\"]},{\"name\":\"filetype\",\"type\":[\"string\",\"null\"]},{\"name\":\"startLogTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"updatedTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"failureInfo\",\"type\":[\"string\",\"null\"]},{\"name\":\"logfilestatusforlv\",\"type\":[\"string\",\"null\"]},{\"name\":\"lvupdatedtime\",\"type\":[\"long\",\"null\"]},{\"name\":\"lverrordetails\",\"type\":[\"string\",\"null\"]},{\"name\":\"statusCsvFiles\",\"type\":[\"string\",\"null\"]},{\"name\":\"csvUpdatedTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"csvErrorDetails\",\"type\":[\"string\",\"null\"]},{\"name\":\"technology\",\"type\":[\"string\",\"null\"]},{\"name\":\"seqStartTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"seqEndTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"hiveStartTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"hiveEndTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"esStartTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"esEndTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"lvfilestarttime\",\"type\":[\"long\",\"null\"]},{\"name\":\"missingVersions\",\"type\":[\"string\",\"null\"]},{\"name\":\"lvPick\",\"type\":[\"string\",\"null\"]},{\"name\":\"lvStatus\",\"type\":[\"string\",\"null\"]},{\"name\":\"lvparseduserid\",\"type\":[\"string\",\"null\"]},{\"name\":\"lvlogfilecnt\",\"type\":[\"long\",\"null\"]},{\"name\":\"processingServer\",\"type\":[\"string\",\"null\"]},{\"name\":\"reportsHiveTblName\",\"type\":[\"string\",\"null\"]},{\"name\":\"compressionstatus\",\"type\":[\"boolean\",\"null\"]},{\"name\":\"eventsCount\",\"type\":[\"int\",\"null\"]},{\"name\":\"ftpstatus\",\"type\":[\"boolean\",\"null\"]},{\"name\":\"userPriorityTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"reprocessedBy\",\"type\":[\"int\",\"null\"]},{\"name\":\"pcapMulti\",\"type\":[\"string\",\"null\"]},{\"name\":\"pcapSingleRm\",\"type\":[\"string\",\"null\"]},{\"name\":\"pcapSingleUm\",\"type\":[\"string\",\"null\"]},{\"name\":\"cpHdfsTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"cpHdfsStartTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"cpHdfsEndTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"hiveDirEpoch\",\"type\":[\"string\",\"null\"]},{\"name\":\"ondemandBy\",\"type\":[\"int\",\"null\"]},{\"name\":\"carrierName\",\"type\":[\"string\",\"null\"]},{\"name\":\"odlvUserId\",\"type\":[\"int\",\"null\"]},{\"name\":\"odlvUpload\",\"type\":[\"boolean\",\"null\"]},{\"name\":\"odlvOnpStatus\",\"type\":[\"string\",\"null\"]},{\"name\":\"odlvLvStatus\",\"type\":[\"string\",\"null\"]},{\"name\":\"zipStartTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"zipEndTime\",\"type\":[\"long\",\"null\"]} , { \"name\": \"logcodes\", \"type\":[\"string\", \"null\"] }, { \"name\": \"triggerCount\", \"type\":[\"int\", \"null\"] } , { \"name\": \"seqRunCount\", \"type\":[\"int\", \"null\"] }, { \"name\": \"hiveRunCount\", \"type\":[\"int\", \"null\"] }, { \"name\": \"esRunCount\", \"type\":[\"int\", \"null\"] }]}"}' -i


curl http://192.168.6.127:8081/subjects/hiveprocessor-DEV3-value/versions -H 'Content-Type: application/json' --data-binary '{"schema":"{\"type\":\"record\",\"namespace\":\"com.verizon.oneparser.avroschemas\",\"name\":\"Logs\",\"version\":\"1\",\"fields\":[{\"name\":\"dmUser\",\"type\":[\"int\",\"null\"]},{\"name\":\"creationTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"lastLogTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"fileName\",\"type\":[\"string\",\"null\"]},{\"name\":\"size\",\"type\":[\"double\",\"null\"]},{\"name\":\"mdn\",\"type\":[\"string\",\"null\"]},{\"name\":\"imei\",\"type\":[\"string\",\"null\"]},{\"name\":\"id\",\"type\":\"long\"},{\"name\":\"firstname\",\"type\":[\"string\",\"null\"]},{\"name\":\"lastname\",\"type\":[\"string\",\"null\"]},{\"name\":\"isinbuilding\",\"type\":[\"int\",\"null\"]},{\"name\":\"hasgps\",\"type\":[\"int\",\"null\"]},{\"name\":\"emailid\",\"type\":[\"string\",\"null\"]},{\"name\":\"status\",\"type\":[\"string\",\"null\"]},{\"name\":\"modelName\",\"type\":[\"string\",\"null\"]},{\"name\":\"fileLocation\",\"type\":[\"string\",\"null\"]},{\"name\":\"esDataStatus\",\"type\":[\"string\",\"null\"]},{\"name\":\"esRecordCount\",\"type\":[\"double\",\"null\"]},{\"name\":\"importstarttime\",\"type\":[\"long\",\"null\"]},{\"name\":\"importstoptime\",\"type\":[\"long\",\"null\"]},{\"name\":\"filetype\",\"type\":[\"string\",\"null\"]},{\"name\":\"startLogTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"updatedTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"failureInfo\",\"type\":[\"string\",\"null\"]},{\"name\":\"logfilestatusforlv\",\"type\":[\"string\",\"null\"]},{\"name\":\"lvupdatedtime\",\"type\":[\"long\",\"null\"]},{\"name\":\"lverrordetails\",\"type\":[\"string\",\"null\"]},{\"name\":\"statusCsvFiles\",\"type\":[\"string\",\"null\"]},{\"name\":\"csvUpdatedTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"csvErrorDetails\",\"type\":[\"string\",\"null\"]},{\"name\":\"technology\",\"type\":[\"string\",\"null\"]},{\"name\":\"seqStartTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"seqEndTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"hiveStartTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"hiveEndTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"esStartTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"esEndTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"lvfilestarttime\",\"type\":[\"long\",\"null\"]},{\"name\":\"missingVersions\",\"type\":[\"string\",\"null\"]},{\"name\":\"lvPick\",\"type\":[\"string\",\"null\"]},{\"name\":\"lvStatus\",\"type\":[\"string\",\"null\"]},{\"name\":\"lvparseduserid\",\"type\":[\"string\",\"null\"]},{\"name\":\"lvlogfilecnt\",\"type\":[\"long\",\"null\"]},{\"name\":\"processingServer\",\"type\":[\"string\",\"null\"]},{\"name\":\"reportsHiveTblName\",\"type\":[\"string\",\"null\"]},{\"name\":\"compressionstatus\",\"type\":[\"boolean\",\"null\"]},{\"name\":\"eventsCount\",\"type\":[\"int\",\"null\"]},{\"name\":\"ftpstatus\",\"type\":[\"boolean\",\"null\"]},{\"name\":\"userPriorityTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"reprocessedBy\",\"type\":[\"int\",\"null\"]},{\"name\":\"pcapMulti\",\"type\":[\"string\",\"null\"]},{\"name\":\"pcapSingleRm\",\"type\":[\"string\",\"null\"]},{\"name\":\"pcapSingleUm\",\"type\":[\"string\",\"null\"]},{\"name\":\"cpHdfsTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"cpHdfsStartTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"cpHdfsEndTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"hiveDirEpoch\",\"type\":[\"string\",\"null\"]},{\"name\":\"ondemandBy\",\"type\":[\"int\",\"null\"]},{\"name\":\"carrierName\",\"type\":[\"string\",\"null\"]},{\"name\":\"odlvUserId\",\"type\":[\"int\",\"null\"]},{\"name\":\"odlvUpload\",\"type\":[\"boolean\",\"null\"]},{\"name\":\"odlvOnpStatus\",\"type\":[\"string\",\"null\"]},{\"name\":\"odlvLvStatus\",\"type\":[\"string\",\"null\"]},{\"name\":\"zipStartTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"zipEndTime\",\"type\":[\"long\",\"null\"]} , { \"name\": \"logcodes\", \"type\":[\"string\", \"null\"] }, { \"name\": \"triggerCount\", \"type\":[\"int\", \"null\"] } , { \"name\": \"seqRunCount\", \"type\":[\"int\", \"null\"] }, { \"name\": \"hiveRunCount\", \"type\":[\"int\", \"null\"] }, { \"name\": \"esRunCount\", \"type\":[\"int\", \"null\"] }]}"}' -i


curl http://192.168.6.127:8081/subjects/ingestion-DEV3-value/versions -H 'Content-Type: application/json' --data-binary '{"schema":"{\"type\":\"record\",\"namespace\":\"com.verizon.oneparser.avroschemas\",\"name\":\"Logs\",\"version\":\"1\",\"fields\":[{\"name\":\"dmUser\",\"type\":[\"int\",\"null\"]},{\"name\":\"creationTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"lastLogTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"fileName\",\"type\":[\"string\",\"null\"]},{\"name\":\"size\",\"type\":[\"double\",\"null\"]},{\"name\":\"mdn\",\"type\":[\"string\",\"null\"]},{\"name\":\"imei\",\"type\":[\"string\",\"null\"]},{\"name\":\"id\",\"type\":\"long\"},{\"name\":\"firstname\",\"type\":[\"string\",\"null\"]},{\"name\":\"lastname\",\"type\":[\"string\",\"null\"]},{\"name\":\"isinbuilding\",\"type\":[\"int\",\"null\"]},{\"name\":\"hasgps\",\"type\":[\"int\",\"null\"]},{\"name\":\"emailid\",\"type\":[\"string\",\"null\"]},{\"name\":\"status\",\"type\":[\"string\",\"null\"]},{\"name\":\"modelName\",\"type\":[\"string\",\"null\"]},{\"name\":\"fileLocation\",\"type\":[\"string\",\"null\"]},{\"name\":\"esDataStatus\",\"type\":[\"string\",\"null\"]},{\"name\":\"esRecordCount\",\"type\":[\"double\",\"null\"]},{\"name\":\"importstarttime\",\"type\":[\"long\",\"null\"]},{\"name\":\"importstoptime\",\"type\":[\"long\",\"null\"]},{\"name\":\"filetype\",\"type\":[\"string\",\"null\"]},{\"name\":\"startLogTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"updatedTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"failureInfo\",\"type\":[\"string\",\"null\"]},{\"name\":\"logfilestatusforlv\",\"type\":[\"string\",\"null\"]},{\"name\":\"lvupdatedtime\",\"type\":[\"long\",\"null\"]},{\"name\":\"lverrordetails\",\"type\":[\"string\",\"null\"]},{\"name\":\"statusCsvFiles\",\"type\":[\"string\",\"null\"]},{\"name\":\"csvUpdatedTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"csvErrorDetails\",\"type\":[\"string\",\"null\"]},{\"name\":\"technology\",\"type\":[\"string\",\"null\"]},{\"name\":\"seqStartTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"seqEndTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"hiveStartTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"hiveEndTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"esStartTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"esEndTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"lvfilestarttime\",\"type\":[\"long\",\"null\"]},{\"name\":\"missingVersions\",\"type\":[\"string\",\"null\"]},{\"name\":\"lvPick\",\"type\":[\"string\",\"null\"]},{\"name\":\"lvStatus\",\"type\":[\"string\",\"null\"]},{\"name\":\"lvparseduserid\",\"type\":[\"string\",\"null\"]},{\"name\":\"lvlogfilecnt\",\"type\":[\"long\",\"null\"]},{\"name\":\"processingServer\",\"type\":[\"string\",\"null\"]},{\"name\":\"reportsHiveTblName\",\"type\":[\"string\",\"null\"]},{\"name\":\"compressionstatus\",\"type\":[\"boolean\",\"null\"]},{\"name\":\"eventsCount\",\"type\":[\"int\",\"null\"]},{\"name\":\"ftpstatus\",\"type\":[\"boolean\",\"null\"]},{\"name\":\"userPriorityTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"reprocessedBy\",\"type\":[\"int\",\"null\"]},{\"name\":\"pcapMulti\",\"type\":[\"string\",\"null\"]},{\"name\":\"pcapSingleRm\",\"type\":[\"string\",\"null\"]},{\"name\":\"pcapSingleUm\",\"type\":[\"string\",\"null\"]},{\"name\":\"cpHdfsTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"cpHdfsStartTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"cpHdfsEndTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"hiveDirEpoch\",\"type\":[\"string\",\"null\"]},{\"name\":\"ondemandBy\",\"type\":[\"int\",\"null\"]},{\"name\":\"carrierName\",\"type\":[\"string\",\"null\"]},{\"name\":\"odlvUserId\",\"type\":[\"int\",\"null\"]},{\"name\":\"odlvUpload\",\"type\":[\"boolean\",\"null\"]},{\"name\":\"odlvOnpStatus\",\"type\":[\"string\",\"null\"]},{\"name\":\"odlvLvStatus\",\"type\":[\"string\",\"null\"]},{\"name\":\"zipStartTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"zipEndTime\",\"type\":[\"long\",\"null\"]} , { \"name\": \"logcodes\", \"type\":[\"string\", \"null\"] }, { \"name\": \"triggerCount\", \"type\":[\"int\", \"null\"] } , { \"name\": \"seqRunCount\", \"type\":[\"int\", \"null\"] }, { \"name\": \"hiveRunCount\", \"type\":[\"int\", \"null\"] }, { \"name\": \"esRunCount\", \"type\":[\"int\", \"null\"] }]}"}' -i

to list the schemas run below command:

curl -X GET  http://192.168.6.127:8081/schemas -i

to delete the schemas run below command:

-- curl -X DELETE http://192.168.6.127:8081/subjects/dlf-DEV3-value 
```
# Step_02 installing postgres 12 version
```
step 1: update ubuntu system
sudo apt update

step 2: install requered package
sudo apt -y install vim bash-completion wget

Step 3: Add PostgreSQL 12 repository
wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -
echo "deb http://apt.postgresql.org/pub/repos/apt/ `lsb_release -cs`-pgdg main" |sudo tee  /etc/apt/sources.list.d/pgdg.list

Step 4: Install PostgreSQL 12 on Ubuntu
sudo apt update
sudo apt -y install postgresql-12 postgresql-client-12

Step 5: Check PostgreSQL service status
systemctl status postgresql.service 

Step 6: Connect PostgreSQL 
sudo su -l postgres
psql

Step 7: Create a database and user roles
It is recommended to reset the password to strong password
psql -c "alter user postgres with password 'Post@12345'"
CREATE DATABASE dmat_test;
5. List the PostgreSQL database:
$\l
```
```
8. Allow remote connection to PostgreSQL Database
sudo vim /etc/postgresql/12/main/postgresql.conf
listen_addresses = '*'          # what IP address(es) to listen on;

sudo systemctl restart postgresql 
netstat  -tunelp | grep 5432
```
```
9. Configure the database cluster to accept connections.
sudo vim /etc/postgresql/12/main/pg_hba.conf

# Database administrative login by Unix domain socket
local   all             postgres                  peer
hostnossl all all 0.0.0.0/0 trust

sudo systemctl restart postgresql
```

#### 10. to connect from outside the VM
- sudo apt install postgresql-client
- psql -U postgres -h 192.168.6.127 -p 5432 dmat_test

# Step_03 installing Elasticsearch:
Step-2 Elasticsearch only
```
Step 1 — Installing and Configuring Elasticsearch
curl -fsSL https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add -
echo "deb https://artifacts.elastic.co/packages/7.x/apt stable main" | sudo tee -a /etc/apt/sources.list.d/elastic-7.x.list
sudo apt update

sudo apt install default-jre

sudo apt install elasticsearch
```
- sudo vim /etc/elasticsearch/elasticsearch.yml
```
#cluster.name: my-application
cluster.name: ortelligence

#path.data: /path/to/data
path.data: /home/ubuntu/elasticsearch-6.7.1

#network.host: 192.168.0.1
network.host: 0.0.0.0

#http.port: 9200
```
- sudo systemctl start elasticsearch
- sudo systemctl enable elasticsearch

- curl -X GET 'http://localhost:9200'

### Step-2 ELK
#####Prerequisites
```
A Linux system running Ubuntu 20.04 or 18.04
Access to a terminal window/command line (Search > Terminal)
A user account with sudo or root privileges
Java version 8 or 11 (required for Logstash)
```
#####Install Java
```
sudo apt update -y
java -version
sudo apt install default-jre -y
java -version
sudo apt install default-jdk -y
java -version
sudo update-alternatives --config java
```
####Install Nginx
```
sudo apt-get install nginx -y
systemctl enable nginx && systemctl start nginx
systemctl start nginx
```

#### Add Elastic Repository
```
cd /tmp
wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add -
sudo apt-get install apt-transport-https -y
echo "deb https://artifacts.elastic.co/packages/7.x/apt stable main" | sudo tee -a /etc/apt/sources.list.d/elastic-7.x.list
sudo apt-get update -y
sudo apt-get install elasticsearch -y
sudo vim /etc/elasticsearch/elasticsearch.yml
```
```
####You should see a configuration file with several different entries and descriptions. Scroll down to find the following entries:

#network.host: 192.168.0.1
#http.port: 9200
### Uncomment the lines by deleting the hash (#) sign at the beginning of both lines and replace 192.168.0.1 with localhost.

network.host: localhost
http.port: 9200

##########By default, JVM heap size is set at 1GB. We recommend setting it to no more than half the size of your total memory. Open the following file for editing:

sudo vim /etc/elasticsearch/jvm.options
6. Find the lines starting with -Xms and -Xmx. In the example below, the maximum (-Xmx) and minimum (-Xms) size is set to 512MB.
#-Xms512m
#-Xmx512m
-Xms2g
-Xmx2g


sudo systemctl start elasticsearch.service

##### will take some time and if successfull no output is shown
sudo systemctl enable elasticsearch.service
sudo systemctl status elasticsearch.service

curl localhost:9200
```

########################################install kibana
sudo apt-get install kibana -y

sudo vim /etc/kibana/kibana.yml

2 Delete the # sign at the beginning of the following lines to activate them:

#server.port: 5601
#server.host: “your-hostname”
#elasticsearch.hosts: [“http://localhost:9200”]
The above-mentioned lines should look as follows:

#server.port: 5601
#server.host: "0.0.0.0"
#elasticsearch.hosts: [“http://localhost:9200”]

sudo systemctl start kibana
sudo systemctl enable kibana
sudo systemctl status kibana
journalctl -u kibana.service -r

#First, use the openssl command to create an administrative Kibana user which you’ll use to access the Kibana web interface. 
As an example we will name this account kibanaadmin, but to ensure greater security we recommend that you choose a non-standard name
for your user that would be difficult to guess.

echo "kibanaadmin:`openssl passwd -apr1`" | sudo tee -a /etc/nginx/htpasswd.users

###user: kibanaadmin
##passwd: tech@4321

kibanaadmin:$apr1$YWfPJRHz$F39oKtThPXFCAGNi1w5uK0
kibanaadmin:$apr1$Bltz87b.$t7LWYRteYK5CUgUN1xVcS/

sudo vim /etc/nginx/sites-available/elk.conf
#######################################################################################################

server {
    listen 80;

    server_name 3.143.45.219;

    auth_basic "Restricted Access";
    auth_basic_user_file /etc/nginx/htpasswd.users;

    location / {
        proxy_pass http://localhost:5601;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
}



###################################################################################################


sudo ln -s /etc/nginx/sites-available/elk.conf /etc/nginx/sites-enabled/elk.conf


sudo nginx -t
sudo systemctl restart nginx



http://3.143.45.219/status


###user: kibanaadmin
##passwd: tech@4321

http://3.143.45.219/


############## install logstash

sudo apt install logstash -y


cd /etc/logstash/conf.d


###Create a configuration file called 02-beats-input.conf where you will set up your Filebeat input:

sudo vim /etc/logstash/conf.d/02-beats-input.conf
 
#####Insert the following input configuration. This specifies a beats input that will listen on TCP port 5044.


input {
  beats {
    port => 5044
  }
}




#####Next, create a configuration file called 10-syslog-filter.conf, where we will add a filter for system logs, also known as syslogs:

sudo vim /etc/logstash/conf.d/10-syslog-filter.conf
##Insert the following syslog filter configuration. This example system logs configuration was taken from official Elastic documentation. 
This filter is used to parse incoming system logs to make them structured and usable by the predefined Kibana dashboards:




filter {
  if [fileset][module] == "system" {
    if [fileset][name] == "auth" {
      grok {
        match => { "message" => ["%{SYSLOGTIMESTAMP:[system][auth][timestamp]} %{SYSLOGHOST:[system][auth][hostname]} sshd(?:\[%{POSINT:[system][auth][pid]}\])?: %{DATA:[system][auth][ssh][event]} %{DATA:[system][auth][ssh][method]} for (invalid user )?%{DATA:[system][auth][user]} from %{IPORHOST:[system][auth][ssh][ip]} port %{NUMBER:[system][auth][ssh][port]} ssh2(: %{GREEDYDATA:[system][auth][ssh][signature]})?",
                  "%{SYSLOGTIMESTAMP:[system][auth][timestamp]} %{SYSLOGHOST:[system][auth][hostname]} sshd(?:\[%{POSINT:[system][auth][pid]}\])?: %{DATA:[system][auth][ssh][event]} user %{DATA:[system][auth][user]} from %{IPORHOST:[system][auth][ssh][ip]}",
                  "%{SYSLOGTIMESTAMP:[system][auth][timestamp]} %{SYSLOGHOST:[system][auth][hostname]} sshd(?:\[%{POSINT:[system][auth][pid]}\])?: Did not receive identification string from %{IPORHOST:[system][auth][ssh][dropped_ip]}",
                  "%{SYSLOGTIMESTAMP:[system][auth][timestamp]} %{SYSLOGHOST:[system][auth][hostname]} sudo(?:\[%{POSINT:[system][auth][pid]}\])?: \s*%{DATA:[system][auth][user]} :( %{DATA:[system][auth][sudo][error]} ;)? TTY=%{DATA:[system][auth][sudo][tty]} ; PWD=%{DATA:[system][auth][sudo][pwd]} ; USER=%{DATA:[system][auth][sudo][user]} ; COMMAND=%{GREEDYDATA:[system][auth][sudo][command]}",
                  "%{SYSLOGTIMESTAMP:[system][auth][timestamp]} %{SYSLOGHOST:[system][auth][hostname]} groupadd(?:\[%{POSINT:[system][auth][pid]}\])?: new group: name=%{DATA:system.auth.groupadd.name}, GID=%{NUMBER:system.auth.groupadd.gid}",
                  "%{SYSLOGTIMESTAMP:[system][auth][timestamp]} %{SYSLOGHOST:[system][auth][hostname]} useradd(?:\[%{POSINT:[system][auth][pid]}\])?: new user: name=%{DATA:[system][auth][user][add][name]}, UID=%{NUMBER:[system][auth][user][add][uid]}, GID=%{NUMBER:[system][auth][user][add][gid]}, home=%{DATA:[system][auth][user][add][home]}, shell=%{DATA:[system][auth][user][add][shell]}$",
                  "%{SYSLOGTIMESTAMP:[system][auth][timestamp]} %{SYSLOGHOST:[system][auth][hostname]} %{DATA:[system][auth][program]}(?:\[%{POSINT:[system][auth][pid]}\])?: %{GREEDYMULTILINE:[system][auth][message]}"] }
        pattern_definitions => {
          "GREEDYMULTILINE"=> "(.|\n)*"
        }
        remove_field => "message"
      }
      date {
        match => [ "[system][auth][timestamp]", "MMM  d HH:mm:ss", "MMM dd HH:mm:ss" ]
      }
      geoip {
        source => "[system][auth][ssh][ip]"
        target => "[system][auth][ssh][geoip]"
      }
    }
    else if [fileset][name] == "syslog" {
      grok {
        match => { "message" => ["%{SYSLOGTIMESTAMP:[system][syslog][timestamp]} %{SYSLOGHOST:[system][syslog][hostname]} %{DATA:[system][syslog][program]}(?:\[%{POSINT:[system][syslog][pid]}\])?: %{GREEDYMULTILINE:[system][syslog][message]}"] }
        pattern_definitions => { "GREEDYMULTILINE" => "(.|\n)*" }
        remove_field => "message"
      }
      date {
        match => [ "[system][syslog][timestamp]", "MMM  d HH:mm:ss", "MMM dd HH:mm:ss" ]
      }
    }
  }
}


###Lastly, create a configuration file called 30-elasticsearch-output.conf:

sudo vim /etc/logstash/conf.d/30-elasticsearch-output.conf
 
Insert the following output configuration. Essentially, this output configures Logstash to store the Beats data in Elasticsearch, which is running at localhost:9200, 
in an index named after the Beat used. The Beat used in this tutorial is Filebeat:


output {
  elasticsearch {
    hosts => ["localhost:9200"]
    manage_template => false
    index => "%{[@metadata][beat]}-%{[@metadata][version]}-%{+YYYY.MM.dd}"
  }
}




###Test your Logstash configuration with this command:

sudo -u logstash /usr/share/logstash/bin/logstash --path.settings /etc/logstash -t


If there are no syntax errors, your output will display Configuration OK after a few seconds. If you don’t see this in your output, check for any errors that appear in your output and update your configuration to correct them.

If your configuration test is successful, start and enable Logstash to put the configuration changes into effect:

sudo systemctl start logstash
sudo systemctl enable logstash




# Step_04 installing hadoop as stanalone:
```
sudo apt update
sudo apt install openjdk-8-jdk -y

java -version
sudo apt install openssh-server openssh-client -y
sudo adduser hdoop
su - hdoop
ssh-keygen -t rsa -P '' -f ~/.ssh/id_rsa
cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
chmod 0600 ~/.ssh/authorized_keys
ssh localhost
```
Downloading Hadoop (Please note link is updated to new version of hadoop here on 6th May 2022)
```
wget https://downloads.apache.org/hadoop/common/hadoop-3.2.3/hadoop-3.2.3.tar.gz
tar xzf hadoop-3.2.3.tar.gz
```
Editng 6 important files

1st File
```
sudo nano .bashrc -  here you might face issue saying hdoop is not sudo user 
if this issue comes then
su - aman
sudo adduser hdoop sudo

sudo nano .bashrc
#Add below lines in this file

#Hadoop Related Options
export HADOOP_HOME=/home/hdoop/hadoop-3.2.3
export HADOOP_INSTALL=$HADOOP_HOME
export HADOOP_MAPRED_HOME=$HADOOP_HOME
export HADOOP_COMMON_HOME=$HADOOP_HOME
export HADOOP_HDFS_HOME=$HADOOP_HOME
export YARN_HOME=$HADOOP_HOME
export HADOOP_COMMON_LIB_NATIVE_DIR=$HADOOP_HOME/lib/native
export PATH=$PATH:$HADOOP_HOME/sbin:$HADOOP_HOME/bin
export HADOOP_OPTS"-Djava.library.path=$HADOOP_HOME/lib/nativ"

source ~/.bashrc
```
2nd File
```
sudo nano $HADOOP_HOME/etc/hadoop/hadoop-env.sh

#Add below line in this file in the end

export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
```
3rd File
```
sudo nano $HADOOP_HOME/etc/hadoop/core-site.xml

#Add below lines in this file(between "<configuration>" and "<"/configuration>")
   <property>
        <name>hadoop.tmp.dir</name>
        <value>/home/hdoop/tmpdata</value>
        <description>A base for other temporary directories.</description>
    </property>
    <property>
        <name>fs.default.name</name>
        <value>hdfs://localhost:9000</value>
        <description>The name of the default file system></description>
    </property>
```
4th File
```
sudo nano $HADOOP_HOME/etc/hadoop/hdfs-site.xml

#Add below lines in this file(between "<configuration>" and "<"/configuration>")

<property>
  <name>dfs.data.dir</name>
  <value>/home/hdoop/dfsdata/namenode</value>
</property>
<property>
  <name>dfs.data.dir</name>
  <value>/home/hdoop/dfsdata/datanode</value>
</property>
<property>
  <name>dfs.replication</name>
  <value>1</value>
</property>

```

5th File
```
sudo nano $HADOOP_HOME/etc/hadoop/mapred-site.xml

#Add below lines in this file(between "<configuration>" and "<"/configuration>")

<property>
  <name>mapreduce.framework.name</name>
  <value>yarn</value>
</property>
```
6th File
```
sudo nano $HADOOP_HOME/etc/hadoop/yarn-site.xml

#Add below lines in this file(between "<configuration>" and "<"/configuration>")

<property>
  <name>yarn.nodemanager.aux-services</name>
  <value>mapreduce_shuffle</value>
</property>
<property>
  <name>yarn.nodemanager.aux-services.mapreduce.shuffle.class</name>
  <value>org.apache.hadoop.mapred.ShuffleHandler</value>
</property>
<property>
  <name>yarn.resourcemanager.hostname</name>
  <value>127.0.0.1</value>
</property>
<property>
  <name>yarn.acl.enable</name>
  <value>0</value>
</property>
<property>
  <name>yarn.nodemanager.env-whitelist</name>
  <value>JAVA_HOME,HADOOP_COMMON_HOME,HADOOP_HDFS_HOME,HADOOP_CONF_DIR,CLASSPATH_PERPEND_DISTCACHE,HADOOP_YARN_HOME,HADOOP_MAPRED_HOME</value>
</property>
```

Launching Hadoop
```
hdfs namenode -format

su - hdoop
cd /home/hdoop/hadoop-3.2.3/sbin
 ./start-dfs.sh
 ./stop-yarn.sh
 ./start-dfs.sh
 ./start-yarn.sh
 jps
 hdfs dfs -ls /

  hdfs dfs -put /home/amantya/tahlimdemofile.txt /
  hdfs dfs -ls /
```
 
# Step_05: Setting up FTP and NFS server:
#### Step_01 FTP mounting with EFS
#### installing NFS client
Step 1: Install NFS Server in Ubuntu
```
	sudo apt update
	sudo apt install nfs-common
```    
Step 2: Create an EFS Mount Point on FTP server
```
	sudo mkdir -p /ftpdatademo
	sudo chown -R nobody:nogroup  /ftpdatademo
	sudo chmod 777 /ftpdatademo
```
Step 3: Mount AWS EFS server
```
### Get the details of EFS endpoints from the console
sudo mount -t nfs4 -o nfsvers=4.1,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,noresvport 192.168.133.80:/ /ftpdatademo

Now the EFS is mounted on location /ftpdatademo

user name: dmatuser
password: dmatuser
port: 2400
location: /ftpdatademo
```
----------------------------------------------------
#### Step_02 FTP mounting with NFS on other servers
Step 1: Install NFS Server in Ubuntu
```
	sudo apt update
	sudo apt install nfs-common
```
Step 2: Create an NFS server Mount Point on FTP server
```
Set up a mount point for the remote NFS share:
sudo mkdir /var/backups

Open the /etc/fstab file with your text editor:
sudo nano /etc/fstab

# <file system>     <dir>       <type>   <options>   <dump>	<pass>
10.10.0.10:/backups /var/backups  nfs      defaults    0       0

mount /var/backups
mount 10.10.0.10:/backups
```
Step 3: Unmounting NFS File Systems
```
umount 10.10.0.10:/backups 
umount /var/backups
```
---------------------------------------------------
#### Step_03 FTP mounting NSF and Setting up FTP server:
192.168.6.128 -- masternode    (for ftp client)

192.168.6.119 -- workernode    (for ftp server host)
  
##### Step_01: Sharing over NFS server
##### on host server:          ### workernode-1 - 192.168.6.127
```
sudo apt update
sudo apt install nfs-kernel-server
```
```
mkdir -p /common/volume/
sudo mkdir -p /common/volume/
sudo chmod -R 777 /common/volume/
sudo vim /etc/exports
/common/volume/  *(no_root_squash,rw,sync)
sudo systemctl start nfs-server
sudo systemctl enable nfs-server
sudo exportfs -v
```
##### Step_02: Setting Up an NFS Mount Point for Clients
##### on client server :          ### masternode-0 - 192.168.6.26
```
sudo apt update
sudo apt install nfs-common

sudo mkdir -p /mnt/ftpdatademo
sudo mount 192.168.6.119:/common/volume/ /mnt/ftpdatademo
```
