# 服务实例包部署安装

## 参考信息
> https://docs.spring.io/spring-boot/docs/current/reference/htmlsingle/#deployment-install
> http://blog.didispace.com/spring-boot-run-backend/
> http://blog.csdn.net/hengyunabc/article/details/51050219
> http://www.cnblogs.com/lobo/p/5657684.html
> http://blog.phpha.com/backup/archives/1458.html

## Centos6 下将服务安装为后台服务

首先修改pom.xml下的插件spring-boot-maven-plugin，并添加executable配置
```
<plugin>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-maven-plugin</artifactId>
    <configuration>
        <executable>true</executable>
    </configuration>
    <executions>
        <execution>
            <goals>
                <goal>build-info</goal>
            </goals>
        </execution>
    </executions>
</plugin>
```

接着，打包，得到的jar用文本编辑器打开，可以看到200多行的这个内容
```
#!/bin/bash
#
#    .   ____          _            __ _ _
#   /\\ / ___'_ __ _ _(_)_ __  __ _ \ \ \ \
#  ( ( )\___ | '_ | '_| | '_ \/ _` | \ \ \ \
#   \\/  ___)| |_)| | | | | || (_| |  ) ) ) )
#    '  |____| .__|_| |_|_| |_\__, | / / / /
#   =========|_|==============|___/=/_/_/_/
#   :: Spring Boot Startup Script ::
#

### BEGIN INIT INFO
# Provides:          service-account
# Required-Start:    $remote_fs $syslog $network
# Required-Stop:     $remote_fs $syslog $network
# Default-Start:     2 3 4 5
# Default-Stop:      0 1 6
# Short-Description: service-account
# Description:       Parent pom providing dependency and plugin management for applications built with Maven
# chkconfig:         2345 99 01
### END INIT INFO

[[ -n "$DEBUG" ]] && set -x

# Initialize variables that cannot be provided by a .conf file
WORKING_DIR="$(pwd)"
# shellcheck disable=SC2153
[[ -n "$JARFILE" ]] && jarfile="$JARFILE"
[[ -n "$APP_NAME" ]] && identity="$APP_NAME"
............. 还有很多内容 .............
```

这样就有了一个集成了Shell脚本的可执行jar。
把jar发布到你在服务器上的目录下。

## 服务安装步骤
```
# 使用root用户登录服务器
su root

# 设置临时变量，服务home目录记录jar名，不带后缀名
ALPACA_HOME=/home/hsit/alpaca
SERVICE_NAME=service-account

# 尝试停止旧服务，如果有的话
service $SERVICE_NAME stop

# 进入目录，设置一个文件名称，之后的操作都需要这个临时变量
cd $ALPACA_HOME

# 删除旧文件，如果有的话
rm -rf $SERVICE_NAME.jar

# 从ftp复制新的服务
wget ftp://hsftp:hsftp@10.188.180.99/jar/$SERVICE_NAME.jar

# 设置所有者与可执行权限
chown hsit:hsit $SERVICE_NAME.jar
chmod 500 $SERVICE_NAME.jar

# 删除旧的软链接，如果有的话
rm -rf /etc/init.d/$SERVICE_NAME

# 创建软链接，此时软链接的指向是无效的
ln -s $ALPACA_HOME/$SERVICE_NAME.jar /etc/init.d/$SERVICE_NAME

# 在jar同目录下创建配置文件
vi $ALPACA_HOME/$SERVICE_NAME.conf

# 接着输入如下内容（此处配置除了RUN_ARGS外都保持默认）：
LOG_FOLDER=./log
JAVA_HOME=/usr/local/jdk1.7.0_80
JAVA_OPTS=-Xmx128M
RUN_ARGS=--spring.profiles.active=prod

# 启动服务
service $SERVICE_NAME start

# 开机启动，添加、打开、关闭、查看服务启动状态
chkconfig --add $SERVICE_NAME
chkconfig $SERVICE_NAME on
chkconfig $SERVICE_NAME off
chkconfig --list
```

## 服务更新步骤
> 如果服务不需要全新部署，只需要更新jar包，那么使用下面的步骤进行服务程序包的更新
> 目的：需要保留旧版本的数据
```

```

> 一些安全相关的设置，可以放置服务程序被勿删除修改什么的
chown hsit:hsit service-account.jar
chmod 500 service-account.jar
chattr +i service-account.jar
chmod 400 service-account.conf
chown root:root service-account.conf

> 注意这里如果使用service service-account start 之类的会拿不到JAVA_HOME这些环境变量，需要使用$NAME.conf来配置服务参数。