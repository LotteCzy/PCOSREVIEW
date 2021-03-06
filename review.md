# 操作系统复习

## 一 操作系统引论

### 1. 操作系统概念

​       操作系统（Operation System，OS）是配置在计算机硬件上的第一层软件，是对硬件系统的收录此扩充。

​       操作系统是一组控制和管理计算机硬件和软件资源，合理的对各类作业进行调度，以及方便用户使用的程序集合。

### 2. 操作系统的类型（可以只记特点）

- 未配置操作系统的计算机系统
  **出现时间**：1945-ENIAC  电子数字积分计算机   1945~50年代中期）
  **工作方式**：
  ① 人工输入方式
  	纸带（卡片）-->输入机-->计算机-->打印结果-->取走纸带
  ② 脱机输入输出方式（off-line I/O）方式
  	<img src=".\review.assets\image-20210115211759036.png" alt="image-20210115211759036" style="zoom:50%;" />

  **特点**：用户独占全机、CPU等待人工操作（串行性），联机输入输出方式（输入输出都由主机控制）。
  **问题**：人机矛盾，CPU和I/O设备间不匹配。

- 单道批处理系统

  **出现时间**：50年代中期出现第二代晶体管计算机

  **定义**：系统对作业的处理是成批进行的，且在内存中始终只保持一道作业，故称为单道批处理系统。

  **特点**：

  ① 自动化		无人工干预

  ② 顺序性		按进入内存的先后执行

  ③ 单道性		内存中之保持了一道作业

  **工作情况**：

  <img src="review.assets\image-20210115212148272.png" alt="image-20210115212148272" style="zoom:50%;" />

- 多道批处理系统
  **多道定义**：内存中同时存在多个相互独立程序。多道技术是共享的基础。
  <img src="PCOSREVIEW\review.assets\image-20210115212507905.png" alt="image-20210115212507905" style="zoom:50%;" />

  **特征**：

  ① 多道性：内存中有多道程序，可以并大执行

  ② 无序性：完成时间与进入内存先后无关

  ③ 调度性：作业从提交到完成需要进行两次调度

  ​		作业调度：外存-->内存（选多个）

  ​		进程调度：分配处理机（选1个）
  **优点**：

  ​	资源利用率高、系统吞吐量大

  ​	**因为**(1)资源忙、(2)完成或运行不下去时才切换

  **缺点**：
  	(1)无交互能力-修改和调试极不方便
  	(2)作业平均周转时间较长

- 分时系统
  **定义**：一台主机上连接了多个终端（显示器和键盘）组成的系统，同时允许多个用户通过自己的终端，以交互方式使用计算机，共享主机中的资源。

  Windows操作系统是一个单用户多任务操作系统

  **特征**：

  (1)多路性 即同时性，宏观上同时，微观上轮流

  (2)独占性 每个用户感觉独占主机

  (3)及时性 较短时间响应(1-3秒)

  (4)交互性

- 实时系统
  **实时定义**：及时响应外部事件请求，在规定的时间完成对该事件的处理，控制所有实时任务协调一致运行。
  **特征**：
  多路性、独占性、及时性、交互性、可靠性

- 上述几种操作系统的比较
  ![image-20210115213520748](C:\Users\Lotte\Desktop\learn\PCOS\review.assets\image-20210115213520748.png)

  批处理、分时系统、实时系统是三种基本的操作系统。

  OS的进一步发展：微机OS、嵌入式OS、网络OS、分布式OS、移动OS、智能化OS

- 微机操作系统的发展
  

### 3. 操作系统的功能

处理机管理功能、储存器管理、设备管理和文件管理等基本功能。此外，为了方便用户使用OS，还需向用户提供方便的用户接口。

### 4. 操作系统的特征

并发、共享、虚拟、异步四个基本特征，其中并发和共享是最基本的特征（四个基本特征想看的话看书P13）

## 二 进程管理

### 1. 程序、进程的区别和联系（概念、特征等）

**区别**：

​	① 进程是动态的，程序是静态的：程序是有序代码的集合；进程是程序的执行。

