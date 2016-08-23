# zookeeper集群安装配置

zk 部署在

192.168.2.71 s1.demo.jy.hsit

192.168.2.72 s2.demo.jy.hsit

192.168.2.73 s3.demo.jy.hsit

![](/cn/install/images/zookeeper_01.png)

安装目录/opt/zookeeper-3.4.8

设置开机启动

su - hsit -c '/opt/zookeeper-3.4.8/bin/zkServer.sh start'

配置conf下的zoo.cfg文件
然后分别复制到三个节点中去
```
# The number of milliseconds of each tick
tickTime=2000
# The number of ticks that the initial
# synchronization phase can take
initLimit=10
# The number of ticks that can pass between
# sending a request and getting an acknowledgement
syncLimit=5
# the directory where the snapshot is stored.
# do not use /tmp for storage, /tmp here is just
# example sakes.
dataDir=/opt/zookeeper-3.4.8/data
# logs
dataLogDir=/opt/zookeeper-3.4.8/logs
# the port at which the clients will connect
clientPort=2181
# the maximum number of client connections.
# increase this if you need to handle more clients
#maxClientCnxns=60
#
# Be sure to read the maintenance section of the
# administrator guide before turning on autopurge.
#
# http://zookeeper.apache.org/doc/current/zookeeperAdmin.html#sc_maintenance
#
# The number of snapshots to retain in dataDir
#autopurge.snapRetainCount=3
# Purge task interval in hours
# Set to "0" to disable auto purge feature
#autopurge.purgeInterval=1

server.1=s1.demo.jy.hsit:2888:3888
server.2=s2.demo.jy.hsit:2888:3888
server.3=s3.demo.jy.hsit:2888:3888

```

集群的重要配置
在三个节点的data目录下分别
echo 1 > myid
echo 2 > myid
echo 3 > myid


