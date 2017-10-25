> 在Spring Boot的异常格式上进行改造

统一异常信息定义
仅替换掉SpringBoot默认的错误信息格式，目前不修改默认的异常行为

> 依赖包

```
<dependency>
    <groupId>alpaca.park</groupId>
    <artifactId>park-starter-error-attributes</artifactId>
    <version>0.0.1-SNAPSHOT</version>
</dependency>
```

> yml配置项

```
server:
  error:
    include-stacktrace: always # 返回的错误信息包含堆栈内容
park.error.enabled: true
```

> 配置项说明

只要设置为true就会直接替换掉原来的异常格式

> 开启配置

```
@ImportAutoConfiguration(value = {
    ParkErrorMvcConfiguration.class
})
@SpringBootApplication
public class DemoApplication {
    public static void main(String[] args) {
        SpringApplication.run(DemoApplication.class, args);
    }
}
```




