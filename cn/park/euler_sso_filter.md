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
<!-- sysd-euler重新编译版 -->
<!-- 增加LocalSession实现序列化接口与默认构造函数 -->
<dependency>
    <groupId>com.icsshs</groupId>
    <artifactId>sysd-euler</artifactId>
    <version>2.4.3</version>
    <exclusions>
        <exclusion>
            <artifactId>*</artifactId>
            <groupId>*</groupId>
        </exclusion>
    </exclusions>
</dependency>
<dependency>
    <groupId>net.sf.ezmorph</groupId>
    <artifactId>ezmorph</artifactId>
    <version>1.0.6</version>
</dependency>
<dependency>
    <groupId>net.sf.json-lib</groupId>
    <artifactId>json-lib</artifactId>
    <version>2.4</version>
    <classifier>jdk15</classifier>
</dependency>
<dependency>
  <groupId>org.apache.httpcomponents</groupId>
  <artifactId>httpclient</artifactId>
  <version>4.5.3</version>
</dependency>
```
> 其他如commons-lang3、commons-collections没有的话自行引入

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
# 开启集成平台的SSO过滤器
park.euler.sso.enabled: true
# 需要进行过滤的地址，默认值：/*
park.euler.sso.filter-url: /manager/*
# 过滤器排序 默认值：1
park.euler.sso.order: 1
# 不经过过滤器的内容
# 默认值：*.css,*.js,*.html,*.eot,*.svg,*.woff,*.woff2,*.png,*.gif,*.jpg,*.jpeg
# park.euler.sso.exclude-urls:
```


