#HADOOP Setup On Ubuntu 12.04

####1.Get JAVA 
```
sudo apt-get install default-java
```

####2.Get Python Package
[pip](Download link) is the most used Python Control package  that could easily handle all of your Python third-party packages.
 - open terminal in your machine
 - go to the folder has the get-pip.py you just download
```
sudo python install get-pip.py
```
 - then pip is installed on your machine, next time if you need to install a package, just run:
```
sudo pip install yourpackagename
```
####3.Get SSH
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


####4.Get Hadoop
We will use Apache Hadoop 2.6.0 for this time   .
Download the [Hadoop] and the extract to the home folder 
```
/home/hadoop/Documents/hadoop-2.6.0-src
```
and then rename it:
```
mv /home/hadoop/Documents/hadoop-2.6.0-src /home/hadoop/Documents/hadoop
```
####5.Config the Hadoop
Since Hadoop running on java, so we will set the JAVA_HOME.
```
vim ~/.bash_profile
```
and then add
```
export JAVA_HOME=/usr/lib/jvm/default-java/bin
```
exit vim and then source the .bash_profile to make the config work
```
source ~/.bash_profile
```


[pip]:<https://bootstrap.pypa.io/get-pip.py>
[hadoop]:<http://apache.spinellicreations.com/hadoop/common/hadoop-2.6.0/hadoop-2.6.0.tar.gz>

