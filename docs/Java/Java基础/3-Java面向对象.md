# Java 面向对象

## 1.  面向对象概述

### 1.1 什么是面向对象

计算机革命的起源来自机器。编程语言就像是机器。它不仅是我们思维放大的工具与另一种表达媒介，更像是我们思想的一部分。语言的灵感来自其他形式的表达，如写作，绘画，雕塑，动画和电影制作。编程语言就是创建应用程序的思想结构。

**面向对象编程（Object-Oriented Programming，OOP）是一种编程思维方式和编码架构**，是一种 **对现实世界理解和抽象的方法**，是计算机编程技术发展到一定阶段后的产物。

> 💡 **什么是对象**：对象是客观存在的事物，可以说任何客观存在的都是可以成为对象，一台电脑，一直钢笔，一个人，一辆轿车等等，都可以称为对象

⭐ 面向对象的基本特点：

- **抽象**：对同一类型的对象的共同属性和行为进行概括，形成**类（class)** 。类是构造对象的模板或蓝图。由类构造（construct) 对象的过程称为创建类的**实例 （instance )**.
- **封装**：将抽象出的数据、代码封装在一起，隐藏对象的属性和实现细节，仅对外提供公共访问方式，将变化隔离，便于使用，提高复用性和安全性
- **继承**：在已有类的基础上，进行扩展形成新的类，提高代码复用性。继承是多态的前提
- **多态**：所谓多态就是同一函数名具有不同的功能实现方式

在面向对象之前，比如 C 语言就是**面向过程编程（Procedure-Oriented Programming，POP）的，这两者的**区别就在于：

- 面向过程是具体化的，流程化的，解决一个问题，你需要一步一步的分析，一步一步的实现。

<img src="https://gitee.com/Kunaly/picture-bed/raw/master/img/image-20210114162614774.png" alt="image-20210114162614774" style="zoom:80%;" />



- 面向对象是模型化的，你只需抽象出一个类，这是一个**封闭的盒子**，拥有数据也拥有解决问题的方法。需要什么功能直接使用就可以了，不必去一步一步的实现。

<img src="https://gitee.com/Kunaly/picture-bed/raw/master/img/image-20210114162815339.png" alt="image-20210114162815339" style="zoom:80%;" />

面向对象编程，是一种通过对象的方式，把现实世界映射到计算机模型的一种编程方法。

现实世界中，我们定义了“人”这种抽象概念，而具体的人则是“小明”、“小红”、“小军”等一个个具体的人。所以，“人”可以定义为一个类（class），而具体的人则是实例（instance）：

| 现实世界 | 计算机模型  | Java代码                   |
| :------- | :---------- | :------------------------- |
| 人       | 类 / class  | class Person { }           |
| 小明     | 实例 / ming | Person ming = new Person() |
| 小红     | 实例 / hong | Person hong = new Person() |
| 小军     | 实例 / jun  | Person jun = new Person()  |

同样的，“书”也是一种抽象的概念，所以它是类，而《Java核心技术》、《Java编程思想》、《Java学习笔记》则是实例：

| 现实世界     | 计算机模型   | Java代码                |
| :----------- | :----------- | :---------------------- |
| 书           | 类 / class   | class Book { }          |
| Java核心技术 | 实例 / book1 | Book book1 = new Book() |
| Java编程思想 | 实例 / book2 | Book book2 = new Book() |
| Java学习笔记 | 实例 / book3 | Book book3 = new Book() |

### 1.2  类和对象

在面向对象中，类和对象是最基本、最重要的组成单元。类实际上是表示一个客观世界某类群体的一些基本特征抽象。对象就是表示一个个具体的东西。所以说类是对象的抽象，对象是类的具体。

#### 1.2.1 Java中的类

类是Java中的一种重要的引用数据类型，也是组成 Java 程序的基本要素，因为所有的 Java 程序都是基于类的。

**Java中类的定义：**

```java
[public][abstract|final]class<class_name>[extends<class_name>][implements<interface_name>] {
    // 定义属性部分
    <property_type><property1>;
    <property_type><property2>;
    <property_type><property3>;
    …
    // 定义方法部分
    function1();
    function2();
    function3();
    …
}
```

提示：上述语法中，中括号“[]”中的部分表示可以省略，竖线“|”表示“或关系”，例如 abstract|final，说明可以使用 abstract 或 final 关键字，但是两个关键字不能同时出现。

上述语法中各关键字的描述如下。

- `public`：表示“共有”的意思。如果使用 public 修饰，则可以被其他类和程序访问。每个 Java 程序的主类都必须是 public 类，作为公共工具供其他类和程序使用的类应定义为 public 类。
- `abstract`：如果类被 abstract 修饰，则该类为抽象类，抽象类不能被实例化，但抽象类中可以有抽象方法（使用 abstract 修饰的方法）和具体方法（没有使用 abstract 修饰的方法）。继承该抽象类的所有子类都必须实现该抽象类中的所有抽象方法（除非子类也是抽象类）。
- `final`：如果类被 final 修饰，则不允许被继承。
- `class`：声明类的关键字。
- `class_name`：类的名称。
- `extends`：表示继承其他类。
- `implements`：表示实现某些接口。
- `property_type`：表示成员变量的类型。
- `property`：表示成员变量名称。
- `function()`：表示成员方法名称。

Java 类名的命名规则：

1. 类名应该以下划线（_）或字母开头，最好以字母开头。
2. 第一个字母最好大写，如果类名由多个单词组成，则每个单词的首字母最好都大写。
3. 类名不能为 Java 中的关键字，例如 boolean、this、int 等。
4. 类名不能包含任何嵌入的空格或点号以及除了下划线（_）和美元符号（$）字符之外的特殊字符。

**例子：**

创建一个新的类，就是创建一个新的数据类型。实例化一个类，就是得到类的一个对象。因此，对象就是一组变量和相关方法的集合，其中变量表明对象的状态和属性，方法表明对象所具有的行为。定义一个类的步骤如下所述。

(1) 声明类。编写类的最外层框架，声明一个名称为 Person 的类。

```java
public class Person {
    // 类的主体
}
```

(2) 编写类的属性。类中的数据和方法统称为类成员。其中，类的属性就是类的数据成员。通过在类的主体中定义变量来描述类所具有的特征（属性），这里声明的变量称为类的成员变量。

(3) 编写类的方法。类的方法描述了类所具有的行为，是类的方法成员。可以简单地把方法理解为独立完成某个功能的单元模块。

下面来定义一个简单的 Person 类。

```java
public class Person {
    private String name;    // 姓名
    private int age;    // 年龄
    public void tell() {   
        // 定义说话的方法
        System.out.println(name+"今年"+age+"岁！");
    }
}
```

如上述代码，在 Person 类中首先定义了两个属性，分别为 name 和 age，然后定义了一个名称为 tell() 的方法。

#### 1.2.2 Java中的对象

对象是对类的实例化。对象具有状态和行为，变量用来表明对象的状态，方法表明对象所具有的行为。Java对象的生命周期包括创建、使用和清除，本文详细介绍对象的创建，在 Java 语言中创建对象分显式创建与隐含创建两种情况。

**显式创建对象**

对象的显式创建方式有 4 种。

**1. 使用 new 关键字创建对象**

这是常用的创建对象的方法，语法格式如下：

```
类名 对象名 = new 类名()；
```

**2. 调用 java.lang.Class 或者 java.lang.reflect.Constuctor 类的 newlnstance() 实例方法**

在 Java 中，可以使用 java.lang.Class 或者 java.lang.reflect.Constuctor 类的 newlnstance() 实例方法来创建对象，代码格式如下：

```
java.lang.Class Class 类对象名称 = java.lang.Class.forName(要实例化的类全称);
类名 对象名 = (类名)Class类对象名称.newInstance();
```


调用 java.lang.Class 类中的 forName() 方法时，需要将要实例化的类的全称（比如 com.mxl.package.Student）作为参数传递过去，然后再调用 java.lang.Class 类对象的 newInstance() 方法创建对象。

**3. 调用对象的 clone() 方法**

该方法不常用，使用该方法创建对象时，要实例化的类必须继承 java.lang.Cloneable 接口。 调用对象的 clone() 方法创建对象的语法格式如下：

```
类名对象名 = (类名)已创建好的类对象名.clone();
```

**4. 调用 java.io.ObjectlnputStream 对象的 readObject() 方法**

下面创建一个示例演示常用的前三种对象创建方法。示例代码如下：

```java
public class Student implements Cloneable {   
    // 实现 Cloneable 接口
    private String Name;    // 学生名字
    private int age;    // 学生年龄
    public Student(String name,int age) {    
        // 构造方法
        this.Name = name;
        this.age = age;
    }
    public Student() {
        this.Name = "name";
        this.age = 0;
    }
    public String toString() {
        return"学生名字："+Name+"，年龄："+age;
    }
    public static void main(String[] args)throws Exception {
        System.out.println("---------使用 new 关键字创建对象---------");
       
        // 使用new关键字创建对象
        Student student1 = new Student("小刘",22);
        System.out.println(student1);
        System.out.println("-----------调用 java.lang.Class 的 newInstance() 方法创建对象-----------");
       
        // 调用 java.lang.Class 的 newInstance() 方法创建对象
        Class c1 = Class.forName("Student");
        Student student2 = (Student)c1.newInstance();
        System.out.println(student2);
        System.out.println("-------------------调用对象的 clone() 方法创建对象----------");

        // 调用对象的 clone() 方法创建对象
        Student student3 = (Student)student2.clone();
        System.out.println(student3);
    }
}
```

对上述示例的说明如下：

- 使用 new 关键字或 Class 对象的 newInstance() 方法创建对象时，都会调用类的构造方法。
- 使用 Class 类的 newInstance() 方法创建对象时，会调用类的默认构造方法，即无参构造方法。
- 使用 Object 类的 clone() 方法创建对象时，不会调用类的构造方法，它会创建一个复制的对象，这个对象和原来的对象具有不同的内存地址，但它们的属性值相同。
- 如果类没有实现 Cloneable 接口，则 clone。方法会抛出 java.lang.CloneNotSupportedException 异常，所以应该让类实现 Cloneable 接口。


