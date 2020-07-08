## Single Node Setup

### hadoop-env.sh

```bash
vi $HADOOP_HOME/etc/hadoop/hadoop-env.sh
```

```bash
export JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk/jre
```

### core-site.xml

- Host: `amadeus`, `bach`
- Port: `9000`

```bash
vi $HADOOP_HOME/etc/hadoop/core-site.xml
```

```xml
<configuration>
    <property>
        <name>fs.defaultFS</name>
        <value>hdfs://amadeus:9000</value>
    </property>
    <property>
        <name>hadoop.proxyuser.vagrant.hosts</name>
        <value>*</value>
    </property>
    <property>
        <name>hadoop.proxyuser.vagrant.groups</name>
        <value>*</value>
    </property>
</configuration>
```

### hdfs-site.xml

```bash
vi $HADOOP_HOME/etc/hadoop/hdfs-site.xml
```

```xml
<configuration>
    <property>
        <name>dfs.replication</name>
        <value>1</value>
    </property>
</configuration>
```

### mapred-site.xml

```bash
mv $HADOOP_HOME/etc/hadoop/mapred-site.xml.template \
   $HADOOP_HOME/etc/hadoop/mapred-site.xml
vi $HADOOP_HOME/etc/hadoop/mapred-site.xml
```

```xml
<configuration>
    <property>
        <name>mapreduce.framework.name</name>
        <value>yarn</value>
    </property>
</configuration>
```

### yarn-site.xml

```bash
vi $HADOOP_HOME/etc/hadoop/yarn-site.xml
```

```xml
<configuration>
    <property>
        <name>yarn.nodemanager.aux-services</name>
        <value>mapreduce_shuffle</value>
    </property>
</configuration>
```

## Execution

### Format File System

```bash
hdfs namenode -format;
hdfs datanode -format;
```

### Start Daemons

```bash
start-dfs.sh;
start-yarn.sh;
```

### Stop Daemons

```bash
stop-yarn.sh;
stop-dfs.sh;
```

### Make Working Directory

```bash
hdfs dfs -mkdir -p /user/$USER
```

### Test

#### Load test files

```bash
hdfs dfs -mkdir -p /user/$USER/input
hdfs dfs -put $HADOOP_HOME/etc/hadoop/*.xml input
hdfs dfs -put $HADOOP_HOME/etc/hadoop/core-site.xml input
```

View the input files

```bash
hdfs dfs -ls -R /
```

#### Run a MapReduce job

Check your hadoop version

```bash
hadoop jar \
$HADOOP_HOME/share/hadoop/mapreduce/hadoop-mapreduce-examples-2.10.0.jar \
grep input output 'dfs[a-z.]+'
```

#### View output files

```bash
hdfs dfs -cat output/*
```

```bash
1       dfsadmin
1       dfs.replication
```

#### webhdfs

```bash
curl -sSL 'http://amadeus:50070/webhdfs/v1/user/vagrant/input/core-site.xml?op=OPEN&user.name=vagrant'
curl -sSL 'http://amadeus:50070/webhdfs/v1/user/vagrant/input?op=LISTSTATUS&user.name=vagrant'
```

```bash
curl -sSL 'http://bach:50070/webhdfs/v1/user/vagrant/input/core-site.xml?op=OPEN&user.name=vagrant'
curl -sSL 'http://bach:50070/webhdfs/v1/user/vagrant/input?op=LISTSTATUS&user.name=vagrant'
```
