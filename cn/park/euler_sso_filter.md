# 集成平台单点登录整合

* 相关依赖包


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
```

