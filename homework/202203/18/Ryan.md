# 你知道的中间件有哪些
中间件是协助用户应用软件和系统软件进行连接的软件，以便于软件各部件之间的沟通。
常见的中间件分为三类：

### 交易中间件

用于处理双向的联机业务，将业务从异构的系统中抽象出来进行高效处理，需要处理大量并发进程。多用于银行业务系统、电信计费系统等场景中。

### 通信中间件

它在将消息从它的源中继到它的目标时充当中间人，主要目的是提供路由并保证消息的高效传递，不处理消息内容。  
如果发送消息时接收者不可用，通信中间件会保留消息，直到可以成功地传递它，主要解决传统结构耦合性问题、系统异步性问题以及缓解大数据量并发的问题等。
常见的有RocketMQ和Kafka。

### 应用服务器中间件

位于客户浏览器和数据库之间，单向地为应用程序提供业务逻辑的展示。常见的有Apache Tomcat和Apache Geronimo等。