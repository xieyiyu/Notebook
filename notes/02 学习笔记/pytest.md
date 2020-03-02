# pytest
pytest 会查找 test 开头或结尾的 module(py 文件), Test 开头的 class, 以及 test 开头的方法

pytest 是在 pluggy 基础上构建的，pluggy 是 pytest 插件管理和 hook 调用的核心，pluggy 的插件能够扩展和自定义 pytest 的功能。

## pytest.fixture
fixture 是 pytest 特有的功能，通过 pytest.fixture 标识定义在函数 A 前面，那么在编写测试函数 B 时，可以讲函数 A 的返回值作为测试函数 B 的传入参数。

通过 @pytest.fixture 装饰器可以注册一个 fixture。对每个参数名，如果已经声明定义 fixture，会自动创建一个实例并传入该测试函数。

```python
import pytest

@pytest.fixture
def smtp_connection():
    import smtplib
    return smtplib.SMTP("smtp.gmail.com", 587, timeout=5)

def test_ehlo(smtp_connection):
    response, msg = smtp_connection.ehlo()
    assert response == 250
    assert 0 # 用于调试
```

执行的过程如下：
1. pytest 收集到测试用例 test_ehlo，其有一个形参 smtp_connection，pytest 查找到一个同名的已经注册的fixture；
2. 执行 smtp_connection() 创建一个 smtp_connection 实例 <smtplib.SMTP object at 0x105992d68> 作为test_ehlo 的实参；
3. 执行 test_ehlo(<smtplib.SMTP object at 0x105992d68>)

注： 可以使用 `pytest --fixtures test_name.py` 来查看可用的 fixture
若要查看以 _ 开头的 fixture， 添加 -v 参数

pytest 的 fixture 允许测试函数轻松的接收和处理应用层对象的预处理，而不必关心import/setup/cleanup 的细节。 
这是依赖注入的的一个极佳的示范，fixture 函数是注入器，而测试函数是 fixture 的使用者。

### confest.py： 共享 fixture 实例
如果想在多个测试模块中共享同一个 fixture 实例，可以把这个 fixture 移动到 conftest.py 文件中；或者是需要使用到来自多个文件的 fixture 函数，可以将这些 fixture 都放在 conftest.py 中。

在测试模块中不需要手动导入 fixture，pytest 会自动发现 conftest.py 中的 fixture。

conftest.py 放在不同的路径下，pytest 会根据层级关系来确定其作用范围，官方建议放在项目根目录下，不宜路径太深。
pytest 在启动后会加载配置文件，例如 ini 文件，和这个 conftest.py。

pytest 命令行参数会被传递给 config 变量，这是一个全局对象，类似的还有 request， session，items。
如果在命令行中给出 “--lf” ，那么这个值将会在 config.option.lf 属性被设置成bool True

#### fixture的查找的顺序
1. 测试类
2. 测试模块
3. conftest.py
4. 内置和第三方的插件。

#### scope：在类/模块/整个测试中共享 fixture 实例
scope 参数的值：function（默认值）、class、module、package 和 session

例如：在 @pytest.fixture(scope='module')，使每个测试模块只调用一次 smtp_connection（默认每个用例都会调用一次），这样模块中的多个测试函数将会共享同一个 fixture 实例

scope 越大，实例化越早。
当函数调用多个 fixtures 的时候，scope 较大的(比如session)实例化早于 scope 较小的(比如function
或者class)。同样 scope 的顺序则按照其在测试函数中定义的顺序及依赖关系来实例化。

### fixture 的清理操作
在fixture退出作用域之前，执行某些清理性操作（例如，关闭服务器的连接等）；
使用 yield 代替return，yield 后面的语句将会在 fixture 退出作用域的时候被调用来清理测试用例。

```python
# conftest.py
import smtplib
import pytest

@pytest.fixture(scope="module")
def smtp_connection():
    smtp_connection = smtplib.SMTP("smtp.gmail.com", 587, timeout=5)
    yield smtp_connection
    print("teardown smtp")
    smtp_connection.close()
```
无论测试是否发生了异常，print 及 smtp.close() 语句将在 module 的最后一个测试函数完成之后被执行。
如果 scope=‘function’，则会在每个测试函数结束后都调用 print 和 smtp.close()

