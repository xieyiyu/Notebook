## 插件在 IDEA 中未安装
比如 WosItemLine::getItemOrderLine 这种调用 WosItemLine 的构造函数 getItemOrderLine
但是使用 ctrl+左键 无法进行跳转
查看 WosItemLine 类，发现使用了 import lombok.Data;
需要在 IDEA 中安装 lombok 插件方可使用：https://blog.csdn.net/qq_31496897/article/details/77970043

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

