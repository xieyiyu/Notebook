# java注解
注解（Annotation）是放在 Java 源码的类、方法、字段、参数前的一种特殊“注释”
注解可以被编译器打包进入 class 文件，可以用作标注的“元数据”

## 注解分类
1. 由编译器使用的注解：不会被编译进入.class文件，在编译后被编译器丢弃
- @Override：编译器检查该方法是否是正确的重写方法。如果发现其父类，或者是引用的接口中并没有该方法时，会报编译错误。
- @SuppressWarnings：告诉编译器忽略此处代码产生的警告。

2. 由工具处理 .class 文件使用的注解，如有些工具会在加载class的时候，对class做动态修改，实现一些特殊的功能。这类注解会被编译进入.class文件，但加载结束后并不会存在于内存中。这类注解只被一些底层库使用，一般我们不必自己处理。

3. 最常用：在程序运行期能够读取的注解，它们在加载后一直存在于JVM中。例如，一个配置了@PostConstruct的方法会在调用构造方法后自动被调用（这是Java代码读取该注解实现的功能，JVM并不会识别该注解）。

## 注解参数
注解可以配置参数，没有指定配置的参数使用默认值，必须是常量
1. 所有基本类型；
2. String；
3. 枚举类型；
4. 基本类型、String、Class以及枚举的数组。

大部分注解会有一个名为value的配置参数，如果参数名称是value，且只有一个参数，那么可以省略参数名称。

## java 内置注解
作用在代码的注解
1. @Override
2. @SuppressWarnings
3. @Deprecated: 标记过时方法。如果使用该方法，会报编译警告

元注解：作用在其他注解的注解
1. @Retention - 标识这个注解怎么保存，是只在代码中，还是编入class文件中，或者是在运行时可以通过反射访问。
2. @Documented - 标记这些注解是否包含在用户文档中。
3. @Target - 标记这个注解应该是哪种 Java 成员。
4. @Inherited - 标记这个注解是继承于哪个注解类(默认 注解并没有继承于任何子类)

新增：
1. @SafeVarargs - Java 7 开始支持，忽略任何使用参数为泛型变量的方法或构造函数调用产生的警告。
2. @FunctionalInterface - Java 8 开始支持，标识一个匿名函数或函数式接口。
3. @Repeatable - Java 8 开始支持，标识某注解可以在同一个声明上使用多次。

### @Target
@Target可以定义Annotation能够被应用于源码的哪些位置：
1. 类或接口：ElementType.TYPE；
2. 字段：ElementType.FIELD；
3. 方法：ElementType.METHOD；
4. 构造方法：ElementType.CONSTRUCTOR；
5. 方法参数：ElementType.PARAMETER

定义注解@Report可用在方法或字段上：
```java
@Target({
    ElementType.FIELD,
    ElementType.METHOD     
})
public @interface Report{
    int type() default 0;
    String level() default "info";
    String value() default ""; }
```

### @Retention
@Retention 定义 Annotation 的生命周期
1. 仅编译期：RetentionPolicy.SOURCE；
2. 仅class文件：RetentionPolicy.CLASS；
3. 运行期：RetentionPolicy.RUNTIME
若 @Retention 不存在，则该 Annotation 默认 为CLASS。
通常自定义的 Annotation 都是RUNTIME，需要加上 @Retention(RetentionPolicy.RUNTIME) 这个元注解

### 



## lombok
### lombok使用
1. 引入相应的 maven 包
```xml
<!--模板代码自动编写工具-->
<dependency>
    <groupId>org.projectlombok</groupId>
    <artifactId>lombok</artifactId>
    <version>1.18.0</version>
    <scope>provided</scope>
</dependency>
```
Lombok 的 scope=provided，说明它只在编译阶段生效，不需要打入包中。
Lombok 在编译期将带 Lombok 注解的 Java 文件正确编译为完整的 Class 文件。

2. 添加IDE工具对Lombok的支持:https://blog.csdn.net/qq_31496897/article/details/77970043
开启 AnnocationProcessors 是为了让 Lombok 注解在编译阶段起到作用。

#### Lombok 注解的使用
1. @Data：作用于类上，是以下注解的集合：@ToString @EqualsAndHashCode @Getter @Setter @RequiredArgsConstructor

2. @Getter/@Setter: 作用类上，生成所有成员变量的getter/setter方法；作用于成员变量上，生成该成员变量的getter/setter方法。可以设定访问权限及是否懒加载等。

3. @ToString：作用于类，覆盖默认的toString()方法，可以通过of属性限定显示某些字段，通过exclude属性排除某些字段。

4. @EqualsAndHashCode：作用于类，覆盖默认的equals和hashCode

5. @RequiredArgsConstructor：生成包含final和@NonNull注解的成员变量的构造器；

```java
import lombok.Data;

@Data
public class WosItemLine {
    private Long id; //将自动生成 getId(), setId(Long) 方法
}
```

6. @Slf4j: 用作日志输出，
如果不想每次都写private  final Logger logger = LoggerFactory.getLogger(当前类名.class); 可以用注解@Slf4j
添加@Sl4j注解后，可以使用 log.info 打印日志

7. @Builder：建筑者模式，是现在比较推崇的一种构建值对象的方式。
1. 创建一个名为ThisClassBuilder的内部静态类，并具有和实体类形同的属性（称为构建器）。
2. 在构建器中：对于目标类中的所有的属性和未初始化的final字段，都会在构建器中创建对应属性。
3. 在构建器中：创建一个无参的default构造函数。
4. 在构建器中：对于实体类中的每个参数，都会对应创建类似于setter的方法，只不过方法名与该参数名相同。 并且返回值是构建器本身（便于链式调用）。
5. 在构建器中：一个build()方法，调用此方法，就会根据设置的值进行创建实体对象。
6. 在构建器中：同时也会生成一个toString()方法。
7. 在实体类中：会创建一个builder()方法，它的目的是用来创建构建器。

参考：https://km.sankuai.com/page/419441176