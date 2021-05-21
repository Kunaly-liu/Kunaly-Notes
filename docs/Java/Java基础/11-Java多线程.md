# Java 多线程

[本文相关代码](Java/Java基础/Codes/ThreadDemo1.zip)

## 1. 相关概念

### 程序、进程、线程

- 程序：为了让计算机完成特定功能的一系列有序指令的集合。
- 进程：是系统进行资源分配和调度的基本单位，简单理解为，正在运行的程序。有自己的生命周期，如：正在运行的QQ，微信，word等。
- 线程：CPU的调度单位，进程中的一个实体，资源的拥有者还是进程。一个进程包含1—n个线程。

### 为什么要引进进程?

进程的引入是为了使多个程序并发执行以改善系统资源的利用率和系统的吞吐量。

### 有了进程为什么还要引入线程呢？

虽然进程能够改善系统资源的利用率和系统的吞吐量。
但是现实是：在多程序执行的情况下会生成多个进程，为了实现并发，系统会根据一定的算法进行进程切换来实现并发效果，但是进程的切换都会消耗较大的时空开销来进行系统资源的重新分配，保存和释放，如果进程一多，就会为其花费不少的处理机时间。
线程的引入就是为了减少程序并发执行时所付出的时空开销。线程本身不拥有资源。

### 进程和线程的区别联系

1. 线程是进程的一部分，它是进程内的一个执行单元。通常一个进程包含一到多个线程，一个进程的多个线程都在进程的地址空间里活动。
2. 引入线程的操作系统中，资源分配的对象是进程，而不是线程。进程仍然是拥有资源的一个独立单位 ，线程使用的资源是进程分到的资源。
3. CPU调度的基本单位是线程，即CPU是分给线程的，真正在CPU上执行的是线程。
4. 进程之间可以并发执行，而一个进程中的这些线程之间也可以并发执行。而且在并发执行的过程中，也需要协作同步。
5. 进程调度，系统需要进行进程上下文切换，需要大量的开销。线程调度，由于统一进程内的线程共享进程的资源，其切换是把线程仅有的部分资源变换即可，从而提高了系统的效率。线程切换比进程切换快得多。
6. 从一个进程得线程向另一个进程得线程切换，将引起进程的上下文切换。
7. 同一进程的多线程共享进程的所有资源，一个线程可以改变另一个线程的数据。而多进程机制则不会产生这种问题。

### 多线程

**什么是真正的多线程并发？**
线程之间互不影响。

**对于单核CPU来说，真的可以做到真正的多线程并发吗？**

- 多核CPU可以做到多线程并发。
- 但是单核CPU不能真正做到，但是可以做到一种“多线程并发”的感觉。（多个线程之间频繁切换执行，给人一种多个事情同时在做）

**多线程中线程之间内存共享吗？**

- 在java中：
- 线程之间共享堆内存和方法区内存；但是栈内存是独立，一个线程一个栈。
- 启动10个线程，会有10个栈空间每个栈之间，互不干扰，各自执行各自的，这就是多线程并发。多线程提高了程序的处理效率。
- 火车站，可以看作是一个进程，而火车站的每个售票窗口可以看作是一个线程。

## 2. 线程的生命周期

线程是一个动态执行的过程，它也有一个从产生到死亡的过程。

下图显示了一个线程完整的生命周期。

