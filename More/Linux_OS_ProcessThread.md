# 进程与线程

操作系统最核心的概念是进程，它是对正在运行的程序的一个抽象。一个进程就是一个正在执行程序的实例，包括程序计数器、寄存器和变量的当前值。


# 进程

1. 线程作为调度和分配的基本单位，进程作为拥有资源的基本单位
2. 不仅进程之间可以并发执行，同一个进程的多个线程之间也可并发执行
3. 进程是拥有资源的一个独立单位，线程不拥有系统资源，但可以访问隶属于
进程的资源.
4. 在创建或撤消进程时，由于系统都要为之分配和回收资源，导致系统的开销
明显大于创建或撤消线程时的开销。


## 进程共享

线程共享的内容包括：

* 进程 代码段
* 进程 数据段
* 进程打开的文件描述符、
* 信号的处理器
* 进程的当前目录
* 进程用户 ID 与进程组 ID    

线程独有的内容包括：

* 线程 ID
* 寄存器组的值
* 线程的堆栈
* 错误返回码
* 线程的信号屏蔽码

## 进程间通信（IPC）

Linux 下进程通信有如下的目的：

1. 数据传输，一个进程需要将它的数据发送给另一个进程，发送的数据量在一个字节到几M之间；
2. 共享数据，多个进程想要操作共享数据，一个进程对数据的修改，其他进程应该立刻看到；
3. 通知事件，一个进程需要向另一个或一组进程发送消息，通知它们发生了某件事情；
4. 资源共享，多个进程之间共享同样的资源。为了做到这一点，需要内核提供锁和同步机制；
5. 进程控制，有些进程希望完全控制另一个进程的执行（如Debug进程），此时控制进程希望能够拦截另一个进程的所有陷入和异常，并能够及时知道它的状态改变。

系统进行进程间通信（IPC）的时候，可用的方式包括信号量、共享内存、消息队列、管道、信号（signal）、套接字(socket)等形式。

Linux中，与IPC相关的命令包括：ipcs、ipcrm（释放IPC）。IPCS命令是Linux下显示进程间通信设施状态的工具。

* ipcs -m: 输出有关共享内存(shared memory)的信息
* ipcs -q: 输出有关信息队列(message queue)的信息

Linux 线程间通信：互斥量（mutex），信号量，条件变量

# 线程



# 进程与线程

下面主要从调度、并发性、系统开销、拥有资源等方面来对线程与进程进行比较。

1. 调度：在传统的操作系统中，CPU调度分派和资源分配的基本单位都是进程。而在引入线程的操作系统中，则把线程作为 CPU 调度和分派的基本单位，而进程作为资源拥有的基本单位。这样传统进程的两个属性分开，线程基本上不拥有资源，可以轻装运行，从而显著提高了系统的并发性。在同一进程中线程的切换不会引起进程的切换，从而避免了昂贵的系统调用。但从一个进程中的线程切换到另一个进程中的线程时，依然会引起进程切换。
2. 并发性：在引入线程的操作系统中，不仅进程之间可以并发执行，而且在一个进程中的多个线程之间也可以并发执行，使得操作系统具有更好的并发性，从而能更加有效地使用系统资源和提高系统的吞吐量。  
3. 拥有资源：不论是传统的操作系统，还是引入了线程的操作系统，进程都是拥有资源的一个基本单位，它可以拥有自己的资源。一般地说，线程自己不拥有系统资源（也有一点必不可少的资源）。但它可以访问其隶属进程的资源，即一个进程的代码段、数据段及所拥有的系统资源（如已打开的文件、I/O设备等），可供该进程中的所有线程所共享。
4. 系统开销：在创建或撤销进程时，系统都要为之分配和回收进程控制块、内存空间、I/O设备等，因此操作系统所付出的开销显著地大于创建或撤销线程时的开销。类似地，在进行进程切换时，涉及到当前进程CPU环境的保存及新被调度运行进程CPU环境的设置。而线程的切换只需要保存和设置少量寄存器地内容，不涉及存储器管理方面的操作。可见，进程切换的开销也远大于线程切换的开销。此外，由于同一个进程中的多个线程具有相同的地址空间，在同步和通信的实现方面线程也比进程容易。在一些操作系统中，线程的切换、同步和通信都无须操作系统内核的干预。
  
# 参考
[进程与线程的一个简单解释](http://www.ruanyifeng.com/blog/2013/04/processes_and_threads.html)  
[Linux的IPC命令](http://www.cnblogs.com/cocowool/archive/2012/05/22/2513027.html)  


