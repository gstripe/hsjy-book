# ActiveMQ 集群说明

## 带HUB的拓扑结构

![](/cn/install/images/activemq_network_or_broker.png)

## 共享文件方式\(Mater-Slave\)

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
> 
> 未来可能需要考虑负载均衡等。

**
需要一个可靠的DSF，这里偷懒暂使用Linux Samba建立了一个共享目录进行测试。
共享目录为 \192.168.2.70\share
**

> service smb start 启动samba服务
> 
> ps -ef \|grep smb 查看进程是否已经启动


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

:wq #保存

```

## 配置开机启动项

```
su root

su - hsit -c '/opt/activemq-5.14.0/bin/activemq start'

```

## forwarding bridge方式

Broker1 连接 Broker2 不使用双向连接（Broker1 -&gt; Broker2）

> duplex="false" 表示仅使用单向通讯
> 
> conduitSubscriptions="false" 表示每个 Consumer 上都会收到所有的发送的消息，一个远程端上注册的多个消费者不会被视为一个消费者。

```
<networkConnectors>
  <networkConnector uri="static://(tcp://s7.demo.jy.hsit:61616)"
     name="s6.p-bridge-s7.c" duplex="false"
     conduitSubscriptions="false"
     decreaseNetworkConsumerPriority="false">
  </networkConnector>
</networkConnectors>
```

## 开启远程监控

在activemq.xml配置文件中的&lt;broker 标签中增加 useJmx="true"，然后重启Borkder即可使用。（这里就不配置安全性相关的选项了）

接着在windows控制台什么的打开jconsole（有配置好JDK环境了）

然后可以看到如下界面：

![](/cn/install/images/jconsole.png)
主界面

![](/cn/install/images/jconsole_remote.png)
选择远程进程，输入ip地址，端口号。一切都是默认的。

![](/cn/install/images/jconsole_remote_insecure.png)
点击连接按钮之后，出现一个提示窗口，直接点Insecure按钮。

![](/cn/install/images/jconsole_connected.png)
进去后就可以看到内存，线程各种信息了。

