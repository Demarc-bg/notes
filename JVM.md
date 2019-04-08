# JVM
## JVM 运行时数据区域

#### java内存模型

java虚拟机在执行java程序时，会把所管理的内存分成若干个不同的数据区域：

- stack(栈区)：主要保存基本数据类型（char、byte、short、int、long、float、double、boolean）以及对象的引用，数据可以共享，速度仅次于寄存器(register)，快于堆
- heap(堆区)：用于存储对象

#### Heap区

- Shared among all jvm threads
- Mark：https://tech.meituan.com/2017/12/29/jvm-optimize.html 美团整理文档
- Method area: 
- Shared among all jvm threads
- stores per-class structures, including run-time constant pool, field, and method date, and the code for methods and constructors
- created on jvm start-up and is logically part of the heap
- Run-time Constant Pool
  - constains several kinds of constants, ranging from numeric literals and field references at run-time.
  - is constructed when the class or interface is created by jvm

#### HotSpot VM Heap area内存结构

采用分代的思想，主要分为新生代Young、老年代Old、持久代Perm

- **分代收集算法** ：分代的思想是根据各个年代的特点采用合适的GC算法

- Young generation：
  - 复制算法 Minor GC：
    - 大多数对象在新生代中创建，其中很多生命周期都很短，因此选用成本并不高的复制算法，也就是说对象留存率不高的话使用复制算法很好
    - 包括Eden、S1、S2三部分内存区域。
    - Eden满了以后，会调用Minor GC。在经历Minor GC之后，多数对象都被销毁了，内存被回收，少数留下的对象会被复制到S1、S2中的一个。主要是复制过程，把留下对象的全部复制到Survivor区内，并更新对象的内存引用地址为新的Survivor内存地址
    - 晋升： 每经历一次Minor GC的过程，Survivor区幸存对象的年龄都会加一，当它超过预设值MaxTenuringThreshold时，这个对象就会从Survivor区被移动到Old区，这个过程称为晋升
    - 缺点： 内存利用率不高，需要克服50%内存浪费情况
    - 改进：扩大Eden区。扩大即意味着扫描Eden区的时间间隔变长，原本应该复制到Survior区的对象因     时间变成已被回收，因此复制过程中的有效对象比例增高
- Old generation：
  - Major GC ： 标记-清理、标记-整理
    - 标记-清理：
      - 也被称为tracing garbage collector，它要把程序能直接、间接访问到的所有对象都标记一次，主要分为Mark和Sweep阶段
      - 算法流程：
        - Mark是指将所有root 引用到的所有对象都mark为true（包括间接引用的对象）
        - Sweep是指将所有mark为True的对象改为False，否则就清除该对象
      - 标记：遍历GC-root，将存活的对象标记
      - 清理：清除未被标记的对象
      - 优点：即使存在循环引用，Mark过程也可以完成
      - 缺点：
        - 内存碎片较多，需要维护一个空闲表，不利于再次分配利用
        - 在Mark-Sweep算法运行时，正常的程序会被挂起
    - 标记-整理：
      - 标记：遍历GC-root，将存活的对象标记
      - 整理：移动所有存活的对象，按照内存地址次序依次排序，然后将末端内存地址以后的内存全部回收
      - 优点：整理阶段后，存活对象即在连续的内存空间上，不会产生内存碎片，有利于再次分配空间
      - 缺点：时间开销较大，比标记-清除多一个移动存活对象的过程，
- Perm generation：
  - 主要存放元数据，类似于jvm Heap区的method方法，存放class、method的结构信息，与gc要回收的对象关系不大，因此可忽略
- 全部GC使用的方法为Full GC

可达性分析