程序执行结果如下：

```
---------使用 new 关键字创建对象---------
学生名字：小刘，年龄：22
-----------调用 java.lang.Class 的 newInstance() 方法创建对象-----------
学生名字：name，年龄：0
-------------------调用对象的done()方法创建对象----------
学生名字：name，年龄：0
```

**隐含创建对象**

除了显式创建对象以外，在 Java 程序中还可以隐含地创建对象，例如下面几种情况。

1）String strName = "strValue"，其中的“strValue”就是一个 String 对象，由 Java 虚拟机隐含地创建。

2）字符串的“+”运算符运算的结果为一个新的 String 对象，示例如下：

```
String str1 = "Hello";String str2 = "Java";String str3 = str1+str2;    // str3引用一个新的String对象
```

3）当 Java 虚拟机加载一个类时，会隐含地创建描述这个类的 Class 实例。

提示：类的加载是指把类的 .class 文件中的二进制数据读入内存中，把它存放在运行时数据区的方法区内，然后在堆区创建一个 java.lang.Class 对象，用来封装类在方法区内的数据结构。

无论釆用哪种方式创建对象，Java 虚拟机在创建一个对象时都包含以下步骤：

- 给对象分配内存。
- 将对象的实例变量自动初始化为其变量类型的默认值。
- 初始化对象，给实例变量赋予正确的初始值。

>
> 注意：每个对象都是相互独立的，在内存中占有独立的内存地址，并且每个对象都具有自己的生命周期，当一个对象的生命周期结束时，对象就变成了垃圾，由 Java 虚拟机自带的垃圾回收机制处理。

#### 1.2.3 匿名对象

经过前面的学习，我们知道创建对象的标准格式如下：

```
类名称 对象名 = new 类名称();
```

每次 new 都相当于开辟了一个新的对象，并开辟了一个新的物理内存空间。如果一个对象只需要使用唯一的一次，就可以使用匿名对象，匿名对象还可以作为实际参数传递。

匿名对象就是没有明确的给出名字的对象，是对象的一种简写形式。一般匿名对象只使用一次，而且匿名对象只在堆内存中开辟空间，而不存在栈内存的引用。

```java
public class Person {
    public String name; // 姓名
    public int age; // 年龄

    // 定义构造方法，为属性初始化
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    // 获取信息的方法
    public void tell() {
        System.out.println("姓名：" + name + "，年龄：" + age);
    }

    public static void main(String[] args) {
        new Person("张三", 30).tell(); // 匿名对象
    }
}
```

程序运行结果为：

```
姓名：张三，年龄：30
```

在以上程序的主方法中可以发现，直接使用了“new Person("张三",30)”语句，这实际上就是一个匿名对象，与之前声明的对象不同，此处没有任何栈内存引用它，所以此对象使用一次之后就等待被 GC（垃圾收集机制）回收。

### 1.3 方法

#### 1.3.1 Java方法定义

Java方法是语句的集合，它们在一起执行一个功能。

- 方法是解决一类问题的步骤的有序组合
- 方法包含于类或对象中
- 方法在程序中被创建，在其他地方被引用

**方法的优点**

1. 使程序变得更简短而清晰。
2. 有利于程序维护。
3. 可以提高程序开发的效率。
4. 提高了代码的重用性。

**方法的命名规则**

- 1.方法的名字的第一个单词应以小写字母作为开头，后面的单词则用大写字母开头写，不使用连接符。例如：**addPerson**。
- 2.下划线可能出现在 JUnit 测试方法名称中用以分隔名称的逻辑组件。一个典型的模式是：**test<MethodUnderTest>_<state>**，例如 **testPop_emptyStack**。

**方法的定义**

```java
修饰符 返回值类型 方法名(参数类型 参数名){
    ...
    方法体
    ...
    return 返回值;
}
```

方法包含一个方法头和一个方法体。下面是一个方法的所有部分：

- **修饰符：**修饰符，这是可选的，告诉编译器如何调用该方法。定义了该方法的访问类型。
- **返回值类型 ：**方法可能会返回值。returnValueType 是方法返回值的数据类型。有些方法执行所需的操作，但没有返回值。在这种情况下，returnValueType 是关键字**void**。
- **方法名：**是方法的实际名称。方法名和参数表共同构成方法签名。
- **参数类型：**参数像是一个占位符。当方法被调用时，传递值给参数。这个值被称为实参或变量。参数列表是指方法的参数类型、顺序和参数的个数。参数是可选的，方法可以不包含任何参数。
- **方法体：**方法体包含具体的语句，定义该方法的功能。