![image-20210510110218155](https://gitee.com/Kunaly/picture-bed/raw/master/img/image-20210510110218155.png)

- 新建状态:

  使用 **new** 关键字和 **Thread** 类或其子类建立一个线程对象后，该线程对象就处于新建状态。它保持这个状态直到程序 **start()** 这个线程。

- 就绪状态:

  当线程对象调用了start()方法之后，该线程就进入就绪状态。就绪状态的线程处于就绪队列中，要等待JVM里线程调度器的调度。

- 运行状态:

  如果就绪状态的线程获取 CPU 资源，就可以执行 **run()**，此时线程便处于运行状态。处于运行状态的线程最为复杂，它可以变为阻塞状态、就绪状态和死亡状态。

- 阻塞状态:

  如果一个线程执行了sleep（睡眠）、suspend（挂起）等方法，失去所占用资源之后，该线程就从运行状态进入阻塞状态。在睡眠时间已到或获得设备资源后可以重新进入就绪状态。可以分为三种：

  - 等待阻塞：运行状态中的线程执行 wait() 方法，使线程进入到等待阻塞状态。
  - 同步阻塞：线程在获取 synchronized 同步锁失败(因为同步锁被其他线程占用)。
  - 其他阻塞：通过调用线程的 sleep() 或 join() 发出了 I/O 请求时，线程就会进入到阻塞状态。当sleep() 状态超时，join() 等待线程终止或超时，或者 I/O 处理完毕，线程重新转入就绪状态。

- 死亡状态:

  一个运行状态的线程完成任务或者其他终止条件发生时，该线程就切换到终止状态。

## 3. 多线程的创建和使用

### 3.1 线程的常见方法

| **序号** | **方法描述**                                                 |
| :------- | :----------------------------------------------------------- |
| 1        | **start()** 使该线程开始执行；**Java** 虚拟机调用该线程的 run 方法。 |
| 2        | **run()** 如果该线程是使用独立的 Runnable 运行对象构造的，则调用该 Runnable 对象的 run 方法；否则，该方法不执行任何操作并返回。 |
| 3        | **setName(String name)** 改变线程名称，使之与参数 name 相同。 |
| 4        | **setPriority(int priority)**  更改线程的优先级。            |
| 5        | **setDaemon(boolean on)** 将该线程标记为守护线程或用户线程。 |
| 6        | **join(long millisec)** 等待该线程终止的时间最长为 millis 毫秒。 |
| 7        | **interrupt()** 中断线程。                                   |
| 8        | **currentThread()** 返回对当前正在执行的线程对象的引用。     |
| 9        | **getName()**  返回此线程的名称。                            |
| 10       | **getState()**  返回此线程的状态。                           |
| 11       | **join()**  等待这个线程死亡。                               |
| 12       | **sleep(long millis)**  使当前正在执行的线程以指定的毫秒数暂停（暂时停止执行），具体取决于系统定时器和调度程序的精度和准确性。 |
| 13       | **yield()**  对调度程序的一个暗示，即当前线程愿意产生当前使用的处理器。 |
| 14       | **setDaemon(boolean on)**  将此线程标记为守护线程或用户线程。 |

### 3.2 创建一个线程

Java 提供了三种创建线程的方法：

- 通过继承 Thread 类本身；
- 通过实现 Runnable 接口；
- 通过 Callable 和 Future 创建线程。

#### 3.2.1 通过继承 Thread 类

```java
package com.kun.thread.demo;
//第一种：直接继承 Thread
public class ThreadTest01 {
    public static void main(String[] args) {
        //这里是主线程，在主栈中执行
        //新建一个分支线程
        MyThread myThread = new MyThread();
        //启动线程
        /*start方法的作用:启动一个分支线程，在JVM种开辟一个新的栈空
         间，这段代码完成后瞬间就结束了，线程就启动成功了*/
        /*启动成功的线程会自动调用run方法，并且run方法在分支栈的底部
        run和main方法平级*/
        myThread.start();
        //myThread.run();//不会启动动线程（为单线程）
        for(int i=0 ;i<100;i++){
            System.out.println("主线程--->"+i);
        }
    }
}

class MyThread extends Thread{
    @Override
    public void run() {
        //编写代码，这段程序在分支线程中执行
        for(int i=0 ;i<100;i++){
            System.out.println("分支线程--->"+i);
        }
    }
}
```

#### 3.2.2 通过实现 Runnable 接口

```java
package com.kun.thread.demo;

public class ThreadTest02 {
    public static void main(String[] args) {
        //创建一个线程的对象
        MyRunnable aa = new MyRunnable();
        //将可运行的对象封装成一个线程对象
        Thread t = new Thread(aa);
        //启动线程
        t.start();
        for (int i = 0; i < 1000; i++) {
            System.out.println("主线程-->" + i);
        }
    }
}

//这并不是一个线程类，是一个可运行的类，他还不是一个线程
class MyRunnable implements Runnable {

    @Override
    public void run() {
        for (int i = 0; i < 1000; i++) {
            System.out.println("分支线程-->" + i);
        }
    }
}
```

改进（使用匿名内部类方式）：

```java
package com.kun.thread.demo;

public class ThreadTest03 {
    public static void main(String[] args) {
        Thread t = new Thread(new Runnable() {
            @Override
            public void run() {
                for (int i = 0; i < 1000; i++) {
                    System.out.println("分支线程--->" + i);
                }
            }
        });
        //启动线程
        t.start();
        for (int i = 0; i < 1000; i++) {
            System.out.println("主线程--->" + i);
        }
    }
}
```

> 为什么上面的 输出结果主线程和分支现场 有先有后，有多又少，这是为什么？
>
> - 控制台只有一个。
> - 占有CPU时间片的多少。
> - 抢时间片等等

#### 3.2.3 通过 Callable 和 Future 创建线程

1.  创建 Callable 接口的实现类，并实现 call() 方法，该 call() 方法将作为线程执行体，并且有返回值。
2.  创建 Callable 实现类的实例，使用 FutureTask 类来包装 Callable 对象，该 FutureTask 对象封装了该 Callable 对象的 call() 方法的返回值。
3.  使用 FutureTask 对象作为 Thread 对象的 target 创建并启动新线程。
4.  调用 FutureTask 对象的 get() 方法来获得子线程执行结束后的返回值。

```java
package com.kun.thread.demo;

import java.util.concurrent.Callable;
import java.util.concurrent.ExecutionException;
import java.util.concurrent.FutureTask;

public class ThreadTest04 {
    public static void main(String[] args) {
        //创建 Callable 实现类的实例
         MyCallable myCallable = new MyCallable();
        //使用 FutureTask 类来包装 Callable 对象
        FutureTask<Integer> ft = new FutureTask<>(myCallable);

        //启动分支线程
        new Thread(ft,"有返回值的分支线程").start();

        //主线程
        for (int i = 0; i < 1000; i++) {
            System.out.println("主线程-->" + i);
        }

        //输出分支线程的返回值
        try {
            System.out.println("子线程的返回值："+ft.get());
        } catch (InterruptedException e) {
            e.printStackTrace();
        } catch (ExecutionException e) {
            e.printStackTrace();
        }

    }
}

class MyCallable implements Callable{
    @Override
    public Integer call() throws Exception {
        int i = 0;
        for ( ; i < 1000; i++) {
            System.out.println("分支线程-->" + i);
        }
        return i;
    }
}
```

#### 3.2.4 创建线程的三种方式的对比

- 采用实现 Runnable、Callable 接口的方式创建多线程时，线程类只是实现了 Runnable 接口或 Callable 接口，还可以继承其他类。
- 使用继承 Thread 类的方式创建多线程时，编写简单，如果需要访问当前线程，则无需使用 Thread.currentThread() 方法，直接使用 this 即可获得当前线程。

### 3.3 获取线程名字

- 怎么获取当前线程对象?
  - 所用的方法static Thread currectThread()为静态方法。
  - Thread currentThread = Thread.currectThread();
- 获取线程对象的名字？
  - String name = 线程对象.getName();
- 修改线程对象的名字?
  - 当线程没有设置名字之前，默认有个名字Thread-0,Thread-1,Thread-2
  - 线程对象.setName(“s1”);方法修改线程的名字。

```java
package com.kun.thread.demo;

public class ThreadTest05 {
    public static void main(String[] args) {
        //以下代码出现在main方法中，所以当前线程就是主线程，获取当前线程对象
        Thread current1 = Thread.currentThread();
        System.out.println(current1.getName());
        //创建线程对象
        MyThread2 t1 = new MyThread2();
        //设置线程的名字
        t1.setName("sss");
        //获取线程的名字
        System.out.println(t1.getName());
        //创建线程对象
        MyThread2 t2 = new MyThread2();
        System.out.println(t2.getName());
        //启动线程
        t1.start();
        for(int i=0;i<10;i++){
            Thread current2 = Thread.currentThread();
            System.out.println(current2.getName()+"-->"+i);
        }
    }
}
class  MyThread2 extends Thread{
    @Override
    public void run() {
        //获取当前对象
        for (int i =0;i<1000;i++){
            //获取当前线程对象
            Thread current2 = Thread.currentThread();
            System.out.println(current2.getName()+"--->"+i);
        }
    }
}
```

### 3.4 线程优先级

- **void setPriority(int newPriotity)方法：设置线程的优先级。**
- int getPriority()方法：获取线程的优先级。
- 最低优先级1（MIN_PRIORITY)
- 最高优先级10(MAX_PRIORITY)
- 默认优先级5(NORM_PRIORITY)

