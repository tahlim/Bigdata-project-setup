# Step_1:- Kafka
- helm chart link “https://confluentinc.github.io/cp-helm-charts/”
- GitHub link: “https://github.com/confluentinc/cp-helm-charts”

### create namespace services
- kubectl create namespace services
### add helm repo
- helm repo add confluentinc https://confluentinc.github.io/cp-helm-charts/
### you just install kafka with custom helm file
- helm install  -n services confluent-chart confluentinc/cp-helm-charts -f confluent-aws-kafka-zookeeper-deployment.yaml 
- helm uninstall confluent-chart -n services
### //create kafka-client pods with yaml file found at location “dmat_eks_deployment_files/confluent-kafka-zookeeper”
- kubectl -n services apply -f dmat_eks_deployment_files/confluent-kafka-zookeeper

------------------------------------------------------
- helm install confluent-chart confluentinc/cp-helm-charts -f confluent-values.yaml -n services
- helm uninstall confluent-chart -n services
### to create topics
- ./createkafka.sh 1
### to create schema
```
- kubectl exec -it kafka-client -n services -- curl http://confluent-chart-cp-schema-registry:8081/subjects/dlf-DEV3-value/versions -H 'Content-Type: application/json' --data-binary '{"schema":"{\"type\":\"record\",\"namespace\":\"com.verizon.oneparser.avroschemas\",\"name\":\"Logs\",\"version\":\"1\",\"fields\":[{\"name\":\"dmUser\",\"type\":[\"int\",\"null\"]},{\"name\":\"creationTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"lastLogTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"fileName\",\"type\":[\"string\",\"null\"]},{\"name\":\"size\",\"type\":[\"double\",\"null\"]},{\"name\":\"mdn\",\"type\":[\"string\",\"null\"]},{\"name\":\"imei\",\"type\":[\"string\",\"null\"]},{\"name\":\"id\",\"type\":\"long\"},{\"name\":\"firstname\",\"type\":[\"string\",\"null\"]},{\"name\":\"lastname\",\"type\":[\"string\",\"null\"]},{\"name\":\"isinbuilding\",\"type\":[\"int\",\"null\"]},{\"name\":\"hasgps\",\"type\":[\"int\",\"null\"]},{\"name\":\"emailid\",\"type\":[\"string\",\"null\"]},{\"name\":\"status\",\"type\":[\"string\",\"null\"]},{\"name\":\"modelName\",\"type\":[\"string\",\"null\"]},{\"name\":\"fileLocation\",\"type\":[\"string\",\"null\"]},{\"name\":\"esDataStatus\",\"type\":[\"string\",\"null\"]},{\"name\":\"esRecordCount\",\"type\":[\"double\",\"null\"]},{\"name\":\"importstarttime\",\"type\":[\"long\",\"null\"]},{\"name\":\"importstoptime\",\"type\":[\"long\",\"null\"]},{\"name\":\"filetype\",\"type\":[\"string\",\"null\"]},{\"name\":\"startLogTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"updatedTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"failureInfo\",\"type\":[\"string\",\"null\"]},{\"name\":\"logfilestatusforlv\",\"type\":[\"string\",\"null\"]},{\"name\":\"lvupdatedtime\",\"type\":[\"long\",\"null\"]},{\"name\":\"lverrordetails\",\"type\":[\"string\",\"null\"]},{\"name\":\"statusCsvFiles\",\"type\":[\"string\",\"null\"]},{\"name\":\"csvUpdatedTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"csvErrorDetails\",\"type\":[\"string\",\"null\"]},{\"name\":\"technology\",\"type\":[\"string\",\"null\"]},{\"name\":\"seqStartTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"seqEndTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"hiveStartTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"hiveEndTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"esStartTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"esEndTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"lvfilestarttime\",\"type\":[\"long\",\"null\"]},{\"name\":\"missingVersions\",\"type\":[\"string\",\"null\"]},{\"name\":\"lvPick\",\"type\":[\"string\",\"null\"]},{\"name\":\"lvStatus\",\"type\":[\"string\",\"null\"]},{\"name\":\"lvparseduserid\",\"type\":[\"string\",\"null\"]},{\"name\":\"lvlogfilecnt\",\"type\":[\"long\",\"null\"]},{\"name\":\"processingServer\",\"type\":[\"string\",\"null\"]},{\"name\":\"reportsHiveTblName\",\"type\":[\"string\",\"null\"]},{\"name\":\"compressionstatus\",\"type\":[\"boolean\",\"null\"]},{\"name\":\"eventsCount\",\"type\":[\"int\",\"null\"]},{\"name\":\"ftpstatus\",\"type\":[\"boolean\",\"null\"]},{\"name\":\"userPriorityTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"reprocessedBy\",\"type\":[\"int\",\"null\"]},{\"name\":\"pcapMulti\",\"type\":[\"string\",\"null\"]},{\"name\":\"pcapSingleRm\",\"type\":[\"string\",\"null\"]},{\"name\":\"pcapSingleUm\",\"type\":[\"string\",\"null\"]},{\"name\":\"cpHdfsTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"cpHdfsStartTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"cpHdfsEndTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"hiveDirEpoch\",\"type\":[\"string\",\"null\"]},{\"name\":\"ondemandBy\",\"type\":[\"int\",\"null\"]},{\"name\":\"carrierName\",\"type\":[\"string\",\"null\"]},{\"name\":\"odlvUserId\",\"type\":[\"int\",\"null\"]},{\"name\":\"odlvUpload\",\"type\":[\"boolean\",\"null\"]},{\"name\":\"odlvOnpStatus\",\"type\":[\"string\",\"null\"]},{\"name\":\"odlvLvStatus\",\"type\":[\"string\",\"null\"]},{\"name\":\"zipStartTime\",\"type\":[\"long\",\"null\"]},{\"name\":\"zipEndTime\",\"type\":[\"long\",\"null\"]} , { \"name\": \"logcodes\", \"type\":[\"string\", \"null\"] }, { \"name\": \"triggerCount\", \"type\":[\"int\", \"null\"] }]}"}'
```
### to check schema, after you create schema
- kubectl exec -it kafka-client -n services -- curl http://confluent-chart-cp-schema-registry:8081/subjects
### to delete schema
- kubectl exec -it kafka-client -n services -- curl -X DELETE http://confluent-chart-cp-schema-registry:8081/subjects/dlf-DEV3-value

