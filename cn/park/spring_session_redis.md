# 基于Redis的Spring Session

> 基于Spring Session组件，并使用redis进行会话的存储

* 导入依赖包

```
<dependency>
    <groupId>alpaca.park</groupId>
    <artifactId>alpaca-park-common</artifactId>
    <version>0.0.1-RELEASE</version>
</dependency>

<!-- spring session redis -->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-redis</artifactId>
</dependency>
<dependency>
    <groupId>org.springframework.session</groupId>
    <artifactId>spring-session-data-redis</artifactId>
</dependency>
```

* 配置文件

> 导入spring-session-data-redis之后必须进行如下配置

```
spring:
  session:
    store-type: redis #如果不需要使用则设置成null，否则在引入了spring-session包之后，会报错
  redis:
    host: 192.168.2.70
    prot: 6379

park:
  session:
    redis:
     style: park # park风格，使用json来进行序列化，建议使用。如果不使用直接写none，将会使用jdk序列方式
    strategy: cookie #会话策略 提供两个值 header、cookie

```

> 注意：
> spring.redis.* 还有其他配置，比如配置pool相关参数，这里使用默认参数
> park.session.strategy:
> 1. header 会话ID存在请求头中；请求头名称默认为： x-auth-token，可以通过park.session.header.name自定义
> 2. cookie 会话id存放在浏览器cookie中；Cookie名称默认为： SESSIONID，可以通过park.session.cookie.name自定义


* 代码编写


```
@SpringBootApplication
@ImportAutoConfiguration(value = {
        ParkRedisSessionConfiguration.class
})
public class ManagerApplication {

    public static void main(String[] args) {
        SpringApplication.run(ManagerApplication.class, args);
    }

}
```

> 特别注意：基于cookie的会话，如果想要会话共享，那么就需要使用nginx来进行反向代理，让cookie保持在同域下。







