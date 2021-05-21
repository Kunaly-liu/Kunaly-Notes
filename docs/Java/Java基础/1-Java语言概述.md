# Java语言概述

## 1. 基础常识

### 1.1 软件

**软件**：软件分为`系统软件`和`应用软件`。

- **系统软件**是负责管理计算机系统中各种独立的硬件，使得它们可以协调工作。系统软件使得计算机使用者和其他软件将计算机当作一个整体而不需要顾及到底层每个硬件是如何工作的。
- **应用软件**是为了某种特定的用途而被开发的软件。它可以是一个特定的程序，比如一个浏览器。也可以是一组功能联系紧密，可以互相协作的程序的集合，比如微软的Office软件。也可以是一个由众多独立程序组成的庞大的软件系统，比如AutoCAD。

**与用户交互的方式**：图形化界面，命令行操作。

### 1.2 计算机语言

1. **第一代语言：**机器语言，指令以二进制代码的形式存在。

2. **第二代语言：**汇编语言，使用助记符表示一条条机器指令。

3. **第三代语言：**高级语言，如：

   - C,Pascal,Fortran等 ： 面向过程的语言
   
   - C++ : 面向过程/面向对象  
   
   - Python，JAVA : 面向对象的高级

## 2. JAVA语言简介

### 2.1 概述

Java 是由 Sun Microsystems 公司于 1995 年 5 月推出的 Java 面向对象程序设计语言和 Java 平台的总称。由 James Gosling和同事们共同研发，并在 1995 年正式推出。后来 Sun 公司被 Oracle （甲骨文）公司收购，Java 也随之成为 Oracle 公司的产品。

Java之父Jgosling团队在开发"Green"项目时，发现C缺少垃圾回收系统，还有可移植的安全性、分部程序设计、和多线程功能。最后他们想要一种易于移植到各种设备上的平台。

Java最初的命名为Oak(橡树)，当时的目的是和家电一起使用。

#### 2.1.1 JAVA发展历史

- 1995 年 5 月 23 日，Java 语言诞生
- 1996 年 1 月，第一个 JDK-JDK1.0 诞生
- 1996 年 4 月，10 个最主要的操作系统供应商申明将在其产品中嵌入 JAVA 技术
- 1996 年 9 月，约 8.3 万个网页应用了 JAVA 技术来制作
- 1997 年 2 月 18 日，JDK1.1 发布
- 1997 年 4 月 2 日，JavaOne 会议召开，参与者逾一万人，创当时全球同类会议规模之纪录
- 1997 年 9 月，JavaDeveloperConnection 社区成员超过十万
- 1998 年 2 月，JDK1.1 被下载超过 2,000,000次
- 1998 年 12 月 8 日，JAVA2 企业平台 J2EE 发布
- 1999 年 6月，SUN 公司发布 Java 的三个版本：标准版（JavaSE, 以前是 J2SE）、企业版（JavaEE 以前是 J2EE）和微型版（JavaME，以前是 J2ME）
- 2000 年 5 月 8 日，JDK1.3 发布
- 2000 年 5 月 29 日，JDK1.4 发布
- 2001 年 6 月 5 日，NOKIA 宣布，到 2003 年将出售 1 亿部支持 Java 的手机
- 2001 年 9 月 24 日，J2EE1.3 发布
- 2002 年 2 月 26 日，J2SE1.4 发布，自此 Java 的计算能力有了大幅提升
- 2004 年 9 月 30 日 18:00PM，J2SE1.5 发布，成为 Java 语言发展史上的又一里程碑。为了表示该版本的重要性，J2SE1.5 更名为 Java SE 5.0
- 2005 年 6 月，JavaOne 大会召开，SUN 公司公开 Java SE 6。此时，Java 的各种版本已经更名，以取消其中的数字 "2"：J2EE 更名为 Java EE，J2SE 更名为 Java SE，J2ME 更名为 Java ME
- 2006 年 12 月，SUN 公司发布 JRE6.0
- 2009 年 04 月 20 日，甲骨文 74 亿美元收购 Sun，取得 Java 的版权。
- 2010 年 11 月，由于甲骨文对于 Java 社区的不友善，因此 Apache 扬言将退出 JCP。
- 2011 年 7 月 28 日，甲骨文发布 Java7.0 的正式版。
- 2014 年 3 月 18 日，Oracle 公司发表 Java SE 8。
- 2017 年 9 月 21 日，Oracle 公司发表 Java SE 9
- 2018 年 3 月 21 日，Oracle 公司发表 Java SE 10
- 2018 年 9 月 25 日，Java SE 11 发布
- 2019 年 3 月 20 日，Java SE 12 发布