​	② 进程是暂时的，程序的永久的：进程是一个状态变化的过程，程序可长久保存。

​	③ 进程与程序的组成不同：进程的组成包括程序、数据和进程控制块（即进程状态信息）。

​	④ 进程与程序的对应关系：通过多次执行，一个程序可对应多个进程；通过调用关系，一个进程可包括多个程序。

**进程的特征**：

​	结构性：由程序+数据+进程控制块组成了进程实体, 称之为进程映像。进程控制块是进程存在的标志。

​	动态性:进程是进程实体的执行过程, 它由创建而产生, 由调度而执行,因某事件而暂停, 由撤销而消亡。在生命周期内, 进程在三种基本状态之间动态转换

​	并发性: 多个进程同时存于内存中,一起向前推进,并发执行

​	独立性: 进程是独立获得资源和独立调度的基本单位

​	异步性: 各进程都各自独立的不可预知的速度向前推进

### 2. 并发和并行执行的区别

并行性是指两个或多个事件再同一时刻发生。

并发性是指两个或多个事件在同一时间间隔内发生。

### 3. 进程的概念以及与程序的区别

**进程定义**：

​	(1)进程是程序的一次执行。

​	(2)进程是可以和别的计算并发执行的计算。

​	(3)进程可定义为一个数据结构及能在其上进行操作的一个程序。

​	(4)进程是一个程序及其数据在处理机上顺序执行时所发生的活动。

​	(5)进程是程序在一个数据集合上运行的过程，它是系统进行资源分配和调度的一个独立单位。

​	(6)进程是一个具有独立功能的程序对某个数据集在处理机上的执行过程和分配资源的基本单位。

**区别**：(问题1 84写了吗)

### 4. 进程的描述

**PCB（进程控制块）：系统感知进程存在的唯一实体** 

为了使参与并发执行的每个程序（含数据）都能独立运行，在操作系统中必须为之配置一个专门的数据结构，称为进程控制块（process control Block， PCB）。系统利用PCB来描述进程的基本情况和活动进程，进而控制和管理进程。这样，由程序块、相关的数据段和PCB三部分便构成了进程实体（又称进程映像）。

### 5. 进程的三种基本状态及转换、进程的阻塞与唤醒

**三种基本状态**：就绪（Ready）、运行（Running）、阻塞（Block）
<img src="C:\Users\Lotte\Desktop\learn\PCOS\review.assets\image-20210115222055191.png" alt="image-20210115222055191" style="zoom: 33%;" />

**三种状态的转换**：

① 就绪 → 运行
调度：调度程序选择一个新的进程运行

② 执行 → 就绪
超时：运行进程用完时间片被中断, 在抢占调度方式中, 因为一高优先级进程进入就绪状态

③ 执行 → 阻塞
I/O请求：当进程发生I/O请求或等待某事件时

④ 阻塞 → 就绪
I/O完成：当I/O完成或所等待的事件发生时

<img src="C:\Users\Lotte\Desktop\learn\PCOS\review.assets\image-20210115222203941.png" alt="image-20210115222203941" style="zoom: 67%;" />

**进程的阻塞与唤醒**：
有下述几类事件会引起进程阻塞或被唤醒：
 　(1) 向系统请求共享资源失败。
 　(2) 等待某种操作的完成。
 　(3) 新数据尚未到达。
 　(4) 等待新任务的到达

### 6. 进程之间的关系

**互斥（间接制约）和同步（直接制约）**

在多道程序环境下，当程序并发执行时，由于资源共享和进程合作，使同处于一个系统中的诸进程之间可能存在着以下两种形式的制约关系。
1) 间接相互制约关系 		共享资源
同处于一个系统中的进程，通常都共享着某种系统资源，如共享CPU、共享I/O设备等。所谓间接相互制约即源于这种资源共享。
2) 直接相互制约关系		 进程合作
这种制约主要源于进程间的合作

### 7. 进程互斥（直接看例题）

临界资源：一次只能允许一个进程使用，若多个进程同时使用，则可能造成系统的混乱。
临界区：每个进程中访问临界资源的那段代码。

