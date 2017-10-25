> 集成平台单点登录整合

与 Spring Boot 工程整合

> 依赖包

```
<dependency>
    <groupId>alpaca.park</groupId>
    <artifactId>park-starter-sso-euler</artifactId>
    <version>0.0.1-SNAPSHOT</version>
</dependency>
```

> yml配置项

```
park:
  sso:
    euler:
      enabled: true
      session-name: PARK_SESSION_NAME
      order: 1
      includes: /*
      excludes: '*.css,*.js,*.eot,*.svg,*.woff,*.woff2,*.png,*.gif,*.jpg,*.jpeg'
      server: http://192.168.2.70/main
```

> 配置项说明

park.sso.euler.enabled: # ture/false 是否开启sso过滤器， 默认false
park.sso.euler.session-name: # 自定义会话名，默认PARK_SESSION_NAME
park.sso.euler.order: # 过滤器顺序，默认1
park.sso.euler.includes: # 需要经过过滤器的地址，默认/\*
park.sso.euler.excludes: # 不需要经过过滤器的，默认如上配置项，注意\*号开头的需要用两个半角单引号包括
park.sso.euler.server: # 单点登录服务器地址，如果有配置则使用，没有配置则使用集成平台传递的地址

> 使用注解开启单点过滤器配置

```
@EnableParkSsoEulerFilter
@SpringBootApplication
public class DemoApplication {
    public static void main(String[] args) {
        SpringApplication.run(DemoApplication.class, args);
    }
}
```

