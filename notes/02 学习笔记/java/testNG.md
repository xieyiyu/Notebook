# TestNG

## TestNG 配置文件
testNG 的测试级别为：suite -> test -> class -> method
- ⼀个 suite(套件) 由⼀个或多个 test 测试组成。
- ⼀个 test(测试) 由⼀个或多个 class 类组成。
- ⼀个 class(类) 由⼀个或多个 method ⽅法组成。
- 一个 method 中可能有多条用例

![testng.xml 文件详细配置信息](./testng.xml)

## TestNG 注解
1. @BeforeSuite/@AfterSuite：被注释⽅法将在某个测试套件运⾏前/某个测试套件所有测试⽅法运⾏后执⾏
2. @BeforeTest/@AfterTest：被注释⽅法将在测试运⾏前/某个测试所有测试⽅法运⾏后执⾏
3. @BeforeClass/@AfterClass：被注释⽅法将在当前类的第⼀个测试⽅法调⽤前，相当于用例执行前的数据准备/当前类所有测试⽅法运⾏后运⾏，相当于用例执行后的数据销毁或恢复
4. @BeforeMethod/@AfterMethod：被注释⽅法将在每⼀个测试⽅法调⽤前/后运⾏
5. @Test：用例执行

@BeforeSuite/@AfterSuite/@BeforeTest/@AfterTest 可以对不同的测试类⽣效，其他注解只在本类范围内⽣效

### 执行顺序
@BeforeSuite->@BeforeTest->@BeforeClass->
{@BeforeMethod->@Test->@AfterMethod} **其中{}内的与多少个@Test，就循环执⾏多少次**
->@AfterClass->@AfterTest->@AfterSuite

## TestNG 参数化
使用 @DataProvider 注解，可以标记⼀个⽅法⽤于为测试⽅法提供数据。
被注释的⽅法必须返回 Object[][]（Iterator<Object[]>）, 其中每个 Object[] 可以作为为这个测试⽅法的参数列表。

@Test ⽅法需要指定 dataProvider 属性，可以从 DataProvider 中接收数据。
DataProvider 是一个二元数组，为测试用例提供参数，有多少组参数就会执行多少次用例，因此它是一个让测试类实例的某个方法执行多次，但每次执行都使用同一个实例。 要从 DataProvider 接收数据的 @Test 方法需要使用与此注释名称相等的 dataProvider 名称。 
```java
import xxx.testbase.TestBase; // 引入另一个包中的文件 testbase 中的 TestBase 类

public class DataProviderTest{
    @Test(dataProvider = "json", description = "xxx")
    public void testDataProvider(JSONObject request, JSONObject expect){ // json 文件中存储的是具体的测试数据
        // 测试逻辑，断言等
    }
}
```

testbase.java
```java
import org.testng.annotations.DataProvider;

public class TestBase{
    @DataProvider(name = "json")
    public Object[][] getJsonAllCases(Method method) {// method 即 testDataProvider
        String testJsonFileName = this.getTestDataFilePath(method, ".json"); // 获取 json 文件，一般是名称相同的文件，也就是找到 testDataProvider.json 文件所在路径
        return JSON2ParamsUtil.JSON2Array(testJsonFileName); // 将 json 文件转换为 TestNG 用例能够接收的格式，即 Object[][]
    }
    // 实际上 case 可以用多种文件形式标识，如 yaml、数据库形式
    // 而 TestBase 就相当于是一个数据源适配器，可以将多种格式的数据源都转化为 Object[][] 格式
    @DataProvide(name = "yaml")
    public Object[][] getYamlCaseData(Method method) {
        // 具体转换逻辑
    }
}
```

## TestNG 依赖
场景测试时，某些用例可以会依赖其他用例的执行，可以通过 dependsOnMethods 让多个用例的执行串起来，若上一个步骤失败则后面的所有步骤都跳过
```java
public class dependTest{
    @Test
    public void firstCase(){...}
    @Test(dependsOnMethods = "firstCase")
    public void secodeCase(){...}
}
```

