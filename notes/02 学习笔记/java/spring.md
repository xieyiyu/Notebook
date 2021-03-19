# spring
定义：Spring是一个轻量级控制反转IoC和面向切面AOP的容器框架。

体系结构：Spring由20多个模块组成，它们可以分为数据访问/集成（Data Access/Integration）、Web、面向切面编程（AOP, Aspects）、应用服务器设备管理（Instrumentation）、消息发送（Messaging）、核心容器（Core Container）和测试（Test）。 

特点：
1. 非侵入式 
所谓非侵入式是指，Spring框架的API不会在业务逻辑上出现，即业务逻辑是POJO（Plain Old Java Objects）。由于业务逻辑中没有Spring的API，所以业务逻辑可以从Spring框架快速的移植到其他框架，即与环境无关。

2. 容器 
Spring作为一个容器，可以管理对象的生命周期、对象与对象之间的依赖关系。可以通过配置文件，来定义对象，以及设置与其他对象的依赖关系。  

3. IoC 
控制反转（Inversion of Control），即创建被调用者的实例不是由调用者完成，而是由Spring容器完成，并注入调用者。 
当应用了IoC，一个对象依赖的其它对象会通过被动的方式传递进来，而不是这个对象自己创建或者查找依赖对象。即，不是对象从容器中查找依赖，而是容器在对象初始化时不等对象请求就主动将依赖传递给它。 

4. AOP 
面向切面编程（AOP，Aspect Orient Programming），是一种编程思想，是面向对象编程OOP的补充。允许通过分离应用的业务逻辑与系统级服务（例如日志和事务管理）进行开发。应用对象只实现它们应该做的——完成业务逻辑——仅此而已。它们并不负责其它的系统级关注点，例如日志或事务支持。 

我们可以把日志、安全、事务管理等服务理解成一个“切面”，那么以前这些服务一直是直接写在业务逻辑的代码当中的，这有两点不好：首先业务逻辑不纯净；其次这些服务被很多业务逻辑反复使用，完全可以剥离出来做到复用。那么AOP就是这些问题的解决方案，可以把这些服务剥离出来形成一个“切面”，以期复用，然后将“切面”动态的“织入”到业务逻辑中，让业务逻辑能够享受到此“切面”的服务。 

功能：
Spring的IOC和AOP两大核心功能可以大大降低应用系统的耦合性、简化开发流程。
Spring框架技术可在不同层次上起作用，比如IOC管理普通的POJO对象、AOP增强了系统服务和其它组件（事务、MVC、JDBC、ORM和远程调用等）。Spring的一大特点就是基于接口编程，它是非侵入式的服务。用户端绑定接口使用JAVA EE服务，而非直接绑定服务，而且应用也可以使用不同的服务（Hibernate、MyBatis等）。我们可以根据自己的需要，使用Spring的一部分服务，而不必使用完整的Spring系列项目。 

## 控制反转 IOC
IoC：是指由spring来负责控制对象的生命周期和对象间的关系。
所有的类都会在spring容器中登记，告诉spring你是个什么东西，你需要什么东西，然后spring会在系统运行到适当的时候，把你要的东西主动给你，同时也把你交给其他需要你的东西。所有的类的创建、销毁都由 spring来控制，也就是说控制对象生存周期的不再是引用它的对象，而是spring。对于某个具体的对象而言，以前是它控制其他对象，现在是所有对象都被spring控制，所以这叫控制反转。

传统编程和IoC的对比
1.传统编程：决定使用哪个具体的实现类的控制权在调用类本身，在编译阶段就确定了。
2.IoC模式：调用类只依赖接口，而不依赖具体的实现类，减少了耦合。控制权交给了容器，在运行的时候才由容器决定将具体的实现动态的“注入”到调用类的对象中。

## 依赖注入 DI
IoC的一个重点是在系统运行中，动态的向某个对象提供它所需要的其他对象。这一点是通过DI（Dependency Injection，依赖注入）来实现的。

## spring 注解
Spring 的 IOC 会将Bean初始化加载到容器中，可以使用 Spring 注解方式或者 Spring XML 配置方式将 Bean 加载到容器中
### 组件类注解
spring作用在类上的注解（有@Component，@Service，@Controller等），都表明这些类是要交给spring容器管理，相当于自动给我们创建了一个bean即注解方式，不用我们手动的配置bean了（如果@Service不指定名称，默认为Bean的id为类名首字母大写，如果这样写@Service（”itemServiceImpl”）相当于给这个类起了个别名，bean的id即是itemServiceImpl,方便注入到别的类中，如下面的暴露服务时用的ref就是@Service的别名或类名首字母小写；通常使用getBean（“bean的id名”）也会用到）；

org.springframework.stereotype.Service 注解
@Service 用于标注业务层组件，主要进行业务的处理（通常定义在servic层）