```java
package com.kun.thread.demo;

public class ThreadTest06 {
    public static void main(String[] args) {
        System.out.println("main begin!");
        Thread f1 = new Thread(new Runnable() {
            @Override
            public void run() {
                for (int i = 0; i < 100; i++) {
                    System.out.println(Thread.currentThread().getName() + "-->" + i + "，优先级：" + Thread.currentThread().getPriority());
                    try {
                        Thread.sleep(1000);
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                }
            }
        });

        Thread f2 = new Thread(new Runnable() {
            @Override
            public void run() {
                for (int i = 0; i < 100; i++) {
                    System.out.println(Thread.currentThread().getName() + "-->" + i + "，优先级：" + Thread.currentThread().getPriority());
                    try {
                        Thread.sleep(1000);
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                }
            }
        });
        //设置f1线程优先级为最高
        f1.setPriority(10);
        //设置f2线程的优先级为最低
        f2.setPriority(1);
        //启动两个线程
        f1.start();
        f2.start();
    }
}
```

### 3.5 join 线程合并

join()/join(long millis)实例方法（线程合并）：使用该方法，当前线程进入阻塞状态，直到其它线程进入消亡后，才再次进入就绪状态。

```java
package com.kun.thread.demo;

public class ThreadTest07 {
    public static void main(String[] args) {
        System.out.println("main begin!");
        Thread f = new Thread(new Runnable() {
            @Override
            public void run() {
                for (int i = 0; i < 100; i++) {
                    System.out.println(Thread.currentThread().getName() + "-->" + i);
                }
            }
        });
        f.setName("ttt");
        f.start();
        //合并到当前线程，当前线程受到阻塞，直到f线程执行结束
        try {
            f.join();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        System.out.println("main over!");
    }
}
```