#### 2.1.2 JAVA体系分类

- JavaSE（J2SE）（Java2 Platform Standard Edition，java平台标准版），JAVA核心库类+GUI(不使用了)
- JavaEE(J2EE)(Java 2 Platform,Enterprise Edition，java平台企业版)，企业级开发
- JavaME(J2ME)(Java 2 Platform Micro Edition，java平台微型版)，手机开发(现在被Android所取代)
- Java Card (Applet) 小家电中使用

#### 2.1.3 JAVA应用领域

- 企业级开发：JAVA后台
- Android：客户端
- 移动领域应用：手机、PDA、机顶盒、汽车通信设备
- 大数据等

#### 2.1.4 JAVA主要特性

- **Java 语言是简单的：**

  Java 语言的语法与 C 语言和 C++ 语言很接近，使得大多数程序员很容易学习和使用。另一方面，Java 丢弃了 C++ 中很少使用的、很难理解的、令人迷惑的那些特性，如操作符重载、多继承、自动的强制类型转换。特别地，Java 语言不使用指针，而是引用。并提供了自动分配和回收内存空间，使得程序员不必为内存管理而担忧。

- **Java 语言是面向对象的：**

  Java 语言提供类、接口和继承等面向对象的特性，为了简单起见，只支持类之间的单继承，但支持接口之间的多继承，并支持类与接口之间的实现机制（关键字为 implements）。Java 语言全面支持动态绑定，而 C++语言只对虚函数使用动态绑定。总之，Java语言是一个纯的面向对象程序设计语言。

- **Java语言是分布式的：**

  Java 语言支持 Internet 应用的开发，在基本的 Java 应用编程接口中有一个网络应用编程接口（java net），它提供了用于网络应用编程的类库，包括 URL、URLConnection、Socket、ServerSocket 等。Java 的 RMI（远程方法激活）机制也是开发分布式应用的重要手段。

- **Java 语言是健壮的：**

  Java 的强类型机制、异常处理、垃圾的自动收集等是 Java 程序健壮性的重要保证。对指针的丢弃是 Java 的明智选择。Java 的安全检查机制使得 Java 更具健壮性。

- **Java语言是安全的：**

  Java通常被用在网络环境中，为此，Java 提供了一个安全机制以防恶意代码的攻击。除了Java 语言具有的许多安全特性以外，Java 对通过网络下载的类具有一个安全防范机制（类 ClassLoader），如分配不同的名字空间以防替代本地的同名类、字节代码检查，并提供安全管理机制（类 SecurityManager）让 Java 应用设置安全哨兵。

- **Java 语言是体系结构中立的：**

  Java 程序（后缀为 java 的文件）在 Java 平台上被编译为体系结构中立的字节码格式（后缀为 class 的文件），然后可以在实现这个 Java 平台的任何系统中运行。这种途径适合于异构的网络环境和软件的分发。

- **Java 语言是跨平台的：**

  Java可以根据JVM来实现跨平台。只要在需要运行java应用程序的操作系统上，先安装一个java虚拟机（JVM）即可。由JVM来负责java程序在该系统中运行。（一次编译，到处运行）

- **Java 语言是可移植的：**

  这种可移植性来源于体系结构中立性，另外，Java 还严格规定了各个基本数据类型的长度。Java 系统本身也具有很强的可移植性，Java 编译器是用 Java 实现的，Java 的运行环境是用 ANSI C 实现的。

- **Java 语言是解释型的：**

  如前所述，Java 程序在 Java 平台上被编译为字节码格式，然后可以在实现这个 Java 平台的任何系统中运行。在运行时，Java 平台中的 Java 解释器对这些字节码进行解释执行，执行过程中需要的类在联接阶段被载入到运行环境中。

