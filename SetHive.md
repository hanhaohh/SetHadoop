# Contin. Setup Hive 1.2.1 with Hadoop 2.6.0

Continuing with our work with Hadoop, we are going to install **Hive** on this **single node** cluster.

Apache Hive is a data warehouse infrastructure built on top of Hadoop for providing data summarization, query, and analysis. While initially developed by Facebook, Apache Hive is now used and developed by other companies such as Netflix.

#### 1. Get Hive
Let's go back to the home directory
```
cd ~/Documents
```
The **[Hive 1.2.1]** (Download link) :http://apache.arvixe.com/hive/hive-1.2.1/
```
wget http://apache.arvixe.com/hive/hive-1.2.1/apache-hive-1.2.1-bin.tar.gz
tar zxvf apache-hive-1.2.1-bin.tar.gz
mv apache-hive-1.2.1-bin.tar.gz hive 
```
#### 2. Configure Hive
Let's **modify ~/.bashrc** to include Hive directory 
```
export HIVE_HOME=/home/hadoop/Documents/hive
export PATH=$HIVE_HOME/bin:/home/hadoop/Documents/hadoop/bin:$PATH
```
Go to Hive folder,
then
```
cd conf
```
```
cp hive-default.xml.template hive-site.xml
cp hive-env.sh.template  hive-env.sh

vim hive-site.xml
```
Servral changes need to be edited in ```hive-site.xml```:
```
line 334: hive.metastore.warehouse.dir is the HDFS directory that hive will store all the data, 
default is /user/hive/warehouse, I change it to /hive/warehouse
```
next, becuase there is some name conflication in hive-site.xml, we will replace every value of field ${system:java.io.tmpdir} to a directory that  created, for example, let's replace with /home/hadoop/Documents/hive/iotmp (/home/hadoop/Documents/hive/iotmp is the directory i manually created)

Otherwise, you will see problem like the error in following images:

https://dn-anything-about-doc.qbox.me/userid46108labid766time1427424512161

**Edit conf/hive-env.sh**

Set HADOOP_HOME to point to a specific hadoop install directory
```
HADOOP_HOME=/home/hadoop/Documents/hadoop
```
Folder containing extra ibraries required for hive compilation/execution can be controlled by:
```
export HIVE_AUX_JARS_PATH=/home/hadoop/Documents/hive_aux
```
save the change, then create folder hive_aux
```
mkdir /home/hadoop/Documents/hive_aux
```
**Final step**

Create hive folder in HDFS
```
hadoop dfs -mkdir /tmp
hadoop dfs -mkdir /hive
hadoop dfs -mkdir /tmp/hive
hadoop dfs -mkdir /hive/warehouse
hadoop dfs -mkdir /tmp/hive
hadoop dfs -chmod 777 /hive/warehouse
hadoop dfs -chmod 777 /tmp/hive
```
remove *$HADOOP_HOME/share/hadoop/yarn/lib/jline-0.9.94.jar* because there will be a confliction between hive's and hadoop's.
```
rm /home/hadoop/Documents/hadoop/share/hadoop/yarn/lib/jline-0.9.94.jar
```

# Get Started
**Hive** is ready to start if nothing goes crazy here:
```
~/Documents/hive/bin/hive
```







[Hive 1.2.1]: http://apache.arvixe.com/hive/hive-1.2.1/apache-hive-1.2.1-bin.tar.gz
