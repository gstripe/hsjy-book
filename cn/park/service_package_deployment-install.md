# 服务实例包部署安装

## 参考信息
> https://docs.spring.io/spring-boot/docs/current/reference/htmlsingle/#deployment-install
> http://blog.didispace.com/spring-boot-run-backend/
> http://blog.csdn.net/hengyunabc/article/details/51050219
> http://www.cnblogs.com/lobo/p/5657684.html

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

> 注意，第一次发布服务的时候需要进行如下配置：

```
# 使用root用户登录服务器
su root

# 删除旧的软链接，如果有的话
rm -rf /etc/init.d/service-account

# 创建软链接，此时软链接的指向是无效的
ln -s /home/hsit/alpaca/service-account.jar /etc/init.d/service-account

# 到这里后台服务就算做好了
ll /etc/init.d

# 可以看到有一个链接指向，即为成功创建

```

## 服务实例
```
# 使用普通用户连接到服务器
sshpass -p hsit ssh hsit@192.168.2.75 -o StrictHostKeyChecking=no

# 尝试停止旧服务，如果有的话
service service-account stope

# 进入目录，设置一个文件名称，之后的操作都需要这个临时变量
cd /home/hsit/alpaca
jarfile=service-account

# 删除旧文件，如果有的话
rm $NAME.jar

# 从ftp复制新的服务
wget ftp://hsftp:hsftp@10.188.180.99/jar/$jarfile.jar

# 设置所有者与权限
chown hsit:hsit $jarfile.jar

# 启动服务
service $jarfile start

```

> 一些安全相关的设置
chown hsit:hsit service-account.jar
chmod 500 service-account.jar
chattr +i service-account.jar

> 注意这里如果使用service service-account start 之类的会拿不到JAVA_HOME这些环境变量，需要使用$NAME.conf来配置服务参数。所以就不用这种方法了。