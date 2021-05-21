# Java 异常处理

## 1.  Java 异常的概念

异常是程序中的一些错误，但并不是所有的错误都是异常，并且错误有时候是可以避免的。

比如说，你的代码少了一个分号，那么运行出来结果是提示是错误 java.lang.Error；如果你用System.out.println(11/0)，那么你是因为你用0做了除数，会抛出 java.lang.ArithmeticException 的异常。

异常发生的原因有很多，通常包含以下几大类：

- 用户输入了非法数据。
- 要打开的文件不存在。
- 网络通信时连接中断，或者JVM内存溢出。

这些异常有的是因为用户错误引起，有的是程序错误引起的，还有其它一些是因为物理错误引起的。-

要理解Java异常处理是如何工作的，你需要掌握以下三种类型的异常：

- **检查性异常：**最具代表的检查性异常是用户错误或问题引起的异常，这是程序员无法预见的。例如要打开一个不存在文件时，一个异常就发生了，这些异常在编译时不能被简单地忽略。
- **运行时异常：** 运行时异常是可能被程序员避免的异常。与检查性异常相反，运行时异常可以在编译时被忽略。
- **错误：** 错误不是异常，而是脱离程序员控制的问题。错误在代码中通常被忽略。例如，当栈溢出时，一个错误就发生了，它们在编译也检查不到的。

## 2. Java 异常继承框架