### 3.6 yield 线程让位

yield()方法（线程让位）：静态方法，暂停当前正在执行的线程对象（回到就绪状态，回到就绪可能会重新抢到），并执行其它对象。（让位方法，让给同等优先权的线程，否则不起作用）

```java
package com.kun.thread.demo;

public class ThreadTest08 {
    public static void main(String[] args) {
        Thread t = new Thread(new MyRunnable3());
        t.setName("t");
        t.start();
        for(int i =0;i<1000;i++){
            System.out.println(Thread.currentThread().getName()+"-->"+i);
        }
    }
}
class  MyRunnable3 implements Runnable{
    @Override
    public void run() {
        for(int i = 0; i <= 1000; i++) {
            if (i % 100 == 0){
                Thread.yield();
            }
            System.out.println(Thread.currentThread().getName()+"-->"+i);
        }
    }
}
```

## 4. 线程同步

- 同步编程模型：
  - 线程之间的执行，需要等待另一个线程执行完毕，才能执行，效率较低。线程排队执行。
- 异步编程模型：
  - 线程之间，各自执行各自的，互不影响，其实就是多线程并发。
- 如何实现多线程之间的“线程同步机制”（线程排队）？
  - 方法为:给要操作的共享资源（重要）加锁。保证一个线程对象在对它操作的时候不被其它线程干扰。
  - Java提供了一个synchronized关键字：如果线程t1遇到了synchronzied关键字，这时候自动找后面“共享资源”的对象锁，找到后，并占有这把锁，然后执行同步代码块的程序。直到执行结束，才会释放该锁。线程t2在t1没有释放锁之前，只能排队。synchronized后面小括号”数据很关键“，必须是多线程共享的数据，才能排队。
  - Synchronized关键字可以对线程对象要操作的资源（如方法，对象等）进行加锁。（同步锁）。
  - synchromized后面的小括号写什么看你想要哪几个线程同步，例如t1,t2…t5,如果你只希望t1,t2,t3,排队，你一定要在括号中写一个t1,t2,t3共享的对象，t4,t5不共享这个对象，就可以并发执行。（这就好比t1,t2,t3,为男生，共享男卫生间。t4,t5为女生就不需要在男卫生间门口排队，他们可以并发的去女卫生间执行（对于一些会去男卫生间上厕所的这里就不讨论，哈哈）。）
