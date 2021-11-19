# Paxos原理 #
Paxos的目的是在分布式系统随时随地有节点失效的场景下，在系统内剩余有效节点对某个value尽快达成一致。值的提出者叫proposer(P)，接受者叫Acceptor(A)。值需要在众多A中按少数服从多数原则达成一致。有以下二阶段操作  
1.第一阶段：任意P就某个value发出提案都得对过半数的A发出提案，每个A收到后，按提案发出的时间戳/编号做出如下反应：

    i.若不是最新提案，不响应。
    ii.若该提案是接到的最新提案，且A仍处在第一阶段，则表示进入预备模式，对对应的P进行响应，响应里面带上次新的lastValue，并不再接受比这个提案的时间戳更早的任意提案。
    iii.若该提案是接到的最新提案，但A处在第二阶段，则回复已接受的valueAccepted。
2.第二阶段：  

    i.若没有过半A响应，P回到第一阶段。
    ii.若过半A响应第一阶段中的ii，则P进入第二阶段，发出值为value的接受请求，若A在两个阶段之间没有接受到其他P的更新的提案，则回复进入接受模式，该A最终接受本value。
    iii.若过半A响应，但其中相当部分为第一阶段中的iii，则P进入第二阶段，发出值为valueAccepted接受请求，相当于是顺从了其他某个P，尽可能快地达到一致。
    
3.保证活性：  

    i.选定主proposer，防止两个完全对等的P在第一阶段形成死锁、相互阻止对方进入第二阶段。