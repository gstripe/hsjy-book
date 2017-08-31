![![](cn/park/images/new_project_maven_add_archetype.pn](cn/park/images/new_project_maven_add_archetype.png)g)# 创建服务工程

## 配置alpaca-service-archetype的Maven坐标

- ### IntelliJ IDEA

1. 打开IDEA菜单：File/New/Project...

2. 进入New Project：在左侧选择Maven，勾选Create from archetype

3. 点击Add Archetype...按钮

4. 在输入框输入对应的坐标

    ```
    <dependency>
      <groupId>alpaca.service</groupId>
      <artifactId>alpaca-service-archetype</artifactId>
      <version>0.0.1-RELEASE</version>
    </dependency>
    ```
5. 点击OK，如图所示说明archetype添加成功
![image](/cn/park/images/new_project_maven_add_archetype.png)

- ### Spring Tool Suite
    
    略

## 使用alpaca-service-archetype创建

- ### IntelliJ IDEA

1. 打开IDEA菜单：File/New/Project...

2. 进入New Project：在左侧选择Maven，勾选Create from archetype

3. 选择alpaca-service-archetype:0.0.1-RELEASE

4. 点击Next

5. 在GroupId项里输入 alpaca.service

6. 在ArtifactId项里输入 service-example

7. 在Version项里输入 0.0.1-SNAPSHOT

8. 点击Next

9. 在Properties属性格中添加一个新的属性Name项:package与Value项:alpaca.service.example，如下图所示：

![image](/cn/park/images/new_project_maven_add_package.png)

10. 点击Next

11. Project name项修改成service-example，顺便在More Settings修改要放置该工程的路径，如下图所示：

![image](/cn/park/images/new_project_more_settings.png)

12. 点击Finish，打开新窗口，开始通过archetype进行项目的生成，如果在右下角有弹出Maven projects need to be imported的提示，请点击其中任何一个选项

13. 工程创建完毕之后，可以看到Message Maven Goal窗口下最后打印出如下信息即为创建成功

    ```
    [INFO] ------------------------------------------------------------------------
    [INFO] BUILD SUCCESS
    [INFO] ------------------------------------------------------------------------
    [INFO] Total time: 26.164 s
    [INFO] Finished at: 2017-08-28T14:35:09+08:00
    [INFO] Final Memory: 15M/247M
    [INFO] ------------------------------------------------------------------------
    [INFO] Maven execution finished
    ```

14. 最终项目结构如下：

![image](/cn/park/images/project_info.png)