## 特殊测试时的方法
1. 忽略测试：@Test(enabled = false)
2. 超时测试或异步测试：设置超时时间 @Test(timeOut = 5000)；
    invocationCount 调用次数、invocationTimeout 调用超时总时间： @Test(invocationCount = 3, invocationTimeOut = 1000)
3. 多线程测试：@Test(threadPoolSize = 5, invocationCount = 10)

## TestNG 监听器
监听器是一个专门用于对其他对象身上发生的事件或状态改变进行监听和做出相应处理的对象，当被监视的对象发生情况时，立即采取相应的行动。通俗地说，
监听器的编码过程是定义一个 Java 类实现监听器接口 org.testng.ITestNGListener。TestNg 中提供的一些常用的监听器都是通过实现org.testng.ITestNGListener接口而完成的。

listeners 首先需要在 TestNG 的配置文件中进行配置，配置文件一般是 testng.xml 格式，放在 resources 目录下
```xml
<listeners>
    <listener class-name="xxx.testbase.util.RetryListener"/>
    <listener class-name="xxx.testbase.util.TestListener"/>
</listeners>
```
RetryListener 和 TestListener 都是业务自定义的监听器，一般是需要实现 TestNG 中的一些接口方法，方可灵活使用
RetryListener 实现了 IAnnotationTransformer 接口，IAnnotationTransformer 是用于修改 @Test 的属性
```java
import java.lang.reflect.Constructor;
import java.lang.reflect.Method;
import org.testng.IAnnotationTransformer;
import org.testng.IRetryAnalyzer;
import org.testng.annotations.ITestAnnotation;

public class RetryListener implements IAnnotationTransformer {
    public RetryListener() {
    }
    public void transform(ITestAnnotation testannotation, Class testClass, Constructor testConstructor, Method testMethod) {
        // 可以看下 IAnnotationTransformer 接口的默认实现 DefaultAnnotationTransformer 类中就是定义了这四个属性
        IRetryAnalyzer retry = testannotation.getRetryAnalyzer();
        if (retry == null) {
            testannotation.setRetryAnalyzer(Retry.class);
        }
    }
}
```

TestListener 实现了 ITestListener 接口，ITestListener 接口主要功能如下：
1. 在测试⽅法成功、结束、跳过后，执⾏⼀些逻辑
2. 在 <test> 执⾏前后加⼀些逻辑
3. extends TestListenerAdapter 会简化你的代码
4. 一些入库、上报等等操作都可以在这里面实现
```java
public class TestListener implements ITestListener {
    public TestListener() {
    }
    // 在所有测试⽅法执⾏结束之后执⾏  @param context
    public void onFinish(ITestContext testContext) {
        TestNGUtil.removeDuplicateResult(testContext);
    }
    // 在测试⽅法开始前执⾏
    public void onTestStart(ITestResult result) {
        // 具体实现，比如在测试前拿到 Traceid，做一些打印操作等
    }
    // 在测试⽅法成功后执⾏
    public void onTestSuccess(ITestResult result) {}
    // 在测试⽅法失败后执⾏
    public void onTestFailure(ITestResult result) {}
    // 在测试⽅法跳过后执⾏
    public void onTestSkipped(ITestResult result) {}
    // 在测试⽅法失败但为百分⽐失败后执⾏
    public void onTestFailedButWithinSuccessPercentage(ITestResult result) {}
    // 在 testClass 实例化之后、configuration ⽅法调⽤之前执⾏ @param context
    public void onStart(ITestContext context) {}
}

```

## TestNG 断言
在执行自动化测试脚本的时候，需要自动判断测试脚本执行完成后的实际结果是否与预期结果一致，这个时候就需要在程序运行之前写入断言，判断当前程序执行后是否正常。
TestNG 中的断言分为硬断言和软断言两种：
### Assert
Assert 类是硬断言，当脚本运行到断言失败时，马上停止运行，断言后面代码将不会被执行。
```java
import org.testng.Assert;
...
Assert.assertEquals(2*2, 4, '计算错误');
```

