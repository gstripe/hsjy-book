# 服务工程结构说明

## 项目结构预览

![](/cn/park/images/service_project_structure.png)

## 项目结构详解

* ### ServiceMainApplication
> Spring Boot 应用启动类
    
    ```
    @EnableSwagger2Doc // 默认使用swagger做为api文档
    @EnableDiscoveryClient // 默认为一个服务实例
    @SpringBootApplication // 一个SpringBoot应用的固定声明
    @MapperScan("alpaca.service.example.mapper") // 扫描Mybatis Mapper
    public class ServiceMainApplication {
    
        // 通过java -jar xxx.jar 启动服务
        public static void main(String[] args) {
            SpringApplication.run(ServiceMainApplication.class, args);
        }
    }
    ```

* ### controller
> 服务接口层，写法遵循Spring MVC的Controller写法
> 注意：接口返回值请勿与例子一样写Object，不方便阅读
> AccountController的findByUsername的请求将会映射为：
> GET http://ip:port/account/admin

    ```
    @RestController // 相当于 @Controller与@ResponseBody 统一返回json格式的内容
    @RequestMapping("account")
    public class AccountController {
    
        @Autowired
        private AccountService accountService; // 注入一个service层的类
    
        @GetMapping("{username}")
        public Object findByUsername(@PathVariable(value = "username") String username) {
            return accountService.findByUsername(username);
        }
    
        @PostMapping("")
        public Object saveAccount(@RequestBody Account account) {
            // 加密一下密码
            String password = account.getPassword();
            password = new BCryptPasswordEncoder().encode(password);
            account.setPassword(password);
            int row = accountService.save(account);
            return row == 1 ? true : false;
        }
    
    }
    ```

* ### entity
> 有Mybatis Generator生成的单表实体，这里我们使用的是tk通用Mapper的生成器生成的带有JPA注解的实体

* ### mapper
> 生成的通用Mapper接口，这里规定有生成器生成的接口不添加任何接口方法，如果需要添加新的接口方法，则自定义一个Mapper

* ### service
> service层，操作Mapper的类，实现业务逻辑，控制数据库事务，缓存相关等。

    ```
    @Service
    public class AccountService extends AlpacaService<Account>{
    
        @SuppressWarnings("SpringJavaAutowiringInspection")
        @Autowired
        private AccountMapper accountMapper;
    
        @Transactional(readOnly = true)
        public Account findByUsername(String username) {
            Account record = new Account();
            record.setUsername(username);
            Account account = accountMapper.selectOne(record);
            return account;
        }
    
        public boolean exists(Long id) {
            Account record = new Account();
            record.setId(id);
            return accountMapper.selectCount(record) == 1 ? true : false;
        }
    
        @Transactional(readOnly = true)
        public Map findByIdToMap(Long id) {
            return accountMapper.selectByIdToMap(id);
        }
    
        @Transactional(readOnly = true)
        public Account findByIdToMap2(Long id) {
            return accountMapper.selectByIdToMap2(id);
        }
    
        @Transactional(readOnly = true)
        public Account findByIdToAccount(Long id) {
            return accountMapper.selectByIdToAccount(id);
        }
    
    }
    ```