- java语言中，任何对象都有“一把锁”，其实就是一个标记（只是称为锁）。

### 4.1 线程安全

举例：多窗口售票

```java
package com.kun.thread.demo;

public class ThreadTest10 {
    public static void main(String[] args) {
        SellTickets sellTickets = new SellTickets();
//        Thread thread01 = new Thread(sellTickets);//第一个线程窗口
//        thread01.start();
//        Thread thread02 = new Thread(sellTickets);//第二个线程窗口
//        thread02.start();
//        Thread thread03 = new Thread(sellTickets);//第三个线程窗口
//        thread03.start();
        new Thread(sellTickets).start();
        new Thread(sellTickets).start();
        new Thread(sellTickets).start();
    }
}

class SellTickets implements Runnable {
    private int ticketNum = 100;
    private boolean loop = true;

    private  void sell() {
        if (ticketNum <= 0) {
            System.out.println("售票结束。。。");
            loop = false;
            return;
        }
        try {
            Thread.sleep(50);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        System.out.println("窗口：" + Thread.currentThread().getName() + "售出一张票，剩余票数：" + (--ticketNum));
    }

    @Override
    public void run() {
        while (loop) {
            sell();
        }
    }
}
```

出现下面情况：当票已经售卖完，仍在售票。

![image-20210510145443229](https://gitee.com/Kunaly/picture-bed/raw/master/img/image-20210510145443229.png )

**Java的三大变量哪些存在线程安全问题？**

- 实例变量（堆内存）：堆只有一个。
- 静态变量（方法区):方法区只有一个。
- 堆和方法区都是多线程共享的，所以可能存在线程安全问题。

### 4.2 Synchronized

Synchronized三种使用方法：

