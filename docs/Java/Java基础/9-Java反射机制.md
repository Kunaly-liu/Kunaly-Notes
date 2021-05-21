# Java 反射机制

## 1.  概述

### 什么是反射？

反射 (Reflection) 是 Java 的特征之一，它允许运行中的 Java 程序获取自身的信息，并且可以操作类或对象的内部属性。

Oracle 官方对反射的解释是：

> Reflection enables Java code to discover information about the fields, methods and constructors of loaded classes, and to use reflected fields, methods, and constructors to operate on their underlying counterparts, within security restrictions.
> The API accommodates applications that need access to either the public members of a target object (based on its runtime class) or the members declared by a given class. It also allows programs to suppress default reflective access control.

简而言之，通过反射，我们可以在运行时获得程序或程序集中每一个类型的成员和成员的信息。程序中一般的对象的类型都是在编译期就确定下来的，而 Java 反射机制可以动态地创建对象并调用其属性，这样的对象的类型在编译期是未知的。所以我们可以通过反射机制直接创建对象，即使这个对象的类型在编译期是未知的。

反射的核心是 JVM 在运行时才动态加载类或调用方法/访问属性，它不需要事先（写代码的时候或编译期）知道运行对象是谁。

Java 反射主要提供以下功能：

- 在运行时判断任意一个对象所属的类；
- 在运行时构造任意一个类的对象；
- 在运行时判断任意一个类所具有的成员变量和方法（通过反射甚至可以调用private方法）；
- 在运行时调用任意一个对象的方法

重点：**是运行时而不是编译时**

### 反射的应用场景：

1. 开发通用框架：反射最重要的用途就是开发各种通用框架。很多框架都素hi配置化的，为了保证框架的通用性，它们可以需要根据配置文件加载不同的对象或类，调用不同的方法，这个时候就必须用到反射--运行时动态加载需要加载的对象。
2. 动态代理：在切面编程中，需要拦截特定的方法，通常，会选择动态代理方式，这时，就需要反射技术来实现了。
3. 注解：注解本身仅仅是起到标记作用，它需要利用反射机制，根据注解标记去调用注解解释器，执行行为。
4. 可扩展性功能：应用程序可以通过使用完全限定名称创建可扩展性对象实例来使用外部的用户定义类。

### 反射的缺点：

1. 性能开销：由于反射涉及及动态解析的类型，因此无法执行某些Java虚拟机优化。因此，反射操作的性能要比非反射操作的性能差，应该在性能敏感的应用程序中频繁调用的代码段中避免。
2. 破坏封装性：反射调用方法时可以忽略权限检查，因此可能会破坏封装性而导致安全问题。
3. 内部曝光：由于反射允许代码执行在非反射代码中非法的操作，例如访问私有字段和方法，所以反射的使用可能会导致意想不到的副作用，这可能会导致代码功能失常并可能破坏可移植性。反射代码打破了抽象，因此可能会随着平台的升级而改变行为。

### 类加载的完整过程：

虚拟机把描述类的数据从 Class 文件加载到内存，并对数据进行校验、转换解析和初始化，最终形成可以被虚拟机直接使用的 Java 类型，这就是虚拟机的类加载机制。

在Java语言里面，类型的加载、连接和初始化过程都是在程序运行期间完成的

**类的加载过程：**

类的整个生命周期如下：

