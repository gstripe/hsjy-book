> 使用Redis存储会话

与 Spring Boot 工程整合

> 依赖包

```
<dependency>
    <groupId>alpaca.park</groupId>
    <artifactId>park-starter-redis-http-session</artifactId>
    <version>0.0.1-SNAPSHOT</version>
</dependency>
```

> yml配置项

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

> 配置项注意事项

spring.redis.\* 还有其他配置，比如配置pool相关参数，这里使用默认参数

park.session.strategy:

1. header 会话ID存在请求头中；请求头名称默认为： x-auth-token，可以通过park.session.header.name自定义

2. cookie 会话id存放在浏览器cookie中；Cookie名称默认为： SESSIONID，可以通过park.session.cookie.name自定义

> 开启配置

```
@ImportAutoConfiguration(value = {
    ParkRedisSessionConfiguration.class
})
@SpringBootApplication
public class DemoApplication {
    public static void main(String[] args) {
        SpringApplication.run(DemoApplication.class, args);
    }
}
```

