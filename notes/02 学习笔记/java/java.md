## java 简介
Java SE 是标准版，包含标准的 JVM 和标准库
Java EE 是企业版，是在 Java SE 的基础上加上了大量的 API 和库，以便方便开发 Web 应用、数据库、消息服务等

JDK：Java Development Kit，只有 Java 源码，要编译成 Java 字节码，需要使用 JDK，因为JDK除了包含JRE，还提供了编译器、调试器等开发工具。
JRE：Java Runtime Environment，运行 Java 字节码的虚拟机

### JAVA_HOME 的 bin 目录下的可执行文件：
java：这个可执行程序其实就是JVM，运行Java程序，就是启动JVM，然后让JVM执行指定的编译后的代码；
javac：这是Java的编译器，它用于把Java源码文件（以.java后缀结尾）编译为Java字节码文件（以.class后缀结尾）；
jar：用于把一组.class文件打包成一个.jar文件，便于发布；
javadoc：用于从Java源码中自动提取注释并生成文档；
jdb：Java调试器，用于开发阶段的运行调试。

## java 程序
```java
public class Hello{
    public static void main(String[] args){ // 定义的 main 方法，里面有一个参数 args，类型是 String[]
        System.out.println("Hello, world!");
    }
}
```
Java源码本质上是一个文本文件，需要先用 javac 把 Hello.java 编译成字节码文件 Hello.class，然后再用 java 命令执行这个字节码文件：
```sh
$ javac Hello.java
$ java Hello # 执行的是 Hello.class
```
java11 之后可以只用 java Hello.java 来执行一个 java 文件

## 数据类型
### 基本数据类型
基本数据类型是 CPU 可以直接进行运算的类型。
1. 整数类型：byte（1个字节），short（2），int（4），long（8，结尾需要加L）,注意整数计算时如果溢出不会报错，但会得到奇怪的结果
2. 浮点数类型：float（4，结尾需要加f），double（8）
3. 字符类型：char（2），注意char类型使用单引号'，且仅有一个字符，要和双引号"的字符串类型区分开。
4. 布尔类型：boolean

Java在内存中使用Unicode表示字符，因此一个英文字符和一个中文字符都用一个char类型表示，它们都占用两个字节。要显示一个字符的Unicode编码，只需将char类型直接赋值给int类型即可

### 引用数据类型
引用类型的变量类似于 C 语言的指针，它内部存储一个“地址”，指向某个对象在内存的位置
String 用双引号"..."表示字符串，一个字符串可以存储0个到任意个字符

如果用+连接字符串和其他数据类型，会将其他数据类型先自动转型为字符串，再连接：

字符串可以用"""..."""表示多行字符串

### 数组
int[] ns = new int[5];
int[] ns = { 68, 79, 91, 85, 62 };

### 常量
使用 final 修饰词，常量名通常全部大写，如：final double PI = 3.14;

## 运算
++写在前面和后面计算结果是不同的，++n 表示先加 1 再引用 n，n++ 表示先引用 n 再加 1。

## 流程控制
格式化输出使用System.out.printf()，通过使用占位符%?，printf()可以把后面的参数格式化成指定格式：
```java
double d = 3.1415926;
System.out.printf("%.2f\n", d); // 显示两位小数3.14
```

%d：格式化输出整数
%x：格式化输出十六进制整数
%f：格式化输出浮点数
%e：格式化输出科学计数法表示的浮点数
%s：格式化字符串

## 命令行参数
main方法可以接受一个命令行参数，它是一个String[]数组。这个命令行参数由JVM接收用户输入并传给main方法。
可以利用接收到的命令行参数，根据不同的参数执行不同的代码。
```java
public class Main {
    public static void main(String[] args) {
        for (String arg : args) {
            if ("-version".equals(arg)) {
                System.out.println("v 1.0");
                break;
            }
        }
    }
}
```

## 面向对象编程
在方法内部，可以使用一个隐含的变量 this，它始终指向当前实例。因此，通过 this.field 就可以访问当前实例的字段。
如果没有命名冲突，可以省略 this，但如果有局部变量和字段重名，那么局部变量优先级更高，就必须加上 this。

