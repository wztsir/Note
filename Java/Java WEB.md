# Java WEB

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220313103421443.png" alt="image-20220313103421443"  />



## JDBC

### 简单实现

```java
 public static void main(String[] args) throws Exception {
//      1、注册驱动
        Class.forName("com.mysql.jdbc.Driver");
//      2、获取连接
//        String url="jdbc:mysql://127.0.0.1:3306/itcast";
//        本机默认URlS简化书写
//        String url="jdbc:mysql:///itcast";
//        禁用安全连接
        String url="jdbc:mysql:///itcast?useSSL=false";
        String username="root";
        String password="root";
        Connection conn = DriverManager.getConnection(url, username, password);
//      3、定义SQL
        String sql="update account set money=2000 where id=2";
//        4、执行SQL的对象（获取数据库的操作对象）
        Statement stmt = conn.createStatement();
//        5、执行SQL
        int count = stmt.executeUpdate(sql);
        System.out.println(count);
     
        stmt.close();
        conn.close();

    }
```

### API

#### 注册驱动DriverManager

1.注册驱动

![image-20220313221321510](C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220313221321510.png)

理解：确定是MySQL驱动，而不是其他数据库

细节的：

- MySQL 5之后的驱动包，可以省略注册驱动的步骤 
- 自动加载jar包中META-INF/services/java.sql.Driver文件 中的驱动类

2.获取数据库的连接

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220313221520058.png" alt="image-20220313221520058" style="zoom:67%;" />

jdbc:mysql是协议

#### Connection

-  获取执行 SQL 的对象 
- 管理事务

创建执行SQL的对象：

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220313222256061.png" alt="image-20220313222256061" style="zoom:67%;" />

管理事务：

开启事务

![image-20220313223211163](C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220313223211163.png)

参与autoCommit 表示是否自动提交事务，true表示自动提交事 务，false表示手动提交事务。而开启事务需要将该参数设为为 false

提交事务

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220313223426568.png" alt="image-20220313223426568" style="zoom: 80%;" />

回滚事务

![image-20220313223349403](C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220313223349403.png)

```java
    3、定义SQL
        String sql1 = "update account set money=2000 where id=2";
        String sql2 = "update account set money=2000 where id=2";
//        4、执行SQL的对象
        Statement stmt = conn.createStatement();
        try {
//          开启事务
            conn.setAutoCommit(false);
//        5、执行SQL
            int count1 = stmt.executeUpdate(sql1);
            System.out.println(count1);
            int count2 = stmt.executeUpdate(sql2);
            System.out.println(count2);
//          提交事务·
            conn.commit();
        } catch (Exception e) {
//          回滚
            conn.rollback();
            e.printStackTrace();
        }
```

#### Statement

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220313225310101.png" alt="image-20220313225310101" style="zoom:67%;" />

#### ResultSet

使用于DQL语句，数据查询（用来处理数据集）

1.boolean next() 将光标从当前位置向前移动一行 

判断当前行是否为有效行 方法返回值说明： 

- true ： 有效行，当前行有数据 
- false ： 无效行，当前行没有数据 

2.xxx getXxx(参数)：获取数据 xxx : 数据类型；如： int getInt(参数) ；String getString(参 数) 

参数 

- int类型的参数：列的编号，从1开始 
- String类型的参数： 列的名称

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220314091129100.png" alt="image-20220314091129100" style="zoom: 80%;" />

```java
   public static void main(String[] args) throws Exception {
//      1、注册驱动
        Class.forName("com.mysql.jdbc.Driver");
//        2、获取连接
        String url = "jdbc:mysql:///itcast?useSSL=false";
        String username = "root";
        String password = "root";
        Connection conn = DriverManager.getConnection(url, username, password);
//      3、定义SQL
        String sql = "select *from account";
//        4、执行SQL的对象
        Statement stmt = conn.createStatement();
//        5、执行SQL
        ResultSet rs = stmt.executeQuery(sql);
        List<Account> list = new ArrayList<>();
        while (rs.next()) {
            Account ac = new Account(rs.getInt("id"),
                    rs.getString("name"),
                    rs.getDouble("money"));

            list.add(ac);
        }
        System.out.println(list);
        stmt.close();
        conn.close();
    }
```

```java
public class Account {
    //    数据类型和表中字段类型对对映
    private int id;
    private String name;
    private double money;
    public Account(int id, String name, double money) {
        this.id = id;
        this.name = name;
        this.money = money;
     }
    }
```

