数据库变更实时传输系统
一个高可用、低延时、高并发、保证数据一致性的数据库变更实时传输系统。对业务开发而言，Dbus屏蔽了复杂的数据库拉取、并发实现甚至databus本身的引用逻辑，业务同学只需要在现有系统中提供一个Http接口、订阅一个MQ主题或者提供一个Thrift接口，就可以轻松获取binlog事件信息。

## Databus
Databus 是一个实时的、可靠的、支持事务的、保持一致性的数据变更抓取系统。
Databus 通过挖掘数据库日志的方式，将数据库变更实时、可靠的从数据库拉取出来，业务可以通过定制化 client 实时获取变更。
Databus 的传输层端到端延迟是微秒级的，每台服务器每秒可以处理数千次数据吞吐变更事件，同时还支持无限回溯能力和丰富的变更订阅功能。

### 功能&特性
1. 来源独立：Databus支持多种数据来源的变更抓取，包括Oracle和MySQL。

2. 可扩展、高度可用：Databus能扩展到支持数千消费者和事务数据来源，同时保持高度可用性。

3. 事务按序提交：Databus能保持来源数据库中的事务完整性，并按照事务分组和来源的提交顺寻交付变更事件。

4. 低延迟、支持多种订阅机制：数据源变更完成后，Databus能在微秒级内将事务提交给消费者。同时，消费者使用Databus中的服务器端过滤功能，可以只获取自己需要的特定数据。

5. 无限回溯：这是Databus最具创新性的组件之一，对消费者支持无限回溯能力。当消费者需要产生数据的完整拷贝时（比如新的搜索索引），它不会对数据库产生任何额外负担，就可以达成目的。当消费者的数据大大落后于来源数据库时，也可以使用该功能。

### Databus 构成
Databus 包括中继Relay、bootstrap服务和客户端库。Bootstrap服务中包括Bootstrap Producer和Bootstrap Server。

快速变化的消费者直接从 Relay 中取事件。如果一个消费者的数据更新大幅落后，它要的数据就不在 Relay 的日志中，而是在 Bootstrap Producer 里面，提交给它的，将会是自消费者上次处理变更之后的所有数据变更快照。

#### Databus Relay
Databus Relay中继的功能主要包括：
1. 从 Databus 来源读取变更行，并在内存缓存内将其序列化为 Databus 变更事件
2. 监听来自 Databus 客户端（包括Bootstrap Producer）的请求，并传输新的 Databus 数据变更事件

#### Databus客户端
功能主要包括：
1. 检查Relay上新的数据变更事件，并执行特定业务逻辑的回调
2. 如果落后Relay太多，向Bootstrap Server发起查询
3. 新Databus客户端会向Bootstrap Server发起bootstrap启动查询，然后切换到向中继发起查询，以完成最新的数据变更事件
4. 单一客户端可以处理整个Databus数据流，或者可以成为消费者集群的一部分，其中每个消费者只处理一部分流数据

#### Databus Bootstrap Producer
功能有：
1. 检查中继上的新数据变更事件
2. 将变更存储在MySQL数据库中
3. MySQL数据库供Bootstrap和客户端使用

#### Databus Bootstrap Server
主要功能是监听来自Databus客户端的请求，并返回长期回溯数据变更事件。