### 构造方法
创建实例时实际上是通过构造方法来初始化实例的
构造方法的名称是类名，参数没有限制，构造方法没有返回值（也没有void），调用构造方法，必须用 new 操作符。
```java
public class Main {
    public static void main(String[] args) {
        Person p = new Person("Xiao Ming", 15);
        System.out.println(p.getName());
    }
}
class Person {
    private String name;
    private int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
    public String getName() {
        return this.name;
    }
}
```
如果没有显式的创建构造方法，编译器会自动生成一个默认构造方法，它没有参数，也没有执行语句；如果有显式创建，则编译器不会自动生成默认构造方法
没有在构造方法中初始化字段时，引用类型的字段默认是null，数值类型的字段用默认值，int类型默认值是0，布尔类型默认值是false

java中创建对象实例的初始化顺序：
1. 先初始化字段，如 int age = 10;表示字段初始化为10，double salary;表示字段默认初始化为0，String name;表示引用类型字段默认初始化为null；
2. 执行构造方法的代码进行初始化。

### 重载与重写
Overload：方法名相同，但各自的参数不同，称为方法重载，方法重载的返回值类型通常都是相同的
Override：在继承关系中，子类如果定义了一个与父类方法签名完全相同的方法，被称为重写。在方法重写前加上 @Override

### 继承
超类、父类、基类；子类，扩展类
Java中，没有明确写extends的类，编译器会自动加上extends Object。所以，任何类，除了Object，都会继承自某个类，一个类有且仅有一个父类

子类无法访问父类的private字段或者private方法，可以将父类中的字段或方法改为 protect 修饰，从而被子类访问
protected关键字可以把字段和方法的访问权限控制在继承树内部，一个protected字段和方法可以被其子类，以及子类的子类所访问，后面我们还会详细讲解。

子类不会继承任何父类的构造方法。子类默认的构造方法是编译器自动生成的，不是继承的。

#### super
super关键字表示父类（超类）。子类引用父类的字段时，可以用super.fieldName。

必须使用 super 的场景：
如果父类没有默认的构造方法，子类就必须显式调用super()并给出参数以便让编译器定位到父类的一个合适的构造方法。

### 多态
多态是指，针对某个类型的方法调用，其真正执行的方法取决于运行时期实际类型的方法。





## Idea文件夹类型
1. Source roots：通过将文件夹指定为这种类别，来告诉IntelliJ IDEA，这个文件夹和它的子文件夹中包含源码，在构建工程时，需要作为一部分被编译进去。
2. Test source roots：这个类型的文件夹与sources root类似，都是用于存放源码，不过是测试的源码（比如单元测试）。test sources root 文件夹可以帮助你将测试代码和产品代码分离开。通常sources root和test sources root的编译结果被放在不同的文件夹中。
3. Resource roots： 存放你的应用中需要用到的资源文件（如：图片、xml或者properties配置文件等）
4. Test resource roots：存放和test resources关联的资源文件
5. Excluded roots：几乎被忽略的。为排除的文件夹中的文件提供了非常有限的编码帮助。



## jar包
jar 文件是一种压缩的文件包，包含了一个名为 META-INF/MANIFEST.MF 的清单文件，该文件是打 jar 包时自动生成的。

用途：将 jar 包提供给他人使用时，对方只需在 CLASSPATH 环境变量中添加 jar 包，则 java 虚拟机就可以在内存中解析该 jar 包了，java 虚拟机会根据路径查找相应的文件，从而进行使用。
优点：体积小、安全、可移植性强、封装好等

jar cvf test.jar test： 将 test 目录打包成一个 test.jar 包
jar xvf test.jar： 解压 test.jar 
jar uvf test.jar Hello.class： 更新 test.jar 中的 Hello.class 文件，若不存在则添加该文件
jar -tf test.jar： 查看 test.jar 文件结构

### 可执行jar包
main 函数是 java 程序执行的入口，因此，可执行 jar 包是某个 .class 文件中提供了 main 函数，但一个 jar 包中可能包含多个 main 函数，可以通过 MANIFEST.MF 文件的的 Main-Class 属性来指定 jar 包的执行入口

java -jar test.jar： 运行可执行 jar 包

MANIFEST.MF 包含了该 jar 包的版本、创建人和类搜索路径 Class-Path 等信息，可执行 jar 包有 Main-Class 属性


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

