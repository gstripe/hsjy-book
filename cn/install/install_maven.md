# Maven安装配置

##　Windows下安装

最新版本下载
```
http://maven.apache.org/download.cgi
```
本地FTP
```
[ftp]/maven/apache-maven-3.3.9-bin.zip
```

配置步骤

* [安装JDK](/cn/install/install_jdk.md)（已经安装则忽略，jdk7以上）

* 解压文件到目录 dev4j/tools下

* 配置环境变量 MVN_HOME、MAVEN_OPTS、添加到Path中

![](/cn/install/images/dev4j_mvn_home.png)

* 控制台执行 mvn -v 出现以下提示说明安装成功

![](/cn/install/images/dev4j_mvn_home_version.png)

> MAVEN_OPTS 避免maven项目过大导致OOM

以上都是默认配置，具体自定义设置请移步此处——[Maven 使用](/cn/usage/useage_maven.md)