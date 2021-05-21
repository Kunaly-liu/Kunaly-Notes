# Java IO流

## 1.  IO 流简介

### 1.1  流的概念

流是一组有顺序的，有起点和终点的字节集合，是对数据传输的总称或抽象。即数据在两设备间的传输称为流，**流的本质是数据传输，根据数据传输特性将流抽象为各种类，方便更直观的进行数据操作。** 

### 1.2 IO流的分类

- 根据处理数据类型的不同分为：字符流和字节流
- 根据数据流向不同分为：输入流和输出流

#### 字符流和字节流

字符流的由来： 因为数据编码的不同，而有了对字符进行高效操作的流对象。本质其实就是基于字节流读取时，去查了指定的码表。 字节流和字符流的区别：

- 读写单位不同：字节流以字节（8bit）为单位，字符流以字符为单位，根据码表映射字符，一次可能读多个字节。
- 处理对象不同：字节流能处理所有类型的数据（如图片、avi等），而字符流只能处理字符类型的数据。

结论：只要是处理纯文本数据，就优先考虑使用字符流。 除此之外都使用字节流。

#### 输入流和输出流

对输入流只能进行读操作，对输出流只能进行写操作，程序中需要根据待传输数据的不同特性而使用不同的流。

### 1.3 Java IO流类层次图

Java.io包下的IO流有很多：