#### PreparedStatement

普通的登入。存在SQL注入的风险

```java
    public static void main(String[] args) throws Exception {
//      1、注册驱动
        Class.forName("com.mysql.jdbc.Driver");
//      2、获取连接
        String url="jdbc:mysql:///itcast?useSSL=false";
        String username="root";
        String password="root";
        Connection conn = DriverManager.getConnection(url, username, password);
        String name="wzt";
        String pd="'or '1'='1 ";
//      3、定义SQL
        String sql="select * from user  where name='"+name+"' and password='"+pd+"'";
        System.out.println(sql);
//      4、执行SQL的对象（获取数据库操作对象）
        Statement stmt = conn.createStatement();
//      5、执行SQL
        ResultSet rs = stmt.executeQuery(sql);
        if(rs.next()){
            System.out.println("登入成功");
        }else{
            System.out.println("登入失败");
        }
        stmt.close();
        conn.close();	
    }
```

功能1：防止注入

![image-20220314145845116](C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220314145845116.png)

```java
 public static void main(String[] args) throws Exception {
//       1、注册驱动(可省略不写)
//     Class.forName("com.mysql.jdbc.Driver");
//      2、获取连接
       String url="jdbc:mysql:///itcast?useSSL=false";
       String username="root";
       String password="root";
       Connection conn = DriverManager.getConnection(url, username, password);
//      3、定义SQL
       String name="wzt";
       String pd="'or '1'='1 ";
       String sql="select * from user  where name= ? and password=? ";
//      4、获取SQL的对象
       PreparedStatement pstmt = conn.prepareStatement(sql);
       pstmt.setString(1,name);
       pstmt.setString(2,pd);
//      5、执行SQL,不需要再导入SQL语句了
       ResultSet rs = pstmt.executeQuery();
       if(rs.next()){
           System.out.println("登入成功");
       }else{
           System.out.println("登入失败");
       }
       pstmt.close();
       conn.close();
   }
```

功能二：预编译，性能优化

java代码同MySQL的交互

<img src="D:\book\java\day03-JDBC\ppt\assets\image-20210725195756848.png" alt="image-20210725195756848" style="zoom:67%;" />

开启预编译的功能：

在代码中编写url时需要加上以下参数。而我们之前根本就没有 开启预编译功能，只是解决了SQL注入漏洞。

```java
useServerPrepStmts=true
```

检查语法与编译SQL花费时间很多

```java
 PreparedStatement pstmt = conn.prepareStatement(sql);
```

传入Mysql,完成了检查与编译的工作

```java
 pstmt.setString(1,name);
 pstmt.setString(2,pd);
```

执行SQL，换不同参数时，检查和编译不需要重复执行了，性能更优

日志：只需要prepare一次，可以直接执行

```java
Prepare select * from user  where name= ? and password=?
Execute    select * from user  where name= 'wzt' and password='\'or \'1\'=\'1 '
Execute    select * from user  where name= 'aaa' and password='bbb'
```

### 数据库连接池

connection不再需要driverManager获取，只需要通过数据库连接池获取即可

数据库连接池的强大功能:

- 数据库连接池是个容器，负责分配、管理数据库连接 (Connection);
- 它允许应用程序重复使用一个现有的数据库连接，而不是再重新建立一个；
- 释放空闲时间超过最大空闲时间的数据库连接来避免因为没 有释放数据库连接而引起的数据库连接遗漏 好处 资源重用 提升系统响应速度 避免数据库连接遗漏

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220314155532358.png" alt="image-20220314155532358" style="zoom:80%;" />

```java
 public static void main(String[] args) throws Exception {
//    1.导入jar包
//    2.定义配置文件
/*#固定的
        driverClassName=com.mysql.jdbc.Driver
        url=jdbc:mysql:///itcast?useSSL=false&useServerPrepStmts=true
        username=root
        password=root
# 初始连接数目
        initialSize=5
# 最大连接数目
        maxActive=10
# 最大等待时间，3s
        maxWait=3000*/
//    3. 加载配置文件
        Properties prop = new Properties();
        prop.load(new FileInputStream("jdbc_demo/src/druid.properties"));
        // 路径：使用相对路径，可以自动识别在use.dir下的所有文件，即默认加上了D:\Project\Java\jdbc（
        // 可以通过 System.out.println(System.getProperty("user.dir"))查询）
//    4、获取连接池对象
        DataSource dataSource = DruidDataSourceFactory.createDataSource(prop);
//    5、获取数据库连接
        Connection connection = dataSource.getConnection();
        System.out.println(connection);
//        System.out.println(System.getProperty("user.dir"));
    }

```

