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

## Shared File System Master Slave 共享文件系统主从配置方法

> 现阶段使用主从两台机子进行业务，业务量大后再做拆分。

> 未来可能需要考虑负载均衡等。

**
需要一个可靠的DSF，这里偷懒暂使用Linux Samba建立了一个共享目录进行测试。
共享目录为 \\192.168.2.70\share
**
挂载文件系统
```
# 在root用户下

# 创建一个目录用来做挂载点
mkdir amq

# 将2.70的share目录挂载到amq下
mount -o username=share,password=share //192.168.2.70/share amq 

# 挂载完毕后可以看到远程目录的内容
ll amq

# 然后在 activemq的data下创建一个软链接链接到这个amq挂载点
ln -s /root/amq/kahadb /opt/activemq-5.14.0/data/kahadb_remote

# 注意 /root/amq/kahadb 路径仅供参考，视具体情况而定。

```

两台机子都配置完毕之后

```
# 进入s6与s7机子（主-从）
cd conf

vi activemq.xml

# 找到 <persistenceAdapter> 标签
# 修改 <kahaDB directory="${activemq.data}/kahadb"/>
# 为 <kahaDB directory="${activemq.data}/kahadb_remote"/>

# 可以的话 在 <broke 的brokerName属性定义一个名字方便识别

```