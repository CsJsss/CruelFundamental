# 二阶段提交 #
二阶段提交是为了保证分布式系统事务一致性而设计的提交协议，它假定众多节点中有且只有一个协调的coordinator node，记为CN，其他为data node，记为DN，且所有undo和redo日志持久化是可靠的。  
阶段一（投票）：  
a.CN向所有DN发出提交事务的询问；
b.所有DN接到询问后，若未遇到故障、死锁等不可抗力，应写好undo、redo日志，并做出事务正常提交的commit回应。若遇到故障等不可抗力，会做出abort回应或不回应。  
阶段二（决策）：
a.CN若收到所有DN的commit，会返回正式提交的指令，DN接到后会正式提交事务，并释放所有相关资源。然后给CN一个ack，CN正式结束当前事务。  
b.CN若收到abort，或超时收不到至少一个DN的信息，则会返回回滚指令，DN接到后会读取相应undo日志进行回滚，将redo日志重置为上一个事务的redo。然后给CN一个ack，CN正式回滚当前事务。