##### 最新案例

ps:使用最新技术，注册驱动省略、从数据库连接池获取连接、以防止SQL注入的方式获取执行数据库对象、处理数据集

```java
  public static void main(String[] args) throws Exception {
//      1、获取数据连接
        Properties pop = new Properties();
        pop.load(new FileInputStream("jdbc_demo/src/druid.properties"));
        DataSource dataSource = DruidDataSourceFactory.createDataSource(pop);
        Connection conn = dataSource.getConnection();
//      2、sql语句
        String sql = "SELECT * FROM tb_brand";
//      3、获取操作数据库对象
        PreparedStatement pstmt = conn.prepareStatement(sql);
//        4、执行sql对象
        ResultSet rs = pstmt.executeQuery();
        Brand brand = null;
        List<Brand> lst = new ArrayList<>();
        while (rs.next()) {
            brand = new Brand(rs.getInt("id"),
                    rs.getString("brand_name"),
                    rs.getString("company_name"),
                    rs.getInt("ordered"),
                    rs.getString("description"),
                    rs.getInt("status")
            );
            lst.add(brand);
        }
        System.out.println(lst);
        rs.close();
        pstmt.close();
        conn.close();
    }
```

ps:考虑真正的业务需求时

查询所有

- SQL：select * from tb_brand; 
- 参数：不需要 
- 结果：List(集合)

## Maven

Maven是专门用于管理和构建Java项目的工具，它的主要功能有： 

- 提供了一套标准化的项目结构 
- 提供了一套标准化的构建流程（编译，测试，打包，发布……） 
- 提供了一套依赖管理机制

### 仓库

- 本地仓库：自己计算机上的一个目录 
- 中央仓库：由Maven团队维护的全球唯一的仓库 地址： https://repo1.maven.org/maven2/ 
- 远程仓库(私服)：一般由公司团队搭建的私有仓库 ；

当项目中使用坐标引入对应依赖jar包后，首先会查找本地仓库中是否有对应的jar包： 如果有，则在项目直接引用; 如果没有，则去中央仓库中下载对应的jar包到本地仓库。

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220315095234204.png" alt="image-20220315095234204" style="zoom: 67%;" />

### 常用命令

- compile ：编译 
- clean：清理 
- test：测试
- package：打包 
- install：安装

### IDEA中配置maven

- 首先创建空项目，将之前的项目关闭
- 配置项目maven环境，找到setting，更改maven的属性即可
- 利用maven创建新的模块

### Maven 坐标

是资源的唯一表示符

主要组成如下：	

- groupId：定义当前Maven项目隶属组织名称（通常是域名反写，例如：com.itheima） 
- artifactId：定义当前Maven项目名称（通常是模块名称，例如 order-service、goods-service） 
- version：定义当前项目版本号
- sco

### scope

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220317145743855.png" alt="image-20220317145743855" style="zoom:67%;" />

## Mybatis

- MyBatis 是一款优秀的持久层框架，用于简化 JDBC 开发
- 负责将数据到保存到数据库的那一层代码。 以后开发我们会将操作数据库的Java代码作为持久层。而Mybatis就是对jdbc代码进行了封装。 
- JavaEE三层架构：表现层、业务层、持久层

框架优化代码的目标

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220317150913438.png" alt="image-20220317150913438" style="zoom:67%;" />

- 硬编码利用配置文件
- 操作繁琐，利用接口，自动帮助完成





## HTML

- 结构：对应的是 HTML 语言 
- 表现：对应的是 CSS 语言 
- 行为：对应的是 JavaScript 语言

### 路径

#### 相对路径

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220317161535724.png" alt="image-20220317161535724" style="zoom: 80%;" />



../img/a.jpg，其中../返回上一级目录

- ./ 表示当前路径 
- ../ 表示上一级路径 
- ../../ 表示上两级路径 

#### 绝对路径

细节的，网络资源目录也是可以存放的

### 标签

#### 基础标签

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220317154403197.png" alt="image-20220317154403197" style="zoom:67%;" />

font：字体标签 

1. face 属性：用来设置字体。如 "楷体"、"宋体"等 

   2.color 属性：设置文字颜色。颜色有三种表示方式 :

