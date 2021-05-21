# JAVA集合

## 1.  JAVA集合框架

Java 集合框架主要包括两种类型的容器，一种是集合（Collection），存储一个元素集合，另一种是图（Map），存储键/值对映射。

Collection 接口又有 3 种子类型，List、Set 和 Queue，再下面是一些抽象类，最后是具体实现类，常用的有 ArrayList、LinkedList、HashSet、LinkedHashSet、HashMap、LinkedHashMap 等等。具体如下图所示：

<img src="https://gitee.com/Kunaly/picture-bed/raw/master/img/image-20210415160532287.png" alt="image-20210415160532287" style="zoom:80%;" />

### 1.1 Connection 接口

#### 1.1.1 List 

**有序、可重复**

- ArrayList
  **优点:** 底层数据结构是数组，查询快，增删慢。
  **缺点:** 线程不安全，效率高
- Vector
  **优点:** 底层数据结构是数组，查询快，增删慢。
  **缺点:** 线程安全，效率低
- LinkedList
  **优点:** 底层数据结构是链表，查询慢，增删快。
  **缺点:** 线程不安全，效率高

#### 1.1.2 SET

**无序、唯一**

- HashSet
  底层数据结构是哈希表。(无序,唯一)
  如何来保证元素唯一性?
  1.依赖两个方法：hashCode()和equals()

- LinkedHashSet
  底层数据结构是链表和哈希表。(FIFO插入有序,唯一)
  1.由链表保证元素有序
  2.由哈希表保证元素唯一

- TreeSet
  底层数据结构是红黑树。(唯一，有序)
  1. 如何保证元素排序的呢?
  自然排序
  比较器排序、
  2. 如何保证元素唯一性的呢?
      根据比较的返回值是否是0来决定

### 1.2 Map

Map接口有三个比较重要的实现类，分别是HashMap、TreeMap和HashTable。

- TreeMap是有序的，HashMap和HashTable是无序的。
- Hashtable的方法是同步的，HashMap的方法不是同步的。这是两者最主要的区别。

> **HashTable和HashMap的区别：**
>
> 1. Hashtable是线程安全的，HashMap不是线程安全的。
>
> 2. HashMap效率较高，Hashtable效率较低。
>    
>    如果对同步性或与遗留代码的兼容性没有任何要求，建议使用HashMap。 查看Hashtable的源代码就可以发现，除构造函数外，Hashtable的所有 public 方法声明中都有 synchronized关键字，而HashMap的源码中则没有。
>    
> 3. Hashtable不允许null值，HashMap允许null值（key和value都允许）
>    
> 4. 父类不同：Hashtable的父类是Dictionary，HashMap的父类是AbstractMap
>


## 2. ArrayList

### 2.1 ArrayList 简介

ArrayList 类是一个可以动态修改的数组，与普通数组的区别就是它是没有固定大小的限制，我们可以添加或删除元素。

ArrayList 继承了 AbstractList ，并实现了 List 接口。底层基于数组实现容量大小动态变化。允许 null 的存在。同时还实现了 RandomAccess、Cloneable、Serializable 接口，所以ArrayList 是支持快速访问、复制、序列化的。

<img src="https://gitee.com/Kunaly/picture-bed/raw/master/img/image-20210415161341327.png" alt="image-20210415161341327" style="zoom: 67%;" />

### 2.2 ArrayList 方法

