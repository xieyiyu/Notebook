1. conftest.py：
   pytest_addoption(parser) 注册命令行选项 
   -> pytest_configure(config)
   -> 从最外层 com.sankuai.zc.open.boxopenapi.http.xxx 的 __init__ 都执行一遍
   -> 到需要执行的用例的 py 文件，加载依赖和参数等，到测试方法 def test_XXX()
   -> pytest_generate_tests(metafunc)，通过 metafunc.parametrize() 实现参数化
   -> pytest_make_parametrize_id(config, val)
   -> pytest_collection_modifyitems(session, config, items)

### conftest.py
选择在 pytest 中执行某个 py 文件，在执行 py 文件的断言逻辑前，首先执行 conftest.py：
过一遍 conftest.py，都是 def 方法，没有需要执行的，然后就会自动去执行 pytest_addoption 方法

#### pytest_addoption(parser)
pytest_addoption(parser) 是一个初始化钩子，用来增加框架所需要的自定义的命令行选项
在这里默认了运行环境是 test，如果需要修改运行环境，则运行时需要加上参数 -E 或 --env

pytest_addoption(parser) 注册 argparse-style 选项以及 ini-style 配置值，在测试运行开始调用一
次。
之后可以通过config对象来访问：
- config.getoption(name) 来获取命令行选项的值
- config.getini(name) 来获取从 ini-style 文件中读取的值

注册完成后得到一个 config 对象，<_pytest.config.Config object at 0x10b96a750>
注册的命令在 config.option.env 和 config.option.swimlane 中得到其值

之后跳转到 pytest_configure(config) 执行
#### pytest_configure(config)
如果在命令行中给出了特定的测试用例 function，这个值将会在 config.args 列表中出现

得到 config.args，是一个 list
- 如果执行的是一个 py 文件或者是一个文件夹，那么 config.args 会得到文件夹或 py 文件的绝对路径
- 如果执行的是 py 文件中的某个 test 方法，那么 
config.args = <class 'list'>: ['test_pullBillQueryBuilder.py::test_pullBillQueryBuilder']

对于 module::function 形式的参数, 即使只是传入固定的 function，在 pytest_generate_tests 也会将整个 module 执行一次，无法只执行这个 function，因为 pytest_generate_tests 就是根据找到的每个 test definition 执行，使用 pytest_configure 来保存结果在 config.modulefunc_pairs，这个会在 pytest_generate_tests 中用到。

pytest_configure(config) 执行完成后，然后执行 __init__ 进行初始化，先从最外层的 com 开始，由外到内，com.sankuai.zc.open.boxopenapi，在 boxopenapi 的 __init__ 中定义了通用参数的 placeholder，因此会执行一遍，再到 http 的 __init__，最后就跳转到具体执行的 py 文件中，先加载头部需要的环境信息以及参数信息，然后就到具体的测试方法中 def test_pullBillQueryBuilder(case_data, req_result)，之后跳转到 pytest_generate_tests

### pytest_generate_tests(metafunc)
metafunc 的属性
fixturenames = <class 'list'>: ['case_data', 'req_result', 'request']
config

得到：
function_name = metafunc.function.__name__  # 正在执行的方法名，与执行用例的 json 名称相同
module_path = Path(metafunc.module.__file__)  # function 所在的 py 文件路径

调用 api_test_data_generator： 
根据 py 文件名（或方法名）和文件路径得到对应用例的 json 文件，对 json 文件进行解析
调用 resource.py 的 replace_env 方法替换 json 文件中的全局变量，<$env> 表示的部分，根据 pytest.ini 的数据
result_json_str = replace_env(json_str, env_section_dict)

如果是 appkey 形式的，在 pytest.ini 配置中不存在，因此也不会替换，是通过后面的请求在 Oceanus 得到的

解析 json 后，得到一个 json 的 list，里面包含多个 case，对每个 case，
```python
for item in test_data_json:
    yield CaseDataRes(item)  # 表明 api_test_data_generator 是个生成器函数，一次只返回一个结果，也就是一个 case
```
执行 resource.py：CaseDataRes(JsonResource)，要找的是 req 和 pre，得到 req_result 和 pre_result
调 resource.py 的 dict2res 方法
```python
elif 'url' in keys:
    return HttpRes(content_dict)
```

最后 metafunc.parametrize("case_data", iterator, indirect=True)
通过 metafunc.parametrize() 实现参数化