- 第一种:同步代码块。灵活
  Synchronized(线程共享对象）{
  同步代码块
  }
- 第二种:在实例方法上使用Synchronzed。
  表示共享对象一定是this.并且同步代码块是整个方法体。
- 第三种:在静态方法上使用Synchronized
  表示找类锁。类锁永远只有一把（保证了静态变量的安全）不管对象有多少，所以对于类锁而言，如果加类锁的话，只要属于该类的对象都是共享资源。

举例：多窗口售票（同步）

```java
package com.kun.thread.demo;

public class ThreadTest10 {
    public static void main(String[] args) {
        SellTickets sellTickets = new SellTickets();
//        Thread thread01 = new Thread(sellTickets);//第一个线程窗口
//        thread01.start();
//        Thread thread02 = new Thread(sellTickets);//第二个线程窗口
//        thread02.start();
//        Thread thread03 = new Thread(sellTickets);//第三个线程窗口
//        thread03.start();
        new Thread(sellTickets).start();
        new Thread(sellTickets).start();
        new Thread(sellTickets).start();
    }
}

class SellTickets implements Runnable {
    private int ticketNum = 100;
    private boolean loop = true;

    //同步方法
    //同一时刻 只能有一个线程访问 sell() 方法
    private synchronized void sell() {
        if (ticketNum <= 0) {
            System.out.println("售票结束。。。");
            loop = false;
            return;
        }
        try {
            Thread.sleep(50);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        System.out.println("窗口：" + Thread.currentThread().getName() + "售出一张票，剩余票数：" + (--ticketNum));
    }

    private void sell1() {
        //同步代码块
        synchronized (this) {
            if (ticketNum <= 0) {
                System.out.println("售票结束。。。");
                loop = false;
                return;
            }
            try {
                Thread.sleep(50);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            System.out.println("窗口：" + Thread.currentThread().getName() + "售出一张票，剩余票数：" + (--ticketNum));
        }
    }

    @Override
    public void run() {
        while (loop) {
            sell1();
        }
    }
}
```

### 4.3 死锁

死锁的概念:

死锁会造成程序不出异常，也不出错误，一直僵持在那里。

例子：

```java
package com.kun.thread.demo;

public class ThreadTest11 {
    public static void main(String[] args) {
        //两个线程共享o1,o2
        Object o1 = new Object();
        Object o2 = new Object();
        Thread t1 = new MyThread01(o1,o2);
        Thread t2 = new MyThread02(o1,o2);
        t1.start();
        t2.start();
    }
}

class MyThread01 extends  Thread {
    Object o1;
    Object o2;

    public MyThread01(Object o1, Object o2) {
        this.o1 = o1;
        this.o2 = o2;
    }

    @Override
    public void run() {
        synchronized (o1) {
            try {
                System.out.println(Thread.currentThread().getName()+"获得o1资源，等待o2资源");
                Thread.sleep(100);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            synchronized (o2) {
            }
        }
    }
}
class  MyThread02 extends Thread {
    Object o1;
    Object o2;

    public MyThread02(Object o1, Object o2) {
        this.o1 = o1;
        this.o2 = o2;
    }

    @Override
    public void run() {
        synchronized (o2) {
            try {
                System.out.println(Thread.currentThread().getName()+"获得o2资源，等待o1资源");
                Thread.sleep(100);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            synchronized (o1) {
            }
        }
    }
}
```

程序进入死锁，无法终止：

![image-20210510150545759](https://gitee.com/Kunaly/picture-bed/raw/master/img/image-20210510150545759.png)

- **总结：**
  - 尽量不要使用两个嵌套synchronized,容易造成死锁。
  - 对于线程调度状态的方法:destroy(),stop(),suspend()等调用后不会释放线程本身的对象锁，容易造成死锁，不建议使用。而resume方法是用来唤醒suspend方法暂定的线程，因而也不建议使用。
- **开发中如何解决线程安全问题？**
  - synchronized会使执行效率降低，让用户体验差，在不得已的时候在选取。
  - 第一种方案：尽量使用局部变量代替实例变量和静态变量。
  - 第二种方案：如果必须使实例变量，那么可以考虑创建多个对象，即不共享。一个线程一个对象。这样就没有安全问题了。（多搞几个卫生间，如果每个人都有一个卫生间，你说还需要排队吗？）
  - 第三种方案：前两者都不能用，采用synchronized，线程同步机制。

### 4.4 守护线程

- **什么是守护线程?**
  - java语言中线程分为用户线程（主线程等）和守护线程。
  - 守护线程其实就是后台线程，其中比较有代表性的是：垃圾回收线程（守护线程）
- **守护线程有什么作用呢？**
  - 比如我们的定时数据自动备份，这个需要用到计时器，当到某个特定点后就自动备份一次。所以用户线程退出后，守护线程自动退出，没有必要进行数据备份了。

例子：

```java
package com.kun.thread.demo;

public class ThreadTest012 {
    public static void main(String[] args) {
        Thread myDaemon=new MyDaemon();
        myDaemon.setName("备份数据");
        //设为守护线程
        myDaemon.setDaemon(true);
        myDaemon.start();
        //主线程
        for(int i =0 ;i<10;i++){
            System.out.println(Thread.currentThread().getName()+"-->"+i);
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}
class MyDaemon extends Thread{
    @Override
    public void run() {
        int i = 0;
        //即使是死循环，但由于改线程是守护者，当用户结束，守护线程自动终止。
        while (true) {
            System.out.println(Thread.currentThread().getName() + "-->" + (++i));
            try {
                Thread.sleep(1000);//模拟一秒记录一次
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}
```

## 5. 线程通信

### 5.1 wait 和 notify

> wait和notify方法不是线程对象的方法，是java中任何一个对象都有的方法，因为这两个方法是Object类自带的。wait方法和notify方法不是通过线程对象调用。（重点）

**Object.wait()方法的作用？**

- 当一个线程执行到wait()方法时，进入一个和该对象相关的等待池，同时失去了对象锁的拥有权，该线程进入阻塞状态，直到调用notify或notifyAll()方法将其唤醒。当前线程必须拥有该对象的锁，如果不拥有，会抛出异常，所以wait()方法必须在synchronized block中调用。（重点）

**sleep和wait区别和联系？**

- 不同点：
  1. sleep不会释放锁，wait会释放锁
  2. sleep是静态方法，可以通过类名直接调用；wait是普通方法，通过锁对象调用。
  3. sleep是Thread类的方法；wait是Object类的方法。
- 相同点：
  1. sleep和wait都会导致线程的阻塞，当阻塞结束，进入就绪态，运行时都是从断点处开始执行。
  2. 在被interrupt后，都会生成InterruptedException异常。

**Object.notify（）/notifyAll()方法的作用？**

- Object o =new Object();
- o.notify()/notifyAll()表示唤醒正在o对象等待的一个线程（优先级高的，优先被唤醒；优先级相同，随机唤醒一个）/所有线程。这个方法不会释放对象锁，这个方法同样必须有其对象锁，否则会抛出异常（IllegalMonitorStateException)。
- wait,notify,notifyAll的调用者必须是同一个对象，否则报异常。

### 5.2 生产者和消费者模型

**什么是“生产者和消费者模型”？**

- 生产线程负责生产，消费线程负责消费。
- 生产线程和消费线程要达到均衡。
- 这是一个特殊的业务需求，需要使用wait方法和notify方法。

![image-20210510152007697](https://gitee.com/Kunaly/picture-bed/raw/master/img/image-20210510152007697.png)

例子：

```java
package com.kun.thread.demo;

import java.util.ArrayList;
import java.util.List;

//List模拟仓库,容量为1，即生产一个消费一个
public class ProductConsumerDemo {
    public static void main(String[] args) {
        //创建一个仓库对象，共享的
        List list = new ArrayList();
        //创建两个线程对象
        //生产者线程
        Thread t1 = new Thread(new Producer(list));
        //消费者线程
        Thread t2 = new Thread(new Consumer(list));
        t1.setName("生产者线程：");
        t2.setName("消费者线程：");
        t1.start();
        t2.start();
    }
}
//生产线程
class Producer implements Runnable{
    //仓库
    private List list;

    public Producer(List list) {
        this.list = list;
    }

    @Override
    public void run() {
        //一直生产
        while(true) {
            synchronized (list) {//给仓库资源加锁
                if (list.size() > 0) {
                    //当前线程进入等待状态，释放锁，不放锁的话，消费者线程无法访问资源（生产者线程）
                    try {
                        list.wait();
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                }
                //程序能执行到这里说明仓库为空，可以生产
                Object obj = new Object();
                list.add(obj);
                System.out.println(Thread.currentThread().getName()+"-->"+"生产了"+ list.size() + "个"+obj +",消费者可以消费了。");
                //唤醒消费者消费
                list.notify();
            }
        }
    }
}
//消费线程
class Consumer implements Runnable{
    //同一个仓库
    private List list;
    public Consumer(List list) {
        this.list = list;
    }
    @Override
    public void run() {
        //一直消费
        while (true){
            synchronized (list){//没有得到锁，以下代码都不能执行
                if(list.size()==0){
                    //仓库空了，停止消费，消费线程进入阻塞，释放list集合的锁
                    try {
                        list.wait();
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                }
                //程序能够执行到这，说明仓库有数据，进行消费
                Object obj= list.remove(0);
                System.out.println(Thread.currentThread().getName()+"-->"+"消费了" + obj + "还剩"+list.size()+"个,生产者该生产了。。。");
                //唤醒生产者进行生产
                list.notify();

            }
        }
    }
}
```

部分执行结果：

![image-20210510152824354](https://gitee.com/Kunaly/picture-bed/raw/master/img/image-20210510152824354.png)



## 📚 References

- 菜鸟教程
- https://www.cnblogs.com/huangjiahuan1314520/p/12683889.html

