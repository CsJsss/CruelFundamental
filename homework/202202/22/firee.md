### C++:volatile 和 atomic 的区别

#### voaltile:

让代码保持汇编级别的一致性，即让 voaltile 的变量 在编译优化前后不会因为外部修改了这个变量而导致逻辑上的错误。

#### atomic：

让代码保持代码级别的一致性，即希望对 atomic 变量操作的每一行代码都有原子性