- **Java 是高性能的：**

  与那些解释型的高级脚本语言相比，Java 的确是高性能的。事实上，Java 的运行速度随着 JIT(Just-In-Time）编译器技术的发展越来越接近于 C++。

- **Java 语言是多线程的：**

  在 Java 语言中，线程是一种特殊的对象，它必须由 Thread 类或其子（孙）类来创建。通常有两种方法来创建线程：其一，使用型构为 Thread(Runnable) 的构造子类将一个实现了 Runnable 接口的对象包装成一个线程，其二，从 Thread 类派生出子类并重写 run 方法，使用该子类创建的对象即为线程。值得注意的是 Thread 类已经实现了 Runnable 接口，因此，任何一个线程均有它的 run 方法，而 run 方法中包含了线程所要运行的代码。线程的活动由一组方法来控制。Java 语言支持多个线程的同时执行，并提供多线程之间的同步机制（关键字为 synchronized）。

- **Java 语言是动态的：**

  Java 语言的设计目标之一是适应于动态变化的环境。Java 程序需要的类能够动态地被载入到运行环境，也可以通过网络来载入所需要的类。这也有利于软件的升级。另外，Java 中的类有一个运行时刻的表示，能进行运行时刻的类型检查。

#### 2.1.5 与C语言和C++的关系

Java可以看成是类C语言发和衍生的产物；

Java语言的变量变量声明、操作符形式、参数传递、流程控制等方面和C语言、C++语言完全相同。

Java继承了C++语言现象对象技术的核心，舍弃了C语言中容易引起错误的指针（以引用取代），运算符重载、多重继承（以接口取代）等特性、增加了垃圾回收器功能用于回收不再引用的对象所占据的内存空间。

## 3. Java运行机制及运行过程

### 3.1 核心机制

Java虚拟机（JVM）、垃圾收集机制（GC）。

### 3.2 运行过程

第一步：代码编写。

第二步：java源文件（以.java结尾的文件）编译。

第三步：java字节码（以.class结尾的文件）运行。

在dos命令窗口下执行java程序：

`javac  java原文件名.java`

`java  java字节码文件名`

### 3.3 运行原理

字节码文件运行在JVM上，JVM运行在操作系统（windows、linux、mac）上，操作系统作用在硬件平台上，同一个Java程序在不同操作系统的JVM中执行，这样就实现了Java程序的跨平台性。

## 4. JAVA语言环境搭建

### 4.1 JDK、JRE、JVM简介

在安装过程中我们会看见 JDK 和 JRE 这两个名词，它们到底是什么呢？

首先，我们需要知道 Java 程序其实是运行在JVM (Java虚拟机) 上的，使用 Java 编译器编译 Java 程序时，生成的是与平台无关的字节码，这些字节码只面向 JVM。不同平台的 JVM 都是不同的，但它们都提供了相同的接口，这也正是 Java 跨平台的原因。其和 JDK、JRE 的关系如下所示：

JDK(Java开发工具包) = JRE(Java运行环境) + 开发工具集（例如Javac编译工具等）

JRE(Java运行环境) = JVM (Java虚拟机) + Java SE 标准类库

#### 4.1.1 JDK

**JDK（Java Development Kit）**：是 Java 的标准开发工具包（**普通用户只需要安装 JRE 来运行 Java 程序。而程序开发者必须安装 JDK 来编译、调试程序**）。它提供了编译、运行 Java 程序所需的各种工具和资源，包括 Java 编译器、Java 运行环境 JRE，以及常用的 Java 基础类库等，是整个 Java 的核心

下图是 Java 8 中 JDK 的安装目录

<img src="https://gitee.com/Kunaly/picture-bed/raw/master/img/image-20210112143213352.png" alt="image-20210112143213352" style="zoom:50%;" />

- `bin` 文件里面存放了JDK的各种开发工具的可执行文件，主要的是编译器 (`javac.exe`)
- `db` 文件是一个先进的全事务处理的基于 Java 技术的数据库（jdk 自带数据库 db 的使用）
- `include` 文件里面是 Java 和 JVM 交互用的头文件
- `jre` 为 Java 运行环境
- `lib` 文件存放的是 JDK 工具命令的实际执行程序

#### 4.1.1 JRE

**JRE（Java runtime environment）**： 是运行基于 Java 语言编写的程序所不可缺少的运行环境，用于解释执行 Java 的字节码文件。

也是通过它，Java 的开发者才得以将自己开发的程序发布到用户手中，让用户使用。JRE 中包含了 Java virtual machine（JVM），runtime class libraries 和 Java application launcher，这些是运行 Java 程序的必要组件。与大家熟知的 JDK 不同，JRE 是 Java 运行环境，并不是一个开发环境，所以没有包含任何开发工具（如编译器和调试器），只是针对于使用 Java 程序的用户。

下图是Java 8中 JRE 的安装目录，里面有两个文件夹 `bin` 和 `lib`。你可以认为 bin 里的就是 JVM，lib 中则是 JVM 工作所需要的类库，而 JVM 和 lib 和起来就称为 JRE。

<img src="https://gitee.com/Kunaly/picture-bed/raw/master/img/image-20210112143352522.png" alt="image-20210112143352522" style="zoom:50%;" />



### 4.2 下载JDK

首先我们需要下载java开发工具包JDK，下载地址：http://www.oracle.com/technetwork/java/javase/downloads/index.html，点击如下下载按钮：

![image-20210112110242261](https://gitee.com/Kunaly/picture-bed/raw/master/img/image-20210112110242261.png)

下载后JDK的安装根据提示进行，还有安装JDK的时候也会安装JRE，一并安装就可以了。

安装JDK，安装过程中可以自定义安装目录等信息，例如我们选择安装目录为 **C:\Program Files (x86)\Java\jdk1.8.0_91**。

### 4.3 配置环境变量

安装完成后，右击"我的电脑"，点击"属性"，选择"高级系统设置"；

变量设置参数如下：

- 变量名：**JAVA_HOME**
- 变量值：**C:\Program Files (x86)\Java\jdk1.8.0_91**     // 要根据自己的实际路径配置

- 变量名：**CLASSPATH**
- 变量值：**.;%JAVA_HOME%\lib\dt.jar;%JAVA_HOME%\lib\tools.jar;**     //记得前面有个"."

- 变量名：**Path**
- 变量值：**%JAVA_HOME%\bin;%JAVA_HOME%\jre\bin;**

### 4.4 测试JDK是否安装成功

1、"开始"->"运行"，键入"cmd"；

2、键入命令: **java -version**、**java**、**javac** 几个命令，出现以下信息，说明环境变量配置成功；

![img](https://gitee.com/Kunaly/picture-bed/raw/master/img/java-win9.png)

### 4.5 常用JAVA开发工具

正所谓工欲善其事必先利其器，我们在开发java语言过程中同样需要一款不错的开发工具，目前市场上的IDE很多，本文为大家推荐以下下几款java开发工具：

- **Eclipse** 另一个免费开源的java IDE，下载地址： http://www.eclipse.org/downloads/packages/

- **MyEclipse** 是在Eclipse 基础上加上自己的插件开发而成的功能强大的企业级集成开发环境，主要用于Java、Java EE以及移动应用的开发。，下载地址： https://www.genuitec.com/products/myeclipse/download/?module=htmlpages&func=display&pid=4

  安装教程：https://mp.weixin.qq.com/s/pMjf-xRY2Zrd43sOreFFDg

- **JetBrains** 的 IDEA， 现在很多人开始使用了，功能很强大，下载地址：https://www.jetbrains.com/idea/download/

  安装教程：https://mp.weixin.qq.com/s/zGQ5W96aGhiUL-KriPZi4Q

- **Notepad++ :** Notepad++ 是在微软视窗环境之下的一个免费的代码编辑器，下载地址：[ http://notepad-plus-plus.org/](http://notepad-plus-plus.org/)

- **Netbeans:**开源免费的java IDE，下载地址： http://www.netbeans.org/index.html



## 5 第一个程序：Hello World

下面看一个最简单的 Java 应用程序：

```java
public class FirstDemo{
    public static void main(String[] args){
        System.out.println("Hello World!")
    }
}
```

## 📚 References

-  菜鸟教程