除了使用 yeild 之外，还可以使用 addfinalizer 函数来注册一个 teardown 的处理函数
```python
# conftest.py
import smtplib
import pytest
@pytest.fixture(scope="module")
def smtp_connection(request):
    smtp_connection = smtplib.SMTP("smtp.gmail.com", 587, timeout=5)

    def fin():
        print("teardown smtp_connection")
        smtp_connection.close()
        request.addfinalizer(fin)
        return smtp_connection
```
yield 和 addfinalizer 在测试结束之后的调用基本类似，但 addfinalizer 可以：
1. 注册多个完成函数
2. 无论 fixture 是否存在异常，addfinalizer 注册的函数都会被调用，即使出现异常，也可以正确的关闭在 fixture 中创建的资源。

### fixture 可以获取测试对象的上下文
fixture 函数可以通过接收一个 request 参数来获取测试函数、测试类、测试模块，甚至测试会话的上下文环境；

扩展上面的 smtp_connection，让其根据不同的测试模块使用不同的服务器。
使用 request.module 属性可以从测试模块中选择获取特定的属性，如下面从 test_anothersmtp.py 模块中获取 smtpserver

```python
# conftest.py
import pytest
import smtplib

@pytest.fixture(scope="module")
def smtp_connection(request):
    server = getattr(request.module, "smtpserver", "smtp.gmail.com")
    smtp_connection = smtplib.SMTP(server, 587, timeout=5)
    yield smtp_connection
    print("finalizing %s (%s)" % (smtp_connection, server))
    smtp_connection.close()
```

```python
# test_anothersmtp.py
smtpserver = "mail.python.org" # 会被smtp fixture读取，会用该模块定义的 smtpserver，而不是 conftest 中默认的 
def test_showhelo(smtp_connection):
    assert 0, smtp_connection.helo()
```

### request
通过 request 参数，可以获取大量信息，包括config、fixturename，以及module、cls、function等
```python
import pytest

@pytest.fixture
def fix1(request):
    for item in dir(request):
        if item.startswith("_"):
            continue
        print("{:18} => {}".format(item, getattr(request, item)))

def test_1(fix1):
    assert 0

if __name__ == "__main__":
    pytest.main(["-v"])
```

### fixtures 工厂方法
？？？

### fixtures 参数化
fixture 函数可以进行参数化的调用，这种情况下，相关测试集会被多次调用，即依赖该 fixture 的测试参数的集合。

标记 fixture 来创建两个 smtp_connection 的实例，这会使得所有的测试使用这两个不同的 fixture 运行两次
```python
# conftest.py
import pytest
import smtplib

@pytest.fixture(scope="module", params=["smtp.gmail.com", "mail.python.org"])
# 为 fixture 添加一个 params 列表，params 可以通过 request.params 在 fixture 中进行访问的列表
def smtp_connection(request):
    smtp_connection = smtplib.SMTP(request.param, 587, timeout=5)
    yield smtp_connection
    print("finalizing %s" % smtp_connection)
    smtp_connection.close()
```

### fixtures 模块化
fixture 函数本身也可以使用其他的 fixture。这可以使得 fixture 的设计更容易模块化，并可以在多个项目中复用。

fixture 可以引用作用域更广泛的 fixture，但是反过来不行，比如 session 作用域的 fixture 不能引用一个 module 作用域的fixture

测试过程中，pytest 会保持激活的 fixture 的数目是最少的 。 如果有一个参数化的 fixture，那么所有
使用它的测试用例会首先使用其一个实例来执行，直到它完成后才会去调用下一个实例。 
这样做使得应用程序的测试中创建和使用全局状态更为简单。

## pytest 中的钩子方法（hook）
钩子函数：
通过设置钩子，应用程序对所有消息事件进行拦截，然后执行钩子函数。 可以对代码进行一定的监控，使用模块来提供不同的行为或在发生某些事情时做出反应。
钩子函数经常会用到回调函数，回调函数是一种钩子函数。

区别：钩子函数在捕获消息的第一时间就执行，而回调函数是捕获结束时，最后一个被执行的。

pytest 整个框架通过调用如下定义良好的 hooks 来实现配置，收集，执行和报告这些过程：
1. 内置 plugins：从代码内部的 _pytest 目录加载；
2. 外部插件（第三方插件）：通过 setuptools entry points 机制发现的第三方插件模块；
3. conftest.py 形式的本地插件：测试目录下的自动模块发现机制；
conftest.py 可以作为最简单的本地 plugin 调用一些 hook 函数，以此来做些强化功能。

原则上，每个 hook 都是一个 1:N 的 python 函数调用， 这里的 N 是对一个给定 hook 的所有注册调用数。
所有的 hook 函数都使用 pytest_xxx 的命名规则，以便于查找并且同其他函数区分开来。

