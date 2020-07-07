# HDFS API Gateway

## Download

- [VirtualBox](https://www.virtualbox.org/wiki/Downloads)
- [Vagrant](https://www.vagrantup.com/downloads)
  
Download [http://apache.mirror.cdnetworks.com/hadoop/common/hadoop-2.10.0/hadoop-2.10.0.tar.gz](http://apache.mirror.cdnetworks.com/hadoop/common/hadoop-2.10.0/hadoop-2.10.0.tar.gz) to `data`.

## Architecture

- Zimmer: API Gateway
- Amadeus: HDFS Cluster 1
- Bach: HDFS Cluster 2

## VM

VM:

```bash
vagrant up
# vagrant halt
# vagrant resume
# vagrant suspend
```

VM connect:

```bash
vagrant ssh amadeus
vagrant ssh bach
# vagrant ssh zimmer
```

SSH set:

```bash
ssh localhost
Are you sure you want to continue connecting (yes/no)? yes
```

JAVA version:

```bash
java -version
javac -version
```

HDFS version:

```bash
hdfs version
```

## HDFS setup

[Single Node](single.node.md)

## API Gateway

[API Gateway](api.md)