- 英文单词：red,pink,blue... 这种方式表示的颜色特别有限，所以一般不用。 
- rgb(值1,值2,值3)：值的取值范围：0~255 此种方式也就是三原色（红绿蓝）设置方式。 例如： rgb(255,0,0)。 这种书写起来比较麻烦，一般不用。 
- #值1值2值3：值的范围：00~FF 这种方式是rgb方式的简化写法，以后基本都用此方式。 值1表示红色的范围，值2表示绿色的范围，值3表示蓝色范围。例如： #ff0000 

3. size 属性：设置文字大小



#### 超链接标签

href：指定访问资源的URL 

target：指定打开资源的方式

-  _self：默认值，在当前页面打开 
- _blank：在空白页面打开

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Title</title>
</head>
<body>
<a href="https://www.itcast.cn" target="_self">点我有惊喜</a>
</body>
</html>
```

#### 布局标签

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220317172152877.png" alt="image-20220317172152877" style="zoom:67%;" />

这两个标签，一般都是和css结合到一块使用来实现页面的布局。 

div 标签 在浏览器上会有换行的效果，而 span 标签在浏览器上没有换行效果。

#### f'orm:表单标签

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220317164314696.png" alt="image-20220317164314696" style="zoom:67%;" />

#### 表单项标签

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220317170302110.png" alt="image-20220317170302110" style="zoom:67%;" />

## CSS

### 导入

### 选择器

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220317173252609.png" alt="image-20220317173252609" style="zoom:67%;" />

元素选择器，也可以认为是标签选择器

## JavaScript

### 低级错误

```javascript
"myFunction('wzt','student')"
```

外面用双引号，里面就用单引号，才能识别出来，并且是英文状态下的

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220319114337244.png" alt="image-20220319114337244" style="zoom:80%;" />



### 变量

#### 局部 变量

在 JavaScript 函数内部声明的变量（使用 var）是*局部*变量，所以只能在函数内部访问它。（该变量的作用域是局部的）。

您可以在不同的函数中使用名称相同的局部变量，因为只有声明过该变量的函数才能识别出该变量。

只要函数运行完毕，本地变量就会被删除。

#### 全局变量

在函数外声明的变量是全局变量，网页上的所有脚本和函数都能访问它

#### var变量

- 作用域：全局变量（在函数体外）
- 变量可以重复定义
- 变量可以存放不同类型的值

```javascript
 {var age=20;

  }
  alert(age);
```

```javascript
{var age=20;
 var age=30;
}
alert(age);
```

```javascript
{var age=20;
age="凝神屏气，我可以";
}
alert(age);
```

#### let变量

- 作用域：只在代码块中有效
- 变量不可以重复定义
- 变量可以存放不同类型的值（同java不一样，其他都一样）

#### 常量

```javascript
{ const age=20;
  age=30;
  alert( typeof age);
}
```

不可以重复赋值

#### 变量的生存期

JavaScript 变量的生命期从它们被声明的时间开始。

局部变量会在函数运行以后被删除。

全局变量会在页面关闭后被删除



### 数据类型

原始数据类型

- number：数字（整数、小数、NaN(Not a Number)）
- string：字符、字符串，单双引皆可
- boolean：布尔。true，false
- null：对象为空
- undefined：当声明的变量未初始化时，该变量的默认值是 undefined

表面上 undefined 与 null 都是什么都没有的意思，但是实际上 undefined 是未定义（就是变量没有初始化），null 是一个变量初始化了，但是什么值都没给，只给了一个空对象；进一步说，undefined 与 null是值相等，类型不相等。



NaN 是一个特殊的数值，NaN 即非数值（Not a Number），这个数值用于本来要返回数值的操作数未返回数值的情况。

NaN 与任何值都不相等，包括 NaN 本身。

可以通过 isNaN() 方法来判断某个数值是否是NaN这个特殊的数，使用 isNaN() 方法会将传入的数值如果是非数值的会将其自动转换成数值类型，若能转换成数值类型，那么这个函数返回 false，若不能转换成数值类型，则这个数就是 NaN，即返回 true。

### 运算符

实际上===才和Java中一样

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220318180459256.png" alt="image-20220318180459256" style="zoom:67%;" />

- 一元运算符：++，-- 
- 算术运算符：+，-，*，/，% 
- 赋值运算符：=，+=，-=… 
- 关系运算符：>，<，>=，<=，!=，==，===… 
- 逻辑运算符：&&，||，! 
- 三元运算符：条件表达式 ? true_value : false_value

关系运算符会自动发生类型转换

### 类型转换

#### 1.转换为int

- string 转换为 number 类型：按照字符串的字面值，转为数字。如果字面值不是数字，则转为NaN
- boolean 转换为 number 类型：true 转为1，false转为0

转换为数字，一是+，二是利用parseInt

```javascript
var age=+"20"
alert(age+parseInt("1"))
```

```javascript
var age=+true
alert(age+parseInt("1"))
```

#### 2.转为boolean

- number 类型转换为 boolean 类型：0和NaN转为false，其他的数字转为true 
- string 类型转换为 boolean 类型：空字符串转为false，其他的字符串转为true 
- null类型转换为 boolean 类型是 false 
- undefined 转换为 boolean 类型是 false

#### 使用场景

由于 JavaScript 会自动进行类型转换，所以上述的判断可以进行简化，由上至下

```javascript
var str = "";
//健壮性判断
if(str != null && str.length > 0){
alert("转为true");
}else {
alert("转为false");
}

