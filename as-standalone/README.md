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
### Step-1 Elasticsearch only
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
transport.host: localhost             #####  note: if you want to access is from outside then you can add this line

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

####################install kibana
```
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
```
sudo vim /etc/nginx/sites-available/elk.conf
```
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
```
```
sudo ln -s /etc/nginx/sites-available/elk.conf /etc/nginx/sites-enabled/elk.conf

sudo nginx -t
sudo systemctl restart nginx

http://3.143.45.219/status


###user: kibanaadmin
##passwd: tech@4321

http://3.143.45.219/

```
############## install logstash
```
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
```

# Step_04 installing hadoop as stanalone:
##### First way ==>
# ==> HDFS
 #### Use the following command to update your system before initiating a new installation:
    sudo apt update
 #### Type the following command in your terminal to install OpenJDK 8:
    sudo apt install openjdk-8-jdk -y
 #### Once the installation process is complete, verify the Java version    
    java -version; javac -version
 #### Install the OpenSSH server and client using the following command:
    sudo apt install openssh-server openssh-client -y
 #### -Utilize the adduser command to create a new Hadoop user:
    sudo adduser hdoop
 #### Switch to the newly created user and enter the corresponding password
    su - hdoop
 #### Enable Passwordless SSH for Hadoop User
    ssh-keygen -t rsa -P '' -f ~/.ssh/id_rsa
 #### Use the cat command to store the public key as authorized_keys in the ssh directory:
    cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
 #### Set the permissions for your user with the chmod command:
    chmod 0600 ~/.ssh/authorized_keys
 #### Verify everything is set up correctly by using the hdoop user to SSH to localhost:
    ssh localhost
 #### Download and Install Hadoop on Ubuntu on this link
    https://hadoop.apache.org/releases.html
 #### Use the provided mirror link and download the Hadoop package with the wget command:
    wget https://dlcdn.apache.org/hadoop/common/hadoop-3.3.4/hadoop-3.3.4.tar.gz 
 #### Once the download is complete, extract the files to initiate the Hadoop installation:
    tar xzf hadoop-3.3.4.tar.gz
 #### Configure Hadoop
  nano .bashrc
#### copy this configuration in .bashrc
    # Hadoop Related Options
    export HADOOP_HOME=/home/hdoop/hadoop-3.3.4
    export HADOOP_INSTALL=$HADOOP_HOME
    export HADOOP_MAPRED_HOME=$HADOOP_HOME
    export HADOOP_COMMON_HOME=$HADOOP_HOME
    export HADOOP_HDFS_HOME=$HADOOP_HOME
    export YARN_HOME=$HADOOP_HOME
    export HADOOP_COMMON_LIB_NATIVE_DIR=$HADOOP_HOME/lib/native
    export PATH=$PATH:$HADOOP_HOME/sbin:$HADOOP_HOME/bin
    export HADOOP_OPTS"-Djava.library.path=$HADOOP_HOME/lib/nativ"