![img](https://gitee.com/Kunaly/picture-bed/raw/master/img/iostream2xx.png)

其中，以Stream结尾的为字节流，以Writer或者Reader结尾的为字符流。所有的输入流都是抽象类IuputStream（字节输入流）或者抽象类Reader（字符输入流）的子类，所有的输出流都是抽象类OutputStream(字节输出流)或者抽象类Writer(字符输出流)的子类。字符流能实现的功能字节流都能实现，反之不一定。如：图片，视频等二进制文件，只能使用字节流读写。

## 2. 字符流

### FileReader

| 构造方法摘要                                                 |
| ------------------------------------------------------------ |
| `FileReader(File file)`      在给定从中读取数据的 `File` 的情况下创建一个新 `FileReader`。 |
| `FileReader(FileDescriptor fd)`      在给定从中读取数据的 `FileDescriptor` 的情况下创建一个新 `FileReader`。 |
| `FileReader(String fileName)`      在给定从中读取数据的文件名的情况下创建一个新 `FileReader`。 |

###  FileWriter

| 构造方法摘要                                                 |
| ------------------------------------------------------------ |
| `FileWriter(File file)`      根据给定的 File 对象构造一个 FileWriter 对象。 |
| `FileWriter(File file, boolean append)`      根据给定的 File 对象构造一个 FileWriter 对象。 |
| `FileWrite*(FileDescriptor fd)`      构造与某个文件描述符相关联的 FileWriter 对象。 |
| `FileWriter(String fileName)`      根据给定的文件名构造一个 FileWriter 对象。 |
| `FileWriter(String fileName, boolean append)`      根据给定的文件名以及指示是否附加写入数据的 boolean 值来构造 FileWriter 对象。 |

使用FileReader和FileWriter类完成文本文件复制：

```java
package IODemo;

import java.io.FileNotFoundException;
import java.io.FileReader;
import java.io.FileWriter;
import java.io.IOException;

public class CopyFile {

    public static void main(String[] args) throws IOException {
        //创建输入流对象
        FileReader fr = new FileReader("D:\\Test\\copyfrom.txt");//文件不存在会抛出java.io.FileNotFoundException
        //创建输出流对象
        FileWriter fw = new FileWriter("D:\\Test\\copyto.txt");
        /*创建输出流做的工作：
         * 1、调用系统资源创建了一个文件
         * 2、创建输出流对象
         * 3、把输出流对象指向文件
         * */
        //文本文件复制，一次读一个字符
        method1(fr, fw);
        //文本文件复制，一次读一个字符数组
        method2(fr, fw);
        fr.close();
        fw.close();
    }

    public static void method1(FileReader fr, FileWriter fw) throws IOException {
        int ch;
        while((ch=fr.read())!=-1) {//读数据
             fw.write(ch);//写数据
         }
        fw.flush();
    }

     public static void method2(FileReader fr, FileWriter fw) throws IOException {
        char chs[]=new char[1024];
         int len=0;
         while((len=fr.read(chs))!=-1) {//读数据
            fw.write(chs,0,len);//写数据
         }
         fw.flush();
    }

}
```

## 3. 字符缓冲流

字符缓冲流具备文本特有的表现形式：行操作。

### BufferedReader

```java
public class BufferedReader extends Reader
```

1. 从字符输入流中读取文本，缓冲各个字符，从而实现字符、数组和行的高效读取。

2. 可以指定缓冲区的大小，或者可使用默认的大小。大多数情况下，默认值就足够大了。

3. 通常，Reader 所作的每个读取请求都会导致对底层字符或字节流进行相应的读取请求。因此，建议用 BufferedReader 包装所有其 read() 操作可能开销很高的 Reader（如 FileReader 和 InputStreamReader）。例如:

   ```java
    BufferedReader in
      = new BufferedReader(new FileReader("foo.in"));
   ```

4. 将缓冲指定文件的输入。如果没有缓冲，则每次调用 `read()` 或` readLine() `都会导致从文件中读取字节，并将其转换为字符后返回，而这是极其低效的。 

### **BufferedWriter** 

```java
public class BufferedWriter extends Writer
```

1. 将文本写入字符输出流，缓冲各个字符，从而提供单个字符、数组和字符串的高效写入。

2. 可以指定缓冲区的大小，或者接受默认的大小。在大多数情况下，默认值就足够大了。

3. 该类提供了 **newLine() 方法**，它使用平台自己的行分隔符概念，此概念由**系统属性 `line.separator`** 定义。并非所有平台都使用新行符 ('\n') 来终止各行。因此调用此方法来终止每个输出行要优于直接写入新行符。

4. 通常 Writer 将其输出立即发送到底层字符或字节流。除非要求提示输出，否则建议用 BufferedWriter 包装所有其 write() 操作可能开销很高的 Writer（如 FileWriters 和 OutputStreamWriters）。例如:

   ```java
    PrintWriter out
      = new PrintWriter(new BufferedWriter(new FileWriter("foo.out")));
   ```

5. 缓冲 PrintWriter 对文件的输出。如果没有缓冲，则每次调用 print() 方法会导致将字符转换为字节，然后立即写入到文件，而这是极其低效的。

 使用BufferedReader和BufferedWriter完成文件复制：

```java
package IODemo;

import java.io.*;

public class CopyFile2 {
    public static void main(String[] args) throws IOException {
        //创建输入流对象
        BufferedReader br = new BufferedReader(new FileReader("D:\\Test\\copyfrom.txt"));//文件不存在会抛出java.io.FileNotFoundException
        //创建输出流对象
        BufferedWriter bw = new BufferedWriter(new FileWriter("D:\\Test\\copyto.txt"));
        //文本文件复制
        char[] chs = new char[1024];
        int len = 0;
        while ((len = br.read(chs)) != -1) {
            bw.write(chs, 0, len);
        }
        //释放资源
        br.close();
        bw.close();
    }
}
```

**缓冲区的工作原理：**

1. 使用了底层流对象从具体设备上获取数据，并将数据存储到缓冲区的数组内。
2. 通过缓冲区的read()方法从缓冲区获取具体的字符数据，这样就提高了效率。
3. 如果用read方法读取字符数据，并存储到另一个容器中，直到读取到了换行符时，将另一个容器临时存储的数据转成字符串返回，就形成了readLine()功能。

## 4. 字节流

### FileInputStream

```java
public class FileInputStream extends InputStream
```

1. `FileInputStream` 从文件系统中的某个文件中获得输入字节。哪些文件可用取决于主机环境。
2. `FileInputStream` 用于读取诸如图像数据之类的原始字节流。

| 构造方法摘要                                                 |
| ------------------------------------------------------------ |
| `FileInputStream(File file)`      通过打开一个到实际文件的连接来创建一个 `FileInputStream`，该文件通过文件系统中的 `File` 对象 `file` 指定。 |
| `FileInputStream(FileDescriptor fdObj)`      通过使用文件描述符 `fdObj` 创建一个 `FileInputStream`，该文件描述符表示到文件系统中某个实际文件的现有连接。 |
| `FileInputStream(String name)`      通过打开一个到实际文件的连接来创建一个 `FileInputStream`，该文件通过文件系统中的路径名 `name` 指定。 |

### FileOutputStream

```java
public class FileOutputStream extends OutputStream
```

1. 文件输出流是用于将数据写入 `File` 或 `FileDescriptor` 的输出流。文件是否可用或能否可以被创建取决于基础平台。特别是某些平台一次只允许一个 `FileOutputStream`（或其他文件写入对象）打开文件进行写入。在这种情况下，如果所涉及的文件已经打开，则此类中的构造方法将失败。
2.  `FileOutputStream` 用于写入诸如图像数据之类的原始字节的流。

| 构造方法摘要                                                 |
| ------------------------------------------------------------ |
| `FileOutputStream(File file)`      创建一个向指定 `File` 对象表示的文件中写入数据的文件输出流。 |
| `FileOutputStream(File file, boolean append)`      创建一个向指定 `File` 对象表示的文件中写入数据的文件输出流。 |
| `FileOutputStream(FileDescriptor fdObj)`      创建一个向指定文件描述符处写入数据的输出文件流，该文件描述符表示一个到文件系统中的某个实际文件的现有连接。 |
| `FileOutputStream(String name)`      创建一个向具有指定名称的文件中写入数据的输出文件流。 |
| `FileOutputStream(String name, boolean append)`      创建一个向具有指定 `name` 的文件中写入数据的输出文件流。 |

例：使用字节流复制图片：

```java
package IODemo;

import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.FileOutputStream;
import java.io.IOException;

public class CopyImg {
    public static void main(String[] args) throws IOException {
         FileInputStream fin=new FileInputStream("D:\\Test\\Img.jpg");
         FileOutputStream fout=new FileOutputStream("D:\\Test\\ImgCopy.jpg");
         int len=0;
         byte[] buff=new byte[1024];
         while((len=fin.read(buff))!=-1) {
             fout.write(buff, 0, len);
         }
         fin.close();
         fout.close();
    }
}
```

## 5. 字节缓冲流

### BufferedInputStream

```java
public class BufferedInputStream extends FilterInputStream
```

`BufferedInputStream` 为另一个输入流添加一些功能，即缓冲输入以及支持 `mark` 和 `reset` 方法的能力。在创建 `BufferedInputStream` 时，会创建一个内部缓冲区数组。在读取或跳过流中的字节时，可根据需要从包含的输入流再次填充该内部缓冲区，一次填充多个字节。`mark` 操作记录输入流中的某个点，`reset` 操作使得在从包含的输入流中获取新字节之前，再次读取自最后一次 `mark` 操作后读取的所有字节。

### BufferedOutputStream

```java
public class BufferedOutputStream extends FilterOutputStream
```

该类实现缓冲的输出流。通过设置这种输出流，应用程序就可以将各个字节写入底层输出流中，而不必针对每次字节写入调用底层系统。

例：使用字节缓冲流实现图片的复制

```java
package IODemo;

import java.io.*;

public class CopyImg2 {
    public static void main(String[] args) throws IOException {
         BufferedInputStream bfin = new BufferedInputStream(new FileInputStream("D:\\Test\\Img.jpg"));
        BufferedOutputStream bfout = new BufferedOutputStream(new FileOutputStream("D:\\Test\\ImgCopy2.jpg"));
         int len=0;
         byte[] buff=new byte[1024];
         while((len=bfin.read(buff))!=-1) {
             bfout.write(buff, 0, len);
         }
         bfin.close();
         bfout.close();
    }
}
```

## 6. 转换流

`InputStreamReader`和`OutputStreamWriter`是字符和字节的桥梁，也可称之为字符转换流。原理：字节流+编码。

`FileReader`和`FileWriter`作为子类，仅作为操作字符文件的便捷类存在。当操作的字符文件，使用的是默认编码表时可以不用父类，而直接使用子类完成操作，简化代码。

一旦要指定其他编码时，不能使用子类，必须使用字符转换流。

### InputStreamReader

```java
public class InputStreamReader extends Reader
```

1. InputStreamReader 是字节流通向字符流的桥梁：它使用指定的 `charset` 读取字节并将其解码为字符。它使用的字符集可以由名称指定或显式给定，或者可以接受平台默认的字符集。

2. 每次调用 InputStreamReader 中的一个 read() 方法都会导致从底层输入流读取一个或多个字节。要启用从字节到字符的有效转换，可以提前从底层流读取更多的字节，使其超过满足当前读取操作所需的字节。

3. 为了达到最高效率，可以考虑在 BufferedReader 内包装 InputStreamReader。例如:

   ```java
    BufferedReader in = new BufferedReader(new InputStreamReader(System.in))；//重要
   ```

   例：使用标准输入流，读取键盘录入的数据，存储到文件a.txt中：

   ```java
   package IODemo;
   
   import java.io.*;
   
   /**
    * 使用标准输入流，读取键盘录入的数据，存储到文件a.txt中
    * 将字节输入流转换成字符输入流，InputStreamReader
    */
   public class InputStreamReaderDemo {
       public static void main(String[] args) throws IOException {
            //method1();
            //method2();
            method3();
       }
   	
       //在 BufferedReader 内包装 InputStreamReader
       public static void method3() throws IOException {
           //创建输入流对象
           BufferedReader r=new BufferedReader(new InputStreamReader(System.in));
           //创建输出流对象
           FileWriter fw=new FileWriter("D:\\Test\\a.txt");
           //读写数据
           char[] chs=new char[1024];
           int len;
           while((len=r.read(chs))!=-1) {
               fw.write(chs,0,len);
               fw.flush();
           }
           //释放资源
           r.close();
           fw.close();
       }
   
       public static void method2() throws IOException {
            //创建字符输入流对象
            InputStream is=System.in;
            Reader r=new InputStreamReader(is);
            //创建输出流对象
            FileWriter fw=new FileWriter("D:\\Test\\a.txt");
   
            //读写数据
            char[] chs=new char[1024];
            int len;
            while((len=r.read(chs))!=-1) {
                fw.write(chs,0,len);
                fw.flush();
            }
            //释放资源
            is.close();
            fw.close();
        }
   
        public static void method1() throws IOException {
            //创建字节输入流对象
            InputStream is=System.in;
            //创建输出流对象
            FileWriter fw=new FileWriter("D:\\Test\\a.txt");
   
            //读写数据
            byte[] bys=new byte[1024];
            int len;
            while((len=is.read(bys))!=-1) {
                fw.write(new String(bys,0,len));
                fw.flush();
            }
            //释放资源
            is.close();
            fw.close();
        }
   }
   ```

### OutputStreamWriter

```java
public class OutputStreamWriter extends Writer
```

1. OutputStreamWriter 是字符流通向字节流的桥梁：可使用指定的 `charset` 将要写入流中的字符编码成字节。它使用的字符集可以由名称指定或显式给定，否则将接受平台默认的字符集。
2. 每次调用 write() 方法都会导致在给定字符（或字符集）上调用编码转换器。在写入底层输出流之前，得到的这些字节将在缓冲区中累积。可以指定此缓冲区的大小，不过，默认的缓冲区对多数用途来说已足够大。注意，传递给 write() 方法的字符没有缓冲。
3. 为了获得最高效率，可考虑将 OutputStreamWriter 包装到 BufferedWriter 中，以避免频繁调用转换器。例如：

```java
Writer out = new BufferedWriter(new OutputStreamWriter(System.out));//重要
```

例如：利用标准输出流将文本输出到命令行：

```java
package IODemo;

import java.io.*;

/**
  * 读取项目目录下的文件copy.java,并输出到命令行
  * 由于标准输出流是字节输出流，所以只能输出字节或者字节数组，但是我们读取到的数据是字符串，如果想进行输出，
  * 还需要转换成字节数组(method1)。
  * 要想通过标准输出流输出字符串，把标准输出流转换成一种字符输出流即可(method2)。
  */
public class OutputStreamWriterDemo {
     public static void main(String[] args) throws IOException {
         //method1();
         //method2();
         method3();
     }


     public static void method3() throws IOException {
         //创建输入流
         File f = new File("D:/Test/copy.txt");
         BufferedReader br=new BufferedReader(new FileReader(f));
         //创建输出流
         BufferedWriter bw=new BufferedWriter(new OutputStreamWriter(System.out));
         String line;//用于接收读到的数据
         while((line=br.readLine())!=null) {
             bw.write(line);
             bw.write("\r\n");
         }
         br.close();
         bw.close();
     }

     public static void method2() throws FileNotFoundException, IOException {
         //创建输入流
         BufferedReader br=new BufferedReader(new FileReader("D:/Test/copy.txt"));
         //创建输出流
         //OutputStream os=System.out;
         Writer w=new OutputStreamWriter(System.out);//多态，父类引用指向子类对象
         String line;//用于接收读到的数据
         while((line=br.readLine())!=null) {
             w.write(line);
             w.write("\r\n");
         }
         br.close();
         w.close();
     }

     public static void method1() throws FileNotFoundException, IOException {
         //创建输入流
         BufferedReader br=new BufferedReader(new FileReader("D:/Test/copy.txt"));
         //创建输出流
         OutputStream os=System.out;
         String line;//用于接收读到的数据
         while((line=br.readLine())!=null) {
             os.write(line.getBytes());
             os.write("\r\n".getBytes());
         }
         br.close();
         os.close();
     }
}
```

```java
package IODemo;

import java.io.*;

public class TransStreamDemo {
    public static void main(String[] args) throws IOException {

        writeCN();
        readCN();

    }
    public static void readCN() throws UnsupportedEncodingException, FileNotFoundException, IOException {
         //InputStreamReader将字节数组使用指定的编码表解码成文字
         InputStreamReader isr=new InputStreamReader(new FileInputStream("temp.txt"),"utf-8");
         char[] buff=new char[1024];
         int len=isr.read(buff);
         System.out.println(new String(buff,0,len));
         isr.close();
    }

     public static void writeCN() throws UnsupportedEncodingException, FileNotFoundException, IOException {
         //OutputStreamWriter将字符串按照指定的编码表转成字节，再使用字符流将这些字节写出去
         OutputStreamWriter osw=new OutputStreamWriter(new FileOutputStream("temp.txt"),"utf-8");//本身是字符流，传入字节流
         osw.write("你好");
         osw.close();
     }
}
```

## 7. 打印流

### PrintWriter

```java
public class PrintWriter extends Writer
```

1. 向文本输出流打印对象的格式化表示形式。此类实现在 `PrintStream` 中的所有 `print` 方法。不能输出字节，但是可以输出其他任意类型。
2. 与 `PrintStream` 类不同，如果启用了自动刷新，则只有在调用 `println`、`printf` 或 `format` 的其中一个方法时才可能完成此操作，而不是每当正好输出换行符时才完成。这些方法使用平台自有的行分隔符概念，而不是换行符。
3. 此类中的方法不会抛出 I/O 异常，尽管其某些构造方法可能抛出异常。客户端可能会查询调用 `checkError()` 是否出现错误。

```java
package IODemo;

import java.io.FileWriter;
import java.io.IOException;
import java.io.PrintWriter;

/**
 * 注意：创建FileWriter对象时boolean参数表示是否追加；
 *      而创建打印流对象时boolean参数表示是否自动刷新
 */
public class PrintWriterDemo {
    public static void main(String[] args) throws IOException {
        //PrintWriter pw=new PrintWriter("print.txt");
        PrintWriter pw=new PrintWriter(new FileWriter("print.txt"),true);
        pw.write("测试打印流");
        pw.println("此句之后换行");
        pw.println("特有功能：自动换行和自动刷新");
        pw.println("利用构造器设置自动刷新");
        pw.close();
    }
}
```

例：使用字符打印流复制文本文件：

```java
package IODemo;

import java.io.*;

/**
 * 使用字符打印流复制文本文件
 */
 public class PrintWriterDemo {
     public static void main(String[] args) throws IOException {
         BufferedReader br=new BufferedReader(new FileReader("copy.java"));
         PrintWriter pw=new PrintWriter("printcopy.java");
         String line;
         while((line=br.readLine())!=null) {
             pw.println(line);
         }
         br.close();
         pw.close();
     }
 }
```

### PrintStream

```java
public class PrintStream extends FilterOutputStreamimplements Appendable, Closeable
```

1. `PrintStream` 为其他输出流添加了功能（增加了很多打印方法），使它们能够方便地打印各种数据值表示形式(例如：希望写一个整数，到目的地整数的表现形式不变。字节流的write方法只将一个整数的最低字节写入到目的地，比如写`fos.write(97)`，到目的地（记事本打开文件）会变成字符'a',需要手动转换：`fos.write(Integer.toString(97).getBytes())`;而采用`PrintStream：ps.print(97)`，则可以保证数据的表现形式)。

   ```java
    //PrintStream的print方法 
    public void print(int i) {
          write(String.valueOf(i));
    }
   ```

2. 与其他输出流不同，`PrintStream` 永远不会抛出 `IOException`；而是，异常情况仅设置可通过` checkError `方法测试的内部标志。
   另外，为了自动刷新，可以创建一个` PrintStream`；这意味着可在写入 byte 数组之后自动调用 flush 方法，可调用其中一个 `println` 方法，或写入一个换行符或字节 ('\n')。

3. `PrintStream` 打印的所有字符都使用平台的默认字符编码转换为字节。在需要写入字符而不是写入字节的情况下，应该使用 `PrintWriter `类。  


例：使用字节打印流复制文本文件。

   ```java
   package IODemo;
   
   import java.io.*;
   
   /**
    * 使用字节打印流复制文本文件
    */
    public class PrintStreamDemo {
        public static void main(String[] args) throws IOException {
            BufferedReader br=new BufferedReader(new FileReader("copy.java"));
            PrintStream ps=new PrintStream("printcopy2.java");
            String line;
            while((line=br.readLine())!=null) {
                ps.println(line);
            }
            br.close();
            ps.close();
        }
    }
   ```

## 8. 对象操作流

### ObjectInputStream

```java
public class ObjectOutputStream extends OutputStream implements ObjectOutput, ObjectStreamConstants
```

1. ObjectOutputStream 将 Java 对象的基本数据类型和图形写入 OutputStream。只能使用 ObjectInputStream 读取（重构）对象。
2. 只能将支持 java.io.Serializable 接口的对象写入流中。
3. writeObject 方法用于将对象写入流中。所有对象（包括 String 和数组）都可以通过 writeObject 写入。可将多个对象或基元写入流中。必须使用与写入对象时相同的类型和顺序从相应 ObjectInputstream 中读回对象。

构造方法：`ObjectOutputStream(OutputStream out)` 　　创建写入指定 OutputStream 的 ObjectOutputStream。

### ObjectOutputStream

```java
public class ObjectInputStream extends InputStream implements ObjectInput, ObjectStreamConstants
```

1. ObjectInputStream 对以前使用 ObjectOutputStream 写入的基本数据和对象进行反序列化。
2. 只有支持 java.io.Serializable 或 java.io.Externalizable 接口的对象才能从流读取。
3. `readObject` 方法用于从流读取对象。应该使用 Java 的安全强制转换来获取所需的类型。在 Java 中，字符串和数组都是对象，所以在序列化期间将其视为对象。读取时，需要将其强制转换为期望的类型。 

例：对象读写：

```java
package IODemo;

import java.io.*;

/**
 *使用对象输出流写对象和对象输入流读对象
 *注意：如果Student没有序列化，会抛出java.io.NotSerializableException
 *Serializable：序列号，是一个标识接口，只起标识作用，没有方法
 *当一个类的对象需要IO流进行读写的时候，这个类必须实现接口
 */
public class ObjectOperate {
    public static void main(String[] args) throws IOException, ClassNotFoundException {
        writeObject();
        //创建对象输入流的对象
        ObjectInputStream ois=new ObjectInputStream(new FileInputStream("a.txt"));
        //读取对象
        try {
            while(true){
                Object obj=ois.readObject();
                System.out.println(obj);
            }
        }catch(EOFException e){
            System.out.println("读到了文件末尾");
        }
        //释放资源
        ois.close();
    }
    public static void writeObject() throws FileNotFoundException, IOException {
        //创建对象输出流的对象
        FileOutputStream fos=new FileOutputStream("a.txt");
        ObjectOutputStream oos=new ObjectOutputStream(fos);
        //创建学生对象
        Student s1=new Student("张三",20);
        Student s2=new Student("李四",30);
        Student s3=new Student("王五",10);
        //写出学生对象
        oos.writeObject(s1);
        oos.writeObject(s2);
        oos.writeObject(s3);
        //释放资源
    }
}
```

```java
package IODemo;

import java.io.*;
import java.util.ArrayList;

/**
 * 使用对象输出流写对象和对象输入流读对象
 * 解决读取对象出现异常的问题,使用集合类
 */
public class ObjectOperate2 {
    public static void main(String[] args) throws IOException, ClassNotFoundException {
        listMethod();
        //创建对象输入流对象
        ObjectInputStream ois=new ObjectInputStream(new FileInputStream("b.txt"));
        //读取数据
        Object obj=ois.readObject();
        //System.out.println(obj);
        //向下转型
        ArrayList<Student> list=(ArrayList<Student>) obj;
        for(Student s:list) {
            System.out.println(s);
        }
        //释放资源
        ois.close();
    }

    public static void listMethod() throws IOException, FileNotFoundException {
        //创建对象输出流的对象
        ObjectOutputStream oos=new ObjectOutputStream(new FileOutputStream("b.txt"));
        //创建集合类
        ArrayList<Student> list=new ArrayList<Student>();
        //添加学生对象
        list.add(new Student("zhangsan",20));
        list.add(new Student("lisi",30));
        //写出集合对象
        oos.writeObject(list);
        //释放资源
        oos.close();
    }

}
```

**序列化接口Serializable的作用：**没有方法，不需要覆写，是一个标记接口为了启动一个序列化功能。唯一的作用就是给每一个需要序列化的类都分配一个序列版本号，这个版本号和类相关联。在序列化时，会将这个序列号也一同保存在文件中，在反序列化时会读取这个序列号和本类的序列号进行匹配，如果不匹配会抛出`java.io.InvalidClassException`.

> 注意：
>
> 静态数据不会被序列化，因为静态数据在方法区，不在对象里。
>
> 或者使用transient关键字修饰，也不会序列化。

## 9. 补充

### SequenceInputStream 

表示其他输入流的逻辑串联。它从输入流的有序集合开始，并从第一个输入流开始读取，直到到达文件末尾，接着从第二个输入流读取，依次类推，直到到达包含的最后一个输入流的文件末尾为止。

案例：媒体文件切割与合并。

图片切割：

```java
package IODemo;

import java.io.File;
import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.IOException;
import java.util.Properties;

/**
 * 将一个媒体文件切割成碎片
 * 思路：
 * 1、读取源文件，将源文件的数据分别复制到多个文件
 * 2、切割方式有两种：按照碎片个数切，或者按照指定大小切
 * 3、一个输入流对应多个输出流
 * 4、每个碎片都需要编号，顺序不能错
 * @throws IOException
 */
public class CutFile {

    public static void main(String[] args) throws IOException {
        File srcFile=new File("D:\\Test\\img.jpg");
        File partsDir=new File("D:\\Test\\cutFiles");
        splitFile(srcFile,partsDir);
    }
    //切割文件
    private static void splitFile(File srcFile, File partsDir) throws IOException {
        if(!(srcFile.exists()&&srcFile.isFile())) {
            throw new RuntimeException("源文件不是正确文件或者不存在");
        }
        if(!partsDir.exists()) {
            partsDir.mkdirs();
        }
        FileInputStream fis=new FileInputStream(srcFile);
        FileOutputStream fos=null;
        byte[] buf=new byte[1024*60];
        int len=0;
        int count=1;
        while((len=fis.read(buf))!=-1) {
            //存储碎片文件
            fos=new FileOutputStream(new File(partsDir,(count++)+".part"));
            fos.write(buf, 0, len);
            fos.close();
        }
        /*将源文件和切割的信息也保存起来，随着碎片文件一起发送
        * 信息：
        * 源文件的名称
        * 碎片的个数
        * 将这些信息单独封装到一个文件中
        * 还要一个输出流完成此操作 */
        String fileName=srcFile.getName();
        int partCount=count;
        fos=new FileOutputStream(new File(partsDir,count+".properties"));
        //        fos.write(("fileName="+fileName+System.lineSeparator()).getBytes());
        //        fos.write(("fileCount="+Integer.toString(partCount)).getBytes());
        Properties prop=new Properties();
        prop.setProperty("fileName", srcFile.getName());
        prop.setProperty("partCount", Integer.toString(partCount));
        //将属性集中的信息持久化
        prop.store(fos, "part file info");
        fis.close();
        fos.close();
    }
}
```

图片组合：

```java
package IODemo;

import com.sun.org.apache.xpath.internal.objects.XNull;

import java.io.*;
import java.util.*;

/**
 * 合并文件
 */
public class MergeFile {
    public static void main(String[] args) throws IOException {
        File pathDir = new File("D:\\Test\\cutFiles");
        //获取配置文件
        File configFile = getConfigFile(pathDir);
        //获取配置文件信息的属性集
        Properties prop = getProperties(configFile);
        System.out.println(prop);
        //获取属性集信息，减肥属性集信息传递到合并方法中
        merge(pathDir,prop);
    }


    private static File getConfigFile(File pathDir) {
        //判断是否存在properties文件
        if(!(pathDir.exists())&&pathDir.isDirectory()){
            throw new RuntimeException(pathDir.toString()+"不是有效目录");
        }
        File[] files = pathDir.listFiles(new FileFilter() {
            @Override
            public boolean accept(File pathname) {
                return pathname.getName().endsWith(".properties");
            }
        });
        if(files.length != 1){
            throw new RuntimeException(pathDir.toString()+"properties 扩展名的文件不存在或者不唯一");
        }
        File configFile = files[0];
        return configFile;
    }

    private static Properties getProperties(File configFile) throws IOException {
        FileInputStream fis = null;
        Properties prop = null;
        try {
            //读取流和配置文件相关联
            fis = new FileInputStream(configFile);
            prop = new Properties();
            //流中的数据加载到集合中
            prop.load(fis);
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        }finally {
            if(fis != null){
                fis.close();
            }
        }
        return prop;
    }

    private static void merge(File pathDir, Properties prop) throws IOException {
        String fileName = prop.getProperty("fileName");
        int partCount = Integer.valueOf(prop.getProperty("partCount"));
        List<FileInputStream> list = new ArrayList<FileInputStream>();
        for(int i = 1; i < partCount; i++){
            list.add(new FileInputStream(pathDir.toString()+"\\"+i+".part"));
        }
        //List自身无法获取Enumeration工具类，到Collection中找
        Enumeration<FileInputStream> en = Collections.enumeration(list);
        SequenceInputStream sis=new SequenceInputStream(en);
        FileOutputStream fos=new FileOutputStream(pathDir.toString()+"\\"+fileName);
        byte[] buf=new byte[1024];
        int len=0;
        while((len=sis.read(buf))!=-1) {
            fos.write(buf,0,len);
        }
        fos.close();
        sis.close();

    }
}
```

### 用于操作数组和字符串的流

ByteArrayInputStream 

ByteArrayOutputStream

CharArrayReader 　

CharArrayWriter

StringReader　　　　

StringWriter

关闭这些流都是无效的，因为这些都未调用系统资源，不需要抛IO异常。

例：

```java
package IODemo;

import java.io.ByteArrayInputStream;
import java.io.ByteArrayOutputStream;

/**
 * 源和目的地都是内存的读写过程
 * 用流的思想去操作数组中的数据
 */
public class ByteArrayStreamDemo {
    public static void main(String[] args) {
        //源：内存
        ByteArrayInputStream bais = new ByteArrayInputStream("nihaohello".getBytes());
        //目的：内存
        ByteArrayOutputStream baos = new ByteArrayOutputStream();//内部有一个可自动增长的数组
        //因为源和目的都是内存，没有调用底层资源，所以不需要关闭，即使调用了close也没有任何效果，关闭后仍然可以使用，不会抛出异常
        int ch = 0;
        while((ch = bais.read())!=-1){
            baos.write(ch);
        }
        System.out.println(baos.toString());
    }
}
```

### RandomAccessFile

RandomAccessFile是java Io体系中功能最丰富的文件内容访问类。即可以读取文件内容，也可以向文件中写入内容。但是和其他输入/输入流不同的是，程序可以直接跳到文件的任意位置来读写数据。 

因为RandomAccessFile可以自由访问文件的任意位置，所以如果我们希望只访问文件的部分内容，那就可以使用RandomAccessFile类。 与OutputStearm,Writer等输出流不同的是，RandomAccessFile类允许自由定位文件记录指针，所以RandomAccessFile可以不从文件开始的地方进行输出，所以RandomAccessFile可以向已存在的文件后追加内容。

 RandomAccessFile类包含了一个记录指针，用以标识当前读写处的位置，当程序新创建一个RandomAccessFile对象时，该对象的文件记录指针位于文件头（也就是0处）,当读/写了n个字节后，文件记录指针将会向后移动n个字节。除此之外，RandomAccessFile可以自由的移动记录指针，即可以向前移动，也可以向后移动。RandomAccessFile包含了以下两个方法来操作文件的记录指针.

- long getFilePointer(); 返回文件记录指针的当前位置
- void seek(long pos); 将文件记录指针定位到pos位置

RandomAccessFile即可以读文件，也可以写，所以它即包含了完全类似于InputStream的3个read()方法，其用法和InputStream的3个read()方法完全一样；也包含了完全类似于OutputStream的3个write()方法，其用法和OutputStream的3个Writer()方法完全一样。除此之外，RandomAccessFile还包含了一系类的readXXX()和writeXXX()方法来完成输入和输出。

RandomAccessFile有两个构造器，其实这两个构造器基本相同，只是指定文件的形式不同而已，一个使用String参数来指定文件名，一个使用File参数来指定文件本身。除此之外，创建RandomAccessFile对象还需要指定一个mode参数。该参数指定RandomAccessFile的访问模式，有以下4个值：

- “r” 以只读方式来打开指定文件夹。如果试图对该RandomAccessFile执行写入方法，都将抛出IOException异常。
- “rw” 以读，写方式打开指定文件。如果该文件尚不存在，则试图创建该文件。
- “rws” 以读，写方式打开指定文件。相对于”rw” 模式，还要求对文件内容或元数据的每个更新都同步写入到底层设备。
- “rwd” 以读，写方式打开指定文件。相对于”rw” 模式，还要求对文件内容每个更新都同步写入到底层设备。

**例1：使用RandomAccessFile实现从指定位置读取文件的功能**

```java
package IODemo;

import java.io.File;
import java.io.IOException;
import java.io.RandomAccessFile;

public class RandomAccessFileDemo1 {
    public  static void main(String[] args)throws IOException {
        String filePath="D:/Test/a.txt";
        RandomAccessFile raf=null;
        File file=null;
        try {
            file=new File(filePath);
            raf=new RandomAccessFile(file,"r");
            // 获取 RandomAccessFile对象文件指针的位置，初始位置为0
            System.out.println("当前指针位置："+raf.getFilePointer());
            //移动文件记录指针的位置
            raf.seek(10);
            System.out.println("当前指针位置："+raf.getFilePointer());
            byte[] b=new byte[1024];
            int hasRead=0;
            //循环读取文件
            while((hasRead=raf.read(b))>0){
                //输出文件读取的内容
                System.out.print(new String(b,0,hasRead));
            }
        }catch (IOException e){
            e.printStackTrace();
        }finally {
            raf.close();
        }
    }
}
```

在上面的程序的关键代码两处，一处是创建了RandomAccessFile对象，该对象以只读模式打开了a.txt文件，这意味着RandomAccessFile文件只能读取文件内容，不能执行写入。第二处调用了seek（10）方法，是指把文件的记录指针定位到10字节的位置。也就是说程序将从10字节开始读取数据。其他部分的代码的读取方式和其他的输入流没有区别。

**例2：使用RandomAccessFile实现向文件中追加内容的功能**

```java
package IODemo;

import java.io.File;
import java.io.IOException;
import java.io.RandomAccessFile;

public class RandomAccessFileDemo2 {
    public  static void main(String[] args)throws IOException {
        String filePath="D:/Test/a.txt";
        RandomAccessFile raf=null;
        File file=null;
        try {
            file=new File(filePath);
            // 以读写的方式打开一个RandomAccessFile对象
            raf=new RandomAccessFile(file,"rw");
            //将记录指针移动到该文件的最后
            raf.seek(raf.length());
            //向文件末尾追加内容
            raf.writeChars("acbdefg");
            raf.writeUTF("这是追加内容。。");
        }catch (IOException e){
            e.printStackTrace();
        }finally {
            raf.close();
        }
    }
}
```

**例3：使用RandomAccessFile实现向文件指定位置插入内容的功能**

> 注：RandomAccessFile不能向文件的指定位置插入内容，如果直接将文件记录指针移动到中间某位置后开始输出，则新输出的内容会覆盖文件原有的内容，如果需要向指定位置插入内容，程序需要先把插入点后面的内容写入缓存区，等把需要插入的数据写入到文件后，再将缓存区的内容追加到文件后面。

```java
package IODemo;

import java.io.*;

public class RandomAccessFileDemo3 {

    public  static void main(String[] args)throws IOException {
        String filePath="D:/Test/a.txt";
        insert(filePath,10,"这是插入指定位置指定内容");
    }

    /**
     * 插入文件指定位置的指定内容
     * @param filePath 文件路径
     * @param pos  插入文件的指定位置
     * @param insertContent 插入文件中的内容
     * @throws IOException
     */
    public static void insert(String filePath,long pos,String insertContent)throws IOException{
        RandomAccessFile raf=null;
        File tmp=File.createTempFile("tmp",null);
        tmp.deleteOnExit();
        try {
            // 以读写的方式打开一个RandomAccessFile对象
            raf = new RandomAccessFile(new File(filePath), "rw");
            //创建一个临时文件来保存插入点后的数据
            FileOutputStream fileOutputStream = new FileOutputStream(tmp);
            FileInputStream fileInputStream = new FileInputStream(tmp);
            //把文件记录指针定位到pos位置
            raf.seek(pos);
            raf.seek(pos);
            //------下面代码将插入点后的内容读入临时文件中保存-----
            byte[] bbuf = new byte[64];
            //用于保存实际读取的字节数据
            int hasRead = 0;
            //使用循环读取插入点后的数据
            while ((hasRead = raf.read(bbuf)) != -1) {
                //将读取的内容写入临时文件
                fileOutputStream.write(bbuf, 0, hasRead);
            }
            //-----下面代码用于插入内容 -----
            //把文件记录指针重新定位到pos位置
            raf.seek(pos);
            //追加需要插入的内容
            raf.write(insertContent.getBytes());
            //追加临时文件中的内容
            while ((hasRead = fileInputStream.read(bbuf)) != -1) {
                //将读取的内容写入临时文件
                raf.write(bbuf, 0, hasRead);
            }
        }catch (Exception e){
            throw  e;
        }
    }

}
```

上面的程序使用File类的createTempFile方法创建了一个临时文件（该文件将在JVM退出后被删除），用于保存被插入点后面的内容。程序先将文件中插入点后的内容读入临时文件中，然后重新定位到插入点，将需要插入的内容添加到文件后面，最后将临时文件的内容添加到文件后面，通过这个过程就可以向指定文件，指定位置插入内容。每次运行上面的程序，都会看到a.txt文件中多了一行内容。

### File 类

File: 文件和目录路径名的抽象表示形式，File类的实例是不可改变的。

#### 构造方法

```java
File(String pathname) 将指定的路径名转换成一个File对象
File(String parent,String child) 通过给定的父抽象路径名和子路径名字符串创建一个新的File实例。
File(File parent,String child) 根据 parent 路径名字符串和 child 路径名字符串创建一个新 File 实例。
```

#### 常用方法

| 序号 | 方法描述                                                     |
| :--- | :----------------------------------------------------------- |
| 1    | **public String getName()** 返回由此抽象路径名表示的文件或目录的名称。 |
| 2    | **public String getParent()****、**  返回此抽象路径名的父路径名的路径名字符串，如果此路径名没有指定父目录，则返回 `null`。 |
| 3    | **public File getParentFile()** 返回此抽象路径名的父路径名的抽象路径名，如果此路径名没有指定父目录，则返回 `null`。 |
| 4    | **public String getPath()** 将此抽象路径名转换为一个路径名字符串。 |
| 5    | **public boolean isAbsolute()** 测试此抽象路径名是否为绝对路径名。 |
| 6    | **public String getAbsolutePath()** 返回抽象路径名的绝对路径名字符串。 |
| 7    | **public boolean canRead()** 测试应用程序是否可以读取此抽象路径名表示的文件。 |
| 8    | **public boolean canWrite()** 测试应用程序是否可以修改此抽象路径名表示的文件。 |
| 9    | **public boolean exists()** 测试此抽象路径名表示的文件或目录是否存在。 |
| 10   | **public boolean isDirectory()** 测试此抽象路径名表示的文件是否是一个目录。 |
| 11   | **public boolean isFile()** 测试此抽象路径名表示的文件是否是一个标准文件。 |
| 12   | **public long lastModified()** 返回此抽象路径名表示的文件最后一次被修改的时间。 |
| 13   | **public long length()** 返回由此抽象路径名表示的文件的长度。 |
| 14   | **public boolean createNewFile() throws IOException** 当且仅当不存在具有此抽象路径名指定的名称的文件时，原子地创建由此抽象路径名指定的一个新的空文件。 |
| 15   | **public boolean delete()**  删除此抽象路径名表示的文件或目录。 |
| 16   | **public void deleteOnExit()** 在虚拟机终止时，请求删除此抽象路径名表示的文件或目录。 |
| 17   | **public String[] list()** 返回由此抽象路径名所表示的目录中的文件和目录的名称所组成字符串数组。 |
| 18   | **public String[] list(FilenameFilter filter)** 返回由包含在目录中的文件和目录的名称所组成的字符串数组，这一目录是通过满足指定过滤器的抽象路径名来表示的。 |
| 19   | **public File[] listFiles()**  返回一个抽象路径名数组，这些路径名表示此抽象路径名所表示目录中的文件。 |
| 20   | **public File[] listFiles(FileFilter filter)** 返回表示此抽象路径名所表示目录中的文件和目录的抽象路径名数组，这些路径名满足特定过滤器。 |
| 21   | **public boolean mkdir()** 创建此抽象路径名指定的目录。      |
| 22   | **public boolean mkdirs()** 创建此抽象路径名指定的目录，包括创建必需但不存在的父目录。 |
| 23   | **public boolean renameTo(File dest)**  重新命名此抽象路径名表示的文件。 |
| 24   | **public boolean setLastModified(long time)** 设置由此抽象路径名所指定的文件或目录的最后一次修改时间。 |
| 25   | **public boolean setReadOnly()** 标记此抽象路径名指定的文件或目录，以便只可对其进行读操作。 |
| 26   | **public static File createTempFile(String prefix, String suffix, File directory) throws IOException** 在指定目录中创建一个新的空文件，使用给定的前缀和后缀字符串生成其名称。 |
| 27   | **public static File createTempFile(String prefix, String suffix) throws IOException** 在默认临时文件目录中创建一个空文件，使用给定前缀和后缀生成其名称。 |
| 28   | **public int compareTo(File pathname)** 按字母顺序比较两个抽象路径名。 |
| 29   | **public int compareTo(Object o)** 按字母顺序比较抽象路径名与给定对象。 |
| 30   | **public boolean equals(Object obj)** 测试此抽象路径名与给定对象是否相等。 |
| 31   | **public String toString()**  返回此抽象路径名的路径名字符串。 |

例：打印指定文件夹及其所有子目录

```java
package IODemo;

import java.io.File;

public class FileDemo1 {
    public static void main(String[] args) {
        File file = new File("D:/Test");
        priintFileTree(file,0);
    }

    private static void priintFileTree(File file, int level) {
        for (int i = 0; i < level; i++){
            System.out.print("\t");
        }
        System.out.println(file.getAbsolutePath());
        if(file.isDirectory()){
            File[] strs = file.listFiles();
            for (int j = 0; j < strs.length; j++){
                File f = strs[j];
                priintFileTree(f,level+1);
            }
        }
    }
}
```

#### File类过滤

**public String[] list(FilenameFilter filter)** 返回由包含在目录中的文件和目录的名称所组成的字符串数组，这一目录是通过满足指定过滤器的抽象路径名来表示的。

 **public File[] listFiles(FileFilter filter)** 返回表示此抽象路径名所表示目录中的文件和目录的抽象路径名数组，这些路径名满足特定过滤器。

File类的list方法可以获取目录下的各个文件，传入过滤器还能按照特定需求取出需要的文件。下面来看一下过滤器怎么用的。首先看

`String[] list(FilenameFilter)`。

查看FilenameFilter源码，发现其实是一个接口：

```java
public interface FilenameFilter {
    /**
     * Tests if a specified file should be included in a file list.
     *
     * @param   dir    the directory in which the file was found.
     * @param   name   the name of the file.
     * @return  <code>true</code> if and only if the name should be
     * included in the file list; <code>false</code> otherwise.
     */
    boolean accept(File dir, String name);
}
```

那么我们要想使用过滤器，应该先实现接口，假设我们要找某个文件夹下的txt文件：

```java
package IODemo;

import java.io.File;
import java.io.FilenameFilter;

/**
 * 查找某目录下的txt文件
 */
public class FileDemo2 {

    public static void main(String[] args) {
        File file = new File("D:/Test");
        if(file.isDirectory()){
            String[] list = file.list(new FilenameFilterByTxt()); //传入过滤器
            for (String f : list) {
                System.out.println(f);
            }
        }
    }
}

class FilenameFilterByTxt implements FilenameFilter{

    @Override
    public boolean accept(File dir, String name) {
        return name.endsWith(".txt"); //当文件名以.txt结尾时返回true
    }
}
```

我们只是传入了过滤器，那么accept方法是如何被调用的呢？

查看`String[] list(FilenameFilter)`源码：

```java
/*list(FilenameFilter)源码解析*/
public String[] list(FilenameFilter filter) {
        String names[] = list();//调用list()方法获取所有名称
        if ((names == null) || (filter == null)) {
            return names;
        }
        List<String> v = new ArrayList<>();//用于保存过滤后的文件名
        for (int i = 0 ; i < names.length ; i++) {//遍历
            //调用filter的accept方法，传入当前目录this和遍历到的名称names[i]
            if (filter.accept(this, names[i])) {
                v.add(names[i]);//满足过滤器条件的添加到集合中
            }
        }
        return v.toArray(new String[v.size()]);//将集合转成数组返回，限定增删操作
 }
```

也就是说，我们实现的accept方法是在构造器中被调用的。

类似地，FileFilter 也是一个接口，采用匿名内部类的方式实现接口，使用File[] listFiles(FileFilter filter)获取目录下所有文件夹：

```java
package IODemo;

import java.io.File;
import java.io.FileFilter;

public class FileDemo3 {
    public static void main(String[] args) {
        File file = new File("D:\\Test");
        if(file.isDirectory()) {
            File[] list=file.listFiles(new FileFilter() {
                @Override
                public boolean accept(File pathname) {
                    // TODO Auto-generated method stub
                    return pathname.isDirectory();
                }

            });

            for(File f:list) {
                System.out.println(f);
            }
        }
    }
}
```

 `File[] listFiles(FileFilter filter)` 方法的源码如下：

```java
/*File[] listFiles(FileFilter filter)源码解析*/
 public File[] listFiles(FileFilter filter) {
        String ss[] = list();//调用list()获取所有的名称数组
        if (ss == null) return null;//健壮性判断，数组为null则返回
        ArrayList<File> files = new ArrayList<>();//创建File类型集合
        for (String s : ss) {//遍历
            File f = new File(s, this);//private File(String child, File parent)私有构造调用
            if ((filter == null) || filter.accept(f))//条件判断
                files.add(f);//添加到集合
        }
        return files.toArray(new File[files.size()]);//集合转成数组返回
}
```

## 10. IO流总结

1.  明确要操作的数据是数据源还是数据目的(要读还是要写)

    源：InputStream　　Reader

   目的：OutputStream　　Writer

2.  明确要操作的设备上的数据是字节还是文本

　　源：

　　　　字节：InputStream

　　　　文本：Reader

　　目的：

　　　　字节：OutputStream

　　　　文本：Writer

3. 明确数据所在的具体设备

　　源设备：

　　　　硬盘：文件 File开头

　　　　内存：数组，字符串

　　　　键盘：System.in

　　　　网络：Socket

　　目的设备：

　　　　硬盘：文件 File开头

　　　　内存：数组，字符串

　　　　屏幕：System.out

　　　　网络：Socket

4. 明确是否需要额外功能？

　　　　需要转换——转换流 InputStreamReader OutputStreamWriter

　　　　需要高效——缓冲流Bufferedxxx

　　　　多个源——序列流 SequenceInputStream

　　　　对象序列化——ObjectInputStream,ObjectOutputStream

　　　　保证数据的输出形式——打印流PrintStream Printwriter

　　　　操作基本数据，保证字节原样性——DataOutputStream,DataInputStream

## 📚 References

-  菜鸟教程

-  https://www.cnblogs.com/hopeyes/p/9736642.html

- https://www.cnblogs.com/oubo/archive/2012/01/06/2394638.html

  