**用P、V原语实现进程的互斥。**

### 8. 进程同步（直接看例题）

公用信号量（互斥信号量 ）（mutex）：为使多个进程能互斥地访问某临界资源，只需为该资源设置一互斥信号量mutex，并设其初始值为1，然后将各进程访问该资源的临界区CS置于wait(mutex)和signal(mutex)操作之间即可。

这样，每个要进入该临界资源的进程，在进入临界区之前，都要先对mutex执行wait操作，若该资源此刻未被访问，本次的wait操作必然成功的，进程可以进入自己的临界区，这时若再有其它进程也想要进入自己的临界区，再对mutex执行wait操作必定会失败，此时该进程阻塞，从而保证了该临界资源能被互斥地访问。

公用信号量 用来实现进程间的互斥，初值为1，允许它所联系的一组进程对它执行P/V操作。

私用信号量 用来实现进程间的同步，初值为0或者某个正整数，仅允许拥有它的进程对其执行P/V操作。

**用P、V原语实现进程的同步。**

### 9. 进程通信

**概念：**

进程通信:是指进程之间的信息交换。

低级通信（互斥、同步）
	利用信号量机制实现进程间的数据传递。
	缺点：1、效率低；2、对用户不透明。

高级通信（进程通信）
	进程之间利用OS提供的一组通信命令，高效地传送大量数据的信息交换方式。
优点：高效，方便，简化了通信程序的设计。

**分类**：

高级通信机制可分为：**共享存储器系统**、**管道通信系统**、**消息传递系统**和**客户机-服务器**四大类。

**共享存储器系统**：
在共享存储器系统中，相互通信的进程共享某些数据结构或共享存储区，进程之间能够通过这些空间进行通信。据此，又可把它们分成以下两种类型：
  (1) 基于共享数据结构的通信方式。
  (2) 基于共享存储区的通信方式。存在

**管道通信系统（首创于UNIX系统）**：

​	管道（Pipe文件）：用于连接一个读进程和一个写进程以实现他们之间通信的一个共享文件。

​	管道通信：发送进程和接收进程利用管道进程通信。

​	向管道(共享文件)提供输入的发送进程(即写进程)以字符流形式将大量的数据送入管道。

​	接受管道输出的接收进程(即读进程)则从管道中接收(读)数据。

​	管道机制必须提供以下三方面的协调能力：

​	① 互斥，即当一个进程正在对pipe执行读/写操作时，其它(另一)进程必须等待。

​	② 同步，指当写(输入)进程把一定数量(如4 KB)的数据写入pipe，便去睡眠等待，直到读(输出)进程取走数据后再把它唤醒。当读进程读一空pipe时，也应睡眠等待，直至写进程将数据写入管道后才将之唤醒。

​	③ 确定对方是否存在，只有确定了对方已存在时才能进行通信。

**消息传递系统：**

​	通信的数据封装在消息中，并利用操作系统提供的一组通信命令(原语)，在进程间进行消息传递，完成进程间的数据交换。

​	直接通信方式

<img src="C:\Users\Lotte\Desktop\learn\PCOS\review.assets\image-20210115230921096.png" alt="image-20210115230921096" style="zoom:50%;" />

​	间接通信方式

<img src="C:\Users\Lotte\Desktop\learn\PCOS\review.assets\image-20210115230934589.png" alt="image-20210115230934589" style="zoom:50%;" />

**客户机-服务器系统：**

1) 套接字(Socket)
 　套接字起源于20世纪70年代加州大学伯克利分校版本的UNIX(即BSD Unix)，是UNIX 操作系统下的网络通信接口。一开始，套接字被设计用在同一台主机上多个应用程序之间的通信(即进程间的通信)，主要是为了解决多对进程同时通信时端口和物理线路的多路复用问题。随着计算机网络技术的发展以及UNIX 操作系统的广泛使用，套接字已逐渐成为最流行的网络通信程序接口之一。