ArrayList API：[https://docs.oracle.com/javase/7/docs/api/java/util/ArrayList.html](https://docs.oracle.com/javase/7/docs/api/java/util/ArrayList.html)

中文版本API : [https://www.runoob.com/manual/jdk11api/java.base/java/util/ArrayList.html](https://www.runoob.com/manual/jdk11api/java.base/java/util/ArrayList.html)

Java ArrayList 常用方法列表如下：

| 方法                                                         | 描述                                          |
| :----------------------------------------------------------- | :-------------------------------------------- |
| [add()](https://www.runoob.com/java/java-arraylist-add.html) | 将元素插入到指定位置的 arraylist 中           |
| [addAll()](https://www.runoob.com/java/java-arraylist-addall.html) | 添加集合中的所有元素到 arraylist 中           |
| [clear()](https://www.runoob.com/java/java-arraylist-clear.html) | 删除 arraylist 中的所有元素                   |
| [clone()](https://www.runoob.com/java/java-arraylist-clone.html) | 复制一份 arraylist                            |
| [contains()](https://www.runoob.com/java/java-arraylist-contains.html) | 判断元素是否在 arraylist                      |
| [get()](https://www.runoob.com/java/java-arraylist-get.html) | 通过索引值获取 arraylist 中的元素             |
| [indexOf()](https://www.runoob.com/java/java-arraylist-indexof.html) | 返回 arraylist 中元素的索引值                 |
| [removeAll()](https://www.runoob.com/java/java-arraylist-removeall.html) | 删除存在于指定集合中的 arraylist 里的所有元素 |
| [remove()](https://www.runoob.com/java/java-arraylist-remove.html) | 删除 arraylist 里的单个元素                   |
| [size()](https://www.runoob.com/java/java-arraylist-size.html) | 返回 arraylist 里元素数量                     |
| [isEmpty()](https://www.runoob.com/java/java-arraylist-isempty.html) | 判断 arraylist 是否为空                       |
| [subList()](https://www.runoob.com/java/java-arraylist-sublist.html) | 截取部分 arraylist 的元素                     |
| [set()](https://www.runoob.com/java/java-arraylist-set.html) | 替换 arraylist 中指定索引的元素               |
| [sort()](https://www.runoob.com/java/java-arraylist-sort.html) | 对 arraylist 元素进行排序                     |
| [toArray()](https://www.runoob.com/java/java-arraylist-toarray.html) | 将 arraylist 转换为数组                       |
| [toString()](https://www.runoob.com/java/java-arraylist-tostring.html) | 将 arraylist 转换为字符串                     |
| [ensureCapacity](https://www.runoob.com/java/java-arraylist-surecapacity.html)() | 设置指定容量大小的 arraylist                  |
| [lastIndexOf()](https://www.runoob.com/java/java-arraylist-lastindexof.html) | 返回指定元素在 arraylist 中最后一次出现的位置 |
| [retainAll()](https://www.runoob.com/java/java-arraylist-retainall.html) | 保留 arraylist 中在指定集合中也存在的那些元素 |
| [containsAll()](https://www.runoob.com/java/java-arraylist-containsall.html) | 查看 arraylist 是否包含指定集合中的所有元素   |
| [trimToSize()](https://www.runoob.com/java/java-arraylist-trimtosize.html) | 将 arraylist 中的容量调整为数组中的元素个数   |
| [removeRange()](https://www.runoob.com/java/java-arraylist-removerange.html) | 删除 arraylist 中指定索引之间存在的元素       |
| [replaceAll()](https://www.runoob.com/java/java-arraylist-replaceall.html) | 将给定的操作内容替换掉数组中每一个元素        |
| [removeIf()](https://www.runoob.com/java/java-arraylist-removeif.html) | 删除所有满足特定条件的 arraylist 元素         |
| [forEach()](https://www.runoob.com/java/java-arraylist-foreach.html) | 遍历 arraylist 中每一个元素并执行特定操作     |

### 2.3 ArrayList 遍历

```java
import java.util.ArrayList;
import java.util.Iterator;
import java.util.List;

public class ArrayListTraverse {
    public void arrayListTraversal(List<Integer> lists){
        /* 第一种遍历方式 */
        System.out.print("for循环的遍历方式：");
        for (int i = 0; i < lists.size(); i++) {
            System.out.print(lists.get(i));
        }
        System.out.println();

        /* 第二种遍历方式 */
        System.out.print("foreach的遍历方式：");
        for (Integer list : lists) {
            System.out.print(list);
        }
        System.out.println();

        /* 第三种遍历方式 */
        System.out.print("Iterator的遍历方式：");
//        for (Iterator<Integer> list = lists.iterator(); list.hasNext();) {
//            System.out.print(list.next());
//        }
        Iterator iterator = lists.iterator();
        while(iterator.hasNext()){
            System.out.print(iterator.next());
        }
        System.out.println();
    }
    public static void main(String[] args) {
        List<Integer> lists = new ArrayList<Integer>();
        /* 添加元素 */
        for (int i = 0; i < 10; i++) {
            lists.add(i);
        }
        new ArrayListTraverse().arrayListTraversal(lists);
    }
}
```

### 2.4 ArrayList 源码解析

当前使用版本为 JDK1.8

#### 2.4.1 类结构

![image-20210419134534744](https://gitee.com/Kunaly/picture-bed/raw/master/img/image-20210419134534744.png)

```java
public class ArrayList<E> extends AbstractList<E>
        implements List<E>, RandomAccess, Cloneable, java.io.Serializable
```

实现了 4 个接口，分别是：

- java.util.List 接口，提供数组的添加、删除、修改、迭代遍历等操作。

- java.util.RandomAccess 接口，表示 ArrayList 支持快速的随机访问。

- java.io.Serializable 接口，表示 ArrayList 支持序列化的功能。

- java.lang.Cloneable 接口，表示 ArrayList 支持克隆。

继承了 java.util.AbstractList 抽象类，而 AbstractList 提供了 List 接口的骨架实现，大幅度的减少了实现迭代遍历相关操作的代码。可能这样表述有点抽象，可以点到 java.util.AbstractList 抽象类中看看，例如说 #iterator()、#indexOf(Object o) 等方法。不过在下面中我们会看到，ArrayList 大量重写了 AbstractList 提供的方法实现。所以，AbstractList 对于 ArrayList 意义不大，更多的是 AbstractList 其它子类享受了这个福利。

#### 2.4.2 属性值

ArrayList 底层是基于数组来实现容量大小动态变化的。

```java
	//空数组,当初始化指定容量为0或者指定初始化元素个数为0时使用
    private static final Object[] EMPTY_ELEMENTDATA = {};
    
    //空数组 区别于上面空数组，仅在无参数构造器时使用，表示默认值
    private static final Object[] DEFAULTCAPACITY_EMPTY_ELEMENTDATA = {};
    
    //用于存储数据数组
    transient Object[] elementData; // non-private to simplify nested class access
    
    //该ArrayList中的元素个数   
    private int size;

```

**上面的 size 是指 elementData 中实际有多少个元素，而 elementData.length 为集合容量，表示最多可以容纳多少个元素。**

 默认初始容量大小为 10;

```java
/**
 * Default initial capacity.
 */
private static final int DEFAULT_CAPACITY = 10;
```

#### 2.4.3 构造函数

##### **无参构造函数**

```
/**
 * Constructs an empty list with an initial capacity of ten.
 */
public ArrayList() {
    this.elementData = DEFAULTCAPACITY_EMPTY_ELEMENTDATA;
}
```

**注意：注释是说构造一个容量大小为 10 的空的 list 集合，但构造函数了只是给 elementData 赋值了一个空的数组，其实是在第一次添加元素时容量扩大至 10 的。**



##### **有参构造函数**

**构造一个初始容量大小为 initialCapacity 的 ArrayList**

```java
/**
 * Constructs an empty list with the specified initial capacity.
 *
 * @param  initialCapacity  the initial capacity of the list
 * @throws IllegalArgumentException if the specified initial capacity
 *         is negative
 */
public ArrayList(int initialCapacity) {
    if (initialCapacity > 0) {
        this.elementData = new Object[initialCapacity];
    } else if (initialCapacity == 0) {
        this.elementData = EMPTY_ELEMENTDATA;
    } else {
        throw new IllegalArgumentException("Illegal Capacity: " + initialCapacity);
    }
}
```

由以上源码可见： 当使用无参构造函数时是把 DEFAULTCAPACITY_EMPTY_ELEMENTDATA 赋值给 elementData。 当 initialCapacity 为零时则是把 EMPTY_ELEMENTDATA 赋值给 elementData。 当 initialCapacity 大于零时初始化一个大小为 initialCapacity 的 object 数组并赋值给 elementData。

**使用指定 Collection 来构造 ArrayList 的构造函数**

```java
/**
 * Constructs a list containing the elements of the specified
 * collection, in the order they are returned by the collection's
 * iterator.
 *
 * @param c the collection whose elements are to be placed into this list
 * @throws NullPointerException if the specified collection is null
 */
public ArrayList(Collection<? extends E> c) {
    elementData = c.toArray();
    if ((size = elementData.length) != 0) {
        // c.toArray might (incorrectly) not return Object[] (see 6260652)
        // 解释：此处是用于解决 JDK-6260652 的 Bug 。它在 JDK9 中被解决，也就是说，JDK8 还会存在该问题。
        if (elementData.getClass() != Object[].class)
            elementData = Arrays.copyOf(elementData, size, Object[].class);
    } else {
        // replace with empty array.
        this.elementData = EMPTY_ELEMENTDATA;
    }
}
```

将 Collection 转化为数组并赋值给 elementData，把 elementData 中元素的个数赋值给 size。 如果 size 不为零，则判断 elementData 的 class 类型是否为 Object[]，不是的话则做一次转换。 如果 size 为零，则把 EMPTY_ELEMENTDATA 赋值给 elementData，相当于new ArrayList(0)。

#### 2.4.4 主要方法

**add(E e) 方法  顺序添加元素 **

```java
public boolean add(E e) {
	//确定容量
	ensureCapacityInternal(size + 1); 
	//将元素添加至现有元素的末尾
	elementData[size++] = e;
	return true;
}
```

只要清楚ArrayList的扩容过程，添加元素的过程就很简单了，只需要将元素添加到现有元素的末尾

**add(int index,E e) 指定位置添加元素 **

```java
public void add(int index, E element) {
	//检查删除位置是否有效
	rangeCheckForAdd(index);
	//确定容量
	ensureCapacityInternal(size + 1);  // Increments modCount!!
	//将该位置后面的所有元素往后移一位
	System.arraycopy(elementData, index, elementData, index + 1,
					 size - index);
	elementData[index] = element;
	size++;
}
```

**删除元素 remove() 方法**

```java
public E remove(int index) {
	//检查删除位置是否越界
	rangeCheck(index);
	modCount++;
	//取出该元素作为方法的返回值
	E oldValue = elementData(index);
	//如果不是删除末尾的元素,需要将删除元素位置后面的所有元素向前移一位
	int numMoved = size - index - 1;
	if (numMoved > 0)
		System.arraycopy(elementData, index+1, elementData, index, numMoved);
	elementData[--size] = null; // clear to let GC do its work
	return oldValue;
}
```

#### 2.4.5 ArrayList 扩容详解

ArrayList最大的特点就是可以动态扩容，下面我们分析扩容过程

```java
    //确认容量是否需要扩容
    private void ensureCapacityInternal(int minCapacity) {
    	
    	if (elementData == DEFAULTCAPACITY_EMPTY_ELEMENTDATA) {
    		//如果为默认初始化，则将最小所需容量设置为默认大小10和传入参数(希望最小容量)的最大值
    		//在第一次添加元素时，数组容量默认值为10
    		minCapacity = Math.max(DEFAULT_CAPACITY, minCapacity);
    	}
    	//确认实际需要的容量大小	
    	ensureExplicitCapacity(minCapacity);
    }
    
    
    private void ensureExplicitCapacity(int minCapacity) {
    	modCount++;
    
    	// 如果最小希望容量大于当前存储元素数组长度,则进行扩容
    	if (minCapacity - elementData.length > 0)
    		grow(minCapacity);
    }
    
    //扩容
    private void grow(int minCapacity) {
    	//记录原存储元素数组长度
    	int oldCapacity = elementData.length;
    	//每次扩容基于原存储元素数组长度 * 1.5 (即原来容量的1.5倍)
    	int newCapacity = oldCapacity + (oldCapacity >> 1);
    	if (newCapacity - minCapacity < 0)
    		//如果扩容后还是小于最小所需容量,则将最小所需容量设置为新容量值
    		newCapacity = minCapacity;
    	//这里的MAX_ARRAY_SIZE为 Integer.MAX_VALUE - 8,如果分配更大的值,可能会造成OutOfMemoryError,但是ArrayList支持将容量扩大到Integer.MAX_VALUE
    	if (newCapacity - MAX_ARRAY_SIZE > 0) 
    		//如果大于ArrayList所希望的最大值,继续扩容
    		newCapacity = hugeCapacity(minCapacity);
    	//将原存储元素数组中的所有元素拷贝之新数组
    	elementData = Arrays.copyOf(elementData, newCapacity);
    }
    
    private static int hugeCapacity(int minCapacity) {
    	//这里minCapacity小于零是不可能的,只有在该值已经溢出Integer的值才会出现小于零的情况,抛出异常
    	if (minCapacity < 0) 
    		throw new OutOfMemoryError();
    	//分配容量最大值为Integer.MAX_VALUE
    	return (minCapacity > MAX_ARRAY_SIZE) ?
    		Integer.MAX_VALUE :
    		MAX_ARRAY_SIZE;
    }
```

**扩容过程主要分为3步：**

1. 确定需要的容量，如果大于当前容量，则触发扩容；
2. 基于原容量的1.5倍计算新容量值，如果新容量值大于所需要的容量值则使用新容量值否则使用所需要的容量值；
3. 创建新容量值的数组，将原数组中元素拷贝至新数组。

**图解扩容过程**：

![image-20210417171317208](https://gitee.com/Kunaly/picture-bed/raw/master/img/image-20210417171317208.png)

ArrayList每次扩容就是新建一个存储元素数组，数组大小为原数组1.5倍，然后将原数组元素拷贝至新数组。

## 3. LinkedList

### 3.1 LinkedList 简介

链表（Linked list）是一种常见的基础数据结构，是一种线性表，但是并不会按线性的顺序存储数据，而是在每一个节点里存到下一个节点的地址。

LinkedList底层使用的是双向链表，双向链表额结构如下：

![img](https://gitee.com/Kunaly/picture-bed/raw/master/img/610px-Doubly-linked-list.svg_.png)



### 3.2 LinkedList 方法

API：[https://www.runoob.com/manual/jdk11api/java.base/java/util/LinkedList.html](https://www.runoob.com/manual/jdk11api/java.base/java/util/LinkedList.html)

| 方法                                           | 描述                                                         |
| :--------------------------------------------- | :----------------------------------------------------------- |
| public boolean add(E e)                        | 链表末尾添加元素，返回是否成功，成功为 true，失败为 false。  |
| public void add(int index, E element)          | 向指定位置插入元素。                                         |
| public boolean addAll(Collection c)            | 将一个集合的所有元素添加到链表后面，返回是否成功，成功为 true，失败为 false。 |
| public boolean addAll(int index, Collection c) | 将一个集合的所有元素添加到链表的指定位置后面，返回是否成功，成功为 true，失败为 false。 |
| public void addFirst(E e)                      | 元素添加到头部。                                             |
| public void addLast(E e)                       | 元素添加到尾部。                                             |
| public boolean offer(E e)                      | 向链表末尾添加元素，返回是否成功，成功为 true，失败为 false。 |
| public boolean offerFirst(E e)                 | 头部插入元素，返回是否成功，成功为 true，失败为 false。      |
| public boolean offerLast(E e)                  | 尾部插入元素，返回是否成功，成功为 true，失败为 false。      |
| public void clear()                            | 清空链表。                                                   |
| public E removeFirst()                         | 删除并返回第一个元素。                                       |
| public E removeLast()                          | 删除并返回最后一个元素。                                     |
| public boolean remove(Object o)                | 删除某一元素，返回是否成功，成功为 true，失败为 false。      |
| public E remove(int index)                     | 删除指定位置的元素。                                         |
| public E poll()                                | 删除并返回第一个元素。                                       |
| public E remove()                              | 删除并返回第一个元素。                                       |
| public boolean contains(Object o)              | 判断是否含有某一元素。                                       |
| public E get(int index)                        | 返回指定位置的元素。                                         |
| public E getFirst()                            | 返回第一个元素。                                             |
| public E getLast()                             | 返回最后一个元素。                                           |
| public int indexOf(Object o)                   | 查找指定元素从前往后第一次出现的索引。                       |
| public int lastIndexOf(Object o)               | 查找指定元素最后一次出现的索引。                             |
| public E peek()                                | 返回第一个元素。                                             |
| public E element()                             | 返回第一个元素。                                             |
| public E peekFirst()                           | 返回头部元素。                                               |
| public E peekLast()                            | 返回尾部元素。                                               |
| public E set(int index, E element)             | 设置指定位置的元素。                                         |
| public Object clone()                          | 克隆该列表。                                                 |
| public Iterator descendingIterator()           | 返回倒序迭代器。                                             |
| public int size()                              | 返回链表元素个数。                                           |
| public ListIterator listIterator(int index)    | 返回从指定位置开始到末尾的迭代器。                           |
| public Object[] toArray()                      | 返回一个由链表元素组成的数组。                               |
| public T[] toArray(T[] a)                      | 返回一个由链表元素转换类型而成的数组。                       |

### 3.3 LinkedList 源码解析

#### 3.3.1 类结构 

![image-20210419134506971](https://gitee.com/Kunaly/picture-bed/raw/master/img/image-20210419134506971.png)

inkedList 是一个继承于AbstractSequentialList的双向链表。其定义如下：

```java
public class LinkedList<E>
    extends AbstractSequentialList<E>
    implements List<E>, Deque<E>, Cloneable, java.io.Serializable {
```
由定义可以看出：

> LinkedList<E>,支持泛型
> 实现Deque接口，说明可以当做队列
> 实现Serializable接口, 可序列化
> 实现Cloneable接口

#### 3.3.2 属性值

```java
//集合元素数量
transient int size = 0;
//链表头节点
transient Node<E> first;
//链表尾节点
transient Node<E> last;
```

节点结构定义:

```java
private static class Node<E> {
        E item;//元素值
        Node<E> next;//后置节点
        Node<E> prev;//前置节点
 
        Node(Node<E> prev, E element, Node<E> next) {
            this.item = element;
            this.next = next;
            this.prev = prev;
        }
    }
```

由节点的结构可以看出，LinkedList是双向链表结构。

#### 3.3.3 构造函数

**无参数构造函数**

    public LinkedList() {
    
    }
**使用集合创建**

```
public LinkedList(Collection<? extends E> c) {
    this();
    addAll(c);  //见下面3.3.4addAll()方法
}
```

#### 3.3.4 主要方法

**1、addAll() 方法**

```java
public boolean addAll(Collection<? extends E> c) {

    //以size为插入位置索引，插入集合c中所有元素
    return addAll(size, c);
}
 
public boolean addAll(int index, Collection<? extends E> c) {

    //检查索引位置是否合法
    checkPositionIndex(index);
 
    //将目标集合c转为数组
    Object[] a = c.toArray();
    //获得待添加目标数组的长度
    int numNew = a.length;
    //若长度为0，无需添加，直接返回
    if (numNew == 0)
        return false;
 
    //index节点的前置节点，后置节点
    Node<E> pred, succ;
    
    //在链表尾部追加数据
    if (index == size) {
        succ = null;
        pred = last;
    } else {
        //取出index节点，作为后置节点
        succ = node(index);
        //前置节点是，index节点的前一个节点
        pred = succ.prev;
    }
    
    //变量数组a，依次添加节点
    for (Object o : a) {
        @SuppressWarnings("unchecked") E e = (E) o;
        //以前置节点pred 和 元素值e，构建new一个新节点，
        Node<E> newNode = new Node<>(pred, e, null);
        //如果前置节点pred是空，说明是头结点
        if (pred == null)
            first = newNode;
        else前置节点不为空则将pred的后置节点设置为新节点newNode
            pred.next = newNode;
        pred = newNode;//将当前节点指针向后移动
    }
 
    //遍历结束，到达链表尾，设置尾节点
    if (succ == null) {
        last = pred;
    } else {
        //否则是在队中插入的节点 ，更新前置节点 后置节点
        pred.next = succ;
        succ.prev = pred;
    }
 
    size += numNew;//更新节点数量size
    modCount++;
    return true;
}
```
**2、获取元素get()**

```java
//根据索引index获取元素
public E get(int index) {
    checkElementIndex(index);//判断是否越界 [0,size)
    return node(index).item; //调用node()方法 取出 Node节点，
}
//根据index 查询出Node
Node<E> node(int index) {
        // assert isElementIndex(index);
        // 首先根据index大小判断其位置，然后进行折半查找。
        if (index < (size >> 1)) {
            Node<E> x = first;
            for (int i = 0; i < index; i++)
                x = x.next;
            return x;
        } else {
            Node<E> x = last;
            for (int i = size - 1; i > index; i--)
                x = x.prev;
            return x;
        }
    }
```

**3、添加元素add 直接添加节点至末尾**

```java
//在尾部插入一个节点： add
public boolean add(E e) {
    linkLast(e);
    return true;
}
 
//生成新节点 并插入到 链表尾部， 更新 last/first 节点。
void linkLast(E e) { 
    final Node<E> l = last; //记录原尾部节点
    final Node<E> newNode = new Node<>(l, e, null);//以原尾部节点为新节点的前置节点
    last = newNode;//更新尾部节点
    if (l == null)//若原链表为空链表，需要额外更新头结点
        first = newNode;
    else//否则更新原尾节点的后置节点为现在的尾节点（新节点）
        l.next = newNode;
    size++;//修改size
    modCount++;//修改modCount
}
```
**4、在指定下标位置插入节点 add(int index, E element)**

```java
//在指定下标，index处，插入一个节点
public void add(int index, E element) {
    checkPositionIndex(index);//检查下标是否越界[0,size]
    if (index == size)//在尾节点后插入
        linkLast(element);
    else//在中间插入
        linkBefore(element, node(index));
}
//在succ节点前，插入一个新节点e
void linkBefore(E e, Node<E> succ) {
    // assert succ != null;
    //保存后置节点的前置节点
    final Node<E> pred = succ.prev;
    //以前置和后置节点和元素值e 构建一个新节点
    final Node<E> newNode = new Node<>(pred, e, succ);
    //新节点new是原节点succ的前置节点
    succ.prev = newNode;
    if (pred == null)//如果之前的前置节点是空，说明succ是原头结点。所以新节点是现在的头结点
        first = newNode;
    else//否则构建前置节点的后置节点为new
        pred.next = newNode;
    size++;//修改数量
    modCount++;//修改modCount
}
```
 **5、删除元素remove**

删除索引为index的元素 remove(int index)

```java
//删：remove目标节点
public E remove(int index) {
    //检查是否越界
    checkElementIndex(index);
    //调用unlink删除节点
    return unlink(node(index));
}

//从链表上删除x节点
E unlink(Node<E> x) {

    // assert x != null;
    //当前节点的元素值，设置为final，不可更改
    final E element = x.item; 
    //当前节点的后置节点
    final Node<E> next = x.next; 
    //当前节点的前置节点
    final Node<E> prev = x.prev;
    
    //如果前置节点为空(说明当前节点原本是头结点)
    if (prev == null) { 
        //则头结点为后置节点 
        first = next;  
    } else { 
        prev.next = next;
        x.prev = null; //将当前节点的 前置节点置空
    }
    
    //如果后置节点为空（说明当前节点原本是尾节点）
    if (next == null) {
        last = prev; //则 尾节点为前置节点
    } else {
        next.prev = prev;
        x.next = null;//将当前节点x的后置节点置空
    }
 
    x.item = null; //将当前元素值置空
    size--; //修改数量
    modCount++;  //修改modCount
    return element; //返回取出的元素值
}
    
private void checkElementIndex(int index) {
    if (!isElementIndex(index))
        throw new IndexOutOfBoundsException(outOfBoundsMsg(index));
}

private boolean isElementIndex(int index) {
    return index >= 0 && index < size;
}
```
**删除指定的元素 remove(Object o)**

```java
//因为要考虑 null元素，也是分情况遍历
public boolean remove(Object o) {
    if (o == null) {//如果要删除的是null节点(从remove和add 里 可以看出，允许元素为null)
        //遍历每个节点 对比
        for (Node<E> x = first; x != null; x = x.next) {
            if (x.item == null) {
                unlink(x);
                return true;
            }
        }
    } else {
        for (Node<E> x = first; x != null; x = x.next) {
            if (o.equals(x.item)) {
                unlink(x);
                return true;
            }
        }
    }
    return false;
}
//将节点x，从链表中删除
E unlink(Node<E> x) {
    // assert x != null;
    final E element = x.item;//继续元素值，供返回
    final Node<E> next = x.next;//保存当前节点的后置节点
    final Node<E> prev = x.prev;//前置节点
 
    if (prev == null) {//前置节点为null，
        first = next;//则首节点为next
    } else {//否则 更新前置节点的后置节点
        prev.next = next;
        x.prev = null;//记得将要删除节点的前置节点置null
    }
    //如果后置节点为null，说明是尾节点
    if (next == null) {
        last = prev;
    } else {//否则更新 后置节点的前置节点
        next.prev = prev;
        x.next = null;//记得删除节点的后置节点为null
    }
    //将删除节点的元素值置null，以便GC
    x.item = null;
    size--;//修改size
    modCount++;//修改modCount
    return element;//返回删除的元素值
}
```
**6、修改元素set**

```java
public E set(int index, E element) {
 //检查越界[0,size)
    checkElementIndex(index);
    //根据index取出对应的Node
    Node<E> x = node(index);
    //保存旧值 供返回
    E oldVal = x.item;
    //用新值覆盖旧值
    x.item = element;
    //返回旧值
    return oldVal;
}
```
### 3.4 LinkedList 总结

LinkedList 是双向链表，对其大部分操作属于对双向链表的增删改查。因此，对于LinkedList的学习主要是掌握数据结构链表的操作。此外，LinkedList在查找时使用了折半查找的方式，提升了查找效率。

### 3.5 ArrayList 与 LinkedList 对比

1. ArrayList是实现了基于动态数组的数据结构，LinkedList是基于链表结构。
2. 对于随机访问的get和set方法，ArrayList要优于LinkedList，因为LinkedList要移动指针。
3. 对于新增和删除操作add和remove，LinkedList比较占优势，因为ArrayList要移动数据。

**使用场景：**

1. 对ArrayList和LinkedList而言，在列表末尾增加一个元素所花的开销都是固定的。对 ArrayList而言，主要是在内部数组中增加一项，指向所添加的元素，偶尔可能会导致对数组重新进行分配；而对LinkedList而言，这个开销是 统一的，分配一个内部Entry对象。
2. 在ArrayList集合中添加或者删除一个元素时，当前的列表所所有的元素都会被移动。而LinkedList集合中添加或者删除一个元素的开销是固定的。
3. LinkedList集合不支持 高效的随机随机访问（RandomAccess），因为可能产生二次项的行为。
4. ArrayList的空间浪费主要体现在在list列表的结尾预留一定的容量空间，而LinkedList的空间花费则体现在它的每一个元素都需要消耗相当的空间。

## 4. Set 

**特点：**

不可重复性

无序性：通过HashCode方法算出的值来决定在数组中存放的位置。

### 4.1 HashSet

#### 4.1.1 HashSet 简介

HashSet实现了 Set 接口，内部是由 HashMap 实例辅助实现的。它不保证元素的顺序，数据允许为 null。

假如 hash 方法将数据分散地比较合理，比如一个 bucket 一个数据，那么 add、remove、contains、size 性能开销是常数时间。

这个类非线程安全的，如果多线程并发访问，并且至少一个线程在做修改操作，那么必须在外部做好同步处理。例如使用：Set s = Collections.synchronizedSet(new HashSet(...));

#### 4.1.2 HashSet 方法

HashSet API : [https://www.runoob.com/manual/jdk11api/java.base/java/util/HashSet.html](https://www.runoob.com/manual/jdk11api/java.base/java/util/HashSet.html)

| 方法                 | 描述                                             |
| -------------------- | ------------------------------------------------ |
| `add(E e)`           | 如果指定的元素尚不存在，则将其添加到此集合中。   |
| `clear()`            | 从该集中删除所有元素。                           |
| `clone()`            | 返回此 `HashSet`实例的浅表副本：未克隆元素本身。 |
| `contains(Object o)` | 如果此set包含指定的元素，则返回 `true` 。        |
| `isEmpty()`          | 如果此集合不包含任何元素，则返回 `true` 。       |
| `iterator()`         | 返回此set中元素的迭代器。                        |
| `remove(Object o)`   | 如果存在，则从该集合中移除指定的元素。           |
| `size()`             | 返回此集合中的元素数（基数）。                   |

#### 4.1.3 HashSet 源码解析

##### 4.1.3.1 类结构

![image-20210419134402213](https://gitee.com/Kunaly/picture-bed/raw/master/img/image-20210419134402213.png)

```java
public class HashSet<E>
    extends AbstractSet<E>
    implements Set<E>, Cloneable, java.io.Serializable
```

HashSet 也实现了 Cloneable 接口和 Serializable 接口，分别用来支持克隆以及支持序列化。还实现了 Set 接口，该接口定义了 Set 集合类型的一套规范。

##### 4.1.3.2 属性值

```java
//HashSet集合中的内容是通过 HashMap 数据结构来存储的
private transient HashMap<E,Object> map;
//向HashSet中添加数据，数据在上面的 map 结构是作为 key 存在的，而value统一都是 PRESENT
private static final Object PRESENT = new Object();
```

第一个 定义一个 HashMap，作为实现 HashSet 的数据结构；

第二个 PRESENT 对象，因为前面讲过 HashMap 是作为键值对 key-value 进行存储的，而 HashSet 不是键值对，那么选择 HashMap 作为实现，其原理就是存储在 HashSet 中的数据 作为 Map 的 key，而 Map 的value 统一为 PRESENT。

##### 4.1.3.3 构造函数

**无参构造**

```java
/**
 * Constructs a new, empty set; the backing <tt>HashMap</tt> instance has
 * default initial capacity (16) and load factor (0.75).
 */
public HashSet() {
    map = new HashMap<>();
}
```

**有参构造**

1、指定初容量

```
public HashSet(int initialCapacity) {
    map = new HashMap<>(initialCapacity);
}
```

2、指定初始 容量的加载因子

```java
/**
 * Constructs a new, empty set; the backing <tt>HashMap</tt> instance has
 * the specified initial capacity and the specified load factor.
 *
 * @param      initialCapacity   the initial capacity of the hash map
 * @param      loadFactor        the load factor of the hash map
 * @throws     IllegalArgumentException if the initial capacity is less
 *             than zero, or if the load factor is nonpositive
 */
public HashSet(int initialCapacity, float loadFactor) {
    map = new HashMap<>(initialCapacity, loadFactor);
}
```

3、构造包含指定集合中的元素

```java
/**
 * Constructs a new set containing the elements in the specified
 * collection.  The <tt>HashMap</tt> is created with default load factor
 * (0.75) and an initial capacity sufficient to contain the elements in
 * the specified collection.
 *
 * @param c the collection whose elements are to be placed into this set
 * @throws NullPointerException if the specified collection is null
 */
public HashSet(Collection<? extends E> c) {
    map = new HashMap<>(Math.max((int) (c.size()/.75f) + 1, 16));
    addAll(c);
}
```

集合容量很好理解，这里我介绍一下什么是加载因子。在 HashMap 中，能够存储元素的数量就是：总的容量*加载因子 ，新增一个元素时，如果HashMap集合中的元素大于前面公式计算的结果了，那么就必须要进行扩容操作，从时间和空间考虑，加载因子一般都选默认的0.75。

##### 4.1.3.4 主要方法

1、添加元素

```java
public boolean add(E e) {
    return map.put(e, PRESENT)==null;
}
```

通过 map.put() 方法来添加元素，该方法如果新插入的key不存在，则返回null，如果新插入的key存在，则返回原key对应的value值（注意新插入的value会覆盖原value值）。

也就是说 HashSet 的 add(E e) 方法，会将 e 作为 key，PRESENT 作为 value 插入到 map 集合中，如果 e 不存在，则插入成功返回 true;如果存在，则返回false。

2、删除元素

```java
public boolean remove(Object o) {
    return map.remove(o)==PRESENT;
}
```

调用 HashMap 的remove(Object o) 方法，该方法会首先查找 map 集合中是否存在 o ，如果存在则删除，并返回该值，如果不存在则返回 null。

也就是说 HashSet 的 remove(Object o) 方法，删除成功返回 true，删除的元素不存在会返回 false。

3、查找元素

```java
public boolean contains(Object o) {
    return map.containsKey(o);
}
```

#### 4.1.4 HashSet 总结

HashSet实际上是一个HashMap实例，都是一个存放链表的数组。它不保证存储元素的迭代顺序；此类允许使用null元素。HashSet中不允许有重复元素，这是因为HashSet是基于HashMap实现的，HashSet中的元素都存放在HashMap的key上面，而value中的值都是统一的一个固定对象private static final Object PRESENT = new Object();

HashSet中add方法调用的是底层HashMap中的put()方法，而如果是在HashMap中调用put，首先会判断key是否存在，如果key存在则修改value值，如果key不存在这插入这个key-value。而在set中，因为value值没有用，也就不存在修改value值的说法，因此往HashSet中添加元素，首先判断元素（也就是key）是否存在，如果不存在这插入，如果存在着不插入，这样HashSet中就不存在重复值。

 所以判断key是否存在就要重写元素的类的equals()和hashCode()方法，当向Set中添加对象时，首先调用此对象所在类的hashCode()方法，计算次对象的哈希值，此哈希值决定了此对象在Set中存放的位置；若此位置没有被存储对象则直接存储，若已有对象则通过对象所在类的equals()比较两个对象是否相同，相同则不能被添加。

### 4.2 TreeSet

#### 4.2.1 TreeSet 简介

TreeSet的作用是保存无重复的数据，不过还对这些数据进行了排序。TreeMap的底层是通过红黑树实现的，（[红黑树具体内容参考连接](http://www.tianxiaobo.com/2018/01/11/%E7%BA%A2%E9%BB%91%E6%A0%91%E8%AF%A6%E7%BB%86%E5%88%86%E6%9E%90/)）所以TreeSet底层也是通过红黑树实现的。TreeSet最主要的特点就是对元素进行了排序。我们对其特点进行总结一下：

（1）TreeSet是基于TreeMap的NavigableSet实现。

（2）TreeSet的元素存储在TreeMap中的key中，TreeMap的value是一个常量对象。

（3）非线程安全 。

（4）java8新增分割器spliterator() 方法。

#### 4.2.2 TreeSet 方法

TreeSet API : [https://www.runoob.com/manual/jdk11api/java.base/java/util/TreeSet.html](https://www.runoob.com/manual/jdk11api/java.base/java/util/TreeSet.html)

| 方法              | 描述                                                         |                                                              |
| :---------------- | :----------------------------------------------------------- | ------------------------------------------------------------ |
| `boolean`         | `add(E e)`                                                   | 如果指定的元素尚不存在，则将其添加到此集合中。               |
| `boolean`         | `addAll(Collection<? extends E> c)`                          | 将指定集合中的所有元素添加到此集合中。                       |
| `E`               | `ceiling(E e)`                                               | 返回此set中大于或等于给定元素的 `null`元素，如果没有这样的元素，则 `null` 。 |
| `void`            | `clear()`                                                    | 从该集中删除所有元素。                                       |
| `Object`          | `clone()`                                                    | 返回此 `TreeSet`实例的浅表副本。                             |
| `boolean`         | `contains(Object o)`                                         | 如果此set包含指定的元素，则返回 `true` 。                    |
| `Iterator<E>`     | `descendingIterator()`                                       | 以降序返回此集合中元素的迭代器。                             |
| `NavigableSet<E>` | `descendingSet()`                                            | 返回此set中包含的元素的逆序视图。                            |
| `E`               | `first()`                                                    | 返回此集合中当前的第一个（最低）元素。                       |
| `E`               | `floor(E e)`                                                 | 返回此set中小于或等于给定元素的最大元素，如果没有这样的元素，则 `null` 。 |
| `SortedSet<E>`    | `headSet(E toElement)`                                       | 返回此set的部分视图，其元素严格小于 `toElement` 。           |
| `NavigableSet<E>` | `headSet(E toElement, boolean inclusive)`                    | 返回此set的部分视图，其元素小于（或等于，如果 `inclusive`为true） `toElement` 。 |
| `E`               | `higher(E e)`                                                | 返回此集合中的最小元素严格大于给定元素，如果没有这样的元素，则 `null` 。 |
| `boolean`         | `isEmpty()`                                                  | 如果此集合不包含任何元素，则返回 `true` 。                   |
| `Iterator<E>`     | `iterator()`                                                 | 以升序返回此集合中元素的迭代器。                             |
| `E`               | `last()`                                                     | 返回此集合中当前的最后一个（最高）元素。                     |
| `E`               | `lower(E e)`                                                 | 返回此集合中的最大元素严格小于给定元素，如果没有这样的元素，则 `null` 。 |
| `E`               | `pollFirst()`                                                | 检索并删除第一个（最低）元素，如果此组为空，则返回 `null` 。 |
| `E`               | `pollLast()`                                                 | 检索并删除最后一个（最高）元素，如果此集合为空，则返回 `null` 。 |
| `boolean`         | `remove(Object o)`                                           | 如果存在，则从该集合中移除指定的元素。                       |
| `int`             | `size()`                                                     | 返回此集合中的元素数（基数）。                               |
| `Spliterator<E>`  | `spliterator()`                                              | 在此集合中的元素上创建*[late-binding](https://www.runoob.com/manual/jdk11api/java.base/java/util/Spliterator.html#binding)*和*故障快速* [`Spliterator`](https://www.runoob.com/manual/jdk11api/java.base/java/util/Spliterator.html) 。 |
| `NavigableSet<E>` | `subSet(E fromElement, boolean fromInclusive, E toElement, boolean toInclusive)` | 返回此set的部分视图，其元素范围为 `fromElement`到 `toElement` 。 |
| `SortedSet<E>`    | `subSet(E fromElement, E toElement)`                         | 返回此set的部分视图，其元素范围从 `fromElement` （含）到 `toElement` （独占）。 |
| `SortedSet<E>`    | `tailSet(E fromElement)`                                     | 返回此set的部分视图，其元素大于或等于 `fromElement` 。       |
| `NavigableSet<E>` | `tailSet(E fromElement, boolean inclusive)`                  | 返回此set的部分视图，其元素大于（或等于，如果 `inclusive`为true） `fromElement` 。 |

**自定义比较器案例：**

要求对学生首先按照年龄进行排序，如果年龄相同，我们再按照名字的长度进行排序，都是升序。

```java
public class Student{
	private String name;
	private int age;
	public Student(String name, int age) {
		super();
		this.name = name;
		this.age = age;
	}
	@Override
	public String toString() {
		return "Student [name=" + name + ", age=" + age + "]";
	}
	public String getName() {
		return name;
	}
	public int getAge() {
		return age;
	}
}
```

```java
import java.util.Comparator;
import java.util.TreeSet;
public class DemoTreeSet {
	public static void main(String[] args) {
		TreeSet<Student> ts = new TreeSet<>(new Comparator<Student>() {
			@Override
			public int compare(Student o1, Student o2) {
				int num = o1.getAge() - o2.getAge();
				return num == 0 ? o1.getName().length() - o2.getName().length() : num;
			}
		});
        ts.add(new Student("张三",43));
        ts.add(new Student("李四",80));
        ts.add(new Student("王五",79));
        ts.add(new Student("王麻子",79));
		for (Student student : ts) {
			System.out.println(student);
		}
	}
}
 
输出：
Student [name=张三, age=43]
Student [name=王五, age=79]
Student [name=王麻子, age=79]
Student [name=李四, age=80]
```

#### 4.2.3 TreeSet 源码解析

##### 4.2.3.1 类结构

![image-20210419153825168](https://gitee.com/Kunaly/picture-bed/raw/master/img/image-20210419153825168.png)

```java
public class TreeSet<E> extends AbstractSet<E>
    implements NavigableSet<E>, Cloneable, java.io.Serializable
```

实现Serializable接口，即支持序列化。
实现Cloneable接口，即能被克隆。
实现Iterable接口，即能用foreach使用迭代器遍历得到集合元素。
实现了NavigableSet接口，即能支持一系列的导航方法。比如查找与指定目标最匹配项。并且，TreeSet中含有一个”NavigableMap类型的成员变量”m，而m实际上是”TreeMap的实例”。
继承AbstractSet，AbstractSet实现set,所以它是一个Set集合，不包含满足element1.eauqals(element2)的元素树，并且最多包含一个null.

所以，TreeSet的本质是一个”有序的，并且没有重复元素”的集合，而且支持自定义排序。

##### 4.2.3.2 属性值

```java
//TreeSet集合中的内容是通过 NavigableMap 数据结构来存储的
private transient NavigableMap<E,Object> m;
//向TreeSet中添加数据，数据在上面的 map 结构是作为 key 存在的，而value统一都是 PRESENT
private static final Object PRESENT = new Object();
```

**注意**：

1、不是说TreeSet是基于TreeMap实现的，为什么这里的参数是NavigableMap？

答：这是因为TreeMap实现了NavigableMap接口。

2、既然TreeSet只使用了NavigableMap的key，那么直接使用null作为NavigableMap的value不就完了，还方面节省内存？

答：我们直接定位到TreeSet的增删方法的源码：

```java
public boolean add(E e) {
    return m.put(e, PRESENT)==null;
}

public boolean remove(Object o) {
    return m.remove(o)==PRESENT;
}
```

在我们使用add方法时会出现两种put情况：

（1）元素不重复，直接插入即可。

（2）元素e重复，m.put(e,PRESENT)一看 e这个key已经存在了，就会将PRESENT替换掉相应的value值。然后map返回这个value。value不等于null，于是返回false。很明显插入失败了。

但是如果我们把PRESENT替换成null呢？这时候m.put(e, PRESENT)一看e这个key已经存在了，于是map返回null。完了这时候你会发现null等于null。整个add方法返回的就是true。这不就矛盾了嘛。命名插入的是重复数据，返回的结果依然还是true。所以这里使用了PRESENT这个对象就能有效地避免这种情况。

##### 4.2.3.3 构造函数

```java
//方式1: NavigableMap继承SortedMap，SortedMap继承Map
TreeSet(NavigableMap<E,Object> m) {
    this.m = m;
}
//方式2:以自然排序的方式创建一个新的TreeSet
public TreeSet() {
    this(new TreeMap<E,Object>());
}
//方式3:以定制排序的方式创建一个TreeSet
public TreeSet(Comparator<? super E> comparator) {
    this(new TreeMap<>(comparator));
}
//方式4：
public TreeSet(Collection<? extends E> c) {
    this(); //调用方式1创建一个TreeSet
    addAll(c); //向TreeSet中添加Collection集合c里的所有元素
}
//方式5：
public TreeSet(SortedSet<E> s) {
    this(s.comparator()); //调用方式3创建一个TreeSet
    addAll(s);//向TreeSet中添加SortedSer s里的所有元素
}
```

从上述可以看出，TreeSet的构造函数都是通过新建一个TreeMap作为实际存储Set元素的容器。因此得出结论: TreeSet的底层实际使用的存储容器就是TreeMap。TreeSet 里绝大部分方法都是直接调用 TreeMap 的方法来实现的。
如addAll()方法的实现：

```java
public  boolean addAll(Collection<? extends E> c) {
    if (m.size()==0 && c.size() > 0 &&
        c instanceof SortedSet &&
        m instanceof TreeMap) {
        SortedSet<? extends E> set = (SortedSet<? extends E>) c;
        //快看！！！我在这！！！
        TreeMap<E,Object> map = (TreeMap<E, Object>) m;
        Comparator<?> cc = set.comparator();
        Comparator<? super E> mc = map.comparator();
        if (cc==mc || (cc != null && cc.equals(mc))) {
            map.addAllForTreeSet(set, PRESENT);
            return true;
        }
    }
    return super.addAll(c);
}
```
Set几乎都成了Map的一个马甲 , 我们来关注一下TreeSet应用的TreeMap。

**自定义比较器案例：**

要求对学生首先按照年龄进行排序，如果年龄相同，我们再按照名字的长度进行排序，都是升序。

```java
public class Student{
	private String name;
	private int age;
	public Student(String name, int age) {
		super();
		this.name = name;
		this.age = age;
	}
	@Override
	public String toString() {
		return "Student [name=" + name + ", age=" + age + "]";
	}
	public String getName() {
		return name;
	}
	public int getAge() {
		return age;
	}
}
```

```java
import java.util.Comparator;
import java.util.TreeSet;
public class DemoTreeSet {
	public static void main(String[] args) {
		TreeSet<Student> ts = new TreeSet<>(new Comparator<Student>() {
			@Override
			public int compare(Student o1, Student o2) {
				int num = o1.getAge() - o2.getAge();
				return num == 0 ? o1.getName().length() - o2.getName().length() : num;
			}
		});
        ts.add(new Student("张三",43));
        ts.add(new Student("李四",80));
        ts.add(new Student("王五",79));
        ts.add(new Student("王麻子",79));
		for (Student student : ts) {
			System.out.println(student);
		}
	}
}
 
输出：
Student [name=张三, age=43]
Student [name=王五, age=79]
Student [name=王麻子, age=79]
Student [name=李四, age=80]
```

##### 4.2.3.4 主要方法

1、返回子set

```java
//底层就是通过TreeMap的subMap()实现的
public NavigableSet<E> subSet(E fromElement, boolean fromInclusive,
                              E toElement,   boolean toInclusive) {
    return new TreeSet<>(m.subMap(fromElement, fromInclusive,
                                   toElement,   toInclusive));
}
```

2、获取首尾元素并删除

```java
//获取第一个元素并从TreeMap中删除该元素
public E pollFirst() {
    Map.Entry<E,?> e = m.pollFirstEntry();
    return (e == null) ? null : e.getKey();
}
//获取最后一个元素并从TreeMap中删除该元素
public E pollLast() {
    Map.Entry<E,?> e = m.pollLastEntry();
    return (e == null) ? null : e.getKey();
}
```

3、读数据

```java
private void readObject(java.io.ObjectInputStream s)
    throws java.io.IOException, ClassNotFoundException {
    // Read in any hidden stuff
    s.defaultReadObject();

    // Read in Comparator
    @SuppressWarnings("unchecked")
        Comparator<? super E> c = (Comparator<? super E>) s.readObject();

    // Create backing TreeMap
    TreeMap<E,Object> tm = new TreeMap<>(c);
    m = tm;

    // Read in size
    int size = s.readInt();
    //读取TreeSet的全部元素
    tm.readTreeSet(size, s, PRESENT);
}
```

4、写数据

```java
//将TreeSet的比较器，容量，所有元素值都写入到输入流中
private void writeObject(java.io.ObjectOutputStream s)
    throws java.io.IOException {
    // Write out any hidden stuff
    s.defaultWriteObject();

    // Write out Comparator
    s.writeObject(m.comparator());

    // Write out size
    s.writeInt(m.size());

    // Write out all elements in the proper order.
    for (E e : m.keySet())
        s.writeObject(e);
}
```



#### 4.2.4 TreeSet 总结

**对比：**

##### 4.2.4.1 TreeSet 和 TreeMap 对比

相同点：
TreeMap和TreeSet都是有序的集合。
TreeMap和TreeSet都是非同步集合，因此他们不能在多线程之间共享，不过可以使用方法Collections.synchroinzedMap()来实现同步。
运行速度都要比Hash集合慢，他们内部对元素的操作时间复杂度为O(logN)，而HashMap/HashSet则为O(1)。

不同点：
最主要的区别就是TreeSet和TreeMap非别实现Set和Map接口
TreeSet只存储一个对象，而TreeMap存储两个对象Key和Value（仅仅key对象有序）
TreeSet中不能有重复对象，而TreeMap中可以存在。

##### 4.2.4.2 TreeSet 和 HashSet 对比

相同点：
都是唯一不重复的Set集合。

不同点：
底层来说，HashSet是用Hash表来存储数据，而TreeSet是用二叉平衡树来存储数据。 功能上来说，由于TreeSet是有序的Set，可以使用SortedSet。接口的first()、last()等方法。但由于要排序，势必要影响速度。所以，如果不需要顺序的话，还是使用HashSet吧，使用Hash表存储数据的HashSet在速度上更胜一筹。如果需要顺序则TreeSet更为明智。
底层来说，HashSet是用Hash表来存储数据，而TreeSet是用二叉平衡树来存储数据。

##### 4.2.4.3 TreeSet 总结

1、不能有重复的元素；
2、具有排序功能；
3、TreeSet中的元素必须实现Comparable接口并重写compareTo()方法，TreeSet判断元素是否重复 、以及确定元素的顺序 靠的都是这个方法；
①对于java类库中定义的类，TreeSet可以直接对其进行存储，如String，Integer等,因为这些类已经实现了Comparable接口);
②对于自定义类，如果不做适当的处理，TreeSet中只能存储一个该类型的对象实例，否则无法判断是否重复。
4、依赖TreeMap。
5、相对HashSet,TreeSet的优势是有序，劣势是相对读取慢。根据不同的场景选择不同的集合。



## 5. Map 

**特点：**

Map存储的是键值对（Key,value），Map中的Key是无序的且不重复的，所有的key可以看成是一个set集合。

Map中的key如果是自定义的对象必须要重写hashcode和equals方法，Map中的value是无序可重复的，所有的value可以看成是Collection集合，Map中的value如果是自定义类的对象必须重写equals方法。

### 5.1 HashMap

#### 5.1.1 HashMap 简介

HashMap 是一个散列表，它存储的内容是键值对(key-value)映射。

HashMap 实现了 Map 接口，根据键的 HashCode 值存储数据，具有很快的访问速度，最多允许一条记录的键为 null，不支持线程同步。

HashMap 是无序的，即不会记录插入的顺序。

HashMap 继承于AbstractMap，实现了 Map、Cloneable、java.io.Serializable 接口。

#### 5.1.2  HashMap 方法

HashMap API: https://www.runoob.com/manual/jdk11api/java.base/java/util/HashMap.html

| 变量和类型            | 方法                                                         | 描述                                                         |
| :-------------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| `void`                | `clear()`                                                    | 从此映射中删除所有映射。                                     |
| `Object`              | `clone()`                                                    | 返回此 `HashMap`实例的浅表副本：未克隆键和值本身。           |
| `V`                   | `compute(K key, BiFunction<? super K,? super V,? extends V> remappingFunction)` | 尝试计算指定键及其当前映射值的映射（如果没有当前映射， `null` ）。 |
| `V`                   | `computeIfAbsent(K key, Function<? super K,? extends V> mappingFunction)` | 如果指定的键尚未与值关联（或映射到 `null` ），则尝试使用给定的映射函数计算其值并将其输入此映射，除非 `null` 。 |
| `V`                   | `computeIfPresent(K key, BiFunction<? super K,? super V,? extends V> remappingFunction)` | 如果指定键的值存在且为非null，则尝试在给定键及其当前映射值的情况下计算新映射。 |
| `boolean`             | `containsKey(Object key)`                                    | 如果此映射包含指定键的映射，则返回 `true` 。                 |
| `boolean`             | `containsValue(Object value)`                                | 如果此映射将一个或多个键映射到指定值，则返回 `true` 。       |
| `Set<Map.Entry<K,V>>` | `entrySet()`                                                 | 返回此映射中包含的映射的[`Set`](https://www.runoob.com/manual/jdk11api/java.base/java/util/Set.html)视图。 |
| `V`                   | `get(Object key)`                                            | 返回指定键映射到的值，如果此映射不包含键的映射，则返回 `null` 。 |
| `boolean`             | `isEmpty()`                                                  | 如果此映射不包含键 - 值映射，则返回 `true` 。                |
| `Set<K>`              | `keySet()`                                                   | 返回此映射中包含的键的[`Set`](https://www.runoob.com/manual/jdk11api/java.base/java/util/Set.html)视图。 |
| `V`                   | `merge(K key, V value, BiFunction<? super V,? super V,? extends V> remappingFunction)` | 如果指定的键尚未与值关联或与null关联，则将其与给定的非空值关联。 |
| `V`                   | `put(K key, V value)`                                        | 将指定的值与此映射中的指定键相关联。                         |
| `void`                | `putAll(Map<? extends K,? extends V> m)`                     | 将指定映射中的所有映射复制到此映射。                         |
| `V`                   | `remove(Object key)`                                         | 从此映射中删除指定键的映射（如果存在）。                     |
| `int`                 | `size()`                                                     | 返回此映射中键 - 值映射的数量。                              |
| `Collection<V>`       | `values()`                                                   | 返回此映射中包含的值的[`Collection`](https://www.runoob.com/manual/jdk11api/java.base/java/util/Collection.html)视图。 |

案例程序：

```java
import java.util.*;

public class HashMapTest{

    public static void main(String[] args) {
        //创建HashMap对象
        HashMap<Integer,String> map = new HashMap<Integer,String>();
        //添加键值对
        map.put(1,"张三");
        map.put(2,"李四");
        map.put(3,"王五");
        map.put(4,"赵六");
        System.out.println(map);
        //计算大小
        System.out.println(map.size());
        //根据key值访问元素
        System.out.println(map.get(3));
        //迭代HashMap
        //方式1：keySet
        for (Integer i : map.keySet()) {
            System.out.println("key："+ i +"; value:"+map.get(i));
        }
        //方式2：entrySet
        for (Map.Entry<Integer,String> entry : map.entrySet()){
            System.out.println("key: " + entry.getKey() + "; value:"+entry.getValue());
        }
        //方式3：Iterator
        Iterator<Map.Entry<Integer,String>> iterator = map.entrySet().iterator();
        while (iterator.hasNext()){
            Map.Entry<Integer,String> entry = iterator.next();
            System.out.println("key: " + entry.getKey() + "; value:"+entry.getValue());
        }
        //输出所有的value
        for (String value : map.values()){
            System.out.print(value + ",");
        }
        System.out.println();
        //删除元素
        map.remove(4);
        System.out.println(map);
        //清空元素
        map.clear();
        System.out.println(map);

    }
}
```

输出结果：

```java
{1=张三, 2=李四, 3=王五, 4=赵六}
4
王五
key：1; value:张三
key：2; value:李四
key：3; value:王五
key：4; value:赵六
key: 1; value:张三
key: 2; value:李四
key: 3; value:王五
key: 4; value:赵六
key: 1; value:张三
key: 2; value:李四
key: 3; value:王五
key: 4; value:赵六
张三,李四,王五,赵六,
{1=张三, 2=李四, 3=王五}
{}
```

##### HashMap遍历

```java
import java.util.HashMap;
import java.util.Iterator;
import java.util.Map;

public class HashMapDemo {
    public static void main(String[] args) {
        Map<Integer,String> map = new HashMap<Integer,String>();
        map.put(1,"乔峰");
        map.put(2,"虚竹");
        map.put(3,"段誉");
        map.put(4,"慕容复");

        //方法1：使用For-Each迭代entries
        for(Map.Entry<Integer,String> entry : map.entrySet()){
            System.out.println("方法1:key = "+entry.getKey()+",value = "+entry.getValue());
        }

        //方法2：使用For-Each迭代keys和values
        for(Integer key : map.keySet()){
            System.out.println("方法2：key = "+key);
        }
        for(String value : map.values()){
            System.out.println("方法2：values = "+value);
        }

        //方法3：使用Iterator迭代entries
        Iterator iterator = map.entrySet().iterator();
        while (iterator.hasNext()){
            Map.Entry entry = (Map.Entry) iterator.next();
            System.out.println("方法3:key = "+entry.getKey()+",value = "+entry.getValue());
        }

        //方法4：迭代keys并搜索values
        for(Integer key : map.keySet()){
            String value = map.get(key);
            System.out.println("方法4:key = "+key+",value = "+value);
        }
    }
}
```

#### 5.1.3 HashMap 源码解析

##### 5.1.3.1 类结构

![image-20210420103134060](https://gitee.com/Kunaly/picture-bed/raw/master/img/image-20210420103134060.png)

```java
public class HashMap<K,V> extends AbstractMap<K,V>
    implements Map<K,V>, Cloneable, Serializable 
```

HashMap 继承于AbstractMap，实现了Map、Cloneable、java.io.Serializable接口。
HashMap 的实现不是同步的，这意味着它不是线程安全的。它的key、value都可以为null。此外，HashMap中的映射不是有序的。



> JDK 1.8 对 HashMap 进行了比较大的优化，底层实现由之前的 “数组+链表” 改为 “数组+链表+红黑树”，本文就 HashMap 的几个常用的重要方法和 JDK 1.8 之前的死循环问题展开学习讨论。
>
> JDK 1.8 的 HashMap 的数据结构如下图所示，当链表节点较少时仍然是以链表存在，当链表节点较多时（大于8）会转为红黑树。
>




##### 5.1.3.2 属性值

```java
// 默认容量16
static final int DEFAULT_INITIAL_CAPACITY = 1 << 4; 
 
// 最大容量 2^30
static final int MAXIMUM_CAPACITY = 1 << 30;    
 
// 默认负载因子0.75
static final float DEFAULT_LOAD_FACTOR = 0.75f; 
 
// 链表节点转换红黑树节点的阈值, 9个节点转
static final int TREEIFY_THRESHOLD = 8; 
 
// 红黑树节点转换链表节点的阈值, 6个节点转
static final int UNTREEIFY_THRESHOLD = 6;   
 
// 转红黑树时, table的最小长度
static final int MIN_TREEIFY_CAPACITY = 64; 
 
// 链表节点, 继承自Entry
static class Node<K,V> implements Map.Entry<K,V> {  
    final int hash;
    final K key;
    V value;
    Node<K,V> next;
 
    // ... ...
}
 
// 红黑树节点
static final class TreeNode<K,V> extends LinkedHashMap.Entry<K,V> {
    TreeNode<K,V> parent;  // red-black tree links
    TreeNode<K,V> left;
    TreeNode<K,V> right;
    TreeNode<K,V> prev;    // needed to unlink next upon deletion
    boolean red;
   
    // ...
}
```

##### 5.1.3.3 构造函数

```java
//1.指定容量和负载因子
public HashMap(int initialCapacity, float loadFactor) {
        if (initialCapacity < 0)
            throw new IllegalArgumentException("Illegal initial capacity: " +
                                               initialCapacity);
        if (initialCapacity > MAXIMUM_CAPACITY)
            initialCapacity = MAXIMUM_CAPACITY;
        if (loadFactor <= 0 || Float.isNaN(loadFactor))
            throw new IllegalArgumentException("Illegal load factor: " +
                                               loadFactor);
        this.loadFactor = loadFactor;
        this.threshold = tableSizeFor(initialCapacity);
}
 
//2.仅指定容量，使用默认的负载因子，内部实现实际上还是依赖的第一种方法
public HashMap(int initialCapacity) {
	this(initialCapacity, DEFAULT_LOAD_FACTOR);
}
 
//3.使用默认容量和负载因子
public HashMap() {
     this.loadFactor = DEFAULT_LOAD_FACTOR; // all other fields defaulted
}
 
//4.根据指定的map初始化，根据指定的map的容量和默认容量共同决定初始化容量，使用默认负载因子
public HashMap(Map<? extends K, ? extends V> m) {
        this.loadFactor = DEFAULT_LOAD_FACTOR;
        putMapEntries(m, false);
}
```

##### 5.1.3.4 主要方法

**get方法**

```java
public V get(Object key) {
    Node<K,V> e;
    return (e = getNode(hash(key), key)) == null ? null : e.value;
}
 
final Node<K,V> getNode(int hash, Object key) {
    Node<K,V>[] tab; Node<K,V> first, e; int n; K k;
    // 1.对table进行校验：table不为空 && table长度大于0 && 
    // table索引位置(使用table.length - 1和hash值进行位与运算)的节点不为空
    if ((tab = table) != null && (n = tab.length) > 0 &&
        (first = tab[(n - 1) & hash]) != null) {
        // 2.检查first节点的hash值和key是否和入参的一样，如果一样则first即为目标节点，直接返回first节点
        if (first.hash == hash && // always check first node
            ((k = first.key) == key || (key != null && key.equals(k))))
            return first;
        // 3.如果first不是目标节点，并且first的next节点不为空则继续遍历
        if ((e = first.next) != null) {
            if (first instanceof TreeNode)
                // 4.如果是红黑树节点，则调用红黑树的查找目标节点方法getTreeNode
                return ((TreeNode<K,V>)first).getTreeNode(hash, key);
            do {
                // 5.执行链表节点的查找，向下遍历链表, 直至找到节点的key和入参的key相等时,返回该节点
                if (e.hash == hash &&
                    ((k = e.key) == key || (key != null && key.equals(k))))
                    return e;
            } while ((e = e.next) != null);
        }
    }
    // 6.找不到符合的返回空
    return null;
}
```

第4步：如果是红黑树节点，则调用红黑树的查找目标节点方法 getTreeNode，**见代码块1详解**。

```java
final TreeNode<K,V> getTreeNode(int h, Object k) {
    // 1.首先找到红黑树的根节点；2.使用根节点调用find方法
    return ((parent != null) ? root() : this).find(h, k, null);
}
```

find 方法如下：

```java
/**
 * 从调用此方法的节点开始查找, 通过hash值和key找到对应的节点
 * 此方法是红黑树节点的查找, 红黑树是特殊的自平衡二叉查找树
 * 平衡二叉查找树的特点：左节点<根节点<右节点
 */
final TreeNode<K,V> find(int h, Object k, Class<?> kc) {
    // 1.将p节点赋值为调用此方法的节点，即为红黑树根节点
    TreeNode<K,V> p = this;
    // 2.从p节点开始向下遍历
    do {
        int ph, dir; K pk;
        TreeNode<K,V> pl = p.left, pr = p.right, q;
        // 3.如果传入的hash值小于p节点的hash值，则往p节点的左边遍历
        if ((ph = p.hash) > h)
            p = pl;
        else if (ph < h) // 4.如果传入的hash值大于p节点的hash值，则往p节点的右边遍历
            p = pr;
        // 5.如果传入的hash值和key值等于p节点的hash值和key值,则p节点为目标节点,返回p节点
        else if ((pk = p.key) == k || (k != null && k.equals(pk)))
            return p;
        else if (pl == null)    // 6.p节点的左节点为空则将向右遍历
            p = pr;
        else if (pr == null)    // 7.p节点的右节点为空则向左遍历
            p = pl;
        // 8.将p节点与k进行比较
        else if ((kc != null ||
                  (kc = comparableClassFor(k)) != null) && // 8.1 kc不为空代表k实现了Comparable
                 (dir = compareComparables(kc, k, pk)) != 0)// 8.2 k<pk则dir<0, k>pk则dir>0
            // 8.3 k<pk则向左遍历(p赋值为p的左节点), 否则向右遍历
            p = (dir < 0) ? pl : pr;
        // 9.代码走到此处, 代表key所属类没有实现Comparable, 直接指定向p的右边遍历
        else if ((q = pr.find(h, k, kc)) != null) 
            return q;
        // 10.代码走到此处代表“pr.find(h, k, kc)”为空, 因此直接向左遍历
        else
            p = pl;
    } while (p != null);
    return null;
}
```

8.将 p 节点与 k 进行比较。如果传入的 key（即代码中的参数 k）所属的类实现了 Comparable 接口（kc 不为空，comparableClassFor 方法见代码块3详解），则将 k 跟 p 节点的 key 进行比较（kc 实现了 Comparable 接口，因此通过 kc 的比较方法进行比较），并将比较结果赋值给 dir，如果 dir<0 则代表 k<pk，则向 p 节点的左边遍历（pl）；否则，向 p 节点的右边遍历（pr）。

代码块3：comparableClassFor

```java
static Class<?> comparableClassFor(Object x) {
    // 1.判断x是否实现了Comparable接口
    if (x instanceof Comparable) {
        Class<?> c; Type[] ts, as; Type t; ParameterizedType p;
        // 2.校验x是否为String类型
        if ((c = x.getClass()) == String.class) // bypass checks
            return c;
        if ((ts = c.getGenericInterfaces()) != null) {
            // 3.遍历x实现的所有接口
            for (int i = 0; i < ts.length; ++i) {
                // 4.如果x实现了Comparable接口，则返回x的Class
                if (((t = ts[i]) instanceof ParameterizedType) &&
                    ((p = (ParameterizedType)t).getRawType() ==
                     Comparable.class) &&
                    (as = p.getActualTypeArguments()) != null &&
                    as.length == 1 && as[0] == c) // type arg is c
                    return c;
            }
        }
    }
    return null;
}
```

**put 方法**

```java
public V put(K key, V value) {
    return putVal(hash(key), key, value, false, true);
}
 
final V putVal(int hash, K key, V value, boolean onlyIfAbsent,
               boolean evict) {
    Node<K,V>[] tab; Node<K,V> p; int n, i;
    // 1.校验table是否为空或者length等于0，如果是则调用resize方法进行初始化
    if ((tab = table) == null || (n = tab.length) == 0)
        n = (tab = resize()).length;
    // 2.通过hash值计算索引位置，将该索引位置的头节点赋值给p，如果p为空则直接在该索引位置新增一个节点即可
    if ((p = tab[i = (n - 1) & hash]) == null)
        tab[i] = newNode(hash, key, value, null);
    else {
        // table表该索引位置不为空，则进行查找
        Node<K,V> e; K k;
        // 3.判断p节点的key和hash值是否跟传入的相等，如果相等, 则p节点即为要查找的目标节点，将p节点赋值给e节点
        if (p.hash == hash &&
            ((k = p.key) == key || (key != null && key.equals(k))))
            e = p;
        // 4.判断p节点是否为TreeNode, 如果是则调用红黑树的putTreeVal方法查找目标节点
        else if (p instanceof TreeNode)
            e = ((TreeNode<K,V>)p).putTreeVal(this, tab, hash, key, value);
        else {
            // 5.走到这代表p节点为普通链表节点，则调用普通的链表方法进行查找，使用binCount统计链表的节点数
            for (int binCount = 0; ; ++binCount) {
                // 6.如果p的next节点为空时，则代表找不到目标节点，则新增一个节点并插入链表尾部
                if ((e = p.next) == null) {
                    p.next = newNode(hash, key, value, null);
                    // 7.校验节点数是否超过8个，如果超过则调用treeifyBin方法将链表节点转为红黑树节点，
                    // 减一是因为循环是从p节点的下一个节点开始的
                    if (binCount >= TREEIFY_THRESHOLD - 1)
                        treeifyBin(tab, hash);
                    break;
                }
                // 8.如果e节点存在hash值和key值都与传入的相同，则e节点即为目标节点，跳出循环
                if (e.hash == hash &&
                    ((k = e.key) == key || (key != null && key.equals(k))))
                    break;
                p = e;  // 将p指向下一个节点
            }
        }
        // 9.如果e节点不为空，则代表目标节点存在，使用传入的value覆盖该节点的value，并返回oldValue
        if (e != null) {
            V oldValue = e.value;
            if (!onlyIfAbsent || oldValue == null)
                e.value = value;
            afterNodeAccess(e); // 用于LinkedHashMap
            return oldValue;
        }
    }
    ++modCount;
    // 10.如果插入节点后节点数超过阈值，则调用resize方法进行扩容
    if (++size > threshold)
        resize();
    afterNodeInsertion(evict);  // 用于LinkedHashMap
    return null;
}
```

**putTreeVal**

```jAVA
/**
 * 红黑树的put操作，红黑树插入会同时维护原来的链表属性, 即原来的next属性
 */
final TreeNode<K,V> putTreeVal(HashMap<K,V> map, Node<K,V>[] tab,
                               int h, K k, V v) {
    Class<?> kc = null;
    boolean searched = false;
    // 1.查找根节点, 索引位置的头节点并不一定为红黑树的根节点
    TreeNode<K,V> root = (parent != null) ? root() : this;
    // 2.将根节点赋值给p节点，开始进行查找
    for (TreeNode<K,V> p = root;;) {
        int dir, ph; K pk;
        // 3.如果传入的hash值小于p节点的hash值，将dir赋值为-1，代表向p的左边查找树
        if ((ph = p.hash) > h)
            dir = -1;
        // 4.如果传入的hash值大于p节点的hash值， 将dir赋值为1，代表向p的右边查找树
        else if (ph < h)
            dir = 1;
        // 5.如果传入的hash值和key值等于p节点的hash值和key值, 则p节点即为目标节点, 返回p节点
        else if ((pk = p.key) == k || (k != null && k.equals(pk)))
            return p;
        // 6.如果k所属的类没有实现Comparable接口 或者 k和p节点的key相等
        else if ((kc == null &&
                  (kc = comparableClassFor(k)) == null) ||
                 (dir = compareComparables(kc, k, pk)) == 0) {
            // 6.1 第一次符合条件, 从p节点的左节点和右节点分别调用find方法进行查找, 如果查找到目标节点则返回
            if (!searched) {
                TreeNode<K,V> q, ch;
                searched = true;
                if (((ch = p.left) != null &&
                     (q = ch.find(h, k, kc)) != null) ||
                    ((ch = p.right) != null &&
                     (q = ch.find(h, k, kc)) != null))
                    return q;
            }
            // 6.2 否则使用定义的一套规则来比较k和p节点的key的大小, 用来决定向左还是向右查找
            dir = tieBreakOrder(k, pk); // dir<0则代表k<pk，则向p左边查找；反之亦然
        }
 
        TreeNode<K,V> xp = p;   // xp赋值为x的父节点,中间变量,用于下面给x的父节点赋值
        // 7.dir<=0则向p左边查找,否则向p右边查找,如果为null,则代表该位置即为x的目标位置
        if ((p = (dir <= 0) ? p.left : p.right) == null) {
            // 走进来代表已经找到x的位置，只需将x放到该位置即可
            Node<K,V> xpn = xp.next;    // xp的next节点
            // 8.创建新的节点, 其中x的next节点为xpn, 即将x节点插入xp与xpn之间
            TreeNode<K,V> x = map.newTreeNode(h, k, v, xpn);
            // 9.调整x、xp、xpn之间的属性关系
            if (dir <= 0)   // 如果时dir <= 0, 则代表x节点为xp的左节点
                xp.left = x;
            else        // 如果时dir> 0, 则代表x节点为xp的右节点
                xp.right = x;
            xp.next = x;    // 将xp的next节点设置为x
            x.parent = x.prev = xp; // 将x的parent和prev节点设置为xp
            // 如果xpn不为空,则将xpn的prev节点设置为x节点,与上文的x节点的next节点对应
            if (xpn != null)
                ((TreeNode<K,V>)xpn).prev = x;
            // 10.进行红黑树的插入平衡调整
            moveRootToFront(tab, balanceInsertion(root, x));
            return null;
        }
    }
}
```

**treeifyBin**

```JAVA
/**
 * 将链表节点转为红黑树节点
 */
final void treeifyBin(Node<K,V>[] tab, int hash) {
    int n, index; Node<K,V> e;
    // 1.如果table为空或者table的长度小于64, 调用resize方法进行扩容
    if (tab == null || (n = tab.length) < MIN_TREEIFY_CAPACITY)
        resize();
    // 2.根据hash值计算索引值，将该索引位置的节点赋值给e，从e开始遍历该索引位置的链表
    else if ((e = tab[index = (n - 1) & hash]) != null) {
        TreeNode<K,V> hd = null, tl = null;
        do {
            // 3.将链表节点转红黑树节点
            TreeNode<K,V> p = replacementTreeNode(e, null);
            // 4.如果是第一次遍历，将头节点赋值给hd
            if (tl == null)	// tl为空代表为第一次循环
                hd = p;
            else {
                // 5.如果不是第一次遍历，则处理当前节点的prev属性和上一个节点的next属性
                p.prev = tl;    // 当前节点的prev属性设为上一个节点
                tl.next = p;    // 上一个节点的next属性设置为当前节点
            }
            // 6.将p节点赋值给tl，用于在下一次循环中作为上一个节点进行一些链表的关联操作（p.prev = tl 和 tl.next = p）
            tl = p;
        } while ((e = e.next) != null);
        // 7.将table该索引位置赋值为新转的TreeNode的头节点，如果该节点不为空，则以以头节点(hd)为根节点, 构建红黑树
        if ((tab[index] = hd) != null)
            hd.treeify(tab);
    }
}
```

**treeify**

```java
/**
 * 构建红黑树
 */
final void treeify(Node<K,V>[] tab) {
    TreeNode<K,V> root = null;
    // 1.将调用此方法的节点赋值给x，以x作为起点，开始进行遍历
    for (TreeNode<K,V> x = this, next; x != null; x = next) {
        next = (TreeNode<K,V>)x.next;   // next赋值为x的下个节点
        x.left = x.right = null;    // 将x的左右节点设置为空
        // 2.如果还没有根节点, 则将x设置为根节点
        if (root == null) {
            x.parent = null;    // 根节点没有父节点
            x.red = false;  // 根节点必须为黑色
            root = x;   // 将x设置为根节点
        }
        else {
            K k = x.key;	// k赋值为x的key
            int h = x.hash;	// h赋值为x的hash值
            Class<?> kc = null;
            // 3.如果当前节点x不是根节点, 则从根节点开始查找属于该节点的位置
            for (TreeNode<K,V> p = root;;) {
                int dir, ph;
                K pk = p.key;
                // 4.如果x节点的hash值小于p节点的hash值，则将dir赋值为-1, 代表向p的左边查找
                if ((ph = p.hash) > h)
                    dir = -1;
                // 5.如果x节点的hash值大于p节点的hash值，则将dir赋值为1, 代表向p的右边查找
                else if (ph < h)
                    dir = 1;
                // 6.走到这代表x的hash值和p的hash值相等，则比较key值
                else if ((kc == null && // 6.1 如果k没有实现Comparable接口 或者 x节点的key和p节点的key相等
                          (kc = comparableClassFor(k)) == null) ||
                         (dir = compareComparables(kc, k, pk)) == 0)
                    // 6.2 使用定义的一套规则来比较x节点和p节点的大小，用来决定向左还是向右查找
                    dir = tieBreakOrder(k, pk);
 
                TreeNode<K,V> xp = p;   // xp赋值为x的父节点,中间变量用于下面给x的父节点赋值
                // 7.dir<=0则向p左边查找,否则向p右边查找,如果为null,则代表该位置即为x的目标位置
                if ((p = (dir <= 0) ? p.left : p.right) == null) {
                    // 8.x和xp节点的属性设置
                    x.parent = xp;  // x的父节点即为最后一次遍历的p节点
                    if (dir <= 0)   // 如果时dir <= 0, 则代表x节点为父节点的左节点
                        xp.left = x;
                    else    // 如果时dir > 0, 则代表x节点为父节点的右节点
                        xp.right = x;
                    // 9.进行红黑树的插入平衡(通过左旋、右旋和改变节点颜色来保证当前树符合红黑树的要求)
                    root = balanceInsertion(root, x);
                    break;
                }
            }
        }
    }
    // 10.如果root节点不在table索引位置的头节点, 则将其调整为头节点
    moveRootToFront(tab, root);
}
```

**resize 方法**

```java
final Node<K,V>[] resize() {
    Node<K,V>[] oldTab = table;
    int oldCap = (oldTab == null) ? 0 : oldTab.length;
    int oldThr = threshold;
    int newCap, newThr = 0;
    // 1.老表的容量不为0，即老表不为空
    if (oldCap > 0) {
        // 1.1 判断老表的容量是否超过最大容量值：如果超过则将阈值设置为Integer.MAX_VALUE，并直接返回老表,
        // 此时oldCap * 2比Integer.MAX_VALUE大，因此无法进行重新分布，只是单纯的将阈值扩容到最大
        if (oldCap >= MAXIMUM_CAPACITY) {
            threshold = Integer.MAX_VALUE;
            return oldTab;
        }
        // 1.2 将newCap赋值为oldCap的2倍，如果newCap<最大容量并且oldCap>=16, 则将新阈值设置为原来的两倍
        else if ((newCap = oldCap << 1) < MAXIMUM_CAPACITY &&
                 oldCap >= DEFAULT_INITIAL_CAPACITY)
            newThr = oldThr << 1; // double threshold
    }
    // 2.如果老表的容量为0, 老表的阈值大于0, 是因为初始容量被放入阈值，则将新表的容量设置为老表的阈值
    else if (oldThr > 0)
        newCap = oldThr;
    else {
        // 3.老表的容量为0, 老表的阈值为0，这种情况是没有传初始容量的new方法创建的空表，将阈值和容量设置为默认值
        newCap = DEFAULT_INITIAL_CAPACITY;
        newThr = (int)(DEFAULT_LOAD_FACTOR * DEFAULT_INITIAL_CAPACITY);
    }
    // 4.如果新表的阈值为空, 则通过新的容量*负载因子获得阈值
    if (newThr == 0) {
        float ft = (float)newCap * loadFactor;
        newThr = (newCap < MAXIMUM_CAPACITY && ft < (float)MAXIMUM_CAPACITY ?
                  (int)ft : Integer.MAX_VALUE);
    }
    // 5.将当前阈值设置为刚计算出来的新的阈值，定义新表，容量为刚计算出来的新容量，将table设置为新定义的表。
    threshold = newThr;
    @SuppressWarnings({"rawtypes","unchecked"})
    Node<K,V>[] newTab = (Node<K,V>[])new Node[newCap];
    table = newTab;
    // 6.如果老表不为空，则需遍历所有节点，将节点赋值给新表
    if (oldTab != null) {
        for (int j = 0; j < oldCap; ++j) {
            Node<K,V> e;
            if ((e = oldTab[j]) != null) {  // 将索引值为j的老表头节点赋值给e
                oldTab[j] = null; // 将老表的节点设置为空, 以便垃圾收集器回收空间
                // 7.如果e.next为空, 则代表老表的该位置只有1个节点，计算新表的索引位置, 直接将该节点放在该位置
                if (e.next == null)
                    newTab[e.hash & (newCap - 1)] = e;
                // 8.如果是红黑树节点，则进行红黑树的重hash分布(跟链表的hash分布基本相同)
                else if (e instanceof TreeNode)
                    ((TreeNode<K,V>)e).split(this, newTab, j, oldCap);
                else { // preserve order
                    // 9.如果是普通的链表节点，则进行普通的重hash分布
                    Node<K,V> loHead = null, loTail = null; // 存储索引位置为:“原索引位置”的节点
                    Node<K,V> hiHead = null, hiTail = null; // 存储索引位置为:“原索引位置+oldCap”的节点
                    Node<K,V> next;
                    do {
                        next = e.next;
                        // 9.1 如果e的hash值与老表的容量进行与运算为0,则扩容后的索引位置跟老表的索引位置一样
                        if ((e.hash & oldCap) == 0) {
                            if (loTail == null) // 如果loTail为空, 代表该节点为第一个节点
                                loHead = e; // 则将loHead赋值为第一个节点
                            else
                                loTail.next = e;    // 否则将节点添加在loTail后面
                            loTail = e; // 并将loTail赋值为新增的节点
                        }
                        // 9.2 如果e的hash值与老表的容量进行与运算为非0,则扩容后的索引位置为:老表的索引位置＋oldCap
                        else {
                            if (hiTail == null) // 如果hiTail为空, 代表该节点为第一个节点
                                hiHead = e; // 则将hiHead赋值为第一个节点
                            else
                                hiTail.next = e;    // 否则将节点添加在hiTail后面
                            hiTail = e; // 并将hiTail赋值为新增的节点
                        }
                    } while ((e = next) != null);
                    // 10.如果loTail不为空（说明老表的数据有分布到新表上“原索引位置”的节点），则将最后一个节点
                    // 的next设为空，并将新表上索引位置为“原索引位置”的节点设置为对应的头节点
                    if (loTail != null) {
                        loTail.next = null;
                        newTab[j] = loHead;
                    }
                    // 11.如果hiTail不为空（说明老表的数据有分布到新表上“原索引+oldCap位置”的节点），则将最后
                    // 一个节点的next设为空，并将新表上索引位置为“原索引+oldCap”的节点设置为对应的头节点
                    if (hiTail != null) {
                        hiTail.next = null;
                        newTab[j + oldCap] = hiHead;
                    }
                }
            }
        }
    }
    // 12.返回新表
    return newTab;
}
```

**remove 方法**

```java
/**
 * 移除某个节点
 */
public V remove(Object key) {
    Node<K,V> e;
    return (e = removeNode(hash(key), key, null, false, true)) == null ?
        null : e.value;
}
 
final Node<K,V> removeNode(int hash, Object key, Object value,
                           boolean matchValue, boolean movable) {
    Node<K,V>[] tab; Node<K,V> p; int n, index;
    // 1.如果table不为空并且根据hash值计算出来的索引位置不为空, 将该位置的节点赋值给p
    if ((tab = table) != null && (n = tab.length) > 0 &&
        (p = tab[index = (n - 1) & hash]) != null) {
        Node<K,V> node = null, e; K k; V v;
        // 2.如果p的hash值和key都与入参的相同, 则p即为目标节点, 赋值给node
        if (p.hash == hash &&
            ((k = p.key) == key || (key != null && key.equals(k))))
            node = p;
        else if ((e = p.next) != null) {
            // 3.否则将p.next赋值给e，向下遍历节点
            // 3.1 如果p是TreeNode则调用红黑树的方法查找节点
            if (p instanceof TreeNode)
                node = ((TreeNode<K,V>)p).getTreeNode(hash, key);
            else {
                // 3.2 否则，进行普通链表节点的查找
                do {
                    // 当节点的hash值和key与传入的相同,则该节点即为目标节点
                    if (e.hash == hash &&
                        ((k = e.key) == key ||
                         (key != null && key.equals(k)))) {
                        node = e;	// 赋值给node, 并跳出循环
                        break;
                    }
                    p = e;  // p节点赋值为本次结束的e，在下一次循环中，e为p的next节点
                } while ((e = e.next) != null); // e指向下一个节点
            }
        }
        // 4.如果node不为空(即根据传入key和hash值查找到目标节点)，则进行移除操作
        if (node != null && (!matchValue || (v = node.value) == value ||
                             (value != null && value.equals(v)))) {
            // 4.1 如果是TreeNode则调用红黑树的移除方法
            if (node instanceof TreeNode)
                ((TreeNode<K,V>)node).removeTreeNode(this, tab, movable);
            // 4.2 如果node是该索引位置的头节点则直接将该索引位置的值赋值为node的next节点，
            // “node == p”只会出现在node是头节点的时候，如果node不是头节点，则node为p的next节点
            else if (node == p)
                tab[index] = node.next;
            // 4.3 否则将node的上一个节点的next属性设置为node的next节点,
            // 即将node节点移除, 将node的上下节点进行关联(链表的移除)
            else
                p.next = node.next;
            ++modCount;
            --size;
            afterNodeRemoval(node); // 供LinkedHashMap使用
            // 5.返回被移除的节点
            return node;
        }
    }
    return null;
}
```

#### 5.1.4 HashMap总结

1. HashMap 的底层是个 Node 数组（Node<K,V>[] table），在数组的具体索引位置，如果存在多个节点，则可能是以链表或红黑树的形式存在。
2. 增加、删除、查找键值对时，定位到哈希桶数组的位置是很关键的一步，源码中是通过下面3个操作来完成这一步：
   1. 拿到 key 的 hashCode 值；
   2. 将 hashCode 的高位参与运算，重新计算 hash 值；
   3. 将计算出来的 hash 值与 “table.length - 1” 进行 & 运算。
3. HashMap 的默认初始容量（capacity）是 16，capacity 必须为 2 的幂次方；默认负载因子（load factor）是 0.75；实际能存放的节点个数（threshold，即触发扩容的阈值）= capacity * load factor。
4. HashMap 在触发扩容后，阈值会变为原来的 2 倍，并且会对所有节点进行重 hash 分布，重 hash 分布后节点的新分布位置只可能有两个：“原索引位置” 或 “原索引+oldCap位置”。例如 capacity 为16，索引位置 5 的节点扩容后，只可能分布在新表 “索引位置5” 和 “索引位置21（5+16）”。
5. 导致 HashMap 扩容后，同一个索引位置的节点重 hash 最多分布在两个位置的根本原因是：1）table的长度始终为 2 的 n 次方；2）索引位置的计算方法为 “(table.length - 1) & hash”。HashMap 扩容是一个比较耗时的操作，定义 HashMap 时尽量给个接近的初始容量值。
6. HashMap 有 threshold 属性和 loadFactor 属性，但是没有 capacity 属性。初始化时，如果传了初始化容量值，该值是存在 threshold 变量，并且 Node 数组是在第一次 put 时才会进行初始化，初始化时会将此时的 threshold 值作为新表的 capacity 值，然后用 capacity 和 loadFactor 计算新表的真正 threshold 值。
7. **当同一个索引位置的节点在增加后大于8，并且此时数组的长度大于等于 64，则会触发链表节点（Node）转红黑树节点（TreeNode），**转成红黑树节点后，其实链表的结构还存在，通过 next 属性维持。链表节点转红黑树节点的具体方法为源码中的 treeifyBin 方法。而如果数组长度小于64，则不会触发链表转红黑树，而是会进行扩容。
8. 当同一个索引位置的节点在移除后达到 6 个时，并且该索引位置的节点为红黑树节点，会触发红黑树节点转链表节点。红黑树节点转链表节点的具体方法为源码中的 untreeify 方法。
9. HashMap 在 JDK 1.8 之后不再有死循环的问题，JDK 1.8 之前存在死循环的根本原因是在扩容后同一索引位置的节点顺序会反掉。
10. HashMap 是非线程安全的，在并发场景下使用 ConcurrentHashMap 来代替。

### 5.2 TreeMap

TreeMap 是一种基于红黑树实现的 Key-Value 结构,如果我们想要自定义一种元素之间的顺序，那么前面的HashMap都是无法实现的，而TreeMap 支持按键值进行升序访问，或者由传入的比较器（Comparator）来控制。

#### 5.2.1 TreeMap 类结构

![image-20210420151501648](https://gitee.com/Kunaly/picture-bed/raw/master/img/image-20210420151501648.png)



```java
public class TreeMap<K,V>
    extends AbstractMap<K,V>
    implements NavigableMap<K,V>, Cloneable, java.io.Serializable
```

TreeMap 继承AbstractMap， AbstractMap 提供了 Map 的基本实现。
TreeMap 实现了Cloneable接口，支持clone()方法，可以被克隆。
TreeMap 实现了Serializable接口，可以被序列化。
除此之外，我们还看到TreeMap 实现了NavigableMap 接口，而NavigableMap接口继承至SortedMap。
SortedMap 是一个扩展自 Map 的一个接口，对该接口的实现要保证所有的 Key 是完全有序的（也就是说可以比较的）。
这个顺序一般是指 Key 的自然序（实现 Comparable 接口）或在创建 SortedMap 时指定一个比较器（Comparator）。当我们元素迭代时，就可以按序访问其中的元素。

#### 5.2.2 TreeMap 属性值

```java
  //比较器，没有指定的话默认使用Key的自然序
  private final Comparator<? super K> comparator;

  //红黑树根节点
  private transient Entry<K,V> root;

  //树中节点的数量
  private transient int size = 0;

  //存储结构被 修改的次数
  private transient int modCount = 0;

  static final class Entry<K,V> implements Map.Entry<K,V> {
    K key; //键
    V value; //值
    Entry<K,V> left;  //左孩子
    Entry<K,V> right; //右孩子
    Entry<K,V> parent; //父节点
    boolean color = BLACK; //节点颜色
    .... //省略方法内容...
 }
```

TreeMap 是基于红黑树来实现的，排序时按照键的自然序（要求实现 Comparable 接口）或者提供一个 Comparator 用于排序。

#### 5.2.3 TreeMap 构造方法

1、无参构造

```java
public TreeMap() {
    comparator = null;
}
```

比较器为null,那么会使用key的比较器,也就意味着key必须实现Comparable 接口,否则在比较的时候就会出现异常，这个我们后面会看到。

2、指定比较器

```java
public TreeMap(Comparator<? super K> comparator) {
    this.comparator = comparator;
}
```

使用自定义的比较器，来比较key之间的大小关系。

3、通过非SortedMap集合构造

```java
public TreeMap(Map<? extends K, ? extends V> m) {
    comparator = null;
    putAll(m);
}
```

将map集合中的元素添加到TreeMap中，比较器为null.
4、通过SortedMap集合构造

```java
public TreeMap(SortedMap<K, ? extends V> m) {
    comparator = m.comparator();
    try {
        buildFromSorted(m.size(), m.entrySet().iterator(), null, null);
    } catch (java.io.IOException cannotHappen) {
    } catch (ClassNotFoundException cannotHappen) {
    }
}
```

通过SortedMap 集合构造，比较器是参数集合的比较器。

#### 5.2.4 TreeMap 主要方法

**get 方法**

```java
public V get(Object key) {
    //通过getEntry 获得节点
    Entry<K,V> p = getEntry(key);
    return (p==null ? null : p.value);
}
```

```java
final Entry<K,V> getEntry(Object key) {
    //如果比较器不为null,则使用比较器获取节点
    if (comparator != null)
        return getEntryUsingComparator(key);
    //如果比较器为null,同时key为NULL，则抛出异常    
    if (key == null)
        throw new NullPointerException();
    //获取key的比较器，因此如果key没有实现Comparable接口，则会发生异常  
    Comparable<? super K> k = (Comparable<? super K>) key;
    Entry<K,V> p = root;
    //从根节点开始遍历二叉树
    while (p != null) {
        int cmp = k.compareTo(p.key);
        //在左子树寻找
        if (cmp < 0)
            p = p.left;
        else if (cmp > 0) //在右子树寻找
            p = p.right;
        else
            return p; //相等，返回节点
    }
    return null;  //否则 没找到，返回null
}

```

```java
// 通过指定的比较器进行比较，实际上和上面是差不多的
final Entry<K,V> getEntryUsingComparator(Object key) {
    
    K k = (K) key;
    Comparator<? super K> cpr = comparator;
    if (cpr != null) {
        Entry<K,V> p = root;
        while (p != null) {
            int cmp = cpr.compare(k, p.key);
            if (cmp < 0)
                p = p.left;
            else if (cmp > 0)
                p = p.right;
            else
                return p;
        }
    }
    return null;
}
```

get 方法很简单，其实就是一颗搜索二叉树的遍历过程，如果查找的节点大于"根"节点，则在其"根"节点的右子树查找，如果小于"根"节点，则在其左子树查找，否则就是相当，返回"根"节点即可。
当指定了比较器时，使用指定的比较器来查找节点，否则通过key的比较器来查找，因此如果在没有指定比较器的情况下，同时key没有实现Comparable接口，则会抛出异常。

**put 方法**

TreeMap的添加方法，实际上就是红黑树的插入过程，因此这里需要红黑树相关知识。

```java
public V put(K key, V value) {
    Entry<K,V> t = root;
    //如果根节点为null,则直接赋值给根节点
    if (t == null) {
        compare(key, key); 
        //默认是黑色节点。
        root = new Entry<>(key, value, null);
        size = 1;
        modCount++;
        return null;
    }
    int cmp;
    Entry<K,V> parent;
    Comparator<? super K> cpr = comparator;
    // 如果比较器不为空，就是用指定的比较器来维护TreeMap的元素顺序
    if (cpr != null) {
         // 查找key要插入的位置
        do {
            parent = t;
            // 比较当前节点的key和新插入的key的大小
            cmp = cpr.compare(key, t.key);
            // 新插入的key小的话，则以当前节点的左孩子节点为新的比较节点
            if (cmp < 0) 
                t = t.left;
            // 新插入的key大的话，则以当前节点的右孩子节点为新的比较节点    
            else if (cmp > 0) 
                t = t.right;
           // 如果当前节点的key和新插入的key相等的话，则覆盖map的value，返回旧值     
            else
                return t.setValue(value);
        } while (t != null);
    }
    else {
        /**
         *如果比较器为空，则使用key作为比较器进行比较
	     *这里要求key不能为空，并且必须实现Comparable接口
	     */
        if (key == null)
            throw new NullPointerException();
        
        Comparable<? super K> k = (Comparable<? super K>) key;
        do {
            parent = t;
            cmp = k.compareTo(t.key);
            if (cmp < 0)
                t = t.left;
            else if (cmp > 0)
                t = t.right;
            else
                return t.setValue(value);
        } while (t != null);
    }
    //生成节点，指定其父节点为 parent
    Entry<K,V> e = new Entry<>(key, value, parent);
    // 如果新节点key的值小于父节点key的值，则插在父节点的左侧
    if (cmp < 0)
        parent.left = e;
    // 如果新节点key的值大于父节点key的值，则插在父节点的右侧    
    else
        parent.right = e;
    // 插入新的节点后，为了保持红黑树平衡，对红黑树进行调整
    fixAfterInsertion(e);
    size++;
    modCount++;
    return null;
}
```

**remove 方法**

删除操作首先需要做的也是搜索二叉树的删除操作，删除操作会删除对应的节点，如果是叶子节点就直接删除，如果是非叶子节点，会用对应的中序遍历的后继节点来顶替要删除节点的位置。删除后就需要做删除修复操作，使的树符合红黑树的定义。

第一步：将红黑树当作一颗二叉查找树，将节点删除。
① 被删除节点为叶节点。那么，直接将该节点删除就OK了。
② 被删除节点只有一个孩子。那么，用孩子节点的代替该节点即可。
③ 被删除节点有两个孩子。那么，先找出它的后继节点；然后把“它的后继节点的内容”复制给“该节点的内容”；之后，删除“它的中序后继节点”，其中序后继节点不可能存在有两个孩子节点的情况，因此就转换成了①，②的情况了。

第二步：通过”旋转和重新着色”等一系列来修正该树，使之重新成为一棵红黑树。

```java
public V remove(Object key) {
    //通过getEntry 得到节点
    Entry<K,V> p = getEntry(key);
    if (p == null)
        return null;
    V oldValue = p.value;
    //删除节点p
    deleteEntry(p);
    // 返回值
    return oldValue;
}
```

deleteEntry 是删除节点操作，这个就是在搜索二叉树的删除节点.

```java
/**
 * Delete node p, and then rebalance the tree.
 */
private void deleteEntry(Entry<K,V> p) {
    modCount++;
    size--;

    // If strictly internal, copy successor's element to p and then make p
    // point to successor.
    //如果存在左右孩子
    if (p.left != null && p.right != null) {
        //后继替代节点
        Entry<K,V> s = successor(p);
        p.key = s.key;
        //将替代节点的值，赋值给p
        p.value = s.value;
        // 转移成 删除s，s要么是叶子节点，要么只有一个孩子，不会出现两个孩子的情况
        p = s;
       } // p has 2 children

       // Start fixup at replacement node, if it exists.
       //得到其左孩子或者右孩子，如果没孩子则为null
       Entry<K,V> replacement = (p.left != null ? p.left : p.right);
       
       //replacement 为null,则现在的p是叶子节点
       if (replacement != null) {
           // Link replacement to parent
            // 将replacement的父节点设置为p的父节点
           replacement.parent = p.parent;
           //p的parent为null,则说明p为根节点
           if (p.parent == null)
               //将根设置为replacement，删除了节点p
               root = replacement;
           // 如果替代节点p是其父节点的左孩子，则将replacement设置为其父节点的左孩子
           else if (p == p.parent.left)
               p.parent.left  = replacement;
           // 如果替代节点p是其父节点的左孩子，则将replacement设置为其父节点的右孩子    
           else
               p.parent.right = replacement;

           // Null out links so they are OK to use by fixAfterDeletion.
            // 将替代节点p的left、right、parent的指针都指向空(从树中移除)，使得gc可以回收
           p.left = p.right = p.parent = null;

           // Fix replacement
           // 如果替代节点p的颜色是黑色，则需要调整红黑树以保持其平衡
           if (p.color == BLACK)
               fixAfterDeletion(replacement); 
       } else if (p.parent == null) { // return if we are the only node.
           root = null; // 只有一个节点，且删除的就是根节点，删除后root置null
       } else { //  No children. Use self as phantom replacement and unlink.
		   //替代节点p 是叶子节点，且不是根节点
		   
		   // 如果p的颜色是黑色，则调整红黑树（先调整，后删除，因为还需要利用其引用关系查找父节点或者兄弟节点）
           if (p.color == BLACK)
               fixAfterDeletion(p);
               
           // 下面是删除替代节点p
           if (p.parent != null) {
               // 重新设置p的父节点的孩子指针
               if (p == p.parent.left)
                   p.parent.left = null;
               else if (p == p.parent.right)
                   p.parent.right = null;
               // 解除p对p父节点的引用    
               p.parent = null;
           }
       }
   }
```

#### 5.2.5 TreeMap 总结

TreeMap 是一种基于红黑树实现的 Key-Value 结构，TreeMap 支持按键值进行升序访问，或者由传入的比较器（Comparator）来控制。当指定了比较器时，使用指定的比较器来查找节点，否则通过key的比较器来查找，因此如果在没有指定比较器的情况下，同时key没有实现Comparable接口，则会抛出异常。
TreeMap 实现了NavigableMap 接口，而NavigableMap接口继承至SortedMap。
SortedMap 是一个扩展自 Map 的一个接口，对该接口的实现要保证所有的 Key 是完全有序的（也就是说可以比较的）。
这个顺序一般是指 Key 的自然序（实现 Comparable 接口）或在创建 SortedMap 时指定一个比较器（Comparator）。当我们元素迭代时，就可以按序访问其中的元素。NavigableMap 是 JDK 1.6 之后新增的接口，扩展了 SortedMap 接口，提供了一些导航方法。
TreeMap 是非线程安全的，在前面对数据结构的操作中都没有进行同步操作。
分析TreeMap主要是分析红黑树，因此需要对红黑树有一定的认识，这样才好理解TreeMap。

### 5.3 HashTable

#### 5.3.1 HashTable 类结构

![image-20210420154227803](https://gitee.com/Kunaly/picture-bed/raw/master/img/image-20210420154227803.png)

```java
public class Hashtable<K,V>
    extends Dictionary<K,V>
    implements Map<K,V>, Cloneable, java.io.Serializable 
```

1）Hashtable继承于Dictionary抽象类，Dictionary中定义了对于容器操作的多种抽象方法。
2）实现Map接口，Hashtable实现了Map接口中定义的方法,具体的方法将在后文中分析。
3）实现Cloneable接口。
4）实现Serializable接口，可序列化。

#### 5.3.2 HashTable 属性值

```java
// 保存key-value的数组,支持泛型 
// Entry同样采用链表解决冲突，每一个Entry本质上是一个单向链表    
private transient Entry<?,?>[] table;
   
// Entry中键值对的数量    
private transient int count;    
   
// 阈值，用于判断是否需要调整Entry的容量
private int threshold;    
   
// 负载因子，当元素个数count大于总容量 * 负载因子时，扩容
private float loadFactor;    
   
// Entry被改变的次数，用于fail-fast机制的实现    
private transient int modCount = 0;
```
#### 5.3.3 HashTable 构造方法

1、无参构造

```java
//无参构造方法
public Hashtable() {
    //默认容量大小为11，负载因子设置为0.75
    this(11, 0.75f);
}
```
2、初始化容量大小为initialCapacity

```java
//带有初始化容量大小的构造方法
public Hashtable(int initialCapacity) {
    this(initialCapacity, 0.75f);
}
```
3、初始化容量为initialCapacity，负载因子为 loadFactor

```java
    public Hashtable(int initialCapacity, float loadFactor) {
    
        //检查参数的合法性
        if (initialCapacity < 0)
            throw new IllegalArgumentException("Illegal Capacity: "+
                                               initialCapacity);
        if (loadFactor <= 0 || Float.isNaN(loadFactor))
            throw new IllegalArgumentException("Illegal Load: "+loadFactor);
 
        //如果设置初始容量为0，则默认修改为1
        if (initialCapacity==0)
            initialCapacity = 1;
        //设置负载因子
        this.loadFactor = loadFactor;
        
        //根据设置的初始化容量创建数组
        table = new Entry<?,?>[initialCapacity];
 
      
        //计算阈值，取初始化容量与可分配的最大容量中的最小值。
        threshold = (int)Math.min(initialCapacity, MAX_ARRAY_SIZE + 1);
    }
```

4、使用Map集合初始化

```java
    //使用Map集合初始化
    public Hashtable(Map<? extends K, ? extends V> t) {
        // 若集合t元素大于5，则初始化容量为集合t中元素数目的2倍
        // 否则初始化容量为11
        // 负载因子设置为0.75
        this(Math.max(2*t.size(), 11), 0.75f);
        //将集合t中元素全部存储
        putAll(t);
    }
    
 
    public synchronized void putAll(Map<? extends K, ? extends V> t) {
        // for循环遍历集合t，将t中元素存储到this集合中
        for (Map.Entry<? extends K, ? extends V> e : t.entrySet())
            //将键值对添加至集合中
            put(e.getKey(), e.getValue());
    }
```

#### 5.3.4 HashTable 主要方法

HashTable API ：https://www.runoob.com/manual/jdk11api/java.base/java/util/Hashtable.html

| 变量和类型            | 方法                                                         | 描述                                                         |
| :-------------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| `void`                | `clear()`                                                    | 清除此哈希表，使其不包含任何键。                             |
| `Object`              | `clone()`                                                    | 创建此哈希表的浅表副本。                                     |
| `V`                   | `compute(K key, BiFunction<? super K,? super V,? extends V> remappingFunction)` | 尝试计算指定键及其当前映射值的映射（如果没有当前映射， `null` ）。 |
| `V`                   | `computeIfAbsent(K key, Function<? super K,? extends V> mappingFunction)` | 如果指定的键尚未与值关联（或映射到 `null` ），则尝试使用给定的映射函数计算其值并将其输入此映射，除非 `null` 。 |
| `V`                   | `computeIfPresent(K key, BiFunction<? super K,? super V,? extends V> remappingFunction)` | 如果指定键的值存在且为非null，则尝试在给定键及其当前映射值的情况下计算新映射。 |
| `boolean`             | `contains(Object value)`                                     | 测试某些键是否映射到此哈希表中的指定值。                     |
| `boolean`             | `containsKey(Object key)`                                    | 测试指定的对象是否是此哈希表中的键。                         |
| `boolean`             | `containsValue(Object value)`                                | 如果此哈希表将一个或多个键映射到此值，则返回true。           |
| `Enumeration<V>`      | `elements()`                                                 | 返回此哈希表中值的枚举。                                     |
| `Set<Map.Entry<K,V>>` | `entrySet()`                                                 | 返回此映射中包含的映射的[`Set`](https://www.runoob.com/manual/jdk11api/java.base/java/util/Set.html)视图。 |
| `boolean`             | `equals(Object o)`                                           | 根据Map接口中的定义，将指定的Object与此Map进行相等性比较。   |
| `V`                   | `get(Object key)`                                            | 返回指定键映射到的值，如果此映射不包含键的映射，则返回 `null` 。 |
| `int`                 | `hashCode()`                                                 | 根据Map接口中的定义返回此Map的哈希码值。                     |
| `boolean`             | `isEmpty()`                                                  | 测试此哈希表是否将键映射到值。                               |
| `Enumeration<K>`      | `keys()`                                                     | 返回此哈希表中键的枚举。                                     |
| `Set<K>`              | `keySet()`                                                   | 返回此映射中包含的键的[`Set`](https://www.runoob.com/manual/jdk11api/java.base/java/util/Set.html)视图。 |
| `V`                   | `merge(K key, V value, BiFunction<? super V,? super V,? extends V> remappingFunction)` | 如果指定的键尚未与值关联或与null关联，则将其与给定的非空值关联。 |
| `V`                   | `put(K key, V value)`                                        | 将指定的 `key`映射到此哈希表中的指定 `value` 。              |
| `void`                | `putAll(Map<? extends K,? extends V> t)`                     | 将指定映射中的所有映射复制到此哈希表。                       |
| `protected void`      | `rehash()`                                                   | 增加此哈希表的容量并在内部重新组织，以便更有效地容纳和访问其条目。 |
| `V`                   | `remove(Object key)`                                         | 从此哈希表中删除键（及其对应的值）。                         |
| `int`                 | `size()`                                                     | 返回此哈希表中的键数。                                       |
| `String`              | `toString()`                                                 | 以一组条目的形式返回此 `Hashtable`对象的字符串表示形式，用大括号括起，并用ASCII字符“ `, ` ”（逗号和空格）分隔。 |
| `Collection<V>`       | `values()`                                                   | 返回此映射中包含的值的[`Collection`](https://www.runoob.com/manual/jdk11api/java.base/java/util/Collection.html)视图。 |

**get 方法**

```java
    public synchronized V get(Object key) {
        
        Entry<?,?> tab[] = table;
        //得到key的hashcode
        int hash = key.hashCode();
        //根据hashcode计算索引值
        int index = (hash & 0x7FFFFFFF) % tab.length;
        //根据index找到key对应Entry链表，遍历链表找到哈希值与键值均与key相同的元素
        for (Entry<?,?> e = tab[index] ; e != null ; e = e.next) {
            if ((e.hash == hash) && e.key.equals(key)) {
                return (V)e.value;
            }
        }
        // 若没有找到，则返回null
        return null;
    }
```

**put 方法**

```java
    public synchronized V put(K key, V value) {
    
        // 检验数据值的合法性
        if (value == null) {
            throw new NullPointerException();
        }
 
        Entry<?,?> tab[] = table;
        //根据键值获取索引index
        int hash = key.hashCode();
        int index = (hash & 0x7FFFFFFF) % tab.length;
        //采用for循环方式解决哈希冲突，如果出现冲突则放在链表末尾。
        @SuppressWarnings("unchecked")
        Entry<K,V> entry = (Entry<K,V>)tab[index];
        for(; entry != null ; entry = entry.next) {
             //当前键值key已存在，更新key的映射值value，并返回旧值
            if ((entry.hash == hash) && entry.key.equals(key)) {
                V old = entry.value;
                entry.value = value;
                return old;
            }
        }
 
        //若没有找到重复键值key，则将key和value添加链表末尾
        addEntry(hash, key, value, index);
        return null;
    }
    
    //添加元素
    private void addEntry(int hash, K key, V value, int index) {
    
    
        modCount++;
 
        Entry<?,?> tab[] = table;
        
        //判断当前数目是否超过阈值
        if (count >= threshold) {
            // 数目超过阈值，扩容
            rehash();
 
            //更新扩容后的数组信息
            tab = table;
            hash = key.hashCode();
            index = (hash & 0x7FFFFFFF) % tab.length;
        }
 
        // 没有超过阈值，则添加至数组中
        @SuppressWarnings("unchecked")
        Entry<K,V> e = (Entry<K,V>) tab[index];
        tab[index] = new Entry<>(hash, key, value, e);
        
        //增加元素数目
        count++;
    }
    
    //扩容方法
    protected void rehash() {
     
        //获取旧数组大小
        int oldCapacity = table.length;
        Entry<?,?>[] oldMap = table;
 
        // 创建新容量大小的Entry数组，数组容量大小为原数组的2倍+1  
        int newCapacity = (oldCapacity << 1) + 1;
        if (newCapacity - MAX_ARRAY_SIZE > 0) {
            if (oldCapacity == MAX_ARRAY_SIZE)
                // Keep running with MAX_ARRAY_SIZE buckets
                return;
            newCapacity = MAX_ARRAY_SIZE;
        }
       Entry<?,?>[] newMap = new Entry<?,?>[newCapacity];
 
        modCount++;
        
        //重新计算阈值
        threshold = (int)Math.min(newCapacity * loadFactor, MAX_ARRAY_SIZE + 1);
        table = newMap;
 
        //将原数组中元素拷贝至新数组
       for (int i = oldCapacity ; i-- > 0 ;) {
            for (Entry<K,V> old = (Entry<K,V>)oldMap[i] ; old != null ; ) {
                Entry<K,V> e = old;
                old = old.next;
 
                int index = (e.hash & 0x7FFFFFFF) % newCapacity;
                e.next = (Entry<K,V>)newMap[index];
                newMap[index] = e;
            }
        }
    }
```

**contains 方法**

```java
    //判断是否含有value
    public boolean containsValue(Object value) {
        return contains(value);
    }
    
    public synchronized boolean contains(Object value) {
    
        //检查参数的合法性
        if (value == null) {
            throw new NullPointerException();
        }
 
        // 双重for循环，外循环遍历数组，内循环遍历链表
        Entry<?,?> tab[] = table;
        for (int i = tab.length ; i-- > 0 ;) {
            for (Entry<?,?> e = tab[i] ; e != null ; e = e.next) {
                if (e.value.equals(value)) {
                    return true;
                }
            }
        }
        return false;
    }
    
    // 判断是否包含键值key
   public synchronized boolean containsKey(Object key) {
        Entry<?,?> tab[] = table;
        int hash = key.hashCode();
        int index = (hash & 0x7FFFFFFF) % tab.length;
        // index定位数组位置，for遍历链表查找元素
        for (Entry<?,?> e = tab[index] ; e != null ; e = e.next) {
            if ((e.hash == hash) && e.key.equals(key)) {
                return true;
            }
        }
        return false;
    }
```

**remove 方法**

```java
//根据键值删除元素，返回被删除元素值
public synchronized V remove(Object key) {
        Entry<?,?> tab[] = table;
        int hash = key.hashCode();
        int index = (hash & 0x7FFFFFFF) % tab.length;
        @SuppressWarnings("unchecked")
        Entry<K,V> e = (Entry<K,V>)tab[index];
         //for遍历链表查找元素
        for(Entry<K,V> prev = null ; e != null ; prev = e, e = e.next) {
            //查找到元素进行链表的节点删除操作
            if ((e.hash == hash) && e.key.equals(key)) {
                modCount++;
                if (prev != null) {
                    prev.next = e.next;
                } else {
                    tab[index] = e.next;
                }
                count--;
                V oldValue = e.value;
                e.value = null;
                return oldValue;
            }
        }
        return null;
    }
```

#### 5.3.5 HashTable 总结

Hashtable是一个散列表，它存储的内容是键值对(key-value)映射。

Hashtable不允许null对象。

Hashtable中的方法使用了synchronized关键字修饰，因此Hashtable是线程安全的。



### 5.4 HashMap 和 HashTable 的区别

1. HashMap 允许 key 和 value 为 null，Hashtable 不允许。
2. HashMap 的默认初始容量为 16，Hashtable 为 11。
3. HashMap 的扩容为原来的 2 倍，Hashtable 的扩容为原来的 2 倍加 1。
4. HashMap 是非线程安全的，Hashtable是线程安全的。（如果你要保证线程安全的话就使⽤ ConcurrentHashMap）
5. HashMap 的 hash 值重新计算过，Hashtable 直接使用 hashCode。
6. HashMap 去掉了 Hashtable 中的 contains 方法。
7. HashMap 继承自 AbstractMap 类，Hashtable 继承自 Dictionary 类。



## 6. 补充内容

### 6.1 Iterator (迭代器)

Java Iterator（迭代器）不是一个集合，它是一种用于访问集合的方法，可用于迭代 ArrayList和 HashSet等集合。

Iterator 基本操作：

it.next() 会返回迭代器的下一个元素，并且更新迭代器的状态。

it.hasNext() 用于检测集合中是否还有元素。

it.remove() 将迭代器返回的元素删除。

示例：

```java
import java.util.ArrayList;
import java.util.Iterator;

public class IteratorTest {
    public static void main(String[] args) {
        ArrayList<Integer> numbers = new ArrayList<Integer>();
        numbers.add(12);
        numbers.add(8);
        numbers.add(2);
        numbers.add(23);
        Iterator<Integer> it = numbers.iterator();
        while(it.hasNext()) {
            Integer i = it.next();
            System.out.println(i);
            if(i < 10) {  
                it.remove();  // 删除小于 10 的元素
            }
        }
        System.out.println(numbers);
    }
}
```

### 6.2 Comparable 和 Comparator

#### 6.2.1 Comparable 简介

Comparable是排序接口。若一个类实现了Comparable接口，就意味着该类支持排序。实现了Comparable接口的类的对象的列表或数组可以通过Collections.sort或Arrays.sort进行自动排序。

此外，实现此接口的对象可以用作有序映射中的键或有序集合中的集合，无需指定比较器。该接口定义如下：

```java
package java.lang;
import java.util.*;
public interface Comparable<T> 
{
    public int compareTo(T o);
}
```

T表示可以与此对象进行比较的那些对象的类型。

此接口只有一个方法compare，比较此对象与指定对象的顺序，如果该对象小于、等于或大于指定对象，则分别返回负整数、零或正整数。

现在我们假设一个Person类，代码如下：

```java
public class Person
{
    String name;
    int age;
    public Person(String name, int age)
    {
        super();
        this.name = name;
        this.age = age;
    }
    public String getName()
    {
        return name;
    }　　
    public int getAge()
    {
        return age;
    }
}
```

　现在有两个Person类的对象，我们如何来比较二者的大小呢？我们可以通过让Person实现Comparable接口：

```java
import java.util.Arrays;

public class Person implements Comparable<Person>
{
    String name;
    int age;
    public Person(String name, int age)
    {
        super();
        this.name = name;
        this.age = age;
    }
    public String getName()
    {
        return name;
    }
    public int getAge()
    {
        return age;
    }
    @Override
    public int compareTo(Person p)
    {
        return this.age-p.getAge();
    }
    public static void main(String[] args)
    {
        Person[] people=new Person[]{new Person("张三", 20),new Person("李四", 10)};
        System.out.println("排序前");
        for (Person person : people)
        {
            System.out.print(person.getName()+":"+person.getAge());
        }
        Arrays.sort(people);
        System.out.println("\n排序后");
        for (Person person : people)
        {
            System.out.print(person.getName()+":"+person.getAge());
        }
    }
}
```

输出结果：

```java
排序前
张三:20李四:10
排序后
李四:10张三:20
```

#### 6.2.2 Comparator 简介

Comparator是比较接口，我们如果需要控制某个类的次序，而该类本身不支持排序(即没有实现Comparable接口)，那么我们就可以建立一个“该类的比较器”来进行排序，这个“比较器”只需要实现Comparator接口即可。也就是说，我们可以通过实现Comparator来新建一个比较器，然后通过这个比较器对类进行排序。该接口定义如下：

```java
package java.util;
public interface Comparator<T>
 {
    int compare(T o1, T o2);
    boolean equals(Object obj);
 }
```

**注意：**

1、若一个类要实现Comparator接口：它一定要实现compare(T o1, T o2) 函数，但可以不实现 equals(Object obj) 函数。

2、int compare(T o1, T o2) 是“比较o1和o2的大小”。返回“负数”，意味着“o1比o2小”；返回“零”，意味着“o1等于o2”；返回“正数”，意味着“o1大于o2”。

现在假如上面的Person类没有实现Comparable接口，该如何比较大小呢？我们可以新建一个类，让其实现Comparator接口，从而构造一个“比较器"。

```java
public class PersonCompartor implements Comparator<Person>
{
    @Override
    public int compare(Person o1, Person o2)
    {
        return o1.getAge()-o2.getAge();
    }
}
```

现在我们就可以利用这个比较器来对其进行排序：

```java
public class Person
{
    String name;
    int age;
    public Person(String name, int age)
    {
        super();
        this.name = name;
        this.age = age;
    }
    public String getName()
    {
        return name;
    }
    public int getAge()
    {
        return age;
    }
    public static void main(String[] args)
    {
        Person[] people=new Person[]{new Person("张三", 20),new Person("李四", 10)};
        System.out.println("排序前");
        for (Person person : people)
        {
            System.out.print(person.getName()+":"+person.getAge());
        }
        Arrays.sort(people,new PersonCompartor());
        System.out.println("\n排序后");
        for (Person person : people)
        {
            System.out.print(person.getName()+":"+person.getAge());
        }
    }
}
```

#### 6.2.3 Comparable和Comparator区别比较

Comparable是排序接口，若一个类实现了Comparable接口，就意味着“该类支持排序”。而Comparator是比较器，我们若需要控制某个类的次序，可以建立一个“该类的比较器”来进行排序。

Comparable相当于“内部比较器”，而Comparator相当于“外部比较器”。

两种方法各有优劣， 用Comparable 简单， 只要实现Comparable 接口的对象直接就成为一个可以比较的对象，但是需要修改源代码。 用Comparator 的好处是不需要修改源代码， 而是另外实现一个比较器， 当某个自定义的对象需要作比较的时候，把比较器和对象一起传递过去就可以比大小了， 并且在Comparator 里面用户可以自己实现复杂的可以通用的逻辑，使其可以匹配一些比较简单的对象，那样就可以节省很多重复劳动了。

## 📚  References

- JDK1.8 源码
- 菜鸟教程 JAVA

