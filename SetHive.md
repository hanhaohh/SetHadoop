# Contin. Setup Hive 1.2.1 with Hadoop 2.6.0

Continuing with our work with Hadoop, we are going to install **Hive** on this **single node** cluster.

Apache Hive is a data warehouse infrastructure built on top of Hadoop for providing data summarization, query, and analysis. While initially developed by Facebook, Apache Hive is now used and developed by other companies such as Netflix.

#### 1. Get Hive
Let's go back to the home directory
```
cd ~/Do
```
The **[Hive 1.2.1]** (Download link) :http://apache.arvixe.com/hive/hive-1.2.1/
```
wget http://apache.arvixe.com/hive/hive-1.2.1/apache-hive-1.2.1-bin.tar.gz
tar zxvf apache-hive-1.2.1-bin.tar.gz
mv apache-hive-1.2.1-bin.tar.gz hive 
```
#### 2. Configure Hive
Let's modify ~/.bashrc to include Hive directory 
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

```




[Hive 1.2.1]: http://apache.arvixe.com/hive/hive-1.2.1/apache-hive-1.2.1-bin.tar.gz