![img](https://gitee.com/Kunaly/picture-bed/raw/master/img/1075644-20181014104324864-1947735438.png)

常见非检查性异常：

| **异常**                        | **描述**                                                     |
| :------------------------------ | :----------------------------------------------------------- |
| ArithmeticException             | 当出现异常的运算条件时，抛出此异常。例如，一个整数"除以零"时，抛出此类的一个实例。 |
| ArrayIndexOutOfBoundsException  | 用非法索引访问数组时抛出的异常。如果索引为负或大于等于数组大小，则该索引为非法索引。 |
| ArrayStoreException             | 试图将错误类型的对象存储到一个对象数组时抛出的异常。         |
| ClassCastException              | 当试图将对象强制转换为不是实例的子类时，抛出该异常。         |
| IllegalArgumentException        | 抛出的异常表明向方法传递了一个不合法或不正确的参数。         |
| IllegalMonitorStateException    | 抛出的异常表明某一线程已经试图等待对象的监视器，或者试图通知其他正在等待对象的监视器而本身没有指定监视器的线程。 |
| IllegalStateException           | 在非法或不适当的时间调用方法时产生的信号。换句话说，即 Java 环境或 Java 应用程序没有处于请求操作所要求的适当状态下。 |
| IllegalThreadStateException     | 线程没有处于请求操作所要求的适当状态时抛出的异常。           |
| IndexOutOfBoundsException       | 指示某排序索引（例如对数组、字符串或向量的排序）超出范围时抛出。 |
| NegativeArraySizeException      | 如果应用程序试图创建大小为负的数组，则抛出该异常。           |
| NullPointerException            | 当应用程序试图在需要对象的地方使用 `null` 时，抛出该异常     |
| NumberFormatException           | 当应用程序试图将字符串转换成一种数值类型，但该字符串不能转换为适当格式时，抛出该异常。 |
| SecurityException               | 由安全管理器抛出的异常，指示存在安全侵犯。                   |
| StringIndexOutOfBoundsException | 此异常由 `String` 方法抛出，指示索引或者为负，或者超出字符串的大小。 |
| UnsupportedOperationException   | 当不支持请求的操作时，抛出该异常。                           |

常见检查性异常：

| **异常**                   | **描述**                                                     |
| :------------------------- | :----------------------------------------------------------- |
| ClassNotFoundException     | 应用程序试图加载类时，找不到相应的类，抛出该异常。           |
| CloneNotSupportedException | 当调用 `Object` 类中的 `clone` 方法克隆对象，但该对象的类无法实现 `Cloneable` 接口时，抛出该异常。 |
| IllegalAccessException     | 拒绝访问一个类的时候，抛出该异常。                           |
| InstantiationException     | 当试图使用 `Class` 类中的 `newInstance` 方法创建一个类的实例，而指定的类对象因为是一个接口或是一个抽象类而无法实例化时，抛出该异常。 |
| InterruptedException       | 一个线程被另一个线程中断，抛出该异常。                       |
| NoSuchFieldException       | 请求的变量不存在                                             |
| NoSuchMethodException      | 请求的方法不存在                                             |

 Throwable 类的主要方法:

| **序号** | **方法及说明**                                               |
| :------- | :----------------------------------------------------------- |
| 1        | **public String getMessage()** 返回关于发生的异常的详细信息。这个消息在Throwable 类的构造函数中初始化了。 |
| 2        | **public Throwable getCause()** 返回一个Throwable 对象代表异常原因。 |
| 3        | **public String toString()** 使用getMessage()的结果返回类的串级名字。 |
| 4        | **public void printStackTrace()** 打印toString()结果和栈层次到System.err，即错误输出流。 |
| 5        | **public StackTraceElement [] getStackTrace()** 返回一个包含堆栈层次的数组。下标为0的元素代表栈顶，最后一个元素代表方法调用堆栈的栈底。 |
| 6        | **public Throwable fillInStackTrace()** 用当前的调用栈层次填充Throwable 对象栈层次，添加到栈层次任何先前信息中。 |

## 3. 异常处理

### 3.1 try-catch

```java
try{
    //code that might generate exceptions    
}catch(Exception e){
    //the code of handling exception1
}
```

使用 try 和 catch 关键字可以捕获异常。try/catch 代码块放在异常可能发生的地方。

Catch 语句包含要捕获异常类型的声明。当保护代码块中发生一个异常时，try 后面的 catch 块就会被检查。

如果发生的异常包含在 catch 块中，异常会被传递到该 catch 块，这和传递一个参数到方法是一样。

**实例：**

下面的例子中声明有两个元素的一个数组，当代码试图访问数组的第三个元素的时候就会抛出一个异常。

```java
public class ExcepTest {
    public static void main(String args[]){
        try{
            int a[] = new int[2];
            System.out.println("Access element three :" + a[3]);
        }catch(ArrayIndexOutOfBoundsException e){
            System.out.println("Exception thrown  :" + e);
        }
        System.out.println("Out of the block");
    }
}
```

以上代码编译运行输出结果如下：

```java
Exception thrown  :java.lang.ArrayIndexOutOfBoundsException: 3
Out of the block
```

### 3.2 多重捕获

一个 try 代码块后面跟随多个 catch 代码块的情况就叫多重捕获。

多重捕获块的语法如下所示：

```java
try{
   // 程序代码
}catch(异常类型1 异常的变量名1){
  // 程序代码
}catch(异常类型2 异常的变量名2){
  // 程序代码
}catch(异常类型3 异常的变量名3){
  // 程序代码
}
```

上面的代码段包含了 3 个 catch块。

可以在 try 语句后面添加任意数量的 catch 块。

如果保护代码中发生异常，异常被抛给第一个 catch 块。

如果抛出异常的数据类型与 `ExceptionType1` 匹配，它在这里就会被捕获。

如果不匹配，它会被传递给第二个 catch 块。

如此，直到异常被捕获或者通过所有的 catch 块。

### 3.3 throw

到目前为止，我们只是获取了被Java运行时系统引发的异常。然而，我们还可以用`throw`语句抛出明确的异常。`Throw`的语法形式如下：

```java
throw ThrowableInstance;
```

这里的ThrowableInstance一定是`Throwable`类类型或者`Throwable`子类类型的一个对象。

程序执行完`throw`语句之后立即停止；`throw`后面的任何语句不被执行，最邻近的`try`块用来检查它是否含有一个与异常类型匹配的`catch`语句。如果发现了匹配的块，控制转向该语句；如果没有发现，次包围的`try`块来检查，以此类推。如果没有发现匹配的`catch`块，默认异常处理程序中断程序的执行并且打印堆栈轨迹。

```java
public class ExcepTest {
    public static void main(String args[]){
        try{
            proc();
        }catch(NullPointerException e){
            System.out.println("Recaught: "+e);
        }
    }

    static void proc(){
        try{
            throw new NullPointerException("demo");
        }catch(NullPointerException e){
            System.out.println("Caught inside proc");
            throw e;
        }
    }

}
```

运行结果：

```java
Caught inside proc
 
Recaught: java.lang.NullPointerException: demo
```

该程序两次处理相同的错误，首先，`main()`方法设立了一个异常关系然后调用proc()。proc()方法设立了另一个异常处理关系并且立即抛出一个`NullPointerException`实例，`NullPointerException`在`main()`中被再次捕获。

该程序阐述了怎样创建Java的标准异常对象，特别注意这一行：`throw new NullPointerException("demo");`

此处`new`用来构造一个`NullPointerException`实例，所有的Java内置的运行时异常有两个构造方法：一个没有参数，一个带有一个字符串参数。当用第二种形式时，参数指定描述异常的字符串。如果对象用作`print()`或者`println()`的参数时，该字符串被显示。这同样可以通过调用getMessage()来实现，getMessage()是由`Throwable`定义的。

### 3.4 throws

如果一个方法可以导致一个异常但不处理它，它必须指定这种行为以使方法的调用者可以保护它们自己而不发生异常。要做到这点，我们可以在方法声明中包含一个`throws`子句。一个`throws`子句列举了一个方法可能引发的所有异常类型。这对于除了`Error`或`RuntimeException`及它们子类以外类型的所有异常是必要的。一个方法可以引发的所有其他类型的异常必须在`throws`子句中声明，否则会导致编译错误。

下面是`throws`子句的方法声明的通用形式：

```java
public void info() throws Exception
{
   //body of method
}
```

Exception 是该方法可能引发的所有的异常,也可以是异常列表，中间以逗号隔开。

**实例：**

```java
class TestThrows{
    static void throw1() throws IllegalAccessException {
        System.out.println("Inside throw1 . ");
        throw new IllegalAccessException("demo");
    }
    public static void main(String[] args){
        try {
            throw1();
        }catch(IllegalAccessException e ){
            System.out.println("Caught " + e);
        }
    }
}
```

`Throws`抛出异常的规则：

- 如果是不受检查异常（`unchecked exception`），即`Error`、`RuntimeException`或它们的子类，那么可以不使用`throws`关键字来声明要抛出的异常，编译仍能顺利通过，但在运行时会被系统抛出。
- 必须声明方法可抛出的任何检查异常（`checked exception`）。即如果一个方法可能出现检查异常，要么用`try-catch`语句捕获，要么用`throws`子句声明将它抛出，否则会导致编译错误。
- 当抛出了异常，该方法的调用者才必须处理或者重新抛出该异常。当方法的调用者无力处理该异常的时候，应该继续抛出。 
- 调用方法必须遵循任何可查异常的处理和声明规则。若覆盖一个方法，则不能声明与覆盖方法不同的异常。声明的任何异常必须是被覆盖方法所声明异常的同类或子类。

### 3.5 finally

finally 关键字用来创建在 try 代码块后面执行的代码块。

无论是否发生异常，finally 代码块中的代码总会被执行。

在 finally 代码块中，可以运行清理类型等收尾善后性质的语句。

finally 代码块出现在 catch 代码块最后，语法如下：

```java
try{
  // 程序代码
}catch(异常类型1 异常的变量名1){
  // 程序代码
}catch(异常类型2 异常的变量名2){
  // 程序代码
}finally{
  // 程序代码
}
```

**实例：**

```java
public class ExcepTest{
  public static void main(String args[]){
    int a[] = new int[2];
    try{
       System.out.println("Access element three :" + a[3]);
    }catch(ArrayIndexOutOfBoundsException e){
       System.out.println("Exception thrown  :" + e);
    }
    finally{
       a[0] = 6;
       System.out.println("First element value: " +a[0]);
       System.out.println("The finally statement is executed");
    }
  }
}
```

输出结果：

```java
Exception thrown  :java.lang.ArrayIndexOutOfBoundsException: 3
First element value: 6
The finally statement is executed
```

**注意：**

- catch 不能独立于 try 存在。
- 在 try/catch 后面添加 finally 块并非强制性要求的。
- try, catch, finally 块之间不能添加任何代码。
- `finally`子句是可选项，可以有也可以无，但是每个`try`语句至少需要一个`catch`或者`finally`子句。
- 如果`finally`块与一个`try`联合使用，`finally`块将在`try`结束之前执行。

## 4. 异常链

异常链顾名思义就是将异常发生的原因一个传一个串起来，即把底层的异常信息传给上层，这样逐层抛出。 Java API文档中给出了一个简单的模型：

```java
try {   
    lowLevelOp();   
} catch (LowLevelException le) {   
    throw (HighLevelException) new HighLevelException().initCause(le);   
}
```

当程序捕获到了一个底层异常，在处理部分选择了继续抛出一个更高级别的新异常给此方法的调用者。 这样异常的原因就会逐层传递。这样，位于高层的异常递归调用getCause()方法，就可以遍历各层的异常原因。 这就是`Java异常链`的原理。异常链的实际应用很少，发生异常时候逐层上抛不是个好注意， 上层拿到这些异常又能奈之何？而且异常逐层上抛会消耗大量资源， 因为要保存一个完整的异常链信息.

## 5. 自定义异常

使用Java内置的异常类可以描述在编程时出现的大部分异常情况。除此之外，用户还可以自定义异常。用户自定义异常类，只需继承`Exception`类即可。

在程序中使用自定义异常类，大体可分为以下几个步骤:

- 创建自定义异常类。
- 在方法中通过`throw`关键字抛出异常对象。
- 如果在当前抛出异常的方法中处理异常，可以使用`try-catch`语句捕获并处理；否则在方法的声明处通过`throws`关键字指明要抛出给方法调用者的异常，继续进行下一步操作。
- 在出现异常方法的调用者中捕获并处理异常。

举例自定义异常：

```java
class MyException extends Exception {
    private int detail;
    MyException(int a){
        detail = a;
    }
    public String toString(){
        return "MyException ["+ detail + "]";
    }
}
public class TestMyException{
    static void compute(int a) throws MyException{
        System.out.println("Called compute(" + a + ")");
        if(a > 10){
            throw new MyException(a);
        }
        System.out.println("Normal exit!");
    }
    public static void main(String [] args){
        try{
            compute(1);
            compute(20);
        }catch(MyException me){
            System.out.println("Caught " + me);
        }
    }
}
```

运行结果：

```java
Called compute(1)
Normal exit!
Called compute(20)
Caught MyException [20]
```



## 📚 References

- 菜鸟教程 JAVA
- https://www.cnblogs.com/happyliu/p/9785698.html
- https://blog.csdn.net/q_all_is_well/article/details/83020710