2) 远程过程调用和远程方法调用
 　远程过程(函数)调用RPC(Remote Procedure Call)，是一个通信[协议](http://zh.wikipedia.org/wiki/網絡傳輸協議)，用于通过网络连接的系统。该协议允许运行于一台主机(本地)系统上的进程调用另一台主机(远程)系统上的进程，而对程序员表现为常规的过程调用，无需额外地为此编程。如果涉及的软件采用[面向对象编程](http://zh.wikipedia.org/wiki/面向对象编程)，那么远程过程调用亦可称做远程方法调用。

### 10. 死锁问题

定义、起因、四个必要条件。

**定义：**所谓死锁（Deadlock），是指多个进程因竞争资源而造成的一种僵局，若无外力作用，这些进程都将永远不能再向前推进。各并发进程彼此等待对方拥有的资源，且在得到对方资源前不释放自己的资源。

**起因：**
① 竞争资源。当系统中供多个进程共享的资源如打印机、公用队列等，其数目不足以满足诸进程的需要时，会引起诸进程对资源的竞争而产生死锁。
② 进程间推进顺序非法。进程在运行过程中，请求和释放资源的顺序不当，也同样会导致产生进程死锁。

**四个必要条件：**

① 互斥条件
一个资源一次只能被一个进程使用。

② 请求和保持条件（部分分配）
保留已经得到的资源，还要求其它的资源。

③ 不可抢占条件
资源只能被占有者释放，不能被其它进程强行抢占。

④ 循环等待条件（循环等待）
系统中的进程形成了环形的资源请求链。

虽然进程在运行过程中可能会发生死锁，但产生进程死锁是必须具备一定条件的。产生死锁必须同时具备上面四个必要条件，只要其中任一个条件不成立，死锁就不会发生。

**死锁预防和死锁避免的措施：**

**死锁预防：**破坏产生死锁的四个必要条件中的一个或几个，以避免发生死锁。

互斥条件是非共享设备所必须的，不仅不能改变，还应加以保证，因此主要是破坏产生死锁的后三个条件

**死锁避免：**属于事先预防的策略，但并不是事先采取某种限制措施，破坏产生死锁的必要条件，而是在资源动态分配过程中，防止系统进入不安全状态，以避免发生死锁。这种方法所施加的限制条件较弱，可能获得较好的系统性能，目前常用此方法来避免发生死锁。

**银行家算法的分析：**看书

### 11. 作业调度算法（FCFS、RR、SJF、HRN），主要计算作业周转时间与平均带权周转时间。

习题有。

## 三 存储管理

### 1. 地址变换：又称地址重定位（地址映射）



### 2. 覆盖和交换技术：能够实现内存的扩展，即实现虚拟内存，动态分区管理三大分配策略。

### 3. 页式管理

###  借助页表实现逻辑地址到物理地址转换、页面淘汰算法（FIFO、OPT、LRU、LFU）、Belady现象、如何划分虚拟逻辑空间和物理地址空间的页号和页大小的二进制位。

### 4. 段式和段页式管理

### 借助段表和段页表实现地址转换、段页式管理访问内存次数等等

### 5. 局部性原理和抖动问题（与Belady的区别）

### 6. 页式管理、段页式管理访问内存次数的计算以及访问时间的计算

### 7. 缺页率的计算

 

## 四 设备管理

### 1. 数据传输控制方式（程序、中断、DMA和通道方式）的特征

### 2. 中断技术（内中断与外中断）

### 3. 设备分配数据结构

### 4. 缓冲技术 

 

## 五 文件系统

### 1. 文件物理存储结构（三种类型）

### 2. 文件存储空间管理（成组链法的磁盘空间的分配和回收、位示图）

### 3. 磁盘调度算法（计算磁道移动次数、数据块传输时间、SCAN和CSCAN算法）

### 4. 根据文件的索引结构如何计算文件的大小

### 5. RAID技术。

​                                                  

## 六  操作系统接口

### 1. 操作系统给用户提供的接口

（命令、系统调用（编程）接口）

### 2. 系统调用的基本概念

（系统态和用户态）