其他注解：
1. @Controller：用于标注控制层组件（如Struts的action，springMVC的controller），前端交互的控制层
2. @Repository：用于标注数据访问层 DAO 组件
3. @Component：用于标注泛指组件，当我们不知道某类属于哪类时（不属于@Controller、@Services等时），就可以标注为@Component

### 装配 Bean 时常用注解
spring作用在属性或方法上的注解（@Autowired，@Resource等），表明是当我用到这个属性或方法时，并不需要我们自己去new，只需要使用注解，spring容器会自动将我们需要的属性，方法创建出来，我们直接用就可以，这就是我们通常说的依赖注入和控制反转

1. @Autowired：属于 Spring 的org.springframework.beans.factory.annotation包下,可用于为类的属性、构造器、方法进行注值
2. @Resource：不属于spring的注解，而是来自于JSR-250位于java.annotation包下，使用该annotation为目标bean指定协作者Bean。 
3. @PostConstruct 和 @PreDestroy 方法 实现初始化和销毁bean之前进行的操作

#### @Resource 和 @Autowired
相同点：@Resource的作用相当于@Autowired，均可标注在字段或属性的setter方法上。
不同点：
1. 提供方 @Autowired是Spring的注解，@Resource是javax.annotation注解，而是来自于JSR-250，J2EE提供，需要JDK1.6及以上
2. 注入方式 @Autowired只按照Type 注入；@Resource默认按Name自动注入，也提供按照Type 注入,使用 @Resource 写法：`@Resource(name = "tiger")`

**@Autowired**
@Autowired 注解可以对类成员变量、方法及构造函数进行标注，完成自动装配的工作。 通过使用 @Autowired 可以消除原来对象需要使用的 set，get 方法以及spring xml 配置文件中 bean 属性中的 property。

使用 `<context:component-scan base-package="xxx" />` 可以告诉 spring 需要使用注解，因此 spring 会自动扫描 xxx 路径下的注解。
原来一个 Zoo 类中有 Tiger 和 Monkey 类，Zoo 类中就必须定义 getTiger、setTiger、getMonkey、setMonkey 方法，且 spring 的配置文件如下：
```xml
<bean id="zoo" class="com.xyy.bean.Zoo" >
    <property name="tiger" ref="tiger" />
    <property name="monkey" ref="monkey" />
</bean>
```
使用 @Autowired 后：
```java
public class Zoo
{
    @Autowired
    private Tiger tiger; // 不再需要写 set、get 方法
    
    @Autowired
    private Monkey monkey;
    
    public String toString(){return tiger + "\n" + monkey;}
}
```
```xml
<context:component-scan base-package="com.xyy" />
<bean id="zoo" class="com.xyy.bean.Zoo" />
```

**@Qualifier**
如果一个 Tiger 类有多个实现类，那么使用 @Autowired 时就必须注明实现类的具体名称
```java
@Autowired
@Qualifier("BigTiger") // 括号里面的应当是 Tiger 接口实现类的类名
private Tiger tiger;
```

**@Service**
使用 @Service 注解可以消除 <bean id="zoo" class="com.xyy.bean.Zoo" /> 这个 bean 配置：
```java
@Service // 写了这个就不用在 spring 的配置文件中配置 bean
public class Zoo{...}
```
Zoo.java 在 Spring 容器中存在的形式就是 "zoo"，即可以通过 ApplicationContext 的 getBean("zoo") 方法来得到Zoo.java 。
@Service注解，其实做了两件事情：
1. 声明Zoo.java是一个bean，这点很重要，因为Zoo.java是一个bean，其他的类才可以使用@Autowired将Zoo作为一个成员变量自动注入
2. Zoo.java在bean中的id是"zoo"，即类名且首字母小写

### spring MVC模块注解
1. @Controller ：表明该类会作为与前端作交互的控制层组件，通过服务接口定义的提供访问应用程序的一种行为，解释用户的输入，将其转换成一个模型然后将试图呈献给用户。
2. @RequestMapping ： 这个注解用于将url映射到整个处理类或者特定的处理请求的方法。可以只用通配符！
3. @RequestParam ：将请求的参数绑定到方法中的参数上，有required参数，默认情况下，required=true，也就是改参数必须要传。如果改参数可以传可不传，可以配置required=false。
4. @PathVariable ： 该注解用于方法修饰方法参数，会将修饰的方法参数变为可供使用的uri变量（可用于动态绑定）。
5. @RequestBody ： @RequestBody是指方法参数应该被绑定到HTTP请求Body上。
6. @ResponseBody ： @ResponseBody与@RequestBody类似，它的作用是将返回类型直接输入到HTTP response body中。

### Spring事务模块注解
在处理dao层或service层的事务操作时，譬如删除失败时的回滚操作。使用**@Transactional** 作为注解，但是需要在配置文件激活
```XML
<!-- 开启注解方式声明事务 -->
    <tx:annotation-driven transaction-manager="transactionManager" />
```

Spring 注解参考文档：https://blog.csdn.net/u010648555/article/details/76299467