调用 pytest_make_parametrize_id
### pytest_make_parametrize_id(config, val)
根据 val 返回一个用于 @pytest.mark.parametrize 的字符串表达式。如果钩子无法解析 val，返回 None。
参数：
config(_pytest.config.Config) - pytest config 对象
val - 参数化的值
argname (str) – pytest自动生成的参数名

pyrig 中重写该钩子，通过 val.id 得到用例的 id，最后 return repr(val)

调用 pytest_collection_modifyitems(session, config, items)
### pytest_collection_modifyitems(session, config, items)
在收集完所有测试用例后调用该钩子方法
collection 完成后，使用 pytest_collection_modifyitems(session, config, items) 钩子修改项目顺序、删除或修改测试项目：
可以修改 items 用例列表,Pytest 将在注册期间验证你是否使用了与规范匹配的参数名称,如果不符合规范，则废弃掉该方法。
参数：
session(_pytest.main.Session)- pytest session 对象
config(_pytest.config.Config) - pytest config对象
items (List[_pytest.nodes.Item]) - 收集的测试用例列表，执行的 case，每个列表元素是 <Function test_pullBillQueryBuilder[p1: 白盒客户端初始化账单筛选项配置_SN维度]>

之后就是处理 case_data、request_result 这些fixture
通过 fixture 的 pre_result、 req_result 拿到执行结果后，再执行 py 中的断言
```python
@pytest.fixture
def req_result(request, case_data):
    return request_result(request.config, case_data.req, case_data.placeholder)
```
### req_result 
req_result： 是一个 fixture，在用例的 py 文件中传入 req_result 作为参数，得到请求返回结果
其中一个参数是 case_data，也是一个 fixture，用于得到用例的 case 文件信息
另一个参数 request 用于获取测试函数的上下文信息

#### case_data
在 case_data 中，会对 placeholders（可以通过 request.module 属性能够从测试函数中得到 placeholders 的值） 中的值进行实际值替换，如果是 thrift 接口，则会将 thrift 的文件路径变为绝对路径

req_result 的实例值是 request_result(request.config, case_data.req, case_data.placeholder)
request_result：

#### request.config 
request.config 是一个全局变量，可以进行命令行参数获取，下面的 config 是 request.config
得到运行的环境信息 env = {'env': config.getoption('env'), 'swimlane': config.getoption('swimlane')}

#### request_result 方法
判断请求是什么对象： http、thrift、mysql、kylin
得到请求结果，即 case 执行的返回 resp，http 请求需要带上 secret 去请求
```python
if isinstance(req, HttpRes):
    secret = placeholder.get('secret') if placeholder else None
    resp = MTHttpReqController(env, req).request(secret)
```

若得到的 resp 是 dict，执行 update_extract(req.extract, resp, placeholder)，如果是其他数据结构，则 ignore placeholder replacement action
如果在 json 中需要提取返回结果 extract，那就将其加到 placeholder 中，供 case 后面的请求使用

将 resp 添加到 req_result_list 中，根据 req 的列表的大小，循环执行并得到每个 resp
最后返回给 return req_result_list[0] if len(req_result_list) == 1 else req_result_list
req_result 这个 fixture 的实例执行完成，得到请求结果

然后 py 文件中拿到这个 req_result，去进行 assert 判断。

对于 pre_result 这个 fixture，也是和 req_result 一样的执行步骤，只是传入的是 json 中的前置条件 case_data.pre

得到 req_result 后，就去执行 py 文件中后面自己写的 assert 逻辑，至此第一个 case 结束

### MTHttpReqController
resp = MTHttpReqController(env, req).request(secret)

MTHttpReqController 集成自 ReqController，传入的 req 需要进行预处理 preprocess
preprocess 是在执行请求操作前对资源进行预处理；必须在子类中进行重写实现；如果没有预处理，则直接返回资源 req

