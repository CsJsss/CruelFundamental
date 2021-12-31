## 优先级反转及解决方式

低优先级任务持有高优先级任务所需要的共享资源，高优先级任务由于缺乏资源处于受阻状态，一直等低优先级任务释放任务为止。低优先级获得CPU时间少，如果有优先级处于两者之间的任务，且不需要那个共享资源，则该中优先级任务超过这两个任务而获得CPU时间。如果高优先级等待资源不是阻塞等待，而是忙循环，低优先级无法获得CPU时间，无法执行及释放资源，导致高优先级任务无法获得资源。

解决方法：1.设置优先级上限（进入临界区的进程将获得高优先级） 2.优先级继承（低优先级进程暂时获得优先级别，释放资源之后回到原来的优先级别。 3.中断禁止