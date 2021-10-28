## 7 服务发现
- 各个服务登记注册，其他服务查看调用
- ZooKeeper，Consul，Etcd，Netflix的Eureka
- 客户端注册，启动注册，保持心跳，直至注销，注册中心可以探活心跳，注册和服务太过耦合
- 三方注册，独立的Registrar，保持高可用
- 服务端发现，需要独立的高可用的路由服务，服务负责查询服务和负载均衡

## 7.1.2 应用程序接口网关
- 进入系统的唯一节点，类似Facade设计模式，封装了所有的功能，认证，监控，负载均衡，缓存，分配，静态内容