==================================================
#### kafka-values file
- vim confluent-values.yaml
```
..
```

# Step_2:- Hive & HDFS
- GitHub link: https://github.com/gradiant/charts
- helm chart link “https://hub.kubeapps.com/charts/gradiant/hive”

### Create a namespace "hive"
- kubectl create namespace hive
### Add helm repo
- helm repo add gradiant https://gradiant.github.io/charts/
### Install chart
- helm install dmat-hive gradiant/hive -n hive
### get list of pods in hive namespace
- kubectl -n hive get pods

### create folders  required for onp in the hdfs namenode
- kubectl -n hive exec -it dmat-hive-hdfs-namenode-0 /bin/bash

- hdfs dfs -mkdir -p /с7000-op-checkpoints
- hdfs dfs -mkdir -p /oneparser-k8s-c7000
- hdfs dfs -mkdir -p /spark2-k8s-history
- hdfs dfs -chmod -R 777 /с7000-op-checkpoints
- hdfs dfs -chmod -R 777 /oneparser-k8s-c7000
- hdfs dfs -chmod -R 777 /spark2-k8s-history
- hdfs dfs -chmod -R 777 /
- hdfs dfs -ls /

- kubectl -n hive cp geoshapes.tar dmat-hive-hdfs-namenode-0:/tmp 
- cd /tmp
- ls
- tar -xvf geoshapes.tar
- ls
- cd geoshapes
- ls
- hdfs dfs -mkdir -p /app/assets/geoShapes/
- hdfs dfs -chmod 777 /app/assets/geoShapes/
- hdfs dfs -chmod 777 /app/assets/
- hdfs dfs -chmod 777 /app
- hdfs dfs -chmod 777 /
- hdfs dfs -copyFromLocal ./* /app/assets/geoShapes/
- hdfs dfs -ls /app/assets/geoShapes/
- hdfs dfs -chmod 777 /app/assets/geoShapes/
- hdfs dfs -ls /app/assets/geoShapes/
- hdfs dfs -chmod 777 /app/assets/geoShapes/*
- hdfs dfs -ls /app/assets/geoShapes/

- kubectl -n hive exec -it dmat-hive-hdfs-namenode-0 -- bash
- hdfs dfs -ls /
- hdfs dfs -ls /app
- hdfs dfs -rm -r /app/assets/geoShapes/
- hdfs dfs -ls /app/assets

### create database on hive-server
- kubectl -n hive exec -it dmat-hive-server-0 /bin/bash
##### go to hive promt by running command hive on the shell, it will open hive shell for us
- hive
##### Run command to get the list of databases available
- SHOW DATABASES;
##### If dmat_logs is not there, create a database by running below command
- CREATE DATABASE dmat_logs;
##### confirm the database dmat_logs created or not
- SHOW DATABASES;
##### if database dmat_logs is there then exit from the hive prompt
- exit or quit or ctrl +D
##### check for the warehouse and db_logs it in ..you will find it in location “/user/hive/warehouse/dmat_logs.db”
- hdfs dfs -ls /user/hive/warehouse
### create database on hive-postgresql server
- kubectl -n hive exec -it dmat-hive-postgresql-0 /bin/bash
- psql -d metastore -U hivepassword is “hive”
##### after entering the database run \l   it will provide you the list of db if dmat_logs is present then exit from it else create db
- \l
- CREATE DATABASE dmat_logs;
##### grant all privilege to it
- GRANT ALL PRIVILEGES ON DATABASE dmat_logs TO hive;
##### check again run  \l to verify
- \l

==================================================
#### bigdata-values file
- vim bigdata-values.yaml
```
hdfs:
  persistence:
  nameNode:
    enabled: true
    storageClass:
    accessMode: ReadWriteOnce
    size: 500Gi
    nodeSelector:
      service: "true"
  dataNode:
    enabled: true
    storageClass:
    accessMode: ReadWriteOnce
    size: 500Gi
    nodeSelector:
      service: "true"
  httpfs:
    nodeSelector:
      service: "true"

hive:
  nodeSelector:
    service: "true"
  persistence:
    enabled: true
    size: 100Gi
hive-metastore:
  nodeSelector:
    service: "true"
  postgres:
    primary:
      nodeSelector:
        service: "true"
```		

# Step_2:- spark-operator

//helm chart link “https://googlecloudplatform.github.io/spark-on-k8s-operator”//
//GitHub link: “https://github.com/GoogleCloudPlatform/spark-on-k8s-operator”//
//Add spark operator repo
helm repo add spark-operator https://googlecloudplatform.github.io/spark-on-k8s-operator
//create a namespace “spark”//
kubectl create namespace spark
//create a namespace “spark-operator”//
kubectl create namespace spark-operator
//create service account spark in ns spark//
kubectl create serviceaccount spark --namespace=spark
//create clusterrolebinding spark-role in ns spark//
kubectl create clusterrolebinding spark-role --clusterrole=edit --serviceaccount=default:spark --namespace=spark
//install helm chart with our custom values files which contains values as per our project//
//you can find the values file at location : “dmat_eks_deployment_files/modified_values_file_aws/spark-operator-aws-values.yaml
helm install spark-operator spark-operator/spark-operator --namespace spark-operator -f dmat_eks_deployment_files/modified_values_file_aws/spark-operator-aws-values.yaml
//get the list of pods related to spark operator//
kubectl -n spark-operator get pods