#### preprocess
resource['url'], resource['appkey'] = parse_http_url(resource.url, self._env)
使用 appkey_mappings.parse_http_url 根据给定的 appkey 生成一个请求 url
需要获取 url 的协议（http or https）和域名地址
1. json 中是 appkey 形式：
  1.1 得到 appkey 和 path -> 调用 OceanusApi(env_e) ，传入环境 test，实例化一个 OceanusApi 对象 oc
       Oceanus 配置管理中心，api 详见：https://km.sankuai.com/page/28273892
      1.1.1 oc.get_appkey_info(appkey)，path = '/api/pool/com.sankuai.zc.open.boxopenapi'，请求 _oceanus_req 方法
            ```python
              path = f"/api/pool/{appkey}"
              data = {'Parameters': {'appkey': appkey, 'token': OCEANUS_TOKEN}}
              return self._oceanus_req(path, json=data)
            ```
      1.1.2 得到实际的 url 为 'http://oceanus.inf.test.sankuai.com/api/pool/com.sankuai.zc.open.boxopenapi'
        然后请求这个 url，得到 oceanus 的返回结果，返回给 appkey_mappings
  
  1.2 得到 protocol = http（或https），site
      {'name': 'boxopenapi.zc.test.sankuai.com', 'locations': [{'location_id': 23275, 'location_path': '/', 'dam_status': 0, 'dam': {}}]}
      得到这个 site 的 name，即 domain = 'boxopenapi.zc.test.sankuai.com'
  
2. json 中直接给的 http 形式： 直接获取端口号和域名地址

3. 得到后，组合 domain_path = f"{domain}{path}" 
  url = f"{protocol}://{swimlane}-sl-{domain_path}" if swimlane not in domain_path else f"{protocol}://{domain_path}"
  得到最终的 url 为：'http://boxopenapi.zc.test.sankuai.com/api/init/pullBillQueryBuilder'

4. 如果需要 sign，通过 get_client_channel 得到 appkey 是属于 pos、blackbox 还是 magicbox
   然后 resource = parse_client_sign(resource, self._env)，增加验签

#### 终端验签
增加pos、小白盒、小黑盒验签逻辑，在服务端打开验签开关的情况下case可以通过
1.默认自动给小白盒、小黑盒、POS的请求增加验签，对json中的sign不再要求（可添加or不添加）
2.POS请求无需手动增加signin接口请求，直接进行正常请求即可，
json的data中batchno字段可随意填写（验签逻辑中会自动替换batchno）
3.如不需要验签，在case中与url、method、json同一级别增加入参need_sign:false
pos端在pay接口后需要query当前pay返回的订单时，两个请求的need_sign值必须相同 (原因：pay和query两个需要batchno相同，pos sign的过程会替换batchno，一个接口替换，一个不替换会导致batchno不同)

5. 返回 resource，初始化 _res 完成，self._res = self.preprocess(resource) 回到父类 ReqController 继续下面的初始化

#### ReqController.request
跳到子类的 req 方法中，是对父类的重写
```python
def req(self, secret=None):
    if self._res['appkey'] and self._res['oceanus_auth']:
        return MTRequest(self._res).sign(secret, self._res['appkey']).request()
    else:
        return MTRequest(self._res).sign(secret).request()
```
带着签名跳到 http.MTRequest

##### MTRequest 类
MTRequest 继承自 RigBaseRequest
sign 方法：
对 secret 进行加密，signed_str = Sha1Sign.sign(self.get_sign_data(), secret)，获取美团SHA-1签名
然后将 sign 添加到请求参数中，即 req 的 json 中 self.update_sign_str('sign', signed_str, 'json')

request 方法：将请求结果转化为 json
return JsonResource(super().request().json())
实际的请求服务器处理是调用父类 RigBaseRequest 的 request() 方法，
```python
def request(self):
    with Session() as session:
        return session.send(self.prepare())
```
requests 会去请求服务器，得到返回结果后，转化为 json 格式，然后调用我们写的 JsonResource 方法类

至此，请求结束，得到结果后返回给 conftest.request_result 方法中
也就是最开始的 resp = MTHttpReqController(env, req).request(secret) 中
再返回给 req_result 这个 fixture

### 执行 json 的第二个 case
第一个 case 的断言逻辑执行完成后，开始执行 json 文件中定义的第二个 case，不会再去解析前面的环境信息，直接去获取 case_data 和 req_result

执行完最后一个 case 的断言逻辑后，整个 py 文件执行结束，没有后续的 teardown

## 重要文件







### 思考
1. 如果想添加 skip，跳过前置条件就错误的 case， 可有在 case_data 中进行判断

### 疑问
没搞懂这里
for item in test_data_json:
  yield CaseDataRes(item)


https://www.cnblogs.com/superhin/p/11478007.html
https://www.cnblogs.com/superhin/p/11733499.html