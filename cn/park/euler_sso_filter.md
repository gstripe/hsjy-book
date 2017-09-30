# 集成平台单点登录整合

* 与 Spring Boot 工程整合

* 导入相关依赖包


```
<dependency>
    <groupId>alpaca.park</groupId>
    <artifactId>alpaca-park-common</artifactId>
    <version>0.0.1-RELEASE</version>
</dependency>
<!-- 集成平台 SSO 需要用到的 依赖包-->
<!-- 增加LocalSession实现序列化接口与默认构造函数 -->
<!-- 整合集成平台单点登录 -->
<dependency>
    <groupId>alpaca.park</groupId>
    <artifactId>park-euler</artifactId>
    <version>2.3.4</version>
</dependency>
```

* 应用主入口配置注解

> 导入自动配置类EulerSessionFilterConfiguration.class

```
@SpringBootApplication
@ImportAutoConfiguration(value = {
    EulerSessionFilterConfiguration.class
})
public class ManagerApplication {

    public static void main(String[] args) {
        SpringApplication.run(ManagerApplication.class, args);
    }

}
```
> 注意，目前EulerSessionFilter尚未实现实际的业务代码，仅仅返回一个LocalSession

* application.yml配置


```
park:
  euler:
    sso:
      enabled: true # 开启集成平台的SSO过滤器
      order: 1 # 过滤器排序 默认值：1
      filter-url: /manager/* # 需要进行过滤的地址，默认值：/
      exclude-urls: *.css,*.js,*.html,*.eot,*.svg,*.woff,*.woff2,*.png,*.gif,*.jpg,*.jpeg # 不经过过滤器的内容
      server: http://192.168.2.119:9080/main
```

> 其他配置说明：
> .server 配置集成平台的单点登录地址，通常是从直接从集成平台的_ssoServer携带过来，如果进行配置则使用配置的内容，例如使用在nginx环境下

