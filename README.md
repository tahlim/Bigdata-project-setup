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
192.168.6.119 -- workernode
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
##### on host server:
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
```
sudo apt update
sudo apt install nfs-common

sudo mkdir -p /mnt/ftpdatademo
sudo mount 192.168.6.119:/common/volume/ /mnt/ftpdatademo
```
