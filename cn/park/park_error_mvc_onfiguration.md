# 统一异常

仅替换掉SpringBoot默认的错误信息格式，目前不修改默认的异常行为

* 依赖包


```
<dependency>
    <groupId>alpaca.park</groupId>
    <artifactId>alpaca-park-common</artifactId>
    <version>0.0.1-RELEASE</version>
</dependency>
```

* 应用主入口配置注解
> 导入自动配置类ParkErrorMvcConfiguration.class
> ParkErrorAttributes为我们自定义内容格式，直接复制DefaultErrorAttributes进行修改。
> 修改内容目前为：
>  * 修改errors的格式，这里获取比较简单的错误信息即可 比如 字段名 跟错误提示信息 与错误内容：{ "field" : "divisor", "value" : "1.0", "message" : ""  }
   * 添加Sleuth的跟踪相关id内容（如果有引入sleuth包，并开启跟踪功能。）

```
@SpringBootApplication
@ImportAutoConfiguration(value = {
    ParkErrorMvcConfiguration.class
})
public class ManagerApplication {

    public static void main(String[] args) {
        SpringApplication.run(ManagerApplication.class, args);
    }

}

```


* 配置文件
```
server:
  error:
    include-stacktrace: always # 返回的错误信息包含堆栈内容
  park: true # 使用我们自己的错误信息格式
```

