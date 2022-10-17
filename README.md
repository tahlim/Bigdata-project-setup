# ============> Hadoop <=============
``
Hadoop:- open source framework, data management tool
data management tool:- data store, manage, scale out storage(manually node add krna)
Hadoop components:- 1.HDFS & Mapreduce   2. HDFS & Yarn
HDFS:- data storage k liye  &  Mapreduce:- processing framework  &  Yarn:- processing
Hadoop daemons:- Namenode & datanode (storage part) , Job tracker & task tracker (process part)
Namenode is master and datanode is slave

Hadoop is a framework that uses distributed storage and parallel processing to store and manage Big Data. It is the most commonly used software to handle Big Data. There are three components of Hadoop.

Hadoop HDFS - Hadoop Distributed File System (HDFS) is the storage unit of Hadoop.
Hadoop MapReduce - Hadoop MapReduce is the processing unit of Hadoop.
Hadoop YARN - Hadoop YARN is a resource management unit of Hadoop.
Let us take a detailed look at Hadoop HDFS in this part of the What is Hadoop article.

Hadoop HDFS
Data is stored in a distributed manner in HDFS. There are two components of HDFS - name node and data node. While there is only one name node, there can be multiple data nodes.
HDFS is specially designed for storing huge datasets in commodity hardware.
``