var str2 = "abc";
//健壮性判断
if(str2){
alert("转为true");
}else {
alert("转为false");
}
```

### 函数



```javascript
var str=24
var a=3
alert(add(a,str))

function add(a,b){
    return a+b;
}
```

```javascript
alert(add(a,b,1))

function add(a,b){
    return a+b;
}
```

参数传递多了也不会报错

函数的另一种书写方式：

```javascript
var str=20;
var a=3;
var jian = function(a,b){
return a-b;
}
alert (jian(str,a))
```

### 对象

#### 数组array

JavaScript 中的数组相当于 Java 中集合。数组的长度是可以变化的，而 JavaScript 是弱类型，所以可以存储任意的类型的数据。

定义数组的两种方式如下：

方式一：

```javascript
var arr3 = [1,2,3];
arr3[10] = 10;
alert(arr3[10]); // 10
alert(arr3[9]); //undefined
```

方式二：

```javascript
var arr = new Array(1,2,3);
 alert(arr);//1,2,3
```





#### 字符串

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220319114717634.png" alt="image-20220319114717634" style="zoom:67%;" />



#### 自定义对象

在 JavaScript 中, 对象 使用 名字作为索引。

如果你使用名字作为索引，当访问数组时，JavaScript 会把数组重新定义为标准对象。

执行这样操作后，数组的方法及属性将不能再使用，否则会产生错误:

```javascript
websites = {site:"菜鸟教程", url:"www.runoob.com", like:460}
```



### BOM

BOM：Browser Object Model 浏览器对象模型。也就是 JavaScript 将浏览器的各个组成部分封装为对象。 我们要操作浏览器的各个组成部分就可以通过操作 BOM 中的对象来实现。比如：我现在想将浏览器地址栏的地址改为 https://www.itheima.com 就可以通过使用 BOM 中定义的 Location 对象的 href 属性，代码： location.href = "https://itheima.com"; BOM 中包含了如下对象： 

- Window：浏览器窗口对象 
- Navigator：浏览器对象 (不常用)
- Screen：屏幕对象 (不常用)
- History：历史记录对象 
- Location：地址栏对象

window:想使用 Location 对象的话，就可以使用 window 对象获取；写成 window.location ，而 window. 可以 省略，简化写成 location 来获取 Location 对象。



控制区域图解：

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220414195934326.png" alt="image-20220414195934326" style="zoom: 67%;" />



[代码详解12-14](D:\Project\Java\JavaScript\html\12-window对象.html)



### DOM

DOM：Document Object Model 文档对象模型。也就是 JavaScript 将 HTML 文档的各个组成部分封装为对象。  XML 就接触过，只不过 XML 文档中的标签需要写代码解析，而 HTML 文档是浏 览器解析。封装的对象分为



API

- getElementById() ：根据id属性值获取，返回单个Element对象 (唯一)
- getElementsByTagName() ：根据标签名称获取，返回Element对象数组 
- getElementsByName() ：根据name属性值获取，返回Element对象数组 
- getElementsByClassName() ：根据class属性值获取，返回Element对象数组

### 事件

事件绑定

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220319173222991.png" alt="image-20220319173222991" style="zoom:67%;" />



#### 案例

form表达元素的句柄

```
//表单元素的句柄
//     Form 对象的 onsubmit 属性指定了一个事件句柄函数。当用户单击了表单中的 Submit 按钮而提交一个表单时，
//     就会调用这个事件句柄函数。注意，当调用方法Form.submit() 时，该处理器函数不会被调用。
//
// 如果 onsubmit 句柄返回 fasle，表单的元素就不会提交。如果该函数返回其他值或什么都没有返回，则表单会被提交。
//1. 获取表单对象
```

[代码实例]( D:\Project\Java\JavaScript\html\19-表单验证.html)



## Git

1、合并同一提交的不同分支

a.git checkout 为要操作的分支，合并至目标的main	分支

```
git rebase main(目标的分支)
```

b.git merge 被合并的分支

```
git checkout -b bugFix
git commit
git checkout main
git commit
git merge bugFix
```

结果

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220328175701475.png" alt="image-20220328175701475" style="zoom:50%;" />

当前HEAD->main,main->c4

2、HEAD

a.分离HEAD

a.操作符 (^)。把这个符号加在引用名称的后面，表示让 Git 寻找指定提交记录的父提交。

```
git checkout main^
```

git checkout HEAD^

两者等价，但注意不是当前分支指向提交的父提交

b.HEAD回退到之前的状态

注意是从当前的HEAD出发

```
git checkout HEAD~ 4
```

c.相对引用最多的就是移动分支。可以直接使用 `-f` 选项让分支指向另一个提交。将 main 分支强制指向 HEAD 的第 3 级父提交。

```
git branch -f main HEAD~3
```

```
git branch -f main XXX(目标节点)
```

3、撤销变更

a.本地有效

```
git reset HEAD~1
```

本地仓库回退至上一个提交，`C2` 所做的变更还在，但是处于未加入暂存区状态。

结果：

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220328184310948.png" alt="image-20220328184310948" style="zoom:50%;" />

b.远程仓库有效（提交新的分支）

```
git revert HEAD
```

当前语句撤销的是当前分支的提交

结果是要撤销的提交记录后面多了一个新提交，这是因为新提交记录 `C2'` 引入了**更改** —— 这些更改刚好是用来撤销 `C2` 这个提交的。也就是说 `C2'` 的状态与 `C1` 是相同的。

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220328184500045.png" alt="image-20220328184500045" style="zoom:50%;" />

4、上传远程仓库

sir-forr/unishop.git特定用户和仓库

```
git remote add origin git@gitee.com:sir-forr/unishop.git
git push -u origin "master"
```

5、开发中常见的命令行(一定要看提示，图形化界面比黑框库更香)

首先：

```
git log(查看本地仓库的提交记录)
```

工作区回退（意味着之前所作的更改全部失效）

- 文件的新建，必须要先提交一次，git才能跟踪到里面的内容（不然在工作区撤销更改，文件会直接消失）

```
git checkout (文件名)可以直接用图形化界面，大小写敏感
```

- 最后合并分支，要在主分支上

```
git marge (filename)
```

- 删除前面的分支

```
 git branch -D (filename)
