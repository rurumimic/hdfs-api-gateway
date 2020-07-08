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

## /etc/hosts

```bash
sudo vi /etc/hosts
```

```bash
127.0.0.1 localhost

192.168.10.101 zimmer
192.168.20.101 amadeus
192.168.30.101 bach
```

## HDFS setup

[Single Node](single.node.md)

## API Gateway

[API Gateway](api.md)

## Local Test

```bash
curl -v 'http://localhost:8000/amadeus/webhdfs/v1/user/vagrant/input/core-site.xml?op=OPEN&user.name=vagrant'
curl -v 'http://localhost:8000/bach/webhdfs/v1/user/vagrant/input/core-site.xml?op=OPEN&user.name=vagrant'
```
