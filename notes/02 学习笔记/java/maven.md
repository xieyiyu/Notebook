## maven
maven 是基于项目对象模型（POM）概念，利用一个中央信息片断来管理一个项目的构建、报告和文档等步骤。可以对 Java 项目进行构建、依赖管理。

### Maven POM
POM.xml(Project Object Model，项目对象模型)是 Maven 工程的基本工作单元，包含了项目的基本信息，用于描述项目如何构建，声明项目依赖，版本等。
执行项目时，maven 在当前目录查找 POM，通过读取 POM 文件来获取所需配置，随后执行项目。

所有 POM 文件都需要 project 元素和三个必需字段：groupId，artifactId，version。
```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <!-- POM模型版本 -->
    <modelVersion>4.0.0</modelVersion>
    <!-- 公司或者组织的唯一标志，并且配置时生成的路径也是由此生成，如下 maven 会将该项目打成的 jar 包放本地路径：/com/sankuai/sjst -->
    <groupId>com.sankuai.sjst</groupId>
    <!-- 项目的唯一 ID，一个 groupId 下面可能多个项目，就是靠 artifactId 来区分的 -->
    <artifactId>m-dispatch</artifactId>
    <!-- 版本号 -->
    <version>2.12.1-SNAPSHOT</version>
    <!--该元素描述了项目相关的所有依赖。 这些依赖组成了项目构建过程中的一个个环节。它们自动从项目定义的仓库中下载。-->
    <dependencies>
        <!-- sso -->
        <dependency>
            <groupId>com.sankuai.it.sso</groupId>
            <artifactId>sso-java-sdk</artifactId>
        </dependency>
    </dependencies>
    <!--在列的项目构建profile，如果被激活，会修改构建处理 -->
    <profiles>
        <!--根据环境参数或命令行参数激活某个构建处理 -->
        <profile>
            <!--构建配置的唯一标识符。即用于命令行激活，也用于在继承时合并具有相同标识符的profile。 -->
            <id>test</id>
            <properties>
                <conf-dir>test</conf-dir>
            </properties>
        </profile>
        <profile>
            <id>stage</id>
            <properties>
                <conf-dir>stage</conf-dir>
            </properties>
        </profile>
        <profile>
            <id>prod</id>
            <properties>
                <conf-dir>prod</conf-dir>
            </properties>
        </profile>
    </profiles>
</project>
```

### maven 构建生命周期
|阶段|处理|描述|
|  ----  | ----  |
|validate    |	 验证   |	验证项目是否正确且所有必须信息是可用的|
|compile     |   执行	|   源代码编译在此阶段完成|
|Test	     |   测试   |   使用适当的单元测试框架（例如JUnit）运行测试|
|package     |   打包	|   创建JAR/WAR包如在 pom.xml 中定义提及的包|
|verify	     |   检查   |	对集成测试的结果进行检查，以保证质量达标|
|install	 |   安装   |	安装打包的项目到本地仓库，以供其他项目使用|
|deploy  	 |   部署	|   拷贝最终的工程包到远程仓库中，以共享给其他开发人员和工程|

maven 的三个标准生命周期（相互独立）：
1. clean：清理项目
2. default(或 build)：构建部署项目
3. site：建立项目站点

maven 的每个生命周期包含一些阶段（phase），这些阶段是有顺序的，并且后面的阶段依赖于前面的阶段。

clean 生命周期包含三个阶段： pre-clean、clean和 post-clean：
1. 调用 pre-clean，只有 pre-clean 阶段执行；
2. 调用 clean，pre-clean 和 clean 阶段会按顺序执行；
3. 调用 post-clean，pre-clean、clea n和 post-clean 都会按顺序执行；

通过 Maven 命令行来编译、测试和打包程序的命令，而这些命令其实就是完成了生命周期的操作。
比如 mvn clean 就是调用 clean 周期的 clean 阶段和 default 的 install 阶段，实际调用的是 pre-clean、clean 以及 validate 到 install 阶段

### maven 打包命令
使用 maven 构建 java 项目，常用的打包命令有 mvn clean package、mvn clean install 和 mvn clean deploy，三者都完成了项目编译、单元测试、打包功能，但区别在于包函的 maven 生命阶段和执行目标不同。
1. mvn clean package 依次执行了 clean、resources、compile、testResources、testCompile、test、jar ７ 个阶段，没有把打好的可执行 jar 包布署到本地 maven 仓库和远程 maven 私服仓库。
2. mvn clean install 依次执行了 clean、resources、compile、testResources、testCompile、test、jar、install 8 个阶段，同时将打好的可执行 jar 包布署到本地 maven 仓库，但没有布署到远程 maven 私服仓库。
3. mvn clean deploy 依次执行了 clean、resources、compile、testResources、testCompile、test、jar、install、deploy ９个阶段，同时将打好的可执行 jar 包布署到本地 maven 仓库和远程 maven 私服仓库。

### maven 插件
Maven 对工程的所有操作都是由插件完成的，一个插件可以支持多种功能，称之为目标（goal），每个构建步骤都可以绑定一个或者多个插件目标
每个 phase 都可以绑定一个或者多个插件目标来进行实现，phase 就相当于 Maven 提供的统一的接口。不绑定到任何 phase 的插件目标可以在构建生命周期之外通过直接调用执行。

执行插件：```mvn [plugin-name]:[goal-name]```

常用插件：
clean： 构建之后清理目标文件。删除目标目录。
compiler： 编译 Java 源文件。
surefile： 运行 JUnit 单元测试。创建测试报告。
jar： 从当前工程中构建 JAR 文件。
war： 从当前工程中构建 WAR 文件。
javadoc： 为工程生成 Javadoc。
antrun： 从构建过程的任意一个阶段中运行一个 ant 任务的集合。

### Snapshot 快照
Snapshot 是一种特殊的版本，指定了某个当前的开发进度的副本。不同于常规的版本，Maven 每次构建都会在远程仓库中检查新的快照，自动获取。

1、Snapshot 版本代表不稳定、尚处于开发中的版本。
2、Release 版本则代表稳定的版本。正式环境中不得使用 snapshot 版本的库

