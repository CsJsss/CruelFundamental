# IO 模型有哪几种

    1.阻塞IO：数据处理线程发起IO请求后，若数据没有准备完毕，则线程会一直等待，直到IO结束。
    2.非阻塞IO：数据处理线程发起IO请求后，若数据没有准备完毕，线程会返回，但会一直发请求询问数据是否准备好，直到IO结束。

# 什么是信号驱动IO

    使用信号驱动函数监控多个IO线程的行为，如epoll，监控不同的IO线程的文件描述符，若某fd就绪，则函数向系统吐出该IO的就绪状态，系统通知对应处理线程去进行IO，无需处理线程一直发请求。
    
# 什么是IO多路复用

    使用信号驱动IO的行为，无需处理线程一直等待或者一直发请求询问，处理线程有对应数据要处理了才被唤醒。