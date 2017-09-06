# 服务实例包部署安装
> 参考信息
> https://docs.spring.io/spring-boot/docs/current/reference/htmlsingle/#deployment-install
> http://blog.didispace.com/spring-boot-run-backend/

## Centos6 下将服务安装为后台服务

首先在pom.xml里面添加插件
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