```





### request&response

[代码详解](D:\Project\Java\JavawebCore\servlet_demo1\src\main\java\com\baseStudy\web)





## Mysql

主键加自增约束：

特性：

- 如果不加id,则默认自增1
- 删除后，从当前表中最大id开始叠加





## 导入项目

### 项目初始化

选择黑点

选择sdk版本，注意maven的地址，在右侧maven的setting中可以查看maven的地址，选择D盘的

尽量少修改包名

修改的话注意pom.xml的配置，注意包名同文件对应

pom.xml的引入jar包，注意：mybatis默认3.5.5，mysql驱动与本地mysql版本一致，Servlet默认3.1.0版本即可

外部文件：

```
<script src="js/vue.js"></script>
<script src="js/axios-0.18.0.js"></script>
<script src="element-ui/lib/index.js"></script>
<link rel="stylesheet" href="element-ui/lib/theme-chalk/index.css">
```



### 项目结构

一个包即一个web项目，怎么样分功能，分不同的包下



## Vue

总结

this的使用

```html
    addBrand(){
                console.log(this.brand);
                let _this=this;//!!!!

                axios({
                    method:"post",
                    url:"http://localhost:8080/webProject_brand/addServlet",
                    data:_this.brand
                }).then(function (resp){
                //   显示添加成功
                    if(resp.data=="success"){
                        _this.dialogVisible=false;
                        // _this.selectAll();
                        _this.$message({
                            message:"恭喜，添加成功",
                            type:"success"
                        })

                    }
                })

            },
```

.then内部的this,访问的是绑定的对象，_this访问的是vue对象

特殊的如果通过=>书写，访问的应该也是vue对象的this
