# 项目原型 - 快速创建项目

这个项目原型可以自动创建形如 [sample](https://github.com/guozilanTK/sample) 结构的项目。

并且这个项目是在 [sample](https://github.com/guozilanTK/sample) 空项目的基础上，通过下面命令创建的原型：

```
maven archetype:create-from-project
```

>在 sample 中执行该命令会生成一个原型项目，当前项目在生成的基础上做了一些简单的修改。

## 如何使用

>项目目前还没法传到 Maven 中央仓库，所以需要先在本地或者私服使用。

1. 下载本项目，然后通过 mvn install 安装到本地。

2. 打开 CMD，输入命令 `mvn archetype:generate -DarchetypeCatalog=local`，如下动画所示：

![create-project](https://user-images.githubusercontent.com/1787798/43684994-4f0f3ffc-98dd-11e8-83d8-d0ea5c3ddb0e.gif)

3. 创建的后项目结构如下：

```
└─user-demo
    ├─user-demo-api
    │  └─src
    │      └─main
    │          └─java
    ├─user-demo-controller
    │  └─src
    │      └─main
    │          └─java
    ├─user-demo-service
    │  └─src
    │      ├─main
    │      │  ├─java
    │      │  └─resources
    │      └─test
    │          ├─java
    │          └─resources
    └─user-demo-web
        └─src
            └─main
                └─webapp
```

4. 以 Maven 导入项目到 IDE

5. 修改 service 模块 src/test/resources 下面的 generatorConfig.xml 配置。

主要修改数据库连接和用户密码，然后修改下面 `<table>` ，改为自己需要的表即可。

改好代码生成器配置后，在 service 模块中执行命令（`mvn mybatis-generator:generate`），或者 IDEA 点击如下图所示插件：

![generator](https://user-images.githubusercontent.com/1787798/43685026-fdb19dc0-98dd-11e8-9be3-8169643a7500.png)

执行后即可生成针对单表的多个代码文件。

执行的部分日志如下：

```
[INFO] Introspecting table country
[INFO] Generating Record class for table country
[INFO] Saving file Country.java
[INFO] Saving file CountryService.java
[INFO] Saving file CountryServiceImpl.java
[INFO] Saving file CountryMapper.java
[INFO] Saving file CountryMapper.xml
[INFO] Saving file CountryController.java
[INFO] Saving file country-main.jsp
[WARNING] 没有配置 "templateFormatterClass" 模板处理器，使用默认的处理器!
[WARNING] 没有配置 "templateFormatterClass" 模板处理器，使用默认的处理器!
[WARNING] 没有配置 "templateFormatterClass" 模板处理器，使用默认的处理器!
[WARNING] 没有配置 "templateFormatterClass" 模板处理器，使用默认的处理器!
[WARNING] 没有配置 "templateFormatterClass" 模板处理器，使用默认的处理器!
[WARNING] 没有配置 "templateFormatterClass" 模板处理器，使用默认的处理器!
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time: 1.326 s
[INFO] Finished at: 2018-08-05T18:35:23+08:00
[INFO] Final Memory: 15M/215M
[INFO] ------------------------------------------------------------------------
```

所有文件都会生成到指定的目录中，如下图所示：

![file-generator](https://user-images.githubusercontent.com/1787798/43685055-7cf71f60-98de-11e8-81b3-cc5c91632d38.png)

6. 真实应用时，可以根据自己的业务逻辑编写对应的模板，直接生成符合自己需要的代码。