![Capture](https://user-images.githubusercontent.com/103019032/191722996-ca371d24-1b32-437d-b098-f8df94b684fd.PNG)

source ~/.bashrc

## Edit hadoop-env.sh File
#### The hadoop-env.sh file serves as a master file to configure YARN, HDFS, MapReduce, and Hadoop-related project settings.
    nano hadoop-3.3.4/etc/hadoop/hadoop-env.sh
![capture4](https://user-images.githubusercontent.com/103019032/191726856-028dee97-1b83-42e1-ad8f-4d5772a40881.PNG)
#### If you have installed the same version as presented in the first part of this tutorial, add the following line:
    export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
![Capture2](https://user-images.githubusercontent.com/103019032/191724808-d61ef9b0-739a-4da2-b006-238048e31916.PNG)
#### Use the provided path to find the OpenJDK directory with the following command:
    readlink -f /usr/bin/javac
#### To set up Hadoop in a pseudo-distributed mode, you need to specify the URL for your NameNode, and the temporary directory Hadoop uses for the map and reduce process.
#### Open the core-site.xml file in a text editor:
    nano hadoop-3.3.4/etc/hadoop/core-site.xml
![capture5](https://user-images.githubusercontent.com/103019032/191727595-4117ab43-bddc-4d9d-9b95-6b8bf5019d23.PNG)
![image](https://user-images.githubusercontent.com/103019032/191727809-c8baf7f8-e3a4-4c8f-aded-b572a3e7fc69.png)
#### Add the following configuration to override the default values for the temporary directory and add your HDFS URL to replace the default local file system setting:
     <configuration>
     <property>
     <name>hadoop.tmp.dir</name>
     <value>/home/hdoop/tmpdata</value>
     </property>
     <property>
     <name>fs.default.name</name>
     <value>hdfs://localhost:9000</value>
     </property>
     </configuration>
#### Edit hdfs-site.xml File
     nano hadoop-3.3.4/etc/hadoop/hdfs-site.xml
![capture6](https://user-images.githubusercontent.com/103019032/191728600-c0933484-f394-4db9-af81-26a73cc3019d.PNG)
#### copy xml file
      <configuration>
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
      </configuration>
 #### Edit mapred-site.xml File
      nano hadoop-3.3.4/etc/hadoop/mapred-site.xml
 ![capture7](https://user-images.githubusercontent.com/103019032/191731283-ce41941f-7799-4067-af9c-41846cff7816.PNG)
 #### copy xml file
       <configuration>
       <property>
       <name>mapreduce.framework.name</name>
       <value>yarn</value>
       </property>
       </configuration>
#### Edit yarn-site.xml File
#### The yarn-site.xml file is used to define settings relevant to YARN. It contains configurations for the Node Manager, Resource Manager, Containers, and Application Master.
      nano hadoop-3.3.4/etc/hadoop/yarn-site.xml
![capture8](https://user-images.githubusercontent.com/103019032/191732089-e84fa7af-01f9-4af9-b2eb-eb9aa0eb613c.PNG)
#### copy xml file
      <configuration>
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
      <value>localhost</value>
      </property>
      <property>
      <name>yarn.acl.enable</name>
      <value>0</value>
      </property>
      <property>
      <name>yarn.nodemanager.env-whitelist</name>   
      <value>JAVA_HOME,HADOOP_COMMON_HOME,HADOOP_HDFS_HOME,HADOOP_CONF_DIR,CLASSPATH_PERPEND_DISTCACHE,HADOOP_YARN_HOME,HADOOP_MAPRED_HOME</value>
      </property>
      </configuration>
 #### It is important to format the NameNode before starting Hadoop services for the first time:
      hdfs namenode -format
 ![image](https://user-images.githubusercontent.com/103019032/191733361-1c442753-ca19-4d3b-8550-e5c280ec5b2d.png)
 
 #### Start Hadoop Cluster
#### Navigate to the hadoop-3.2.1/sbin directory and execute the following commands to start the NameNode and DataNode:
      ./start-dfs.sh
![image](https://user-images.githubusercontent.com/103019032/191734003-316171e8-0cfc-4886-b5f4-4e0619e357e6.png)
#### Once the namenode, datanodes, and secondary namenode are up and running, start the YARN resource and nodemanagers by typing:
      ./start-yarn.sh
![image](https://user-images.githubusercontent.com/103019032/191734216-996db6eb-ccef-4327-8050-e87f69d4aeb9.png)
#### Type this simple command to check if all the daemons are active and running as Java processes:
     jps
![image](https://user-images.githubusercontent.com/103019032/191734386-511cc3a6-b2b0-4eb9-b206-b86fe504c308.png)
#### Access Hadoop UI from Browser
     http://localhost:9870
![image](https://user-images.githubusercontent.com/103019032/191734724-053f96b3-62f8-438e-b29b-0121315a2679.png)
![image](https://user-images.githubusercontent.com/50055329/192437980-1e61208c-2f59-47cf-a149-e67cac444379.png)


# ==> HIVE
#### Download and Untar Hive,go to this link
     https://hive.apache.org/downloads.html
![capture9](https://user-images.githubusercontent.com/103019032/191893410-3956553d-6318-43b0-8e9d-938e00574ddc.PNG)
![capture10](https://user-images.githubusercontent.com/103019032/191893571-56b834f5-25f1-4fb5-9d75-c9a841d77f5c.PNG)
![capture11](https://user-images.githubusercontent.com/103019032/191893662-37ddf626-189d-4281-a56f-5cc1876e9775.PNG)
#### Alternatively, access your Ubuntu command line and download the compressed Hive files using and the wget command followed by the download path:
     wget https://downloads.apache.org/hive/hive-3.1.2/apache-hive-3.1.2-bin.tar.gz
#### Once the download process is complete, untar the compressed Hive package:
     tar xzf apache-hive-3.1.2-bin.tar.gz
#### Configure Hive Environment Variables (bashrc)
     nano .bashrc
#### Append the following Hive environment variables to the .bashrc file:
     export HIVE_HOME= "home/hdoop/apache-hive-3.1.2-bin"
     export PATH=$PATH:$HIVE_HOME/bin
![capture12](https://user-images.githubusercontent.com/103019032/191895189-8831c373-8f90-4c49-a62c-49735a65143c.PNG)
#### Edit hive-config.sh file
     nano apache-hive-3.1.2-bin/bin/hive-config.sh
![capture13](https://user-images.githubusercontent.com/103019032/191896225-2f2925b6-0b3e-4a93-8071-9c6a5bd403c3.PNG)
![image](https://user-images.githubusercontent.com/103019032/191896302-945031a1-2ac8-406f-a362-47be06a99278.png)
#### Create Hive Directories in HDFS
#### Create tmp Directory
      hdfs dfs -mkdir /tmp
      hdfs dfs -chmod g+w /tmp
      hdfs dfs -ls /
#### Create warehouse Directory
      hdfs dfs -mkdir -p /user/hive/warehouse
#### Add write and execute permissions to warehouse group members:
      hdfs dfs -chmod g+w /user/hive/warehouse
#### Check if the permissions were added correctly:
      hdfs dfs -ls /user/hive
#### Initiate Derby Database
      apache-hive-3.1.2-bin/bin/schematool -dbType derby -initSchema
#### After doing this command the message shown this type:
![image](https://user-images.githubusercontent.com/103019032/191899286-3fe7a1d3-e197-406a-a743-ca65b7299af2.png)
#### How to Fix guava Incompatibility Error in Hive:
      ls apache-hive-3.1.2-bin/lib
![image](https://user-images.githubusercontent.com/103019032/191917489-1248ff91-c0dc-40ff-b438-d1b791e5cce4.png)
#### Locate the guava jar file in the Hadoop lib directory as well:
      ls hadoop-3.3.4/share/hadoop/hdfs/lib
![image](https://user-images.githubusercontent.com/103019032/191918520-3ea8d545-fbba-48f9-b413-abcd0111efa1.png)
#### The two listed versions are not compatible and are causing the error. Remove the existing guava file from the Hive lib directory:
      rm apache-hive-3.1.2-bin/lib/guava-19.0.jar
#### Copy the guava file from the Hadoop lib directory to the Hive lib directory:
      cp hadoop-3.3.4/share/hadoop/hdfs/lib/guava-27.0-jre.jar apache-hive-3.1.2-bin/lib/
#### Use the schematool command once again to initiate the Derby database:
      $apache-hive-3.1.2-bin/bin/schematool -dbType derby -initSchema
#### Start the Hive command-line interface using the following commands:
      apache-hive-3.1.2-bin$ bin/hive
![image](https://user-images.githubusercontent.com/103019032/191919454-87cf43c3-75f3-41d3-b908-03c57b36ae3a.png)
#### I have used some command for creating a database and show the database:
      create database <database_name>;
      show databases;
![capture14](https://user-images.githubusercontent.com/103019032/191921010-820cf2e9-dc7b-42fa-a2b8-9da3a8722fe7.PNG)

##### Second way ==>
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
