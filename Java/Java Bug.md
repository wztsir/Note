#### 2022.0417

web开发中前端导入后端 servlet 的数据出现问题。

现象：返回404，找不到页面

form表单的action地址写错

现象：返回页面一片空白

连接建立正确，重点排查 servlet 代码 ，但是参入的参数，doGet 与 doPost方法

现象：返回404,查看报错，报错非常具体  Communications link failure

```
org.apache.ibatis.exceptions.PersistenceException: 
### Error querying database.  Cause: com.mysql.jdbc.exceptions.jdbc4.CommunicationsException: Communications link failure

The last packet sent successfully to the server was 0 milliseconds ago. The driver has not received any packets from the server.
### The error may exist in com/baseStudy/mapper/UserMapper.java (best guess)
### The error may involve com.baseStudy.mapper.UserMapper.select
### The error occurred while executing a query
### Cause: com.mysql.jdbc.exceptions.jdbc4.CommunicationsException: Communications link failure
根本原因。
com.mysql.jdbc.exceptions.jdbc4.CommunicationsException: Communications link failure
```

原因：mysql本地数据库未打开

现象：404 根本原因：java.sql.SQLException: Could not retrieve transation read-only status server

原因：jdbc驱动版本过低，mysql使用8.0.28版本

```
<!-- <version>5.1.34</version>-->
     <version>8.0.11</version>
```

#### 2022.0419

jsp页面返回数据

```
${brand.brandName}
```

jsp没有导入相关依赖项，没有关闭忽略

```jsp
<%@ page isELIgnored="false" %>
<%--必须导入jstl的依赖--%>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
```

#### 2022.04.20

UserMapepper.xml文件一直标红

检查相关的导入项目mybatis,mysql，都有，原来文件格式出错，为fxml

#### 2022.04.21

使用maven，修改目录后爆红，可以clean-》target目录，删除已经生成的冗余目录

jsp页面：背景图片无法识别显示，实际上运行的代码出现问题

最后，多重启了几次tomcat，识别出来了，猜测，两次项目的tomcat没有做好隔离

#### 2022.04.24

1、database数据表字段与类对象属性名不对应，查找出为null

暴力：直接修改数据库字段名（没有实质解决问题）

问题：没有通过注解申明引用

```
@ResultMap("brandResultMap")
```

2、数据无法显示，数据brand数据一条都没有

技巧：检查控制台，查看是否发出请求，答案是没有发出请求

进一步检查：axios包没有显示的通过如下引入

```
<script src="js/axios-0.18.0.js"></script>
```

#### 2022.04.25

报错

```
org.apache.ibatis.exceptions.PersistenceException: 
### Error updating database.  Cause: java.sql.SQLException: Could not retrieve transation read-only status server
### The error may exist in com/baseStudy/mapper/BrandMapper.java (best guess)
### The error may involve com.baseStudy.mapper.BrandMapper.add-Inline
### The error occurred while setting parameters
### SQL: insert into tb_brand values(null,?,?,?,?,?)
### Cause: java.sql.SQLException: Could not retrieve transation read-only status server
    org.apache.ibatis.exceptions.ExceptionFactory.wrapException(ExceptionFactory.java:30)
    org.apache.ibatis.session.defaults.DefaultSqlSession.update(DefaultSqlSession.java:199)
    org.apache.ibatis.session.defaults.DefaultSqlSession.insert(DefaultSqlSession.java:184)
    org.apache.ibatis.binding.MapperMethod.execute(MapperMethod.java:62)
    org.apache.ibatis.binding.MapperProxy$PlainMethodInvoker.invoke(MapperProxy.java:152)
    org.apache.ibatis.binding.MapperProxy.invoke(MapperProxy.java:85)
    jdk.proxy4/jdk.proxy4.$Proxy30.add(Unknown Source)
    com.baseStudy.service.impl.BrandServiceImpl.add(BrandServiceImpl.java:31)
    com.baseStudy.web.servlet.AddServlet.doGet(AddServlet.java:28)
    javax.servlet.http.HttpServlet.service(HttpServlet.java:621)
    javax.servlet.http.HttpServlet.service(HttpServlet.java:728)
    org.apache.tomcat.websocket.server.WsFilter.doFilter(WsFilter.java:51)
```

无法识别出到底是什么sql语句

同2022.0417一样的解决办法，即本地mysql版本与mysql-connector-java驱动包过低

#### 2022.05.04

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220504231601406.png" alt="image-20220504231601406" style="zoom:50%;" />

无法识别导入的spring包

由于电脑长时间开启，出现问题，解决办法，删除模块，重新布置环境

坐标导入错误

需要导入spring-mvc，但是导入的是spring-context  

#### 2022.05.09

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220509232026683.png" alt="image-20220509232026683" style="zoom: 67%;" />

首先通过了service与control层级的测试，判断不是这里出错，所以一定是访问静态资源出错

ps：没有查出原因，之后自然好的

更改springBoot版本为2.5.0（在application.yml中乱添加静态资源的访问路径帮倒忙）

BUG：无法自动加载index.jsp，但是可以自动加载html文件

#### 2022.5.29

数据库sql语句创建用户

```
create user U1 identified by 'U1';
```

创建出的用户名为U1，密码创建也为U1；

#### 2022.06.10

新增html文件

访问：http://localhost:8080/backend/page/demo/upload.html

出错

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220509232026683.png" alt="image-20220509232026683" style="zoom: 67%;" />

解决办法，重启电脑，过滤器没有进行登入检验，在/bachend目录下，直接放行

#### 2022.06.14

对于地址的，内存存储中引用类型的数据，存在在堆中，唯一

```java
   List<TreeNode> leftTree = build(low,i-1);
            List<TreeNode> rightTree = build(i+1,high);
//            细节的，代码出错，，由于加入的是root,root只初始化一次，无论怎么更改，最后值永远只有一个
            TreeNode root=new TreeNode(i);
            for (TreeNode left : leftTree) {
                for (TreeNode right : rightTree) {
                    root.right=right;
                    root.left=left;
                    res.add(root);

                }
            }
```

要添加不同的root,但是只new 一次，最后res的值都会一样

改

```java
            List<TreeNode> leftTree = build(low,i-1);
            List<TreeNode> rightTree = build(i+1,high);
//            细节的，代码出错，，由于加入的是root,root只初始化一次，无论怎么更改，最后值永远只有一个
            for (TreeNode left : leftTree) {
                for (TreeNode right : rightTree) {
                    TreeNode root=new TreeNode(i);
                    root.right=right;
                    root.left=left;
                    res.add(root);
                }
            }
```
