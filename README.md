# Lab 07

## Hadoop Setup

   * Switch to home folder: `cd ~`
   * Download Hadoop: `wget https://dlcdn.apache.org/hadoop/common/hadoop-3.3.1/hadoop-3.3.1.tar.gz`
   * Extract Hadoop: `tar -xvzf hadoop-3.3.1.tar.gz`
   * Install prerequisites (run in terminal):

```
sudo apt update
sudo apt install openjdk-8-jdk openjdk-8-jre
sudo apt install openssh-server openssh-client
```

   * Setup a user for Hadoop:

```
sudo adduser --gecos "" hadoop
xhost +
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

   * Then run: `source ~/.bashrc; echo $HADOOP_HOME`
   * Switch back to the gb760 user: `exit`
   * Get Hadoop configuration files:

```
cd ~/hadoop-3.3.1/etc/hadoop/
wget https://raw.githubusercontent.com/GENBUS760/Lab07/master/hadoop-config/core-site.xml
wget https://raw.githubusercontent.com/GENBUS760/Lab07/master/hadoop-config/hdfs-site.xml
wget https://raw.githubusercontent.com/GENBUS760/Lab07/master/hadoop-config/mapred-site.xml
wget https://raw.githubusercontent.com/GENBUS760/Lab07/master/hadoop-config/yarn-site.xml
wget https://raw.githubusercontent.com/GENBUS760/Lab07/master/hadoop-config/hadoop-env.sh
```

   * Create directories needed by Hadoop:

```
su hadoop
mkdir ~/hadooptmpdata
mkdir -p ~/hdfs/namenode ~/hdfs/datanode
```
   * Format the NameNode: `hdfs namenode -format`
   * Start HDFS: `start-dfs.sh`
   * Start YARN: `start-yarn.sh`
   * Check Java processes: `jps`
