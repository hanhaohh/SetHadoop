#                      BI&ABootcamp
## HADOOP Setup On Ubuntu 12.04

#### 1.Get JAVA 
```
sudo apt-get install openjdk-7-jre,openjdk-7-jdk
```

#### 2.Get Python Package
[pip]  is the most used Python Control package  that could easily handle all of your Python third-party packages.
 - open terminal in your machine
 - go to the folder has the get-pip.py you just download
```
sudo python get-pip.py 
```
 - then pip is installed on your machine, next time if you need to install a package, just run:
```
sudo pip install yourpackagename
```
#### 3.Get SSH
ssh must be installed and sshd must be running to use the Hadoop scripts that manage remote Hadoop daemons. 
To install SSH and rsync on Linux:
```
sudo apt-get install openssh-server
sudo apt-get install ssh
sudo apt-get install rsync
```
For nodes of cluster to communicate without password,we set up ssh. 
```
cd ~/.ssh/                     
ssh-keygen -t rsa   //create the public key and private key for this node 
cat id_rsa.pub >> authorized_keys   //add my public key to my authorized users list, it means this node allow itself to login
```


#### 4.Get Hadoop
We will use Apache Hadoop 2.6.0 for this time   .
Download the [Hadoop] and the extract to the home folder 
```
/home/hadoop/Documents/hadoop-2.6.0-src
```
and then rename it:
```
mv /home/hadoop/Documents/hadoop-2.6.0-src /home/hadoop/Documents/hadoop
```
#### 5.Config the Hadoop
Since Hadoop running on java, so we will set the JAVA_HOME.
```
vim ~/.bashrc
```
and then add
```
export PATH=$PATH:/home/hadoop/Documents/hadoop/bin:/home/hadoop/Documents/hadoop/sbin
export JAVA_HOME= /usr/lib/jvm/java-1.7.0-openjdk-amd64
```
exit vim and then source the .bash_profile to make the config work
```
source ~/.bashrc
```
Create folders that hadoop could save data to.
```
mkdir ~/hadoop_data
mkdir ~/hadoop_data/tmp
mkdir  ~/hadoop_data/tmp/
mkdir ~/hadoop_data/tmp/dfs/
mkdir ~/hadoop_data/tmp/dfs/data
mkdir ~/hadoop_data/tmp/dfs/name
```


There are 2 files need to be changed:

  -  core-site.xml
```
vim /home/hadoop/Documents/hadoop/etc/hadoop/core-site.xml
```
and then add:
```
<configuration>
    <property>
        <name>hadoop.tmp.dir</name>
        <value>file:/home/hadoop/hadoop_data/tmp</value>
        <description>Abase for other temporary directories.</description>
    </property>
    <property>
        <name>fs.defaultFS</name>
        <value>hdfs://localhost:9000</value>
    </property>
</configuration>
```
  -  hdfs-site.xml
```
<configuration>
    <property>
        <name>dfs.replication</name>
        <value>1</value>
    </property>
    <property>
        <name>dfs.namenode.name.dir</name>
        <value>file:/home/hadoop/hadoop_data/tmp/dfs/name</value>
    </property>
    <property>
        <name>dfs.datanode.data.dir</name>
        <value>file:/home/hadoop/hadoop_data/tmp/dfs/data</value>
    </property>
</configuration>
```

#### Get Started
Format our hdfs system:
```
hadoop namenode -format
```
if nothing goes crazy, you are good to go, to start your single node cluster:
```
start-dfs.sh
```
You can type ```jps``` to see if the hadoop system is running ok

If you do not see namenode or datanode daemon running, you could run ```stop-all.sh```
and restart your machine and try ```start-dfs.sh``` again

if it still does not work, please check the previous steps or email me at  <bgutta@stevens.edu> or <hhan2@stevens.edu>.

[pip]:<https://bootstrap.pypa.io/get-pip.py>
[hadoop]:<http://apache.spinellicreations.com/hadoop/common/hadoop-2.6.0/hadoop-2.6.0.tar.gz>

