1. 修饰符

![修饰符](https://raw.githubusercontent.com/youminglan/Picture/main/img/20210507151653.png)

​	**default** (即默认，什么也不写）: 在同一包内可见，不使用任何修饰符。使用对象：	类、接口、变量、方法。

​	**private** : 在同一类内可见。使用对象：变量、方法。 **注意：不能修饰类（外部类）**

​	**public** : 对所有类可见。使用对象：类、接口、变量、方法

​	**protected** : 对同一包内的类和所有子类可见。使用对象：变量、方法。 **注意：不	 能修饰类（外部类）**。

​	**static** ：用来修饰类方法和类变量。

​	**final** ：用来修饰类、方法和变量，final 修饰的类不能够被继承，修饰的方法不能被	继承类重新定义，修饰的变量为常量，是不可修改的。

​	**abstract** ：用来创建抽象类和抽象方法。

​	**synchronized 和 volatile** ：主要用于线程的编程。



2. try、catch

   try就像一个网，把try{}里面的代码所抛出的异常都网住，然后把异常交给catch{}里面的代码去处理。

   最后执行finally之中的代码。无论try中代码有没有异常，也无论catch是否将异常捕获到，finally中的代码都一定会被执行。

   ```java
   try
   {
       code;
   }catch(e)
   {
       alter(e.number);
   }
   ```

   

3. Java垃圾回收机制

   垃圾回收是一种在堆内存中找出哪些对象在被使用，还有哪些对象没被使用，并且将后者回收掉的机制。

   所谓使用中的对象，指的是程序中还有引用的对象；而未使用中的对象，值得是程序中没有引用的对象，该对象占用的内存也可以被回收掉。

   Java中提供垃圾回收器，释放内存由回收器负责。

   垃圾回收步骤：

   - 标记

   垃圾回收的第一步是标记。垃圾回收器此时会找出内存哪些在使用中，哪些不是。

   ![垃圾回收标记](https://raw.githubusercontent.com/youminglan/Picture/main/img/20210507154157.png)

   上图中，蓝色表示已引用对象，橙色表示未引用对象。垃圾回收器要检查完所有的对象，才能知道哪些有被引用，哪些没。如果系统里所有的对象都要检查，那这一步可能会相当耗时间。

   - 清除

   垃圾回收的第二步是清除，这一步会删掉标记出的未引用对象。

   ![垃圾回收清除](https://raw.githubusercontent.com/youminglan/Picture/main/img/20210507154259.png)

   内存分配器会保留指向可用内存中的引用，以分配给新的对象。

   - 压缩

   垃圾回收的第三步是压缩，为了提升性能，删除了未引用对象后，还可以将剩下的已引用对象放在一起（压缩），这样就能更简单快捷地分配新对象了。

   ![垃圾回收压缩](https://raw.githubusercontent.com/youminglan/Picture/main/img/20210507154416.png)

4. Thread类

   一个进程包括由操作系统分配的内存空间，包含一个或多个线程。一个线程不能独立的存在，它必须是进程的一部分。一个进程一直运行，直到所有的非守护线程都结束运行后才能结束。

   线程从创建到最终的消亡，要经历若干个状态。一般来说，线程包括以下这几个状态：创建(new)、就绪(runnable)、运行(running)、阻塞(blocked)、time waiting、waiting、消亡（dead）。

   线程从创建到消亡之间的状态：

   ![线程从创建到消亡之间的状态](https://raw.githubusercontent.com/youminglan/Picture/main/img/20210507155244.png)

   - 新建状态(New):

     使用 **new** 关键字和 **Thread** 类或其子类建立一个线程对象后，该线程对象就处于新建状态。它保持这个状态直到程序 **start()** 这个线程。

   - 就绪状态(Runable):

     当线程对象调用了start()方法之后，该线程就进入就绪状态。就绪状态的线程处于就绪队列中，要等待JVM里线程调度器的调度。

   - 运行状态(Running):

     如果就绪状态的线程获取 CPU 资源，就可以执行 **run()**，此时线程便处于运行状态。处于运行状态的线程最为复杂，它可以变为阻塞状态、就绪状态和死亡状态。

   - 阻塞状态(Blocked):

     如果一个线程执行了sleep（睡眠）、suspend（挂起）等方法，失去所占用资源之后，该线程就从运行状态进入阻塞状态。在睡眠时间已到或获得设备资源后可以重新进入就绪状态。可以分为三种：

     - 等待阻塞：运行状态中的线程执行 wait() 方法，使线程进入到等待阻塞状态。
     - 同步阻塞：线程在获取 synchronized 同步锁失败(因为同步锁被其他线程占用)。
     - 其他阻塞：通过调用线程的 sleep() 或 join() 发出了 I/O 请求时，线程就会进入到阻塞状态。当sleep() 状态超时，join() 等待线程终止或超时，或者 I/O 处理完毕，线程重新转入就绪状态。

   - 死亡状态(Dead):

     一个运行状态的线程完成任务或者其他终止条件发生时，该线程就切换到终止状态。

     Thread类中常用的方法：

     1）start方法

     　　start()用来启动一个线程，当调用start方法后，系统才会开启一个新的线程来执行用户定义的子任务，在这个过程中，会为相应的线程分配需要的资源。

     2）run方法

     　　run()方法是不需要用户来调用的，当通过start方法启动一个线程之后，当线程获得了CPU执行时间，便进入run方法体去执行具体的任务。注意，继承Thread类必须重写run方法，在run方法中定义具体要执行的任务。

     3）sleep方法

     ​		sleep()相当于让线程睡眠，交出CPU，让CPU去执行其他的任务。

5. 进程和线程的区别

   进程

   应用程序的执行实例，有独立的内存空间和系统资源

   线程

   CPU调度和分派的基本单位，进程中执行运算的最小单位，可完成一个独立的顺序控制流程

6. super、this

   this用法：

   - 表示对当前对象的引用，在类内部当中对自己的一个引用，可以方便类中方法访问自己的属性

     ```java
     public class A{
        public A getA(){
     return this;//表示获取当前实例本身
        }
     }
     ```

   - 表示类的成员变量，而非函数参数

     ```java
     public class A{
        private　int a = 0;//位置1
        public A getA(int a){
     this.a = a;//前面this.a表示 位置1 的a，赋值=号右侧的表示参数a
        }
     }
     ```

7. Java异常类

   异常发生的原因有很多，通常包含以下几大类：

   - 用户输入了非法数据。
   - 要打开的文件不存在。
   - 网络通信时连接中断，或者JVM内存溢出。

   所有的异常类是从 java.lang.Exception 类继承的子类。Exception 类是 Throwable 类的子类，Throwable 类还有一个子类Error。Error 用来指示运行时环境发生的错误。

   ![exception-hierarchy](https://raw.githubusercontent.com/youminglan/Picture/main/img/20210507164642.png)

   异常类有两个主要的子类：IOException 类和 RuntimeException 类。

   
