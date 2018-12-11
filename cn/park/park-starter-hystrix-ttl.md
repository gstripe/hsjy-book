> Hystrix隔离策略为默认的时候（thread），ThreadLocal内容丢失的处理

这里使用transmittable-thread-local来解决跨线程传递的丢失内容的问题


```
        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>transmittable-thread-local</artifactId>
            <version>2.10.2</version>
        </dependency>
```

