### Python: 简述 GIL，为什么有了GIL还要关注线程安全

GIL: Global Interpreter Lock 全局解释器锁

- 每个CPU核在同一时间只能执行一个线程

  

在Python多线程下，每个线程的执行方式：

1. 获取GIL
2. 执行代码直到sleep 或者是Python虚拟机将其挂起
3. 释放GIL

- 某个线程想要执行，必须先拿到GIL。可以把GIL看作是“通行证”，并且在一个Python进程中，GIL只有一个。拿不到通行证的线程，就不允许进入CPU执行。

- 而每次释放GIL锁，线程进行锁竞争、切换线程，会消耗资源。并且由于GIL锁存在，python里一个进程永远只能同时执行一个线程(拿到GIL的线程才能执行)，这就是为什么在多核CPU上，python的多线程效率并不高。
- Python 3 GIL不使用ticks计数，改为使用计时器（执行时间达到阈值后，当前线程释放GIL），这样对CPU密集型程序更加友好，但依然没有解决GIL导致的同一时间只能执行一个线程的问题，所以效率依然不尽如人意
- 多核多线程比单核多线程更差
  - 单核下多线程，每次释放GIL，唤醒的那个线程都能获取到GIL锁，所以能够无缝执行。
  - 多核下，CPU0释放GIL后，其他CPU上的线程都会进行竞争，但GIL可能会马上又被CPU0拿到，导致其他几个CPU上被唤醒后的线程会醒着等待到切换时间后又进入待调度状态，这样会造成线程颠簸(thrashing)，导致效率更低



Reference: [zhihu](https://zhuanlan.zhihu.com/p/20953544)

---

为什么有了GIL还要关注线程安全？

- GIL 的作用是：对于一个解释器，只能有一个thread在执行bytecode。所以每时每刻只有一条bytecode在被执行一个thread。GIL保证了bytecode 这层面上是thread safe的。

- 例子：虽然两个线程A、B由于GIL锁的存在，不会同时执行。（假设A、B功能是对一个全局变量 m 进行+1）但是A由于时间片用完切回B之前的最后一步操作可能是读取m的值，记作m1.此时B执行读取m的值，m加一，写回m，此时m的值是m1+1.又切回A，A执行加一，写回m，而写回的值是多少呢？还是m1+1.