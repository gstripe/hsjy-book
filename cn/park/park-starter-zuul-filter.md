> 集成平台单点登录整合

与 Spring Boot 工程整合

> 依赖包

```
<dependency>
    <groupId>alpaca.park</groupId>
    <artifactId>park-starter-zuul-filter</artifactId>
    <version>0.0.1-SNAPSHOT</version>
</dependency>
```

> yml配置项

```
park.zuul.filter.enabled: true
park.zuul.filter.bean: euler
park.zuul.filter.euler.sso-server: http://192.168.2.70/main
```

> 配置项说明

TODO


> 使用注解开启单点过滤器配置

```
@EnableZuulProxy
@EnableFeignClients
@EnableDiscoveryClient
@EnableCircuitBreaker
@EnableParkZuulFilter
@SpringBootApplication
public class GatewayApplication {
    public static void main(String[] args) {
        SpringApplication.run(GatewayApplication.class, args);
    }
}
```

