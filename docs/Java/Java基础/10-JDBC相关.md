# JDBC

## 1. JDBC 概述

[本文相关代码](Java/Java基础/Codes/JDBC_Demo1.zip)

### 什么是 JDBC ?

JDBC： Java DataBase Connectivity（java数据库连接）
它是sun公司提供的一套java应用程序访问数据库的技术或规范。是一种用于执行SQL语句的Java API，它统一和规范了应用程序与数据库的连接、执行SQL语句，并到得到返回结果等各类操作，可以为多种关系数据库提供统一访问，它由一组用Java语言编写的类和接口组成。

**JDBC定义了一些接口**

- 驱动管理 DriverManager
- 连接接口 Connection DatabasemetaData
- 语句对象接口 Statement PreparedStatement CallableStatement
- 结果集接口 ResultSet ResultMetaData

### JDBC工作原理

JDBC只定义接口，具体实现由各个数据厂商负责。程序使用时只需要调用接口，实际调用的是底层数据库厂商的实现部分。

![image-20210430113032962](https://gitee.com/Kunaly/picture-bed/raw/master/img/image-20210430113032962.png)

### JDBC 相关接口

#### Driver接口及驱动类加载

要使用JDBC接口，需要先将对应数据库的实现部分(驱动)加载进来
mysql:

```java
// MySQL 8.0 以下版本 - JDBC 驱动名及数据库 URL
static final String JDBC_DRIVER = "com.mysql.jdbc.Driver";  
static final String URL = "jdbc:mysql://localhost:3306/test";
 
// MySQL 8.0 以上版本 - JDBC 驱动名及数据库 URL
//static final String JDBC_DRIVER = "com.mysql.cj.jdbc.Driver";  
//static final String URL = "jdbc:mysql://localhost:3306/test?useUnicode=true&characterEncoding=utf8&zeroDateTimeBehavior=CONVERT_TO_NULL&useSSL=false&serverTimezone=Asia/Shanghai";
// 注册 JDBC 驱动
Class.forName(JDBC_DRIVER);
```

#### Connection接口

Connection接口负责应用程序对数据库的连接，在加载驱动之后，使用url、username、password三个参数，创建到具体数据库的连接。

```java
Class.forName("com.mysql.jdbc.Driver");
Connection conn = DriverManager.getConnection("url","username","password");
```

```java
1.createStatement()：创建数据库连接
2.prepareStatement(String sql):创建预处理语句
3.prepareCall(String sql):创建可调用语句
4.getAutoCommit():获取自动提交的模式
5.setAutoCommit():设置自动提交的模式
6.commit():提交所执行的SQL语句
7.rollback():回滚所执行的SQL语句
8.getMetaData():获取一个DatabaseMetaData对象，该对象包含了有关数据库的基本信息
9.close():关闭数据库连接
10.isClose()：判断数据库连接是否超时或被显示关闭
```

#### Statement接口

Statement接口用来处理发送到数据库的SQL语句对象，通过Connection对象创建。主要有三个常用方法：

```java
Statement stmt = conn.createStatement();
//execute方法，如果执行的sql是查询语句且有结果集则返回true，如果是非查询语句或者没有结果集，返回false
boolean flag = stmt.execute(sql);
//执行查询语句，返回结果集
ResultSet rs = stmt.executeQuery(sql);
//执行DML语句，返回影响的记录数
int flag = stmt.executeUpdate(sql);
```

```java
1.execute(String sql):执行SQL语句，如果返回值是结果集则为true,否则为false
2.executeQuery(String sql):执行SQL语句，返回值为ResultSet
3.executeUpdate(String sql):执行SQL语句，返回值为所影响的行数
4.addBatch(String sql):向当前Statement对象的命令列表中添加新的批处理SQL语句
5.clearBatch():清空当前Statement对象的命令列表
6.executeBatch()：执行当前Statement对象的批处理语句，返回值为每个语句所影响的函数数组
7.getConnection():返回创建了该Statement对象的Connection对象
8.getQueryTimeout():获取等待处理结果的时间
9.setQueryTimeout():设置等待处理结果的时间
```

#### ResultSet接口

执行查询`SQL`语句后返回的结果集，由`ResultSet`接口接收。
常用处理方式：遍历/判断是否由结果。

```java
String sql = "select * from table";
ResultSet rs = stmt.executeQuery(sql);
while(rs.next()){
    System.out.println(rs.getInt("age")+rs.getString("name"));
}
```

查询的结果存放在ResultSet对象的一系列行中，指针的最初位置在行首，使用next()方法用来在行间移动，getXXX()方法用来取得字段的内容。

```java
1.first()/beforeFirst():将游标移动到ResultSet中第一条记录(的前面)
2.last()/afterLast():将游标移动到ResultSet中最后一条记录(的后面)
3.absolute(int column):将游标移动到相对于第一行的指定行，负数则为相对于最后一条记录
4.relative(int rows):将游标移动到相对于当前行的第几行,正为向下，负为向上
5.next():将游标下移一行
6.previous():将游标上移一行
7.insertRow():向当前ResultSet和数据库中被插入行处插入一条记录
8.deleteRow():将当前ResultSet中的当前行和数据库中对应的记录删除
9.updateRow():用当前ResultSet中已更新的记录更新数据库中对应的记录
10.cancelUpdate():取消当前对ResultSet和数据库中所做的操作
11.findColumn(String columnName):返回当前ResultSet中与指定列名对应的索引
12.getRow():返回ResultSet中的当前行号
13.refreshRow():更新当前ResultSet中的所有记录
14.getMetaData():返回描述ResultSet的ResultSetMetaData对象
15.isAfterLast(): 是否到了结尾
16.isBeforeFirst(): 是否到了开头
17.isFirst():是否第一条记录   
18.isLast(): 是否最后一条记录
19.wasNull():检查列值是否为NULL值，如果列的类型为基本类型，且数据库中的值为0，那么这项检查就很重要。由于数据库NULL也返回0，所以0值和数据库的NULL不能区分。如果列的类型为对象，可以简单地将返回值与null比较  
20.close():关闭当前ResultSet
```



### JDBC 编程

1. 新建项目，下载需要的JDBC驱动包 mysql-connector-java-8.0.21.jar

   MySQL的驱动下载地址：http://dev.mysql.com/downloads/。

2. 在项目下新建libs文件夹，将jar包复制到libs目录下。

   右键`mysql-connector-java-8.0.21.jar`, 选择 Add as Library...添加为库。

   注意：如果是Dynamic Web Project（动态的web项目）话，则是把驱动jar放到WebRoot目录中的WEB-INF目录中的lib目录下即可

#### JDBC使用的简单步骤

1. 加载驱动，建立连接

   加载驱动：把驱动类加载到内存
   注册驱动：把驱动类的对象交给DriverManager管理，用于后面创建连接等使用。
   第一种方式：`DriverManager.registerDriver(new Driver());`//不建议使用 

   第二种方式：`Class.forName(“com.mysql.jdbc.Driver”);`//通过反射，加载与注册驱动类，解耦合（不直接依赖）

2. 创建语句对象

3. 执行SQL语句

4. 处理结果集

5. 关闭连接

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;
import java.sql.Statement;

/**
 * 此类用于演示JDBC使用的简单步骤
 * 前提：
 * ①新建文件夹libs,将mysql-connector-java-8.0.21.jar复制到项目的libs目录
 * ②右击mysql-connector-java-8.0.21.jar,选择Add as Library...添加成库。
 */
public class TestConnection {
    public static void main(String[] args) throws SQLException, ClassNotFoundException {
        // 1.加载驱动（准备工作）
        Class.forName("com.mysql.cj.jdbc.Driver");
        // 2.获取连接
        /*
         * 参数1：url
         * 格式：jdbc:mysql://主机名:端口号/库名
         * 参数2：用户名
         * 参数3：密码
         */
        Connection connection = DriverManager.getConnection("jdbc:mysql://localhost:3306/test?useUnicode=true&characterEncoding=utf8&zeroDateTimeBehavior=CONVERT_TO_NULL&useSSL=false&serverTimezone=Asia/Shanghai",
                "root", "123456");
        // 3.执行增删改查★
        //①获取执行sql语句的命令对象
        Statement statement = connection.createStatement();
        //②执行sql语句
        int update = statement.executeUpdate("delete from user where id=13");
        //③处理结果
        System.out.println(update>0?"success":"failure");
        // 4.关闭连接
        statement.close();
        connection.close();
    }
}
```

#### PreparedSratement的使用

```java
import org.junit.Test;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.util.Scanner;

/**
 * 一、向user表中插入数据，效果如下：
 请输入编号：13
 请输入姓名：张三丰
 请输入年龄：200
 请输入性别：男
 插入成功！
 */
public class TestPreparedStatementByUtils {
    //增删改
    @Test
    public void test1() throws Exception {
        Scanner input = new Scanner(System.in);
        System.out.println("请输入编号：");
        int id = input.nextInt();
        System.out.println("请输入姓名：");
        String name = input.next();
        System.out.println("请输入年龄：");
        int age = input.nextInt();
        System.out.println("请输入性别：");
        String sex = input.next();

        //-----------------------------连接数据库的步骤-----------------
        //1.获取连接
        Class.forName("com.mysql.cj.jdbc.Driver");
        Connection connection = DriverManager.getConnection("jdbc:mysql://localhost:3306/test?useUnicode=true&characterEncoding=utf8&zeroDateTimeBehavior=CONVERT_TO_NULL&useSSL=false&serverTimezone=Asia/Shanghai",
                "root", "123456");
        //2、执行插入
        PreparedStatement statement = connection.prepareStatement("insert into user values(?,?,?,?)");
        statement.setInt(1, id);
        statement.setString(2, name);
        statement.setInt(3, age);
        statement.setString(4, sex);
        int update = statement.executeUpdate();
        System.out.println(update>0?"插入成功":"插入失败");
        //3.关闭
        statement.close();
        connection.close();
    }
    //查询
    @Test
    public void test2() throws Exception {
//		请输入编号：13
        Scanner input = new Scanner(System.in);
        System.out.println("请输入编号：");
        int id = input.nextInt();
        //-----------------------------连接数据库的步骤-----------------
        //1.获取连接
        Class.forName("com.mysql.cj.jdbc.Driver");
        Connection connection = DriverManager.getConnection("jdbc:mysql://localhost:3306/test?useUnicode=true&characterEncoding=utf8&zeroDateTimeBehavior=CONVERT_TO_NULL&useSSL=false&serverTimezone=Asia/Shanghai",
                "root", "123456");
        //2、执行查询
        PreparedStatement statement = connection.prepareStatement(
                "select id,name,age,sex from user where id = ?");
        statement.setInt(1, id);
        ResultSet set = statement.executeQuery();
        if(set.next()) {
            String name = set.getString(2);
            int age = set.getInt(3);
            String sex = set.getString(4);
            System.out.println(id+"\t"+name+"\t"+age+"\t"+sex);
        }
        //3.关闭
        set.close();
        statement.close();
        connection.close();
    }
}
```

#### JDBC中的Statement 和PreparedStatement的区别？

1. PreparedStatement 继承于 Statement
2. Statement 一般用于执行固定的没有参数的SQL
3. PreparedStatement 一般用于执行有？参数预编译的SQL语句。
4. PreparedStatement支持?操作参数，相对于Statement更加灵活。
5. PreparedStatement可以防止SQL注入，安全性高于Statement。
   

#### 批处理

`JDBCUtils.java`见下面2.数据库连接池部分

```java
import org.junit.Test;

import java.sql.Connection;
import java.sql.PreparedStatement;

/**
 * 此类用于演示批处理
 * 情况1：多条sql语句的批量执行【较少使用】
 * Statement+批处理：提高了执行的效率，并没有减少编译的次数
 * 情况2：一条sql语句的批量传参【较多使用】
 * PreparedStatement+批处理：减少了执行的次数，也减少了编译的次数，大大提高效率
 * 相关API：
 *     addBatch()
 *     executeBatch()
 *     clearBatch()
 * 注意：
 *     ①需要在url添加reWriteBatchedStatement = true
 *   驱动类使用的版本：8.0.21 但不能使用5.1.7（不支持批处理）
 *  ②插入时，使用values，而不是value！
 *案例：添加50000条用户记录
 */

public class TestBatch {
    //没有使用批处理
    @Test
    public void testNoBatch() throws Exception {
        long start = System.currentTimeMillis();
        //1.获取连接
        Connection connection = JDBCUtils.getConnection();
        //2.执行插入
        PreparedStatement statement = connection.prepareStatement("insert into user values(NULL,?,?,?)");
        for(int i=1;i<=50000;i++) {
            statement.setString(1, "john"+i);
            statement.setInt(2, 0);
            statement.setString(3, "男");
            statement.executeUpdate();
        }
        //3.关闭
        JDBCUtils.close(null, statement, connection);
        long end = System.currentTimeMillis();
        System.out.println("没有使用批处理耗时：" + (end-start));
    }
    //使用批处理
    @Test
    public void testUseBatch() throws Exception {
        long start = System.currentTimeMillis();
        //1.获取连接
        Connection connection = JDBCUtils.getConnection();
        //2.执行插入
        PreparedStatement statement = connection.prepareStatement("insert into user values(NULL,?,?,?)");
        for(int i=1;i<=50000;i++) {
            statement.setString(1, "john"+i);
            statement.setInt(2, 0);
            statement.setString(3, "女");
            //添加到批处理包（放到框中）
            statement.addBatch();
            if(i%1000==0) {
                statement.executeBatch();//执行批处理包的sql(将框中的苹果们运到了楼上)
                statement.clearBatch();//清空批处理包的sql(卸货)
            }
        }
        //3.关闭
        JDBCUtils.close(null, statement, connection);
        long end = System.currentTimeMillis();
        System.out.println("使用批处理耗时：" + (end-start));
    }
}
```

#### 二进制Blob类型数据的读写

```java
import org.junit.Test;

import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.InputStream;
import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.ResultSet;

/**
 * 此类用于演示Blob类型数据的读写
 * 注意：只能使用PreparedStatement实现Blob类型的读写，不能使用Statement
 * 相关API：
 *     setBlob(占位符索引，InputStream)
 *     InputStream is =getBinaryStream(列索引)
 */
public class TestBlob {
    //测试Blob类型数据的写入：修改小苍的照片为指定照片
    @Test
    public void test1() throws Exception {
        //1.获取连接
        Connection connection = JDBCUtils.getConnection();
        //2.执行修改
        PreparedStatement statement = connection.prepareStatement("update userwithphoto set photo = ? where name = ?");
        FileInputStream fileInputStream = new FileInputStream("Resources\\a.jpg");
        statement.setBlob(1, fileInputStream);
        statement.setString(2, "小苍");
        int update = statement.executeUpdate();
        System.out.println(update>0?"插入成功":"插入失败");
        //3.关闭
        JDBCUtils.close(null, statement, connection);
    }
    //测试Blob类型数据的读取：将小苍的图片读取到项目的根目录下
    @Test
    public void test2() throws Exception {
        //1.获取连接
        Connection connection = JDBCUtils.getConnection();
        //2.执行查询
        PreparedStatement statement = connection.prepareStatement("select photo from userwithphoto where name = ?");
        statement.setString(1, "小苍");
        ResultSet set = statement.executeQuery();
        if(set.next()) {
//       Blob blob = set.getBlob(1);
//       InputStream binaryStream = blob.getBinaryStream();
            InputStream inputStream = set.getBinaryStream(1);
            FileOutputStream fos = new FileOutputStream("src\\beauty.jpg");
            //边读边写：复制图片
            byte[] b = new byte[1024];
            int len;
            while((len=inputStream.read(b))!=-1) {
                fos.write(b, 0, len);
            }
            fos.close();
            inputStream.close();
        }
        //3.关闭连接资源
        JDBCUtils.close(set, statement, connection);
    }
}
```

## 2.数据库连接池

javax.sql包下的DataSource是一个数据库连接池接口。一些开源组织对它进行了实现。
多种开源的数据库连接池：C3P0，DBCP，Druid，BoneCP，Proxool等。

### 连接池的好处

1. 提高效率
2. 提高重用性
3. 采用一套统一的管理机制，减少数据库崩溃问题

### 说说数据库连接池工作原理和实现方案？

1. 工作原理：JAVA EE服务器启动时会建立一定数量的池连接，并一直维持不少于此数目的池连接。客户端程序需要连接时，池驱动程序会返回一个未使用的池连接并将其表记为忙。如果当前没有空闲连接，池驱动程序就新建一定数量的连接，新建连接的数量有配置参数决定。当使用的池连接调用完成后，池驱动程序将此连接表记为空闲，其他调用就可以使用这个连接。
2. 实现方案：返回的Connection是原始Connection的代理，代理Connection的close方法，当调用close方法时，不是真正关连接，而是把它代理的Connection对象放回到连接池中，等待下一次重复利用。

### Druid的使用

**Druid使用方式一：**

```java
	//创建一个数据库连接池
	DruidDataSource dds = new DruidDataSource();
	//设置连接参数	
	dds.setUrl("jdbc:mysql://localhost:3306/test");
	dds.setUsername("root");
	dds.setPassword("123456");
	dds.setDriverClassName("com.mysql.jdbc.Driver");	
	//设置池子中的初始化连接数
	dds.setInitialSize(5);
	//设置池子中的最大连接数
	dds.setMaxActive(10);
	//设置池子中的最小连接数
	dds.setMinIdle(5);		
	//获取连接	
	Connection connection = dds.getConnection();	
	System.out.println("connected!");
```

**Druid使用方式二：**

```java
	Properties properties = new Properties();	properties.load(this.getClass().getClassLoader().getResourceAsStream("druid.properties"));	
	//1、获取连接池
	DataSource dataSource = DruidDataSourceFactory.createDataSource(properties);
	//2、获取连接
	Connection connection = dataSource.getConnection();
	System.out.println(connection);	
	//3.关闭连接
	connection.close();
```

**`druid.properties`:**

```java
#key=value
driverClassName=com.mysql.cj.jdbc.Driver
url=jdbc:mysql://localhost:3306/test?useUnicode=true&characterEncoding=utf8&zeroDateTimeBehavior=CONVERT_TO_NULL&useSSL=false&serverTimezone=Asia/Shanghai
username=root
password=123456
initialSize=10
minIdle=5
maxActive=20
maxWait=5000
```

### JDBCUTils工具类

需要提前导入`druid-1.1.10.jar` 和 `c3p0-0.9.1.2.jar`。

```java
import com.alibaba.druid.pool.DruidDataSourceFactory;
import com.mchange.v2.c3p0.ComboPooledDataSource;

import javax.sql.DataSource;
import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;
import java.util.Properties;

/**
 * jdbc工具类
 */
public class JDBCUtils {
    static DataSource dataSource;
    static {
        try {
            Properties properties = new Properties();
            properties.load(JDBCUtils.class.getClassLoader().getResourceAsStream("druid.properties"));
            dataSource = DruidDataSourceFactory.createDataSource(properties);
        }catch (Exception e) {
            e.printStackTrace();
        }
    }
    //使用druid获取连接
    public static Connection getConnection() throws Exception  {
        return dataSource.getConnection();
    }
    //使用c3p0获取连接
    public static Connection getConnection2() throws SQLException {
        ComboPooledDataSource cpds = new ComboPooledDataSource("hello");
        return cpds.getConnection();
    }
    //释放连接资源
    public static void close(ResultSet set, Statement statement, Connection connection){
        try {
            if(set!=null)
                set.close();
            if(statement!=null)
                statement.close();
            if(connection!=null)
                connection.close();
        } catch (SQLException e) {
            throw new RuntimeException(e);
        }
    }
}
```

### 事务

**事务的流程：**

start -> A,B账户均存在 -> A账户扣除1000元 -> B账户增加1000元 -> end

**事物四大特性：**

- 原子性(Atomicity):事务必须是原子工作单元；对于其数据修改，要么全都执行，要么全都不执行
- 一致性(Consistency):事务在完成时，必须使所有的数据都保持一致状态
- 隔离性(Isolation):由并发事务所作的修改必须与任何其他并发事物所作的修改隔离
- 持久性:事务完成之后，它对于系统的影响是永久性的

**JDBC事物API**

- Connection.getAutoCommit() 获得当前事务的提交方式，默认为true
- Connection.setAutoCommit() 设置事务的提交属性，参数是true：自动提交；反之。
- Connection.commit() 提交事物
- Connection.rollback() 回滚事务

**JDBC处理事务的通常模式**

- 先将事务的自动提交关闭
- 执行事务中的若干SQL语句
- 事务提交:SQL失败则回滚
- 恢复JDBC的事务提交状态，释放资源。
  

```java
import org.junit.Test;

import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.SQLException;

public class TestTransaction {
    @Test
    public void testTransaction() {
        //1.获取连接
        Connection connection = null;
        //事务使用步骤二：编写事务的语句
        //2.执行增删改查
        PreparedStatement statement = null;
        try {
            connection = JDBCUtils.getConnection();
            //事务使用步骤一：开启事务
            connection.setAutoCommit(false);//取消了事务的自动提交+开启事务
            statement = connection.prepareStatement("update account set balance = ? where username = ?");
            statement.setDouble(1, 995);
            statement.setString(2, "张三");
            statement.executeUpdate();
            int i=1/0;
            //操作2：李四的钱多5块
            statement.setDouble(1, 1005);
            statement.setString(2, "李四");
            statement.executeUpdate();
            //事务使用步骤三：结束事务
            connection.commit();//如果执行到该处，说明上面操作没有异常，则可以正常提交事务
        } catch (Exception e) {
            try {
                connection.rollback();//如果执行到该处，说明try块操作有异常，则需要回滚！
            } catch (SQLException e1) {
                e1.printStackTrace();
            }
        }
        finally {
            //3.关闭连接
            JDBCUtils.close(null, statement, connection);
        }
    }
}
```

## 📚 References

- https://blog.csdn.net/github_39430101/article/details/77844465
- https://blog.csdn.net/weixin_47410197/article/details/113834058?utm_medium=distribute.pc_relevant_t0.none-task-blog-2%7Edefault%7EBlogCommendFromMachineLearnPai2%7Edefault-1.baidujs&dist_request_id=1619752229757_32510&depth_1-utm_source=distribute.pc_relevant_t0.none-task-blog-2%7Edefault%7EBlogCommendFromMachineLearnPai2%7Edefault-1.baidujs
- https://blog.csdn.net/Charles_ZengYC/article/details/104508034?utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromBaidu%7Edefault-1.baidujs&dist_request_id=1619752098395_09792&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromBaidu%7Edefault-1.baidujs
