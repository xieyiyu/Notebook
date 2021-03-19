# JAVA 基础
<!-- GFM-TOC -->
* [java 简介](#java-简介)
* [java 程序](#java-程序)
* [数据类型](#数据类型)
    * [基本数据类型](#基本数据类型)
    * [引用数据类型](#引用数据类型)
    * [数组](#数组)
    * [常量](#常量)
    * [java 集合类](#java-集合类)
        * [List 列表](#List-列表)
        * [Map 映射](#Map-映射)
        * [Set 集合](#Set-集合)
        * [Collections](#Collections)
* [运算](#运算)
* [流程控制](#流程控制)
* [命令行参数](#命令行参数)
* [面向对象编程](#面向对象编程)
    * [构造方法](#构造方法)
    * [重载与重写](#重载与重写)
    * [继承](#继承)
    * [多态](#多态)
    * [javabean](#javabean)
* [jar包](#jar包)
* [反射](#反射)
<!-- GFM-TOC -->

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

### java 集合类
Java 的集合类定义在 java.util 包中，支持泛型，主要提供了3种集合类，包括List，Set和Map。Collection是最基本的集合接口，声明了适用于 Set和List 的通用方法。

#### List 列表
List 中的对象有序，可以重复，允许按照对象在集中的索引位置检索对象。List和数组相似，但数据对于增删操作十分不方便，而 List 相当于是封装了添加和删除的操作，操作 List 时使用 add() 或 remove() 方法十分方便，不用关注内部元素的移动。

List 有两种实现：ArrayList（数组） 和 LinkedList（链表），一般都是使用 ArrayList
1. 获取指定元素：ArrayList 速度很快，而 LinkedList 需要从头开始查找元素
2. 添加元素到末尾：两者都很快，效率相同
3. 在指定位置添加/删除：ArrayList 需要移动元素，而 LinkedList 不需要移动元素
4. 内存占用：ArrayList 较少，而 LinkedList 较大

```java
List<String> list = new ArrayList<>();
list.add('1');
list.add(null); // 允许添加 null，注意不是引号
list.get(1) // 获取指定索引的元素，得到 null
list.size() // 获取列表长度，2 ['1', null]
for (int i=0; i<list.size(); i++){
    System.out.println(list.get(i)); // 遍历数组，但使用 get() 方法只对 ArrayList 的实现是高效的
}
//最好用 for each 进行遍历，只要实现了 Iterable 接口的集合类都可以用 for each 进行遍历
for (String s : list){
    System.out.pringln(s);
}
```

#### Map 映射
Map 中每个元素包含一对键对象和值对象，没有重复的键对象，值对象可以重复，它的有些实现类能对集合中的键对象进行排序。
直接用 Map 遍历输出是无序的
```java
Map<String, Integer> map = new HashMap<>();
map.put("Bob", 20); // 调用 put(K key, V value) 方法，把 key 和 value 做了映射并放入 Map 中
map.put("Lily", 24);
map.containsKey("Bob"); // True; 调用 boolean containsKey(K key) 方法判断一个 key 是否在 Map 中存在
// 遍历 map, 使用 for each 循环遍历 Map 对象的 entrySet() 集合，它包含每一个 key-value 映射
for(Map.Entry<String, Integer> entry : map.entrySet()){
    String key = entry.getKey();
    Integer value = entry.getValue();
}
```

正确使用 Map 必须保证：
1. 作为 key 的对象必须正确覆写 equals() 方法，相等的两个 key 实例调用 equals() 必须返回 true；我们常用的 key 是 String 类，已经在 java 内覆写了 equals() 方法，但如果 key 是自己写的一个类，就必须保证在这个类里正确覆写了 equals() 方法

2. 作为 key 的对象还必须正确覆写 hashCode()方法，且 hashCode() 方法要严格遵循以下规范：
    - 如果两个对象相等，则两个对象的 hashCode() 必须相等；
    - 如果两个对象不相等，则两个对象的 hashCode() 尽量不要相等。

提高程序效率的技巧：
1. 若 Map 的 key 是 enum 类型，推荐使用 EnumMap，既保证速度，也不浪费空间。
```java
Map<DayOfWeek, String> map = new EnumMap<>(DayOfWeek.class);
```

#### TreeMap
TreeMap 在内部会对 Key 进行排序，保证遍历时以 Key 的顺序来进行排序。
使用 TreeMap 时，放入的 Key 必须实现 Comparable 接口。String、Integer 这些类已经实现了 Comparable 接口，因此可以直接作为 Key 使用。
若作为 Key 的 class 没有实现 Comparable 接口，则必须在创建 TreeMap 的同时指定一个自定义排序算法。

### Set 集合
Set 中的对象无序，不重复，但它有些实现类中的对象可以按特定方式排序。
Set 常用于去重，最常用的 Set 实现类是 HashSet，实际上，HashSet 仅仅是对 HashMap 的一个简单封装
```java
Set<String> set = new HashSet<>()
```

### Collections
Collections是JDK提供的工具类，同样位于java.util包中。它提供了一系列静态方法，能更方便地操作各种集合。（注意多个s）
```java
import java.util.*;
Collections.sort(list); //排序
Collections.shuffle(list); //洗牌，打乱列表顺序
```

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

### javabean
javabean 是一个遵循特定写法的Java类，实际是一种规范，表达实体和信息的规范，便于封装重用
1、这个类必须具有一个公共的(public)无参构造函数；
2、所有属性私有化（private）；
3、私有化的属性必须通过public类型的方法（getter和setter）暴露给其他程序，并且方法的命名也必须遵循一定的命名规范。 
4、这个类应是可序列化的。实现Serializable 接口，用于实现bean的持久性

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


## 反射
- 反射 Reflection，是指在程序运行时才知道要操作的类是什么，并且可以在运行时获取类的完整构造，并调用对应的方法。能够动态的获取信息以及动态调用对象的方法，
- 正射：Apple apple = new Apple(); //直接初始化，在使用某个类时就知道它是什么类，是用来做什么的

在反射中，要获取一个类或调用一个类的方法，我们首先需要获取到该类的 Class 对象。如下面的 Class.forName(类路径)
```java
public class Apple {
    private int price;
    public int getPrice() {
        return price;
    }
    public void setPrice(int price) {
        this.price = price;
    }

    public static void main(String[] args) throws Exception{
        //正常的调用
        Apple apple = new Apple();
        apple.setPrice(5);
        System.out.println("Apple Price:" + apple.getPrice());

        //使用反射调用
        Class clz = Class.forName("com.myproject.api.Apple"); //1. 获取类的 Class 对象实例，知道类的全路径名时可以用 forName
        Method setPriceMethod = clz.getMethod("setPrice", int.class); 
        Constructor appleConstructor = clz.getConstructor(); //2. 根据 Class 对象实例获取 Constructor 对象
        Object appleObj = appleConstructor.newInstance(); //3. 使用 Constructor 对象的 newInstance 方法获取反射类对象
        setPriceMethod.invoke(appleObj, 14); // 利用 invoke 方法调用方法
        Method getPriceMethod = clz.getMethod("getPrice"); 
        System.out.println("Apple Price:" + getPriceMethod.invoke(appleObj));
    }
}
```

反射机制很重要的一点就是“运行时”，其使得我们可以在程序运行时加载、探索以及使用编译期间完全未知的 .class 文件。换句话说，Java 程序可以加载一个运行时才得知名称的 .class 文件，然后获悉其完整构造，并生成其对象实体、或对其 fields（变量）设值、或调用其 methods（方法）。

## 文件读写IO
- java.io 同步IO是指，读写IO时代码必须等待数据返回后才继续执行后续代码，优点是代码编写简单，缺点是CPU执行效率低。
- java.nio 异步IO是指，读写IO时仅发出请求，然后立刻执行后续代码，优点是CPU执行效率高，缺点是代码编写复杂。

java.io 
字节流接口：InputStream/OutputStream，以 byte 为单位读取；文件的实现类为：FileInputStream、FileOutputStream
字符流接口：Reader/Writer，以 char 为单位读取；文件的实现类为：FileReader和FileWriter

```java
File f = new File('/user/xieyiyu'); // f为一个目录
File[] fs = f.listFiles();  // 列出目录 f 下的所有文件和子目录
```

### InputStream
提供数据的基础 InputStream：
1、 FileInputStream：从文件读取数据，是最终数据源
2、 ByteArrayInputStream：
3、 ServletInputStream：从HTTP请求读取数据，是最终数据源

提供额外附加功能的 InputStream：
1、 BufferedInputStream：缓冲功能
2、 DigestInputStream：计算签名功能
3、 CipherInputStream：加密/解密功能

如果想给一个基础 InputStream 附加额外的功能时，比如为 FileInputStream 提供缓冲的功能来提高读取的效率，可以用 BufferedInputStream 来包装 这个InputStream，得到的包装类型是 BufferedInputStream，但它仍然被视为一个 InputStream：
```java
InputStream file = new FileInputStream("filename.txt");
InputStream buffered = new BufferedInputStream(file)；
```

以上这种通过一个“基础”组件再叠加各种“附加”功能组件的模式，被称为 Filter 模式（或者装饰器模式：Decorator），可以让我们通过少量的类来实现各种功能的组合。

### Reader
Reader/Writer 是字符流接口，以 char 为单位进行读取。

1. InputStream 是字节输入流的所有类的超类，一般我们使用它的子类, 如 FileInputStream 等。一次读取一个 byte，最低级
2. InputStreamReader 是字节流通向字符流的桥梁，可以将字节流转换为字符流。一次读取一个字符，较高级
3. BufferedReader 是由 Reader 类扩展而来，提供通用的缓冲方式文本读取，可以使用 readLine 方法读取一个文本行，
优势：从字符输入流中读取文本，缓冲各个字符，从而提供字符、数组和行的高效读取。最高级
```java
import java.io.*;
class IOdemo{
    public static String readFile(){
        StringBuffer stringBuffer = new StringBuffer();
        try{
            FileInputStream fileInputStream = new FileInputStream('/user/xieyiyu/myfile.txt'); //读取文件中的数据，字节流
            InputStreamReader inputStreamReader = new InputStreamReader(fileInputStream, "utf-8"); // 将字节流转换为字符流
            BufferedReader bufferedReader = new BufferedReader(inputStreamReader); // 创建字符流缓冲区

            string tmpString;
            while((tmpString = bufferedReader.readline()) != null){
                stringBuffer.apped(tmpString);
            }
            bufferedReader.close()
        } catch(IOException exp){
            exp.printStackTrace();
        }
    }
    return stringBuffer.tostring();
}
```