![img](https://gitee.com/Kunaly/picture-bed/raw/master/img/14923529-ac753500687cf9d2.png)

##### 加载

1. 通过全限定类名来获取定义此类的二进制字节流。
2. 将这个字节流所代表的静态存储结构转化为方法区的运行时数据结构。
3. 在内存中生成一个代表这个类的 java.lang.Class 对象，作为方法区这个类的各种数据的访问入口。

##### 验证

验证是连接阶段的第一步，这一阶段的目的是为了确保 Class 文件的字节流中包含的信息符合当前虚拟机的要求，并且不会危害虚拟机自身的安全。

1. 文件格式验证：如是否以魔数 0xCAFEBABE 开头、主、次版本号是否在当前虚拟机处理范围之内、常量合理性验证等。
   此阶段保证输入的字节流能正确地解析并存储于方法区之内，格式上符合描述一个 Java类型信息的要求。
2. 元数据验证：是否存在父类，父类的继承链是否正确，抽象类是否实现了其父类或接口之中要求实现的所有方法，字段、方法是否与父类产生矛盾等。
   第二阶段，保证不存在不符合 Java 语言规范的元数据信息。
3. 字节码验证：通过数据流和控制流分析，确定程序语义是合法的、符合逻辑的。例如保证跳转指令不会跳转到方法体以外的字节码指令上。
4. 符号引用验证：在解析阶段中发生，保证可以将符号引用转化为直接引用。

可以考虑使用 `-Xverify:none` 参数来关闭大部分的类验证措施，以缩短虚拟机类加载的时间。

##### 准备

为**类变量**分配内存并设置类变量初始值，这些变量所使用的内存都将在方法区中进行分配。

##### 解析

虚拟机将常量池内的`符号引用`替换为`直接引用`的过程。
解析动作主要针对类或接口、字段、类方法、接口方法、方法类型、方法句柄和调用点限定符 7 类符号引用进行。

##### 初始化

到初始化阶段，才真正开始执行类中定义的 Java 程序代码，此阶段是执行 `<clinit>()` 方法的过程。

`<clinit>()` 方法是由编译器按语句在源文件中出现的顺序，依次自动收集类中的所有**类变量**的赋值动作和静态代码块中的语句合并产生的。（不包括构造器中的语句。构造器是初始化对象的，类加载完成后，创建对象时候将调用的 `<init>()` 方法来初始化对象）

静态语句块中只能访问到定义在静态语句块之前的变量，定义在它之后的变量，在前面的静态语句块可以赋值，但是不能访问，如下程序：

```java
Copypublic class Test {
    static {
        // 给变量赋值可以正常编译通过
        i = 0;
        // 这句编译器会提示"非法向前引用"
        System.out.println(i);
    }

    static int i = 1;
}
```

`<clinit>()` 不需要显式调用父类（接口除外，接口不需要调用父接口的初始化方法，只有使用到父接口中的静态变量时才需要调用）的初始化方法 `<clinit>()`，虚拟机会保证在子类的 `<clinit>()` 方法执行之前，父类的 `<clinit>()` 方法已经执行完毕，也就意味着父类中定义的静态语句块要优先于子类的变量赋值操作。

`<clinit>()` 方法对于类或接口来说并不是必需的，如果一个类中没有静态语句块，也没有对变量的赋值操作，那么编译器可以不为这个类生成 `<clinit>()` 方法。

虚拟机会保证一个类的 `<clinit>()` 方法在多线程环境中被正确地加锁、同步，如果多个线程同时去初始化一个类，那么只会有一个线程去执行这个类的 `<clinit>()` 方法，其他线程都需要阻塞等待，直到活动线程执行 `<clinit>()` 方法完毕。

### 类加载器

把实现类加载阶段中的“通过一个类的全限定名来获取描述此类的二进制字节流”这个动作的代码模块称为“类加载器”。

将 class 文件二进制数据放入方法区内，然后在堆内（heap）创建一个 java.lang.Class 对象，Class 对象封装了类在方法区内的数据结构，并且向开发者提供了访问方法区内的数据结构的接口。

目前类加载器却在类层次划分、OSGi、热部署、代码加密等领域非常重要，我们运行任何一个 Java 程序都会涉及到类加载器。

##### 类的唯一性和类加载器

对于任意一个类，都需要由加载它的类加载器和这个类本身一同确立其在Java虚拟机中的唯一性。

即使两个类来源于同一个 Class 文件，被同一个虚拟机加载，只要加载它们的类加载器不同，那这两个类也不相等。
这里所指的“相等”，包括代表类的 Class 对象的 equals() 方法、 isAssignableFrom() 方法、isInstance() 方法的返回结果，也包括使用 instanceof 关键字做对象所属关系判定等情况。



### java.lang.reflect 包

java.lang.reflect 包的核心接口和类如下：

Member 接口 - 反映关于单个成员(字段或方法)或构造函数的标识信息。

Field 类 - 提供一个类的域的信息以及访问类的域的接口。

Method 类 - 提供一个类的方法的信息以及访问类的方法的接口。

Constructor 类 - 提供一个类的构造函数的信息以及访问类的构造函数的接口。

Array 类 - 该类提供动态地生成和访问 JAVA 数组的方法。

Modifier 类 - 提供了 static 方法和常量，对类和成员访问修饰符进行解码。

Proxy 类 - 提供动态地生成代理类和类实例的静态方法。


## 2. 反射的基本应用

上面我们提到了反射可以用于判断任意对象所属的类，获得 Class 对象，构造任意一个对象以及调用一个对象。这里我们介绍一下基本反射功能的使用和实现(反射相关的类一般都在 java.lang.relfect 包里)。

### 2.1 Class 类

Class就是普通的一个类，和我们平时写的类没有什么区别，它位于java.lang包下，和java.lang.reflect包下的类共同支持了java的整个反射功能。

常用方法：

| Modifier and Type           | Method and Description                                       |
| --------------------------- | ------------------------------------------------------------ |
| `<U> 类<? extends U>`       | `asSubclass(类<U> clazz)`  `类`这个 `类`对象来表示由指定的类对象表示的类的子类。 |
| `T`                         | `cast(Object obj)`  施放一个目的是通过本表示的类或接口 `类`对象。 |
| `boolean`                   | `desiredAssertionStatus()`  如果要在调用此方法时初始化该类，则返回将分配给此类的断言状态。 |
| `static 类<?>`              | `forName(String className)`  返回与给定字符串名称的类或接口相关联的 `类`对象。 |
| `static 类<?>`              | `forName(String name,  boolean initialize, ClassLoader loader)`  使用给定的类加载器返回与给定字符串名称的类或接口相关联的 `类`对象。 |
| `AnnotatedType[]`           | `getAnnotatedInterfaces()`  返回一个 `AnnotatedType`对象的数组，  `AnnotatedType`使用类型指定由此 `AnnotatedType`对象表示的实体的超级  `类` 。 |
| `AnnotatedType`             | `getAnnotatedSuperclass()`  返回一个 `AnnotatedType`对象，该对象表示使用类型来指定由此  `类`对象表示的实体的 `类`类。 |
| `<A extends Annotation>A`   | `getAnnotation(类<A> annotationClass)`  返回该元素的，如果这样的注释 *，*否则返回null指定类型的注释。 |
| `Annotation[]`              | `getAnnotations()`  返回此元素上 *存在的*注释。              |
| `<A extends Annotation>A[]` | `getAnnotationsByType(类<A> annotationClass)`  返回与此元素相关 *联的注释* 。 |
| `String`                    | `getCanonicalName()`  返回由Java语言规范定义的基础类的规范名称。 |
| `类<?>[]`                   | `getClasses()`  返回包含一个数组 `类`表示所有的公共类和由此表示的类的成员接口的对象  `类`对象。 |
| `ClassLoader`               | `getClassLoader()`  返回类的类加载器。                       |
| `类<?>`                     | `getComponentType()`  返回 `类`数组的组件类型的Class。       |
| `Constructor<T>`            | `getConstructor(类<?>... parameterTypes)`  返回一个 `Constructor`对象，该对象反映  `Constructor`对象表示的类的指定的公共 `类`函数。 |
| `Constructor<?>[]`          | `getConstructors()`  返回包含一个数组 `Constructor`对象反射由此表示的类的所有公共构造  `类`对象。 |
| `<A extends Annotation>A`   | `getDeclaredAnnotation(类<A> annotationClass)`  如果这样的注释 *直接存在* ，则返回指定类型的元素注释，否则返回null。 |
| `Annotation[]`              | `getDeclaredAnnotations()`  返回 *直接存在*于此元素上的注释。 |
| `<A extends Annotation>A[]` | `getDeclaredAnnotationsByType(类<A> annotationClass)`  如果此类注释 *直接存在*或 *间接存在，*则返回该元素的注释（指定类型）。 |
| `类<?>[]`                   | `getDeclaredClasses()`  返回一个反映所有被这个 `类`对象表示的类的成员声明的类和 `类`对象的数组。 |
| `Constructor<T>`            | `getDeclaredConstructor(类<?>... parameterTypes)`  返回一个 `Constructor`对象，该对象反映  `Constructor`对象表示的类或接口的指定 `类`函数。 |
| `Constructor<?>[]`          | `getDeclaredConstructors()`  返回一个反映 `Constructor`对象表示的类声明的所有  `Constructor`对象的数组 `类` 。 |
| `Field`                     | `getDeclaredField(String name)`  返回一个 `Field`对象，它反映此表示的类或接口的指定已声明字段 `类`对象。 |
| `Field[]`                   | `getDeclaredFields()`  返回的数组 `Field`对象反映此表示的类或接口声明的所有字段 `类`对象。 |
| `方法`                      | `getDeclaredMethod(String name,  类<?>... parameterTypes)`  返回一个 `方法`对象，它反映此表示的类或接口的指定声明的方法 `类`对象。 |
| `方法[]`                    | `getDeclaredMethods()`  返回包含一个数组 `方法`对象反射的类或接口的所有声明的方法，通过此表示  `类`对象，包括公共，保护，默认（包）访问和私有方法，但不包括继承的方法。 |
| `类<?>`                     | `getDeclaringClass()`  如果由此 `类`对象表示的类或接口是另一个类的成员，则返回表示其声明的类的  `类`对象。 |
| `类<?>`                     | `getEnclosingClass()`  返回底层类的即时封闭类。              |
| `Constructor<?>`            | `getEnclosingConstructor()`  如果此`类`对象表示构造函数中的本地或匿名类，则返回表示底层类的立即封闭构造函数的[`Constructor`](../../java/lang/reflect/Constructor.html)对象。 |
| `方法`                      | `getEnclosingMethod()`  如果此`类`对象表示方法中的本地或匿名类，则返回表示[基础](../../java/lang/reflect/Method.html)类的即时封闭方法的`方法`对象。 |
| `T[]`                       | `getEnumConstants()`  返回此枚举类的元素，如果此Class对象不表示枚举类型，则返回null。 |
| `Field`                     | `getField(String name)`  返回一个 `Field`对象，它反映此表示的类或接口的指定公共成员字段  `类`对象。 |
| `Field[]`                   | `getFields()`  返回包含一个数组 `Field`对象反射由此表示的类或接口的所有可访问的公共字段  `类`对象。 |
| `Type[]`                    | `getGenericInterfaces()`  返回 `Type`表示通过由该对象所表示的类或接口直接实现的接口秒。 |
| `Type`                      | `getGenericSuperclass()`  返回 `Type`表示此所表示的实体（类，接口，基本类型或void）的直接超类  `类` 。 |
| `类<?>[]`                   | `getInterfaces()`  确定由该对象表示的类或接口实现的接口。    |
| `方法`                      | `getMethod(String name,  类<?>... parameterTypes)`  返回一个 `方法`对象，它反映此表示的类或接口的指定公共成员方法 `类`对象。 |
| `方法[]`                    | `getMethods()`  返回包含一个数组 `方法`对象反射由此表示的类或接口的所有公共方法  `类`对象，包括那些由类或接口和那些从超类和超接口继承的声明。 |
| `int`                       | `getModifiers()`  返回此类或接口的Java语言修饰符，以整数编码。 |
| `String`                    | `getName()`  返回由 `类`对象表示的实体（类，接口，数组类，原始类型或空白）的名称，作为  `String` 。 |
| `软件包`                    | `getPackage()`  获取此类的包。                               |
| `ProtectionDomain`          | `getProtectionDomain()`  返回 `ProtectionDomain` 。          |
| `URL`                       | `getResource(String name)`  查找具有给定名称的资源。         |
| `InputStream`               | `getResourceAsStream(String name)`  查找具有给定名称的资源。 |
| `Object[]`                  | `getSigners()`  获得这个类的签名者。                         |
| `String`                    | `getSimpleName()`  返回源代码中给出的基础类的简单名称。      |
| `类<? super T>`             | `getSuperclass()`  返回 `类`表示此所表示的实体（类，接口，基本类型或void）的超类 `类` 。 |
| `String`                    | `getTypeName()`  为此类型的名称返回一个内容丰富的字符串。    |
| `TypeVariable<类<T>>[]`     | `getTypeParameters()`  返回一个 `TypeVariable`对象的数组，它们以声明顺序表示由此  `GenericDeclaration`对象表示的通用声明声明的类型变量。 |
| `boolean`                   | `isAnnotation()`  如果此 `类`对象表示注释类型，则返回true。  |
| `boolean`                   | `isAnnotationPresent(类<? extends  Annotation> annotationClass)`  如果此元素上 *存在*指定类型的注释，则返回true，否则返回false。 |
| `boolean`                   | `isAnonymousClass()`  返回 `true`当且仅当基础类是匿名类时。  |
| `boolean`                   | `isArray()`  确定此 `类`对象是否表示数组类。                 |
| `boolean`                   | `isAssignableFrom(类<?> cls)`  确定由此 `类`对象表示的类或接口是否与由指定的Class  `类`表示的类或接口相同或是超类或 `类`接口。 |
| `boolean`                   | `isEnum()`  当且仅当该类在源代码中被声明为枚举时才返回true。 |
| `boolean`                   | `isInstance(Object obj)`  确定指定的Object是否与此 `Object`表示的对象分配 `类` 。 |
| `boolean`                   | `isInterface()`  确定指定 `类`对象表示接口类型。             |
| `boolean`                   | `isLocalClass()`  返回 `true`当且仅当基础类是本地类时。      |
| `boolean`                   | `isMemberClass()`  返回 `true`当且仅当基础类是成员类时。     |
| `boolean`                   | `isPrimitive()`  确定指定 `类`对象表示一个基本类型。         |
| `boolean`                   | `isSynthetic()`  如果这个类是一个合成类，返回`true` ;  返回`false`其他。 |
| `T`                         | `newInstance()`  创建由此 `类`对象表示的类的新实例。         |
| `String`                    | `toGenericString()`  返回描述此 `类`的字符串，包括有关修饰符和类型参数的信息。 |
| `String`                    | `toString()`  将对象转换为字符串。                           |

#### 2.1.1 获取Class类

1. 使用 Class 类的 forName 静态方法

   ```java
   Class aClass1 = Class.forName("java.lang.String");
   ```

2. 任何数据类型（包括基本的数据类型）都有一个“静态”的class属性

   ```java
   Class aClass2 = String.class;
   ```

3. 使用对象的getClass()方法

   ```java
   Class aClass3 = "hello".getClass();
   ```

4. 通过类加载器ClassLoader的loadClass方法

   ```java
   ClassLoader cl = this.getClass().getClassLoader();
   Class aClass4 = cl.loadClass("类的全类名");
   ```

   例子：

   ```java
   package reflectDemo;
   
   public class ClassDemo1 {
   
       public static void main(String[] args) throws ClassNotFoundException {
           Class aClass1 = Class.forName("java.lang.String");
           System.out.println(aClass1);
   
           Class aClass2 = String.class;
           System.out.println(aClass2);
   
           String s = "hello";
           Class aClass3 = s.getClass();
           System.out.println(aClass3);
   
           ClassLoader cl = ClassDemo1.class.getClassLoader();
           Class aClass4 = cl.loadClass("java.lang.String");
           System.out.println(aClass4);
       }
   }
   ```

   

#### 2.1.2 判断类的实例

一般地，我们用 `instanceof` 关键字来判断是否为某个类的实例。同时我们也可以借助反射中 Class 对象的 `isInstance()` 方法来判断是否为某个类的实例，它是一个 native 方法：

```java
public native boolean isInstance(Object obj);
```

例：

```java
package reflectDemo;

import java.util.ArrayList;
import java.util.List;

public class InstanceofDemo {
    public static void main(String[] args) {
        ArrayList arrayList = new ArrayList();
        if(arrayList instanceof List){
            System.out.println("1.ArrayList is List");
        }

        if(List.class.isInstance(arrayList)){
            System.out.println("2.ArrayList is List");
        }
    }
}
```

输出结果：

1.ArrayList is List
2.ArrayList is List



#### 2.1.3 创建实例

通过反射来生成对象主要有两种方式。

- 使用Class对象的newInstance()方法来创建Class对象对应类的实例。

```java
Class<?> c = String.class;
Object str = c.newInstance();
```

- 先通过Class对象获取指定的Constructor对象，再调用Constructor对象的newInstance()方法来创建实例。这种方法可以用指定的构造器构造类的实例。

```java
//获取String所对应的Class对象
Class<?> c = String.class;
//获取String类带一个String参数的构造器
Constructor constructor = c.getConstructor(String.class);
//根据构造器创建实例
Object obj = constructor.newInstance("bbb");
System.out.println(obj);
```

例：

```java
package reflectDemo;

import java.lang.reflect.Constructor;
import java.lang.reflect.InvocationTargetException;

public class NewInstanceDemo {
    public static void main(String[] args) throws IllegalAccessException, InstantiationException, NoSuchMethodException, InvocationTargetException {
        //方式1:
        Class c1 = StringBuilder.class;
        StringBuilder sb = (StringBuilder) c1.newInstance();
        sb.append("aaa");
        System.out.println(sb.toString());

        //方式2:
        //获取String所对应的Class对象
        Class c2 = String.class;
        //获取String类带一个String参数的构造器
        Constructor constructor = c2.getConstructor(String.class);
        //根据构造器创建实例
        String str = (String) constructor.newInstance("bbb");
        System.out.println(str);

    }
}
```

输出结果：

aaa
bbb

#### 2.1.4 获取方法

获取某个Class对象的方法集合，主要有以下几个方法：

- `getDeclaredMethods` 方法返回类或接口声明的所有方法，包括公共、保护、默认（包）访问和私有方法，但不包括继承的方法。

```java
public Method[] getDeclaredMethods() throws SecurityException
```

- `getMethods` 方法返回某个类的所有公用（public）方法，包括其继承类的公用方法。

```java
public Method[] getMethods() throws SecurityException
```

- `getMethod` 方法返回一个特定的方法，其中第一个参数为方法名称，后面的参数为方法的参数对应Class的对象。

```java
public Method getMethod(String name, Class<?>... parameterTypes)
```

只是这样描述的话可能难以理解，我们用例子来理解这三个方法：

```java
package reflectDemo;

import java.lang.reflect.InvocationTargetException;
import java.lang.reflect.Method;

public class test1 {
    public static void main(String[] args) throws InvocationTargetException, NoSuchMethodException, InstantiationException, IllegalAccessException {
        test();
    }
    public static void test() throws IllegalAccessException, InstantiationException, NoSuchMethodException, InvocationTargetException {
        Class<?> c = methodClass.class;
        Object object = c.newInstance();
        Method[] methods = c.getMethods();
        Method[] declaredMethods = c.getDeclaredMethods();
        //获取methodClass类的add方法
        Method method = c.getMethod("add", int.class, int.class);
        //getMethods()方法获取的所有方法
        System.out.println("getMethods获取的方法：");
        for(Method m:methods)
            System.out.println(m);
        //getDeclaredMethods()方法获取的所有方法
        System.out.println("getDeclaredMethods获取的方法：");
        for(Method m:declaredMethods)
            System.out.println(m);
    }
}
class methodClass {

    public final int fuck = 3;
    public int add(int a,int b) {
        return a+b;
    }
    public int sub(int a,int b) {
        return a+b;
    }
}
```

程序运行的结果如下:

```
getMethods获取的方法：
public int org.ScZyhSoft.common.methodClass.add(int,int)
public int org.ScZyhSoft.common.methodClass.sub(int,int)
public final void java.lang.Object.wait() throws java.lang.InterruptedException
public final void java.lang.Object.wait(long,int) throws java.lang.InterruptedException
public final native void java.lang.Object.wait(long) throws java.lang.InterruptedException
public boolean java.lang.Object.equals(java.lang.Object)
public java.lang.String java.lang.Object.toString()
public native int java.lang.Object.hashCode()
public final native java.lang.Class java.lang.Object.getClass()
public final native void java.lang.Object.notify()
public final native void java.lang.Object.notifyAll()
getDeclaredMethods获取的方法：
public int org.ScZyhSoft.common.methodClass.add(int,int)
public int org.ScZyhSoft.common.methodClass.sub(int,int)
```

可以看到，通过 `getMethods()` 获取的方法可以获取到父类的方法,比如 java.lang.Object 下定义的各个方法。

#### 2.1.5 获取构造器信息

获取类构造器的用法与上述获取方法的用法类似。主要是通过Class类的getConstructor方法得到Constructor类的一个实例，而Constructor类有一个newInstance方法可以创建一个对象实例:

```java
public T newInstance(Object ... initargs)
```

此方法可以根据传入的参数来调用对应的Constructor创建对象实例。例子见2.1.3

#### 2.1.6 获取类的成员变量

主要是这几个方法，在此不再赘述：

- `getFiled`：访问公有的成员变量
- `getDeclaredField`：所有已声明的成员变量，但不能得到其父类的成员变量

`getFileds` 和 `getDeclaredFields` 方法用法同上（参照 Method）。

```java
import java.lang.reflect.Field;

public class test2 {
    public static void main(String[] args){
        test();
    }
    public static void test()  {
        Class<?> c = Student.class;
        //获取的所有属性
        Field[] fields = c.getDeclaredFields();
        System.out.println("getDeclaredFields获取的属性：");
        for(Field f : fields)
            System.out.println(f);

        //getFields获取的所有方法
        Field[] fields1 = c.getFields();
        System.out.println("getFields获取的属性：");
        for(Field f : fields)
            System.out.println(f);
        
       //获取某个属性：
        Field field = c.getDeclaredField("sex");
        System.out.println(field.getType() + " : " + field.getName());
    }
}
class Student{
    private  String name;
    public  int age;
    public  String sex;
}
```

**为私有属性设置值：**

字段是私有的，外面是无法进行调用的；但是可以通过反射的方式绕过去，从而为其进行设置值。

```java
import java.lang.reflect.Field;

public class test2 {
    public static void main(String[] args) throws NoSuchFieldException, InstantiationException, IllegalAccessException {
        test();
    }
    public static void test() throws NoSuchFieldException, IllegalAccessException, InstantiationException {
        Class<?> c = Student.class;
        Student student = (Student) c.newInstance();
        Field field = c.getDeclaredField("name");
        if(!field.isAccessible()){
            field.setAccessible(true);
        }
        field.set(student,"小明");
        System.out.println(student.toString());
    }
}
class Student{
    private  String name;
    public  int age;
    public  String sex;

    @Override
    public String toString() {
        return "Student{" +
                "name='" + name + '\'' +
                ", age=" + age +
                ", sex='" + sex + '\'' +
                '}';
    }
}
```

#### 2.1.7 调用方法

当我们从类中获取了一个方法后，我们就可以用 `invoke()` 方法来调用这个方法。`invoke` 方法的原型为:

```java
public Object invoke(Object obj, Object... args)
        throws IllegalAccessException, IllegalArgumentException,
           InvocationTargetException
```

下面是一个实例：

```java
package reflectDemo;

import java.lang.reflect.InvocationTargetException;
import java.lang.reflect.Method;

public class test3 {

    public static void main(String[] args) throws IllegalAccessException, InstantiationException, NoSuchMethodException, InvocationTargetException {
        Class<?> klass = methodClass2.class;
        //创建methodClass的实例
        Object obj = klass.newInstance();
        //获取methodClass类的add方法
        Method method = klass.getMethod("add",int.class,int.class);
        //调用method对应的方法 => add(1,4)
        Object result = ((Method) method).invoke(obj,1,4);
        System.out.println(result);
    }
}

class methodClass2 {
    public final int fuck = 3;
    public int add(int a,int b) {
        return a+b;
    }
    public int sub(int a,int b) {
        return a+b;
    }
}
```

#### 2.1.8 利用反射创建数组

数组在Java里是比较特殊的一种类型，它可以赋值给一个Object Reference。下面我们看一看利用反射创建数组的例子：

```java
public static void testArray() throws ClassNotFoundException {
        Class<?> cls = Class.forName("java.lang.String");
        Object array = Array.newInstance(cls,25);
        //往数组里添加内容
        Array.set(array,0,"zhangsan");
        Array.set(array,1,"lisi");
        Array.set(array,2,"wangwu");
        Array.set(array,3,"zhaoliu");
        Array.set(array,4,"hello");
        //获取某一项的内容
        System.out.println(Array.get(array,3));
    }
```

其中的Array类为`java.lang.reflect.Array`类。我们通过`Array.newInstance()`创建数组对象，它的原型是:

```java
public static Object newInstance(Class<?> componentType, int length)
        throws NegativeArraySizeException {
        return newArray(componentType, length);
    }
```

而 `newArray` 方法是一个 native 方法，结构如下：

```java
private static native Object newArray(Class<?> componentType, int length)
        throws NegativeArraySizeException;
```

## 3. 总结

由于反射会额外消耗一定的系统资源，因此如果不需要动态地创建一个对象，那么就不需要用反射。

另外，反射调用方法时可以忽略权限检查，因此可能会破坏封装性而导致安全问题。



## 📚 References

- https://blog.csdn.net/weixin_42759988/article/details/98531712?utm_medium=distribute.pc_relevant.none-task-blog-baidujs_title-0&spm=1001.2101.3001.4242
- https://blog.csdn.net/lemonZhaoTao/article/details/89766142
- https://blog.csdn.net/a745233700/article/details/82893076
