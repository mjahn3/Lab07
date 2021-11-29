# Lab 07

   * Switch to home folder: `cd ~`
   * Download Hadoop: `wget https://dlcdn.apache.org/hadoop/common/hadoop-3.3.1/hadoop-3.3.1.tar.gz`
   * Extract Hadoop: `tar -xvzf hadoop-3.3.1.tar.gz`

   * Install prerequisites (run in terminal):
```
sudo apt update
sudo apt install ssh
sudo apt install openjdk-8-jdk openjdk-8-jre
sudo apt install openssh-server openssh-client
```

   * Setup a user for Hadoop:
```
sudo adduser --gecos "" hadoop
su hadoop
ssh-keygen -t rsa
cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
```

   * Test hadoop user:
```
ssh localhost
exit
```

   * Copy-paste the following at the end of ~/.bashrc (`gedit ~/.bashrc`):
```
export HADOOP_HOME=/home/hadoop/hadoop-3.3.1
export HADOOP_INSTALL=$HADOOP_HOME
export HADOOP_MAPRED_HOME=$HADOOP_HOME
export HADOOP_COMMON_HOME=$HADOOP_HOME
export HADOOP_HDFS_HOME=$HADOOP_HOME
export YARN_HOME=$HADOOP_HOME
export HADOOP_COMMON_LIB_NATIVE_DIR=$HADOOP_HOME/lib/native
export PATH=$PATH:$HADOOP_HOME/sbin:$HADOOP_HOME/bin
export HADOOP_OPTS="-Djava.library.path=$HADOOP_HOME/lib/native"
```

   * Then run: `source ~/.bashrc`

   * Edit a Hadoop configuration file: `gedit ~/hadoop-3.3.1/etc/hadoop/hadoop-env.sh`

       * Change: `export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64` 
       * Save and close

   * Edit a Hadoop configuration file: `gedit ~/hadoop-3.3.1/etc/hadoop/core-site.xml`

```
<property>
  <name>fs.defaultFS</name>
  <value>hdfs://localhost:9000</value>
</property>

<property>
  <name>hadoop.tmp.dir</name>
  <value>/home/hadoop/hadooptmpdata</value>
</property>
```
   * Edit a Hadoop configuration file: `gedit ~/hadoop-3.3.1/etc/hadoop/hdfs-site.xml`

```
<property>
  <name>dfs.replication</name>
  <value>1</value>
</property>

<property>
  <name>dfs.name.dir</name>
  <value>file:///home/hadoop/hdfs/namenode</value>
</property>

<property>
  <name>dfs.data.dir</name>
  <value>file:///home/hadoop/hdfs/datanode</value>
</property>

```

   * Edit a Hadoop configuration file: `gedit ~/hadoop-3.3.1/etc/hadoop/mapred-site.xml`

```
<property>
  <name>mapreduce.framework.name</name>
  <value>yarn</value>
</property>
```

   * Edit a Hadoop configuration file: `gedit ~/hadoop-3.3.1/etc/hadoop/yarn-site.xml`

```
<property>
  <name>mapreduceyarn.nodemanager.aux-services</name>
  <value>mapreduce_shuffle</value>
</property>
```

   * Create the temporary directory: `mkdir ~/hadooptmpdata`
   * Create NameNode/DataNode directories: `mkdir -p ~/hdfs/namenode ~/hdfs/datanode`

   * Format the NameNode: `hdfs namenode -format`
   * Start HDFS: `start-dfs.sh`
   * Start YARN: `start-yarn.sh`
   * Check Java processes: `jps`