### 在 pytest 中有以下几种 hook 函数：
1. Bootstrapping hooks, 启动 pytest 时引入
2. Initialization hooks, 初始化插件, 及 conftest.py 文件
3. Collection hooks, 从目录/文件中发现 testcase
4. Test running hooks, 执行 case 时调用
5. Reporting hooks, 报告相关
6. Debugging/Interaction hooks, 特殊 hook 函数, 异常交互相关

### pytest_addoption(parser)
pytest_addoption(parser) 是一个 Initialization hooks 初始化钩子，在插件及 conftest.py 中调用

在命令行中我们可以增加框架所需要的自定义的 option（比如一些环境信息，是 test 还是 st 环境），这需要有一个地方来接收这些参数，这些是 config 对象，就使用到了 pytest_addoption(parser) 这个钩子。
pytest_addoption(parser) 通过Parser注册命令行参数 argparse-style, 以及添加 ini-stype 配置值注册，在测试运行开始调用一次。
注意，因为 pytest 的插件查找机制，该函数只应该在测试的 root 文件夹下的插件及 conftest.py 中实现

```python
parser.addoption("-E", "--env", action='store', dest='', default='test', help=f"xxx")
parser.addoption("-S", "--swimlane", action='store', dest='', default='',help=f"xxx")
```
注意： 自定义的命令行选项不能全部写在一行，一个命令应该用 parser.addoption 写一行，否则是指同一个参数的不同表示方式。

之后可以通过config对象来访问：
- config.getoption(name) 来获取命令行选项的值
- config.getini(name) 来获取从 ini-style 文件中读取的值

### pytest_configure(config)
命令行解析完成后, 初始化 conftest.py 文件时执行

### pytest_generate_tests(metafunc)
如果想要自定义或动态决定 fixture 的参数或范围，可以使用 pytest_generate_tests(metafunc) 这个 Collection hooks（在收集测试用例时），向测试方法传递参数, 生成对测试函数的（多个）参数化调用。
在测试用例的收集过程中被调用，它接收一个 metafunc 对象，我们可以通过其访问测试请求的上下文，更重要的是，可以使用 metafunc.parametrize 方法自定义参数化的行为；

定制加载外部数据，此处可以根据 cls 名称读取数据文件（txt, csv等），并将结果添加到 parametrize 方法内

Metafunc.parametrize(argnames, argvalues, indirect=False, ids=None, scope=None) 根据给定的参数列表里的参数添加新的函数调用。参数化是在 collection 阶段执行的。
如果有比较耗费资源的设置，请使用间接设置的方法而不是在测试用例里直接设置。
1. argnames - 由逗号分隔的代表参数名的字符串，或者一个参数字符串的列表/元组
2. argvalues - argvalues的数量决定了测试函数会被调用多少次。 如果只有一个参数，那么argvalues是一个list，如果有N个参数，argvalues是一个N元tuple，tuple里的每个值代表一个
参数。
3. indirect - 由参数名或者布尔值组成的列表。 这个列表是argnames的一个子集。如果这里配置了argnames，那么对应的列表中的argname会作为request.param传递给相关的fixture函数，因此使用这种方式可以在setup阶段执行开销较大的设置



### pytest_collection_modifyitems(session, config, items)
所有的测试用例收集完毕后调用, 可以再次过滤或者对它们重新排序

### pytest 参数
#### pytest_generate_tests(metafunc)
Metafunc objects are passed to the :func:`pytest_generate_tests <_pytest.hookspec.pytest_generate_tests>` hook.
They help to inspect a test function and to generate tests according to
test configuration or values specified in the class or module where a
test function is defined.

#### pytest_configure(config)
config：
command line options, ini-file and conftest.py processing
access to configuration values, pluginmanager and plugin hooks.


## pytest.ini
pytest 配置文件可以改变 pytest 的运行方式，它是一个固定的文件 pytest.ini 文件，读取配置信息，按指定的方式去运行。
[pytest]
# https://docs.pytest.org/en/latest/customize.html#adding-default-options
addopts = -s

-s 允许测试运行时输出任何符合标准的输出流信息，例如代码里面的 print
执行 pytets 就默认带上这个参数，也可以增加其他的参数，这样就不用每次执行的时候在命令行上自己加上 -s 参数了





## 参考文档
[pytest hooks](https://www.jianshu.com/p/32b645b61339)