![image-20210114172734750](https://gitee.com/Kunaly/picture-bed/raw/master/img/image-20210114172734750.png)

#### 1.3.2 通过值传递参数

调用一个方法时候需要提供参数，你必须按照参数列表指定的顺序提供。

例如，下面的方法连续n次打印一个消息：

实例：

下面的例子演示按值传递的效果。

该程序创建一个方法，该方法用于交换两个变量。

```java
public class TestPassByValue {
  public static void main(String[] args) {
    int num1 = 1;
    int num2 = 2;
 
    System.out.println("交换前 num1 的值为：" +
                        num1 + " ，num2 的值为：" + num2);
 
    // 调用swap方法
    swap(num1, num2);
    System.out.println("交换后 num1 的值为：" +
                       num1 + " ，num2 的值为：" + num2);
  }
  /** 交换两个变量的方法 */
  public static void swap(int n1, int n2) {
    System.out.println("\t进入 swap 方法");
    System.out.println("\t\t交换前 n1 的值为：" + n1
                         + "，n2 的值：" + n2);
    // 交换 n1 与 n2的值
    int temp = n1;
    n1 = n2;
    n2 = temp;
 
    System.out.println("\t\t交换后 n1 的值为 " + n1
                         + "，n2 的值：" + n2);
  }
}
```

以上实例编译运行结果如下：

```
交换前 num1 的值为：1 ，num2 的值为：2
    进入 swap 方法
        交换前 n1 的值为：1，n2 的值：2
        交换后 n1 的值为 2，n2 的值：1
交换后 num1 的值为：1 ，num2 的值为：2
```

传递两个参数调用swap方法。有趣的是，方法被调用后，实参的值并没有改变。

#### 1.3.3 方法的重载

```java
public class TestMax {
   /** 主方法 */
   public static void main(String[] args) {
      int i = 5;
      int j = 2;
      int k = max(i, j);
      System.out.println( i + " 和 " + j + " 比较，最大值是：" + k);
   }
 
   /** 返回两个整数变量较大的值 */
   public static int max(int num1, int num2) {
      int result;
      if (num1 > num2)
         result = num1;
      else
         result = num2;
 
      return result; 
   }
   /** 返回两个浮点数变量较大的值 */
   public static double max(double num1, double num2) {
  		if (num1 > num2)
    		return num1;
 		else
 	   	 	return num2;
   }   
}
```

如果你调用max方法时传递的是int型参数，则 int型参数的max方法就会被调用；

如果传递的是double型参数，则double类型的max方法体会被调用，这叫做方法重载；

就是说一个类的两个方法拥有相同的名字，但是有不同的参数列表。

Java编译器根据方法签名判断哪个方法应该被调用。

方法重载可以让程序更清晰易读。执行密切相关任务的方法应该使用相同的名字。

重载的方法必须拥有不同的参数列表。你不能仅仅依据修饰符或者返回类型的不同来重载方法。

#### 1.3.4 变量的作用域

变量的范围是程序中该变量可以被引用的部分。

方法内定义的变量被称为局部变量。

局部变量的作用范围从声明开始，直到包含它的块结束。

局部变量必须声明才可以使用。

方法的参数范围涵盖整个方法。参数实际上是一个局部变量。

for循环的初始化部分声明的变量，其作用范围在整个循环。

但循环体内声明的变量其适用范围是从它声明到循环体结束。它包含如下所示的变量声明：

<img src="https://gitee.com/Kunaly/picture-bed/raw/master/img/image-20210115090052301.png" alt="image-20210115090052301" style="zoom: 67%;" />

你可以在一个方法里，不同的非嵌套块中多次声明一个具有相同的名称局部变量，但你不能在嵌套块内两次声明局部变量。

#### 1.3.5 构造方法

当一个对象被创建时候，构造方法用来初始化该对象。构造方法和它所在类的名字相同，但构造方法没有返回值。

通常会使用构造方法给一个类的实例变量赋初值，或者执行其它必要的步骤来创建一个完整的对象。

不管你是否自定义构造方法，所有的类都有构造方法，因为 Java 自动提供了一个默认构造方法，默认构造方法的访问修饰符和类的访问修饰符相同(类为 public，构造函数也为 public；类改为 protected，构造函数也改为 protected)。

一旦你定义了自己的构造方法，默认构造方法就会失效。

**实例：**

```java
// 一个简单的构造函数
class MyClass {
  int x;
 
  // 以下是构造函数
  MyClass() {
    x = 10;
  }
  // 有参数的构造方法
  MyClass(int i){
     x = i;
  }
}
```

```java
public class ConsDemo {
   public static void main(String args[]) {
      MyClass t1 = new MyClass();
      MyClass t2 = new MyClass();
      System.out.println(t1.x + " " + t2.x);
      
      MyClass t3 = new MyClass( 10 );
      MyClass t4 = new MyClass( 20 );
      System.out.println(t3.x + " " + t4.x);
   }
}
```

#### 1.3.6 可变参数

JDK 1.5 开始，Java支持传递同类型的可变参数给一个方法。

方法的可变参数的声明如下所示：

```
typeName... parameterName
```

在方法声明中，在指定参数类型后加一个省略号(...) 。

一个方法中只能指定一个可变参数，它必须是方法的最后一个参数。任何普通的参数必须在它之前声明。

**实例：**

```java
public class VarargsDemo {
    public static void main(String args[]) {
        // 调用可变参数的方法
        printMax(34, 3, 3, 2, 56.5);
        printMax(new double[]{1, 2, 3});
    }
 
    public static void printMax( double... numbers) {
        if (numbers.length == 0) {
            System.out.println("No argument passed");
            return;
        }
 
        double result = numbers[0];
 
        for (int i = 1; i <  numbers.length; i++){
            if (numbers[i] >  result) {
                result = numbers[i];
            }
        }
        System.out.println("The max value is " + result);
    }
}
```

以上实例编译运行结果如下：

```
The max value is 56.5
The max value is 3.0
```

#### 1.3.7 finalize() 方法

Java 允许定义这样的方法，它在对象被垃圾收集器析构(回收)之前调用，这个方法叫做 finalize( )，它用来清除回收对象。

例如，你可以使用 finalize() 来确保一个对象打开的文件被关闭了。

在 finalize() 方法里，你必须指定在对象销毁时候要执行的操作。

finalize() 一般格式是：

```java
protected void finalize()
{
   // 在这里终结代码
}
```

关键字 protected 是一个限定符，它确保 finalize() 方法不会被该类以外的代码调用。

当然，Java 的内存回收可以由 JVM 来自动完成。如果你手动使用，则可以使用上面的方法。

**实例：**

```java
public class FinalizationDemo {  
  public static void main(String[] args) {  
    Cake c1 = new Cake(1);  
    Cake c2 = new Cake(2);  
    Cake c3 = new Cake(3);  
      
    c2 = c3 = null;  
    System.gc(); //调用Java垃圾收集器
  }  
}  
 
class Cake extends Object {  
  private int id;  
  public Cake(int id) {  
    this.id = id;  
    System.out.println("Cake Object " + id + "is created");  
  }  
    
  protected void finalize() throws java.lang.Throwable {  
    super.finalize();  
    System.out.println("Cake Object " + id + "is disposed");  
  }  
}
```

输出结果如下：

```java
Cake Object 1is created
Cake Object 2is created
Cake Object 3is created
Cake Object 3is disposed
Cake Object 2is disposed
```

## 2. 面向对象核心

### 2.1  封装

#### 2.1.1  Java类的封装

```
封装将类的某些信息隐藏在类内部，不允许外部程序直接访问，只能通过该类提供的方法来实现对隐藏信息的操作和访问。
```

例如：一台计算机内部极其复杂，有主板、CPU、硬盘和内存， 而一般用户不需要了解它的内部细节，不需要知道主板的型号、CPU 主频、硬盘和内存的大小，于是计算机制造商将用机箱把计算机封装起来，对外提供了一些接口，如鼠标、键盘和显示器等，这样当用户使用计算机就非常方便。

封装的特点：

- 只能通过规定的方法访问数据。
- 隐藏类的实例细节，方便修改和实现。


实现封装的具体步骤如下：

1. 修改属性的可见性来限制对属性的访问，一般设为 private。
2. 为每个属性创建一对赋值（setter）方法和取值（getter）方法，一般设为 public，用于属性的读写。
3. 在赋值和取值方法中，加入属性控制语句（对属性值的合法性进行判断）。

**实例：**

下面以一个员工类的封装为例介绍封装过程。一个员工的主要属性有姓名、年龄、联系电话和家庭住址。假设员工类为 Employee，示例如下：

```java
public class Employee {
    private String name; // 姓名
    private int age; // 年龄
    private String phone; // 联系电话
    private String address; // 家庭住址

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        // 对年龄进行限制
        if (age < 18 || age > 40) {
            System.out.println("年龄必须在18到40之间！");
            this.age = 20; // 默认年龄
        } else {
            this.age = age;
        }
    }

    public String getPhone() {
        return phone;
    }

    public void setPhone(String phone) {
        this.phone = phone;
    }

    public String getAddress() {
        return address;
    }

    public void setAddress(String address) {
        this.address = address;
    }
}
```

如上述代码所示，使用 private 关键字修饰属性，这就意味着除了 Employee 类本身外，其他任何类都不可以访问这些属性。但是，可以通过这些属性的 setXxx() 方法来对其进行赋值，通过 getXxx() 方法来访问这些属性。

在 age 属性的 setAge() 方法中，首先对用户传递过来的参数 age 进行判断，如果 age 的值不在 18 到 40 之间，则将 Employee 类的 age 属性值设置为 20，否则为传递过来的参数值。

编写测试类 EmployeeTest，在该类的 main() 方法中调用 Employee 属性的 setXxx() 方法对其相应的属性进行赋值，并调用 getXxx() 方法访问属性，代码如下：

```java
public class EmployeeTest {
    public static void main(String[] args) {
        Employee people = new Employee();
        people.setName("王丽丽");
        people.setAge(35);
        people.setPhone("13653835964");
        people.setAddress("河北省石家庄市");
        System.out.println("姓名：" + people.getName());
        System.out.println("年龄：" + people.getAge());
        System.out.println("电话：" + people.getPhone());
        System.out.println("家庭住址：" + people.getAddress());
    }
}
```

运行该示例，输出结果如下：

```
姓名：王丽丽
年龄：35
电话：13653835964
家庭住址：河北省石家庄市
```


通过封装，实现了对属性的数据访问限制，满足了年龄的条件。在属性的赋值方法中可以对属性进行限制操作，从而给类中的属性赋予合理的值， 并通过取值方法获取类中属性的值（也可以直接调用类中的属性名称来获取属性值）。

### 2.2 继承

#### 2.1.1 Java类的继承

Java中的继承就是在已经存在类的基础上进行扩展，从而产生新的类。已经存在的类称为父类、基类或超类，而新产生的类称为子类或派生类。在子类中，不仅包含父类的属性和方法，还可以增加新的属性和方法。

Java 中子类继承父类的语法格式如下：

```
修饰符 class class_name extends extend_class { 
	// 类的主体
}
```

其中，class_name 表示子类（派生类）的名称；extend_class 表示父类（基类）的名称；extends 关键字直接跟在子类名之后，其后面是该类要继承的父类名称。例如：

```
public class Student extends Person{}
```

Java 的继承通过 extends 关键字来实现，extends 的英文意思是扩展，而不是继承。extends 很好的体现了子类和父类的关系，即子类是对父类的扩展，子类是一种特殊的父类。从这个角度看，使用继承来描述子类和父类的关系是错误的，用扩展更恰当。

那么为什么国内把 extends 翻译为“继承”呢？子类扩展父类之后就可以获得父类的属性和方法，这与汉语中的继承（子类从父类获得一笔财富称为继承）具有相似性。

> Java 与 C++定义继承类的方式十分相似。Java 用关键字 extends 代替了 C++ 中的冒号（：）。在 Java 中，所有的继承都是公有继承， 而没有 C++ 中的私有继承和保护继承。

类的继承不改变类成员的访问权限，也就是说，如果父类的成员是公有的、被保护的或默认的，它的子类仍具有相应的这些特性，并且子类不能获得父类的构造方法。

**实例：**

教师和学生都属于人，他们具有共同的属性：姓名、年龄、性别和身份证号，而学生还具有学号和所学专业两个属性，教师还具有教龄和所教专业两个属性。下面编写 Java 程序代码，使教师（Teacher）类和学生（Student）类都继承于人（People）类，具体的实现步骤如下。

1）创建人类 People，并定义 name、age、sex、sn 属性，代码如下：

```java
public class People {
    public String name; // 姓名
    public int age; // 年龄
    public String sex; // 性别
    public String sn; // 身份证号
    public People(String name, int age, String sex, String sn) {
        this.name = name;
        this.age = age;
        this.sex = sex;
        this.sn = sn;
    }
    public String toString() {
        return "姓名：" + name + "\n年龄：" + age + "\n性别：" + sex + "\n身份证号：" + sn;
    }
}
```

如上述代码，在 People 类中包含 4 个公有属性、一个构造方法和一个 toString() 方法。

2）创建 People 类的子类 Student 类，并定义 stuNo 和 department 属性，代码如下：

```java
public class Student extends People {
    private String stuNo; // 学号
    private String department; // 所学专业
    public Student(String name, int age, String sex, String sn, String stuno, String department) {
        super(name, age, sex, sn); // 调用父类中的构造方法
        this.stuNo = stuno;
        this.department = department;
    }
    public String toString() {
        return "姓名：" + name + "\n年龄：" + age + "\n性别：" + sex + "\n身份证号：" + sn + "\n学号：" + stuNo + "\n所学专业：" + department;
    }
}
```

由于 Student 类继承自 People 类，因此，在 Student 类中同样具有 People 类的属性和方法，这里重写了父类中的 toString() 方法。

注意：如果在父类中存在有参的构造方法而并没有重载无参的构造方法，那么在子类中必须含有有参的构造方法，因为如果在子类中不含有构造方法，默认会调用父类中无参的构造方法，而在父类中并没有无参的构造方法，因此会出错。

3）创建 People 类的另一个子类 Teacher，并定义 tYear 和 tDept 属性，代码如下：

```java
public class Teacher extends People {
    private int tYear; // 教龄
    private String tDept; // 所教专业
    public Teacher(String name, int age, String sex, String sn, int tYear, String tDept) {
        super(name, age, sex, sn); // 调用父类中的构造方法
        this.tYear = tYear;
        this.tDept = tDept;
    }
    public String toString() {
        return "姓名：" + name + "\n年龄：" + age + "\n性别:" + sex + "\n身份证号：" + sn + "\n教龄：" + tYear + "\n所教专业：" + tDept;
    }
}
```

Teacher 类与 Student 类相似，同样重写了父类中的 toString() 方法。

4）编写测试类 PeopleTest，在该类中创建 People 类的不同对象，分别调用它们的 toString() 方法，输出不同的信息。具体的代码如下：

```java
public class PeopleTest {
    public static void main(String[] args) {
        // 创建Student类对象
        People stuPeople = new Student("王丽丽", 23, "女", "410521198902145589", "00001", "计算机应用与技术");
        System.out.println("----------------学生信息---------------------");
        System.out.println(stuPeople);
        // 创建Teacher类对象
        People teaPeople = new Teacher("张文", 30, "男", "410521198203128847", 5, "计算机应用与技术");
        System.out.println("----------------教师信息----------------------");
        System.out.println(teaPeople);
    }
} 
```

运行程序，输出的结果如下：

```
----------------学生信息---------------------
姓名：王丽丽
年龄：23
性别：女
身份证号：410521198902145589
学号：00001
所学专业：计算机应用与技术
----------------教师信息----------------------
姓名：张文
年龄：30
性别:男
身份证号：410521198203128847
教龄：5
所教专业：计算机应用与技术
```

#### 2.1.2 单继承

Java 语言摒弃了 C++ 中难以理解的多继承特征，即 Java 不支持多继承，只允许一个类直接继承另一个类，即子类只能有一个直接父类，extends 关键字后面只能有一个类名。例如，如下代码会导致编译错误：

```java
class Student extends Person,Person1,Person2{…}
class Student extends Person,extends Person1,extends Person2{…}
```


很多地方在介绍 Java 的单继承时，可能会说 Java 类只能有一个父类，严格来讲，这种说法是错误的，应该是一个类只能有一个直接父类，但是它可以有多个间接的父类。例如，Student 类继承 Person 类，Person 类继承 Person1 类，Person1 类继承 Person2 类，那么 Person1 和 Person2 类是 Student 类的间接父类。图 1 展示了单继承的关系。

![image-20210115101036377](https://gitee.com/Kunaly/picture-bed/raw/master/img/image-20210115101036377.png)
从图 1 中可以看出，三角形、四边形和五边形的直接父类是多边形类，它们的间接父类是图形类。图形类、多边形类和三角形、四边形、五边形类形成了一个继承的分支。在这个分支上，位于下层的子类会继承上层所有直接或间接父类的属性和方法。如果两个类不在同一个继承树分支上，就不会存在继承关系，例如多边形类和直线。

如果定义一个 Java 类时并未显式指定这个类的直接父类，则这个类默认继承 java.lang.Object 类。因此，java.lang.Object 类是所有类的父类，要么是其直接父类，要么是其间接父类。因此所有的 Java 对象都可调用 java.lang.Object 类所定义的实例方法。

使用继承的注意点：

1. 子类一般比父类包含更多的属性和方法。
2. 父类中的 private 成员在子类中是不可见的，因此在子类中不能直接使用它们。
3. 父类和其子类间必须存在“是一个”即“is-a”的关系，否则不能用继承。但也并不是所有符合“is-a”关系的都应该用继承。例如，正方形是一个矩形，但不能让正方形类来继承矩形类，因为正方形不能从矩形扩展得到任何东西。正确的继承关系是正方形类继承图形类。
4. Java 只允许单一继承（即一个子类只能有一个直接父类），C++ 可以多重继承（即一个子类有多个直接父类）。



**继承的优缺点**

在面向对象语言中，继承是必不可少的、非常优秀的语言机制，它有如下优点：

1. 实现代码共享，减少创建类的工作量，使子类可以拥有父类的方法和属性。
2. 提高代码维护性和可重用性。
3. 提高代码的可扩展性，更好的实现父类的方法。


自然界的所有事物都是优点和缺点并存的，继承的缺点如下：

1. 继承是侵入性的。只要继承，就必须拥有父类的属性和方法。
2. 降低代码灵活性。子类拥有父类的属性和方法后多了些约束。
3. 增强代码耦合性（开发项目的原则为高内聚低耦合）。当父类的常量、变量和方法被修改时，需要考虑子类的修改，有可能会导致大段的代码需要重构。

#### 2.1.3 Super关键字

由于子类不能继承父类的构造方法，因此，如果要调用父类的构造方法，可以使用 super 关键字。super 可以用来访问父类的构造方法、普通方法和属性。

super 关键字的功能：

- 在子类的构造方法中显式的调用父类构造方法
- 访问父类的成员方法和变量。

**super调用成员属性**

当父类和子类具有相同的数据成员时，JVM 可能会模糊不清。我们可以使用以下代码片段更清楚地理解它。

```java
class Person {
    int age = 12;
}
class Student extends Person {
    int age = 18;
    void display() {
        System.out.println("学生年龄：" + super.age);
    }
}
class Test {
    public static void main(String[] args) {
        Student stu = new Student();
        stu.display();
    }
}
```

输出结果为：

```
学生年龄：12
```

在上面的例子中，父类和子类都有一个成员变量 age。我们可以使用 super 关键字访问 Person 类中的 age 变量。

**super调用成员方法**

当父类和子类都具有相同的方法名时，可以使用 super 关键字访问父类的方法。具体如下代码所示。

```java
class Person {
    void message() {
        System.out.println("This is person class");
    }
}
class Student extends Person {
    void message() {
        System.out.println("This is student class");
    }
    void display() {
        message();
        super.message();
    }
}
class Test {
    public static void main(String args[]) {
        Student s = new Student();
        s.display();
    }
}
```

输出结果为：

```
This is student class
This is person class
```

在上面的例子中，可以看到如果只调用方法 message( )，是当前的类 message( ) 被调用，使用 super 关键字时，是父类的 message( ) 被调用。

#### 2.1.4 super和this的区别

this 指的是当前对象的引用，super 是当前对象的父对象的引用。下面先简单介绍一下 super 和 this 关键字的用法。

super 关键字的用法：

- super.父类属性名：调用父类中的属性
- super.父类方法名：调用父类中的方法
- super()：调用父类的无参构造方法
- super(参数)：调用父类的有参构造方法


如果构造方法的第一行代码不是 this() 和 super()，则系统会默认添加 super()。


this 关键字的用法：

- this.属性名：表示当前对象的属性
- this.方法名(参数)：表示调用当前对象的方法


当局部变量和成员变量发生冲突时，使用`this.`进行区分。

关于 super 和 this 关键字的异同，可简单总结为以下几条。

1. 子类和父类中变量或方法名称相同时，用 super 关键字来访问。可以理解为 super 是指向自己父类对象的一个指针。在子类中调用父类的构造方法。
2. this 是自身的一个对象，代表对象本身，可以理解为 this 是指向对象本身的一个指针。在同一个类中调用其它方法。
3. this 和 super 不能同时出现在一个构造方法里面，因为 this 必然会调用其它的构造方法，其它的构造方法中肯定会有 super 语句的存在，所以在同一个构造方法里面有相同的语句，就失去了语句的意义，编译器也不会通过。
4. this( ) 和 super( ) 都指的是对象，所以，均不可以在 static 环境中使用，包括 static 变量、static 方法和 static 语句块。
5. 从本质上讲，this 是一个指向对象本身的指针, 然而 super 是一个 Java 关键字。

**实例：**

在 Animal 类和 Cat 类中分别定义了 public 类型的 name 属性和 private 类型的 name 属性，并且 Cat 类继承 Animal 类。那么，我们可以在 Cat 类中通过 super 关键字来访问父类 Animal 中的 name 属性，通过 this 关键字来访问本类中的 name 属性，如下面的代码：

```java
// 父类Animal的定义
public class Animal {
    public String name; // 动物名字
}
//子类Cat的定义
public class Cat extends Animal {
    private String name; // 名字
    public Cat(String aname, String dname) {
        super.name = aname; // 通过super关键字来访问父类中的name属性
        this.name = dname; // 通过this关键字来访问本类中的name属性
    }
    public String toString() {
        return "我是" + super.name + "，我的名字叫" + this.name;
    }
    public static void main(String[] args) {
        Animal cat = new Cat("动物", "喵星人");
        System.out.println(cat);
    }
}
```

上述代码演示了使用 super 关键字访问父类中与子类同名的成员变量 name，this 关键字访问本类的 name 变量。运行程序，输出结果如下：

```
我是动物，我的名字叫喵星人
```

#### 2.1.5 向上转型和向下转型

将一个类型强制转换成另一个类型的过程被称为类型转换。本节所说的对象类型转换，是指存在继承关系的对象，不是任意类型的对象。当对不存在继承关系的对象进行强制类型转换时，会抛出Java强制类型转换（java.lang.ClassCastException）异常。

Java 语言允许某个类型的引用变量引用子类的实例，而且可以对这个引用变量进行类型转换。Java 中引用类型之间的类型转换（前提是两个类是父子关系）主要有两种，分别是向上转型（upcasting）和向下转型（downcasting）。

##### 1）向上转型

父类引用指向子类对象为向上转型，语法格式如下：

```
fatherClass obj = new sonClass();
```

其中，fatherClass 是父类名称或接口名称，obj 是创建的对象，sonClass 是子类名称。

向上转型就是把子类对象直接赋给父类引用，不用强制转换。使用向上转型可以调用父类类型中的所有成员，不能调用子类类型中特有成员，最终运行效果看子类的具体实现。

##### 2）向下转型

与向上转型相反，子类对象指向父类引用为向下转型，语法格式如下：

```
sonClass obj = (sonClass) fatherClass;
```

其中，fatherClass 是父类名称，obj 是创建的对象，sonClass 是子类名称。

向下转型可以调用子类类型中所有的成员，不过需要注意的是如果父类引用对象指向的是子类对象，那么在向下转型的过程中是安全的，也就是编译是不会出错误。但是如果父类引用对象是父类本身，那么在向下转型的过程中是不安全的，编译不会出错，但是运行时会出现我们开始提到的 Java 强制类型转换异常，一般使用 instanceof 运算符来避免出此类错误。

例如，Animal 类表示动物类，该类对应的子类有 Dog 类，使用对象类型表示如下：

```java
Animal animal = new Dog();    // 向上转型，把Dog类型转换为Animal类型
Dog dog = (Dog) animal;    // 向下转型，把Animal类型转换为Dog类型
```

下面通过具体的示例演示对象类型的转换。例如，父类 Animal 和子类 Cat 中都定义了实例变量 name、静态变量 staticName、实例方法 eat() 和静态方法 staticEat()。此外，子类 Cat 中还定义了实例变量 str 和实例方法 eatMethod()。

父类 Animal 的代码如下:

```java
public class Animal {
    public String name = "Animal：动物";
    public static String staticName = "Animal：可爱的动物";
    public void eat() {
        System.out.println("Animal：吃饭");
    }
    public static void staticEat() {
        System.out.println("Animal：动物在吃饭");
    }
}
```

子类 Cat 的代码如下： 

```java
public class Cat extends Animal {
    public String name = "Cat：猫";
    public String str = "Cat：可爱的小猫";
    public static String staticName = "Dog：我是喵星人";
    public void eat() {
        System.out.println("Cat：吃饭");
    }
    public static void staticEat() {
        System.out.println("Cat：猫在吃饭");
    }
    public void eatMethod() {
        System.out.println("Cat：猫喜欢吃鱼");
    }
    public static void main(String[] args) {
        Animal animal = new Cat();
        Cat cat = (Cat) animal; // 向下转型
        System.out.println(animal.name); // 输出Animal类的name变量
        System.out.println(animal.staticName); // 输出Animal类的staticName变量
        animal.eat(); // 输出Cat类的eat()方法
        animal.staticEat(); // 输出Animal类的staticEat()方法
        System.out.println(cat.str); // 调用Cat类的str变量
        cat.eatMethod(); // 调用Cat类的eatMethod()方法
    }
}
```

通过引用类型变量来访问所引用对象的属性和方法时，Java 虚拟机将采用以下绑定规则：

- 实例方法与引用变量实际引用的对象的方法进行绑定，这种绑定属于动态绑定，因为是在运行时由 Java 虚拟机动态决定的。例如，animal.eat() 是将 eat() 方法与 Cat 类绑定。
- 静态方法与引用变量所声明的类型的方法绑定，这种绑定属于静态绑定，因为是在编译阶段已经做了绑定。例如，animal.staticEat() 是将 staticEat() 方法与 Animal 类进行绑定。
- 成员变量（包括静态变量和实例变量）与引用变量所声明的类型的成员变量绑定，这种绑定属于静态绑定，因为在编译阶段已经做了绑定。例如，animal.name 和 animal.staticName 都是与 Animal 类进行绑定。


对于 Cat 类，运行时将会输出如下结果：

```
Animal：动物
Animal：可爱的动物
Cat：吃饭
Animal：动物在吃饭
Cat：可爱的小猫
Cat：猫喜欢吃鱼
```

##### 3）强制对象类型转换

Java 编译器允许在具有直接或间接继承关系的类之间进行类型转换。对于向下转型，必须进行强制类型转换；对于向上转型，不必使用强制类型转换。

例如，对于一个引用类型的变量，Java 编译器按照它声明的类型来处理。如果使用 animal 调用 str 和 eatMethod() 方法将会出错，如下：

```java
animal.str = "";    // 编译出错，提示Animal类中没有str属性
animal.eatMethod();    // 编译出错，提示Animal类中没有eatMethod()方法
```


如果要访问 Cat 类的成员，必须通过强制类型转换，如下：

```java
((Cat)animal).str = "";    // 编译成功((Cat)animal).eatMethod();    // 编译成功
```


把 Animal 对象类型强制转换为 Cat 对象类型，这时上面两句编译成功。对于如下语句，由于使用了强制类型转换，所以也会编译成功，例如：

```java
Cat cat = (Cat)animal;    // 编译成功，将Animal对象类型强制转换为Cat对象类型
```


类型强制转换时想运行成功就必须保证父类引用指向的对象一定是该子类对象，最好使用 instanceof 运算符判断后，再强转，例如：

```java
Animal animal = new Cat();
if (animal instanceof Cat) {    
	Cat cat = (Cat) animal; // 向下转型   
    ...
}
```


子类的对象可以转换成父类类型，而父类的对象实际上无法转换为子类类型。因为通俗地讲，父类拥有的成员子类肯定也有，而子类拥有的成员，父类不一定有。因此，对于向上转型，不必使用强制类型转换。例如：

```
Cat cat = new Cat();Animal animal = cat;    // 向上转型，不必使用强制类型转换
```


如果两种类型之间没有继承关系，那么将不允许进行类型转换。例如：

```java
Dog dog = new Dog();Cat cat = (Cat)dog;    // 编译出错，不允许把Dog对象类型转换为Cat对象类型
```

### 2.3 重写和重载

#### 2.3.1 方法的重载

Java允许同一个类中定义多个同名方法，只要它们的形参列表不同即可。如果同一个类中包含了两个或两个以上方法名相同的方法，但形参列表不同，这种情况被称为方法重载（overload）。

例如，在 JDK 的 java.io.PrintStream 中定义了十多个同名的 println() 方法。

```java
public void println(int i){…}
public void println(double d){…}
public void println(String s){…}
```

这些方法完成的功能类似，都是格式化输出。根据参数的不同来区分它们，以进行不同的格式化处理和输出。它们之间就构成了方法的重载。实际调用时，根据实参的类型来决定调用哪一个方法。例如：

```java
System.out.println(102);     // 调用println(int i)方法
System.out.println(102.25);     // 调用println(double d)方法
System.out.println("价格为 102.25");   // 调用println(String s)方法
```


方法重载的要求是两同一不同：同一个类中方法名相同，参数列表不同。至于方法的其他部分，如方法返回值类型、修饰符等，与方法重载没有任何关系。

使用方法重载其实就是避免出现繁多的方法名，有些方法的功能是相似的，如果重新建立一个方法，重新取个方法名称，会降低程序可读性。

**实例：**

在比较数值时，数值的个数和类型是不固定的，可能是两个 int 类型的数值，也可能是两个 double 类型的数值，或者是两个 double、一个 int 类型的数值；在这种情况下就可以使用方法的重载来实现数值之间的比较功能。具体实现代码如下：

```java
public class OverLoading {
    public void max(int a, int b) {
        // 含有两个int类型参数的方法
        System.out.println(a > b ? a : b);
    }
    public void max(double a, double b) {
        // 含有两个double类型参数的方法
        System.out.println(a > b ? a : b);
    }
    public void max(double a, double b, int c) {
        // 含有两个double类型参数和一个int类型参数的方法
        double max = (double) (a > b ? a : b);
        System.out.println(c > max ? c : max);
    }
    public static void main(String[] args) {
        OverLoading ol = new OverLoading();
        System.out.println("1 与 5 比较，较大的是：");
        ol.max(1, 5);
        System.out.println("5.205 与 5.8 比较，较大的是：");
        ol.max(5.205, 5.8);
        System.out.println("2.15、0.05、58 中，较大的是：");
        ol.max(2.15, 0.05, 58);
    }
}
```

编译、运行上面程序完全正常，虽然 3 个 max() 方法的方法名相同，但因为它们的形参列表不同，所以系统可以正常区分出这 3 个方法。当运行时，Java 虚拟机会根据传递过来的不同参数来调用不同的方法。运行结果如下：

```
1 与 5 比较，较大的是：
5
5.205 与 5.8 比较，较大的是：
5.8
2.15、0.05、58 中，较大的是：
58.0
```

为什么方法重载不能用方法的返回值类型区分呢？

对于`int f( ) { }`和`void( ) { }`两个方法，如果这样调用`int result = f();`，系统可以识别是调用返回值类型为 int 的方法，但 Java 调用方法时可以忽略方法返回值，如果采用如下方法来调用`f();`，你能判断是调用哪个方法吗？如果你尚且不能判断，那么 Java 系统也会糊涂。在编程过程中有一条重要规则就是不要让系统糊涂，系统一糊涂，肯定就是你错了。因此，Java 里不能用方法返回值类型作为区分方法重载的依据。

#### 2.3.2 方法的重写

在子类中如果创建了一个与父类中相同名称、相同返回值类型、相同参数列表的方法，只是方法体中的实现不同，以实现不同于父类的功能，这种方式被称为方法重写（override），又称为方法覆盖。当父类中的方法无法满足子类需求或子类具有特有功能的时候，需要方法重写。

子类可以根据需要，定义特定于自己的行为。既沿袭了父类的功能名称，又根据子类的需要重新实现父类方法，从而进行扩展增强。

在重写方法时，需要遵循下面的规则：

- 参数列表必须完全与被重写的方法参数列表相同。
- 返回的类型必须与被重写的方法的返回类型相同（Java 1.5 版本之前返回值类型必须一样，之后的 Java 版本放宽了限制，返回值类型必须小于或者等于父类方法的返回值类型）。
- 访问权限不能比父类中被重写方法的访问权限更低（public>protected>default>private）。
- 重写方法一定不能抛出新的检査异常或者比被重写方法声明更加宽泛的检査型异常。例如，父类的一个方法声明了一个检査异常 IOException，在重写这个方法时就不能抛出 Exception，只能拋出 IOException 的子类异常，可以抛出非检査异常。


另外还要注意以下几条：

- 重写的方法可以使用 @Override 注解来标识。
- 父类的成员方法只能被它的子类重写。
- 声明为 final 的方法不能被重写。
- 声明为 static 的方法不能被重写，但是能够再次声明。
- 构造方法不能被重写。
- 子类和父类在同一个包中时，子类可以重写父类的所有方法，除了声明为 private 和 final 的方法。
- 子类和父类不在同一个包中时，子类只能重写父类的声明为 public 和 protected 的非 final 方法。
- 如果不能继承一个方法，则不能重写这个方法。

**实例：**

每种动物都有名字和年龄属性，但是喜欢吃的食物是不同的，比如狗喜欢吃骨头、猫喜欢吃鱼等，因此每种动物的介绍方式是不一样的。

下面编写 Java 程序，在父类 Animal 中定义 getInfo() 方法，并在子类 Cat 中重写该方法， 实现猫的介绍方式。父类 Animal 的代码如下：

```java
public class Animal {
    public String name; // 名字
    public int age; // 年龄
    public Animal(String name, int age) {
        this.name = name;
        this.age = age;
    }
    public String getInfo() {
        return "我叫" + name + "，今年" + age + "岁了。";
    }
}
```

子类 Cat 的代码如下：

```java
public class Cat extends Animal {
    private String hobby;
    public Cat(String name, int age, String hobby) {
        super(name, age);
        this.hobby = hobby;
    }
    public String getInfo() {
        return "喵！大家好！我叫" + this.name + "，我今年" + this.age + "岁了，我爱吃" + hobby + "。";
    }
    public static void main(String[] args) {
        Animal animal = new Cat("小白", 2, "鱼");
        System.out.println(animal.getInfo());
    }
}
```

如上述代码，在 Animal 类中定义了一个返回值类型为 String、名称为 getInfo() 的方法，而 Cat 类继承自该类，因此 Cat 类同样含有与 Animal 类中相同的 getInfo() 方法。但是我们在 Cat 类中又重新定义了一个 getInfo() 方法，即重写了父类中的 getInfo() 方法。

在 main() 方法中，创建了 Cat 类的对象 animal，并调用了 getInfo() 方法。输出的结果如下：

```
喵！大家好！我叫小白，我今年2岁了，我爱吃鱼。
```

如果子类中创建了一个成员变量，而该变量的类型和名称都与父类中的同名成员变量相同，我们则称作变量隐藏。

### 2.4 多态

#### 2.4.1 Java的多态性

多态性是面向对象编程的又一个重要特征，它是指在父类中定义的属性和方法被子类继承之后，可以具有不同的数据类型或表现出不同的行为，这使得同一个属性或方法在父类及其各个子类中具有不同的含义。

对面向对象来说，多态分为编译时多态和运行时多态。其中编译时多态是静态的，主要是指方法的重载，它是根据参数列表的不同来区分不同的方法。通过编译之后会变成两个不同的方法，在运行时谈不上多态。而运行时多态是动态的，它是通过动态绑定来实现的，也就是大家通常所说的多态性。

Java 实现多态有 3 个必要条件：继承、重写和向上转型。只有满足这 3 个条件，开发人员才能够在同一个继承结构中使用统一的逻辑实现代码处理不同的对象，从而执行不同的行为。

- 继承：在多态中必须存在有继承关系的子类和父类。
- 重写：子类对父类中某些方法进行重新定义，在调用这些方法时就会调用子类的方法。
- 向上转型：在多态中需要将子类的引用赋给父类对象，只有这样该引用才既能可以调用父类的方法，又能调用子类的方法。

**实例：**

下面通过一个例子来演示重写如何实现多态性。例子使用了类的继承和运行时多态机制，具体步骤如下。

1）创建 Figure 类，在该类中首先定义存储二维对象的尺寸，然后定义有两个参数的构造方法，最后添加 area() 方法，该方法计算对象的面积。代码如下：

```java
public class Figure {
    double dim1;
    double dim2;
    Figure(double d1, double d2) {
        // 有参的构造方法
        this.dim1 = d1;
        this.dim2 = d2;
    }
    double area() {
        // 用于计算对象的面积
        System.out.println("父类中计算对象面积的方法，没有实际意义，需要在子类中重写。");
        return 0;
    }
}
```

2）创建继承自 Figure 类的 Rectangle 子类，该类调用父类的构造方法，并且重写父类中的 area() 方法。代码如下：

```java
public class Rectangle extends Figure {
    Rectangle(double d1, double d2) {
        super(d1, d2);
    }
    double area() {
        System.out.println("长方形的面积：");
        return super.dim1 * super.dim2;
    }
}
```

3）创建继承自 Figure 类的 Triangle 子类，该类与 Rectangle 相似。代码如下：

```java
public class Triangle extends Figure {
    Triangle(double d1, double d2) {
        super(d1, d2);
    }
    double area() {
        System.out.println("三角形的面积：");
        return super.dim1 * super.dim2 / 2;
    }
}
```

4）创建 Test 测试类，在该类的 main() 方法中首先声明 Figure 类的变量 figure，然后分别为 figure 变量指定不同的对象，并调用这些对象的 area() 方法。代码如下：

```java
public class Test {
    public static void main(String[] args) {
        Figure figure; // 声明Figure类的变量
        figure = new Rectangle(9, 9);
        System.out.println(figure.area());
        System.out.println("===============================");
        figure = new Triangle(6, 8);
        System.out.println(figure.area());
        System.out.println("===============================");
        figure = new Figure(10, 10);
        System.out.println(figure.area());
    }
}
```

从上述代码可以发现，无论 figure 变量的对象是 Rectangle 还是 Triangle，它们都是 Figure 类的子类，因此可以向上转型为该类，从而实现多态。

5）执行上述代码，输出结果如下：

```
长方形的面积：
81.0
===============================
三角形的面积：
24.0
===============================
父类中计算对象面积的方法，没有实际意义，需要在子类中重写。
0.0
```

### 2.5 抽象类和接口

#### 2.5.1 Java抽象类

在面向对象的概念中，所有的对象都是通过类来描绘的，但是反过来，并不是所有的类都是用来描绘对象的，如果一个类中没有包含足够的信息来描绘一个具体的对象，那么这样的类称为抽象类。

在 Java 中抽象类的语法格式如下：

```java
<abstract>class<class_name> {
    <abstract><type><method_name>(parameter-iist);
}
```

其中，abstract 表示该类或该方法是抽象的；class_name 表示抽象类的名称；method_name 表示抽象方法名称，parameter-list 表示方法参数列表。

如果一个方法使用 abstract 来修饰，则说明该方法是抽象方法，抽象方法只有声明没有实现。需要注意的是 abstract 关键字只能用于普通方法，不能用于 static 方法或者构造方法中。

抽象方法的 3 个特征如下：

1. 抽象方法没有方法体
2. 抽象方法必须存在于抽象类中
3. 子类重写父类时，必须重写父类所有的抽象方法


注意：在使用 abstract 关键字修饰抽象方法时不能使用 private 修饰，因为抽象方法必须被子类重写，而如果使用了 private 声明，则子类是无法重写的。

抽象类的定义和使用规则如下：

1. 抽象类和抽象方法都要使用 abstract 关键字声明。
2. 如果一个方法被声明为抽象的，那么这个类也必须声明为抽象的。而一个抽象类中，可以有 0~n 个抽象方法，以及 0~n 个具体方法。
3. 抽象类不能实例化，也就是不能使用 new 关键字创建对象。

**实例：**

不同几何图形的面积计算公式是不同的，但是它们具有的特性是相同的，都具有长和宽这两个属性，也都具有面积计算的方法。那么可以定义一个抽象类，在该抽象类中含有两个属性（width 和 height）和一个抽象方法 area( )，具体步骤如下。

1）首先创建一个表示图形的抽象类 Shape，代码如下所示。

```java
public abstract class Shape {
    public int width; // 几何图形的长
    public int height; // 几何图形的宽
    public Shape(int width, int height) {
        this.width = width;
        this.height = height;
    }
    public abstract double area(); // 定义抽象方法，计算面积
}
```

2）定义一个正方形类，该类继承自形状类 Shape，并重写了 area( ) 抽象方法。正方形类的代码如下:

```java
public class Square extends Shape {
    public Square(int width, int height) {
        super(width, height);
    }
    // 重写父类中的抽象方法，实现计算正方形面积的功能
    @Override
    public double area() {
        return width * height;
    }
}
```

3）定义一个三角形类，该类与正方形类一样，需要继承形状类 Shape，并重写父类中的抽象方法 area()。三角形类的代码实现如下：

```java
public class Triangle extends Shape {
    public Triangle(int width, int height) {
        super(width, height);
    }
    // 重写父类中的抽象方法，实现计算三角形面积的功能
    @Override
    public double area() {
        return 0.5 * width * height;
    }
}
```

4）最后创建一个测试类，分别创建正方形类和三角形类的对象，并调用各类中的 area() 方法，打印出不同形状的几何图形的面积。测试类的代码如下：

```java
public class ShapeTest {
    public static void main(String[] args) {
        Square square = new Square(5, 4); // 创建正方形类对象
        System.out.println("正方形的面积为：" + square.area());
        Triangle triangle = new Triangle(2, 5); // 创建三角形类对象
        System.out.println("三角形的面积为：" + triangle.area());
    }
}
```

在该程序中，创建了 4 个类，分别为图形类 Shape、正方形类 Square、三角形类 Triangle 和测试类 ShapeTest。其中图形类 Shape 是一个抽象类，创建了两个属性，分别为图形的长度和宽度，并通过构造方法 Shape( ) 给这两个属性赋值。

在 Shape 类的最后定义了一个抽象方法 area( )，用来计算图形的面积。在这里，Shape 类只是定义了计算图形面积的方法，而对于如何计算并没有任何限制。也可以这样理解，抽象类 Shape 仅定义了子类的一般形式。

正方形类 Square 继承抽象类 Shape，并实现了抽象方法 area( )。三角形类 Triangle 的实现和正方形类相同，这里不再介绍。

 

在测试类 ShapeTest 的 main( ) 方法中，首先创建了正方形类和三角形类的实例化对象 square 和 triangle，然后分别调用 area( ) 方法实现了面积的计算功能。

5）运行该程序，输出的结果如下：

```
正方形的面积为：20.0
三角形的面积为：5.0
```

#### 2.5.2 Java接口

接口（英文：Interface），在JAVA编程语言中是一个抽象类型，是抽象方法的集合，接口通常以interface来声明。一个类通过继承接口的方式，从而来继承接口的抽象方法。

接口并不是类，编写接口的方式和类很相似，但是它们属于不同的概念。类描述对象的属性和方法。接口则包含类要实现的方法。

除非实现接口的类是抽象类，否则该类要定义接口中的所有方法。

接口无法被实例化，但是可以被实现。一个实现接口的类，必须实现接口内所描述的所有方法，否则就必须声明为抽象类。另外，在 Java 中，接口类型可用来声明一个变量，他们可以成为一个空指针，或是被绑定在一个以此接口实现的对象。

**接口与类相似点：**

- 一个接口可以有多个方法。
- 接口文件保存在 .java 结尾的文件中，文件名使用接口名。
- 接口的字节码文件保存在 .class 结尾的文件中。
- 接口相应的字节码文件必须在与包名称相匹配的目录结构中。

**接口与类的区别：**

- 接口不能用于实例化对象。
- 接口没有构造方法。
- 接口中所有的方法必须是抽象方法。
- 接口不能包含成员变量，除了 static 和 final 变量。
- 接口不是被类继承了，而是要被类实现。
- 接口支持多继承。

**接口特性**

- 接口中每一个方法也是隐式抽象的,接口中的方法会被隐式的指定为 **public abstract**（只能是 public abstract，其他修饰符都会报错）。
- 接口中可以含有变量，但是接口中的变量会被隐式的指定为 **public static final** 变量（并且只能是 public，用 private 修饰会报编译错误）。
- 接口中的方法是不能在接口中实现的，只能由实现接口的类来实现接口中的方法。

**抽象类和接口的区别**

- 抽象类中的方法可以有方法体，就是能实现方法的具体功能，但是接口中的方法不行。
- 抽象类中的成员变量可以是各种类型的，而接口中的成员变量只能是 **public static final** 类型的。
- 接口中不能含有静态代码块以及静态方法(用 static 修饰的方法)，而抽象类是可以有静态代码块和静态方法。
- 一个类只能继承一个抽象类，而一个类却可以实现多个接口。

> **注**：JDK 1.8 以后，接口里可以有静态方法和方法体了。



**定义接口**

Java 接口的定义方式与类基本相同，不过接口定义使用的关键字是 interface，接口定义的语法格式如下：

```java
[public] interface interface_name [extends interface1_name[, interface2_name,…]] {    
    // 接口体，其中可以包含定义常量和声明方法    
	[public] [static] [final] type constant_name = value;    // 定义常量    	
	[public] [abstract] returnType method_name(parameter_list);    // 声明方法
}
```

对以上语法的说明如下：

- public 表示接口的修饰符，当没有修饰符时，则使用默认的修饰符，此时该接口的访问权限仅局限于所属的包；
- interface_name 表示接口的名称。接口名应与类名采用相同的命名规则，即如果仅从语法角度来看，接口名只要是合法的标识符即可。如果要遵守 Java 可读性规范，则接口名应由多个有意义的单词连缀而成，每个单词首字母大写，单词与单词之间无需任何分隔符。
- extends 表示接口的继承关系；
- interface1_name 表示要继承的接口名称；
- constant_name 表示变量名称，一般是 static 和 final 型的；
- returnType 表示方法的返回值类型；
- parameter_list 表示参数列表，在接口中的方法是没有方法体的。

注意：一个接口可以有多个直接父接口，但接口只能继承接口，不能继承类。


接口对于其声明、变量和方法都做了许多限制，这些限制作为接口的特征归纳如下：

- 具有 public 访问控制符的接口，允许任何类使用；没有指定 public 的接口，其访问将局限于所属的包。
- 方法的声明不需要其他修饰符，在接口中声明的方法，将隐式地声明为公有的（public）和抽象的（abstract）。
- 在 Java 接口中声明的变量其实都是常量，接口中的变量声明，将隐式地声明为 public、static 和 final，即常量，所以接口中定义的变量必须初始化。
- `接口没有构造方法，不能被实例化`。例如：

```
public interface A {
	publicA(){…}    // 编译出错，接口不允许定义构造方法
}
```

一个接口不能够实现另一个接口，但它可以继承多个其他接口。子接口可以对父接口的方法和常量进行重写。例如：

```java
public interface StudentInterface extends PeopleInterface {   
    // 接口 StudentInterface 继承 PeopleInterface    
    int age = 25;    // 常量age重写父接口中的age常量    
    void getInfo();    // 方法getInfo()重写父接口中的getInfo()方法
}
```

例如，定义一个接口 MyInterface，并在该接口中声明常量和方法，如下：

```java
public interface MyInterface {     // 接口myInterface    
    String name;    // 不合法，变量name必须初始化   
    int age = 20;    // 合法，等同于 public static final int age = 20;    
    void getInfo();    // 方法声明，等同于 public abstract void getInfo();
}
```

**实现接口**

接口的主要用途就是被实现类实现，一个类可以实现一个或多个接口，继承使用 extends 关键字，实现则使用 implements 关键字。因为一个类可以实现多个接口，这也是 Java 为单继承灵活性不足所作的补充。类实现接口的语法格式如下：

```java
<public> class <class_name> [extends superclass_name] [implements interface1_name[, interface2_name…]] {
    // 主体
}
```

对以上语法的说明如下：

- public：类的修饰符；
- superclass_name：需要继承的父类名称；
- interface1_name：要实现的接口名称。


实现接口需要注意以下几点：

- 实现接口与继承父类相似，一样可以获得所实现接口里定义的常量和方法。如果一个类需要实现多个接口，则多个接口之间以逗号分隔。
- 一个类可以继承一个父类，并同时实现多个接口，implements 部分必须放在 extends 部分之后。
- 一个类实现了一个或多个接口之后，这个类必须完全实现这些接口里所定义的全部抽象方法（也就是重写这些抽象方法）；否则，该类将保留从父接口那里继承到的抽象方法，该类也必须定义成抽象类。

**实例：**

在程序的开发中，需要完成两个数的求和运算和比较运算功能的类非常多。那么可以定义一个接口来将类似的功能组织在一起。下面创建一个示例，具体介绍接口的实现方式。

1）创建一个名称为 IMath 的接口，代码如下：

```java
public interface IMath {    
	public int sum();    // 完成两个数的相加    
    public int maxNum(int a,int b);    // 获取较大的数
}
```

2）定义一个 MathClass 类并实现 IMath 接口，MathClass 类实现代码如下：

```java
public class MathClass implements IMath {    
    private int num1;    // 第 1 个操作数    
    private int num2;    // 第 2 个操作数    
    public MathClass(int num1,int num2) {        
        // 构造方法        
        this.num1 = num1;        
        this.num2 = num2;    
    }   
    // 实现接口中的求和方法    
    public int sum() {        
        return num1 + num2;    
    }   
    // 实现接口中的获取较大数的方法    
    public int maxNum(int a,int b) {        
        if(a >= b) {            
            return a;        
        } else {            
            return b;        
        }    
    }
}
```

在实现类中，所有的方法都使用了 public 访问修饰符声明。无论何时实现一个由接口定义的方法，它都必须实现为 public，因为接口中的所有成员都显式声明为 public。

3）最后创建测试类 NumTest，实例化接口的实现类 MathClass，调用该类中的方法并输出结果。该类内容如下：

```java
public class NumTest {    
    public static void main(String[] args) {        
        // 创建实现类的对象        
        MathClass calc = new MathClass(100, 300);        
        System.out.println("100 和 300 相加结果是：" + calc.sum()); 
        System.out.println("100 比较 300，哪个大：" + calc.maxNum(100, 300));    
    }
}
```

程序运行结果如下所示。

```
100 和 300 相加结果是：400
100 比较 300，哪个大：300
```

在该程序中，首先定义了一个 IMath 的接口，在该接口中只声明了两个未实现的方法，这两个方法需要在接口的实现类中实现。在实现类 MathClass 中定义了两个私有的属性，并赋予两个属性初始值，同时创建了该类的构造方法。因为该类实现了 MathClass 接口，因此必须实现接口中的方法。在最后的测试类中，需要创建实现类对象，然后通过实现类对象调用实现类中的方法。

### 2.6 内部类

#### 2.6.1 内部类简介

在类内部可定义成员变量和方法，且在类内部也可以定义另一个类。如果在类 Outer 的内部再定义一个类 Inner，此时类 Inner 就称为内部类（或称为嵌套类），而类 Outer 则称为外部类（或称为宿主类）。

内部类可以很好地实现隐藏，一般的非内部类是不允许有 private 与 protected 权限的，但内部类可以。内部类拥有外部类的所有元素的访问权限。

内部类可以分为：实例内部类、静态内部类和成员内部类，每种内部类都有它特定的一些特点，本节先详细介绍一些和内部类相关的知识。

在类 A 中定义类 B，那么类 B 就是内部类，也称为嵌套类，相对而言，类 A 就是外部类。如果有多层嵌套，例如类 A 中有内部类 B，而类 B 中还有内部类 C，那么通常将最外层的类称为顶层类（或者顶级类）。

内部类也可以分为多种形式，与变量非常类似，如图 1 所示。

<img src="https://gitee.com/Kunaly/picture-bed/raw/master/img/image-20210115111730622.png" alt="image-20210115111730622" style="zoom:80%;" />

内部类的特点如下：

1. 内部类仍然是一个独立的类，在编译之后内部类会被编译成独立的`.class`文件，但是前面冠以外部类的类名和`$`符号。
2. 内部类不能用普通的方式访问。内部类是外部类的一个成员，因此内部类可以自由地访问外部类的成员变量，无论是否为 private 的。
3. 内部类声明成静态的，就不能随便访问外部类的成员变量，仍然是只能访问外部类的静态成员变量。



**内部类的实例：**

```java
public class Test {
    public class InnerClass {
        public int getSum(int x,int y) {
            return x + y;
        }
    }
    public static void main(String[] args) {
        Test.InnerClass ti = new Test().new InnerClass();
        int i = ti.getSum(2,3);
        System.out.println(i);    // 输出5
    }
}
```

有关内部类的说明有如下几点。

- 外部类只有两种访问级别：public 和默认；内部类则有 4 种访问级别：public、protected、 private 和默认。
- 在外部类中可以直接通过内部类的类名访问内部类。

```
InnerClass ic = new InnerClass();    // InnerClass为内部类的类名
```

- 在外部类以外的其他类中则需要通过内部类的完整类名访问内部类。

```
Test.InnerClass ti = newTest().new InnerClass();    // Test.innerClass是内部类的完整类名
```

- 内部类与外部类不能重名。

#### 2.6.2 实例内部类

实例内部类是指没有用 static 修饰的内部类，有的地方也称为非静态内部类。示例代码如下：

```java
public class Outer {
    class Inner {
        // 实例内部类
    }
}
```

上述示例中的 Inner 类就是实例内部类。实例内部类有如下特点。

1）在外部类的静态方法和外部类以外的其他类中，必须通过外部类的实例创建内部类的实例。

```java
public class Outer {
    class Inner1 {
    }
    Inner1 i = new Inner1(); // 不需要创建外部类实例
    public void method1() {
        Inner1 i = new Inner1(); // 不需要创建外部类实例
    }
    public static void method2() {
        Inner1 i = new Outer().new inner1(); // 需要创建外部类实例
    }
    class Inner2 {
        Inner1 i = new Inner1(); // 不需要创建外部类实例
    }
}
class OtherClass {
    Outer.Inner i = new Outer().new Inner(); // 需要创建外部类实例
}
```

2）在实例内部类中，可以访问外部类的所有成员。

```java
public class Outer {
    public int a = 100;
    static int b = 100;
    final int c = 100;
    private int d = 100;
    public String method1() {
        return "实例方法1";
    }
    public static String method2() {
        return "静态方法2";
    }
    class Inner {
        int a2 = a + 1; // 访问public的a
        int b2 = b + 1; // 访问static的b
        int c2 = c + 1; // 访问final的c
        int d2 = d + 1; // 访问private的d
        String str1 = method1(); // 访问实例方法method1
        String str2 = method2(); // 访问静态方法method2
    }
    public static void main(String[] args) {
        Inner i = new Outer().new Inner(); // 创建内部类实例
        System.out.println(i.a2); // 输出101
        System.out.println(i.b2); // 输出101
        System.out.println(i.c2); // 输出101
        System.out.println(i.d2); // 输出101
        System.out.println(i.str1); // 输出实例方法1
        System.out.println(i.str2); // 输出静态方法2
    }
}
```

`提示：如果有多层嵌套，则内部类可以访问所有外部类的成员。`

3）在外部类中不能直接访问内部类的成员，而必须通过内部类的实例去访问。如果类 A 包含内部类 B，类 B 中包含内部类 C，则在类 A 中不能直接访问类 C，而应该通过类 B 的实例去访问类 C。

4）外部类实例与内部类实例是一对多的关系，也就是说一个内部类实例只对应一个外部类实例，而一个外部类实例则可以对应多个内部类实例。

如果实例内部类 B 与外部类 A 包含有同名的成员 t，则在类 B 中 t 和 this.t 都表示 B 中的成员 t，而 A.this.t 表示 A 中的成员 t。

```java
public class Outer {
    int a = 10;
    class Inner {
        int a = 20;
        int b1 = a;
        int b2 = this.a;
        int b3 = Outer.this.a;
    }
    public static void main(String[] args) {
        Inner i = new Outer().new Inner();
        System.out.println(i.b1); // 输出20
        System.out.println(i.b2); // 输出20
        System.out.println(i.b3); // 输出10
    }
}
```

5）在实例内部类中不能定义 static 成员，除非同时使用 final 和 static 修饰。

#### 2.6.3 静态内部类

静态内部类是指使用 static 修饰的内部类。示例代码如下：

```java
public class Outer {
    static class Inner {
        // 静态内部类
    }
}
```

上述示例中的 Inner 类就是静态内部类。静态内部类有如下特点。

1）在创建静态内部类的实例时，不需要创建外部类的实例。

```java
public class Outer {
    static class Inner {
    }
}
class OtherClass {
    Outer.Inner oi = new Outer.Inner();
}
```

2）静态内部类中可以定义静态成员和实例成员。外部类以外的其他类需要通过完整的类名访问静态内部类中的静态成员，如果要访问静态内部类中的实例成员，则需要通过静态内部类的实例。

```java
public class Outer {
    static class Inner {
        int a = 0;    // 实例变量a
        static int b = 0;    // 静态变量 b
    }
}
class OtherClass {
    Outer.Inner oi = new Outer.Inner();
    int a2 = oi.a;    // 访问实例成员
    int b2 = Outer.Inner.b;    // 访问静态成员
}
```

3）静态内部类可以直接访问外部类的静态成员，如果要访问外部类的实例成员，则需要通过外部类的实例去访问。

```java
public class Outer {
    int a = 0;    // 实例变量
    static int b = 0;    // 静态变量
    static class Inner {
        Outer o = new Outer;
        int a2 = o.a;    // 访问实例变量
        int b2 = b;    // 访问静态变量
    }
}
```

#### 2.6.4 局部内部类

局部内部类是指在一个方法中定义的内部类。示例代码如下：

```java
public class Test {
    public void method() {
        class Inner {
            // 局部内部类
        }
    }
}
```

局部内部类有如下特点：

1）局部内部类与局部变量一样，不能使用访问控制修饰符（public、private 和 protected）和 static 修饰符修饰。

2）局部内部类只在当前方法中有效。

```java
public class Test {
    Inner i = new Inner();    // 编译出错
    Test.Inner ti = new Test.Inner();    // 编译出错
    Test.Inner ti2 = new Test().new Inner();    // 编译出错
    public void method() {
        class Inner{
        
        }
        Inner i = new Inner();
    }
}
```

3）局部内部类中不能定义 static 成员。

4）局部内部类中还可以包含内部类，但是这些内部类也不能使用访问控制修饰符（public、private 和 protected）和 static 修饰符修饰。

5）在局部内部类中可以访问外部类的所有成员。

6）在局部内部类中只可以访问当前方法中 final 类型的参数与变量。如果方法中的成员与外部类中的成员同名，则可以使用 <OuterClassName>.this.<MemberName> 的形式访问外部类中的成员。

```java
public class Test {
    int a = 0;
    int d = 0;
    public void method() {
        int b = 0;
        final int c = 0;
        final int d = 10;
        class Inner {
            int a2 = a;    // 访问外部类中的成员
            // int b2 = b;    // 编译出错
            int c2 = c;    // 访问方法中的成员
            int d2 = d;    // 访问方法中的成员
            int d3 = Test.this.d;    //访问外部类中的成员
        }
        Inner i = new Inner();
        System.out.println(i.d2);    // 输出10
        System.out.println(i.d3);    // 输出0
    }
    public static void main(String[] args) {
        Test t = new Test();
        t.method();
    }
}
```

#### 2.6.5 匿名类

匿名类是指没有类名的内部类，必须在创建时使用 new 语句来声明类。其语法形式如下：

```java
new <类或接口>() {
    // 类的主体
};
```

这种形式的 new 语句声明一个新的匿名类，它对一个给定的类进行扩展，或者实现一个给定的接口。使用匿名类可使代码更加简洁、紧凑，模块化程度更高。

匿名类有两种实现方式：

- 继承一个类，重写其方法。
- 实现一个接口（可以是多个），实现其方法。


下面通过代码来说明。

```java
public class Out {
    void show() {
        System.out.println("调用 Out 类的 show() 方法");
    }
}
public class TestAnonymousInterClass {
    // 在这个方法中构造一个匿名内部类
    private void show() {
        Out anonyInter = new Out() {
            // 获取匿名内部类的实例
            void show() {
                System.out.println("调用匿名类中的 show() 方法");
            }
        };
        anonyInter.show();
    }
    public static void main(String[] args) {
        TestAnonymousInterClass test = new TestAnonymousInterClass();
        test.show();
    }
}
```

程序的输出结果如下：

```
调用匿名类中的 show() 方法
```

从输出结果可以看出，匿名内部类有自己的实现。

提示：匿名内部类实现一个接口的方式与实现一个类的方式相同，这里不再赘述。

匿名类有如下特点：

1）匿名类和局部内部类一样，可以访问外部类的所有成员。如果匿名类位于一个方法中，则匿名类只能访问方法中 final 类型的局部变量和参数。

```java
public static void main(String[] args) {
    int a = 10;
    final int b = 10;
    Out anonyInter = new Out() {
        void show() {
            // System.out.println("调用了匿名类的 show() 方法"+a);    // 编译出错
            System.out.println("调用了匿名类的 show() 方法"+b);    // 编译通过
        }
    };
    anonyInter.show();
}
```

> 从 Java 8 开始添加了 Effectively final 功能，在 Java 8 及以后的版本中代码第 6 行不会出现编译错误。详情请见[Java8新特性：Effectively final](#jump1)

2）匿名类中允许使用非静态代码块进行成员初始化操作。

```java
Out anonyInter = new Out() {
    int i; {    // 非静态代码块
        i = 10;    //成员初始化
    }
    public void show() {
        System.out.println("调用了匿名类的 show() 方法"+i);
    }
};
```

3）匿名类的非静态代码块会在父类的构造方法之后被执行。

#### <span id="jump1">2.6.6 Java8新特性：Effectively final</span>

Java 中局部内部类和匿名内部类访问的局部变量必须由 final 修饰，以保证内部类和外部类的数据一致性。但从 Java 8 开始，我们可以不加 final 修饰符，由系统默认添加，当然这在 Java 8 以前的版本是不允许的。Java 将这个功能称为 Effectively final 功能。

编写同样的代码，分别在 Java 7 和 Java 8 下运行，代码如下：

```java
public class Test {
    public static void main(String[] args) {
        String name = "C语言中文网";
        new Runnable() {
            @Override
            public void run() {
                System.out.println(name);
            }
        }
    }
}
```

图 1 是 Java 7 编译结果，图 2 和图 3 是 Java 8 编译结果。

<img src="https://gitee.com/Kunaly/picture-bed/raw/master/img/image-20210115113359593.png" alt="image-20210115113359593" style="zoom:80%;" />

可以看到在 Java 7（图 1）中出现代码错误，提示我们必须显式的声明这个变量为 final 的（run 方法中代码为输出 name 语句，即`System.out.println(name);`）。

<img src="https://gitee.com/Kunaly/picture-bed/raw/master/img/image-20210115113428521.png" alt="image-20210115113428521" style="zoom:80%;" />

<img src="https://gitee.com/Kunaly/picture-bed/raw/master/img/image-20210115113446229.png" alt="image-20210115113446229" style="zoom:80%;" />

因为系统会默认添加 final 修饰符，所以在图 2 和图 3 中可以在匿名内部类中直接使用非 final 变量，而 final 修饰的局部变量不能在被重新赋值，所以图 3 中出现编译错误。也就是说从 Java 8 开始，它不要求程序员必须将访问的局部变量显式的声明为 final 的。只要该变量不被重新赋值就可以。

一个非 final 的局部变量或方法参数，其值在初始化后就从未更改，那么该变量就是 effectively final。在 Lambda 表达式中，使用局部变量的时候，也要求该变量必须是 final 的，所以 effectively final 在 Lambda 表达式上下文中非常有用。

Lambda 表达式在编程中是经常使用的，而匿名内部类是很少使用的。那么，我们在 Lambda 编程中每一个被使用到的局部变量都去显示定义成 final 吗？显然这不是一个好方法。所以，Java 8 引入了 effectively final 新概念。

总结一下，规则没有改变，Lambda 表达式和匿名内部类访问的局部变量必须是 final 的，只是不需要程序员显式的声明变量为 final 的，从而节省时间。

## 📚 References

-  廖雪峰JAVA教程
-  菜鸟教程
- C语言中文网

