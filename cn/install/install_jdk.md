# jdk安装

## 此处安装jdk-7u80-linux-x64.tar.gz
```
# root
su root
# Download and unzip the packaged version.
wget ftp://hsftp:hsftp@10.188.180.99/devtools/jdk/jdk-7u80-linux-x64.tar.gz
tar -zxvf jdk-7u80-linux-x64.tar.gz
# change owner jdk1.7.0_80
chown -R hsit.hsit jdk1.7.0_80

# hsit
cd ~
vi .bash_profile
# edit add
export JAVA_HOME=/opt/jdk1.7.0_80
export PATH=$JAVA_HOME/bin:$PATH
# save :wq
source .bash_profile

# test
java -version
# info
java version "1.7.0_80"
Java(TM) SE Runtime Environment (build 1.7.0_80-b15)
Java HotSpot(TM) 64-Bit Server VM (build 24.80-b11, mixed mode)
```
```
其他：
在root下配置
#set java environment
vi /etc/profile

#jdk
export JAVA_HOME=/usr/local/jdk1.7.0_80
export PATH=$PATH:$JAVA_HOME/bin

#live
source /etc/profile
```

## Windows下安装

* 下载\[ftp\]/jdk/jdk-7u80-windows-x64.zip
* 解压到/dev4j/sdk下
* 配置环境变量 JAVA\_HOME  
  ![](/cn/install/images/dev4j_java_home.png)

* 控制台执行 java -version 出现以下提示说明安装成功  
  ![](/cn/install/images/dev4j_java_home_version.png)