- assertTrue / assertFalse ：判断是否为 True/False。
- assertSame / assertNotSame ：判断引用地址是否 相同/不相同。
- assertNull / assertNotNull ：判断是否为 null/不为null。
- assertEquals /  assertNotEquals ：判断是否 相等/ 不相等，Object 类型的对象需要实现 haseCode 及 equals 方法。
- assertEqualsNoOrder：判断忽略顺序是否相等

### SoftAssert
SoftAssert 类是软断言。如果断言失败的话，程序不会停止运行，会继续执行这个断言下的其他语句或者断言，不影响其他断言的运行。
软断言必须创建实例对象，才能调用相关实例方法进行软断言，且在最后一个断言后面，必须调用 assertAll() 方法
```java
import org.testng.annotations.Test;
import org.testng.asserts.SoftAssert;

public class TestSoftAssert {
    @Test
    public void testSoftAssert(){
        SoftAssert assertion = new SoftAssert(); // 必须实例化 SoftAssert
        assertion.assertEquals(5, 6, "我俩不是一样大");
        System.out.println("脚本执行结束"); // 仍会执行
        assertion.assertAll(); // 最后必须有这个~
    }
}
```

## 编写测试类
```java
@ContextConfiguration(locations = {"classpath:thrift-context/rmspromotioncenter.xml"}) // 在 resource/thrift-context 目录下
public class ProcessTest extends TestBase {
    @Autowired(required = false)
    MyManageThriftService myManageThriftService;

    public ProcessTest() throws IOException {
    }

    @Contributor(owner = "xxx") // 框架自定义注解
    @Test(dataProvider = "json", description = "xx功能")
    public void myMethodTestCase(JSONObject preconditions, String comments, JSONObject request, JSONObject expect) throws IOException, TException {
        // 初始化参数
        Context context = eventEditor.context;
        Prepare.initTrace();
        // 具体逻辑和断言...
    }
}
```
### ContextConfiguration
@ContextConfiguration 用于加载配置类，表示我们想要导入这个测试类的某些bean，将 class 路径中的单个 xml 文件加载进来，可以自动扫描该文件下的所有 bean，之后在测试类中使用 @Autowired 注解可以获取自动扫描包下的所有 bean
- classpath：只会到设置的 class 路径中查找找文件。
- classpath*：不仅包含class路径，还包括jar文件中（class路径）进行查找。

xml 文件中：
```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="propertyConfigure" class="org.springframework.beans.factory.config.PropertyPlaceholderConfigurer">
        <property name="ignoreUnresolvablePlaceholders" value="true"/>
        <property name="ignoreResourceNotFound" value="true"/>
        <property name="locations">
            <list>
                <value>classpath:config.properties</value>
            </list>
        </property>
    </bean>

    <bean id="myManageThriftService" class="xxx.proxy.ThriftClientProxy" destroy-method="destroy">
        <property name="xxx" ref="xxx"/>
        <property name="serviceInterface" value="xxx.MyManageThriftService"/>
        <property name="timeout" value="10000"/> <!-- 可不配置，默认10 -->
        <property name="remoteServerPort" value="9000"/> <!-- Server 监听端口 -->
        <property name="appKey" value="com.xxx"/> <!--本地服务 appkey -->
        <property name="remoteAppkey" value="com.xxx"/>  <!-- 目标server appkey -->
    </bean>
</beans>
```

### Autowired


### TestNG与spring集成
#### AbstractTestNGSpringContextTests
测试类必须继承 AbstractTestNGSpringContextTests 类才拥有注入实例的能力，与 spring 和依赖注入相关


参考文档：
TestNG系列-TestNG入门：https://www.jianshu.com/p/b8b4ee8d3b99