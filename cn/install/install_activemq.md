# ActiveMQ 集群说明

## 带HUB的拓扑结构

![](/cn/install/images/activemq_network_or_broker.png)

## 共享文件方式(Mater-Slave)

> 当然需要使用分布式文件系统，这里DFS目前只用了共享文件系统来代替

![](/cn/install/images/activemq_shared_file_system_master_slave.png)

# 配置说明

分别在各台机子上复制activemq二进制包到opt下，解压，授权

```
su root

cd /opt

wget ftp://hsftp:hsftp@10.188.180.99/devtools/mq/apache-activemq-5.14.0-bin.tar.gz

tar -zxvf apache-activemq-5.14.0-bin.tar.gz

chown -R hsit.hsit apache-activemq-5.14.0

su hsit

cd apache-activemq-5.14.0

# 进入解压后的目录之后进行每台机子的配置

```
