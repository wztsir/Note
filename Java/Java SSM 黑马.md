# Spring_day01

**今日目标**

> * 掌握Spring相关概念
> * 完成IOC/DI的入门案例编写
> * 掌握IOC的相关配置与使用
> * 掌握DI的相关配置与使用

## 1，课程介绍

对于一门新技术，我们需要从`为什么要学`、`学什么`以及`怎么学`这三个方向入手来学习。那对于Spring来说:

### 1.1 为什么要学?

* 从使用和占有率看

  * Spring在市场的占有率与使用率高

  * Spring在企业的技术选型命中率高

  * 所以说,Spring技术是JavaEE开发必备技能，企业开发技术选型命中率>==90%==

    ![image-20210729171139088](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day01/assets/image-20210729171139088.png)

    **说明**:对于未使用Spring的项目一般都是些比较老的项目，大多都处于维护阶段。

* 从专业角度看

  * 随着时代发展，软件规模与功能都呈几何式增长，开发难度也在不断递增，该如何解决?
    * Spring可以==简化开发==，降低企业级开发的复杂性，使开发变得更简单快捷
  * 随着项目规模与功能的增长,遇到的问题就会增多，为了解决问题会引入更多的框架，这些框架如何协调工作?
    * Spring可以==框架整合==，高效整合其他技术，提高企业级应用开发与运行效率

  综上所述，==Spring是一款非常优秀而且功能强大的框架，不仅要学，而且还要学好。==

### 1.2 学什么?

从上面的介绍中，我们可以看到Spring框架主要的优势是在`简化开发`和`框架整合`上，至于如何实现就是咱们要学习Spring框架的主要内容:

* 简化开发: Spring框架中提供了两个大的核心技术，分别是:

  * ==IOC==
  * ==AOP==
    * ==事务处理==

   1.Spring的简化操作都是基于这两块内容,所以这也是Spring学习中最为重要的两个知识点。

   2.事务处理属于Spring中AOP的具体应用，可以简化项目中的事务管理，也是Spring技术中的一大亮点。

* 框架整合: Spring在框架整合这块已经做到了极致，它可以整合市面上几乎所有主流框架，比如:

  - ==MyBatis==
  - MyBatis-plus
  - Struts
  - Struts2
  - Hibernate
  - ……

  这些框架中，我们目前只学习了MyBatis，所以在Spring框架的学习中，主要是学习如何整合MyBatis。

  综上所述，对于Spring的学习，主要学习四块内容:

  ==(1)IOC,(2)整合Mybatis(IOC的具体应用)，(3)AOP,(4)声明式事务(AOP的具体应用)==

### 1.3 怎么学?

* 学习Spring框架设计思想
  * 对于Spring来说，它能迅速占领全球市场，不只是说它的某个功能比较强大，更重要是在它的`思想`上。
* 学习基础操作，思考操作与思想间的联系
  * 掌握了Spring的设计思想，然后就需要通过一些基础操作来思考操作与思想之间的关联关系
* 学习案例，熟练应用操作的同时，体会思想
  * 会了基础操作后，就需要通过大量案例来熟练掌握框架的具体应用，加深对设计思想的理解。

介绍完`为什么要学`、`学什么`和`怎么学`Spring框架后，大家需要重点掌握的是:

* Spring很优秀，需要认真重点的学习
* Spring的学习主线是IOC、AOP、声明式事务和整合MyBais

接下来，咱们就开始进入Spring框架的学习。

## 2，Spring相关概念

### 2.1 初识Spring

在这一节，主要通过以下两个点来了解下Spring:

#### 2.1.1 Spring家族

* 官网：https://spring.io，从官网我们可以大概了解到：

  * Spring能做什么:用以开发web、微服务以及分布式系统等,光这三块就已经占了JavaEE开发的九成多。
  * Spring并不是单一的一个技术，而是一个大家族，可以从官网的`Projects`中查看其包含的所有技术。

* Spring发展到今天已经形成了一种开发的生态圈,Spring提供了若干个项目,每个项目用于完成特定的功能。

  * Spring已形成了完整的生态圈，也就是说我们可以完全使用Spring技术完成整个项目的构建、设计与开发。

  * Spring有若干个项目，可以根据需要自行选择，把这些个项目组合起来，起了一个名称叫==全家桶==，如下图所示

    ![image-20210729171850181](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day01/assets/image-20210729171850181.png)

    **说明:**

    图中的图标都代表什么含义，可以进入`https://spring.io/projects`网站进行对比查看。

    这些技术并不是所有的都需要学习，额外需要重点关注`Spring Framework`、`SpringBoot`和`SpringCloud`:

    ![1629714811435](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day01/assets/1629714811435.png)

    * Spring Framework:Spring框架，是Spring中最早最核心的技术，也是所有其他技术的基础。
    * SpringBoot:Spring是来简化开发，而SpringBoot是来帮助Spring在简化的基础上能更快速进行开发。
    * SpringCloud:这个是用来做分布式之微服务架构的相关开发。

    除了上面的这三个技术外，还有很多其他的技术，也比较流行，如SpringData,SpringSecurity等，这些都可以被应用在我们的项目中。我们今天所学习的Spring其实指的是==Spring Framework==。

#### 2.1.2 了解Spring发展史

 接下来我们介绍下Spring Framework这个技术是如何来的呢?

![image-20210729171926576](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day01/assets/image-20210729171926576.png)

Spring发展史

* IBM(IT公司-国际商业机器公司)在1997年提出了EJB思想,早期的JAVAEE开发大都基于该思想。
* Rod Johnson(Java和J2EE开发领域的专家)在2002年出版的`Expert One-on-One J2EE Design and Development`,书中有阐述在开发中使用EJB该如何做。
* Rod Johnson在2004年出版的`Expert One-on-One J2EE Development without EJB`,书中提出了比EJB思想更高效的实现方案，并且在同年将方案进行了具体的落地实现，这个实现就是Spring1.0。
* 随着时间推移，版本不断更新维护，目前最新的是Spring5
  * Spring1.0是纯配置文件开发
  * Spring2.0为了简化开发引入了注解开发，此时是配置文件加注解的开发方式
  * Spring3.0已经可以进行纯注解开发，使开发效率大幅提升，我们的课程会以注解开发为主
  * Spring4.0根据JDK的版本升级对个别API进行了调整
  * Spring5.0已经全面支持JDK8，现在Spring最新的是5系列所以建议大家把JDK安装成1.8版

本节介绍了Spring家族与Spring的发展史，需要大家重点掌握的是:

* 今天所学的Spring其实是Spring家族中的Spring Framework
* Spring Framework是Spring家族中其他框架的底层基础，学好Spring可以为其他Spring框架的学习打好基础

### 2.2 Spring系统架构

前面我们说spring指的是Spring Framework,那么它其中都包含哪些内容以及我们该如何学习这个框架?

针对这些问题，我们将从`系统架构图`和`课程学习路线`来进行说明:

#### 2.2.1 系统架构图

* Spring Framework是Spring生态圈中最基础的项目，是其他项目的根基。

* Spring Framework的发展也经历了很多版本的变更，每个版本都有相应的调整

  ![image-20210729172153796](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day01/assets/image-20210729172153796.png)

* Spring Framework的5版本目前没有最新的架构图，而最新的是4版本，所以接下来主要研究的是4的架构图

  ![1629720945720](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day01/assets/1629720945720.png)

  (1)核心层

  * Core Container:核心容器，这个模块是Spring最核心的模块，其他的都需要依赖该模块

  (2)AOP层

  * AOP:面向切面编程，它依赖核心层容器，目的是==在不改变原有代码的前提下对其进行功能增强==
  * Aspects:AOP是思想,Aspects是对AOP思想的具体实现

  (3)数据层

  * Data Access:数据访问，Spring全家桶中有对数据访问的具体实现技术
  * Data Integration:数据集成，Spring支持整合其他的数据层解决方案，比如Mybatis
  * Transactions:事务，Spring中事务管理是Spring AOP的一个具体实现，也是后期学习的重点内容

  (4)Web层

  * 这一层的内容将在SpringMVC框架具体学习

  (5)Test层

  * Spring主要整合了Junit来完成单元测试和集成测试

#### 2.2.2 课程学习路线

介绍完Spring的体系结构后，从中我们可以得出对于Spring的学习主要包含四部分内容，分别是:

* ==Spring的IOC/DI==
* ==Spring的AOP==
* ==AOP的具体应用,事务管理==
* ==IOC/DI的具体应用,整合Mybatis==

![1629722300996](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day01/assets/1629722300996.png)

对于这节的内容，大家重点要记住的是Spring需要学习的四部分内容。接下来就从第一部分开始学起。

### 2.3 Spring核心概念

在Spring核心概念这部分内容中主要包含`IOC/DI`、`IOC容器`和`Bean`,那么问题就来了，这些都是什么呢?

#### 2.3.1 目前项目中的问题

要想解答这个问题，就需要先分析下目前咱们代码在编写过程中遇到的问题:

![1629723232339](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day01/assets/1629723232339.png)

(1)业务层需要调用数据层的方法，就需要在业务层new数据层的对象

(2)如果数据层的实现类发生变化，那么业务层的代码也需要跟着改变，发生变更后，都需要进行编译打包和重部署

(3)所以，现在代码在编写的过程中存在的问题是：==耦合度偏高==

针对这个问题，该如何解决呢?

![1629724206002](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day01/assets/1629724206002.png)

我们就想，如果能把框中的内容给去掉，不就可以降低依赖了么，但是又会引入新的问题，去掉以后程序能运行么?

答案肯定是不行，因为bookDao没有赋值为Null，强行运行就会出空指针异常。

所以现在的问题就是，业务层不想new对象，运行的时候又需要这个对象，该咋办呢?

针对这个问题，Spring就提出了一个解决方案:

* 使用对象时，在程序中不要主动使用new产生对象，转换为由==外部==提供对象

这种实现思就是Spring的一个核心概念

#### 2.3.2 IOC、IOC容器、Bean、DI

1. ==IOC（Inversion of Control）控制反转==

(1)什么是控制反转呢？

* 使用对象时，由主动new产生对象转换为由==外部==提供对象，此过程中对象创建控制权由程序转移到外部，此思想称为控制反转。
  * 业务层要用数据层的类对象，以前是自己`new`的
  * 现在自己不new了，交给`别人[外部]`来创建对象
  * `别人[外部]`就反转控制了数据层对象的创建权
  * 这种思想就是控制反转
  * 别人[外部]指定是什么呢?继续往下学

(2)Spring和IOC之间的关系是什么呢?

* Spring技术对IOC思想进行了实现
* Spring提供了一个容器，称为==IOC容器==，用来充当IOC思想中的"外部"
* IOC思想中的`别人[外部]`指的就是Spring的IOC容器

(3)IOC容器的作用以及内部存放的是什么?

* IOC容器负责对象的创建、初始化等一系列工作，其中包含了数据层和业务层的类对象
* 被创建或被管理的对象在IOC容器中统称为==Bean==
* IOC容器中放的就是一个个的Bean对象

(4)当IOC容器中创建好service和dao对象后，程序能正确执行么?

* 不行，因为service运行需要依赖dao对象
* IOC容器中虽然有service和dao对象
* 但是service对象和dao对象没有任何关系
* 需要把dao对象交给service,也就是说要绑定service和dao对象之间的关系

像这种在容器中建立对象与对象之间的绑定关系就要用到DI:

2. ==DI（Dependency Injection）依赖注入==

![1629735078619](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day01/assets/1629735078619.png)

(1)什么是依赖注入呢?

* 在容器中建立bean与bean之间的依赖关系的整个过程，称为依赖注入
  * 业务层要用数据层的类对象，以前是自己`new`的
  * 现在自己不new了，靠`别人[外部其实指的就是IOC容器]`来给注入进来
  * 这种思想就是依赖注入

(2)IOC容器中哪些bean之间要建立依赖关系呢?

* 这个需要程序员根据业务需求提前建立好关系，如业务层需要依赖数据层，service就要和dao建立依赖关系

介绍完Spring的IOC和DI的概念后，我们会发现这两个概念的最终目标就是:==充分解耦==，具体实现靠:

* 使用IOC容器管理bean（IOC)
* 在IOC容器内将有依赖关系的bean进行关系绑定（DI）
* 最终结果为:使用对象时不仅可以直接从IOC容器中获取，并且获取到的bean已经绑定了所有的依赖关系.

#### 2.3.3 核心概念小结

这节比较重要，重点要理解`什么是IOC/DI思想`、`什么是IOC容器`和`什么是Bean`：

(1)什么IOC/DI思想?

* IOC:控制反转，控制反转的是对象的创建权
* DI:依赖注入，绑定对象与对象之间的依赖关系

(2)什么是IOC容器?

Spring创建了一个容器用来存放所创建的对象，这个容器就叫IOC容器

(3)什么是Bean?

容器中所存放的一个个对象就叫Bean或Bean对象

## 3，入门案例

介绍完Spring的核心概念后，接下来我们得思考一个问题就是，Spring到底是如何来实现IOC和DI的，那接下来就通过一些简单的入门案例，来演示下具体实现过程:

### 3.1 IOC入门案例

对于入门案例，我们得先`分析思路`然后再`代码实现`，

#### 3.1.1 入门案例思路分析

(1)Spring是使用容器来管理bean对象的，那么管什么? 

* 主要管理项目中所使用到的类对象，比如(Service和Dao)

(2)如何将被管理的对象告知IOC容器?

* 使用配置文件

(3)被管理的对象交给IOC容器，要想从容器中获取对象，就先得思考如何获取到IOC容器?

* Spring框架提供相应的接口

(4)IOC容器得到后，如何从容器中获取bean?

* 调用Spring框架提供对应接口中的方法

(5)使用Spring导入哪些坐标?

* 用别人的东西，就需要在pom.xml添加对应的依赖

#### 3.1.2 入门案例代码实现

> 需求分析:将BookServiceImpl和BookDaoImpl交给Spring管理，并从容器中获取对应的bean对象进行方法调用。
>
> 1.创建Maven的java项目
>
> 2.pom.xml添加Spring的依赖jar包
>
> 3.创建BookService,BookServiceImpl，BookDao和BookDaoImpl四个类
>
> 4.resources下添加spring配置文件，并完成bean的配置
>
> 5.使用Spring提供的接口完成IOC容器的创建
>
> 6.从容器中获取对象进行方法调用





##### 步骤1:创建Maven项目

![1629734010072](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day01/assets/1629734010072.png)

##### 步骤2:添加Spring的依赖jar包

pom.xml

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-context</artifactId>
        <version>5.2.10.RELEASE</version>
    </dependency>
    <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
        <version>4.12</version>
        <scope>test</scope>
    </dependency>
</dependencies>
```

##### 步骤3:添加案例中需要的类

创建BookService,BookServiceImpl，BookDao和BookDaoImpl四个类

```java
public interface BookDao {
    public void save();
}
public class BookDaoImpl implements BookDao {
    public void save() {
        System.out.println("book dao save ...");
    }
}
public interface BookService {
    public void save();
}
public class BookServiceImpl implements BookService {
    private BookDao bookDao = new BookDaoImpl();
    public void save() {
        System.out.println("book service save ...");
        bookDao.save();
    }
}
```

##### 步骤4:添加spring配置文件

resources下添加spring配置文件applicationContext.xml，并完成bean的配置

![1629734336440](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day01/assets/1629734336440.png)

##### 步骤5:在配置文件中完成bean的配置

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
 
    <!--bean标签标示配置bean
    	id属性标示给bean起名字
    	class属性表示给bean定义类型
	-->
	<bean id="bookDao" class="com.itheima.dao.impl.BookDaoImpl"/>
    <bean id="bookService" class="com.itheima.service.impl.BookServiceImpl"/>

</beans>
```

**==注意事项：bean定义时id属性在同一个上下文中(配置文件)不能重复==**

##### 步骤6:获取IOC容器

使用Spring提供的接口完成IOC容器的创建，创建App类，编写main方法

```java
public class App {
    public static void main(String[] args) {
        //获取IOC容器
		ApplicationContext ctx = new ClassPathXmlApplicationContext("applicationContext.xml"); 
    }
}
```

##### 步骤7:从容器中获取对象进行方法调用

```java
public class App {
    public static void main(String[] args) {
        //获取IOC容器
		ApplicationContext ctx = new ClassPathXmlApplicationContext("applicationContext.xml"); 
//        BookDao bookDao = (BookDao) ctx.getBean("bookDao");
//        bookDao.save();
        BookService bookService = (BookService) ctx.getBean("bookService");
        bookService.save();
    }
}
```

##### 步骤8:运行程序

测试结果为：

![image-20210729184337603](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day01/assets/image-20210729184337603.png)

Spring的IOC入门案例已经完成，但是在`BookServiceImpl`的类中依然存在`BookDaoImpl`对象的new操作，它们之间的耦合度还是比较高，这块该如何解决，就需要用到下面的`DI:依赖注入`。

### 3.2 DI入门案例

对于DI的入门案例，我们依然先`分析思路`然后再`代码实现`，

#### 3.2.1 入门案例思路分析

(1)要想实现依赖注入，必须要基于IOC管理Bean

- DI的入门案例要依赖于前面IOC的入门案例

(2)Service中使用new形式创建的Dao对象是否保留?

- 需要删除掉，最终要使用IOC容器中的bean对象

(3)Service中需要的Dao对象如何进入到Service中?

- 在Service中提供方法，让Spring的IOC容器可以通过该方法传入bean对象

(4)Service与Dao间的关系如何描述?

- 使用配置文件

#### 3.2.2 入门案例代码实现

> 需求:基于IOC入门案例，在BookServiceImpl类中删除new对象的方式，使用Spring的DI完成Dao层的注入
>
> 1.删除业务层中使用new的方式创建的dao对象
>
> 2.在业务层提供BookDao的setter方法
>
> 3.在配置文件中添加依赖注入的配置
>
> 4.运行程序调用方法

##### 步骤1: 去除代码中的new

在BookServiceImpl类中，删除业务层中使用new的方式创建的dao对象

```java
public class BookServiceImpl implements BookService {
    //删除业务层中使用new的方式创建的dao对象
    private BookDao bookDao;

    public void save() {
        System.out.println("book service save ...");
        bookDao.save();
    }
}
```

##### 步骤2:为属性提供setter方法

在BookServiceImpl类中,为BookDao提供setter方法

```java
public class BookServiceImpl implements BookService {
    //删除业务层中使用new的方式创建的dao对象
    private BookDao bookDao;

    public void save() {
        System.out.println("book service save ...");
        bookDao.save();
    }
    //提供对应的set方法
    public void setBookDao(BookDao bookDao) {
        this.bookDao = bookDao;
    }
}

```

##### 步骤3:修改配置完成注入

在配置文件中添加依赖注入的配置

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
    <!--bean标签标示配置bean
    	id属性标示给bean起名字
    	class属性表示给bean定义类型
	-->
    <bean id="bookDao" class="com.itheima.dao.impl.BookDaoImpl"/>

    <bean id="bookService" class="com.itheima.service.impl.BookServiceImpl">
        <!--配置server与dao的关系-->
        <!--property标签表示配置当前bean的属性
        		name属性表示配置哪一个具体的属性
        		ref属性表示参照哪一个bean
		-->
        <property name="bookDao" ref="bookDao"/>
    </bean>

</beans>
```

==注意:配置中的两个bookDao的含义是不一样的==

* name="bookDao"中`bookDao`的作用是让Spring的IOC容器在获取到名称后，将首字母大写，前面加set找对应的`setBookDao()`方法进行对象注入
* ref="bookDao"中`bookDao`的作用是让Spring能在IOC容器中找到id为`bookDao`的Bean对象给`bookService`进行注入
* 综上所述，对应关系如下:

![1629736314989](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day01/assets/1629736314989.png)

##### 步骤4:运行程序

运行，测试结果为：

![image-20210729184337603](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day01/assets/image-20210729184337603.png)

## 4，IOC相关内容

通过前面两个案例，我们已经学习了`bean如何定义配置`，`DI如何定义配置`以及`容器对象如何获取`的内容，接下来主要是把这三块内容展开进行详细的讲解，深入的学习下这三部分的内容，首先是bean基础配置。

### 4.1 bean基础配置

对于bean的配置中，主要会讲解`bean基础配置`,`bean的别名配置`,`bean的作用范围配置`==(重点)==,这三部分内容：

#### 4.1.1 bean基础配置(id与class)

对于bean的基础配置，在前面的案例中已经使用过:

```
<bean id="" class=""/>
```

其中，bean标签的功能、使用方式以及id和class属性的作用，我们通过一张图来描述下

![image-20210729183500978](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day01/assets/image-20210729183500978.png)

这其中需要大家重点掌握的是:==bean标签的id和class属性的使用==。

**思考：**

* class属性能不能写接口如`BookDao`的类全名呢?

答案肯定是不行，因为接口是没办法创建对象的。

* 前面提过为bean设置id时，id必须唯一，但是如果由于命名习惯而产生了分歧后，该如何解决?

在解决这个问题之前，我们需要准备下开发环境，对于开发环境我们可以有两种解决方案:

* 使用前面IOC和DI的案例

* 重新搭建一个新的案例环境,目的是方便大家查阅代码

  * 搭建的内容和前面的案例是一样的，内容如下：

    ![1629769227068](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day01/assets/1629769227068.png)

#### 4.1.2 bean的name属性

环境准备好后，接下来就可以在这个环境的基础上来学习下bean的别名配置，

首先来看下别名的配置说明:

![image-20210729183558051](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day01/assets/image-20210729183558051.png)

##### 步骤1：配置别名

打开spring的配置文件applicationContext.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <!--name:为bean指定别名，别名可以有多个，使用逗号，分号，空格进行分隔-->
    <bean id="bookService" name="service service4 bookEbi" class="com.itheima.service.impl.BookServiceImpl">
        <property name="bookDao" ref="bookDao"/>
    </bean>

    <!--scope：为bean设置作用范围，可选值为单例singloton，非单例prototype-->
    <bean id="bookDao" name="dao" class="com.itheima.dao.impl.BookDaoImpl"/>
</beans>
```

**说明:Ebi全称Enterprise Business Interface，翻译为企业业务接口**

##### 步骤2:根据名称容器中获取bean对象

```java
public class AppForName {
    public static void main(String[] args) {
        ApplicationContext ctx = new ClassPathXmlApplicationContext("applicationContext.xml");
        //此处根据bean标签的id属性和name属性的任意一个值来获取bean对象
        BookService bookService = (BookService) ctx.getBean("service4");
        bookService.save();
    }
}
```

##### 步骤3:运行程序

测试结果为：

![image-20210729184337603](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day01/assets/image-20210729184337603.png)

==注意事项:==

* ​	Lbean依赖注入的ref属性指定bean，必须在容器中存在

  ![1629771744003](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day01/assets/1629771744003.png)

* 如果不存在,则会报错，如下:

  ![1629771880920](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day01/assets/1629771880920.png)

  这个错误大家需要特别关注下:

  ![1629771972886](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day01/assets/1629771972886.png)

  获取bean无论是通过id还是name获取，如果无法获取到，将抛出异常==NoSuchBeanDefinitionException==

#### 4.1.3 bean作用范围scope配置

关于bean的作用范围是bean属性配置的一个==重点==内容。

看到这个作用范围，我们就得思考bean的作用范围是来控制bean哪块内容的?

我们先来看下`bean作用范围的配置属性`:

![image-20210729183628138](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day01/assets/image-20210729183628138.png)

##### 4.1.3.1 验证IOC容器中对象是否为单例

###### 验证思路

​	同一个bean获取两次，将对象打印到控制台，看打印出的地址值是否一致。

###### 具体实现

* 创建一个AppForScope的类，在其main方法中来验证

  ```java
  public class AppForScope {
      public static void main(String[] args) {
          ApplicationContext ctx = new 
              ClassPathXmlApplicationContext("applicationContext.xml");
  
          BookDao bookDao1 = (BookDao) ctx.getBean("bookDao");
          BookDao bookDao2 = (BookDao) ctx.getBean("bookDao");
          System.out.println(bookDao1);
          System.out.println(bookDao2);
      }
  }
  ```

* 打印，观察控制台的打印结果

  ![1629772538893](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day01/assets/1629772538893.png)

* 结论:默认情况下，Spring创建的bean对象都是单例的

获取到结论后，问题就来了，那如果我想创建出来非单例的bean对象，该如何实现呢?

##### 4.1.3.2 配置bean为非单例

在Spring配置文件中，配置scope属性来实现bean的非单例创建

* 在Spring的配置文件中，修改`<bean>`的scope属性

  ```xml
  <bean id="bookDao" name="dao" class="com.itheima.dao.impl.BookDaoImpl" scope=""/>
  ```

* 将scope设置为`singleton`

  ```xml
  <bean id="bookDao" name="dao" class="com.itheima.dao.impl.BookDaoImpl" scope="singleton"/>
  ```

  运行AppForScope，打印看结果

  ![1629772538893](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day01/assets/1629772538893.png)

* 将scope设置为`prototype`

  ```
  <bean id="bookDao" name="dao" class="com.itheima.dao.impl.BookDaoImpl" scope="prototype"/>
  ```

  运行AppForScope，打印看结果

  ![1629772928714](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day01/assets/1629772928714.png)

* 结论，使用bean的`scope`属性可以控制bean的创建是否为单例：

  * `singleton`默认为单例
  * `prototype`为非单例

##### 4.1.3.3 scope使用后续思考

介绍完`scope`属性以后，我们来思考几个问题:

* 为什么bean默认为单例?
  * bean为单例的意思是在Spring的IOC容器中只会有该类的一个对象
  * bean对象只有一个就避免了对象的频繁创建与销毁，达到了bean对象的复用，性能高
* bean在容器中是单例的，会不会产生线程安全问题?
  * 如果对象是有状态对象，即该对象有成员变量可以用来存储数据的，
  * 因为所有请求线程共用一个bean对象，所以会存在线程安全问题。
  * 如果对象是无状态对象，即该对象没有成员变量没有进行数据存储的，
  * 因方法中的局部变量在方法调用完成后会被销毁，所以不会存在线程安全问题。
* 哪些bean对象适合交给容器进行管理?
  * 表现层对象
  * 业务层对象
  * 数据层对象
  * 工具对象
* 哪些bean对象不适合交给容器进行管理?
  * 封装实例的域对象，因为会引发线程安全问题，所以不适合。

#### 4.14 bean基础配置小结

关于bean的基础配置中，需要大家掌握以下属性:

![1631529887695](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day01/assets/1631529887695.png)

### 4.2 bean实例化

对象已经能交给Spring的IOC容器来创建了，但是容器是如何来创建对象的呢?

就需要研究下`bean的实例化过程`，在这块内容中主要解决两部分内容，分别是

* bean是如何创建的
* 实例化bean的三种方式，`构造方法`,`静态工厂`和`实例工厂`

在讲解这三种创建方式之前，我们需要先确认一件事:

bean本质上就是对象，对象在new的时候会使用构造方法完成，那创建bean也是使用构造方法完成的。

基于这个知识点出发，我们来验证spring中bean的三种创建方式，

#### 4.2.1 环境准备

为了方便大家阅读代码，重新准备个开发环境，

* 创建一个Maven项目
* pom.xml添加依赖
* resources下添加spring的配置文件applicationContext.xml

这些步骤和前面的都一致，大家可以快速的拷贝即可，最终项目的结构如下:

![1629775585694](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day01/assets/1629775585694.png)

#### 4.2.2 构造方法实例化

在上述的环境下，我们来研究下Spring中的第一种bean的创建方式`构造方法实例化`:

##### 步骤1:准备需要被创建的类

准备一个BookDao和BookDaoImpl类

```java
public interface BookDao {
    public void save();
}

public class BookDaoImpl implements BookDao {
    public void save() {
        System.out.println("book dao save ...");
    }

}
```

##### 步骤2:将类配置到Spring容器

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

	<bean id="bookDao" class="com.itheima.dao.impl.BookDaoImpl"/>

</beans>
```

##### 步骤3:编写运行程序

```java
public class AppForInstanceBook {
    public static void main(String[] args) {
        ApplicationContext ctx = new 
            ClassPathXmlApplicationContext("applicationContext.xml");
        BookDao bookDao = (BookDao) ctx.getBean("bookDao");
        bookDao.save();

    }
}
```

##### 步骤4:类中提供构造函数测试

在BookDaoImpl类中添加一个无参构造函数，并打印一句话，方便观察结果。

```java
public class BookDaoImpl implements BookDao {
    public BookDaoImpl() {
        System.out.println("book dao constructor is running ....");
    }
    public void save() {
        System.out.println("book dao save ...");
    }

}
```

运行程序，如果控制台有打印构造函数中的输出，说明Spring容器在创建对象的时候也走的是构造函数

![1629775972507](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day01/assets/1629775972507.png)

##### 步骤5:将构造函数改成private测试

```java
public class BookDaoImpl implements BookDao {
    private BookDaoImpl() {
        System.out.println("book dao constructor is running ....");
    }
    public void save() {
        System.out.println("book dao save ...");
    }

}
```

运行程序，能执行成功,说明内部走的依然是构造函数,能访问到类中的私有构造方法,显而易见Spring底层用的是反射

![1629775972507](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day01/assets/1629775972507.png)

##### 步骤6:构造函数中添加一个参数测试

```java
public class BookDaoImpl implements BookDao {
    private BookDaoImpl(int i) {
        System.out.println("book dao constructor is running ....");
    }
    public void save() {
        System.out.println("book dao save ...");
    }

}
```

运行程序，

程序会报错，说明Spring底层使用的是类的无参构造方法。

![1629776331499](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day01/assets/1629776331499.png)

#### 4.2.3 分析Spring的错误信息

接下来，我们主要研究下Spring的报错信息来学一学如阅读。

* 错误信息从下往上依次查看，因为上面的错误大都是对下面错误的一个包装，最核心错误是在最下面
* Caused by: java.lang.NoSuchMethodException: com.itheima.dao.impl.BookDaoImpl.`<init>`()
  * Caused by 翻译为`引起`，即出现错误的原因
  * java.lang.NoSuchMethodException:抛出的异常为`没有这样的方法异常`
  * com.itheima.dao.impl.BookDaoImpl.`<init>`():哪个类的哪个方法没有被找到导致的异常，`<init>`()指定是类的构造方法，即该类的无参构造方法

如果最后一行错误获取不到错误信息，接下来查看第二层:

Caused by: org.springframework.beans.BeanInstantiationException: Failed to instantiate [com.itheima.dao.impl.BookDaoImpl]: No default constructor found; nested exception is java.lang.NoSuchMethodException: com.itheima.dao.impl.BookDaoImpl.`<init>`()

* nested:嵌套的意思，后面的异常内容和最底层的异常是一致的
* Caused by: org.springframework.beans.BeanInstantiationException: Failed to instantiate [com.itheima.dao.impl.BookDaoImpl]: No default constructor found; 
  * Caused by: `引发`
  * BeanInstantiationException:翻译为`bean实例化异常`
  * No default constructor found:没有一个默认的构造函数被发现

看到这其实错误已经比较明显，给大家个练习，把倒数第三层的错误分析下吧:

Exception in thread "main" org.springframework.beans.factory.BeanCreationException: Error creating bean with name 'bookDao' defined in class path resource [applicationContext.xml]: Instantiation of bean failed; nested exception is org.springframework.beans.BeanInstantiationException: Failed to instantiate [com.itheima.dao.impl.BookDaoImpl]: No default constructor found; nested exception is java.lang.NoSuchMethodException: com.itheima.dao.impl.BookDaoImpl.`<init>`()。

至此，关于Spring的构造方法实例化就已经学习完了，因为每一个类默认都会提供一个无参构造函数，所以其实真正在使用这种方式的时候，我们什么也不需要做。这也是我们以后比较常用的一种方式。

#### 4.2.4 静态工厂实例化

接下来研究Spring中的第二种bean的创建方式`静态工厂实例化`:

##### 4.2.4.1 工厂方式创建bean

在讲这种方式之前，我们需要先回顾一个知识点是使用工厂来创建对象的方式:

(1)准备一个OrderDao和OrderDaoImpl类

```java
public interface OrderDao {
    public void save();
}

public class OrderDaoImpl implements OrderDao {
    public void save() {
        System.out.println("order dao save ...");
    }
}
```

(2)创建一个工厂类OrderDaoFactory并提供一个==静态方法==

```java
//静态工厂创建对象
public class OrderDaoFactory {
    public static OrderDao getOrderDao(){
        return new OrderDaoImpl();
    }
}
```

(3)编写AppForInstanceOrder运行类，在类中通过工厂获取对象

```java
public class AppForInstanceOrder {
    public static void main(String[] args) {
        //通过静态工厂创建对象
        OrderDao orderDao = OrderDaoFactory.getOrderDao();
        orderDao.save();
    }
}
```

(4)运行后，可以查看到结果

![1629786862329](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day01/assets/1629786862329.png)

如果代码中对象是通过上面的这种方式来创建的，如何将其交给Spring来管理呢?

##### 4.2.4.2 静态工厂实例化

这就要用到Spring中的静态工厂实例化的知识了，具体实现步骤为:

(1)在spring的配置文件application.properties中添加以下内容:

```xml
<bean id="orderDao" class="com.itheima.factory.OrderDaoFactory" factory-method="getOrderDao"/>
```

class:工厂类的类全名

factory-mehod:具体工厂类中创建对象的方法名

对应关系如下图:

![image-20210729195248948](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day01/assets/image-20210729195248948.png)

(2)在AppForInstanceOrder运行类，使用从IOC容器中获取bean的方法进行运行测试

```java
public class AppForInstanceOrder {
    public static void main(String[] args) {
        ApplicationContext ctx = new ClassPathXmlApplicationContext("applicationContext.xml");

        OrderDao orderDao = (OrderDao) ctx.getBean("orderDao");

        orderDao.save();

    }
}
```

(3)运行后，可以查看到结果

![1629786862329](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day01/assets/1629786862329.png)

看到这，可能有人会问了，你这种方式在工厂类中不也是直接new对象的，和我自己直接new没什么太大的区别，而且静态工厂的方式反而更复杂，这种方式的意义是什么?

主要的原因是:

* 在工厂的静态方法中，我们除了new对象还可以做其他的一些业务操作，这些操作必不可少,如:

```java
public class OrderDaoFactory {
    public static OrderDao getOrderDao(){
        System.out.println("factory setup....");//模拟必要的业务操作
        return new OrderDaoImpl();
    }
}
```

之前new对象的方式就无法添加其他的业务内容，重新运行，查看结果:

![1629788036885](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day01/assets/1629788036885.png)

介绍完静态工厂实例化后，这种方式一般是用来兼容早期的一些老系统，所以==了解为主==。

#### 4.2.5 实例工厂与FactoryBean

接下来继续来研究Spring的第三种bean的创建方式`实例工厂实例化`:

##### 4.2.3.1 环境准备

(1)准备一个UserDao和UserDaoImpl类

```java
public interface UserDao {
    public void save();
}

public class UserDaoImpl implements UserDao {

    public void save() {
        System.out.println("user dao save ...");
    }
}
```

(2)创建一个工厂类OrderDaoFactory并提供一个普通方法，注意此处和静态工厂的工厂类不一样的地方是方法不是静态方法

```java
public class UserDaoFactory {
    public UserDao getUserDao(){
        return new UserDaoImpl();
    }
}
```

(3)编写AppForInstanceUser运行类，在类中通过工厂获取对象

```java
public class AppForInstanceUser {
    public static void main(String[] args) {
        //创建实例工厂对象
        UserDaoFactory userDaoFactory = new UserDaoFactory();
        //通过实例工厂对象创建对象
        UserDao userDao = userDaoFactory.getUserDao();
        userDao.save();
}
```

(4)运行后，可以查看到结果

![1629788769436](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day01/assets/1629788769436.png)

对于上面这种实例工厂的方式如何交给Spring管理呢?

##### 4.2.3.2 实例工厂实例化

具体实现步骤为:

(1)在spring的配置文件中添加以下内容:

```xml
<bean id="userFactory" class="com.itheima.factory.UserDaoFactory"/>
<bean id="userDao" factory-method="getUserDao" factory-bean="userFactory"/>
```

实例化工厂运行的顺序是:

* 创建实例化工厂对象,对应的是第一行配置

* 调用对象中的方法来创建bean，对应的是第二行配置

  * factory-bean:工厂的实例对象

  * factory-method:工厂对象中的具体创建对象的方法名,对应关系如下:

    ![image-20210729200203249](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day01/assets/image-20210729200203249.png)

factory-mehod:具体工厂类中创建对象的方法名

(2)在AppForInstanceUser运行类，使用从IOC容器中获取bean的方法进行运行测试

```java
public class AppForInstanceUser {
    public static void main(String[] args) {
        ApplicationContext ctx = new 
            ClassPathXmlApplicationContext("applicationContext.xml");
        UserDao userDao = (UserDao) ctx.getBean("userDao");
        userDao.save();
    }
}
```

(3)运行后，可以查看到结果

![1629788769436](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day01/assets/1629788769436.png)

实例工厂实例化的方式就已经介绍完了，配置的过程还是比较复杂，所以Spring为了简化这种配置方式就提供了一种叫`FactoryBean`的方式来简化开发。

##### 4.2.3.3 FactoryBean的使用

具体的使用步骤为:

(1)创建一个UserDaoFactoryBean的类，实现FactoryBean接口，重写接口的方法

```java
public class UserDaoFactoryBean implements FactoryBean<UserDao> {
    //代替原始实例工厂中创建对象的方法
    public UserDao getObject() throws Exception {
        return new UserDaoImpl();
    }
    //返回所创建类的Class对象
    public Class<?> getObjectType() {
        return UserDao.class;
    }
}
```

(2)在Spring的配置文件中进行配置

```xml
<bean id="userDao" class="com.itheima.factory.UserDaoFactoryBean"/>
```

(3)AppForInstanceUser运行类不用做任何修改，直接运行

![1629788769436](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day01/assets/1629788769436.png)

这种方式在Spring去整合其他框架的时候会被用到，所以这种方式需要大家理解掌握。

查看源码会发现，FactoryBean接口其实会有三个方法，分别是:

```java
T getObject() throws Exception;

Class<?> getObjectType();

default boolean isSingleton() {
		return true;
}
```

方法一:getObject()，被重写后，在方法中进行对象的创建并返回

方法二:getObjectType(),被重写后，主要返回的是被创建类的Class对象

方法三:没有被重写，因为它已经给了默认值，从方法名中可以看出其作用是设置对象是否为单例，默认true，从意思上来看，我们猜想默认应该是单例，如何来验证呢?

思路很简单，就是从容器中获取该对象的多个值，打印到控制台，查看是否为同一个对象。

```java
public class AppForInstanceUser {
    public static void main(String[] args) {
        ApplicationContext ctx = new 
            ClassPathXmlApplicationContext("applicationContext.xml");
        UserDao userDao1 = (UserDao) ctx.getBean("userDao");
        UserDao userDao2 = (UserDao) ctx.getBean("userDao");
        System.out.println(userDao1);
        System.out.println(userDao2);
    }
}
```

打印结果，如下:

![1629790070607](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day01/assets/1629790070607.png)

通过验证，会发现默认是单例，那如果想改成单例具体如何实现?

只需要将isSingleton()方法进行重写，修改返回为false，即可

```java
//FactoryBean创建对象
public class UserDaoFactoryBean implements FactoryBean<UserDao> {
    //代替原始实例工厂中创建对象的方法
    public UserDao getObject() throws Exception {
        return new UserDaoImpl();
    }

    public Class<?> getObjectType() {
        return UserDao.class;
    }

    public boolean isSingleton() {
        return false;
    }
}
```

重新运行AppForInstanceUser，查看结果

![1629790197860](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day01/assets/1629790197860.png)

从结果中可以看出现在已经是非单例了，但是一般情况下我们都会采用单例，也就是采用默认即可。所以isSingleton()方法一般不需要进行重写。

#### 4.2.6 bean实例化小结

通过这一节的学习，需要掌握:

(1)bean是如何创建的呢?

```
构造方法
```

(2)Spring的IOC实例化对象的三种方式分别是:

* 构造方法(常用)
* 静态工厂(了解)
* 实例工厂(了解)
  * FactoryBean(实用)

这些方式中，重点掌握`构造方法`和`FactoryBean`即可。

需要注意的一点是，构造方法在类中默认会提供，但是如果重写了构造方法，默认的就会消失，在使用的过程中需要注意，如果需要重写构造方法，最好把默认的构造方法也重写下。

### 4.3 bean的生命周期

关于bean的相关知识还有最后一个是`bean的生命周期`,对于生命周期，我们主要围绕着`bean生命周期控制`来讲解:

* 首先理解下什么是生命周期?
  * 从创建到消亡的完整过程,例如人从出生到死亡的整个过程就是一个生命周期。
* bean生命周期是什么?
  * bean对象从创建到销毁的整体过程。
* bean生命周期控制是什么?
  * 在bean创建后到销毁前做一些事情。

现在我们面临的问题是如何在bean的创建之后和销毁之前把我们需要添加的内容添加进去。

#### 4.3.1 环境准备

还是老规矩，为了方便大家后期代码的阅读，我们重新搭建下环境:

- 创建一个Maven项目
- pom.xml添加依赖
- resources下添加spring的配置文件applicationContext.xml

这些步骤和前面的都一致，大家可以快速的拷贝即可，最终项目的结构如下:

![1629791473409](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day01/assets/1629791473409.png)

(1)项目中添加BookDao、BookDaoImpl、BookService和BookServiceImpl类

```java
public interface BookDao {
    public void save();
}

public class BookDaoImpl implements BookDao {
    public void save() {
        System.out.println("book dao save ...");
    }
}

public interface BookService {
    public void save();
}

public class BookServiceImpl implements BookService{
    private BookDao bookDao;

    public void setBookDao(BookDao bookDao) {
        this.bookDao = bookDao;
    }

    public void save() {
        System.out.println("book service save ...");
        bookDao.save();
    }
}
```

(2)resources下提供spring的配置文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="bookDao" class="com.itheima.dao.impl.BookDaoImpl"/>
</beans>
```

(3)编写AppForLifeCycle运行类，加载Spring的IOC容器，并从中获取对应的bean对象

```java
public class AppForLifeCycle {
    public static void main( String[] args ) {
        ApplicationContext ctx = new 
        	ClassPathXmlApplicationContext("applicationContext.xml");
        BookDao bookDao = (BookDao) ctx.getBean("bookDao");
        bookDao.save();
    }
}
```

#### 4.3.2 生命周期设置

接下来，在上面这个环境中来为BookDao添加生命周期的控制方法，具体的控制有两个阶段:

* bean创建之后，想要添加内容，比如用来初始化需要用到资源
* bean销毁之前，想要添加内容，比如用来释放用到的资源

##### 步骤1:添加初始化和销毁方法

针对这两个阶段，我们在BooDaoImpl类中分别添加两个方法，==方法名任意==

```java
public class BookDaoImpl implements BookDao {
    public void save() {
        System.out.println("book dao save ...");
    }
    //表示bean初始化对应的操作
    public void init(){
        System.out.println("init...");
    }
    //表示bean销毁前对应的操作
    public void destory(){
        System.out.println("destory...");
    }
}
```

##### 步骤2:配置生命周期

在配置文件添加配置，如下:

```xml
<bean id="bookDao" class="com.itheima.dao.impl.BookDaoImpl" init-method="init" destroy-method="destory"/>
```

##### 步骤3:运行程序

运行AppForLifeCycle打印结果为:

![1629792339889](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day01/assets/1629792339889.png)

从结果中可以看出，init方法执行了，但是destroy方法却未执行，这是为什么呢?

* Spring的IOC容器是运行在JVM中
* 运行main方法后,JVM启动,Spring加载配置文件生成IOC容器,从容器获取bean对象，然后调方法执行
* main方法执行完后，JVM退出，这个时候IOC容器中的bean还没有来得及销毁就已经结束了
* 所以没有调用对应的destroy方法

知道了出现问题的原因，具体该如何解决呢?

#### 4.3.3 close关闭容器

* ApplicationContext中没有close方法

* 需要将ApplicationContext更换成ClassPathXmlApplicationContext

  ```java
  ClassPathXmlApplicationContext ctx = new 
      ClassPathXmlApplicationContext("applicationContext.xml");
  ```

* 调用ctx的close()方法

  ```
  ctx.close();
  ```

* 运行程序，就能执行destroy方法的内容

  ![1629792857608](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day01/assets/1629792857608.png)

#### 4.3.4 注册钩子关闭容器

* 在容器未关闭之前，提前设置好回调函数，让JVM在退出之前回调此函数来关闭容器

* 调用ctx的registerShutdownHook()方法

  ```
  ctx.registerShutdownHook();
  ```

  **注意:**registerShutdownHook在ApplicationContext中也没有

* 运行后，查询打印结果

  ![1629792857608](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day01/assets/1629792857608.png)

两种方式介绍完后，close和registerShutdownHook选哪个?

相同点:这两种都能用来关闭容器

不同点:close()是在调用的时候关闭，registerShutdownHook()是在JVM退出前调用关闭。

分析上面的实现过程，会发现添加初始化和销毁方法，即需要编码也需要配置，实现起来步骤比较多也比较乱。

Spring提供了两个接口来完成生命周期的控制，好处是可以不用再进行配置`init-method`和`destroy-method`

接下来在BookServiceImpl完成这两个接口的使用:

修改BookServiceImpl类，添加两个接口`InitializingBean`， `DisposableBean`并实现接口中的两个方法`afterPropertiesSet`和`destroy`

```java
public class BookServiceImpl implements BookService, InitializingBean, DisposableBean {
    private BookDao bookDao;
    public void setBookDao(BookDao bookDao) {
        this.bookDao = bookDao;
    }
    public void save() {
        System.out.println("book service save ...");
        bookDao.save(); 
    }
    public void destroy() throws Exception {
        System.out.println("service destroy");
    }
    public void afterPropertiesSet() throws Exception {
        System.out.println("service init");
    }
}
```

重新运行AppForLifeCycle类，

![1629794527419](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day01/assets/1629794527419.png)

那第二种方式的实现，我们也介绍完了。

**小细节**

* 对于InitializingBean接口中的afterPropertiesSet方法，翻译过来为`属性设置之后`。

* 对于BookServiceImpl来说，bookDao是它的一个属性

* setBookDao方法是Spring的IOC容器为其注入属性的方法

* 思考:afterPropertiesSet和setBookDao谁先执行?

  * 从方法名分析，猜想应该是setBookDao方法先执行

  * 验证思路，在setBookDao方法中添加一句话

    ```java
    public void setBookDao(BookDao bookDao) {
            System.out.println("set .....");
            this.bookDao = bookDao;
        }
    
    ```

  * 重新运行AppForLifeCycle，打印结果如下:

    ![1629794928636](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day01/assets/1629794928636.png)

    验证的结果和我们猜想的结果是一致的，所以初始化方法会在类中属性设置之后执行。

#### 4.3.5 bean生命周期小结

(1)关于Spring中对bean生命周期控制提供了两种方式:

* 在配置文件中的bean标签中添加`init-method`和`destroy-method`属性
* 类实现`InitializingBean`与`DisposableBean`接口，这种方式了解下即可。

(2)对于bean的生命周期控制在bean的整个生命周期中所处的位置如下:

* 初始化容器
  * 1.创建对象(内存分配)
  * 2.执行构造方法
  * 3.执行属性注入(set操作)
  * ==4.执行bean初始化方法==
* 使用bean
  * 1.执行业务操作
* 关闭/销毁容器
  * ==1.执行bean销毁方法==

(3)关闭容器的两种方式:

* ConfigurableApplicationContext是ApplicationContext的子类
  * close()方法
  * registerShutdownHook()方法

## 5，DI相关内容

前面我们已经完成了bean相关操作的讲解，接下来就进入第二个大的模块`DI依赖注入`，首先来介绍下Spring中有哪些注入方式?

我们先来思考

* 向一个类中传递数据的方式有几种?
  * 普通方法(set方法)
  * 构造方法
* 依赖注入描述了在容器中建立bean与bean之间的依赖关系的过程，如果bean运行需要的是数字或字符串呢?
  * 引用类型
  * 简单类型(基本数据类型与String)

Spring就是基于上面这些知识点，为我们提供了两种注入方式，分别是:

* setter注入
  * 简单类型
  * ==引用类型==
* 构造器注入
  * 简单类型
  * 引用类型

依赖注入的方式已经介绍完，接下来挨个学习下:

### 5.1 setter注入

1. 对于setter方式注入引用类型的方式之前已经学习过，快速回顾下:

* 在bean中定义引用类型属性，并提供可访问的==set==方法

```java
public class BookServiceImpl implements BookService {
    private BookDao bookDao;
    public void setBookDao(BookDao bookDao) {
        this.bookDao = bookDao;
    }
}
```

* 配置中使用==property==标签==ref==属性注入引用类型对象

```xml
<bean id="bookService" class="com.itheima.service.impl.BookServiceImpl">
	<property name="bookDao" ref="bookDao"/>
</bean>

<bean id="bookDao" class="com.itheima.dao.imipl.BookDaoImpl"/>
```

#### 5.1.1 环境准备

为了更好的学习下面内容，我们依旧准备一个新环境:

- 创建一个Maven项目
- pom.xml添加依赖
- resources下添加spring的配置文件

这些步骤和前面的都一致，大家可以快速的拷贝即可，最终项目的结构如下:

![1629799214191](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day01/assets/1629799214191.png)

(1)项目中添加BookDao、BookDaoImpl、UserDao、UserDaoImpl、BookService和BookServiceImpl类

```java
public interface BookDao {
    public void save();
}

public class BookDaoImpl implements BookDao {
    public void save() {
        System.out.println("book dao save ...");
    }
}
public interface UserDao {
    public void save();
}
public class UserDaoImpl implements UserDao {
    public void save() {
        System.out.println("user dao save ...");
    }
}

public interface BookService {
    public void save();
}

public class BookServiceImpl implements BookService{
    private BookDao bookDao;

    public void setBookDao(BookDao bookDao) {
        this.bookDao = bookDao;
    }

    public void save() {
        System.out.println("book service save ...");
        bookDao.save();
    }
}
```

(2)resources下提供spring的配置文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="bookDao" class="com.itheima.dao.impl.BookDaoImpl"/>
    <bean id="bookService" class="com.itheima.service.impl.BookServiceImpl">
        <property name="bookDao" ref="bookDao"/>
    </bean>
</beans>
```

(3)编写AppForDISet运行类，加载Spring的IOC容器，并从中获取对应的bean对象

```java
public class AppForDISet {
    public static void main( String[] args ) {
        ApplicationContext ctx = new ClassPathXmlApplicationContext("applicationContext.xml");
        BookService bookService = (BookService) ctx.getBean("bookService");
        bookService.save();
    }
}
```

接下来，在上面这个环境中来完成setter注入的学习:

#### 5.1.2 注入引用数据类型

> 需求:在bookServiceImpl对象中注入userDao
>
> 1.在BookServiceImpl中声明userDao属性
>
> 2.为userDao属性提供setter方法
>
> 3.在配置文件中使用property标签注入

##### 步骤1:声明属性并提供setter方法

在BookServiceImpl中声明userDao属性，并提供setter方法

```java
public class BookServiceImpl implements BookService{
    private BookDao bookDao;
    private UserDao userDao;
    
    public void setUserDao(UserDao userDao) {
        this.userDao = userDao;
    }
    public void setBookDao(BookDao bookDao) {
        this.bookDao = bookDao;
    }

    public void save() {
        System.out.println("book service save ...");
        bookDao.save();
        userDao.save();
    }
}
```

##### 步骤2:配置文件中进行注入配置

在applicationContext.xml配置文件中使用property标签注入

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="bookDao" class="com.itheima.dao.impl.BookDaoImpl"/>
    <bean id="userDao" class="com.itheima.dao.impl.UserDaoImpl"/>
    <bean id="bookService" class="com.itheima.service.impl.BookServiceImpl">
        <property name="bookDao" ref="bookDao"/>
        <property name="userDao" ref="userDao"/>
    </bean>
</beans>
```

##### 步骤3:运行程序

运行AppForDISet类，查看结果，说明userDao已经成功注入。

![1629799873386](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day01/assets/1629799873386.png)

#### 5.1.3 注入简单数据类型

> 需求：给BookDaoImpl注入一些简单数据类型的数据
>
> 参考引用数据类型的注入，我们可以推出具体的步骤为:
>
> 1.在BookDaoImpl类中声明对应的简单数据类型的属性
>
> 2.为这些属性提供对应的setter方法
>
> 3.在applicationContext.xml中配置

**思考:**

引用类型使用的是`<property name="" ref=""/>`,简单数据类型还是使用ref么?

ref是指向Spring的IOC容器中的另一个bean对象的，对于简单数据类型，没有对应的bean对象，该如何配置?

##### 步骤1:声明属性并提供setter方法

在BookDaoImpl类中声明对应的简单数据类型的属性,并提供对应的setter方法

```java
public class BookDaoImpl implements BookDao {

    private String databaseName;
    private int connectionNum;

    public void setConnectionNum(int connectionNum) {
        this.connectionNum = connectionNum;
    }

    public void setDatabaseName(String databaseName) {
        this.databaseName = databaseName;
    }

    public void save() {
        System.out.println("book dao save ..."+databaseName+","+connectionNum);
    }
}
```

##### 步骤2:配置文件中进行注入配置

在applicationContext.xml配置文件中使用property标签注入

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="bookDao" class="com.itheima.dao.impl.BookDaoImpl">
        <property name="databaseName" value="mysql"/>
     	<property name="connectionNum" value="10"/>
    </bean>
    <bean id="userDao" class="com.itheima.dao.impl.UserDaoImpl"/>
    <bean id="bookService" class="com.itheima.service.impl.BookServiceImpl">
        <property name="bookDao" ref="bookDao"/>
        <property name="userDao" ref="userDao"/>
    </bean>
</beans>
```

**说明:**

value:后面跟的是简单数据类型，对于参数类型，Spring在注入的时候会自动转换，但是不能写成

```xml
<property name="connectionNum" value="abc"/>
```

这样的话，spring在将`abc`转换成int类型的时候就会报错。

##### 步骤3:运行程序

运行AppForDISet类，查看结果，说明userDao已经成功注入。

![1629800324721](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day01/assets/1629800324721.png)

**注意:**两个property注入标签的顺序可以任意。

对于setter注入方式的基本使用就已经介绍完了，

* 对于引用数据类型使用的是`<property name="" ref=""/>`
* 对于简单数据类型使用的是`<property name="" value=""/>`

### 5.2 构造器注入

#### 5.2.1 环境准备

构造器注入也就是构造方法注入，学习之前，还是先准备下环境:

- 创建一个Maven项目
- pom.xml添加依赖
- resources下添加spring的配置文件

这些步骤和前面的都一致，大家可以快速的拷贝即可，最终项目的结构如下:

![1629800748639](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day01/assets/1629800748639.png)

(1)项目中添加BookDao、BookDaoImpl、UserDao、UserDaoImpl、BookService和BookServiceImpl类

```java
public interface BookDao {
    public void save();
}

public class BookDaoImpl implements BookDao {
    
    private String databaseName;
    private int connectionNum;
    
    public void save() {
        System.out.println("book dao save ...");
    }
}
public interface UserDao {
    public void save();
}
public class UserDaoImpl implements UserDao {
    public void save() {
        System.out.println("user dao save ...");
    }
}

public interface BookService {
    public void save();
}

public class BookServiceImpl implements BookService{
    private BookDao bookDao;

    public void setBookDao(BookDao bookDao) {
        this.bookDao = bookDao;
    }

    public void save() {
        System.out.println("book service save ...");
        bookDao.save();
    }
}
```

(2)resources下提供spring的配置文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="bookDao" class="com.itheima.dao.impl.BookDaoImpl"/>
    <bean id="bookService" class="com.itheima.service.impl.BookServiceImpl">
        <property name="bookDao" ref="bookDao"/>
    </bean>
</beans>
```

(3)编写AppForDIConstructor运行类，加载Spring的IOC容器，并从中获取对应的bean对象

```java
public class AppForDIConstructor {
    public static void main( String[] args ) {
        ApplicationContext ctx = new ClassPathXmlApplicationContext("applicationContext.xml");
        BookService bookService = (BookService) ctx.getBean("bookService");
        bookService.save();
    }
}
```

#### 5.2.2 构造器注入引用数据类型

接下来，在上面这个环境中来完成构造器注入的学习:

> 需求：将BookServiceImpl类中的bookDao修改成使用构造器的方式注入。
>
> 1.将bookDao的setter方法删除掉
>
> 2.添加带有bookDao参数的构造方法
>
> 3.在applicationContext.xml中配置

##### 步骤1:删除setter方法并提供构造方法

在BookServiceImpl类中将bookDao的setter方法删除掉,并添加带有bookDao参数的构造方法

```java
public class BookServiceImpl implements BookService{
    private BookDao bookDao;

    public BookServiceImpl(BookDao bookDao) {
        this.bookDao = bookDao;
    }

    public void save() {
        System.out.println("book service save ...");
        bookDao.save();
    }
}
```

##### 步骤2:配置文件中进行配置构造方式注入

在applicationContext.xml中配置

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="bookDao" class="com.itheima.dao.impl.BookDaoImpl"/>
    <bean id="bookService" class="com.itheima.service.impl.BookServiceImpl">
        <constructor-arg name="bookDao" ref="bookDao"/>
    </bean>
</beans>
```

**说明:**

标签<constructor-arg>中

* name属性对应的值为构造函数中方法形参的参数名，必须要保持一致。

* ref属性指向的是spring的IOC容器中其他bean对象。

##### 步骤3：运行程序

运行AppForDIConstructor类，查看结果，说明bookDao已经成功注入。

![1629802656916](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day01/assets/1629802656916.png)

#### 5.2.3 构造器注入多个引用数据类型

> 需求:在BookServiceImpl使用构造函数注入多个引用数据类型，比如userDao
>
> 1.声明userDao属性
>
> 2.生成一个带有bookDao和userDao参数的构造函数
>
> 3.在applicationContext.xml中配置注入

##### 步骤1:提供多个属性的构造函数

在BookServiceImpl声明userDao并提供多个参数的构造函数

```java
public class BookServiceImpl implements BookService{
    private BookDao bookDao;
    private UserDao userDao;

    public BookServiceImpl(BookDao bookDao,UserDao userDao) {
        this.bookDao = bookDao;
        this.userDao = userDao;
    }

    public void save() {
        System.out.println("book service save ...");
        bookDao.save();
        userDao.save();
    }
}
```

步骤2:配置文件中配置多参数注入

在applicationContext.xml中配置注入

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="bookDao" class="com.itheima.dao.impl.BookDaoImpl"/>
    <bean id="userDao" class="com.itheima.dao.impl.UserDaoImpl"/>
    <bean id="bookService" class="com.itheima.service.impl.BookServiceImpl">
        <constructor-arg name="bookDao" ref="bookDao"/>
        <constructor-arg name="userDao" ref="userDao"/>
    </bean>
</beans>
```

**说明:**这两个`<contructor-arg>`的配置顺序可以任意

##### 步骤3:运行程序

运行AppForDIConstructor类，查看结果，说明userDao已经成功注入。

![1629802697318](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day01/assets/1629802697318.png)

#### 5.2.4 构造器注入多个简单数据类型

> 需求:在BookDaoImpl中，使用构造函数注入databaseName和connectionNum两个参数。
>
> 参考引用数据类型的注入，我们可以推出具体的步骤为:
>
> 1.提供一个包含这两个参数的构造方法
>
> 2.在applicationContext.xml中进行注入配置

##### 步骤1:添加多个简单属性并提供构造方法

修改BookDaoImpl类，添加构造方法

```java
public class BookDaoImpl implements BookDao {
    private String databaseName;
    private int connectionNum;

    public BookDaoImpl(String databaseName, int connectionNum) {
        this.databaseName = databaseName;
        this.connectionNum = connectionNum;
    }

    public void save() {
        System.out.println("book dao save ..."+databaseName+","+connectionNum);
    }
}
```

##### 步骤2:配置完成多个属性构造器注入

在applicationContext.xml中进行注入配置

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="bookDao" class="com.itheima.dao.impl.BookDaoImpl">
        <constructor-arg name="databaseName" value="mysql"/>
        <constructor-arg name="connectionNum" value="666"/>
    </bean>
    <bean id="userDao" class="com.itheima.dao.impl.UserDaoImpl"/>
    <bean id="bookService" class="com.itheima.service.impl.BookServiceImpl">
        <constructor-arg name="bookDao" ref="bookDao"/>
        <constructor-arg name="userDao" ref="userDao"/>
    </bean>
</beans>
```

**说明:**这两个`<contructor-arg>`的配置顺序可以任意

##### 步骤3:运行程序

运行AppForDIConstructor类，查看结果

![1629803111769](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day01/assets/1629803111769.png)

上面已经完成了构造函数注入的基本使用，但是会存在一些问题:

![1629803529598](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day01/assets/1629803529598.png)

* 当构造函数中方法的参数名发生变化后，配置文件中的name属性也需要跟着变
* 这两块存在紧耦合，具体该如何解决?

在解决这个问题之前，需要提前说明的是，这个参数名发生变化的情况并不多，所以上面的还是比较主流的配置方式，下面介绍的，大家都以了解为主。

方式一:删除name属性，添加type属性，按照类型注入

```xml
<bean id="bookDao" class="com.itheima.dao.impl.BookDaoImpl">
    <constructor-arg type="int" value="10"/>
    <constructor-arg type="java.lang.String" value="mysql"/>
</bean>
```

* 这种方式可以解决构造函数形参名发生变化带来的耦合问题
* 但是如果构造方法参数中有类型相同的参数，这种方式就不太好实现了

方式二:删除type属性，添加index属性，按照索引下标注入，下标从0开始

```xml
<bean id="bookDao" class="com.itheima.dao.impl.BookDaoImpl">
    <constructor-arg index="1" value="100"/>
    <constructor-arg index="0" value="mysql"/>
</bean>
```

* 这种方式可以解决参数类型重复问题
* 但是如果构造方法参数顺序发生变化后，这种方式又带来了耦合问题

介绍完两种参数的注入方式，具体我们该如何选择呢?

1. 强制依赖使用构造器进行，使用setter注入有概率不进行注入导致null对象出现
   * 强制依赖指对象在创建的过程中必须要注入指定的参数
2. 可选依赖使用setter注入进行，灵活性强
   * 可选依赖指对象在创建过程中注入的参数可有可无
3. Spring框架倡导使用构造器，第三方框架内部大多数采用构造器注入的形式进行数据初始化，相对严谨
4. 如果有必要可以两者同时使用，使用构造器注入完成强制依赖的注入，使用setter注入完成可选依赖的注入
5. 实际开发过程中还要根据实际情况分析，如果受控对象没有提供setter方法就必须使用构造器注入
6. **==自己开发的模块推荐使用setter注入==**

这节中主要讲解的是Spring的依赖注入的实现方式:

* setter注入

  * 简单数据类型

    ```xml
    <bean ...>
    	<property name="" value=""/>
    </bean>
    ```

  * 引用数据类型

    ```xml
    <bean ...>
    	<property name="" ref=""/>
    </bean>
    ```

* 构造器注入

  * 简单数据类型

    ```xml
    <bean ...>
    	<constructor-arg name="" index="" type="" value=""/>
    </bean>
    ```

  * 引用数据类型

    ```xml
    <bean ...>
    	<constructor-arg name="" index="" type="" ref=""/>
    </bean>
    ```

* 依赖注入的方式选择上

  * 建议使用setter注入
  * 第三方技术根据情况选择

### 5.3 自动配置

前面花了大量的时间把Spring的注入去学习了下，总结起来就一个字==麻烦==。

问:麻烦在哪?

答:配置文件的编写配置上。

问:有更简单方式么?

答:有，自动配置

什么是自动配置以及如何实现自动配置，就是接下来要学习的内容：

#### 5.3.1 什么是依赖自动装配?

* IoC容器根据bean所依赖的资源在容器中自动查找并注入到bean中的过程称为自动装配

#### 5.3.2 自动装配方式有哪些?

* ==按类型（常用）==
* 按名称
* 按构造方法
* 不启用自动装配

#### 5.3.3 准备下案例环境

- 创建一个Maven项目
- pom.xml添加依赖
- resources下添加spring的配置文件

这些步骤和前面的都一致，大家可以快速的拷贝即可，最终项目的结构如下:

![1629805387647](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day01/assets/1629805387647.png)

(1)项目中添加BookDao、BookDaoImpl、BookService和BookServiceImpl类

```java
public interface BookDao {
    public void save();
}

public class BookDaoImpl implements BookDao {
    
    private String databaseName;
    private int connectionNum;
    
    public void save() {
        System.out.println("book dao save ...");
    }
}
public interface BookService {
    public void save();
}

public class BookServiceImpl implements BookService{
    private BookDao bookDao;

    public void setBookDao(BookDao bookDao) {
        this.bookDao = bookDao;
    }

    public void save() {
        System.out.println("book service save ...");
        bookDao.save();
    }
}
```

(2)resources下提供spring的配置文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="bookDao" class="com.itheima.dao.impl.BookDaoImpl"/>
    <bean id="bookService" class="com.itheima.service.impl.BookServiceImpl">
        <property name="bookDao" ref="bookDao"/>
    </bean>
</beans>
```

(3)编写AppForAutoware运行类，加载Spring的IOC容器，并从中获取对应的bean对象

```java
public class AppForAutoware {
    public static void main( String[] args ) {
        ApplicationContext ctx = new ClassPathXmlApplicationContext("applicationContext.xml");
        BookService bookService = (BookService) ctx.getBean("bookService");
        bookService.save();
    }
}
```

#### 5.3.4 完成自动装配的配置

接下来，在上面这个环境中来完成`自动装配`的学习:

自动装配只需要修改applicationContext.xml配置文件即可:

(1)将`<property>`标签删除

(2)在`<bean>`标签中添加autowire属性

首先来实现按照类型注入的配置

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean class="com.itheima.dao.impl.BookDaoImpl"/>
    <!--autowire属性：开启自动装配，通常使用按类型装配-->
    <bean id="bookService" class="com.itheima.service.impl.BookServiceImpl" autowire="byType"/>

</beans>
```

==注意事项:==

* 需要注入属性的类中对应属性的setter方法不能省略
* 被注入的对象必须要被Spring的IOC容器管理
* 按照类型在Spring的IOC容器中如果找到多个对象，会报`NoUniqueBeanDefinitionException`

一个类型在IOC中有多个对象，还想要注入成功，这个时候就需要按照名称注入，配置方式为:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean class="com.itheima.dao.impl.BookDaoImpl"/>
    <!--autowire属性：开启自动装配，通常使用按类型装配-->
    <bean id="bookService" class="com.itheima.service.impl.BookServiceImpl" autowire="byName"/>

</beans>
```

==注意事项:==

* 按照名称注入中的名称指的是什么?

  ![1629806856156](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day01/assets/1629806856156.png)

  * bookDao是private修饰的，外部类无法直接方法
  * 外部类只能通过属性的set方法进行访问
  * 对外部类来说，setBookDao方法名，去掉set后首字母小写是其属性名
    * 为什么是去掉set首字母小写?
    * 这个规则是set方法生成的默认规则，set方法的生成是把属性名首字母大写前面加set形成的方法名
  * 所以按照名称注入，其实是和对应的set方法有关，但是如果按照标准起名称，属性名和set对应的名是一致的

* 如果按照名称去找对应的bean对象，找不到则注入Null

* 当某一个类型在IOC容器中有多个对象，按照名称注入只找其指定名称对应的bean对象，不会报错 

两种方式介绍完后，以后用的更多的是==按照类型==注入。

最后对于依赖注入，需要注意一些其他的配置特征:

1. 自动装配用于引用类型依赖注入，不能对简单类型进行操作
2. 使用按类型装配时（byType）必须保障容器中相同类型的bean唯一，推荐使用
3. 使用按名称装配时（byName）必须保障容器中具有指定名称的bean，因变量名与配置耦合，不推荐使用
4. 自动装配优先级低于setter注入与构造器注入，同时出现时自动装配配置失效



byName：必须保证bean中有同类中等待注入的变量同名，耦合度较高



### 5.4 集合注入

前面我们已经能完成引入数据类型和简单数据类型的注入，但是还有一种数据类型==集合==，集合中既可以装简单数据类型也可以装引用数据类型，对于集合，在Spring中该如何注入呢?

先来回顾下，常见的集合类型有哪些?

* 数组
* List
* Set
* Map
* Properties

针对不同的集合类型，该如何实现注入呢?

#### 5.4.1 环境准备

- 创建一个Maven项目
- pom.xml添加依赖
- resources下添加spring的配置文件applicationContext.xml

这些步骤和前面的都一致，大家可以快速的拷贝即可，最终项目的结构如下:

![1629807579330](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day01/assets/1629807579330.png)

(1)项目中添加添加BookDao、BookDaoImpl类

```java
public interface BookDao {
    public void save();
}

public class BookDaoImpl implements BookDao {
    
public class BookDaoImpl implements BookDao {

    private int[] array;

    private List<String> list;

    private Set<String> set;

    private Map<String,String> map;

    private Properties properties;

     public void save() {
        System.out.println("book dao save ...");

        System.out.println("遍历数组:" + Arrays.toString(array));

        System.out.println("遍历List" + list);

        System.out.println("遍历Set" + set);

        System.out.println("遍历Map" + map);

        System.out.println("遍历Properties" + properties);
    }
	//setter....方法省略，自己使用工具生成
}
```

(2)resources下提供spring的配置文件，applicationContext.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="bookDao" class="com.itheima.dao.impl.BookDaoImpl"/>
</beans>
```

(3)编写AppForDICollection运行类，加载Spring的IOC容器，并从中获取对应的bean对象

```java
public class AppForDICollection {
    public static void main( String[] args ) {
        ApplicationContext ctx = new ClassPathXmlApplicationContext("applicationContext.xml");
        BookDao bookDao = (BookDao) ctx.getBean("bookDao");
        bookDao.save();
    }
}
```

接下来，在上面这个环境中来完成`集合注入`的学习:

下面的所以配置方式，都是在bookDao的bean标签中使用<property>进行注入

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="bookDao" class="com.itheima.dao.impl.BookDaoImpl">
        
    </bean>
</beans>
```

#### 5.4.2 注入数组类型数据

```xml
<property name="array">
    <array>
        <value>100</value>
        <value>200</value>
        <value>300</value>
    </array>
</property>
```

#### 5.4.3 注入List类型数据

```xml
<property name="list">
    <list>
        <value>itcast</value>
        <value>itheima</value>
        <value>boxuegu</value>
        <value>chuanzhihui</value>
    </list>
</property>
```

#### 5.4.4 注入Set类型数据

```xml
<property name="set">
    <set>
        <value>itcast</value>
        <value>itheima</value>
        <value>boxuegu</value>
        <value>boxuegu</value>
    </set>
</property>
```

#### 5.4.5 注入Map类型数据

```xml
<property name="map">
    <map>
        <entry key="country" value="china"/>
        <entry key="province" value="henan"/>
        <entry key="city" value="kaifeng"/>
    </map>
</property>
```

#### 5.4.6 注入Properties类型数据

```xml
<property name="properties">
    <props>
        <prop key="country">china</prop>
        <prop key="province">henan</prop>
        <prop key="city">kaifeng</prop>
    </props>
</property>
```

配置完成后，运行下看结果:

![1629808046783](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day01/assets/1629808046783.png)

**说明：**

* property标签表示setter方式注入，构造方式注入constructor-arg标签内部也可以写`<array>`、`<list>`、`<set>`、`<map>`、`<props>`标签
* List的底层也是通过数组实现的，所以`<list>`和`<array>`标签是可以混用
* 集合中要添加引用类型，只需要把`<value>`标签改成`<ref>`标签，这种方式用的比较少



# Spring_day02

**今日目标**

> * 掌握IOC/DI配置管理第三方bean
> * 掌握IOC/DI的注解开发
> * 掌握IOC/DI注解管理第三方bean
> * 完成Spring与Mybatis及Junit的整合开发

## 1，IOC/DI配置管理第三方bean

前面所讲的知识点都是基于我们自己写的类，现在如果有需求让我们去管理第三方jar包中的类，该如何管理?

### 1.1 案例:数据源对象管理

在这一节中，我们将通过一个案例来学习下对于第三方bean该如何进行配置管理。

以后我们会用到很多第三方的bean,本次案例将使用咱们前面提到过的数据源`Druid(德鲁伊)`和`C3P0`来配置学习下。

#### 1.1.1 环境准备

学习之前，先来准备下案例环境:

* 创建一个Maven项目

  ![1629860338328](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day02/assets/1629860338328.png)

* pom.xml添加依赖

  ```xml
  <dependencies>
      <dependency>
          <groupId>org.springframework</groupId>
          <artifactId>spring-context</artifactId>
          <version>5.2.10.RELEASE</version>
      </dependency>
  </dependencies>
  ```

* resources下添加spring的配置文件applicationContext.xml

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <beans xmlns="http://www.springframework.org/schema/beans"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="
              http://www.springframework.org/schema/beans
              http://www.springframework.org/schema/beans/spring-beans.xsd">
  
  </beans>
  ```

* 编写一个运行类App

  ```java
  public class App {
      public static void main(String[] args) {
          ApplicationContext ctx = new ClassPathXmlApplicationContext("applicationContext.xml");
      }
  }
  ```

#### 1.1.2 思路分析

在上述环境下，我们来对数据源进行配置管理，先来分析下思路:

> 需求:使用Spring的IOC容器来管理Druid连接池对象
>
> 1.使用第三方的技术，需要在pom.xml添加依赖
>
> 2.在配置文件中将【第三方的类】制作成一个bean，让IOC容器进行管理
>
> 3.数据库连接需要基础的四要素`驱动`、`连接`、`用户名`和`密码`，【如何注入】到对应的bean中
>
> 4.从IOC容器中获取对应的bean对象，将其打印到控制台查看结果

**思考:**

* 第三方的类指的是什么?
* 如何注入数据库连接四要素?

#### 1.1.3 实现Druid管理

带着这两个问题，把下面的案例实现下:

##### 步骤1:导入`druid`的依赖

pom.xml中添加依赖

```xml
<dependency>
    <groupId>com.alibaba</groupId>
    <artifactId>druid</artifactId>
    <version>1.1.16</version>
</dependency>
```

##### 步骤2:配置第三方bean

在applicationContext.xml配置文件中添加`DruidDataSource`的配置

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="
            http://www.springframework.org/schema/beans
            http://www.springframework.org/schema/beans/spring-beans.xsd">
	<!--管理DruidDataSource对象-->
    <bean class="com.alibaba.druid.pool.DruidDataSource">
        <property name="driverClassName" value="com.mysql.jdbc.Driver"/>
        <property name="url" value="jdbc:mysql://localhost:3306/spring_db"/>
        <property name="username" value="root"/>
        <property name="password" value="root"/>
    </bean>
</beans>
```

**说明:**

* driverClassName:数据库驱动
* url:数据库连接地址
* username:数据库连接用户名
* password:数据库连接密码
* 数据库连接的四要素要和自己使用的数据库信息一致。

##### 步骤3:从IOC容器中获取对应的bean对象

```java
public class App {
    public static void main(String[] args) {
       ApplicationContext ctx = new ClassPathXmlApplicationContext("applicationContext.xml");
       DataSource dataSource = (DataSource) ctx.getBean("dataSource");
       System.out.println(dataSource);
    }
}
```

##### 步骤4:运行程序

打印如下结果: 说明第三方bean对象已经被spring的IOC容器进行管理

![1629887733081](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day02/assets/1629887733081.png)

做完案例后，我们可以将刚才思考的两个问题答案说下:

- 第三方的类指的是什么?

  ```
  DruidDataSource
  ```

- 如何注入数据库连接四要素?

  ```
  setter注入
  ```

#### 1.1.4 实现C3P0管理

完成了DruidDataSource的管理，接下来我们再来加深下练习，这次我们来管理`C3P0`数据源，具体的实现步骤是什么呢?

>需求:使用Spring的IOC容器来管理C3P0连接池对象
>
>实现方案和上面基本一致，重点要关注管理的是哪个bean对象`?

##### 步骤1:导入`C3P0`的依赖

pom.xml中添加依赖

```xml
<dependency>
    <groupId>c3p0</groupId>
    <artifactId>c3p0</artifactId>
    <version>0.9.1.2</version>
</dependency>
```

**对于新的技术，不知道具体的坐标该如何查找?**

* 直接百度搜索

* 从mvn的仓库`https://mvnrepository.com/`中进行搜索

  ![1629888540286](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day02/assets/1629888540286.png)

##### 步骤2:配置第三方bean

在applicationContext.xml配置文件中添加配置

```xml
<bean id="dataSource" class="com.mchange.v2.c3p0.ComboPooledDataSource">
    <property name="driverClass" value="com.mysql.jdbc.Driver"/>
    <property name="jdbcUrl" value="jdbc:mysql://localhost:3306/spring_db"/>
    <property name="user" value="root"/>
    <property name="password" value="root"/>
    <property name="maxPoolSize" value="1000"/>
</bean>
```

**==注意:==**

* ComboPooledDataSource的属性是通过setter方式进行注入
* 想注入属性就需要在ComboPooledDataSource类或其上层类中有提供属性对应的setter方法
* C3P0的四个属性和Druid的四个属性是不一样的

##### 步骤3:运行程序

程序会报错，错误如下

![1629889170229](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day02/assets/1629889170229.png)

报的错为==ClassNotFoundException==,翻译出来是`类没有发现的异常`，具体的类为`com.mysql.jdbc.Driver`。错误的原因是缺少mysql的驱动包。

分析出错误的原因，具体的解决方案就比较简单，只需要在pom.xml把驱动包引入即可。

```xml
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>5.1.47</version>
</dependency>
```

添加完mysql的驱动包以后，再次运行App,就可以打印出结果:

![1629903845404](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day02/assets/1629903845404.png)

**注意：**

* 数据连接池在配置属性的时候，除了可以注入数据库连接四要素外还可以配置很多其他的属性，具体都有哪些属性用到的时候再去查，一般配置基础的四个，其他都有自己的默认值
* Druid和C3P0在没有导入mysql驱动包的前提下，一个没报错一个报错，说明Druid在初始化的时候没有去加载驱动，而C3P0刚好相反
* Druid程序运行虽然没有报错，但是当调用DruidDataSource的getConnection()方法获取连接的时候，也会报找不到驱动类的错误

### 1.2 加载properties文件

上节中我们已经完成两个数据源`druid`和`C3P0`的配置，但是其中包含了一些问题，我们来分析下:

* 这两个数据源中都使用到了一些固定的常量如数据库连接四要素，把这些值写在Spring的配置文件中不利于后期维护
* 需要将这些值提取到一个外部的properties配置文件中
* Spring框架如何从配置文件中读取属性值来配置就是接下来要解决的问题。

问题提出来后，具体该如何实现?

#### 1.2.1 第三方bean属性优化

##### 1.2.1.1 实现思路

> 需求:将数据库连接四要素提取到properties配置文件，spring来加载配置信息并使用这些信息来完成属性注入。
>
> 1.在resources下创建一个jdbc.properties(文件的名称可以任意)
>
> 2.将数据库连接四要素配置到配置文件中
>
> 3.在Spring的配置文件中加载properties文件
>
> 4.使用加载到的值实现属性注入
>
> 其中第3，4步骤是需要大家重点关注，具体是如何实现。

##### 1.2.1.2 实现步骤

###### 步骤1:准备properties配置文件

resources下创建一个jdbc.properties文件,并添加对应的属性键值对

```properties
jdbc.driver=com.mysql.jdbc.Driver
jdbc.url=jdbc:mysql://127.0.0.1:3306/spring_db
jdbc.username=root
jdbc.password=root
```

###### 步骤2:开启`context`命名空间

在applicationContext.xml中开`context`命名空间

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="
            http://www.springframework.org/schema/beans
            http://www.springframework.org/schema/beans/spring-beans.xsd
            http://www.springframework.org/schema/context
            http://www.springframework.org/schema/context/spring-context.xsd">
</beans>
```

###### 步骤3:加载properties配置文件

在配置文件中使用`context`命名空间下的标签来加载properties配置文件

```xml
<context:property-placeholder location="jdbc.properties"/>
```

###### 步骤4:完成属性注入

使用`${key}`来读取properties配置文件中的内容并完成属性注入

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="
            http://www.springframework.org/schema/beans
            http://www.springframework.org/schema/beans/spring-beans.xsd
            http://www.springframework.org/schema/context
            http://www.springframework.org/schema/context/spring-context.xsd">
    
    <context:property-placeholder location="jdbc.properties"/>
    <bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource">
        <property name="driverClassName" value="${jdbc.driver}"/>
        <property name="url" value="${jdbc.url}"/>
        <property name="username" value="${jdbc.username}"/>
        <property name="password" value="${jdbc.password}"/>
    </bean>
</beans>
```

至此，读取外部properties配置文件中的内容就已经完成。

#### 1.2.2 读取单个属性

##### 1.2.2.1 实现思路

对于上面的案例，效果不是很明显，我们可以换个案例来演示下:

> 需求:从properties配置文件中读取key为name的值，并将其注入到BookDao中并在save方法中进行打印。
>
> 1.在项目中添加BookDao和BookDaoImpl类
>
> 2.为BookDaoImpl添加一个name属性并提供setter方法
>
> 3.在jdbc.properties中添加数据注入到bookDao中打印方便查询结果
>
> 4.在applicationContext.xml添加配置完成配置文件加载、属性注入(${key})

##### 1.2.2.2 实现步骤

###### 步骤1:在项目中添对应的类

BookDao和BookDaoImpl类，并在BookDaoImpl类中添加`name`属性与setter方法

```java
public interface BookDao {
    public void save();
}

public class BookDaoImpl implements BookDao {
    private String name;

    public void setName(String name) {
        this.name = name;
    }

    public void save() {
        System.out.println("book dao save ..." + name);
    }
}
```

###### 步骤2:完成配置文件的读取与注入

在applicationContext.xml添加配置，`bean的配置管理`、`读取外部properties`、`依赖注入`:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="
            http://www.springframework.org/schema/beans
            http://www.springframework.org/schema/beans/spring-beans.xsd
            http://www.springframework.org/schema/context
            http://www.springframework.org/schema/context/spring-context.xsd">
    
    <context:property-placeholder location="jdbc.properties"/>
    
    <bean id="bookDao" class="com.itheima.dao.impl.BookDaoImpl">
        <property name="name" value="${jdbc.driver}"/>
    </bean>
</beans>
```

###### 步骤3:运行程序

在App类中，从IOC容器中获取bookDao对象，调用方法，查看值是否已经被获取到并打印控制台

```java
public class App {
    public static void main(String[] args) throws Exception{
        ApplicationContext ctx = new ClassPathXmlApplicationContext("applicationContext.xml");
        BookDao bookDao = (BookDao) ctx.getBean("bookDao");
        bookDao.save();

    }
}
```

![1629975492444](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day02/assets/1629975492444.png)

##### 1.2.2.3 注意事项

至此，读取properties配置文件中的内容就已经完成，但是在使用的时候，有些注意事项:

* 问题一:键值对的key为`username`引发的问题

  1.在properties中配置键值对的时候，如果key设置为`username`

  ```
  username=root666
  ```

  2.在applicationContext.xml注入该属性

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <beans xmlns="http://www.springframework.org/schema/beans"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xmlns:context="http://www.springframework.org/schema/context"
         xsi:schemaLocation="
              http://www.springframework.org/schema/beans
              http://www.springframework.org/schema/beans/spring-beans.xsd
              http://www.springframework.org/schema/context
              http://www.springframework.org/schema/context/spring-context.xsd">
      
      <context:property-placeholder location="jdbc.properties"/>
      
      <bean id="bookDao" class="com.itheima.dao.impl.BookDaoImpl">
          <property name="name" value="${username}"/>
      </bean>
  </beans>
  ```

  3.运行后，在控制台打印的却不是`root666`，而是自己电脑的用户名

  ![1629975934694](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day02/assets/1629975934694.png)

  4.出现问题的原因是`<context:property-placeholder/>`标签会加载系统的环境变量，而且环境变量的值会被优先加载，如何查看系统的环境变量?

  ```java
  public static void main(String[] args) throws Exception{
      Map<String, String> env = System.getenv();
      System.out.println(env);
  }
  ```

  大家可以自行运行，在打印出来的结果中会有一个USERNAME=XXX[自己电脑的用户名称]

  5.解决方案

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <beans xmlns="http://www.springframework.org/schema/beans"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xmlns:context="http://www.springframework.org/schema/context"
         xsi:schemaLocation="
              http://www.springframework.org/schema/beans
              http://www.springframework.org/schema/beans/spring-beans.xsd
              http://www.springframework.org/schema/context
              http://www.springframework.org/schema/context/spring-context.xsd">
      
      <context:property-placeholder location="jdbc.properties" system-properties-mode="NEVER"/>
  </beans>
  ```

  system-properties-mode:设置为NEVER,表示不加载系统属性，就可以解决上述问题。

  当然还有一个解决方案就是避免使用`username`作为属性的`key`。

* 问题二:当有多个properties配置文件需要被加载，该如何配置?

  1.调整下配置文件的内容，在resources下添加`jdbc.properties`,`jdbc2.properties`,内容如下:

  jdbc.properties

  ```properties
  jdbc.driver=com.mysql.jdbc.Driver
  jdbc.url=jdbc:mysql://127.0.0.1:3306/spring_db
  jdbc.username=root
  jdbc.password=root
  ```

  jdbc2.properties

  ```properties
  username=root666
  ```

  2.修改applicationContext.xml

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <beans xmlns="http://www.springframework.org/schema/beans"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xmlns:context="http://www.springframework.org/schema/context"
         xsi:schemaLocation="
              http://www.springframework.org/schema/beans
              http://www.springframework.org/schema/beans/spring-beans.xsd
              http://www.springframework.org/schema/context
              http://www.springframework.org/schema/context/spring-context.xsd">
      <!--方式一 -->
      <context:property-placeholder location="jdbc.properties,jdbc2.properties" system-properties-mode="NEVER"/>
      <!--方式二-->
      <context:property-placeholder location="*.properties" system-properties-mode="NEVER"/>
      <!--方式三 -->
      <context:property-placeholder location="classpath:*.properties" system-properties-mode="NEVER"/>
      <!--方式四-->
      <context:property-placeholder location="classpath*:*.properties" system-properties-mode="NEVER"/>
  </beans>	
  ```

  **说明:**

  * 方式一:可以实现，如果配置文件多的话，每个都需要配置
  * 方式二:`*.properties`代表所有以properties结尾的文件都会被加载，可以解决方式一的问题，但是不标准
  * 方式三:标准的写法，`classpath:`代表的是从根路径下开始查找，但是只能查询当前项目的根路径
  * 方式四:不仅可以加载当前项目还可以加载当前项目所依赖的所有项目的根路径下的properties配置文件

#### 1.2.3 加载properties文件小结

  本节主要讲解的是properties配置文件的加载，需要掌握的内容有:

  * 如何开启`context`命名空间

    ![1629980280952](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day02/assets/1629980280952.png)

  * 如何加载properties配置文件

    ```xml
    <context:property-placeholder location="" system-properties-mode="NEVER"/>
    ```

  * 如何在applicationContext.xml引入properties配置文件中的值

    ```
    ${key}
    ```

## 2，核心容器

前面已经完成bean与依赖注入的相关知识学习，接下来我们主要学习的是IOC容器中的==核心容器==。

这里所说的核心容器，大家可以把它简单的理解为`ApplicationContext`，前面虽然已经用到过，但是并没有系统的学习，接下来咱们从以下几个问题入手来学习下容器的相关知识:

* 如何创建容器?
* 创建好容器后，如何从容器中获取bean对象?
* 容器类的层次结构是什么?
* BeanFactory是什么?

### 2.1 环境准备

在学习和解决上述问题之前，先来准备下案例环境:

* 创建一个Maven项目

* pom.xml添加Spring的依赖

  ```xml
  <dependencies>
      <dependency>
          <groupId>org.springframework</groupId>
          <artifactId>spring-context</artifactId>
          <version>5.2.10.RELEASE</version>
      </dependency>
  </dependencies>
  ```

* resources下添加applicationContext.xml

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <beans xmlns="http://www.springframework.org/schema/beans"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="
              http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
      <bean id="bookDao" class="com.itheima.dao.impl.BookDaoImpl"/>
  </beans>
  ```

* 添加BookDao和BookDaoImpl类

  ```java
  public interface BookDao {
      public void save();
  }
  public class BookDaoImpl implements BookDao {
      public void save() {
          System.out.println("book dao save ..." );
      }
  }
  ```

* 创建运行类App

  ```java
  public class App {
      public static void main(String[] args) {
          ApplicationContext ctx = new ClassPathXmlApplicationContext("applicationContext.xml");
          BookDao bookDao = (BookDao) ctx.getBean("bookDao");
          bookDao.save();
      }
  }
  ```

最终创建好的项目结构如下:

![1629982672522](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day02/assets/1629982672522.png)

### 2.2 容器

#### 2.2.1 容器的创建方式

案例中创建`ApplicationContext`的方式为:

```java
ApplicationContext ctx = new ClassPathXmlApplicationContext("applicationContext.xml");
```

这种方式翻译为:==类路径下的XML配置文件==

除了上面这种方式，Spring还提供了另外一种创建方式为:

```java
ApplicationContext ctx = new FileSystemXmlApplicationContext("applicationContext.xml");
```

这种方式翻译为:==文件系统下的XML配置文件==

使用这种方式，运行，会出现如下错误:

![1629983245121](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day02/assets/1629983245121.png)

从错误信息中能发现，这种方式是从项目路径下开始查找`applicationContext.xml`配置文件的，所以需要将其修改为:

```java
ApplicationContext ctx = new FileSystemXmlApplicationContext("D:\\workspace\\spring\\spring_10_container\\src\\main\\resources\\applicationContext.xml"); 
```

**说明:**大家练习的时候，写自己的具体路径。

这种方式虽能实现，但是当项目的位置发生变化后,代码也需要跟着改,耦合度较高,不推荐使用。

#### 2.2.2 Bean的三种获取方式

方式一，就是目前案例中获取的方式:

```java
BookDao bookDao = (BookDao) ctx.getBean("bookDao");
```

这种方式存在的问题是每次获取的时候都需要进行类型转换，有没有更简单的方式呢?

方式二：

```
BookDao bookDao = ctx.getBean("bookDao"，BookDao.class);
```

这种方式可以解决类型强转问题，但是参数又多加了一个，相对来说没有简化多少。

方式三:

```
BookDao bookDao = ctx.getBean(BookDao.class);
```

这种方式就类似我们之前所学习依赖注入中的按类型注入。必须要确保IOC容器中该类型对应的bean对象只能有一个。

#### 2.2.3 容器类层次结构

(1)在IDEA中双击`shift`,输入BeanFactory

![1629985148294](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day02/assets/1629985148294.png)

(2)点击进入BeanFactory类，ctrl+h,就能查看到如下结构的层次关系

![1629984980781](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day02/assets/1629984980781.png)

从图中可以看出，容器类也是从无到有根据需要一层层叠加上来的，大家重点理解下这种设计思想。

#### 2.2.4 BeanFactory的使用

使用BeanFactory来创建IOC容器的具体实现方式为:

```java
public class AppForBeanFactory {
    public static void main(String[] args) {
        Resource resources = new ClassPathResource("applicationContext.xml");
        BeanFactory bf = new XmlBeanFactory(resources);
        BookDao bookDao = bf.getBean(BookDao.class);
        bookDao.save();
    }
}
```

为了更好的看出`BeanFactory`和`ApplicationContext`之间的区别，在BookDaoImpl添加如下构造函数:

```java
public class BookDaoImpl implements BookDao {
    public BookDaoImpl() {
        System.out.println("constructor");
    }
    public void save() {
        System.out.println("book dao save ..." );
    }
}
```

如果不去获取bean对象，打印会发现：

* BeanFactory是延迟加载，只有在获取bean对象的时候才会去创建

* ApplicationContext是立即加载，容器加载的时候就会创建bean对象

* ApplicationContext要想成为延迟加载，只需要按照如下方式进行配置

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <beans xmlns="http://www.springframework.org/schema/beans"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="
              http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
      <bean id="bookDao" class="com.itheima.dao.impl.BookDaoImpl"  lazy-init="true"/>
  </beans>
  ```

**小结**

这一节中所讲的知识点包括:

* 容器创建的两种方式

  * ClassPathXmlApplicationContext[掌握]
  * FileSystemXmlApplicationContext[知道即可]

* 获取Bean的三种方式

  * getBean("名称"):需要类型转换
  * getBean("名称",类型.class):多了一个参数
  * getBean(类型.class):容器中不能有多个该类的bean对象

  上述三种方式，各有各的优缺点，用哪个都可以。

* 容器类层次结构

  * 只需要知晓容器的最上级的父接口为 BeanFactory即可

* BeanFactory

  * 使用BeanFactory创建的容器是延迟加载
  * 使用ApplicationContext创建的容器是立即加载
  * 具体BeanFactory如何创建只需要了解即可。

### 2.2 核心容器总结

这节中没有新的知识点，只是对前面知识的一个大总结，共包含如下内容:

#### 2.2.1 容器相关

- BeanFactory是IoC容器的顶层接口，初始化BeanFactory对象时，加载的bean延迟加载
- ApplicationContext接口是Spring容器的核心接口，初始化时bean立即加载
- ApplicationContext接口提供基础的bean操作相关方法，通过其他接口扩展其功能
- ApplicationContext接口常用初始化类
  - **==ClassPathXmlApplicationContext(常用)==**
  - FileSystemXmlApplicationContext

#### 2.2.2 bean相关

![1629986510487](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day02/assets/1629986510487.png)

其实整个配置中最常用的就两个属性==id==和==class==。

把scope、init-method、destroy-method框起来的原因是，后面注解在讲解的时候还会用到，所以大家对这三个属性关注下。

#### 2.2.3 依赖注入相关

![1629986848563](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day02/assets/1629986848563.png)

## 3，IOC/DI注解开发

Spring的IOC/DI对应的配置开发就已经讲解完成，但是使用起来相对来说还是比较复杂的，复杂的地方在==配置文件==。

前面咱们聊Spring的时候说过，Spring可以简化代码的开发，到现在并没有体会到。

所以Spring到底是如何简化代码开发的呢?

要想真正简化开发，就需要用到Spring的注解开发，Spring对注解支持的版本历程:

* 2.0版开始支持注解
* 2.5版注解功能趋于完善
* 3.0版支持纯注解开发

关于注解开发，我们会讲解两块内容`注解开发定义bean`和`纯注解开发`。

注解开发定义bean用的是2.5版提供的注解，纯注解开发用的是3.0版提供的注解。

### 3.1 环境准备

在学习注解开发之前，先来准备下案例环境:

- 创建一个Maven项目

- pom.xml添加Spring的依赖

  ```xml
  <dependencies>
      <dependency>
          <groupId>org.springframework</groupId>
          <artifactId>spring-context</artifactId>
          <version>5.2.10.RELEASE</version>
      </dependency>
  </dependencies>
  ```

- resources下添加applicationContext.xml

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <beans xmlns="http://www.springframework.org/schema/beans"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="
              http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
      <bean id="bookDao" class="com.itheima.dao.impl.BookDaoImpl"/>
  </beans>
  ```

- 添加BookDao、BookDaoImpl、BookService、BookServiceImpl类

  ```java
  public interface BookDao {
      public void save();
  }
  public class BookDaoImpl implements BookDao {
      public void save() {
          System.out.println("book dao save ..." );
      }
  }
  public interface BookService {
      public void save();
  }
  
  public class BookServiceImpl implements BookService {
      public void save() {
          System.out.println("book service save ...");
      }
  }
  
  ```

- 创建运行类App

  ```java
  public class App {
      public static void main(String[] args) {
          ApplicationContext ctx = new ClassPathXmlApplicationContext("applicationContext.xml");
          BookDao bookDao = (BookDao) ctx.getBean("bookDao");
          bookDao.save();
      }
  }
  ```

最终创建好的项目结构如下:

![1629989221808](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day02/assets/1629989221808.png)

### 3.2 注解开发定义bean

在上述环境的基础上，我们来学一学Spring是如何通过注解实现bean的定义开发?

#### 步骤1:删除原XML配置

将配置文件中的`<bean>`标签删除掉

```xml
<bean id="bookDao" class="com.itheima.dao.impl.BookDaoImpl"/>
```

#### 步骤2:Dao上添加注解

在BookDaoImpl类上添加`@Component`注解

```java
@Component("bookDao")
public class BookDaoImpl implements BookDao {
    public void save() {
        System.out.println("book dao save ..." );
    }
}
```

==注意:@Component注解不可以添加在接口上，因为接口是无法创建对象的。==

XML与注解配置的对应关系:

![1629990315619](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day02/assets/1629990315619.png)

#### 步骤3:配置Spring的注解包扫描

为了让Spring框架能够扫描到写在类上的注解，需要在配置文件上进行包扫描

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="
            http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
    <context:component-scan base-package="com.itheima"/>
</beans>
```

**说明:**

component-scan

* component:组件,Spring将管理的bean视作自己的一个组件
* scan:扫描

base-package指定Spring框架扫描的包路径，它会扫描指定包及其子包中的所有类上的注解。

* 包路径越多[如:com.itheima.dao.impl]，扫描的范围越小速度越快
* 包路径越少[如:com.itheima],扫描的范围越大速度越慢
* 一般扫描到项目的组织名称即Maven的groupId下[如:com.itheima]即可。

#### 步骤4：运行程序

运行`App`类查看打印结果

![1630027590558](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day02/assets/1630027590558.png)

#### 步骤5:Service上添加注解

在BookServiceImpl类上也添加`@Component`交给Spring框架管理

```java
@Component
public class BookServiceImpl implements BookService {
    private BookDao bookDao;

    public void setBookDao(BookDao bookDao) {
        this.bookDao = bookDao;
    }

    public void save() {
        System.out.println("book service save ...");
        bookDao.save();
    }
}
```

#### 步骤6:运行程序

在App类中，从IOC容器中获取BookServiceImpl对应的bean对象，打印

```java
public class App {
    public static void main(String[] args) {
        ApplicationContext ctx = new ClassPathXmlApplicationContext("applicationContext.xml");
        BookDao bookDao = (BookDao) ctx.getBean("bookDao");
        System.out.println(bookDao);
        //按类型获取bean
        BookService bookService = ctx.getBean(BookService.class);
        System.out.println(bookService);
    }
}
```

打印观察结果，两个bean对象都已经打印到控制台

![1630027743910](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day02/assets/1630027743910.png)

**说明:**

* BookServiceImpl类没有起名称，所以在App中是按照类型来获取bean对象

* @Component注解如果不起名称，会有一个默认值就是`当前类名首字母小写`，所以也可以按照名称获取，如

  ```java
  BookService bookService = (BookService)ctx.getBean("bookServiceImpl");
  System.out.println(bookService);
  ```

对于@Component注解，还衍生出了其他三个注解`@Controller`、`@Service`、`@Repository`

通过查看源码会发现:

![1630028345074](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day02/assets/1630028345074.png)

这三个注解和@Component注解的作用是一样的，为什么要衍生出这三个呢?

方便我们后期在编写类的时候能很好的区分出这个类是属于`表现层`、`业务层`还是`数据层`的类。

#### 知识点1:@Component等

| 名称 | @Component/@Controller/@Service/@Repository |
| ---- | ------------------------------------------- |
| 类型 | 类注解                                      |
| 位置 | 类定义上方                                  |
| 作用 | 设置该类为spring管理的bean                  |
| 属性 | value（默认）：定义bean的id                 |

### 3.2 纯注解开发模式

上面已经可以使用注解来配置bean,但是依然有用到配置文件，在配置文件中对包进行了扫描，Spring在3.0版已经支持纯注解开发

* Spring3.0开启了纯注解开发模式，使用Java类替代配置文件，开启了Spring快速开发赛道

具体如何实现?

#### 3.2.1 思路分析

实现思路为: 

* 将配置文件applicationContext.xml删除掉，使用类来替换。

#### 3.2.2 实现步骤

##### 步骤1:创建配置类

创建一个配置类`SpringConfig`

```java
public class SpringConfig {
}

```

##### 步骤2:标识该类为配置类

在配置类上添加`@Configuration`注解，将其标识为一个配置类,替换`applicationContext.xml`

```java
@Configuration
public class SpringConfig {
}
```

##### 步骤3:用注解替换包扫描配置

在配置类上添加包扫描注解`@ComponentScan`替换`<context:component-scan base-package=""/>`

```java
@Configuration
@ComponentScan("com.itheima")
public class SpringConfig {
}
```

##### 步骤4:创建运行类并执行

创建一个新的运行类`AppForAnnotation`

```java
public class AppForAnnotation {

    public static void main(String[] args) {
        ApplicationContext ctx = new AnnotationConfigApplicationContext(SpringConfig.class);
        BookDao bookDao = (BookDao) ctx.getBean("bookDao");
        System.out.println(bookDao);
        BookService bookService = ctx.getBean(BookService.class);
        System.out.println(bookService);
    }
}
```

运行AppForAnnotation,可以看到两个对象依然被获取成功

![1630029110506](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day02/assets/1630029110506.png)

至此，纯注解开发的方式就已经完成了，主要内容包括:

* Java类替换Spring核心配置文件

  ![1630029254372](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day02/assets/1630029254372.png)

* @Configuration注解用于设定当前类为配置类

* @ComponentScan注解用于设定扫描路径，此注解只能添加一次，多个数据请用数组格式

  ```
  @ComponentScan({com.itheima.service","com.itheima.dao"})
  ```

* 读取Spring核心配置文件初始化容器对象切换为读取Java配置类初始化容器对象

  ```java
  //加载配置文件初始化容器
  ApplicationContext ctx = new ClassPathXmlApplicationContext("applicationContext.xml");
  //加载配置类初始化容器
  ApplicationContext ctx = new AnnotationConfigApplicationContext(SpringConfig.class);
  ```

#### 知识点1：@Configuration

| 名称 | @Configuration              |
| ---- | --------------------------- |
| 类型 | 类注解                      |
| 位置 | 类定义上方                  |
| 作用 | 设置该类为spring配置类      |
| 属性 | value（默认）：定义bean的id |

#### 知识点2：@ComponentScan

| 名称 | @ComponentScan                                           |
| ---- | -------------------------------------------------------- |
| 类型 | 类注解                                                   |
| 位置 | 类定义上方                                               |
| 作用 | 设置spring配置类扫描路径，用于加载使用注解格式定义的bean |
| 属性 | value（默认）：扫描路径，此路径可以逐层向下扫描          |

**小结:**

这一节重点掌握的是使用注解完成Spring的bean管理，需要掌握的内容为:

* 记住@Component、@Controller、@Service、@Repository这四个注解
* applicationContext.xml中`<context:component-san/>`的作用是指定扫描包路径，注解为@ComponentScan
* @Configuration标识该类为配置类，使用类替换applicationContext.xml文件
* ClassPathXmlApplicationContext是加载XML配置文件
* AnnotationConfigApplicationContext是加载配置类

### 3.3 注解开发bean作用范围与生命周期管理

使用注解已经完成了bean的管理，接下来按照前面所学习的内容，将通过配置实现的内容都换成对应的注解实现，包含两部分内容:`bean作用范围`和`bean生命周期`。

#### 3.3.1 环境准备

老规矩，学习之前先来准备环境:

- 创建一个Maven项目

- pom.xml添加Spring的依赖

  ```xml
  <dependencies>
      <dependency>
          <groupId>org.springframework</groupId>
          <artifactId>spring-context</artifactId>
          <version>5.2.10.RELEASE</version>
      </dependency>
  </dependencies>
  ```

- 添加一个配置类`SpringConfig`

  ```java
  @Configuration
  @ComponentScan("com.itheima")
  public class SpringConfig {
  }
  ```

- 添加BookDao、BookDaoImpl类

  ```java
  public interface BookDao {
      public void save();
  }
  @Repository
  public class BookDaoImpl implements BookDao {
      public void save() {
          System.out.println("book dao save ..." );
      }
  }
  ```

- 创建运行类App

  ```java
  public class App {
      public static void main(String[] args) {
          AnnotationConfigApplicationContext ctx = new AnnotationConfigApplicationContext(SpringConfig.class);
          BookDao bookDao1 = ctx.getBean(BookDao.class);
          BookDao bookDao2 = ctx.getBean(BookDao.class);
          System.out.println(bookDao1);
          System.out.println(bookDao2);
      }
  }
  ```

最终创建好的项目结构如下:

![1630031112993](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day02/assets/1630031112993.png)

#### 3.3.2 Bean的作用范围

(1)先运行App类,在控制台打印两个一摸一样的地址，说明默认情况下bean是单例

![1630031192753](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day02/assets/1630031192753.png)

(2)要想将BookDaoImpl变成非单例，只需要在其类上添加`@scope`注解

```java
@Repository
//@Scope设置bean的作用范围
@Scope("prototype")
public class BookDaoImpl implements BookDao {

    public void save() {
        System.out.println("book dao save ...");
    }
}
```

再次执行App类，打印结果:

![1630031808947](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day02/assets/1630031808947.png)

##### 知识点1：@Scope

| 名称 | @Scope                                                       |
| ---- | ------------------------------------------------------------ |
| 类型 | 类注解                                                       |
| 位置 | 类定义上方                                                   |
| 作用 | 设置该类创建对象的作用范围<br/>可用于设置创建出的bean是否为单例对象 |
| 属性 | value（默认）：定义bean作用范围，<br/>==默认值singleton（单例），可选值prototype（非单例）== |

#### 3.3.3 Bean的生命周期

(1)在BookDaoImpl中添加两个方法，`init`和`destroy`,方法名可以任意

```java
@Repository
public class BookDaoImpl implements BookDao {
    public void save() {
        System.out.println("book dao save ...");
    }
    public void init() {
        System.out.println("init ...");
    }
    public void destroy() {
        System.out.println("destroy ...");
    }
}

```

(2)如何对方法进行标识，哪个是初始化方法，哪个是销毁方法?

只需要在对应的方法上添加`@PostConstruct`和`@PreDestroy`注解即可。

```java
@Repository
public class BookDaoImpl implements BookDao {
    public void save() {
        System.out.println("book dao save ...");
    }
    @PostConstruct //在构造方法之后执行，替换 init-method
    public void init() {
        System.out.println("init ...");
    }
    @PreDestroy //在销毁方法之前执行,替换 destroy-method
    public void destroy() {
        System.out.println("destroy ...");
    }
}

```

(3)要想看到两个方法执行，需要注意的是`destroy`只有在容器关闭的时候，才会执行，所以需要修改App的类

```java
public class App {
    public static void main(String[] args) {
        AnnotationConfigApplicationContext ctx = new AnnotationConfigApplicationContext(SpringConfig.class);
        BookDao bookDao1 = ctx.getBean(BookDao.class);
        BookDao bookDao2 = ctx.getBean(BookDao.class);
        System.out.println(bookDao1);
        System.out.println(bookDao2);
        ctx.close(); //关闭容器
    }
}
```

(4)运行App,类查看打印结果，证明init和destroy方法都被执行了。

![1630032385498](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day02/assets/1630032385498.png)

==**注意:**@PostConstruct和@PreDestroy注解如果找不到，需要导入下面的jar包==

```java
<dependency>
  <groupId>javax.annotation</groupId>
  <artifactId>javax.annotation-api</artifactId>
  <version>1.3.2</version>
</dependency>
```

找不到的原因是，从JDK9以后jdk中的javax.annotation包被移除了，这两个注解刚好就在这个包中。

##### 知识点1：@PostConstruct

| 名称 | @PostConstruct         |
| ---- | ---------------------- |
| 类型 | 方法注解               |
| 位置 | 方法上                 |
| 作用 | 设置该方法为初始化方法 |
| 属性 | 无                     |

##### 知识点2：@PreDestroy

| 名称 | @PreDestroy          |
| ---- | -------------------- |
| 类型 | 方法注解             |
| 位置 | 方法上               |
| 作用 | 设置该方法为销毁方法 |
| 属性 | 无                   |

**小结**

![1630033039358](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day02/assets/1630033039358.png)

### 3.4 注解开发依赖注入

Spring为了使用注解简化开发，并没有提供`构造函数注入`、`setter注入`对应的注解，只提供了自动装配的注解实现。

#### 3.4.1 环境准备

在学习之前，把案例环境介绍下:

- 创建一个Maven项目

- pom.xml添加Spring的依赖

  ```xml
  <dependencies>
      <dependency>
          <groupId>org.springframework</groupId>
          <artifactId>spring-context</artifactId>
          <version>5.2.10.RELEASE</version>
      </dependency>
  </dependencies>
  ```

- 添加一个配置类`SpringConfig`

  ```java
  @Configuration
  @ComponentScan("com.itheima")
  public class SpringConfig {
  }
  ```

- 添加BookDao、BookDaoImpl、BookService、BookServiceImpl类

  ```java
  public interface BookDao {
      public void save();
  }
  @Repository
  public class BookDaoImpl implements BookDao {
      public void save() {
          System.out.println("book dao save ..." );
      }
  }
  public interface BookService {
      public void save();
  }
  @Service
  public class BookServiceImpl implements BookService {
      private BookDao bookDao;
  	public void setBookDao(BookDao bookDao) {
          this.bookDao = bookDao;
      }
      public void save() {
          System.out.println("book service save ...");
          bookDao.save();
      }
  }
  ```

- 创建运行类App

  ```java
  public class App {
      public static void main(String[] args) {
          AnnotationConfigApplicationContext ctx = new AnnotationConfigApplicationContext(SpringConfig.class);
          BookService bookService = ctx.getBean(BookService.class);
          bookService.save();
      }
  }
  ```

最终创建好的项目结构如下:

![1630033604129](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day02/assets/1630033604129.png)

环境准备好后，运行后会发现有问题

![1630033710052](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day02/assets/1630033710052.png)

出现问题的原因是，在BookServiceImpl类中添加了BookDao的属性，并提供了setter方法，但是目前是没有提供配置注入BookDao的，所以bookDao对象为Null,调用其save方法就会报`控指针异常`。

#### 3.4.2 注解实现按照类型注入

对于这个问题使用注解该如何解决?

(1) 在BookServiceImpl类的bookDao属性上添加`@Autowired`注解

```java
@Service
public class BookServiceImpl implements BookService {
    @Autowired
    private BookDao bookDao;
    
//	  public void setBookDao(BookDao bookDao) {
//        this.bookDao = bookDao;
//    }
    public void save() {
        System.out.println("book service save ...");
        bookDao.save();
    }
}
```

**注意:**

* @Autowired可以写在属性上，也可也写在setter方法上，最简单的处理方式是`写在属性上并将setter方法删除掉`
* 为什么setter方法可以删除呢?
  * 自动装配基于反射设计创建对象并通过暴力反射为私有属性进行设值
  * 普通反射只能获取public修饰的内容
  * 暴力反射除了获取public修饰的内容还可以获取private修改的内容
  * 所以此处无需提供setter方法

(2)@Autowired是按照类型注入，那么对应BookDao接口如果有多个实现类，比如添加BookDaoImpl2

```java
@Repository
public class BookDaoImpl2 implements BookDao {
    public void save() {
        System.out.println("book dao save ...2");
    }
}
```

这个时候再次运行App，就会报错

![1630034272959](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day02/assets/1630034272959.png)

此时，按照类型注入就无法区分到底注入哪个对象，解决方案:`按照名称注入`

* 先给两个Dao类分别起个名称

  ```java
  @Repository("bookDao")
  public class BookDaoImpl implements BookDao {
      public void save() {
          System.out.println("book dao save ..." );
      }
  }
  @Repository("bookDao2")
  public class BookDaoImpl2 implements BookDao {
      public void save() {
          System.out.println("book dao save ...2" );
      }
  }
  ```

  此时就可以注入成功，但是得思考个问题: 

  * @Autowired是按照类型注入的，给BookDao的两个实现起了名称，它还是有两个bean对象，为什么不报错?

  * @Autowired默认按照类型自动装配，如果IOC容器中同类的Bean找到多个，就按照变量名和Bean的名称匹配。因为变量名叫`bookDao`而容器中也有一个`booDao`，所以可以成功注入。

  * 分析下面这种情况是否能完成注入呢?

    ![1630036236150](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day02/assets/1630036236150.png)

  * 不行，因为按照类型会找到多个bean对象，此时会按照`bookDao`名称去找，因为IOC容器只有名称叫`bookDao1`和`bookDao2`,所以找不到，会报`NoUniqueBeanDefinitionException`

#### 3.4.3 注解实现按照名称注入

当根据类型在容器中找到多个bean,注入参数的属性名又和容器中bean的名称不一致，这个时候该如何解决，就需要使用到`@Qualifier`来指定注入哪个名称的bean对象。

```java
@Service
public class BookServiceImpl implements BookService {
    @Autowired
    @Qualifier("bookDao1")
    private BookDao bookDao;
    
    public void save() {
        System.out.println("book service save ...");
        bookDao.save();
    }
}
```

@Qualifier注解后的值就是需要注入的bean的名称。

==注意:@Qualifier不能独立使用，必须和@Autowired一起使用==

#### 3.4.4 简单数据类型注入

引用类型看完，简单类型注入就比较容易懂了。简单类型注入的是基本数据类型或者字符串类型，下面在`BookDaoImpl`类中添加一个`name`属性，用其进行简单类型注入

```java
@Repository("bookDao")
public class BookDaoImpl implements BookDao {
    private String name;
    public void save() {
        System.out.println("book dao save ..." + name);
    }
}
```

数据类型换了，对应的注解也要跟着换，这次使用`@Value`注解，将值写入注解的参数中就行了

```java
@Repository("bookDao")
public class BookDaoImpl implements BookDao {
    @Value("itheima")
    private String name;
    public void save() {
        System.out.println("book dao save ..." + name);
    }
}
```

注意数据格式要匹配，如将"abc"注入给int值，这样程序就会报错。

介绍完后，会有一种感觉就是这个注解好像没什么用，跟直接赋值是一个效果，还没有直接赋值简单，所以这个注解存在的意义是什么?

#### 3.4.5 注解读取properties配置文件

`@Value`一般会被用在从properties配置文件中读取内容进行使用，具体如何实现?

##### 步骤1：resource下准备properties文件

jdbc.properties

```properties
name=itheima888
```

##### 步骤2: 使用注解加载properties配置文件

在配置类上添加`@PropertySource`注解

```java
@Configuration
@ComponentScan("com.itheima")
@PropertySource("jdbc.properties")
public class SpringConfig {
}

```

##### 步骤3：使用@Value读取配置文件中的内容

```java
@Repository("bookDao")
public class BookDaoImpl implements BookDao {
    @Value("${name}")
    private String name;
    public void save() {
        System.out.println("book dao save ..." + name);
    }
}
```

步骤4:运行程序

运行App类，查看运行结果，说明配置文件中的内容已经被加载到

![1630084683663](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day02/assets/1630084683663.png)

**注意:**

* 如果读取的properties配置文件有多个，可以使用`@PropertySource`的属性来指定多个

  ```java
  @PropertySource({"jdbc.properties","xxx.properties"})
  ```

* `@PropertySource`注解属性中不支持使用通配符`*`,运行会报错

  ```java
  @PropertySource({"*.properties"})
  ```

* `@PropertySource`注解属性中可以把`classpath:`加上,代表从当前项目的根路径找文件

  ```java
  @PropertySource({"classpath:jdbc.properties"})
  ```

#### 知识点1：@Autowired


| 名称 | @Autowired                                                   |
| ---- | ------------------------------------------------------------ |
| 类型 | 属性注解  或  方法注解（了解）  或  方法形参注解（了解）     |
| 位置 | 属性定义上方  或  标准set方法上方  或  类set方法上方  或  方法形参前面 |
| 作用 | 为引用类型属性设置值                                         |
| 属性 | required：true/false，定义该属性是否允许为null               |

#### 知识点2：@Qualifier

| 名称 | @Qualifier                                           |
| ---- | ---------------------------------------------------- |
| 类型 | 属性注解  或  方法注解（了解）                       |
| 位置 | 属性定义上方  或  标准set方法上方  或  类set方法上方 |
| 作用 | 为引用类型属性指定注入的beanId                       |
| 属性 | value（默认）：设置注入的beanId                      |

#### 知识点3：@Value

| 名称 | @Value                                               |
| ---- | ---------------------------------------------------- |
| 类型 | 属性注解  或  方法注解（了解）                       |
| 位置 | 属性定义上方  或  标准set方法上方  或  类set方法上方 |
| 作用 | 为  基本数据类型  或  字符串类型  属性设置值         |
| 属性 | value（默认）：要注入的属性值                        |

#### 知识点4：@PropertySource

| 名称 | @PropertySource                                              |
| ---- | ------------------------------------------------------------ |
| 类型 | 类注解                                                       |
| 位置 | 类定义上方                                                   |
| 作用 | 加载properties文件中的属性值                                 |
| 属性 | value（默认）：设置加载的properties文件对应的文件名或文件名组成的数组 |

## 4，IOC/DI注解开发管理第三方bean

前面定义bean的时候都是在自己开发的类上面写个注解就完成了，但如果是第三方的类，这些类都是在jar包中，我们没有办法在类上面添加注解，这个时候该怎么办?

遇到上述问题，我们就需要有一种更加灵活的方式来定义bean,这种方式不能在原始代码上面书写注解，一样能定义bean,这就用到了一个全新的注解==@Bean==。

这个注解该如何使用呢?

咱们把之前使用配置方式管理的数据源使用注解再来一遍，通过这个案例来学习下@Bean的使用。

### 4.1 环境准备

学习@Bean注解之前先来准备环境:

- 创建一个Maven项目

- pom.xml添加Spring的依赖

  ```xml
  <dependencies>
      <dependency>
          <groupId>org.springframework</groupId>
          <artifactId>spring-context</artifactId>
          <version>5.2.10.RELEASE</version>
      </dependency>
  </dependencies>
  ```

- 添加一个配置类`SpringConfig`

  ```java
  @Configuration
  public class SpringConfig {
  }
  ```

- 添加BookDao、BookDaoImpl类

  ```java
  public interface BookDao {
      public void save();
  }
  @Repository
  public class BookDaoImpl implements BookDao {
      public void save() {
          System.out.println("book dao save ..." );
      }
  }
  ```

- 创建运行类App

  ```java
  public class App {
      public static void main(String[] args) {
          AnnotationConfigApplicationContext ctx = new AnnotationConfigApplicationContext(SpringConfig.class);
      }
  }
  ```

最终创建好的项目结构如下:

![1630122466404](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day02/assets/1630122466404.png)

### 4.2 注解开发管理第三方bean

在上述环境中完成对`Druid`数据源的管理，具体的实现步骤为:

#### 步骤1:导入对应的jar包

```xml
<dependency>
    <groupId>com.alibaba</groupId>
    <artifactId>druid</artifactId>
    <version>1.1.16</version>
</dependency>
```

#### 步骤2:在配置类中添加一个方法

注意该方法的返回值就是要创建的Bean对象类型

```java
@Configuration
public class SpringConfig {
    public DataSource dataSource(){
        DruidDataSource ds = new DruidDataSource();
        ds.setDriverClassName("com.mysql.jdbc.Driver");
        ds.setUrl("jdbc:mysql://localhost:3306/spring_db");
        ds.setUsername("root");
        ds.setPassword("root");
        return ds;
    }
}
```

#### 步骤3:在方法上添加`@Bean`注解

@Bean注解的作用是将方法的返回值制作为Spring管理的一个bean对象

```java
@Configuration
public class SpringConfig {
	@Bean
    public DataSource dataSource(){
        DruidDataSource ds = new DruidDataSource();
        ds.setDriverClassName("com.mysql.jdbc.Driver");
        ds.setUrl("jdbc:mysql://localhost:3306/spring_db");
        ds.setUsername("root");
        ds.setPassword("root");
        return ds;
    }
}
```

**注意:不能使用`DataSource ds = new DruidDataSource()`**

因为DataSource接口中没有对应的setter方法来设置属性。

#### 步骤4:从IOC容器中获取对象并打印

```java
public class App {
    public static void main(String[] args) {
        AnnotationConfigApplicationContext ctx = new AnnotationConfigApplicationContext(SpringConfig.class);
        DataSource dataSource = ctx.getBean(DataSource.class);
        System.out.println(dataSource);
    }
}
```

至此使用@Bean来管理第三方bean的案例就已经完成。

如果有多个bean要被Spring管理，直接在配置类中多些几个方法，方法上添加@Bean注解即可。

### 4.3 引入外部配置类

如果把所有的第三方bean都配置到Spring的配置类`SpringConfig`中，虽然可以，但是不利于代码阅读和分类管理，所有我们就想能不能按照类别将这些bean配置到不同的配置类中?

对于数据源的bean,我们新建一个`JdbcConfig`配置类，并把数据源配置到该类下。

```java
public class JdbcConfig {
	@Bean
    public DataSource dataSource(){
        DruidDataSource ds = new DruidDataSource();
        ds.setDriverClassName("com.mysql.jdbc.Driver");
        ds.setUrl("jdbc:mysql://localhost:3306/spring_db");
        ds.setUsername("root");
        ds.setPassword("root");
        return ds;
    }
}
```

现在的问题是，这个配置类如何能被Spring配置类加载到，并创建DataSource对象在IOC容器中?

针对这个问题，有两个解决方案:

#### 4.3.1 使用包扫描引入

##### 步骤1:在Spring的配置类上添加包扫描

```java
@Configuration
@ComponentScan("com.itheima.config")
public class SpringConfig {
	
}
```

##### 步骤2:在JdbcConfig上添加配置注解

JdbcConfig类要放入到`com.itheima.config`包下，需要被Spring的配置类扫描到即可

```java
@Configuration
public class JdbcConfig {
	@Bean
    public DataSource dataSource(){
        DruidDataSource ds = new DruidDataSource();
        ds.setDriverClassName("com.mysql.jdbc.Driver");
        ds.setUrl("jdbc:mysql://localhost:3306/spring_db");
        ds.setUsername("root");
        ds.setPassword("root");
        return ds;
    }
}
```

##### 步骤3:运行程序

依然能获取到bean对象并打印控制台。

这种方式虽然能够扫描到，但是不能很快的知晓都引入了哪些配置类，所有这种方式不推荐使用。

#### 4.3.2 使用`@Import`引入

方案一实现起来有点小复杂，Spring早就想到了这一点，于是又给我们提供了第二种方案。

这种方案可以不用加`@Configuration`注解，但是必须在Spring配置类上使用`@Import`注解手动引入需要加载的配置类

##### 步骤1:去除JdbcConfig类上的注解

```java
public class JdbcConfig {
	@Bean
    public DataSource dataSource(){
        DruidDataSource ds = new DruidDataSource();
        ds.setDriverClassName("com.mysql.jdbc.Driver");
        ds.setUrl("jdbc:mysql://localhost:3306/spring_db");
        ds.setUsername("root");
        ds.setPassword("root");
        return ds;
    }
}
```

##### 步骤2:在Spring配置类中引入

```java
@Configuration
//@ComponentScan("com.itheima.config")
@Import({JdbcConfig.class})
public class SpringConfig {
	
}
```

**注意:**

* 扫描注解可以移除

* @Import参数需要的是一个数组，可以引入多个配置类。

* @Import注解在配置类中只能写一次，下面的方式是==不允许的==

  ```java
  @Configuration
  //@ComponentScan("com.itheima.config")
  @Import(JdbcConfig.class)
  @Import(Xxx.class)
  public class SpringConfig {
  	
  }
  ```

##### 步骤3:运行程序

依然能获取到bean对象并打印控制台

### 知识点1：@Bean

| 名称 | @Bean                                  |
| ---- | -------------------------------------- |
| 类型 | 方法注解                               |
| 位置 | 方法定义上方                           |
| 作用 | 设置该方法的返回值作为spring管理的bean |
| 属性 | value（默认）：定义bean的id            |

### 知识点2：@Import

| 名称 | @Import                                                      |
| ---- | ------------------------------------------------------------ |
| 类型 | 类注解                                                       |
| 位置 | 类定义上方                                                   |
| 作用 | 导入配置类                                                   |
| 属性 | value（默认）：定义导入的配置类类名，<br/>当配置类有多个时使用数组格式一次性导入多个配置类 |

### 4.4 注解开发实现为第三方bean注入资源

在使用@Bean创建bean对象的时候，如果方法在创建的过程中需要其他资源该怎么办?

这些资源会有两大类，分别是`简单数据类型` 和`引用数据类型`。

#### 4.4.1 简单数据类型

##### 4.4.1.1 需求分析

对于下面代码关于数据库的四要素不应该写死在代码中，应该是从properties配置文件中读取。如何来优化下面的代码?

```java
public class JdbcConfig {
	@Bean
    public DataSource dataSource(){
        DruidDataSource ds = new DruidDataSource();
        ds.setDriverClassName("com.mysql.jdbc.Driver");
        ds.setUrl("jdbc:mysql://localhost:3306/spring_db");
        ds.setUsername("root");
        ds.setPassword("root");
        return ds;
    }
}
```

##### 4.4.1.2 注入简单数据类型步骤

###### 步骤1:类中提供四个属性

```java
public class JdbcConfig {
    private String driver;
    private String url;
    private String userName;
    private String password;
	@Bean
    public DataSource dataSource(){
        DruidDataSource ds = new DruidDataSource();
        ds.setDriverClassName("com.mysql.jdbc.Driver");
        ds.setUrl("jdbc:mysql://localhost:3306/spring_db");
        ds.setUsername("root");
        ds.setPassword("root");
        return ds;
    }
}
```

###### 步骤2:使用`@Value`注解引入值

```java
public class JdbcConfig {
    @Value("com.mysql.jdbc.Driver")
    private String driver;
    @Value("jdbc:mysql://localhost:3306/spring_db")
    private String url;
    @Value("root")
    private String userName;
    @Value("password")
    private String password;
	@Bean
    public DataSource dataSource(){
        DruidDataSource ds = new DruidDataSource();
        ds.setDriverClassName(driver);
        ds.setUrl(url);
        ds.setUsername(userName);
        ds.setPassword(password);
        return ds;
    }
}
```

###### 扩展

现在的数据库连接四要素还是写在代码中，需要做的是将这些内容提

取到jdbc.properties配置文件，大家思考下该如何实现?

> 1.resources目录下添加jdbc.properties
>
> 2.配置文件中提供四个键值对分别是数据库的四要素
>
> 3.使用@PropertySource加载jdbc.properties配置文件
>
> 4.修改@Value注解属性的值，将其修改为`${key}`，key就是键值对中的键的值

具体的实现就交由大家自行实现下。

#### 4.4.2 引用数据类型

##### 4.4.2.1 需求分析 

假设在构建DataSource对象的时候，需要用到BookDao对象，该如何把BookDao对象注入进方法内让其使用呢?

```java
public class JdbcConfig {
	@Bean
    public DataSource dataSource(){
        DruidDataSource ds = new DruidDataSource();
        ds.setDriverClassName("com.mysql.jdbc.Driver");
        ds.setUrl("jdbc:mysql://localhost:3306/spring_db");
        ds.setUsername("root");
        ds.setPassword("root");
        return ds;
    }
}
```

##### 4.4.2.2 注入引用数据类型步骤

###### 步骤1:在SpringConfig中扫描BookDao

扫描的目的是让Spring能管理到BookDao,也就是说要让IOC容器中有一个bookDao对象

```java
@Configuration
@ComponentScan("com.itheima.dao")
@Import({JdbcConfig.class})
public class SpringConfig {
}
```

###### 步骤2:在JdbcConfig类的方法上添加参数

```java
@Bean
public DataSource dataSource(BookDao bookDao){
    System.out.println(bookDao);
    DruidDataSource ds = new DruidDataSource();
    ds.setDriverClassName(driver);
    ds.setUrl(url);
    ds.setUsername(userName);
    ds.setPassword(password);
    return ds;
}
```

==引用类型注入只需要为bean定义方法设置形参即可，容器会根据类型自动装配对象。==

###### 步骤3:运行程序

![1630125475609](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day02/assets/1630125475609.png)



## 5，注解开发总结

前面我们已经完成了XML配置和注解的开发实现，至于两者之间的差异，咱们放在一块去对比回顾下:

![1630134786448](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day02/assets/1630134786448.png)

## 6，Spring整合

课程学习到这里，已经对Spring有一个简单的认识了，Spring有一个容器，叫做IoC容器，里面保存bean。在进行企业级开发的时候，其实除了将自己写的类让Spring管理之外，还有一部分重要的工作就是使用第三方的技术。前面已经讲了如何管理第三方bean了，下面结合IoC和DI，整合2个常用技术，进一步加深对Spring的使用理解。

### 6.1 Spring整合Mybatis思路分析

#### 6.1.1 环境准备

在准备环境的过程中，我们也来回顾下Mybatis开发的相关内容:

##### 步骤1:准备数据库表

Mybatis是来操作数据库表，所以先创建一个数据库及表

```sql
create database spring_db character set utf8;
use spring_db;
create table tbl_account(
    id int primary key auto_increment,
    name varchar(35),
    money double
);
```

##### 步骤2:创建项目导入jar包

项目的pom.xml添加相关依赖

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-context</artifactId>
        <version>5.2.10.RELEASE</version>
    </dependency>
    <dependency>
        <groupId>com.alibaba</groupId>
        <artifactId>druid</artifactId>
        <version>1.1.16</version>
    </dependency>
    <dependency>
        <groupId>org.mybatis</groupId>
        <artifactId>mybatis</artifactId>
        <version>3.5.6</version>
    </dependency>
    <dependency>
        <groupId>mysql</groupId>
        <artifactId>mysql-connector-java</artifactId>
        <version>5.1.47</version>
    </dependency>
</dependencies>
```

##### 步骤3:根据表创建模型类

```java
public class Account implements Serializable {

    private Integer id;
    private String name;
    private Double money;
	//setter...getter...toString...方法略    
}
```

##### 步骤4:创建Dao接口

```java
public interface AccountDao {

    @Insert("insert into tbl_account(name,money)values(#{name},#{money})")
    void save(Account account);

    @Delete("delete from tbl_account where id = #{id} ")
    void delete(Integer id);

    @Update("update tbl_account set name = #{name} , money = #{money} where id = #{id} ")
    void update(Account account);

    @Select("select * from tbl_account")
    List<Account> findAll();

    @Select("select * from tbl_account where id = #{id} ")
    Account findById(Integer id);
}
```

##### 步骤5:创建Service接口和实现类

```java
public interface AccountService {

    void save(Account account);

    void delete(Integer id);

    void update(Account account);

    List<Account> findAll();

    Account findById(Integer id);

}

@Service
public class AccountServiceImpl implements AccountService {

    @Autowired
    private AccountDao accountDao;

    public void save(Account account) {
        accountDao.save(account);
    }

    public void update(Account account){
        accountDao.update(account);
    }

    public void delete(Integer id) {
        accountDao.delete(id);
    }

    public Account findById(Integer id) {
        return accountDao.findById(id);
    }

    public List<Account> findAll() {
        return accountDao.findAll();
    }
}
```

##### 步骤6:添加jdbc.properties文件

resources目录下添加，用于配置数据库连接四要素

```properties
jdbc.driver=com.mysql.jdbc.Driver
jdbc.url=jdbc:mysql://localhost:3306/spring_db?useSSL=false
jdbc.username=root
jdbc.password=root
```

useSSL:关闭MySQL的SSL连接

##### 步骤7:添加Mybatis核心配置文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
    <!--读取外部properties配置文件-->
    <properties resource="jdbc.properties"></properties>
    <!--别名扫描的包路径-->
    <typeAliases>
        <package name="com.itheima.domain"/>
    </typeAliases>
    <!--数据源-->
    <environments default="mysql">
        <environment id="mysql">
            <transactionManager type="JDBC"></transactionManager>
            <dataSource type="POOLED">
                <property name="driver" value="${jdbc.driver}"></property>
                <property name="url" value="${jdbc.url}"></property>
                <property name="username" value="${jdbc.username}"></property>
                <property name="password" value="${jdbc.password}"></property>
            </dataSource>
        </environment>
    </environments>
    <!--映射文件扫描包路径-->
    <mappers>
        <package name="com.itheima.dao"></package>
    </mappers>
</configuration>
```

##### 步骤8:编写应用程序

```java
public class App {
    public static void main(String[] args) throws IOException {
        // 1. 创建SqlSessionFactoryBuilder对象
        SqlSessionFactoryBuilder sqlSessionFactoryBuilder = new SqlSessionFactoryBuilder();
        // 2. 加载SqlMapConfig.xml配置文件
        InputStream inputStream = Resources.getResourceAsStream("SqlMapConfig.xml.bak");
        // 3. 创建SqlSessionFactory对象
        SqlSessionFactory sqlSessionFactory = sqlSessionFactoryBuilder.build(inputStream);
        // 4. 获取SqlSession
        SqlSession sqlSession = sqlSessionFactory.openSession();
        // 5. 执行SqlSession对象执行查询，获取结果User
        AccountDao accountDao = sqlSession.getMapper(AccountDao.class);

        Account ac = accountDao.findById(1);
        System.out.println(ac);

        // 6. 释放资源
        sqlSession.close();
    }
}
```

##### 步骤9:运行程序

![1630136904087](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day02/assets/1630136904087.png)

#### 6.1.2 整合思路分析

Mybatis的基础环境我们已经准备好了，接下来就得分析下在上述的内容中，哪些对象可以交给Spring来管理?

* Mybatis程序核心对象分析

  ![1630137189480](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day02/assets/1630137189480.png)

  从图中可以获取到，真正需要交给Spring管理的是==SqlSessionFactory==

* 整合Mybatis，就是将Mybatis用到的内容交给Spring管理，分析下配置文件

  ![1630137388717](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day02/assets/1630137388717.png)

  **说明:**

  * 第一行读取外部properties配置文件，Spring有提供具体的解决方案`@PropertySource`,需要交给Spring
  * 第二行起别名包扫描，为SqlSessionFactory服务的，需要交给Spring
  * 第三行主要用于做连接池，Spring之前我们已经整合了Druid连接池，这块也需要交给Spring
  * 前面三行一起都是为了创建SqlSession对象用的，那么用Spring管理SqlSession对象吗?回忆下SqlSession是由SqlSessionFactory创建出来的，所以只需要将SqlSessionFactory交给Spring管理即可。
  * 第四行是Mapper接口和映射文件[如果使用注解就没有该映射文件]，这个是在获取到SqlSession以后执行具体操作的时候用，所以它和SqlSessionFactory创建的时机都不在同一个时间，可能需要单独管理。

### 6.2 Spring整合Mybatis

前面我们已经分析了Spring与Mybatis的整合，大体需要做两件事，

第一件事是:Spring要管理MyBatis中的SqlSessionFactory

第二件事是:Spring要管理Mapper接口的扫描

具体该如何实现，具体的步骤为:

#### 步骤1:项目中导入整合需要的jar包

```xml
<dependency>
    <!--Spring操作数据库需要该jar包-->
    <groupId>org.springframework</groupId>
    <artifactId>spring-jdbc</artifactId>
    <version>5.2.10.RELEASE</version>
</dependency>
<dependency>
    <!--
		Spring与Mybatis整合的jar包
		这个jar包mybatis在前面，是Mybatis提供的
	-->
    <groupId>org.mybatis</groupId>
    <artifactId>mybatis-spring</artifactId>
    <version>1.3.0</version>
</dependency>
```

#### 步骤2:创建Spring的主配置类

```java
//配置类注解
@Configuration
//包扫描，主要扫描的是项目中的AccountServiceImpl类
@ComponentScan("com.itheima")
public class SpringConfig {
}

```

#### 步骤3:创建数据源的配置类

在配置类中完成数据源的创建

```java
public class JdbcConfig {
    @Value("${jdbc.driver}")
    private String driver;
    @Value("${jdbc.url}")
    private String url;
    @Value("${jdbc.username}")
    private String userName;
    @Value("${jdbc.password}")
    private String password;

    @Bean
    public DataSource dataSource(){
        DruidDataSource ds = new DruidDataSource();
        ds.setDriverClassName(driver);
        ds.setUrl(url);
        ds.setUsername(userName);
        ds.setPassword(password);
        return ds;
    }
}
```

#### 步骤4:主配置类中读properties并引入数据源配置类

```java
@Configuration
@ComponentScan("com.itheima")
@PropertySource("classpath:jdbc.properties")
@Import(JdbcConfig.class)
public class SpringConfig {
}

```

#### 步骤5:创建Mybatis配置类并配置SqlSessionFactory

```java
public class MybatisConfig {
    //定义bean，SqlSessionFactoryBean，用于产生SqlSessionFactory对象
    @Bean
    public SqlSessionFactoryBean sqlSessionFactory(DataSource dataSource){
        SqlSessionFactoryBean ssfb = new SqlSessionFactoryBean();
        //设置模型类的别名扫描
        ssfb.setTypeAliasesPackage("com.itheima.domain");
        //设置数据源
        ssfb.setDataSource(dataSource);
        return ssfb;
    }
    //定义bean，返回MapperScannerConfigurer对象
    @Bean
    public MapperScannerConfigurer mapperScannerConfigurer(){
        MapperScannerConfigurer msc = new MapperScannerConfigurer();
        msc.setBasePackage("com.itheima.dao");
        return msc;
    }
}
```

**说明:**

* 使用SqlSessionFactoryBean封装SqlSessionFactory需要的环境信息

  ![1630138835057](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day02/assets/1630138835057.png)

  * SqlSessionFactoryBean是前面我们讲解FactoryBean的一个子类，在该类中将SqlSessionFactory的创建进行了封装，简化对象的创建，我们只需要将其需要的内容设置即可。
  * 方法中有一个参数为dataSource,当前Spring容器中已经创建了Druid数据源，类型刚好是DataSource类型，此时在初始化SqlSessionFactoryBean这个对象的时候，发现需要使用DataSource对象，而容器中刚好有这么一个对象，就自动加载了DruidDataSource对象。

* 使用MapperScannerConfigurer加载Dao接口，创建代理对象保存到IOC容器中

  ![1630138916939](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day02/assets/1630138916939.png)

  * 这个MapperScannerConfigurer对象也是MyBatis提供的专用于整合的jar包中的类，用来处理原始配置文件中的mappers相关配置，加载数据层的Mapper接口类
  * MapperScannerConfigurer有一个核心属性basePackage，就是用来设置所扫描的包路径

#### 步骤6:主配置类中引入Mybatis配置类

```java
@Configuration
@ComponentScan("com.itheima")
@PropertySource("classpath:jdbc.properties")
@Import({JdbcConfig.class,MybatisConfig.class})
public class SpringConfig {
}
```

#### 步骤7:编写运行类

在运行类中，从IOC容器中获取Service对象，调用方法获取结果

```java
public class App2 {
    public static void main(String[] args) {
        ApplicationContext ctx = new AnnotationConfigApplicationContext(SpringConfig.class);

        AccountService accountService = ctx.getBean(AccountService.class);

        Account ac = accountService.findById(1);
        System.out.println(ac);
    }
}

```

#### 步骤8:运行程序

![1630139036627](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day02/assets/1630139036627.png)

支持Spring与Mybatis的整合就已经完成了，其中主要用到的两个类分别是:

* ==SqlSessionFactoryBean==
* ==MapperScannerConfigurer==

### 6.3 Spring整合Junit

整合Junit与整合Druid和MyBatis差异比较大，为什么呢？Junit是一个搞单元测试用的工具，它不是我们程序的主体，也不会参加最终程序的运行，从作用上来说就和之前的东西不一样，它不是做功能的，看做是一个辅助工具就可以了。

#### 6.3.1 环境准备

这块环境，大家可以直接使用Spring与Mybatis整合的环境即可。当然也可以重新创建一个，因为内容是一模一样，所以我们直接来看下项目结构即可:

![1630139720273](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day02/assets/1630139720273.png)

#### 6.3.2 整合Junit步骤

在上述环境的基础上，我们来对Junit进行整合。

##### 步骤1:引入依赖

pom.xml

```xml
<dependency>
    <groupId>junit</groupId>
    <artifactId>junit</artifactId>
    <version>4.12</version>
    <scope>test</scope>
</dependency>

<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-test</artifactId>
    <version>5.2.10.RELEASE</version>
</dependency>
```

##### 步骤2:编写测试类

在test\java下创建一个AccountServiceTest,这个名字任意

```java
//设置类运行器
@RunWith(SpringJUnit4ClassRunner.class)
//设置Spring环境对应的配置类
@ContextConfiguration(classes = {SpringConfiguration.class}) //加载配置类
//@ContextConfiguration(locations={"classpath:applicationContext.xml"})//加载配置文件
public class AccountServiceTest {
    //支持自动装配注入bean
    @Autowired
    private AccountService accountService;
    @Test
    public void testFindById(){
        System.out.println(accountService.findById(1));

    }
    @Test
    public void testFindAll(){
        System.out.println(accountService.findAll());
    }
}
```

**注意:**

* 单元测试，如果测试的是注解配置类，则使用`@ContextConfiguration(classes = 配置类.class)`
* 单元测试，如果测试的是配置文件，则使用`@ContextConfiguration(locations={配置文件名,...})`
* Junit运行后是基于Spring环境运行的，所以Spring提供了一个专用的类运行器，这个务必要设置，这个类运行器就在Spring的测试专用包中提供的，导入的坐标就是这个东西`SpringJUnit4ClassRunner`
* 上面两个配置都是固定格式，当需要测试哪个bean时，使用自动装配加载对应的对象，下面的工作就和以前做Junit单元测试完全一样了

#### 知识点1：@RunWith

| 名称 | @RunWith                          |
| ---- | --------------------------------- |
| 类型 | 测试类注解                        |
| 位置 | 测试类定义上方                    |
| 作用 | 设置JUnit运行器                   |
| 属性 | value（默认）：运行所使用的运行期 |

#### 知识点2：@ContextConfiguration

| 名称 | @ContextConfiguration                                        |
| ---- | ------------------------------------------------------------ |
| 类型 | 测试类注解                                                   |
| 位置 | 测试类定义上方                                               |
| 作用 | 设置JUnit加载的Spring核心配置                                |
| 属性 | classes：核心配置类，可以使用数组的格式设定加载多个配置类<br/>locations:配置文件，可以使用数组的格式设定加载多个配置文件名称 |



# Spring_day03

**今日目标**

> * 理解并掌握AOP相关概念
> * 能够说出AOP的工作流程
> * 能运用AOP相关知识完成对应的案例编写
> * 重点掌握Spring的声明式事务管理

## 1，AOP简介

前面我们在介绍Spring的时候说过，Spring有两个核心的概念，一个是`IOC/DI`，一个是`AOP`。

前面已经对`IOC/DI`进行了系统的学习，接下来要学习它的另一个核心内容，就是==AOP==。

对于AOP,我们前面提过一句话是:==AOP是在不改原有代码的前提下对其进行增强。==

对于下面的内容，我们主要就是围绕着这一句话进行展开学习，主要学习两方面内容`AOP核心概念`,`AOP作用`:

### 1.1 什么是AOP?

* AOP(Aspect Oriented Programming)面向切面编程，一种编程范式，指导开发者如何组织程序结构。
  * OOP(Object Oriented Programming)面向对象编程

我们都知道OOP是一种编程思想，那么AOP也是一种编程思想，编程思想主要的内容就是指导程序员该如何编写程序，所以它们两个是不同的`编程范式`。

### 1.2 AOP作用

- 作用:在不惊动原始设计的基础上为其进行功能增强，前面咱们有技术就可以实现这样的功能即代理模式。

前面咱们有技术就可以实现这样的功能即`代理模式`。

### 1.3 AOP核心概念

为了能更好的理解AOP的相关概念，我们准备了一个环境，整个环境的内容我们暂时可以不用关注，最主要的类为:`BookDaoImpl`

```java
@Repository
public class BookDaoImpl implements BookDao {
    public void save() {
        //记录程序当前执行执行（开始时间）
        Long startTime = System.currentTimeMillis();
        //业务执行万次
        for (int i = 0;i<10000;i++) {
            System.out.println("book dao save ...");
        }
        //记录程序当前执行时间（结束时间）
        Long endTime = System.currentTimeMillis();
        //计算时间差
        Long totalTime = endTime-startTime;
        //输出信息
        System.out.println("执行万次消耗时间：" + totalTime + "ms");
    }
    public void update(){
        System.out.println("book dao update ...");
    }
    public void delete(){
        System.out.println("book dao delete ...");
    }
    public void select(){
        System.out.println("book dao select ...");
    }
}
```

代码的内容相信大家都能够读懂，对于`save`方法中有计算万次执行消耗的时间。

当在App类中从容器中获取bookDao对象后，分别执行其`save`,`delete`,`update`和`select`方法后会有如下的打印结果:

![1630143927489](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day03/assets/1630143927489.png)

这个时候，我们就应该有些疑问?

* 对于计算万次执行消耗的时间只有save方法有，为什么delete和update方法也会有呢?
* delete和update方法有，那什么select方法为什么又没有呢?

这个案例中其实就使用了Spring的AOP，在不惊动(改动)原有设计(代码)的前提下，想给谁添加功能就给谁添加。这个也就是Spring的理念：

* 无入侵式/无侵入式

说了这么多，Spring到底是如何实现的呢?

![1630144353462](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day03/assets/1630144353462.png)

(1)前面一直在强调，Spring的AOP是对一个类的方法在不进行任何修改的前提下实现增强。对于上面的案例中BookServiceImpl中有`save`,`update`,`delete`和`select`方法,这些方法我们给起了一个名字叫==连接点==

(2)在BookServiceImpl的四个方法中，`update`和`delete`只有打印没有计算万次执行消耗时间，但是在运行的时候已经有该功能，那也就是说`update`和`delete`方法都已经被增强，所以对于需要增强的方法我们给起了一个名字叫==切入点==

(3)执行BookServiceImpl的update和delete方法的时候都被添加了一个计算万次执行消耗时间的功能，将这个功能抽取到一个方法中，换句话说就是存放共性功能的方法，我们给起了个名字叫==通知==

(4)通知是要增强的内容，会有多个，切入点是需要被增强的方法，也会有多个，那哪个切入点需要添加哪个通知，就需要提前将它们之间的关系描述清楚，那么对于通知和切入点之间的关系描述，我们给起了个名字叫==切面==

(5)通知是一个方法，方法不能独立存在需要被写在一个类中，这个类我们也给起了个名字叫==通知类==

至此AOP中的核心概念就已经介绍完了，总结下:

* 连接点(JoinPoint)：程序执行过程中的任意位置，粒度为执行方法、抛出异常、设置变量等
  * 在SpringAOP中，理解为方法的执行
* 切入点(Pointcut):匹配连接点的式子
  * 在SpringAOP中，一个切入点可以描述一个具体方法，也可也匹配多个方法
    * 一个具体的方法:如com.itheima.dao包下的BookDao接口中的无形参无返回值的save方法
    * 匹配多个方法:所有的save方法，所有的get开头的方法，所有以Dao结尾的接口中的任意方法，所有带有一个参数的方法
  * 连接点范围要比切入点范围大，是切入点的方法也一定是连接点，但是是连接点的方法就不一定要被增强，所以可能不是切入点。
* 通知(Advice):在切入点处执行的操作，也就是共性功能
  * 在SpringAOP中，功能最终以方法的形式呈现
* 通知类：定义通知的类
* 切面(Aspect):描述通知与切入点的对应关系。

**小结**

这一节中主要讲解了AOP的概念与作用，以及AOP中的核心概念，学完以后大家需要能说出:

* 什么是AOP?
* AOP的作用是什么?
* AOP中核心概念分别指的是什么?
  * 连接点
  * 切入点
  * 通知
  * 通知类
  * 切面

## 2，AOP入门案例

### 2.1 需求分析

案例设定：测算接口执行效率，但是这个案例稍微复杂了点，我们对其进行简化。

简化设定：在方法执行前输出当前系统时间。

对于SpringAOP的开发有两种方式，XML 和 ==注解==，我们使用哪个呢?

因为现在注解使用的比较多，所以本次课程就采用注解完成AOP的开发。

总结需求为:使用SpringAOP的注解方式完成在方法执行的前打印出当前系统时间。

### 2.2 思路分析

需求明确后，具体该如何实现，都有哪些步骤，我们先来分析下:

> 1.导入坐标(pom.xml)
>
> 2.制作连接点(原始操作，Dao接口与实现类)
>
> 3.制作共性功能(通知类与通知)
>
> 4.定义切入点
>
> 5.绑定切入点与通知关系(切面)

### 2.3 环境准备

* 创建一个Maven项目

* pom.xml添加Spring依赖

  ```xml
  <dependencies>
      <dependency>
          <groupId>org.springframework</groupId>
          <artifactId>spring-context</artifactId>
          <version>5.2.10.RELEASE</version>
      </dependency>
  </dependencies>
  ```

* 添加BookDao和BookDaoImpl类

  ```java
  public interface BookDao {
      public void save();
      public void update();
  }
  
  @Repository
  public class BookDaoImpl implements BookDao {
  
      public void save() {
          System.out.println(System.currentTimeMillis());
          System.out.println("book dao save ...");
      }
  
      public void update(){
          System.out.println("book dao update ...");
      }
  }
  ```

* 创建Spring的配置类

  ```java
  @Configuration
  @ComponentScan("com.itheima")
  public class SpringConfig {
  }
  ```

* 编写App运行类

  ```java
  public class App {
      public static void main(String[] args) {
          ApplicationContext ctx = new AnnotationConfigApplicationContext(SpringConfig.class);
          BookDao bookDao = ctx.getBean(BookDao.class);
          bookDao.save();
      }
  }
  ```

最终创建好的项目结构如下:

![1630167092142](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day03/assets/1630167092142.png)

**说明:**

* 目前打印save方法的时候，因为方法中有打印系统时间，所以运行的时候是可以看到系统时间
* 对于update方法来说，就没有该功能
* 我们要使用SpringAOP的方式在不改变update方法的前提下让其具有打印系统时间的功能。



### 2.4 AOP实现步骤

#### 步骤1:添加依赖

pom.xml

```xml
<dependency>
    <groupId>org.aspectj</groupId>
    <artifactId>aspectjweaver</artifactId>
    <version>1.9.4</version>
</dependency>
```

![1630146885493](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day03/assets/1630146885493.png)

* 因为`spring-context`中已经导入了`spring-aop`,所以不需要再单独导入`spring-aop`
* 导入AspectJ的jar包,AspectJ是AOP思想的一个具体实现，Spring有自己的AOP实现，但是相比于AspectJ来说比较麻烦，所以我们直接采用Spring整合ApsectJ的方式进行AOP开发。

#### 步骤2:定义接口与实现类

```
环境准备的时候，BookDaoImpl已经准备好，不需要做任何修改
```

#### 步骤3:定义通知类和通知

通知就是将共性功能抽取出来后形成的方法，共性功能指的就是当前系统时间的打印。

```java
public class MyAdvice {
    public void method(){
        System.out.println(System.currentTimeMillis());
    }
}
```

类名和方法名没有要求，可以任意。

#### 步骤4:定义切入点

BookDaoImpl中有两个方法，分别是save和update，我们要增强的是update方法，该如何定义呢?

```java
public class MyAdvice {
    @Pointcut("execution(void com.itheima.dao.BookDao.update())")
    private void pt(){}
    public void method(){
        System.out.println(System.currentTimeMillis());
    }
}
```

**说明:**

* 切入点定义依托一个不具有实际意义的方法进行，即无参数、无返回值、方法体无实际逻辑。
* execution及后面编写的内容，后面会有章节专门去学习。

#### 步骤5:制作切面

切面是用来描述通知和切入点之间的关系，如何进行关系的绑定?

```java
public class MyAdvice {
    @Pointcut("execution(void com.itheima.dao.BookDao.update())")
    private void pt(){}
    
    @Before("pt()")
    public void method(){
        System.out.println(System.currentTimeMillis());
    }
}
```

绑定切入点与通知关系，并指定通知添加到原始连接点的具体执行==位置==

![1630148447689](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day03/assets/1630148447689.png)

**说明:**@Before翻译过来是之前，也就是说通知会在切入点方法执行之前执行，除此之前还有其他四种类型，后面会讲。

#### 步骤6:将通知类配给容器并标识其为切面类

```java
@Component
@Aspect
public class MyAdvice {
    @Pointcut("execution(void com.itheima.dao.BookDao.update())")
    private void pt(){}
    
    @Before("pt()")
    public void method(){
        System.out.println(System.currentTimeMillis());
    }
}
```

#### 步骤7:开启注解格式AOP功能

```java
@Configuration
@ComponentScan("com.itheima")
@EnableAspectJAutoProxy
public class SpringConfig {
}
```

#### 步骤8:运行程序

```java
public class App {
    public static void main(String[] args) {
        ApplicationContext ctx = new AnnotationConfigApplicationContext(SpringConfig.class);
        BookDao bookDao = ctx.getBean(BookDao.class);
        bookDao.update();
    }
}
```

看到在执行update方法之前打印了系统时间戳，说明对原始方法进行了增强，AOP编程成功。

![1630147945888](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day03/assets/1630147945888.png)

### 知识点1：@EnableAspectJAutoProxy  

| 名称 | @EnableAspectJAutoProxy |
| ---- | ----------------------- |
| 类型 | 配置类注解              |
| 位置 | 配置类定义上方          |
| 作用 | 开启注解格式AOP功能     |

### 知识点2：@Aspect

| 名称 | @Aspect               |
| ---- | --------------------- |
| 类型 | 类注解                |
| 位置 | 切面类定义上方        |
| 作用 | 设置当前类为AOP切面类 |

### 知识点3：@Pointcut   

| 名称 | @Pointcut                   |
| ---- | --------------------------- |
| 类型 | 方法注解                    |
| 位置 | 切入点方法定义上方          |
| 作用 | 设置切入点方法              |
| 属性 | value（默认）：切入点表达式 |

### 知识点4：@Before

| 名称 | @Before                                                      |
| ---- | ------------------------------------------------------------ |
| 类型 | 方法注解                                                     |
| 位置 | 通知方法定义上方                                             |
| 作用 | 设置当前通知方法与切入点之间的绑定关系，当前通知方法在原始切入点方法前运行 |

## 3，AOP工作流程

AOP的入门案例已经完成，对于刚才案例的执行过程，我们就得来分析分析，这一节我们主要讲解两个知识点:`AOP工作流程`和`AOP核心概念`。其中核心概念是对前面核心概念的补充。

### 3.1 AOP工作流程

由于AOP是基于Spring容器管理的bean做的增强，所以整个工作过程需要从Spring加载bean说起:

#### 流程1:Spring容器启动

* 容器启动就需要去加载bean,哪些类需要被加载呢?
* 需要被增强的类，如:BookServiceImpl
* 通知类，如:MyAdvice
* 注意此时bean对象还没有创建成功

#### 流程2:读取所有切面配置中的切入点

![1630151682428](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day03/assets/1630151682428.png)

* 上面这个例子中有两个切入点的配置，但是第一个`ptx()`并没有被使用，所以不会被读取。

#### 流程3:初始化bean，

判定bean对应的类中的方法是否匹配到任意切入点

* 注意第1步在容器启动的时候，bean对象还没有被创建成功。

* 要被实例化bean对象的类中的方法和切入点进行匹配

  ![1630152538083](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day03/assets/1630152538083.png)

  * 匹配失败，创建原始对象,如`UserDao`
    * 匹配失败说明不需要增强，直接调用原始对象的方法即可。
  * 匹配成功，创建原始对象（==目标对象==）的==代理==对象,如:`BookDao`
    * 匹配成功说明需要对其进行增强
    * 对哪个类做增强，这个类对应的对象就叫做目标对象
    * 因为要对目标对象进行功能增强，而采用的技术是动态代理，所以会为其创建一个代理对象
    * 最终运行的是代理对象的方法，在该方法中会对原始方法进行功能增强

#### 流程4:获取bean执行方法

* 获取的bean是原始对象时，调用方法并执行，完成操作
* 获取的bean是代理对象时，根据代理对象的运行模式运行原始方法与增强的内容，完成操作

#### 验证容器中是否为代理对象

为了验证IOC容器中创建的对象和我们刚才所说的结论是否一致，首先先把结论理出来:

* 如果目标对象中的方法会被增强，那么容器中将存入的是目标对象的代理对象
* 如果目标对象中的方法不被增强，那么容器中将存入的是目标对象本身。

##### 验证思路

> 1.要执行的方法，不被定义的切入点包含，即不要增强，打印当前类的getClass()方法
>
> 2.要执行的方法，被定义的切入点包含，即要增强，打印出当前类的getClass()方法
>
> 3.观察两次打印的结果

##### 步骤1:修改App类,获取类的类型

```java
public class App {
    public static void main(String[] args) {
        ApplicationContext ctx = new AnnotationConfigApplicationContext(SpringConfig.class);
        BookDao bookDao = ctx.getBean(BookDao.class);
        System.out.println(bookDao);
        System.out.println(bookDao.getClass());
    }
}
```

##### 步骤2:修改MyAdvice类，不增强

因为定义的切入点中，被修改成`update1`,所以BookDao中的update方法在执行的时候，就不会被增强，

所以容器中的对象应该是目标对象本身。

```java
@Component
@Aspect
public class MyAdvice {
    @Pointcut("execution(void com.itheima.dao.BookDao.update1())")
    private void pt(){}
    
    @Before("pt()")
    public void method(){
        System.out.println(System.currentTimeMillis());
    }
}
```

##### 步骤3:运行程序

![1630154495165](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day03/assets/1630154495165.png)

##### 步骤4:修改MyAdvice类，增强

因为定义的切入点中，被修改成`update`,所以BookDao中的update方法在执行的时候，就会被增强，

所以容器中的对象应该是目标对象的代理对象

```java
@Component
@Aspect
public class MyAdvice {
    @Pointcut("execution(void com.itheima.dao.BookDao.update())")
    private void pt(){}
    
    @Before("pt()")
    public void method(){
        System.out.println(System.currentTimeMillis());
    }
}
```

##### 步骤5:运行程序

![1630154625564](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day03/assets/1630154625564.png)

至此对于刚才的结论，我们就得到了验证，这块大家需要注意的是:

不能直接打印对象，从上面两次结果中可以看出，直接打印对象走的是对象的toString方法，不管是不是代理对象打印的结果都是一样的，原因是内部对toString方法进行了重写。

### 3.2 AOP核心概念

在上面介绍AOP的工作流程中，我们提到了两个核心概念，分别是:

* 目标对象(Target)：原始功能去掉共性功能对应的类产生的对象，这种对象是无法直接完成最终工作的
* 代理(Proxy)：目标对象无法直接完成工作，需要对其进行功能回填，通过原始对象的代理对象实现

上面这两个概念比较抽象，简单来说，

目标对象就是要增强的类[如:BookServiceImpl类]对应的对象，也叫原始对象，不能说它不能运行，只能说它在运行的过程中对于要增强的内容是缺失的。

SpringAOP是在不改变原有设计(代码)的前提下对其进行增强的，它的底层采用的是代理模式实现的，所以要对原始对象进行增强，就需要对原始对象创建代理对象，在代理对象中的方法把通知[如:MyAdvice中的method方法]内容加进去，就实现了增强,这就是我们所说的代理(Proxy)。

**小结**

通过这一节中，我们需要掌握的内容有：

* 能说出AOP的工作流程
* AOP的核心概念
  * 目标对象、连接点、切入点
  * 通知类、通知
  * 切面
  * 代理
* SpringAOP的本质或者可以说底层实现是通过代理模式。

## 4，AOP配置管理

### 4.1 AOP切入点表达式

前面的案例中，有涉及到如下内容:

![1630155937718](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day03/assets/1630155937718.png)

对于AOP中切入点表达式，我们总共会学习三个内容，分别是`语法格式`、`通配符`和`书写技巧`。

#### 4.1.1 语法格式

首先我们先要明确两个概念:

* 切入点:要进行增强的方法
* 切入点表达式:要进行增强的方法的描述方式

对于切入点的描述，我们其实是有两中方式的，先来看下前面的例子

![1630156172790](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day03/assets/1630156172790.png)

描述方式一：执行com.itheima.dao包下的BookDao接口中的无参数update方法

```java
execution(void com.itheima.dao.BookDao.update())
```

描述方式二：执行com.itheima.dao.impl包下的BookDaoImpl类中的无参数update方法

```
execution(void com.itheima.dao.impl.BookDaoImpl.update())
```

因为调用接口方法的时候最终运行的还是其实现类的方法，所以上面两种描述方式都是可以的。

对于切入点表达式的语法为:

* 切入点表达式标准格式：动作关键字(访问修饰符  返回值  包名.类/接口名.方法名(参数) 异常名）

对于这个格式，我们不需要硬记，通过一个例子，理解它:

```
execution(public User com.itheima.service.UserService.findById(int))
```

* execution：动作关键字，描述切入点的行为动作，例如execution表示执行到指定切入点
* public:访问修饰符,还可以是public，private等，可以省略
* User：返回值，写返回值类型
* com.itheima.service：包名，多级包使用点连接
* UserService:类/接口名称
* findById：方法名
* int:参数，直接写参数的类型，多个类型用逗号隔开
* 异常名：方法定义中抛出指定异常，可以省略

切入点表达式就是要找到需要增强的方法，所以它就是对一个具体方法的描述，但是方法的定义会有很多，所以如果每一个方法对应一个切入点表达式，想想这块就会觉得将来编写起来会比较麻烦，有没有更简单的方式呢?

就需要用到下面所学习的通配符。

#### 4.1.2 通配符

我们使用通配符描述切入点，主要的目的就是简化之前的配置，具体都有哪些通配符可以使用?

* `*`:单个独立的任意符号，可以独立出现，也可以作为前缀或者后缀的匹配符出现

  ```
  execution（public * com.itheima.*.UserService.find*(*))
  ```

  匹配com.itheima包下的任意包中的UserService类或接口中所有find开头的带有一个参数的方法

* `..`：多个连续的任意符号，可以独立出现，常用于简化包名与参数的书写

  ```
  execution（public User com..UserService.findById(..))
  ```

  匹配com包下的任意包中的UserService类或接口中所有名称为findById的方法

* `+`：专用于匹配子类类型

  ```
  execution(* *..*Service+.*(..))
  ```

  这个使用率较低，描述子类的，咱们做JavaEE开发，继承机会就一次，使用都很慎重，所以很少用它。*Service+，表示所有以Service结尾的接口的子类。

接下来，我们把案例中使用到的切入点表达式来分析下:

![1630163744963](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day03/assets/1630163744963.png)

```java
execution(void com.itheima.dao.BookDao.update())
匹配接口，能匹配到
execution(void com.itheima.dao.impl.BookDaoImpl.update())
匹配实现类，能匹配到
execution(* com.itheima.dao.impl.BookDaoImpl.update())
返回值任意，能匹配到
execution(* com.itheima.dao.impl.BookDaoImpl.update(*))
返回值任意，但是update方法必须要有一个参数，无法匹配，要想匹配需要在update接口和实现类添加参数
execution(void com.*.*.*.*.update())
返回值为void,com包下的任意包三层包下的任意类的update方法，匹配到的是实现类，能匹配
execution(void com.*.*.*.update())
返回值为void,com包下的任意两层包下的任意类的update方法，匹配到的是接口，能匹配
execution(void *..update())
返回值为void，方法名是update的任意包下的任意类，能匹配
execution(* *..*(..))
匹配项目中任意类的任意方法，能匹配，但是不建议使用这种方式，影响范围广
execution(* *..u*(..))
匹配项目中任意包任意类下只要以u开头的方法，update方法能满足，能匹配
execution(* *..*e(..))
匹配项目中任意包任意类下只要以e结尾的方法，update和save方法能满足，能匹配
execution(void com..*())
返回值为void，com包下的任意包任意类任意方法，能匹配，*代表的是方法
execution(* com.itheima.*.*Service.find*(..))
将项目中所有业务层方法的以find开头的方法匹配
execution(* com.itheima.*.*Service.save*(..))
将项目中所有业务层方法的以save开头的方法匹配
```

后面两种更符合我们平常切入点表达式的编写规则

#### 4.1.3 书写技巧

对于切入点表达式的编写其实是很灵活的，那么在编写的时候，有没有什么好的技巧让我们用用:

- 所有代码按照标准规范开发，否则以下技巧全部失效
- 描述切入点通**==常描述接口==**，而不描述实现类,如果描述到实现类，就出现紧耦合了
- 访问控制修饰符针对接口开发均采用public描述（**==可省略访问控制修饰符描述==**）
- 返回值类型对于增删改类使用精准类型加速匹配，对于查询类使用\*通配快速描述
- **==包名==**书写**==尽量不使用..匹配==**，效率过低，常用\*做单个包描述匹配，或精准匹配
- **==接口名/类名==**书写名称与模块相关的**==采用\*匹配==**，例如UserService书写成\*Service，绑定业务层接口名
- **==方法名==**书写以**==动词==**进行**==精准匹配==**，名词采用*匹配，例如getById书写成getBy*,selectAll书写成selectAll
- 参数规则较为复杂，根据业务方法灵活调整
- 通常**==不使用异常==**作为**==匹配==**规则

### 4.2 AOP通知类型

前面的案例中，有涉及到如下内容:

![1630164718080](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day03/assets/1630164718080.png)

它所代表的含义是将`通知`添加到`切入点`方法执行的==前面==。

除了这个注解外，还有没有其他的注解，换个问题就是除了可以在前面加，能不能在其他的地方加?

#### 4.2.1 类型介绍

我们先来回顾下AOP通知:

* AOP通知描述了抽取的共性功能，根据共性功能抽取的位置不同，最终运行代码时要将其加入到合理的位置

通知具体要添加到切入点的哪里?

共提供了5种通知类型:

- 前置通知
- 后置通知
- **==环绕通知(重点)==**
- 返回后通知(了解)
- 抛出异常后通知(了解)

为了更好的理解这几种通知类型，我们来看一张图

![1630166147697](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day03/assets/1630166147697.png)

(1)前置通知，追加功能到方法执行前,类似于在代码1或者代码2添加内容

(2)后置通知,追加功能到方法执行后,不管方法执行的过程中有没有抛出异常都会执行，类似于在代码5添加内容

(3)返回后通知,追加功能到方法执行后，只有方法正常执行结束后才进行,类似于在代码3添加内容，如果方法执行抛出异常，返回后通知将不会被添加

(4)抛出异常后通知,追加功能到方法抛出异常后，只有方法执行出异常才进行,类似于在代码4添加内容，只有方法抛出异常后才会被添加

(5)环绕通知,环绕通知功能比较强大，它可以追加功能到方法执行的前后，这也是比较常用的方式，它可以实现其他四种通知类型的功能，具体是如何实现的，需要我们往下学习。

#### 4.2.2 环境准备

- 创建一个Maven项目

- pom.xml添加Spring依赖

  ```xml
  <dependencies>
      <dependency>
          <groupId>org.springframework</groupId>
          <artifactId>spring-context</artifactId>
          <version>5.2.10.RELEASE</version>
      </dependency>
      <dependency>
        <groupId>org.aspectj</groupId>
        <artifactId>aspectjweaver</artifactId>
        <version>1.9.4</version>
      </dependency>
  </dependencies>
  ```

- 添加BookDao和BookDaoImpl类

  ```java
  public interface BookDao {
      public void update();
      public int select();
  }
  
  @Repository
  public class BookDaoImpl implements BookDao {
      public void update(){
          System.out.println("book dao update ...");
      }
      public int select() {
          System.out.println("book dao select is running ...");
          return 100;
      }
  }
  ```

- 创建Spring的配置类

  ```java
  @Configuration
  @ComponentScan("com.itheima")
  @EnableAspectJAutoProxy
  public class SpringConfig {
  }
  ```

- 创建通知类

  ```java
  @Component
  @Aspect
  public class MyAdvice {
      @Pointcut("execution(void com.itheima.dao.BookDao.update())")
      private void pt(){}
  
      public void before() {
          System.out.println("before advice ...");
      }
  
      public void after() {
          System.out.println("after advice ...");
      }
  
      public void around(){
          System.out.println("around before advice ...");
          System.out.println("around after advice ...");
      }
  
      public void afterReturning() {
          System.out.println("afterReturning advice ...");
      }
      
      public void afterThrowing() {
          System.out.println("afterThrowing advice ...");
      }
  }
  ```

- 编写App运行类

  ```java
  public class App {
      public static void main(String[] args) {
          ApplicationContext ctx = new AnnotationConfigApplicationContext(SpringConfig.class);
          BookDao bookDao = ctx.getBean(BookDao.class);
          bookDao.update();
      }
  }
  ```

最终创建好的项目结构如下:

![1630167385146](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day03/assets/1630167385146.png)

#### 4.2.3 通知类型的使用

##### 前置通知

修改MyAdvice,在before方法上添加`@Before注解`

```java
@Component
@Aspect
public class MyAdvice {
    @Pointcut("execution(void com.itheima.dao.BookDao.update())")
    private void pt(){}
    
    @Before("pt()")
    //此处也可以写成 @Before("MyAdvice.pt()"),不建议
    public void before() {
        System.out.println("before advice ...");
    }
}
```

![1630167805723](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day03/assets/1630167805723.png)

##### 后置通知

```java
@Component
@Aspect
public class MyAdvice {
    @Pointcut("execution(void com.itheima.dao.BookDao.update())")
    private void pt(){}
    
    @Before("pt()")
    public void before() {
        System.out.println("before advice ...");
    }
    @After("pt()")
    public void after() {
        System.out.println("after advice ...");
    }
}
```

![1630167887131](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day03/assets/1630167887131.png)

##### 环绕通知

###### 基本使用

```java
@Component
@Aspect
public class MyAdvice {
    @Pointcut("execution(void com.itheima.dao.BookDao.update())")
    private void pt(){}
    
    @Around("pt()")
    public void around(){
        System.out.println("around before advice ...");
        System.out.println("around after advice ...");
    }
}
```

![1630167969051](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day03/assets/1630167969051.png)

运行结果中，通知的内容打印出来，但是原始方法的内容却没有被执行。

因为环绕通知需要在原始方法的前后进行增强，所以环绕通知就必须要能对原始操作进行调用，具体如何实现?

```java
@Component
@Aspect
public class MyAdvice {
    @Pointcut("execution(void com.itheima.dao.BookDao.update())")
    private void pt(){}
    
    @Around("pt()")
    public void around(ProceedingJoinPoint pjp) throws Throwable{
        System.out.println("around before advice ...");
        //表示对原始操作的调用
        pjp.proceed();
        System.out.println("around after advice ...");
    }
}
```

**说明:**proceed()为什么要抛出异常?

原因很简单，看下源码就知道了

![1630168248052](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day03/assets/1630168248052.png)

再次运行，程序可以看到原始方法已经被执行了

![1630168293492](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day03/assets/1630168293492.png)

###### 注意事项

(1)原始方法有返回值的处理

* 修改MyAdvice,对BookDao中的select方法添加环绕通知，

```java
@Component
@Aspect
public class MyAdvice {
    @Pointcut("execution(void com.itheima.dao.BookDao.update())")
    private void pt(){}
    
    @Pointcut("execution(int com.itheima.dao.BookDao.select())")
    private void pt2(){}
    
    @Around("pt2()")
    public void aroundSelect(ProceedingJoinPoint pjp) throws Throwable {
        System.out.println("around before advice ...");
        //表示对原始操作的调用
        pjp.proceed();
        System.out.println("around after advice ...");
    }
}
```

* 修改App类，调用select方法

```java
public class App {
    public static void main(String[] args) {
        ApplicationContext ctx = new AnnotationConfigApplicationContext(SpringConfig.class);
        BookDao bookDao = ctx.getBean(BookDao.class);
        int num = bookDao.select();
        System.out.println(num);
    }
}
```

运行后会报错，错误内容为:

Exception in thread "main" org.springframework.aop.AopInvocationException: ==Null return value from advice does not match primitive return type for: public abstract int com.itheima.dao.BookDao.select()==
	at org.springframework.aop.framework.JdkDynamicAopProxy.invoke(JdkDynamicAopProxy.java:226)
	at com.sun.proxy.$Proxy19.select(Unknown Source)
	at com.itheima.App.main(App.java:12)

错误大概的意思是:`空的返回不匹配原始方法的int返回`

* void就是返回Null
* 原始方法就是BookDao下的select方法

所以如果我们使用环绕通知的话，要根据原始方法的返回值来设置环绕通知的返回值，具体解决方案为:

```java
@Component
@Aspect
public class MyAdvice {
    @Pointcut("execution(void com.itheima.dao.BookDao.update())")
    private void pt(){}
    
    @Pointcut("execution(int com.itheima.dao.BookDao.select())")
    private void pt2(){}
    
    @Around("pt2()")
    public Object aroundSelect(ProceedingJoinPoint pjp) throws Throwable {
        System.out.println("around before advice ...");
        //表示对原始操作的调用
        Object ret = pjp.proceed();
        System.out.println("around after advice ...");
        return ret;
    }
}
```

**说明:**

​	为什么返回的是Object而不是int的主要原因是Object类型更通用。

​	在环绕通知中是可以对原始方法返回值就行修改的。

##### 返回后通知

```java
@Component
@Aspect
public class MyAdvice {
    @Pointcut("execution(void com.itheima.dao.BookDao.update())")
    private void pt(){}
    
    @Pointcut("execution(int com.itheima.dao.BookDao.select())")
    private void pt2(){}
    
    @AfterReturning("pt2()")
    public void afterReturning() {
        System.out.println("afterReturning advice ...");
    }
}
```

![1630169124446](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day03/assets/1630169124446.png)



**注意：**返回后通知是需要在原始方法`select`正常执行后才会被执行，如果`select()`方法执行的过程中出现了异常，那么返回后通知是不会被执行。后置通知是不管原始方法有没有抛出异常都会被执行。这个案例大家下去可以自己练习验证下。

##### 异常后通知

```java
@Component
@Aspect
public class MyAdvice {
    @Pointcut("execution(void com.itheima.dao.BookDao.update())")
    private void pt(){}
    
    @Pointcut("execution(int com.itheima.dao.BookDao.select())")
    private void pt2(){}
    
    @AfterReturning("pt2()")
    public void afterThrowing() {
        System.out.println("afterThrowing advice ...");
    }
}
```

![1630169357146](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day03/assets/1630169357146.png)

**注意：**异常后通知是需要原始方法抛出异常，可以在`select()`方法中添加一行代码`int i = 1/0`即可。如果没有抛异常，异常后通知将不会被执行。

学习完这5种通知类型，我们来思考下环绕通知是如何实现其他通知类型的功能的?

因为环绕通知是可以控制原始方法执行的，所以我们把增强的代码写在调用原始方法的不同位置就可以实现不同的通知类型的功能，如:

![1630170090945](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day03/assets/1630170090945.png)

##### 通知类型总结

###### 知识点1：@After

| 名称 | @After                                                       |
| ---- | ------------------------------------------------------------ |
| 类型 | 方法注解                                                     |
| 位置 | 通知方法定义上方                                             |
| 作用 | 设置当前通知方法与切入点之间的绑定关系，当前通知方法在原始切入点方法后运行 |

###### 知识点2：@AfterReturning  

| 名称 | @AfterReturning                                              |
| ---- | ------------------------------------------------------------ |
| 类型 | 方法注解                                                     |
| 位置 | 通知方法定义上方                                             |
| 作用 | 设置当前通知方法与切入点之间绑定关系，当前通知方法在原始切入点方法正常执行完毕后执行 |

###### 知识点3：@AfterThrowing  

| 名称 | @AfterThrowing                                               |
| ---- | ------------------------------------------------------------ |
| 类型 | 方法注解                                                     |
| 位置 | 通知方法定义上方                                             |
| 作用 | 设置当前通知方法与切入点之间绑定关系，当前通知方法在原始切入点方法运行抛出异常后执行 |

###### 知识点4：@Around

| 名称 | @Around                                                      |
| ---- | ------------------------------------------------------------ |
| 类型 | 方法注解                                                     |
| 位置 | 通知方法定义上方                                             |
| 作用 | 设置当前通知方法与切入点之间的绑定关系，当前通知方法在原始切入点方法前后运行 |

==**环绕通知注意事项**==

1. 环绕通知必须依赖形参ProceedingJoinPoint才能实现对原始方法的调用，进而实现原始方法调用前后同时添加通知
2. 通知中如果未使用ProceedingJoinPoint对原始方法进行调用将跳过原始方法的执行
3. 对原始方法的调用可以不接收返回值，通知方法设置成void即可，如果接收返回值，最好设定为Object类型
4. 原始方法的返回值如果是void类型，通知方法的返回值类型可以设置成void,也可以设置成Object
5. 由于无法预知原始方法运行后是否会抛出异常，因此环绕通知方法必须要处理Throwable异常

介绍完这么多种通知类型，具体该选哪一种呢?

我们可以通过一些案例加深下对通知类型的学习。

### 4.3 业务层接口执行效率

#### 4.3.1 需求分析

这个需求也比较简单，前面我们在介绍AOP的时候已经演示过:

* 需求:任意业务层接口执行均可显示其执行效率（执行时长）

这个案例的目的是查看每个业务层执行的时间，这样就可以监控出哪个业务比较耗时，将其查找出来方便优化。

具体实现的思路:

(1) 开始执行方法之前记录一个时间

(2) 执行方法

(3) 执行完方法之后记录一个时间

(4) 用后一个时间减去前一个时间的差值，就是我们需要的结果。

所以要在方法执行的前后添加业务，经过分析我们将采用`环绕通知`。

**说明:**原始方法如果只执行一次，时间太快，两个时间差可能为0，所以我们要执行万次来计算时间差。

#### 4.3.2 环境准备

- 创建一个Maven项目

- pom.xml添加Spring依赖

  ```xml
  <dependencies>
      <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-context</artifactId>
        <version>5.2.10.RELEASE</version>
      </dependency>
      <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-jdbc</artifactId>
        <version>5.2.10.RELEASE</version>
      </dependency>
      <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-test</artifactId>
        <version>5.2.10.RELEASE</version>
      </dependency>
      <dependency>
        <groupId>org.aspectj</groupId>
        <artifactId>aspectjweaver</artifactId>
        <version>1.9.4</version>
      </dependency>
      <dependency>
        <groupId>mysql</groupId>
        <artifactId>mysql-connector-java</artifactId>
        <version>5.1.47</version>
      </dependency>
      <dependency>
        <groupId>com.alibaba</groupId>
        <artifactId>druid</artifactId>
        <version>1.1.16</version>
      </dependency>
      <dependency>
        <groupId>org.mybatis</groupId>
        <artifactId>mybatis</artifactId>
        <version>3.5.6</version>
      </dependency>
      <dependency>
        <groupId>org.mybatis</groupId>
        <artifactId>mybatis-spring</artifactId>
        <version>1.3.0</version>
      </dependency>
      <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
        <version>4.12</version>
        <scope>test</scope>
      </dependency>
    </dependencies>
  ```

- 添加AccountService、AccountServiceImpl、AccountDao与Account类

  ```java
  public interface AccountService {
      void save(Account account);
      void delete(Integer id);
      void update(Account account);
      List<Account> findAll();
      Account findById(Integer id);
  }
  
  @Service
  public class AccountServiceImpl implements AccountService {
  
      @Autowired
      private AccountDao accountDao;
  
      public void save(Account account) {
          accountDao.save(account);
      }
  
      public void update(Account account){
          accountDao.update(account);
      }
  
      public void delete(Integer id) {
          accountDao.delete(id);
      }
  
      public Account findById(Integer id) {
          return accountDao.findById(id);
      }
  
      public List<Account> findAll() {
          return accountDao.findAll();
      }
  }
  public interface AccountDao {
  
      @Insert("insert into tbl_account(name,money)values(#{name},#{money})")
      void save(Account account);
  
      @Delete("delete from tbl_account where id = #{id} ")
      void delete(Integer id);
  
      @Update("update tbl_account set name = #{name} , money = #{money} where id = #{id} ")
      void update(Account account);
  
      @Select("select * from tbl_account")
      List<Account> findAll();
  
      @Select("select * from tbl_account where id = #{id} ")
      Account findById(Integer id);
  }
  
  public class Account implements Serializable {
  
      private Integer id;
      private String name;
      private Double money;
      //setter..getter..toString方法省略
  }
  ```

- resources下提供一个jdbc.properties

  ```properties
  jdbc.driver=com.mysql.jdbc.Driver
  jdbc.url=jdbc:mysql://localhost:3306/spring_db?useSSL=false
  jdbc.username=root
  jdbc.password=root
  ```

- 创建相关配置类

  ```java
  //Spring配置类:SpringConfig
  @Configuration
  @ComponentScan("com.itheima")
  @PropertySource("classpath:jdbc.properties")
  @Import({JdbcConfig.class,MybatisConfig.class})
  public class SpringConfig {
  }
  //JdbcConfig配置类
  public class JdbcConfig {
      @Value("${jdbc.driver}")
      private String driver;
      @Value("${jdbc.url}")
      private String url;
      @Value("${jdbc.username}")
      private String userName;
      @Value("${jdbc.password}")
      private String password;
  
      @Bean
      public DataSource dataSource(){
          DruidDataSource ds = new DruidDataSource();
          ds.setDriverClassName(driver);
          ds.setUrl(url);
          ds.setUsername(userName);
          ds.setPassword(password);
          return ds;
      }
  }
  //MybatisConfig配置类
  public class MybatisConfig {
  
      @Bean
      public SqlSessionFactoryBean sqlSessionFactory(DataSource dataSource){
          SqlSessionFactoryBean ssfb = new SqlSessionFactoryBean();
          ssfb.setTypeAliasesPackage("com.itheima.domain");
          ssfb.setDataSource(dataSource);
          return ssfb;
      }
  
      @Bean
      public MapperScannerConfigurer mapperScannerConfigurer(){
          MapperScannerConfigurer msc = new MapperScannerConfigurer();
          msc.setBasePackage("com.itheima.dao");
          return msc;
      }
  }
  
  ```

- 编写Spring整合Junit的测试类

  ```java
  @RunWith(SpringJUnit4ClassRunner.class)
  @ContextConfiguration(classes = SpringConfig.class)
  public class AccountServiceTestCase {
      @Autowired
      private AccountService accountService;
  
      @Test
      public void testFindById(){
          Account ac = accountService.findById(2);
      }
  
      @Test
      public void testFindAll(){
          List<Account> all = accountService.findAll();
      }
  
  }
  ```

最终创建好的项目结构如下:

![1630214631112](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day03/assets/1630214631112.png)

#### 4.3.3 功能开发

##### 步骤1:开启SpringAOP的注解功能

在Spring的主配置文件SpringConfig类中添加注解

```java
@EnableAspectJAutoProxy
```

##### 步骤2:创建AOP的通知类

* 该类要被Spring管理，需要添加@Component

* 要标识该类是一个AOP的切面类，需要添加@Aspect
* 配置切入点表达式，需要添加一个方法，并添加@Pointcut

```java
@Component
@Aspect
public class ProjectAdvice {
    //配置业务层的所有方法
    @Pointcut("execution(* com.itheima.service.*Service.*(..))")
    private void servicePt(){}
    
    public void runSpeed(){
        
    } 
}
```

##### 步骤3:添加环绕通知

在runSpeed()方法上添加@Around

```java
@Component
@Aspect
public class ProjectAdvice {
    //配置业务层的所有方法
    @Pointcut("execution(* com.itheima.service.*Service.*(..))")
    private void servicePt(){}
    //@Around("ProjectAdvice.servicePt()") 可以简写为下面的方式
    @Around("servicePt()")
    public Object runSpeed(ProceedingJoinPoint pjp){
        Object ret = pjp.proceed();
        return ret;
    } 
}
```

**注意:**目前并没有做任何增强

##### 步骤4:完成核心业务，记录万次执行的时间

```java
@Component
@Aspect
public class ProjectAdvice {
    //配置业务层的所有方法
    @Pointcut("execution(* com.itheima.service.*Service.*(..))")
    private void servicePt(){}
    //@Around("ProjectAdvice.servicePt()") 可以简写为下面的方式
    @Around("servicePt()")
    public void runSpeed(ProceedingJoinPoint pjp){
        
        long start = System.currentTimeMillis();
        for (int i = 0; i < 10000; i++) {
           pjp.proceed();
        }
        long end = System.currentTimeMillis();
        System.out.println("业务层接口万次执行时间: "+(end-start)+"ms");
    } 
}
```

##### 步骤5:运行单元测试类

![1630215355776](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day03/assets/1630215355776.png)

**注意:**因为程序每次执行的时长是不一样的，所以运行多次最终的结果是不一样的。

##### 步骤6:程序优化

目前程序所面临的问题是，多个方法一起执行测试的时候，控制台都打印的是:

`业务层接口万次执行时间:xxxms`

我们没有办法区分到底是哪个接口的哪个方法执行的具体时间，具体如何优化?

```java
@Component
@Aspect
public class ProjectAdvice {
    //配置业务层的所有方法
    @Pointcut("execution(* com.itheima.service.*Service.*(..))")
    private void servicePt(){}
    //@Around("ProjectAdvice.servicePt()") 可以简写为下面的方式
    @Around("servicePt()")
    public void runSpeed(ProceedingJoinPoint pjp){
        //获取执行签名信息
        Signature signature = pjp.getSignature();
        //通过签名获取执行操作名称(接口名)
        String className = signature.getDeclaringTypeName();
        //通过签名获取执行操作名称(方法名)
        String methodName = signature.getName();
        
        long start = System.currentTimeMillis();
        for (int i = 0; i < 10000; i++) {
           pjp.proceed();
        }
        long end = System.currentTimeMillis();
        System.out.println("万次执行："+ className+"."+methodName+"---->" +(end-start) + "ms");
    } 
}
```

##### 步骤7:运行单元测试类

![1630215743444](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day03/assets/1630215743444.png)



==补充说明==

当前测试的接口执行效率仅仅是一个理论值，并不是一次完整的执行过程。

这块只是通过该案例把AOP的使用进行了学习，具体的实际值是有很多因素共同决定的。

### 4.4 AOP通知获取数据

目前我们写AOP仅仅是在原始方法前后追加一些操作，接下来我们要说说AOP中数据相关的内容，我们将从`获取参数`、`获取返回值`和`获取异常`三个方面来研究切入点的相关信息。

前面我们介绍通知类型的时候总共讲了五种，那么对于这五种类型都会有参数，返回值和异常吗?

我们先来一个个分析下:

* 获取切入点方法的参数，所有的通知类型都可以获取参数
  * JoinPoint：适用于前置、后置、返回后、抛出异常后通知
  * ProceedingJoinPoint：适用于环绕通知
* 获取切入点方法返回值，前置和抛出异常后通知是没有返回值，后置通知可有可无，所以不做研究
  * 返回后通知
  * 环绕通知
* 获取切入点方法运行异常信息，前置和返回后通知是不会有，后置通知可有可无，所以不做研究
  * 抛出异常后通知
  * 环绕通知

#### 4.4.1 环境准备

- 创建一个Maven项目

- pom.xml添加Spring依赖

  ```xml
  <dependencies>
      <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-context</artifactId>
        <version>5.2.10.RELEASE</version>
      </dependency>
      <dependency>
        <groupId>org.aspectj</groupId>
        <artifactId>aspectjweaver</artifactId>
        <version>1.9.4</version>
      </dependency>
    </dependencies>
  ```

- 添加BookDao和BookDaoImpl类

  ```java
  public interface BookDao {
      public String findName(int id);
  }
  @Repository
  public class BookDaoImpl implements BookDao {
  
      public String findName(int id) {
          System.out.println("id:"+id);
          return "itcast";
      }
  }
  ```

- 创建Spring的配置类

  ```java
  @Configuration
  @ComponentScan("com.itheima")
  @EnableAspectJAutoProxy
  public class SpringConfig {
  }
  ```

- 编写通知类

  ```java
  @Component
  @Aspect
  public class MyAdvice {
      @Pointcut("execution(* com.itheima.dao.BookDao.findName(..))")
      private void pt(){}
  
      @Before("pt()")
      public void before() {
          System.out.println("before advice ..." );
      }
  
      @After("pt()")
      public void after() {
          System.out.println("after advice ...");
      }
  
      @Around("pt()")
      public Object around() throws Throwable{
          Object ret = pjp.proceed();
          return ret;
      }
      @AfterReturning("pt()")
      public void afterReturning() {
          System.out.println("afterReturning advice ...");
      }
  
  
      @AfterThrowing("pt()")
      public void afterThrowing() {
          System.out.println("afterThrowing advice ...");
      }
  }
  ```

- 编写App运行类

  ```java
  public class App {
      public static void main(String[] args) {
          ApplicationContext ctx = new AnnotationConfigApplicationContext(SpringConfig.class);
          BookDao bookDao = ctx.getBean(BookDao.class);
          String name = bookDao.findName(100);
          System.out.println(name);
      }
  }
  ```

最终创建好的项目结构如下:

![1630233154992](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day03/assets/1630233154992.png)

#### 4.4.2 获取参数

##### 非环绕通知获取方式

在方法上添加JoinPoint,通过JoinPoint来获取参数

```java
@Component
@Aspect
public class MyAdvice {
    @Pointcut("execution(* com.itheima.dao.BookDao.findName(..))")
    private void pt(){}

    @Before("pt()")
    public void before(JoinPoint jp) 
        Object[] args = jp.getArgs();
        System.out.println(Arrays.toString(args));
        System.out.println("before advice ..." );
    }
	//...其他的略
}
```

运行App类，可以获取如下内容，说明参数100已经被获取

![1630233291929](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day03/assets/1630233291929.png)

**思考:方法的参数只有一个，为什么获取的是一个数组?**

因为参数的个数是不固定的，所以使用数组更通配些。

如果将参数改成两个会是什么效果呢?

(1)修改BookDao接口和BookDaoImpl实现类

```java
public interface BookDao {
    public String findName(int id,String password);
}
@Repository
public class BookDaoImpl implements BookDao {

    public String findName(int id,String password) {
        System.out.println("id:"+id);
        return "itcast";
    }
}
```

(2)修改App类，调用方法传入多个参数

```java
public class App {
    public static void main(String[] args) {
        ApplicationContext ctx = new AnnotationConfigApplicationContext(SpringConfig.class);
        BookDao bookDao = ctx.getBean(BookDao.class);
        String name = bookDao.findName(100,"itheima");
        System.out.println(name);
    }
}
```

(3)运行App，查看结果,说明两个参数都已经被获取到

![1630233548743](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day03/assets/1630233548743.png)

**说明:**

使用JoinPoint的方式获取参数适用于`前置`、`后置`、`返回后`、`抛出异常后`通知。剩下的大家自行去验证。

##### 环绕通知获取方式

环绕通知使用的是ProceedingJoinPoint，因为ProceedingJoinPoint是JoinPoint类的子类，所以对于ProceedingJoinPoint类中应该也会有对应的`getArgs()`方法，我们去验证下:

```java
@Component
@Aspect
public class MyAdvice {
    @Pointcut("execution(* com.itheima.dao.BookDao.findName(..))")
    private void pt(){}

    @Around("pt()")
    public Object around(ProceedingJoinPoint pjp)throws Throwable {
        Object[] args = pjp.getArgs();
        System.out.println(Arrays.toString(args));
        Object ret = pjp.proceed();
        return ret;
    }
	//其他的略
}
```

运行App后查看运行结果，说明ProceedingJoinPoint也是可以通过getArgs()获取参数

![1630233974310](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day03/assets/1630233974310.png)

**注意:**

* pjp.proceed()方法是有两个构造方法，分别是:

  ![1630234756123](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day03/assets/1630234756123.png)

  * 调用无参数的proceed，当原始方法有参数，会在调用的过程中自动传入参数

  * 所以调用这两个方法的任意一个都可以完成功能

  * 但是当需要修改原始方法的参数时，就只能采用带有参数的方法,如下:

    ```java
    @Component
    @Aspect
    public class MyAdvice {
        @Pointcut("execution(* com.itheima.dao.BookDao.findName(..))")
        private void pt(){}
    
        @Around("pt()")
        public Object around(ProceedingJoinPoint pjp) throws Throwable{
            Object[] args = pjp.getArgs();
            System.out.println(Arrays.toString(args));
            args[0] = 666;
            Object ret = pjp.proceed(args);
            return ret;
        }
    	//其他的略
    }
    ```

    有了这个特性后，我们就可以在环绕通知中对原始方法的参数进行拦截过滤，避免由于参数的问题导致程序无法正确运行，保证代码的健壮性。

#### 4.4.3 获取返回值

对于返回值，只有返回后`AfterReturing`和环绕`Around`这两个通知类型可以获取，具体如何获取?

##### 环绕通知获取返回值

```java
@Component
@Aspect
public class MyAdvice {
    @Pointcut("execution(* com.itheima.dao.BookDao.findName(..))")
    private void pt(){}

    @Around("pt()")
    public Object around(ProceedingJoinPoint pjp) throws Throwable{
        Object[] args = pjp.getArgs();
        System.out.println(Arrays.toString(args));
        args[0] = 666;
        Object ret = pjp.proceed(args);
        return ret;
    }
	//其他的略
}
```

上述代码中，`ret`就是方法的返回值，我们是可以直接获取，不但可以获取，如果需要还可以进行修改。

##### 返回后通知获取返回值

```java
@Component
@Aspect
public class MyAdvice {
    @Pointcut("execution(* com.itheima.dao.BookDao.findName(..))")
    private void pt(){}

    @AfterReturning(value = "pt()",returning = "ret")
    public void afterReturning(Object ret) {
        System.out.println("afterReturning advice ..."+ret);
    }
	//其他的略
}
```

==注意:==

(1)参数名的问题

![1630237320870](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day03/assets/1630237320870.png)

(2)afterReturning方法参数类型的问题

参数类型可以写成String，但是为了能匹配更多的参数类型，建议写成Object类型

(3)afterReturning方法参数的顺序问题

![1630237586682](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day03/assets/1630237586682.png)

运行App后查看运行结果，说明返回值已经被获取到

![1630237372286](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day03/assets/1630237372286.png)

#### 4.4.4 获取异常

对于获取抛出的异常，只有抛出异常后`AfterThrowing`和环绕`Around`这两个通知类型可以获取，具体如何获取?

##### 环绕通知获取异常

这块比较简单，以前我们是抛出异常，现在只需要将异常捕获，就可以获取到原始方法的异常信息了

```java
@Component
@Aspect
public class MyAdvice {
    @Pointcut("execution(* com.itheima.dao.BookDao.findName(..))")
    private void pt(){}

    @Around("pt()")
    public Object around(ProceedingJoinPoint pjp){
        Object[] args = pjp.getArgs();
        System.out.println(Arrays.toString(args));
        args[0] = 666;
        Object ret = null;
        try{
            ret = pjp.proceed(args);
        }catch(Throwable throwable){
            t.printStackTrace();
        }
        return ret;
    }
	//其他的略
}
```

在catch方法中就可以获取到异常，至于获取到异常以后该如何处理，这个就和你的业务需求有关了。

##### 抛出异常后通知获取异常

```java
@Component
@Aspect
public class MyAdvice {
    @Pointcut("execution(* com.itheima.dao.BookDao.findName(..))")
    private void pt(){}

    @AfterThrowing(value = "pt()",throwing = "t")
    public void afterThrowing(Throwable t) {
        System.out.println("afterThrowing advice ..."+t);
    }
	//其他的略
}
```

如何让原始方法抛出异常，方式有很多，

```java
@Repository
public class BookDaoImpl implements BookDao {

    public String findName(int id,String password) {
        System.out.println("id:"+id);
        if(true){
            throw new NullPointerException();
        }
        return "itcast";
    }
}
```

==注意:==

![1630239939043](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day03/assets/1630239939043.png)

运行App后，查看控制台，就能看的异常信息被打印到控制台

![1630239997560](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day03/assets/1630239997560.png)



至此，AOP通知如何获取数据就已经讲解完了，数据中包含`参数`、`返回值`、`异常(了解)`。

### 4.5 百度网盘密码数据兼容处理

#### 4.5.1 需求分析

需求: 对百度网盘分享链接输入密码时尾部多输入的空格做兼容处理。

![1630240203033](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day03/assets/1630240203033.png)

问题描述:

* 点击链接，会提示，请输入提取码，如下图所示

  ![1630240528228](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day03/assets/1630240528228.png)

* 当我们从别人发给我们的内容中复制提取码的时候，有时候会多复制到一些空格，直接粘贴到百度的提取码输入框

* 但是百度那边记录的提取码是没有空格的

* 这个时候如果不做处理，直接对比的话，就会引发提取码不一致，导致无法访问百度盘上的内容

* 所以多输入一个空格可能会导致项目的功能无法正常使用。

* 此时我们就想能不能将输入的参数先帮用户去掉空格再操作呢?

答案是可以的，我们只需要在业务方法执行之前对所有的输入参数进行格式处理——trim()

* 是对所有的参数都需要去除空格么?

也没有必要，一般只需要针对字符串处理即可。

* 以后涉及到需要去除前后空格的业务可能会有很多，这个去空格的代码是每个业务都写么?

可以考虑使用AOP来统一处理。

* AOP有五种通知类型，该使用哪种呢?

我们的需求是将原始方法的参数处理后在参与原始方法的调用，能做这件事的就只有环绕通知。

综上所述，我们需要考虑两件事:
①：在业务方法执行之前对所有的输入参数进行格式处理——trim()
②：使用处理后的参数调用原始方法——环绕通知中存在对原始方法的调用

#### 4.5.2 环境准备

- 创建一个Maven项目

- pom.xml添加Spring依赖

  ```xml
  <dependencies>
      <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-context</artifactId>
        <version>5.2.10.RELEASE</version>
      </dependency>
      <dependency>
        <groupId>org.aspectj</groupId>
        <artifactId>aspectjweaver</artifactId>
        <version>1.9.4</version>
      </dependency>
    </dependencies>
  ```

- 添加ResourcesService，ResourcesServiceImpl,ResourcesDao和ResourcesDaoImpl类

  ```java
  public interface ResourcesDao {
      boolean readResources(String url, String password);
  }
  @Repository
  public class ResourcesDaoImpl implements ResourcesDao {
      public boolean readResources(String url, String password) {
          //模拟校验
          return password.equals("root");
      }
  }
  public interface ResourcesService {
      public boolean openURL(String url ,String password);
  }
  @Service
  public class ResourcesServiceImpl implements ResourcesService {
      @Autowired
      private ResourcesDao resourcesDao;
  
      public boolean openURL(String url, String password) {
          return resourcesDao.readResources(url,password);
      }
  }
  
  ```

- 创建Spring的配置类

  ```java
  @Configuration
  @ComponentScan("com.itheima")
  public class SpringConfig {
  }
  ```

- 编写App运行类

  ```java
  public class App {
      public static void main(String[] args) {
          ApplicationContext ctx = new AnnotationConfigApplicationContext(SpringConfig.class);
          ResourcesService resourcesService = ctx.getBean(ResourcesService.class);
          boolean flag = resourcesService.openURL("http://pan.baidu.com/haha", "root");
          System.out.println(flag);
      }
  }
  ```

最终创建好的项目结构如下:

![1630241681697](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day03/assets/1630241681697.png)

现在项目的效果是，当输入密码为"root"控制台打印为true,如果密码改为"root  "控制台打印的是false

需求是使用AOP将参数进行统一处理，不管输入的密码`root`前后包含多少个空格，最终控制台打印的都是true。

#### 4.5.3 具体实现

##### 步骤1:开启SpringAOP的注解功能

```java
@Configuration
@ComponentScan("com.itheima")
@EnableAspectJAutoProxy
public class SpringConfig {
}
```

##### 步骤2:编写通知类

```java
@Component
@Aspect
public class DataAdvice {
    @Pointcut("execution(boolean com.itheima.service.*Service.*(*,*))")
    private void servicePt(){}
    
}
```

##### 步骤3:添加环绕通知

```java
@Component
@Aspect
public class DataAdvice {
    @Pointcut("execution(boolean com.itheima.service.*Service.*(*,*))")
    private void servicePt(){}
    
    @Around("DataAdvice.servicePt()")
    // @Around("servicePt()")这两种写法都对
    public Object trimStr(ProceedingJoinPoint pjp) throws Throwable {
        Object ret = pjp.proceed();
        return ret;
    }
    
}
```

##### 步骤4:完成核心业务，处理参数中的空格

```java
@Component
@Aspect
public class DataAdvice {
    @Pointcut("execution(boolean com.itheima.service.*Service.*(*,*))")
    private void servicePt(){}
    
    @Around("DataAdvice.servicePt()")
    // @Around("servicePt()")这两种写法都对
    public Object trimStr(ProceedingJoinPoint pjp) throws Throwable {
        //获取原始方法的参数
        Object[] args = pjp.getArgs();
        for (int i = 0; i < args.length; i++) {
            //判断参数是不是字符串
            if(args[i].getClass().equals(String.class)){
                args[i] = args[i].toString().trim();
            }
        }
        //将修改后的参数传入到原始方法的执行中
        Object ret = pjp.proceed(args);
        return ret;
    }
    
}
```

##### 步骤5:运行程序

不管密码`root`前后是否加空格，最终控制台打印的都是true

##### 步骤6:优化测试

为了能更好的看出AOP已经生效，我们可以修改ResourcesImpl类，在方法中将密码的长度进行打印

```java
@Repository
public class ResourcesDaoImpl implements ResourcesDao {
    public boolean readResources(String url, String password) {
        System.out.println(password.length());
        //模拟校验
        return password.equals("root");
    }
}
```

再次运行成功，就可以根据最终打印的长度来看看，字符串的空格有没有被去除掉。

**注意：**

![1630242491831](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day03/assets/1630242491831.png)

## 5，AOP总结

AOP的知识就已经讲解完了，接下来对于AOP的知识进行一个总结:

### 5.1 AOP的核心概念

* 概念：AOP(Aspect Oriented Programming)面向切面编程，一种编程范式
* 作用：在不惊动原始设计的基础上为方法进行功能==增强==
* 核心概念
  * 代理（Proxy）：SpringAOP的核心本质是采用代理模式实现的
  * 连接点（JoinPoint）：在SpringAOP中，理解为任意方法的执行
  * 切入点（Pointcut）：匹配连接点的式子，也是具有共性功能的方法描述
  * 通知（Advice）：若干个方法的共性功能，在切入点处执行，最终体现为一个方法
  * 切面（Aspect）：描述通知与切入点的对应关系
  * 目标对象（Target）：被代理的原始对象成为目标对象

### 5.2 切入点表达式

* 切入点表达式标准格式：动作关键字(访问修饰符  返回值  包名.类/接口名.方法名（参数）异常名)

  ```
  execution(* com.itheima.service.*Service.*(..))
  ```

* 切入点表达式描述通配符：

  * 作用：用于快速描述，范围描述
  * `*`：匹配任意符号（常用）
  * `..` ：匹配多个连续的任意符号（常用）
  * `+`：匹配子类类型

* 切入点表达式书写技巧

  1.按==标准规范==开发
  2.查询操作的返回值建议使用\*匹配
  3.减少使用..的形式描述包
  4.==对接口进行描述==，使用\*表示模块名，例如UserService的匹配描述为*Service
  5.方法名书写保留动词，例如get，使用\*表示名词，例如getById匹配描述为getBy\*
  6.参数根据实际情况灵活调整

### 5.3 五种通知类型

- 前置通知
- 后置通知
- 环绕通知（重点）
  - 环绕通知依赖形参ProceedingJoinPoint才能实现对原始方法的调用
  - 环绕通知可以隔离原始方法的调用执行
  - 环绕通知返回值设置为Object类型
  - 环绕通知中可以对原始方法调用过程中出现的异常进行处理
- 返回后通知
- 抛出异常后通知

### 5.4 通知中获取参数

- 获取切入点方法的参数，所有的通知类型都可以获取参数
  - JoinPoint：适用于前置、后置、返回后、抛出异常后通知
  - ProceedingJoinPoint：适用于环绕通知
- 获取切入点方法返回值，前置和抛出异常后通知是没有返回值，后置通知可有可无，所以不做研究
  - 返回后通知
  - 环绕通知
- 获取切入点方法运行异常信息，前置和返回后通知是不会有，后置通知可有可无，所以不做研究
  - 抛出异常后通知
  - 环绕通知

## 6，AOP事务管理

### 6.1 Spring事务简介

#### 6.1.1 相关概念介绍

- 事务作用：在数据层保障一系列的数据库操作同成功同失败
- Spring事务作用：在数据层或**==业务层==**保障一系列的数据库操作同成功同失败

数据层有事务我们可以理解，为什么业务层也需要处理事务呢?

举个简单的例子，

* 转账业务会有两次数据层的调用，一次是加钱一次是减钱
* 把事务放在数据层，加钱和减钱就有两个事务
* 没办法保证加钱和减钱同时成功或者同时失败
* 这个时候就需要将事务放在业务层进行处理。

Spring为了管理事务，提供了一个平台事务管理器`PlatformTransactionManager`

![1630243651541](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day03/assets/1630243651541.png)

commit是用来提交事务，rollback是用来回滚事务。

PlatformTransactionManager只是一个接口，Spring还为其提供了一个具体的实现:

![1630243993380](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day03/assets/1630243993380.png)

从名称上可以看出，我们只需要给它一个DataSource对象，它就可以帮你去在业务层管理事务。其内部采用的是JDBC的事务。所以说如果你持久层采用的是JDBC相关的技术，就可以采用这个事务管理器来管理你的事务。而Mybatis内部采用的就是JDBC的事务，所以后期我们Spring整合Mybatis就采用的这个DataSourceTransactionManager事务管理器。

#### 6.1.2 转账案例-需求分析

接下来通过一个案例来学习下Spring是如何来管理事务的。

先来分析下需求:

需求: 实现任意两个账户间转账操作

需求微缩: A账户减钱，B账户加钱

为了实现上述的业务需求，我们可以按照下面步骤来实现下:
①：数据层提供基础操作，指定账户减钱（outMoney），指定账户加钱（inMoney）

②：业务层提供转账操作（transfer），调用减钱与加钱的操作

③：提供2个账号和操作金额执行转账操作

④：基于Spring整合MyBatis环境搭建上述操作

#### 6.1.3 转账案例-环境搭建

##### 步骤1:准备数据库表

之前我们在整合Mybatis的时候已经创建了这个表,可以直接使用

```sql
create database spring_db character set utf8;
use spring_db;
create table tbl_account(
    id int primary key auto_increment,
    name varchar(35),
    money double
);
insert into tbl_account values(1,'Tom',1000);
insert into tbl_account values(2,'Jerry',1000);
```

##### 步骤2:创建项目导入jar包

项目的pom.xml添加相关依赖

```xml
<dependencies>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-context</artifactId>
      <version>5.2.10.RELEASE</version>
    </dependency>
    <dependency>
      <groupId>com.alibaba</groupId>
      <artifactId>druid</artifactId>
      <version>1.1.16</version>
    </dependency>

    <dependency>
      <groupId>org.mybatis</groupId>
      <artifactId>mybatis</artifactId>
      <version>3.5.6</version>
    </dependency>

    <dependency>
      <groupId>mysql</groupId>
      <artifactId>mysql-connector-java</artifactId>
      <version>5.1.47</version>
    </dependency>

    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-jdbc</artifactId>
      <version>5.2.10.RELEASE</version>
    </dependency>

    <dependency>
      <groupId>org.mybatis</groupId>
      <artifactId>mybatis-spring</artifactId>
      <version>1.3.0</version>
    </dependency>

    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>4.12</version>
      <scope>test</scope>
    </dependency>

    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-test</artifactId>
      <version>5.2.10.RELEASE</version>
    </dependency>

  </dependencies>
```

##### 步骤3:根据表创建模型类

```java
public class Account implements Serializable {

    private Integer id;
    private String name;
    private Double money;
	//setter...getter...toString...方法略    
}
```

##### 步骤4:创建Dao接口

```java
public interface AccountDao {

    @Update("update tbl_account set money = money + #{money} where name = #{name}")
    void inMoney(@Param("name") String name, @Param("money") Double money);

    @Update("update tbl_account set money = money - #{money} where name = #{name}")
    void outMoney(@Param("name") String name, @Param("money") Double money);
}
```

##### 步骤5:创建Service接口和实现类

```java
public interface AccountService {
    /**
     * 转账操作
     * @param out 传出方
     * @param in 转入方
     * @param money 金额
     */
    public void transfer(String out,String in ,Double money) ;
}

@Service
public class AccountServiceImpl implements AccountService {

    @Autowired
    private AccountDao accountDao;

    public void transfer(String out,String in ,Double money) {
        accountDao.outMoney(out,money);
        accountDao.inMoney(in,money);
    }

}
```

##### 步骤6:添加jdbc.properties文件

```properties
jdbc.driver=com.mysql.jdbc.Driver
jdbc.url=jdbc:mysql://localhost:3306/spring_db?useSSL=false
jdbc.username=root
jdbc.password=root
```

##### 步骤7:创建JdbcConfig配置类

```java
public class JdbcConfig {
    @Value("${jdbc.driver}")
    private String driver;
    @Value("${jdbc.url}")
    private String url;
    @Value("${jdbc.username}")
    private String userName;
    @Value("${jdbc.password}")
    private String password;

    @Bean
    public DataSource dataSource(){
        DruidDataSource ds = new DruidDataSource();
        ds.setDriverClassName(driver);
        ds.setUrl(url);
        ds.setUsername(userName);
        ds.setPassword(password);
        return ds;
    }
}
```

##### 步骤8:创建MybatisConfig配置类

```java
public class MybatisConfig {

    @Bean
    public SqlSessionFactoryBean sqlSessionFactory(DataSource dataSource){
        SqlSessionFactoryBean ssfb = new SqlSessionFactoryBean();
        ssfb.setTypeAliasesPackage("com.itheima.domain");
        ssfb.setDataSource(dataSource);
        return ssfb;
    }

    @Bean
    public MapperScannerConfigurer mapperScannerConfigurer(){
        MapperScannerConfigurer msc = new MapperScannerConfigurer();
        msc.setBasePackage("com.itheima.dao");
        return msc;
    }
}
```

##### 步骤9:创建SpringConfig配置类

```java
@Configuration
@ComponentScan("com.itheima")
@PropertySource("classpath:jdbc.properties")
@Import({JdbcConfig.class,MybatisConfig.class})
public class SpringConfig {
}

```

##### 步骤10:编写测试类

```java
@RunWith(SpringJUnit4ClassRunner.class)
@ContextConfiguration(classes = SpringConfig.class)
public class AccountServiceTest {

    @Autowired
    private AccountService accountService;

    @Test
    public void testTransfer() throws IOException {
        accountService.transfer("Tom","Jerry",100D);
    }

}
```

最终创建好的项目结构如下:

![1630247220645](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day03/assets/1630247220645.png)

#### 6.1.4 事务管理

上述环境，运行单元测试类，会执行转账操作，`Tom`的账户会减少100，`Jerry`的账户会加100。

这是正常情况下的运行结果，但是如果在转账的过程中出现了异常，如:

```java
@Service
public class AccountServiceImpl implements AccountService {

    @Autowired
    private AccountDao accountDao;

    public void transfer(String out,String in ,Double money) {
        accountDao.outMoney(out,money);
        int i = 1/0;
        accountDao.inMoney(in,money);
    }

}
```

这个时候就模拟了转账过程中出现异常的情况，正确的操作应该是转账出问题了，`Tom`应该还是900，`Jerry`应该还是1100，但是真正运行后会发现，并没有像我们想象的那样，`Tom`账户为800而`Jerry`还是1100,100块钱凭空消息了，银行乐疯了。如果把转账换个顺序，银行就该哭了。

不管哪种情况，都是不允许出现的，对刚才的结果我们做一个分析:

①：程序正常执行时，账户金额A减B加，没有问题

②：程序出现异常后，转账失败，但是异常之前操作成功，异常之后操作失败，整体业务失败

当程序出问题后，我们需要让事务进行回滚，而且这个事务应该是加在业务层上，而Spring的事务管理就是用来解决这类问题的。

Spring事务管理具体的实现步骤为:

##### 步骤1:在需要被事务管理的方法上添加注解

```java
public interface AccountService {
    /**
     * 转账操作
     * @param out 传出方
     * @param in 转入方
     * @param money 金额
     */
    //配置当前接口方法具有事务
    public void transfer(String out,String in ,Double money) ;
}

@Service
public class AccountServiceImpl implements AccountService {

    @Autowired
    private AccountDao accountDao;
	@Transactional
    public void transfer(String out,String in ,Double money) {
        accountDao.outMoney(out,money);
        int i = 1/0;
        accountDao.inMoney(in,money);
    }

}
```

==注意:==

@Transactional可以写在接口类上、接口方法上、实现类上和实现类方法上

* 写在接口类上，该接口的所有实现类的所有方法都会有事务
* 写在接口方法上，该接口的所有实现类的该方法都会有事务
* 写在实现类上，该类中的所有方法都会有事务
* 写在实现类方法上，该方法上有事务
* ==建议写在实现类或实现类的方法上==

##### 步骤2:在JdbcConfig类中配置事务管理器

```java
public class JdbcConfig {
    @Value("${jdbc.driver}")
    private String driver;
    @Value("${jdbc.url}")
    private String url;
    @Value("${jdbc.username}")
    private String userName;
    @Value("${jdbc.password}")
    private String password;

    @Bean
    public DataSource dataSource(){
        DruidDataSource ds = new DruidDataSource();
        ds.setDriverClassName(driver);
        ds.setUrl(url);
        ds.setUsername(userName);
        ds.setPassword(password);
        return ds;
    }

    //配置事务管理器，mybatis使用的是jdbc事务
    @Bean
    public PlatformTransactionManager transactionManager(DataSource dataSource){
        DataSourceTransactionManager transactionManager = new DataSourceTransactionManager();
        transactionManager.setDataSource(dataSource);
        return transactionManager;
    }
}
```

**注意：**事务管理器要根据使用技术进行选择，Mybatis框架使用的是JDBC事务，可以直接使用`DataSourceTransactionManager`

##### 步骤3：开启事务注解

在SpringConfig的配置类中开启

```java
@Configuration
@ComponentScan("com.itheima")
@PropertySource("classpath:jdbc.properties")
@Import({JdbcConfig.class,MybatisConfig.class
//开启注解式事务驱动
@EnableTransactionManagement
public class SpringConfig {
}

```

##### 步骤4:运行测试类

会发现在转换的业务出现错误后，事务就可以控制回顾，保证数据的正确性。

##### 知识点1：@EnableTransactionManagement

| 名称 | @EnableTransactionManagement           |
| ---- | -------------------------------------- |
| 类型 | 配置类注解                             |
| 位置 | 配置类定义上方                         |
| 作用 | 设置当前Spring环境中开启注解式事务支持 |

##### 知识点2：@Transactional   

| 名称 | @Transactional                                               |
| ---- | ------------------------------------------------------------ |
| 类型 | 接口注解  类注解  方法注解                                   |
| 位置 | 业务层接口上方  业务层实现类上方  业务方法上方               |
| 作用 | 为当前业务层方法添加事务（如果设置在类或接口上方则类或接口中所有方法均添加事务） |

### 6.2 Spring事务角色

这节中我们重点要理解两个概念，分别是`事务管理员`和`事务协调员`。

1. 未开启Spring事务之前:

![1630248794837](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day03/assets/1630248794837.png)

* AccountDao的outMoney因为是修改操作，会开启一个事务T1
* AccountDao的inMoney因为是修改操作，会开启一个事务T2
* AccountService的transfer没有事务，
  * 运行过程中如果没有抛出异常，则T1和T2都正常提交，数据正确
  * 如果在两个方法中间抛出异常，T1因为执行成功提交事务，T2因为抛异常不会被执行
  * 就会导致数据出现错误

2. 开启Spring的事务管理后

![1630249111055](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day03/assets/1630249111055.png)

* transfer上添加了@Transactional注解，在该方法上就会有一个事务T
* AccountDao的outMoney方法的事务T1加入到transfer的事务T中
* AccountDao的inMoney方法的事务T2加入到transfer的事务T中
* 这样就保证他们在同一个事务中，当业务层中出现异常，整个事务就会回滚，保证数据的准确性。

通过上面例子的分析，我们就可以得到如下概念:



- 事务管理员：发起事务方，在Spring中通常指代业务层开启事务的方法
- 事务协调员：加入事务方，在Spring中通常指代数据层方法，也可以是业务层方法

==注意:==

目前的事务管理是基于`DataSourceTransactionManager`和`SqlSessionFactoryBean`使用的是同一个数据源。

### 6.3 Spring事务属性

上一节我们介绍了两个概念，事务的管理员和事务的协同员，对于这两个概念具体做什么的，我们待会通过案例来使用下。除了这两个概念，还有就是事务的其他相关配置都有哪些，就是我们接下来要学习的内容。

在这一节中，我们主要学习三部分内容`事务配置`、`转账业务追加日志`、`事务传播行为`。

#### 6.3.1 事务配置

![1630250069844](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day03/assets/1630250069844.png)

上面这些属性都可以在`@Transactional`注解的参数上进行设置。

* readOnly：true只读事务，false读写事务，增删改要设为false,查询设为true。

* timeout:设置超时时间单位秒，在多长时间之内事务没有提交成功就自动回滚，-1表示不设置超时时间。

* rollbackFor:当出现指定异常进行事务回滚

* noRollbackFor:当出现指定异常不进行事务回滚

  * 思考:出现异常事务会自动回滚，这个是我们之前就已经知道的

  * noRollbackFor是设定对于指定的异常不回滚，这个好理解

  * rollbackFor是指定回滚异常，对于异常事务不应该都回滚么，为什么还要指定?

    * 这块需要更正一个知识点，并不是所有的异常都会回滚事务，比如下面的代码就不会回滚

      ```java
      public interface AccountService {
          /**
           * 转账操作
           * @param out 传出方
           * @param in 转入方
           * @param money 金额
           */
          //配置当前接口方法具有事务
          public void transfer(String out,String in ,Double money) throws IOException;
      }
      
      @Service
      public class AccountServiceImpl implements AccountService {
      
          @Autowired
          private AccountDao accountDao;
      	@Transactional
          public void transfer(String out,String in ,Double money) throws IOException{
              accountDao.outMoney(out,money);
              //int i = 1/0; //这个异常事务会回滚
              if(true){
                  throw new IOException(); //这个异常事务就不会回滚
              }
              accountDao.inMoney(in,money);
          }
      
      }
      ```

* 出现这个问题的原因是，Spring的事务只会对`Error异常`和`RuntimeException异常`及其子类进行事务回顾，其他的异常类型是不会回滚的，对应IOException不符合上述条件所以不回滚
      

  * 此时就可以使用rollbackFor属性来设置出现IOException异常不回滚

    ```java
    @Service
    public class AccountServiceImpl implements AccountService {
    
        @Autowired
        private AccountDao accountDao;
    	 @Transactional(rollbackFor = {IOException.class})
        public void transfer(String out,String in ,Double money) throws IOException{
            accountDao.outMoney(out,money);
            //int i = 1/0; //这个异常事务会回滚
            if(true){
                throw new IOException(); //这个异常事务就不会回滚
            }
            accountDao.inMoney(in,money);
        }
    
    }
    ```

* rollbackForClassName等同于rollbackFor,只不过属性为异常的类全名字符串

* noRollbackForClassName等同于noRollbackFor，只不过属性为异常的类全名字符串

* isolation设置事务的隔离级别

  * DEFAULT   :默认隔离级别, 会采用数据库的隔离级别
  * READ_UNCOMMITTED : 读未提交
  * READ_COMMITTED : 读已提交
  * REPEATABLE_READ : 重复读取
  * SERIALIZABLE: 串行化

介绍完上述属性后，还有最后一个事务的传播行为，为了讲解该属性的设置，我们需要完成下面的案例。


#### 6.3.2 转账业务追加日志案例

##### 6.3.2.1 需求分析

在前面的转案例的基础上添加新的需求，完成转账后记录日志。

- 需求：实现任意两个账户间转账操作，并对每次转账操作在数据库进行留痕
- 需求微缩：A账户减钱，B账户加钱，数据库记录日志

基于上述的业务需求，我们来分析下该如何实现:

①：基于转账操作案例添加日志模块，实现数据库中记录日志

②：业务层转账操作（transfer），调用减钱、加钱与记录日志功能

需要注意一点就是，我们这个案例的预期效果为:

==无论转账操作是否成功，均进行转账操作的日志留痕==

##### 6.3.2.2 环境准备

该环境是基于转账环境来完成的，所以环境的准备可以参考`6.1.3的环境搭建步骤`，在其基础上，我们继续往下写

###### 步骤1:创建日志表

```sql
create table tbl_log(
   id int primary key auto_increment,
   info varchar(255),
   createDate datetime
)
```

###### 步骤2:添加LogDao接口

```java
public interface LogDao {
    @Insert("insert into tbl_log (info,createDate) values(#{info},now())")
    void log(String info);
}

```

###### 步骤3:添加LogService接口与实现类

```java
public interface LogService {
    void log(String out, String in, Double money);
}
@Service
public class LogServiceImpl implements LogService {

    @Autowired
    private LogDao logDao;
	@Transactional
    public void log(String out,String in,Double money ) {
        logDao.log("转账操作由"+out+"到"+in+",金额："+money);
    }
}
```

###### 步骤4:在转账的业务中添加记录日志

```java
public interface AccountService {
    /**
     * 转账操作
     * @param out 传出方
     * @param in 转入方
     * @param money 金额
     */
    //配置当前接口方法具有事务
    public void transfer(String out,String in ,Double money)throws IOException ;
}
@Service
public class AccountServiceImpl implements AccountService {

    @Autowired
    private AccountDao accountDao;
    @Autowired
    private LogService logService;
	@Transactional
    public void transfer(String out,String in ,Double money) {
        try{
            accountDao.outMoney(out,money);
            accountDao.inMoney(in,money);
        }finally {
            logService.log(out,in,money);
        }
    }

}
```

###### 步骤5:运行程序

* 当程序正常运行，tbl_account表中转账成功，tbl_log表中日志记录成功

* 当转账业务之间出现异常(int i =1/0),转账失败，tbl_account成功回滚，但是tbl_log表未添加数据
* 这个结果和我们想要的不一样，什么原因?该如何解决?
* 失败原因:日志的记录与转账操作隶属同一个事务，同成功同失败
* 最终效果:无论转账操作是否成功，日志必须保留

#### 6.3.3 事务传播行为

![1630253779575](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day03/assets/1630253779575.png)

对于上述案例的分析:

* log方法、inMoney方法和outMoney方法都属于增删改，分别有事务T1,T2,T3
* transfer因为加了@Transactional注解，也开启了事务T
* 前面我们讲过Spring事务会把T1,T2,T3都加入到事务T中
* 所以当转账失败后，所有的事务都回滚，导致日志没有记录下来
* 这和我们的需求不符，这个时候我们就想能不能让log方法单独是一个事务呢?

要想解决这个问题，就需要用到事务传播行为，所谓的事务传播行为指的是:

事务传播行为：事务协调员对事务管理员所携带事务的处理态度。

具体如何解决，就需要用到之前我们没有说的`propagation属性`。

##### 1.修改logService改变事务的传播行为

```java
@Service
public class LogServiceImpl implements LogService {

    @Autowired
    private LogDao logDao;
	//propagation设置事务属性：传播行为设置为当前操作需要新事务
    @Transactional(propagation = Propagation.REQUIRES_NEW)
    public void log(String out,String in,Double money ) {
        logDao.log("转账操作由"+out+"到"+in+",金额："+money);
    }
}
```

运行后，就能实现我们想要的结果，不管转账是否成功，都会记录日志。

##### 2.事务传播行为的可选值

![1630254257628](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Spring笔记/spring_day03/assets/1630254257628.png)

对于我们开发实际中使用的话，因为默认值需要事务是常态的。根据开发过程选择其他的就可以了，例如案例中需要新事务就需要手工配置。其实入账和出账操作上也有事务，采用的就是默认值。

# SpringMVC_day01

**今日内容**

>* 理解SpringMVC相关概念
>* 完成SpringMVC的入门案例
>* 学会使用PostMan工具发送请求和数据
>* 掌握SpringMVC如何接收请求、数据和响应结果
>* 掌握RESTful风格及其使用
>* 完成基于RESTful的案例编写

SpringMVC是隶属于Spring框架的一部分，主要是用来进行Web开发，是对Servlet进行了封装。

对于SpringMVC我们主要学习如下内容:

* SpringMVC简介
* ==请求与响应==
* ==REST风格==
* ==SSM整合(注解版)==
* 拦截器

SpringMVC是处于Web层的框架，所以其主要的作用就是用来接收前端发过来的请求和数据然后经过处理并将处理的结果响应给前端，所以如何处理请求和响应是SpringMVC中非常重要的一块内容。

REST是一种软件架构风格，可以降低开发的复杂性，提高系统的可伸缩性，后期的应用也是非常广泛。

SSM整合是把咱们所学习的SpringMVC+Spring+Mybatis整合在一起来完成业务开发，是对我们所学习这三个框架的一个综合应用。

对于SpringMVC的学习，最终要达成的目标:

1. ==掌握基于SpringMVC获取请求参数和响应json数据操作==
2. ==熟练应用基于REST风格的请求路径设置与参数传递==
3. 能够根据实际业务建立前后端开发通信协议并进行实现
4. ==基于SSM整合技术开发任意业务模块功能==

## 1，SpringMVC概述

学习SpringMVC我们先来回顾下现在web程序是如何做的，咱们现在web程序大都基于三层架构来实现。

三层架构

![1630427303762](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day01/assets/1630427303762.png)

* 浏览器发送一个请求给后端服务器，后端服务器现在是使用Servlet来接收请求和数据

* 如果所有的处理都交给Servlet来处理的话，所有的东西都耦合在一起，对后期的维护和扩展极为不利

* 将后端服务器Servlet拆分成三层，分别是`web`、`service`和`dao`
  * web层主要由servlet来处理，负责页面请求和数据的收集以及响应结果给前端
  * service层主要负责业务逻辑的处理
  * dao层主要负责数据的增删改查操作
* servlet处理请求和数据的时候，存在的问题是一个servlet只能处理一个请求
* 针对web层进行了优化，采用了MVC设计模式，将其设计为`controller`、`view`和`Model`
  * controller负责请求和数据的接收，接收后将其转发给service进行业务处理
  * service根据需要会调用dao对数据进行增删改查
  * dao把数据处理完后将结果交给service,service再交给controller
  * controller根据需求组装成Model和View,Model和View组合起来生成页面转发给前端浏览器
  * 这样做的好处就是controller可以处理多个请求，并对请求进行分发，执行不同的业务操作。

随着互联网的发展，上面的模式因为是同步调用，性能慢慢的跟不是需求，所以异步调用慢慢的走到了前台，是现在比较流行的一种处理方式。

![1630427769938](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day01/assets/1630427769938.png)



* 因为是异步调用，所以后端不需要返回view视图，将其去除
* 前端如果通过异步调用的方式进行交互，后台就需要将返回的数据转换成json格式进行返回
* SpringMVC==主要==负责的就是
  * controller如何接收请求和数据
  * 如何将请求和数据转发给业务层
  * 如何将响应数据转换成json发回到前端

介绍了这么多，对SpringMVC进行一个定义

* SpringMVC是一种基于Java实现MVC模型的轻量级Web框架

* 优点

  * 使用简单、开发便捷(相比于Servlet)
  * 灵活性强

  这里所说的优点，就需要我们在使用的过程中慢慢体会。

## 2，SpringMVC入门案例

因为SpringMVC是一个Web框架，将来是要替换Servlet,所以先来回顾下以前Servlet是如何进行开发的?

1.创建web工程(Maven结构)

2.设置tomcat服务器，加载web工程(tomcat插件)

3.导入坐标(Servlet)

4.定义处理请求的功能类(UserServlet)

5.设置请求映射(配置映射关系)

SpringMVC的制作过程和上述流程几乎是一致的，具体的实现流程是什么?

1.创建web工程(Maven结构)

2.设置tomcat服务器，加载web工程(tomcat插件)

3.导入坐标(==SpringMVC==+Servlet)

4.定义处理请求的功能类(==UserController==)

5.==设置请求映射(配置映射关系)==

6.==将SpringMVC设定加载到Tomcat容器中==

### 2.1 需求分析

### 2.2 案例制作

#### 步骤1:创建Maven项目

打开IDEA,创建一个新的web项目

![1630428920116](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day01/assets/1630428920116.png)

#### 步骤2:补全目录结构

因为使用骨架创建的项目结构不完整，需要手动补全

![1630429288339](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day01/assets/1630429288339.png)

#### 步骤3:导入jar包

将pom.xml中多余的内容删除掉，再添加SpringMVC需要的依赖

```java
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.itheima</groupId>
  <artifactId>springmvc_01_quickstart</artifactId>
  <version>1.0-SNAPSHOT</version>
  <packaging>war</packaging>

  <dependencies>
    <dependency>
      <groupId>javax.servlet</groupId>
      <artifactId>javax.servlet-api</artifactId>
      <version>3.1.0</version>
      <scope>provided</scope>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-webmvc</artifactId>
      <version>5.2.10.RELEASE</version>
    </dependency>
  </dependencies>

  <build>
    <plugins>
      <plugin>
        <groupId>org.apache.tomcat.maven</groupId>
        <artifactId>tomcat7-maven-plugin</artifactId>
        <version>2.1</version>
        <configuration>
          <port>80</port>
          <path>/</path>
        </configuration>
      </plugin>
    </plugins>
  </build>
</project>

```

**说明:**servlet的坐标为什么需要添加`<scope>provided</scope>`?

* scope是maven中jar包依赖作用范围的描述，
* 如果不设置默认是`compile`在在编译、运行、测试时均有效
* 如果运行有效的话就会和tomcat中的servlet-api包发生冲突，导致启动报错

* provided代表的是该包只在编译和测试的时候用，运行的时候无效直接使用tomcat中的，就避免冲突

#### 步骤4:创建配置类

```java
@Configuration
@ComponentScan("com.itheima.controller")
public class SpringMvcConfig {
}
```

#### 步骤5:创建Controller类

```java
@Controller
public class UserController {
    
    @RequestMapping("/save")
    public void save(){
        System.out.println("user save ...");
    }
}

```

#### 步骤6:使用配置类替换web.xml

将web.xml删除，换成ServletContainersInitConfig

```java
public class ServletContainersInitConfig extends AbstractDispatcherServletInitializer {
    //加载springmvc配置类
    protected WebApplicationContext createServletApplicationContext() {
        //初始化WebApplicationContext对象
        AnnotationConfigWebApplicationContext ctx = new AnnotationConfigWebApplicationContext();
        //加载指定配置类
        ctx.register(SpringMvcConfig.class);
        return ctx;
    }

    //设置由springmvc控制器处理的请求映射路径
    protected String[] getServletMappings() {
        return new String[]{"/"};
    }

    //加载spring配置类
    protected WebApplicationContext createRootApplicationContext() {
        return null;
    }
}
```

#### 步骤7:配置Tomcat环境

![1630430302683](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day01/assets/1630430302683.png)

#### 步骤8:启动运行项目

![1630430345246](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day01/assets/1630430345246.png)

#### 步骤9:浏览器访问

浏览器输入`http://localhost/save`进行访问，会报如下错误:

#### ![1630430401561](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day01/assets/1630430401561.png)

页面报错的原因是后台没有指定返回的页面，目前只需要关注控制台看`user save ...`有没有被执行即可。

#### 步骤10:修改Controller返回值解决上述问题

前面我们说过现在主要的是前端发送异步请求，后台响应json数据，所以接下来我们把Controller类的save方法进行修改

```java
@Controller
public class UserController {
    
    @RequestMapping("/save")
    public String save(){
        System.out.println("user save ...");
        return "{'info':'springmvc'}";
    }
}

```

再次重启tomcat服务器，然后重新通过浏览器测试访问,会发现还是会报错，这次的错是404

![1630430658028](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day01/assets/1630430658028.png)

出错的原因是，如果方法直接返回字符串，springmvc会把字符串当成页面的名称在项目中进行查找返回，因为不存在对应返回值名称的页面，所以会报404错误，找不到资源。

而我们其实是想要直接返回的是json数据，具体如何修改呢?

#### 步骤11:设置返回数据为json

```java
@Controller
public class UserController {
    
    @RequestMapping("/save")
    @ResponseBody
    public String save(){
        System.out.println("user save ...");
        return "{'info':'springmvc'}";
    }
}

```

再次重启tomcat服务器，然后重新通过浏览器测试访问，就能看到返回的结果数据

![1630430835628](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day01/assets/1630430835628.png)

至此SpringMVC的入门案例就已经完成。

**注意事项**

* SpringMVC是基于Spring的，在pom.xml只导入了`spring-webmvc`jar包的原因是它会自动依赖spring相关坐标
* AbstractDispatcherServletInitializer类是SpringMVC提供的快速初始化Web3.0容器的抽象类
* AbstractDispatcherServletInitializer提供了三个接口方法供用户实现
  * createServletApplicationContext方法，创建Servlet容器时，加载SpringMVC对应的bean并放入WebApplicationContext对象范围中，而WebApplicationContext的作用范围为ServletContext范围，即整个web容器范围
  * getServletMappings方法，设定SpringMVC对应的请求映射路径，即SpringMVC拦截哪些请求
  * createRootApplicationContext方法，如果创建Servlet容器时需要加载非SpringMVC对应的bean,使用当前方法进行，使用方式和createServletApplicationContext相同。
  * createServletApplicationContext用来加载SpringMVC环境
  * createRootApplicationContext用来加载Spring环境

### 知识点1：@Controller

| 名称 | @Controller                   |
| ---- | ----------------------------- |
| 类型 | 类注解                        |
| 位置 | SpringMVC控制器类定义上方     |
| 作用 | 设定SpringMVC的核心控制器bean |

### 知识点2：@RequestMapping

| 名称     | @RequestMapping                 |
| -------- | ------------------------------- |
| 类型     | 类注解或方法注解                |
| 位置     | SpringMVC控制器类或方法定义上方 |
| 作用     | 设置当前控制器方法请求访问路径  |
| 相关属性 | value(默认)，请求访问路径       |

### 知识点3：@ResponseBody

| 名称 | @ResponseBody                                    |
| ---- | ------------------------------------------------ |
| 类型 | 类注解或方法注解                                 |
| 位置 | SpringMVC控制器类或方法定义上方                  |
| 作用 | 设置当前控制器方法响应内容为当前返回值，无需解析 |

### 2.3 入门案例总结

- 一次性工作
  - 创建工程，设置服务器，加载工程
  - 导入坐标
  - 创建web容器启动类，加载SpringMVC配置，并设置SpringMVC请求拦截路径
  - SpringMVC核心配置类（设置配置类，扫描controller包，加载Controller控制器bean）
- 多次工作
  - 定义处理请求的控制器类
  - 定义处理请求的控制器方法，并配置映射路径（@RequestMapping）与返回json数据（@ResponseBody）

### 2.4 工作流程解析

为了更好的使用SpringMVC,我们将SpringMVC的使用过程总共分两个阶段来分析，分别是`启动服务器初始化过程`和`单次请求过程`

![1630432494752](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day01/assets/1630432494752.png)

#### 2.4.1 启动服务器初始化过程

1. 服务器启动，执行ServletContainersInitConfig类，初始化web容器

   * 功能类似于以前的web.xml

2. 执行createServletApplicationContext方法，创建了WebApplicationContext对象

   * 该方法加载SpringMVC的配置类SpringMvcConfig来初始化SpringMVC的容器

3. 加载SpringMvcConfig配置类

   ![1630433335744](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day01/assets/1630433335744.png)

4. 执行@ComponentScan加载对应的bean

   * 扫描指定包及其子包下所有类上的注解，如Controller类上的@Controller注解

5. 加载UserController，每个@RequestMapping的名称对应一个具体的方法

   ![1630433398932](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day01/assets/1630433398932.png)

   * 此时就建立了 `/save` 和 save方法的对应关系

6. 执行getServletMappings方法，设定SpringMVC拦截请求的路径规则

   ![1630433510528](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day01/assets/1630433510528.png)

   * `/`代表所拦截请求的路径规则，只有被拦截后才能交给SpringMVC来处理请求


#### 2.4.2 单次请求过程

1. 发送请求`http://localhost/save`
2. web容器发现该请求满足SpringMVC拦截规则，将请求交给SpringMVC处理
3. 解析请求路径/save
4. 由/save匹配执行对应的方法save(）
   * 上面的第五步已经将请求路径和方法建立了对应关系，通过/save就能找到对应的save方法
5. 执行save()
6. 检测到有@ResponseBody直接将save()方法的返回值作为响应体返回给请求方

### 2.5 bean加载控制

#### 2.5.1 问题分析

入门案例的内容已经做完了，在入门案例中我们创建过一个`SpringMvcConfig`的配置类，再回想前面咱们学习Spring的时候也创建过一个配置类`SpringConfig`。这两个配置类都需要加载资源，那么它们分别都需要加载哪些内容?

我们先来看下目前我们的项目目录结构:

![1630459727575](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day01/assets/1630459727575.png)

* config目录存入的是配置类,写过的配置类有:

  * ServletContainersInitConfig
  * SpringConfig
  * SpringMvcConfig
  * JdbcConfig
  * MybatisConfig
* controller目录存放的是SpringMVC的controller类
* service目录存放的是service接口和实现类
* dao目录存放的是dao/Mapper接口

controller、service和dao这些类都需要被容器管理成bean对象，那么到底是该让SpringMVC加载还是让Spring加载呢?

* SpringMVC加载其相关bean(表现层bean),也就是controller包下的类
* Spring控制的bean
  * 业务bean(Service)
  * 功能bean(DataSource,SqlSessionFactoryBean,MapperScannerConfigurer等)

分析清楚谁该管哪些bean以后，接下来要解决的问题是如何让Spring和SpringMVC分开加载各自的内容。

在SpringMVC的配置类`SpringMvcConfig`中使用注解`@ComponentScan`，我们只需要将其扫描范围设置到controller即可，如

![1630460319004](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day01/assets/1630460319004.png)

在Spring的配置类`SpringConfig`中使用注解`@ComponentScan`,当时扫描的范围中其实是已经包含了controller,如:

![1630460408159](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day01/assets/1630460408159.png)

从包结构来看的话，Spring已经多把SpringMVC的controller类也给扫描到，所以针对这个问题该如何解决，就是咱们接下来要学习的内容。

概括的描述下咱们现在的问题就是==因为功能不同，如何避免Spring错误加载到SpringMVC的bean?==

#### 2.5.2 思路分析

针对上面的问题，解决方案也比较简单，就是:

* 加载Spring控制的bean的时候排除掉SpringMVC控制的bean

具体该如何排除：

* 方式一:Spring加载的bean设定扫描范围为精准范围，例如service包、dao包等
* 方式二:Spring加载的bean设定扫描范围为com.itheima,排除掉controller包中的bean
* 方式三:不区分Spring与SpringMVC的环境，加载到同一个环境中[了解即可]

#### 2.5.4 环境准备

- 创建一个Web的Maven项目

- pom.xml添加Spring依赖

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  
  <project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
  
    <groupId>com.itheima</groupId>
    <artifactId>springmvc_02_bean_load</artifactId>
    <version>1.0-SNAPSHOT</version>
    <packaging>war</packaging>
  
    <dependencies>
      <dependency>
        <groupId>javax.servlet</groupId>
        <artifactId>javax.servlet-api</artifactId>
        <version>3.1.0</version>
        <scope>provided</scope>
      </dependency>
      <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-webmvc</artifactId>
        <version>5.2.10.RELEASE</version>
      </dependency>
      <dependency>
        <groupId>com.alibaba</groupId>
        <artifactId>druid</artifactId>
        <version>1.1.16</version>
      </dependency>
  
      <dependency>
        <groupId>org.mybatis</groupId>
        <artifactId>mybatis</artifactId>
        <version>3.5.6</version>
      </dependency>
  
      <dependency>
        <groupId>mysql</groupId>
        <artifactId>mysql-connector-java</artifactId>
        <version>5.1.47</version>
      </dependency>
  
      <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-jdbc</artifactId>
        <version>5.2.10.RELEASE</version>
      </dependency>
  
      <dependency>
        <groupId>org.mybatis</groupId>
        <artifactId>mybatis-spring</artifactId>
        <version>1.3.0</version>
      </dependency>
    </dependencies>
  
    <build>
      <plugins>
        <plugin>
          <groupId>org.apache.tomcat.maven</groupId>
          <artifactId>tomcat7-maven-plugin</artifactId>
          <version>2.1</version>
          <configuration>
            <port>80</port>
            <path>/</path>
          </configuration>
        </plugin>
      </plugins>
    </build>
  </project>
  
  ```

- 创建对应的配置类

  ```java
  public class ServletContainersInitConfig extends AbstractDispatcherServletInitializer {
      protected WebApplicationContext createServletApplicationContext() {
          AnnotationConfigWebApplicationContext ctx = new AnnotationConfigWebApplicationContext();
          ctx.register(SpringMvcConfig.class);
          return ctx;
      }
      protected String[] getServletMappings() {
          return new String[]{"/"};
      }
      protected WebApplicationContext createRootApplicationContext() {
        return null;
      }
  }
  
  @Configuration
  @ComponentScan("com.itheima.controller")
  public class SpringMvcConfig {
  }
  
  @Configuration
  @ComponentScan("com.itheima")
  public class SpringConfig {
  }
  
  ```

- 编写Controller，Service，Dao，Domain类

  ```java
  @Controller
  public class UserController {
  
      @RequestMapping("/save")
      @ResponseBody
      public String save(){
          System.out.println("user save ...");
          return "{'info':'springmvc'}";
      }
  }
  
  public interface UserService {
      public void save(User user);
  }
  
  @Service
  public class UserServiceImpl implements UserService {
      public void save(User user) {
          System.out.println("user service ...");
      }
  }
  
  public interface UserDao {
      @Insert("insert into tbl_user(name,age)values(#{name},#{age})")
      public void save(User user);
  }
  public class User {
      private Integer id;
      private String name;
      private Integer age;
      //setter..getter..toString略
  }
  ```

最终创建好的项目结构如下:

![1630461261820](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day01/assets/1630461261820.png)

#### 2.5.5 设置bean加载控制

方式一:修改Spring配置类，设定扫描范围为精准范围。

```java
@Configuration
@ComponentScan({"com.itheima.service","com.itheima.dao"})
public class SpringConfig {
}
```

**说明:**

上述只是通过例子说明可以精确指定让Spring扫描对应的包结构，真正在做开发的时候，因为Dao最终是交给`MapperScannerConfigurer`对象来进行扫描处理的，我们只需要将其扫描到service包即可。



本次dao层由mybatis代理开发，即自动创建的对象，不需要导入，加上“com.itheima.dao”的通用性更好一些，当不使用mybatis，或者自己实现dao层实现类时，依旧可以正常运作



方式二:修改Spring配置类，设定扫描范围为com.itheima,排除掉controller包中的bean

```java
@Configuration
@ComponentScan(value="com.itheima",
    excludeFilters=@ComponentScan.Filter(
    	type = FilterType.ANNOTATION,
        classes = Controller.class
    )
)
public class SpringConfig {
}
```

* excludeFilters属性：设置扫描加载bean时，排除的过滤规则

* type属性：设置排除规则，当前使用按照bean定义时的注解类型进行排除

  * ANNOTATION：按照注解排除
  * ASSIGNABLE_TYPE:按照指定的类型过滤
  * ASPECTJ:按照Aspectj表达式排除，基本上不会用
  * REGEX:按照正则表达式排除
  * CUSTOM:按照自定义规则排除

  大家只需要知道第一种ANNOTATION即可

* classes属性：设置排除的具体注解类，当前设置排除@Controller定义的bean

如何测试controller类已经被排除掉了?

```java
public class App{
	public static void main (String[] args){
        AnnotationConfigApplicationContext ctx = new AnnotationConfigApplicationContext(SpringConfig.class);
        System.out.println(ctx.getBean(UserController.class));
    }
}
```

如果被排除了，该方法执行就会报bean未被定义的错误

![1630462200947](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day01/assets/1630462200947.png)

==注意:测试的时候，需要把SpringMvcConfig配置类上的@ComponentScan注解注释掉，否则不会报错==

出现问题的原因是，

* Spring配置类扫描的包是`com.itheima`
* SpringMVC的配置类，`SpringMvcConfig`上有一个@Configuration注解，也会被Spring扫描到
* SpringMvcConfig上又有一个@ComponentScan，把controller类又给扫描进来了
* 所以如果不把@ComponentScan注释掉，Spring配置类将Controller排除，但是因为扫描到SpringMVC的配置类，又将其加载回来，演示的效果就出不来
* 解决方案，也简单，把SpringMVC的配置类移出Spring配置类的扫描范围即可。

最后一个问题，有了Spring的配置类，要想在tomcat服务器启动将其加载，我们需要修改ServletContainersInitConfig

```java
public class ServletContainersInitConfig extends AbstractDispatcherServletInitializer {
    protected WebApplicationContext createServletApplicationContext() {
        AnnotationConfigWebApplicationContext ctx = new AnnotationConfigWebApplicationContext();
        ctx.register(SpringMvcConfig.class);
        return ctx;
    }
    protected String[] getServletMappings() {
        return new String[]{"/"};
    }
    protected WebApplicationContext createRootApplicationContext() {
      AnnotationConfigWebApplicationContext ctx = new AnnotationConfigWebApplicationContext();
        ctx.register(SpringConfig.class);
        return ctx;
    }
}
```

对于上述的配置方式，Spring还提供了一种更简单的配置方式，可以不用再去创建`AnnotationConfigWebApplicationContext`对象，不用手动`register`对应的配置类，如何实现?

```java
public class ServletContainersInitConfig extends AbstractAnnotationConfigDispatcherServletInitializer {

    protected Class<?>[] getRootConfigClasses() {
        return new Class[]{SpringConfig.class};
    }

    protected Class<?>[] getServletConfigClasses() {
        return new Class[]{SpringMvcConfig.class};
    }

    protected String[] getServletMappings() {
        return new String[]{"/"};
    }
}
```



### 知识点1：@ComponentScan

| 名称     | @ComponentScan                                               |
| -------- | ------------------------------------------------------------ |
| 类型     | 类注解                                                       |
| 位置     | 类定义上方                                                   |
| 作用     | 设置spring配置类扫描路径，用于加载使用注解格式定义的bean     |
| 相关属性 | excludeFilters:排除扫描路径中加载的bean,需要指定类别(type)和具体项(classes)<br/>includeFilters:加载指定的bean，需要指定类别(type)和具体项(classes) |





## 3，PostMan工具的使用

### 3.1 PostMan简介

代码编写完后，我们要想测试，只需要打开浏览器直接输入地址发送请求即可。发送的是`GET`请求可以直接使用浏览器，但是如果要发送的是`POST`请求呢?

如果要求发送的是post请求，我们就得准备页面在页面上准备form表单，测试起来比较麻烦。所以我们就需要借助一些第三方工具，如PostMan.

* PostMan是一款功能强大的网页调试与发送网页HTTP请求的Chrome插件。![1630463382386](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day01/assets/1630463382386.png)
* 作用：常用于进行接口测试

* 特征
  * 简单
  * 实用
  * 美观
  * 大方

### 3.2 PostMan安装

双击`资料\Postman-win64-8.3.1-Setup.exe`即可自动安装，

安装完成后，如果需要注册，可以按照提示进行注册，如果底部有跳过测试的链接也可以点击跳过注册

![1630463816424](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day01/assets/1630463816424.png)

看到如下界面，就说明已经安装成功。

![1630463887711](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day01/assets/1630463887711.png)

### 3.3 PostMan使用

#### 3.3.1 创建WorkSpace工作空间

![](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day01/assets/image-20210805150044862.png)

#### 3.3.2 发送请求

![1630464489898](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day01/assets/1630464489898.png)

#### 3.3.3 保存当前请求

![1630464783034](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day01/assets/1630464783034.png)

**注意:**第一次请求需要创建一个新的目录，后面就不需要创建新目录，直接保存到已经创建好的目录即可。

## 4，请求与响应

前面我们已经完成了入门案例相关的知识学习，接来了我们就需要针对SpringMVC相关的知识点进行系统的学习，之前我们提到过，SpringMVC是web层的框架，主要的作用是接收请求、接收数据、响应结果，所以这一章节是学习SpringMVC的==重点==内容，我们主要会讲解四部分内容:

* 请求映射路径
* 请求参数
* 日期类型参数传递
* 响应json数据

### 4.1 设置请求映射路径

#### 4.1.1 环境准备

- 创建一个Web的Maven项目

- pom.xml添加Spring依赖

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  
  <project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
  
    <groupId>com.itheima</groupId>
    <artifactId>springmvc_03_request_mapping</artifactId>
    <version>1.0-SNAPSHOT</version>
    <packaging>war</packaging>
  
    <dependencies>
      <dependency>
        <groupId>javax.servlet</groupId>
        <artifactId>javax.servlet-api</artifactId>
        <version>3.1.0</version>
        <scope>provided</scope>
      </dependency>
      <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-webmvc</artifactId>
        <version>5.2.10.RELEASE</version>
      </dependency>
    </dependencies>
  
    <build>
      <plugins>
        <plugin>
          <groupId>org.apache.tomcat.maven</groupId>
          <artifactId>tomcat7-maven-plugin</artifactId>
          <version>2.1</version>
          <configuration>
            <port>80</port>
            <path>/</path>
          </configuration>
        </plugin>
      </plugins>
    </build>
  </project>
  
  ```

- 创建对应的配置类

  ```java
  public class ServletContainersInitConfig extends AbstractAnnotationConfigDispatcherServletInitializer {
  
      protected Class<?>[] getServletConfigClasses() {
          return new Class[]{SpringMvcConfig.class};
      }
      protected String[] getServletMappings() {
          return new String[]{"/"};
      }
      protected Class<?>[] getRootConfigClasses() {
          return new Class[0];
      }
  }
  
  @Configuration
  @ComponentScan("com.itheima.controller")
  public class SpringMvcConfig {
  }
  
  ```

- 编写BookController和UserController

  ```java
  @Controller
  public class UserController {
  
      @RequestMapping("/save")
      @ResponseBody
      public String save(){
          System.out.println("user save ...");
          return "{'module':'user save'}";
      }
      
      @RequestMapping("/delete")
      @ResponseBody
      public String save(){
          System.out.println("user delete ...");
          return "{'module':'user delete'}";
      }
  }
  
  @Controller
  public class BookController {
  
      @RequestMapping("/save")
      @ResponseBody
      public String save(){
          System.out.println("book save ...");
          return "{'module':'book save'}";
      }
  }
  ```

最终创建好的项目结构如下:

![1630466431549](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day01/assets/1630466431549.png)

把环境准备好后，启动Tomcat服务器，后台会报错:

![1630466555934](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day01/assets/1630466555934.png)

从错误信息可以看出:

* UserController有一个save方法，访问路径为`http://localhost/save`
* BookController也有一个save方法，访问路径为`http://localhost/save`
* 当访问`http://localhost/saved`的时候，到底是访问UserController还是BookController?

#### 4.1.2 问题分析

团队多人开发，每人设置不同的请求路径，冲突问题该如何解决?

解决思路:为不同模块设置模块名作为请求路径前置

对于Book模块的save,将其访问路径设置`http://localhost/book/save`

对于User模块的save,将其访问路径设置`http://localhost/user/save`

这样在同一个模块中出现命名冲突的情况就比较少了。

#### 4.1.3 设置映射路径

##### 步骤1:修改Controller

```java
@Controller
public class UserController {

    @RequestMapping("/user/save")
    @ResponseBody
    public String save(){
        System.out.println("user save ...");
        return "{'module':'user save'}";
    }
    
    @RequestMapping("/user/delete")
    @ResponseBody
    public String save(){
        System.out.println("user delete ...");
        return "{'module':'user delete'}";
    }
}

@Controller
public class BookController {

    @RequestMapping("/book/save")
    @ResponseBody
    public String save(){
        System.out.println("book save ...");
        return "{'module':'book save'}";
    }
}
```

问题是解决了，但是每个方法前面都需要进行修改，写起来比较麻烦而且还有很多重复代码，如果/user后期发生变化，所有的方法都需要改，耦合度太高。

##### 步骤2:优化路径配置

优化方案:

```java
@Controller
@RequestMapping("/user")
public class UserController {

    @RequestMapping("/save")
    @ResponseBody
    public String save(){
        System.out.println("user save ...");
        return "{'module':'user save'}";
    }
    
    @RequestMapping("/delete")
    @ResponseBody
    public String save(){
        System.out.println("user delete ...");
        return "{'module':'user delete'}";
    }
}

@Controller
@RequestMapping("/book")
public class BookController {

    @RequestMapping("/save")
    @ResponseBody
    public String save(){
        System.out.println("book save ...");
        return "{'module':'book save'}";
    }
}
```

**注意:**

* 当类上和方法上都添加了`@RequestMapping`注解，前端发送请求的时候，要和两个注解的value值相加匹配才能访问到。
* @RequestMapping注解value属性前面加不加`/`都可以

扩展小知识:

对于PostMan如何觉得字小不好看，可以使用`ctrl+=`调大，`ctrl+-`调小。

### 4.2 请求参数

请求路径设置好后，只要确保页面发送请求地址和后台Controller类中配置的路径一致，就可以接收到前端的请求，接收到请求后，如何接收页面传递的参数?

关于请求参数的传递与接收是和请求方式有关系的，目前比较常见的两种请求方式为：

* GET
* POST

针对于不同的请求前端如何发送，后端如何接收?

#### 4.2.1 环境准备

- 创建一个Web的Maven项目

- pom.xml添加Spring依赖

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  
  <project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
  
    <groupId>com.itheima</groupId>
    <artifactId>springmvc_03_request_mapping</artifactId>
    <version>1.0-SNAPSHOT</version>
    <packaging>war</packaging>
  
    <dependencies>
      <dependency>
        <groupId>javax.servlet</groupId>
        <artifactId>javax.servlet-api</artifactId>
        <version>3.1.0</version>
        <scope>provided</scope>
      </dependency>
      <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-webmvc</artifactId>
        <version>5.2.10.RELEASE</version>
      </dependency>
    </dependencies>
  
    <build>
      <plugins>
        <plugin>
          <groupId>org.apache.tomcat.maven</groupId>
          <artifactId>tomcat7-maven-plugin</artifactId>
          <version>2.1</version>
          <configuration>
            <port>80</port>
            <path>/</path>
          </configuration>
        </plugin>
      </plugins>
    </build>
  </project>
  
  ```

- 创建对应的配置类

  ```java
  public class ServletContainersInitConfig extends AbstractAnnotationConfigDispatcherServletInitializer {
  
      protected Class<?>[] getServletConfigClasses() {
          return new Class[]{SpringMvcConfig.class};
      }
      protected String[] getServletMappings() {
          return new String[]{"/"};
      }
      protected Class<?>[] getRootConfigClasses() {
          return new Class[0];
      }
  }
  
  @Configuration
  @ComponentScan("com.itheima.controller")
  public class SpringMvcConfig {
  }
  
  ```

- 编写UserController

  ```java
  @Controller
  public class UserController {
  
      @RequestMapping("/commonParam")
      @ResponseBody
      public String commonParam(){
          return "{'module':'commonParam'}";
      }
  }
  ```

* 编写模型类，User和Address

  ```java
  public class Address {
      private String province;
      private String city;
      //setter...getter...略
  }
  public class User {
      private String name;
      private int age;
      //setter...getter...略
  }
  ```

最终创建好的项目结构如下:

![1630467830654](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day01/assets/1630467830654.png)

#### 4.2.2 参数传递

##### GET发送单个参数

发送请求与参数:

```
http://localhost/commonParam?name=itcast
```

![1630467921300](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day01/assets/1630467921300.png)

接收参数：

```java
@Controller
public class UserController {

    @RequestMapping("/commonParam")
    @ResponseBody
    public String commonParam(String name){
        System.out.println("普通参数传递 name ==> "+name);
        return "{'module':'commonParam'}";
    }
}
```

##### GET发送多个参数

发送请求与参数:

```
http://localhost/commonParam?name=itcast&age=15
```

![1630468045733](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day01/assets/1630468045733.png)

接收参数：

```java
@Controller
public class UserController {

    @RequestMapping("/commonParam")
    @ResponseBody
    public String commonParam(String name,int age){
        System.out.println("普通参数传递 name ==> "+name);
        System.out.println("普通参数传递 age ==> "+age);
        return "{'module':'commonParam'}";
    }
}
```

##### GET请求中文乱码

如果我们传递的参数中有中文，你会发现接收到的参数会出现中文乱码问题。

发送请求:`http://localhost/commonParam?name=张三&age=18`

控制台:

![1630480536510](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day01/assets/1630480536510.png)

出现乱码的原因相信大家都清楚，Tomcat8.5以后的版本已经处理了中文乱码的问题，但是IDEA中的Tomcat插件目前只到Tomcat7，所以需要修改pom.xml来解决GET请求中文乱码问题

```xml
<build>
    <plugins>
      <plugin>
        <groupId>org.apache.tomcat.maven</groupId>
        <artifactId>tomcat7-maven-plugin</artifactId>
        <version>2.1</version>
        <configuration>
          <port>80</port><!--tomcat端口号-->
          <path>/</path> <!--虚拟目录-->
          <uriEncoding>UTF-8</uriEncoding><!--访问路径编解码字符集-->
        </configuration>
      </plugin>
    </plugins>
  </build>
```

##### POST发送参数

发送请求与参数:

![1630480812809](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day01/assets/1630480812809.png)接收参数：

和GET一致，不用做任何修改

```java
@Controller
public class UserController {

    @RequestMapping("/commonParam")
    @ResponseBody
    public String commonParam(String name,int age){
        System.out.println("普通参数传递 name ==> "+name);
        System.out.println("普通参数传递 age ==> "+age);
        return "{'module':'commonParam'}";
    }
}
```

##### POST请求中文乱码

发送请求与参数:

![1630480964421](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day01/assets/1630480964421.png)

接收参数:

控制台打印，会发现有中文乱码问题。

![1630481008109](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day01/assets/1630481008109.png)

解决方案:配置过滤器

```java
public class ServletContainersInitConfig extends AbstractAnnotationConfigDispatcherServletInitializer {
    protected Class<?>[] getRootConfigClasses() {
        return new Class[0];
    }

    protected Class<?>[] getServletConfigClasses() {
        return new Class[]{SpringMvcConfig.class};
    }

    protected String[] getServletMappings() {
        return new String[]{"/"};
    }

    //乱码处理
    @Override
    protected Filter[] getServletFilters() {
        CharacterEncodingFilter filter = new CharacterEncodingFilter();
        filter.setEncoding("UTF-8");
        return new Filter[]{filter};
    }
}
```

CharacterEncodingFilter是在spring-web包中，所以用之前需要导入对应的jar包。

### 4.3 五种类型参数传递

前面我们已经能够使用GET或POST来发送请求和数据，所携带的数据都是比较简单的数据，接下来在这个基础上，我们来研究一些比较复杂的参数传递，常见的参数种类有:

* 普通参数
* POJO类型参数
* 嵌套POJO类型参数
* 数组类型参数
* 集合类型参数

这些参数如何发送，后台改如何接收?我们一个个来学习。

#### 4.3.1 普通参数

* 普通参数:url地址传参，地址参数名与形参变量名相同，定义形参即可接收参数。

![1630481585729](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day01/assets/1630481585729.png)

如果形参与地址参数名不一致该如何解决?

发送请求与参数:

```
http://localhost/commonParamDifferentName?name=张三&age=18
```

后台接收参数:

```java
@RequestMapping("/commonParamDifferentName")
@ResponseBody
public String commonParamDifferentName(String userName , int age){
    System.out.println("普通参数传递 userName ==> "+userName);
    System.out.println("普通参数传递 age ==> "+age);
    return "{'module':'common param different name'}";
}
```

因为前端给的是`name`,后台接收使用的是`userName`,两个名称对不上，导致接收数据失败:

![1630481772035](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day01/assets/1630481772035.png)

解决方案:使用@RequestParam注解

```java
@RequestMapping("/commonParamDifferentName")
    @ResponseBody
    public String commonParamDifferentName(@RequestPaam("name") String userName , int age){
        System.out.println("普通参数传递 userName ==> "+userName);
        System.out.println("普通参数传递 age ==> "+age);
        return "{'module':'common param different name'}";
    }
```

**注意:写上@RequestParam注解框架就不需要自己去解析注入，能提升框架处理性能**

#### 4.3.2 POJO数据类型

简单数据类型一般处理的是参数个数比较少的请求，如果参数比较多，那么后台接收参数的时候就比较复杂，这个时候我们可以考虑使用POJO数据类型。

* POJO参数：请求参数名与形参对象属性名相同，定义POJO类型形参即可接收参数

此时需要使用前面准备好的POJO类，先来看下User

```java
public class User {
    private String name;
    private int age;
    //setter...getter...略
}
```

发送请求和参数:

![1630482186745](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day01/assets/1630482186745.png)

后台接收参数:

```java
//POJO参数：请求参数与形参对象中的属性对应即可完成参数传递
@RequestMapping("/pojoParam")
@ResponseBody
public String pojoParam(User user){
    System.out.println("pojo参数传递 user ==> "+user);
    return "{'module':'pojo param'}";
}
```

**注意:**

* POJO参数接收，前端GET和POST发送请求数据的方式不变。
* ==请求参数key的名称要和POJO中属性的名称一致，否则无法封装。==

#### 4.3.3 嵌套POJO类型参数

如果POJO对象中嵌套了其他的POJO类，如

```java
public class Address {
    private String province;
    private String city;
    //setter...getter...略
}
public class User {
    private String name;
    private int age;
    private Address address;
    //setter...getter...略
}
```

* 嵌套POJO参数：请求参数名与形参对象属性名相同，按照对象层次结构关系即可接收嵌套POJO属性参数

发送请求和参数:

![1630482363291](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day01/assets/1630482363291.png)

后台接收参数:

```java
//POJO参数：请求参数与形参对象中的属性对应即可完成参数传递
@RequestMapping("/pojoParam")
@ResponseBody
public String pojoParam(User user){
    System.out.println("pojo参数传递 user ==> "+user);
    return "{'module':'pojo param'}";
}
```

**注意:**

==请求参数key的名称要和POJO中属性的名称一致，否则无法封装==

#### 4.3.4 数组类型参数

举个简单的例子，如果前端需要获取用户的爱好，爱好绝大多数情况下都是多个，如何发送请求数据和接收数据呢?

* 数组参数：请求参数名与形参对象属性名相同且请求参数为多个，定义数组类型即可接收参数

发送请求和参数:

![1630482999626](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day01/assets/1630482999626.png)

后台接收参数:

```java
  //数组参数：同名请求参数可以直接映射到对应名称的形参数组对象中
    @RequestMapping("/arrayParam")
    @ResponseBody
    public String arrayParam(String[] likes){
        System.out.println("数组参数传递 likes ==> "+ Arrays.toString(likes));
        return "{'module':'array param'}";
    }
```

#### 4.3.5 集合类型参数

数组能接收多个值，那么集合是否也可以实现这个功能呢?

发送请求和参数:

![1630484283773](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day01/assets/1630484283773.png)

后台接收参数:

```java
//集合参数：同名请求参数可以使用@RequestParam注解映射到对应名称的集合对象中作为数据
@RequestMapping("/listParam")
@ResponseBody
public String listParam(List<String> likes){
    System.out.println("集合参数传递 likes ==> "+ likes);
    return "{'module':'list param'}";
}
```

运行会报错，

![1630484339065](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day01/assets/1630484339065.png)

错误的原因是:SpringMVC将List看做是一个POJO对象来处理，将其创建一个对象并准备把前端的数据封装到对象中，但是List是一个接口无法创建对象，所以报错。

解决方案是:使用`@RequestParam`注解

```java
//集合参数：同名请求参数可以使用@RequestParam注解映射到对应名称的集合对象中作为数据
@RequestMapping("/listParam")
@ResponseBody
public String listParam(@RequestParam List<String> likes){
    System.out.println("集合参数传递 likes ==> "+ likes);
    return "{'module':'list param'}";
}
```

* 集合保存普通参数：请求参数名与形参集合对象名相同且请求参数为多个，@RequestParam绑定参数关系
* 对于简单数据类型使用数组会比集合更简单些。

### 知识点1：@RequestParam

| 名称     | @RequestParam                                          |
| -------- | ------------------------------------------------------ |
| 类型     | 形参注解                                               |
| 位置     | SpringMVC控制器方法形参定义前面                        |
| 作用     | 绑定请求参数与处理器方法形参间的关系                   |
| 相关参数 | required：是否为必传参数 <br/>defaultValue：参数默认值 |

### 4.4 JSON数据传输参数

前面我们说过，现在比较流行的开发方式为异步调用。前后台以异步方式进行交换，传输的数据使用的是==JSON==,所以前端如果发送的是JSON数据，后端该如何接收?

对于JSON数据类型，我们常见的有三种:

- json普通数组（["value1","value2","value3",...]）
- json对象（{key1:value1,key2:value2,...}）
- json对象数组（[{key1:value1,...},{key2:value2,...}]）

对于上述数据，前端如何发送，后端如何接收?

#### JSON普通数组

###### 步骤1:pom.xml添加依赖

SpringMVC默认使用的是jackson来处理json的转换，所以需要在pom.xml添加jackson依赖

```xml
<dependency>
    <groupId>com.fasterxml.jackson.core</groupId>
    <artifactId>jackson-databind</artifactId>
    <version>2.9.0</version>
</dependency>
```

###### 步骤2:PostMan发送JSON数据

![1630485135061](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day01/assets/1630485135061.png)

###### 步骤3:开启SpringMVC注解支持

在SpringMVC的配置类中开启SpringMVC的注解支持，这里面就包含了将JSON转换成对象的功能。

```java
@Configuration
@ComponentScan("com.itheima.controller")
//开启json数据类型自动转换
@EnableWebMvc
public class SpringMvcConfig {
}
```

###### 步骤4:参数前添加@RequestBody

```java
//使用@RequestBody注解将外部传递的json数组数据映射到形参的集合对象中作为数据
@RequestMapping("/listParamForJson")
@ResponseBody
public String listParamForJson(@RequestBody List<String> likes){
    System.out.println("list common(json)参数传递 list ==> "+likes);
    return "{'module':'list common for json param'}";
}
```

###### 步骤5:启动运行程序

![1630492624684](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day01/assets/1630492624684.png)

JSON普通数组的数据就已经传递完成，下面针对JSON对象数据和JSON对象数组的数据该如何传递呢?

#### JSON对象数据

我们会发现，只需要关注请求和数据如何发送?后端数据如何接收?

请求和数据的发送:

```json
{
	"name":"itcast",
	"age":15
}
```

![1630493105450](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day01/assets/1630493105450.png)

后端接收数据：

```java
@RequestMapping("/pojoParamForJson")
@ResponseBody
public String pojoParamForJson(@RequestBody User user){
    System.out.println("pojo(json)参数传递 user ==> "+user);
    return "{'module':'pojo for json param'}";
}
```

启动程序访问测试

![1630493233550](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day01/assets/1630493233550.png)

**说明:**

address为null的原因是前端没有传递数据给后端。

如果想要address也有数据，我们需求修改前端传递的数据内容:

```json
{
	"name":"itcast",
	"age":15,
    "address":{
        "province":"beijing",
        "city":"beijing"
    }
}
```

再次发送请求，就能看到address中的数据

![1630493450694](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day01/assets/1630493450694.png)

#### JSON对象数组

集合中保存多个POJO该如何实现?

请求和数据的发送:

```json
[
    {"name":"itcast","age":15},
    {"name":"itheima","age":12}
]
```

 ![1630493501205](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day01/assets/1630493501205.png)

后端接收数据:

```java
@RequestMapping("/listPojoParamForJson")
@ResponseBody
public String listPojoParamForJson(@RequestBody List<User> list){
    System.out.println("list pojo(json)参数传递 list ==> "+list);
    return "{'module':'list pojo for json param'}";
}
```

启动程序访问测试

![1630493561137](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day01/assets/1630493561137.png)

**小结**

SpringMVC接收JSON数据的实现步骤为:

(1)导入jackson包

(2)使用PostMan发送JSON数据

(3)开启SpringMVC注解驱动，在配置类上添加@EnableWebMvc注解

(4)Controller方法的参数前添加@RequestBody注解

#### 知识点1：@EnableWebMvc

| 名称 | @EnableWebMvc             |
| ---- | ------------------------- |
| 类型 | ==配置类注解==            |
| 位置 | SpringMVC配置类定义上方   |
| 作用 | 开启SpringMVC多项辅助功能 |

#### 知识点2：@RequestBody

| 名称 | @RequestBody                                                 |
| ---- | ------------------------------------------------------------ |
| 类型 | ==形参注解==                                                 |
| 位置 | SpringMVC控制器方法形参定义前面                              |
| 作用 | 将请求中请求体所包含的数据传递给请求参数，此注解一个处理器方法只能使用一次 |

#### @RequestBody与@RequestParam区别

* 区别
  * @RequestParam用于接收url地址传参，表单传参【application/x-www-form-urlencoded】
  * @RequestBody用于接收json数据【application/json】

* 应用
  * 后期开发中，发送json格式数据为主，@RequestBody应用较广
  * 如果发送非json格式数据，选用@RequestParam接收请求参数

### 4.5 日期类型参数传递

前面我们处理过简单数据类型、POJO数据类型、数组和集合数据类型以及JSON数据类型，接下来我们还得处理一种开发中比较常见的一种数据类型，`日期类型`

日期类型比较特殊，因为对于日期的格式有N多中输入方式，比如:

* 2088-08-18
* 2088/08/18
* 08/18/2088
* ......

针对这么多日期格式，SpringMVC该如何接收，它能很好的处理日期类型数据么?

#### 步骤1:编写方法接收日期数据

在UserController类中添加方法，把参数设置为日期类型

```java
@RequestMapping("/dataParam")
@ResponseBody
public String dataParam(Date date)
    System.out.println("参数传递 date ==> "+date);
    return "{'module':'data param'}";
}
```

#### 步骤2:启动Tomcat服务器

查看控制台是否报错，如果有错误，先解决错误。

#### 步骤3:使用PostMan发送请求

使用PostMan发送GET请求，并设置date参数

`http://localhost/dataParam?date=2088/08/08`

![1630494320917](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day01/assets/1630494320917.png)

#### 步骤4:查看控制台

![1630494443738](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day01/assets/1630494443738.png)

通过打印，我们发现SpringMVC可以接收日期数据类型，并将其打印在控制台。

这个时候，我们就想如果把日期参数的格式改成其他的，SpringMVC还能处理么?

#### 步骤5:更换日期格式

为了能更好的看到程序运行的结果，我们在方法中多添加一个日期参数

```java
@RequestMapping("/dataParam")
@ResponseBody
public String dataParam(Date date,Date date1)
    System.out.println("参数传递 date ==> "+date);
    return "{'module':'data param'}";
}
```

使用PostMan发送请求，携带两个不同的日期格式，

`http://localhost/dataParam?date=2088/08/08&date1=2088-08-08`

![1630494565970](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day01/assets/1630494565970.png)

发送请求和数据后，页面会报400，控制台会报出一个错误

Resolved [org.springframework.web.method.annotation.==MethodArgumentTypeMismatchException==: Failed to convert value of type 'java.lang.String' to required type 'java.util.Date'; nested exception is org.springframework.core.convert.==ConversionFailedException==: Failed to convert from type [java.lang.String] to type [java.util.Date] for value '2088-08-08'; nested exception is java.lang.IllegalArgumentException]

从错误信息可以看出，错误的原因是在将`2088-08-08`转换成日期类型的时候失败了，原因是SpringMVC默认支持的字符串转日期的格式为`yyyy/MM/dd`,而我们现在传递的不符合其默认格式，SpringMVC就无法进行格式转换，所以报错。

解决方案也比较简单，需要使用`@DateTimeFormat`

```java
@RequestMapping("/dataParam")
@ResponseBody
public String dataParam(Date date,
                        @DateTimeFormat(pattern="yyyy-MM-dd") Date date1)
    System.out.println("参数传递 date ==> "+date);
	System.out.println("参数传递 date1(yyyy-MM-dd) ==> "+date1);
    return "{'module':'data param'}";
}
```

重新启动服务器，重新发送请求测试，SpringMVC就可以正确的进行日期转换了

![1630495221038](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day01/assets/1630495221038.png)

#### 步骤6:携带时间的日期

接下来我们再来发送一个携带时间的日期，看下SpringMVC该如何处理?

先修改UserController类，添加第三个参数

```java
@RequestMapping("/dataParam")
@ResponseBody
public String dataParam(Date date,
                        @DateTimeFormat(pattern="yyyy-MM-dd") Date date1,
                        @DateTimeFormat(pattern="yyyy/MM/dd HH:mm:ss") Date date2)
    System.out.println("参数传递 date ==> "+date);
	System.out.println("参数传递 date1(yyyy-MM-dd) ==> "+date1);
	System.out.println("参数传递 date2(yyyy/MM/dd HH:mm:ss) ==> "+date2);
    return "{'module':'data param'}";
}
```

使用PostMan发送请求，携带两个不同的日期格式，

`http://localhost/dataParam?date=2088/08/08&date1=2088-08-08&date2=2088/08/08 8:08:08`

![1630495347289](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day01/assets/1630495347289.png)

重新启动服务器，重新发送请求测试，SpringMVC就可以将日期时间的数据进行转换

![1630495507353](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day01/assets/1630495507353.png)



#### 知识点1：@DateTimeFormat

| 名称     | @DateTimeFormat                 |
| -------- | ------------------------------- |
| 类型     | ==形参注解==                    |
| 位置     | SpringMVC控制器方法形参前面     |
| 作用     | 设定日期时间型数据格式          |
| 相关属性 | pattern：指定日期时间格式字符串 |

#### 内部实现原理

讲解内部原理之前，我们需要先思考个问题:

* 前端传递字符串，后端使用日期Date接收
* 前端传递JSON数据，后端使用对象接收
* 前端传递字符串，后端使用Integer接收
* 后台需要的数据类型有很多中
* 在数据的传递过程中存在很多类型的转换

问:谁来做这个类型转换?

答:SpringMVC

问:SpringMVC是如何实现类型转换的?

答:SpringMVC中提供了很多类型转换接口和实现类

在框架中，有一些类型转换接口，其中有:

* (1) Converter接口

```java
/**
*	S: the source type
*	T: the target type
*/
public interface Converter<S, T> {
    @Nullable
    //该方法就是将从页面上接收的数据(S)转换成我们想要的数据类型(T)返回
    T convert(S source);
}
```

**注意:Converter所属的包为`org.springframework.core.convert.converter`**

Converter接口的实现类

![1630496385398](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day01/assets/1630496385398.png)

框架中有提供很多对应Converter接口的实现类，用来实现不同数据类型之间的转换,如:

请求参数年龄数据（String→Integer）

日期格式转换（String → Date）

* (2) HttpMessageConverter接口

该接口是实现对象与JSON之间的转换工作

**==注意:SpringMVC的配置类把@EnableWebMvc当做标配配置上去，不要省略==**

### 4.6 响应

SpringMVC接收到请求和数据后，进行一些了的处理，当然这个处理可以是转发给Service，Service层再调用Dao层完成的，不管怎样，处理完以后，都需要将结果告知给用户。

比如:根据用户ID查询用户信息、查询用户列表、新增用户等。

对于响应，主要就包含两部分内容：

* 响应页面
* 响应数据
  * 文本数据
  * json数据

因为异步调用是目前常用的主流方式，所以我们需要更关注的就是如何返回JSON数据，对于其他只需要认识了解即可。

#### 4.6.1 环境准备

- 创建一个Web的Maven项目

- pom.xml添加Spring依赖

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  
  <project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
  
    <groupId>com.itheima</groupId>
    <artifactId>springmvc_05_response</artifactId>
    <version>1.0-SNAPSHOT</version>
    <packaging>war</packaging>
  
    <dependencies>
      <dependency>
        <groupId>javax.servlet</groupId>
        <artifactId>javax.servlet-api</artifactId>
        <version>3.1.0</version>
        <scope>provided</scope>
      </dependency>
      <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-webmvc</artifactId>
        <version>5.2.10.RELEASE</version>
      </dependency>
      <dependency>
        <groupId>com.fasterxml.jackson.core</groupId>
        <artifactId>jackson-databind</artifactId>
        <version>2.9.0</version>
      </dependency>
    </dependencies>
  
    <build>
      <plugins>
        <plugin>
          <groupId>org.apache.tomcat.maven</groupId>
          <artifactId>tomcat7-maven-plugin</artifactId>
          <version>2.1</version>
          <configuration>
            <port>80</port>
            <path>/</path>
          </configuration>
        </plugin>
      </plugins>
    </build>
  </project>
  
  ```

- 创建对应的配置类

  ```java
  public class ServletContainersInitConfig extends AbstractAnnotationConfigDispatcherServletInitializer {
      protected Class<?>[] getRootConfigClasses() {
          return new Class[0];
      }
  
      protected Class<?>[] getServletConfigClasses() {
          return new Class[]{SpringMvcConfig.class};
      }
  
      protected String[] getServletMappings() {
          return new String[]{"/"};
      }
  
      //乱码处理
      @Override
      protected Filter[] getServletFilters() {
          CharacterEncodingFilter filter = new CharacterEncodingFilter();
          filter.setEncoding("UTF-8");
          return new Filter[]{filter};
      }
  }
  
  @Configuration
  @ComponentScan("com.itheima.controller")
  //开启json数据类型自动转换
  @EnableWebMvc
  public class SpringMvcConfig {
  }
  
  
  ```

- 编写模型类User

  ```java
  public class User {
      private String name;
      private int age;
      //getter...setter...toString省略
  }
  ```

- webapp下创建page.jsp

  ```jsp
  <html>
  <body>
  <h2>Hello Spring MVC!</h2>
  </body>
  </html>
  ```

- 编写UserController

  ```java
  @Controller
  public class UserController {
  
      
  }
  ```

最终创建好的项目结构如下:

![1630497314131](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day01/assets/1630497314131.png)

#### 4.6.2 响应页面[了解]

##### 步骤1:设置返回页面

```java
@Controller
public class UserController {
    
    @RequestMapping("/toJumpPage")
    //注意
    //1.此处不能添加@ResponseBody,如果加了该注入，会直接将page.jsp当字符串返回前端
    //2.方法需要返回String
    public String toJumpPage(){
        System.out.println("跳转页面");
        return "page.jsp";
    }
    
}
```

##### 步骤2:启动程序测试

此处涉及到页面跳转，所以不适合采用PostMan进行测试，直接打开浏览器，输入

`http://localhost/toJumpPage`

![1630497496785](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day01/assets/1630497496785.png)

#### 4.6.3 返回文本数据[了解]

##### 步骤1:设置返回文本内容

```java
@Controller
public class UserController {
    
   	@RequestMapping("/toText")
	//注意此处该注解就不能省略，如果省略了,会把response text当前页面名称去查找，如果没有回报404错误
    @ResponseBody
    public String toText(){
        System.out.println("返回纯文本数据");
        return "response text";
    }
    
}
```

##### 步骤2:启动程序测试

此处不涉及到页面跳转，因为我们现在发送的是GET请求，可以使用浏览器也可以使用PostMan进行测试，输入地址`http://localhost/toText`访问

![1630497741388](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day01/assets/1630497741388.png)

#### 4.6.4 响应JSON数据

##### 响应POJO对象

```java
@Controller
public class UserController {
    
    @RequestMapping("/toJsonPOJO")
    @ResponseBody
    public User toJsonPOJO(){
        System.out.println("返回json对象数据");
        User user = new User();
        user.setName("itcast");
        user.setAge(15);
        return user;
    }
    
}
```

返回值为实体类对象，设置返回值为实体类类型，即可实现返回对应对象的json数据，需要依赖==@ResponseBody==注解和==@EnableWebMvc==注解

重新启动服务器，访问`http://localhost/toJsonPOJO`

![1630497954896](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day01/assets/1630497954896.png)

##### 响应POJO集合对象

```java
@Controller
public class UserController {
    
    @RequestMapping("/toJsonList")
    @ResponseBody
    public List<User> toJsonList(){
        System.out.println("返回json集合数据");
        User user1 = new User();
        user1.setName("传智播客");
        user1.setAge(15);

        User user2 = new User();
        user2.setName("黑马程序员");
        user2.setAge(12);

        List<User> userList = new ArrayList<User>();
        userList.add(user1);
        userList.add(user2);

        return userList;
    }
    
}

```

重新启动服务器，访问`http://localhost/toJsonList`

![1630498084047](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day01/assets/1630498084047.png)

#### 知识点1：@ResponseBody

| 名称     | @ResponseBody                                                |
| -------- | ------------------------------------------------------------ |
| 类型     | ==方法\类注解==                                              |
| 位置     | SpringMVC控制器方法定义上方和控制类上                        |
| 作用     | 设置当前控制器返回值作为响应体,<br/>写在类上，该类的所有方法都有该注解功能 |
| 相关属性 | pattern：指定日期时间格式字符串                              |

**说明:**

* 该注解可以写在类上或者方法上
* 写在类上就是该类下的所有方法都有@ReponseBody功能
* 当方法上有@ReponseBody注解后
  * 方法的返回值为字符串，会将其作为文本内容直接响应给前端
  * 方法的返回值为对象，会将对象转换成JSON响应给前端

此处又使用到了类型转换，内部还是通过Converter接口的实现类完成的，所以Converter除了前面所说的功能外，它还可以实现:

* 对象转Json数据(POJO -> json)
* 集合转Json数据(Collection -> json)

## 5，Rest风格

对于Rest风格，我们需要学习的内容包括:

* REST简介
* REST入门案例
* REST快速开发
* 案例:基于RESTful页面数据交互

### 5.1 REST简介

* ==REST==（Representational State Transfer），表现形式状态转换,它是一种软件架构==风格==

  当我们想表示一个网络资源的时候，可以使用两种方式:

  * 传统风格资源描述形式
    * `http://localhost/user/getById?id=1` 查询id为1的用户信息
    * `http://localhost/user/saveUser` 保存用户信息
  * REST风格描述形式
    * `http://localhost/user/1` 
    * `http://localhost/user`

传统方式一般是一个请求url对应一种操作，这样做不仅麻烦，也不安全，因为会程序的人读取了你的请求url地址，就大概知道该url实现的是一个什么样的操作。

查看REST风格的描述，你会发现请求地址变的简单了，并且光看请求URL并不是很能猜出来该URL的具体功能

所以REST的优点有:

- 隐藏资源的访问行为，无法通过地址得知对资源是何种操作
- 书写简化

但是我们的问题也随之而来了，一个相同的url地址即可以是新增也可以是修改或者查询，那么到底我们该如何区分该请求到底是什么操作呢?

* 按照REST风格访问资源时使用==行为动作==区分对资源进行了何种操作
  * `http://localhost/users`	查询全部用户信息 GET（查询）
  * `http://localhost/users/1`  查询指定用户信息 GET（查询）
  * `http://localhost/users`    添加用户信息    POST（新增/保存）
  * `http://localhost/users`    修改用户信息    PUT（修改/更新）
  * `http://localhost/users/1`  删除用户信息    DELETE（删除）

请求的方式比较多，但是比较常用的就4种，分别是`GET`,`POST`,`PUT`,`DELETE`。

按照不同的请求方式代表不同的操作类型。

* 发送GET请求是用来做查询
* 发送POST请求是用来做新增
* 发送PUT请求是用来做修改
* 发送DELETE请求是用来做删除

但是==注意==:

* 上述行为是约定方式，约定不是规范，可以打破，所以称REST风格，而不是REST规范
  * REST提供了对应的架构方式，按照这种架构设计项目可以降低开发的复杂性，提高系统的可伸缩性
  * REST中规定GET/POST/PUT/DELETE针对的是查询/新增/修改/删除，但是我们如果非要用GET请求做删除，这点在程序上运行是可以实现的
  * 但是如果绝大多数人都遵循这种风格，你写的代码让别人读起来就有点莫名其妙了。
* 描述模块的名称通常使用复数，也就是加s的格式描述，表示此类资源，而非单个资源，例如:users、books、accounts......

清楚了什么是REST风格后，我们后期会经常提到一个概念叫`RESTful`，那什么又是RESTful呢?

* 根据REST风格对资源进行访问称为==RESTful==。

后期我们在进行开发的过程中，大多是都是遵从REST风格来访问我们的后台服务，所以可以说咱们以后都是基于RESTful来进行开发的。

### 5.2 RESTful入门案例

#### 5.2.1 环境准备

- 创建一个Web的Maven项目

- pom.xml添加Spring依赖

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  
  <project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
  
    <groupId>com.itheima</groupId>
    <artifactId>springmvc_06_rest</artifactId>
    <version>1.0-SNAPSHOT</version>
    <packaging>war</packaging>
  
    <dependencies>
      <dependency>
        <groupId>javax.servlet</groupId>
        <artifactId>javax.servlet-api</artifactId>
        <version>3.1.0</version>
        <scope>provided</scope>
      </dependency>
      <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-webmvc</artifactId>
        <version>5.2.10.RELEASE</version>
      </dependency>
      <dependency>
        <groupId>com.fasterxml.jackson.core</groupId>
        <artifactId>jackson-databind</artifactId>
        <version>2.9.0</version>
      </dependency>
    </dependencies>
  
    <build>
      <plugins>
        <plugin>
          <groupId>org.apache.tomcat.maven</groupId>
          <artifactId>tomcat7-maven-plugin</artifactId>
          <version>2.1</version>
          <configuration>
            <port>80</port>
            <path>/</path>
          </configuration>
        </plugin>
      </plugins>
    </build>
  </project>
  
  ```

- 创建对应的配置类

  ```java
  public class ServletContainersInitConfig extends AbstractAnnotationConfigDispatcherServletInitializer {
      protected Class<?>[] getRootConfigClasses() {
          return new Class[0];
      }
  
      protected Class<?>[] getServletConfigClasses() {
          return new Class[]{SpringMvcConfig.class};
      }
  
      protected String[] getServletMappings() {
          return new String[]{"/"};
      }
  
      //乱码处理
      @Override
      protected Filter[] getServletFilters() {
          CharacterEncodingFilter filter = new CharacterEncodingFilter();
          filter.setEncoding("UTF-8");
          return new Filter[]{filter};
      }
  }
  
  @Configuration
  @ComponentScan("com.itheima.controller")
  //开启json数据类型自动转换
  @EnableWebMvc
  public class SpringMvcConfig {
  }
  
  
  ```

- 编写模型类User和Book

  ```java
  public class User {
      private String name;
      private int age;
      //getter...setter...toString省略
  }
  
  public class Book {
      private String name;
      private double price;
       //getter...setter...toString省略
  }
  ```

- 编写UserController和BookController

  ```java
  @Controller
  public class UserController {
  	@RequestMapping("/save")
      @ResponseBody
      public String save(@RequestBody User user) {
          System.out.println("user save..."+user);
          return "{'module':'user save'}";
      }
  
      @RequestMapping("/delete")
      @ResponseBody
      public String delete(Integer id) {
          System.out.println("user delete..." + id);
          return "{'module':'user delete'}";
      }
  
      @RequestMapping("/update")
      @ResponseBody
      public String update(@RequestBody User user) {
          System.out.println("user update..." + user);
          return "{'module':'user update'}";
      }
  
      @RequestMapping("/getById")
      @ResponseBody
      public String getById(Integer id) {
          System.out.println("user getById..." + id);
          return "{'module':'user getById'}";
      }
  
      @RequestMapping("/findAll")
      @ResponseBody
      public String getAll() {
          System.out.println("user getAll...");
          return "{'module':'user getAll'}";
      }
  }
  
  
  @Controller
  public class BookController {
      
  	@RequestMapping(value = "/books",method = RequestMethod.POST)
      @ResponseBody
      public String save(@RequestBody Book book){
          System.out.println("book save..." + book);
          return "{'module':'book save'}";
      }
  
      @RequestMapping(value = "/books/{id}",method = RequestMethod.DELETE)
      @ResponseBody
      public String delete(@PathVariable Integer id){
          System.out.println("book delete..." + id);
          return "{'module':'book delete'}";
      }
  
      @RequestMapping(value = "/books",method = RequestMethod.PUT)
      @ResponseBody
      public String update(@RequestBody Book book){
          System.out.println("book update..." + book);
          return "{'module':'book update'}";
      }
  
      @RequestMapping(value = "/books/{id}",method = RequestMethod.GET)
      @ResponseBody
      public String getById(@PathVariable Integer id){
          System.out.println("book getById..." + id);
          return "{'module':'book getById'}";
      }
  
      @RequestMapping(value = "/books",method = RequestMethod.GET)
      @ResponseBody
      public String getAll(){
          System.out.println("book getAll...");
          return "{'module':'book getAll'}";
      }
      
  }
  ```

最终创建好的项目结构如下:

![1630503741455](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day01/assets/1630503741455.png)

#### 5.2.2 思路分析

> 需求:将之前的增删改查替换成RESTful的开发方式。
>
> 1.之前不同的请求有不同的路径,现在要将其修改为统一的请求路径
>
> 修改前: 新增: /save ,修改: /update,删除 /delete...
>
> 修改后: 增删改查: /users
>
> 2.根据GET查询、POST新增、PUT修改、DELETE删除对方法的请求方式进行限定
>
> 3.发送请求的过程中如何设置请求参数?

#### 5.2.3 修改RESTful风格

##### 新增

```java
@Controller
public class UserController {
	//设置当前请求方法为POST，表示REST风格中的添加操作
    @RequestMapping(value = "/users",method = RequestMethod.POST)
    @ResponseBody
    public String save() {
        System.out.println("user save...");
        return "{'module':'user save'}";
    }
}
```

* 将请求路径更改为`/users`

  * 访问该方法使用 POST: `http://localhost/users`

* 使用method属性限定该方法的访问方式为`POST`

  * 如果发送的不是POST请求，比如发送GET请求，则会报错

    ![1630505392070](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day01/assets/1630505392070.png)

##### 删除

```java
@Controller
public class UserController {
    //设置当前请求方法为DELETE，表示REST风格中的删除操作
	@RequestMapping(value = "/users",method = RequestMethod.DELETE)
    @ResponseBody
    public String delete(Integer id) {
        System.out.println("user delete..." + id);
        return "{'module':'user delete'}";
    }
}
```

* 将请求路径更改为`/users`
  - 访问该方法使用 DELETE: `http://localhost/users`

访问成功，但是删除方法没有携带所要删除数据的id,所以针对RESTful的开发，如何携带数据参数?

###### 传递路径参数

前端发送请求的时候使用:`http://localhost/users/1`,路径中的`1`就是我们想要传递的参数。

后端获取参数，需要做如下修改:

* 修改@RequestMapping的value属性，将其中修改为`/users/{id}`，目的是和路径匹配
* 在方法的形参前添加@PathVariable注解

```java
@Controller
public class UserController {
    //设置当前请求方法为DELETE，表示REST风格中的删除操作
	@RequestMapping(value = "/users/{id}",method = RequestMethod.DELETE)
    @ResponseBody
    public String delete(@PathVariable Integer id) {
        System.out.println("user delete..." + id);
        return "{'module':'user delete'}";
    }
}
```

**思考如下两个问题:**

(1)如果方法形参的名称和路径`{}`中的值不一致，该怎么办?

![1630506231379](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day01/assets/1630506231379.png)

(2)如果有多个参数需要传递该如何编写?

前端发送请求的时候使用:`http://localhost/users/1/tom`,路径中的`1`和`tom`就是我们想要传递的两个参数。

后端获取参数，需要做如下修改:

```java
@Controller
public class UserController {
    //设置当前请求方法为DELETE，表示REST风格中的删除操作
	@RequestMapping(value = "/users/{id}/{name}",method = RequestMethod.DELETE)
    @ResponseBody
    public String delete(@PathVariable Integer id,@PathVariable String name) {
        System.out.println("user delete..." + id+","+name);
        return "{'module':'user delete'}";
    }
}
```

##### 修改

```java
@Controller
public class UserController {
    //设置当前请求方法为PUT，表示REST风格中的修改操作
    @RequestMapping(value = "/users",method = RequestMethod.PUT)
    @ResponseBody
    public String update(@RequestBody User user) {
        System.out.println("user update..." + user);
        return "{'module':'user update'}";
    }
}
```

- 将请求路径更改为`/users`

  - 访问该方法使用 PUT: `http://localhost/users`

- 访问并携带参数:

  ![1630506507096](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day01/assets/1630506507096.png)

##### 根据ID查询

```java
@Controller
public class UserController {
    //设置当前请求方法为GET，表示REST风格中的查询操作
    @RequestMapping(value = "/users/{id}" ,method = RequestMethod.GET)
    @ResponseBody
    public String getById(@PathVariable Integer id){
        System.out.println("user getById..."+id);
        return "{'module':'user getById'}";
    }
}
```

将请求路径更改为`/users`

- 访问该方法使用 GET: `http://localhost/users/666`

##### 查询所有

```java
@Controller
public class UserController {
    //设置当前请求方法为GET，表示REST风格中的查询操作
    @RequestMapping(value = "/users" ,method = RequestMethod.GET)
    @ResponseBody
    public String getAll() {
        System.out.println("user getAll...");
        return "{'module':'user getAll'}";
    }
}
```

将请求路径更改为`/users`

- 访问该方法使用 GET: `http://localhost/users`

**小结**

RESTful入门案例，我们需要学习的内容如下:

(1)设定Http请求动作(动词)

@RequestMapping(value="",==method== = RequestMethod.==POST|GET|PUT|DELETE==)

(2)设定请求参数(路径变量)

@RequestMapping(value="/users/=={id}==",method = RequestMethod.DELETE)

@ReponseBody

public String delete(==@PathVariable== Integer ==id==){

}

#### 知识点1：@PathVariable

| 名称 | @PathVariable                                                |
| ---- | ------------------------------------------------------------ |
| 类型 | ==形参注解==                                                 |
| 位置 | SpringMVC控制器方法形参定义前面                              |
| 作用 | 绑定路径参数与处理器方法形参间的关系，要求路径参数名与形参名一一对应 |

关于接收参数，我们学过三个注解`@RequestBody`、`@RequestParam`、`@PathVariable`,这三个注解之间的区别和应用分别是什么?

* 区别
  * @RequestParam用于接收url地址传参或表单传参
  * @RequestBody用于接收json数据
  * @PathVariable用于接收路径参数，使用{参数名称}描述路径参数
* 应用
  * 后期开发中，发送请求参数超过1个时，以json格式为主，@RequestBody应用较广
  * 如果发送非json格式数据，选用@RequestParam接收请求参数
  * 采用RESTful进行开发，当参数数量较少时，例如1个，可以采用@PathVariable接收请求路径变量，通常用于传递id值

### 5.3 RESTful快速开发

做完了RESTful的开发，你会发现==好麻烦==，麻烦在哪?

![1630507339724](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day01/assets/1630507339724.png)

问题1：每个方法的@RequestMapping注解中都定义了访问路径/books，重复性太高。

问题2：每个方法的@RequestMapping注解中都要使用method属性定义请求方式，重复性太高。

问题3：每个方法响应json都需要加上@ResponseBody注解，重复性太高。

对于上面所提的这三个问题，具体该如何解决?

```java
@RestController //@Controller + ReponseBody
@RequestMapping("/books")
public class BookController {
    
	//@RequestMapping(method = RequestMethod.POST)
    @PostMapping
    public String save(@RequestBody Book book){
        System.out.println("book save..." + book);
        return "{'module':'book save'}";
    }

    //@RequestMapping(value = "/{id}",method = RequestMethod.DELETE)
    @DeleteMapping("/{id}")
    public String delete(@PathVariable Integer id){
        System.out.println("book delete..." + id);
        return "{'module':'book delete'}";
    }

    //@RequestMapping(method = RequestMethod.PUT)
    @PutMapping
    public String update(@RequestBody Book book){
        System.out.println("book update..." + book);
        return "{'module':'book update'}";
    }

    //@RequestMapping(value = "/{id}",method = RequestMethod.GET)
    @GetMapping("/{id}")
    public String getById(@PathVariable Integer id){
        System.out.println("book getById..." + id);
        return "{'module':'book getById'}";
    }

    //@RequestMapping(method = RequestMethod.GET)
    @GetMapping
    public String getAll(){
        System.out.println("book getAll...");
        return "{'module':'book getAll'}";
    }
    
}
```

对于刚才的问题，我们都有对应的解决方案：

问题1：每个方法的@RequestMapping注解中都定义了访问路径/books，重复性太高。

```
将@RequestMapping提到类上面，用来定义所有方法共同的访问路径。
```

问题2：每个方法的@RequestMapping注解中都要使用method属性定义请求方式，重复性太高。

```
使用@GetMapping  @PostMapping  @PutMapping  @DeleteMapping代替
```

问题3：每个方法响应json都需要加上@ResponseBody注解，重复性太高。

```
1.将ResponseBody提到类上面，让所有的方法都有@ResponseBody的功能
2.使用@RestController注解替换@Controller与@ResponseBody注解，简化书写
```

#### 知识点1：@RestController

| 名称 | @RestController                                              |
| ---- | ------------------------------------------------------------ |
| 类型 | ==类注解==                                                   |
| 位置 | 基于SpringMVC的RESTful开发控制器类定义上方                   |
| 作用 | 设置当前控制器类为RESTful风格，<br/>等同于@Controller与@ResponseBody两个注解组合功能 |

#### 知识点2：@GetMapping @PostMapping @PutMapping @DeleteMapping

| 名称     | @GetMapping @PostMapping @PutMapping @DeleteMapping          |
| -------- | ------------------------------------------------------------ |
| 类型     | ==方法注解==                                                 |
| 位置     | 基于SpringMVC的RESTful开发控制器方法定义上方                 |
| 作用     | 设置当前控制器方法请求访问路径与请求动作，每种对应一个请求动作，<br/>例如@GetMapping对应GET请求 |
| 相关属性 | value（默认）：请求访问路径                                  |

### 5.4 RESTful案例

#### 5.4.1 需求分析

需求一:图片列表查询，从后台返回数据，将数据展示在页面上

![1630508310063](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day01/assets/1630508310063.png)

需求二:新增图片，将新增图书的数据传递到后台，并在控制台打印

![1630508367105](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day01/assets/1630508367105.png)

**说明:**此次案例的重点是在SpringMVC中如何使用RESTful实现前后台交互，所以本案例并没有和数据库进行交互，所有数据使用`假`数据来完成开发。

步骤分析:

> 1.搭建项目导入jar包
>
> 2.编写Controller类，提供两个方法，一个用来做列表查询，一个用来做新增
>
> 3.在方法上使用RESTful进行路径设置
>
> 4.完成请求、参数的接收和结果的响应
>
> 5.使用PostMan进行测试
>
> 6.将前端页面拷贝到项目中
>
> 7.页面发送ajax请求
>
> 8.完成页面数据的展示

#### 5.4.2 环境准备

- 创建一个Web的Maven项目

- pom.xml添加Spring依赖

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  
  <project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
  
    <groupId>com.itheima</groupId>
    <artifactId>springmvc_07_rest_case</artifactId>
    <version>1.0-SNAPSHOT</version>
    <packaging>war</packaging>
  
    <dependencies>
      <dependency>
        <groupId>javax.servlet</groupId>
        <artifactId>javax.servlet-api</artifactId>
        <version>3.1.0</version>
        <scope>provided</scope>
      </dependency>
      <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-webmvc</artifactId>
        <version>5.2.10.RELEASE</version>
      </dependency>
      <dependency>
        <groupId>com.fasterxml.jackson.core</groupId>
        <artifactId>jackson-databind</artifactId>
        <version>2.9.0</version>
      </dependency>
    </dependencies>
  
    <build>
      <plugins>
        <plugin>
          <groupId>org.apache.tomcat.maven</groupId>
          <artifactId>tomcat7-maven-plugin</artifactId>
          <version>2.1</version>
          <configuration>
            <port>80</port>
            <path>/</path>
          </configuration>
        </plugin>
      </plugins>
    </build>
  </project>
  
  ```

- 创建对应的配置类

  ```java
  public class ServletContainersInitConfig extends AbstractAnnotationConfigDispatcherServletInitializer {
      protected Class<?>[] getRootConfigClasses() {
          return new Class[0];
      }
  
      protected Class<?>[] getServletConfigClasses() {
          return new Class[]{SpringMvcConfig.class};
      }
  
      protected String[] getServletMappings() {
          return new String[]{"/"};
      }
  
      //乱码处理
      @Override
      protected Filter[] getServletFilters() {
          CharacterEncodingFilter filter = new CharacterEncodingFilter();
          filter.setEncoding("UTF-8");
          return new Filter[]{filter};
      }
  }
  
  @Configuration
  @ComponentScan("com.itheima.controller")
  //开启json数据类型自动转换
  @EnableWebMvc
  public class SpringMvcConfig {
  }
  
  
  ```

- 编写模型类Book

  ```java
  public class Book {
      private Integer id;
      private String type;
      private String name;
      private String description;
      //setter...getter...toString略
  }
  ```

- 编写BookController

  ```java
  @Controller
  public class BookController {
  
      
  }
  ```

最终创建好的项目结构如下:

![1630508864017](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day01/assets/1630508864017.png)

#### 5.4.2 后台接口开发

##### 步骤1:编写Controller类并使用RESTful进行配置

```java
@RestController
@RequestMapping("/books")
public class BookController {

    @PostMapping
    public String save(@RequestBody Book book){
        System.out.println("book save ==> "+ book);
        return "{'module':'book save success'}";
    }

 	@GetMapping
    public List<Book> getAll(){
        System.out.println("book getAll is running ...");
        List<Book> bookList = new ArrayList<Book>();

        Book book1 = new Book();
        book1.setType("计算机");
        book1.setName("SpringMVC入门教程");
        book1.setDescription("小试牛刀");
        bookList.add(book1);

        Book book2 = new Book();
        book2.setType("计算机");
        book2.setName("SpringMVC实战教程");
        book2.setDescription("一代宗师");
        bookList.add(book2);

        Book book3 = new Book();
        book3.setType("计算机丛书");
        book3.setName("SpringMVC实战教程进阶");
        book3.setDescription("一代宗师呕心创作");
        bookList.add(book3);

        return bookList;
    }

}
```

##### 步骤2：使用PostMan进行测试

测试新增

```json
{
    "type":"计算机丛书",
    "name":"SpringMVC终极开发",
    "description":"这是一本好书"
}
```

![1630509266954](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day01/assets/1630509266954.png)

测试查询

![](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day01/assets/image-20210805140307371.png)

#### 5.4.3 页面访问处理

##### 步骤1:拷贝静态页面

将`资料\功能页面`下的所有内容拷贝到项目的`webapp`目录下

![1630510166433](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day01/assets/1630510166433.png)

##### 步骤2:访问pages目录下的books.html

打开浏览器输入`http://localhost/pages/books.html`

![1630510225182](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day01/assets/1630510225182.png)

(1)出现错误的原因?

![1630510264650](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day01/assets/1630510264650.png)

SpringMVC拦截了静态资源，根据/pages/books.html去controller找对应的方法，找不到所以会报404的错误。

(2)SpringMVC为什么会拦截静态资源呢?

![1630510397429](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day01/assets/1630510397429.png)

(3)解决方案?

* SpringMVC需要将静态资源进行放行。

```java
@Configuration
public class SpringMvcSupport extends WebMvcConfigurationSupport {
    //设置静态资源访问过滤，当前类需要设置为配置类，并被扫描加载
    @Override
    protected void addResourceHandlers(ResourceHandlerRegistry registry) {
        //当访问/pages/????时候，从/pages目录下查找内容
        registry.addResourceHandler("/pages/**").addResourceLocations("/pages/");
        registry.addResourceHandler("/js/**").addResourceLocations("/js/");
        registry.addResourceHandler("/css/**").addResourceLocations("/css/");
        registry.addResourceHandler("/plugins/**").addResourceLocations("/plugins/");
    }
}

```

* 该配置类是在config目录下，SpringMVC扫描的是controller包，所以该配置类还未生效，要想生效需要将SpringMvcConfig配置类进行修改

```java
@Configuration
@ComponentScan({"com.itheima.controller","com.itheima.config"})
@EnableWebMvc
public class SpringMvcConfig {
}

或者

@Configuration
@ComponentScan("com.itheima")
@EnableWebMvc
public class SpringMvcConfig {
}
```

##### 步骤3:修改books.html页面

```html
<!DOCTYPE html>

<html>
    <head>
        <!-- 页面meta -->
        <meta charset="utf-8">
        <title>SpringMVC案例</title>
        <!-- 引入样式 -->
        <link rel="stylesheet" href="../plugins/elementui/index.css">
        <link rel="stylesheet" href="../plugins/font-awesome/css/font-awesome.min.css">
        <link rel="stylesheet" href="../css/style.css">
    </head>

    <body class="hold-transition">

        <div id="app">

            <div class="content-header">
                <h1>图书管理</h1>
            </div>

            <div class="app-container">
                <div class="box">
                    <div class="filter-container">
                        <el-input placeholder="图书名称" style="width: 200px;" class="filter-item"></el-input>
                        <el-button class="dalfBut">查询</el-button>
                        <el-button type="primary" class="butT" @click="openSave()">新建</el-button>
                    </div>

                    <el-table size="small" current-row-key="id" :data="dataList" stripe highlight-current-row>
                        <el-table-column type="index" align="center" label="序号"></el-table-column>
                        <el-table-column prop="type" label="图书类别" align="center"></el-table-column>
                        <el-table-column prop="name" label="图书名称" align="center"></el-table-column>
                        <el-table-column prop="description" label="描述" align="center"></el-table-column>
                        <el-table-column label="操作" align="center">
                            <template slot-scope="scope">
                                <el-button type="primary" size="mini">编辑</el-button>
                                <el-button size="mini" type="danger">删除</el-button>
                            </template>
                        </el-table-column>
                    </el-table>

                    <div class="pagination-container">
                        <el-pagination
                            class="pagiantion"
                            @current-change="handleCurrentChange"
                            :current-page="pagination.currentPage"
                            :page-size="pagination.pageSize"
                            layout="total, prev, pager, next, jumper"
                            :total="pagination.total">
                        </el-pagination>
                    </div>

                    <!-- 新增标签弹层 -->
                    <div class="add-form">
                        <el-dialog title="新增图书" :visible.sync="dialogFormVisible">
                            <el-form ref="dataAddForm" :model="formData" :rules="rules" label-position="right" label-width="100px">
                                <el-row>
                                    <el-col :span="12">
                                        <el-form-item label="图书类别" prop="type">
                                            <el-input v-model="formData.type"/>
                                        </el-form-item>
                                    </el-col>
                                    <el-col :span="12">
                                        <el-form-item label="图书名称" prop="name">
                                            <el-input v-model="formData.name"/>
                                        </el-form-item>
                                    </el-col>
                                </el-row>
                                <el-row>
                                    <el-col :span="24">
                                        <el-form-item label="描述">
                                            <el-input v-model="formData.description" type="textarea"></el-input>
                                        </el-form-item>
                                    </el-col>
                                </el-row>
                            </el-form>
                            <div slot="footer" class="dialog-footer">
                                <el-button @click="dialogFormVisible = false">取消</el-button>
                                <el-button type="primary" @click="saveBook()">确定</el-button>
                            </div>
                        </el-dialog>
                    </div>

                </div>
            </div>
        </div>
    </body>

    <!-- 引入组件库 -->
    <script src="../js/vue.js"></script>
    <script src="../plugins/elementui/index.js"></script>
    <script type="text/javascript" src="../js/jquery.min.js"></script>
    <script src="../js/axios-0.18.0.js"></script>

    <script>
        var vue = new Vue({

            el: '#app',

            data:{
				dataList: [],//当前页要展示的分页列表数据
                formData: {},//表单数据
                dialogFormVisible: false,//增加表单是否可见
                dialogFormVisible4Edit:false,//编辑表单是否可见
                pagination: {},//分页模型数据，暂时弃用
            },

            //钩子函数，VUE对象初始化完成后自动执行
            created() {
                this.getAll();
            },

            methods: {
                // 重置表单
                resetForm() {
                    //清空输入框
                    this.formData = {};
                },

                // 弹出添加窗口
                openSave() {
                    this.dialogFormVisible = true;
                    this.resetForm();
                },

                //添加
                saveBook () {
                    axios.post("/books",this.formData).then((res)=>{

                    });
                },

                //主页列表查询
                getAll() {
                    axios.get("/books").then((res)=>{
                        this.dataList = res.data;
                    });
                },

            }
        })
    </script>
</html>
```



# SpringMVC_day02

**今日内容**

> * 完成SSM的整合开发
> * 能够理解并实现统一结果封装与统一异常处理
> * 能够完成前后台功能整合开发
> * 掌握拦截器的编写



![image-20220506162559333](C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220506162559333.png)



## 1，SSM整合

前面我们已经把`Mybatis`、`Spring`和`SpringMVC`三个框架进行了学习，今天主要的内容就是把这三个框架整合在一起完成我们的业务功能开发，具体如何来整合，我们一步步来学习。

### 1.1 流程分析

(1) 创建工程

* 创建一个Maven的web工程
* pom.xml添加SSM需要的依赖jar包
* 编写Web项目的入口配置类，实现`AbstractAnnotationConfigDispatcherServletInitializer`重写以下方法
  * getRootConfigClasses()	：返回Spring的配置类->需要==SpringConfig==配置类
  * getServletConfigClasses() ：返回SpringMVC的配置类->需要==SpringMvcConfig==配置类
  * getServletMappings()      : 设置SpringMVC请求拦截路径规则
  * getServletFilters()       ：设置过滤器，解决POST请求中文乱码问题

(2)SSM整合[==重点是各个配置的编写==]

* SpringConfig
  * 标识该类为配置类 @Configuration
  * 扫描Service所在的包 @ComponentScan
  * 在Service层要管理事务 @EnableTransactionManagement
  * 读取外部的properties配置文件 @PropertySource
  * 整合Mybatis需要引入Mybatis相关配置类 @Import
    * 第三方数据源配置类 JdbcConfig
      * 构建DataSource数据源，DruidDataSouroce,需要注入数据库连接四要素， @Bean @Value
      * 构建平台事务管理器，DataSourceTransactionManager,@Bean
    * Mybatis配置类 MybatisConfig
      * 构建SqlSessionFactoryBean并设置别名扫描与数据源，@Bean
      * 构建MapperScannerConfigurer并设置DAO层的包扫描
* SpringMvcConfig
  * 标识该类为配置类 @Configuration
  * 扫描Controller所在的包 @ComponentScan
  * 开启SpringMVC注解支持 @EnableWebMvc

(3)功能模块[与具体的业务模块有关]

* 创建数据库表
* 根据数据库表创建对应的模型类
* 通过Dao层完成数据库表的增删改查(接口+自动代理)
* 编写Service层[Service接口+实现类]
  * @Service
  * @Transactional
  * 整合Junit对业务层进行单元测试
    * @RunWith
    * @ContextConfiguration
    * @Test
* 编写Controller层
  * 接收请求 @RequestMapping @GetMapping @PostMapping @PutMapping @DeleteMapping
  * 接收数据 简单、POJO、嵌套POJO、集合、数组、JSON数据类型
    * @RequestParam
    * @PathVariable
    * @RequestBody
  * 转发业务层 
    * @Autowired
  * 响应结果
    * @ResponseBody

### 1.2 整合配置

掌握上述的知识点后，接下来，我们就可以按照上述的步骤一步步的来完成SSM的整合。

#### 步骤1：创建Maven的web项目

可以使用Maven的骨架创建

![1630561266760](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day02/assets/1630561266760.png)

#### 步骤2:添加依赖

pom.xml添加SSM所需要的依赖jar包

```xml
<?xml version="1.0" encoding="UTF-8"?>

<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <groupId>com.itheima</groupId>
  <artifactId>springmvc_08_ssm</artifactId>
  <version>1.0-SNAPSHOT</version>
  <packaging>war</packaging>

  <dependencies>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-webmvc</artifactId>
      <version>5.2.10.RELEASE</version>
    </dependency>

    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-jdbc</artifactId>
      <version>5.2.10.RELEASE</version>
    </dependency>

    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-test</artifactId>
      <version>5.2.10.RELEASE</version>
    </dependency>

    <dependency>
      <groupId>org.mybatis</groupId>
      <artifactId>mybatis</artifactId>
      <version>3.5.6</version>
    </dependency>

    <dependency>
      <groupId>org.mybatis</groupId>
      <artifactId>mybatis-spring</artifactId>
      <version>1.3.0</version>
    </dependency>

    <dependency>
      <groupId>mysql</groupId>
      <artifactId>mysql-connector-java</artifactId>
      <version>5.1.47</version>
    </dependency>

    <dependency>
      <groupId>com.alibaba</groupId>
      <artifactId>druid</artifactId>
      <version>1.1.16</version>
    </dependency>

    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>4.12</version>
      <scope>test</scope>
    </dependency>

    <dependency>
      <groupId>javax.servlet</groupId>
      <artifactId>javax.servlet-api</artifactId>
      <version>3.1.0</version>
      <scope>provided</scope>
    </dependency>

    <dependency>
      <groupId>com.fasterxml.jackson.core</groupId>
      <artifactId>jackson-databind</artifactId>
      <version>2.9.0</version>
    </dependency>
  </dependencies>

  <build>
    <plugins>
      <plugin>
        <groupId>org.apache.tomcat.maven</groupId>
        <artifactId>tomcat7-maven-plugin</artifactId>
        <version>2.1</version>
        <configuration>
          <port>80</port>
          <path>/</path>
        </configuration>
      </plugin>
    </plugins>
  </build>
</project>


```

#### 步骤3:创建项目包结构

![1630561591931](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day02/assets/1630561591931.png)

* config目录存放的是相关的配置类
* controller编写的是Controller类
* dao存放的是Dao接口，因为使用的是Mapper接口代理方式，所以没有实现类包
* service存的是Service接口，impl存放的是Service实现类
* resources:存入的是配置文件，如Jdbc.properties
* webapp:目录可以存放静态资源
* test/java:存放的是测试类

#### 步骤4:创建SpringConfig配置类

```java
@Configuration
@ComponentScan({"com.itheima.service"})
@PropertySource("classpath:jdbc.properties")
@Import({JdbcConfig.class,MyBatisConfig.class})
@EnableTransactionManagement
public class SpringConfig {
}
```

#### 步骤5:创建JdbcConfig配置类

```java
public class JdbcConfig {
    @Value("${jdbc.driver}")
    private String driver;
    @Value("${jdbc.url}")
    private String url;
    @Value("${jdbc.username}")
    private String username;
    @Value("${jdbc.password}")
    private String password;

    @Bean
    public DataSource dataSource(){
        DruidDataSource dataSource = new DruidDataSource();
        dataSource.setDriverClassName(driver);
        dataSource.setUrl(url);
        dataSource.setUsername(username);
        dataSource.setPassword(password);
        return dataSource;
    }

    @Bean
    public PlatformTransactionManager transactionManager(DataSource dataSource){
        DataSourceTransactionManager ds = new DataSourceTransactionManager();
        ds.setDataSource(dataSource);
        return ds;
    }
}
```

#### 步骤6:创建MybatisConfig配置类

```java
public class MyBatisConfig {
    @Bean
    public SqlSessionFactoryBean sqlSessionFactory(DataSource dataSource){
        SqlSessionFactoryBean factoryBean = new SqlSessionFactoryBean();
        factoryBean.setDataSource(dataSource);
        factoryBean.setTypeAliasesPackage("com.itheima.domain");
        return factoryBean;
    }

    @Bean
    public MapperScannerConfigurer mapperScannerConfigurer(){
        MapperScannerConfigurer msc = new MapperScannerConfigurer();
        msc.setBasePackage("com.itheima.dao");
        return msc;
    }
}
```

#### 步骤7:创建jdbc.properties

在resources下提供jdbc.properties,设置数据库连接四要素

```properties
jdbc.driver=com.mysql.jdbc.Driver
jdbc.url=jdbc:mysql://localhost:3306/ssm_db
jdbc.username=root
jdbc.password=root
```

#### 步骤8:创建SpringMVC配置类

```java
@Configuration
@ComponentScan("com.itheima.controller")
@EnableWebMvc
public class SpringMvcConfig {
}
```

#### 步骤9:创建Web项目入口配置类

```java
public class ServletConfig extends AbstractAnnotationConfigDispatcherServletInitializer {
    //加载Spring配置类
    protected Class<?>[] getRootConfigClasses() {
        return new Class[]{SpringConfig.class};
    }
    //加载SpringMVC配置类
    protected Class<?>[] getServletConfigClasses() {
        return new Class[]{SpringMvcConfig.class};
    }
    //设置SpringMVC请求地址拦截规则
    protected String[] getServletMappings() {
        return new String[]{"/"};
    }
    //设置post请求中文乱码过滤器
    @Override
    protected Filter[] getServletFilters() {
        CharacterEncodingFilter filter = new CharacterEncodingFilter();
        filter.setEncoding("utf-8");
        return new Filter[]{filter};
    }
}

```

至此SSM整合的环境就已经搭建好了。在这个环境上，我们如何进行功能模块的开发呢?

### 1.3 功能模块开发

> 需求:对表tbl_book进行新增、修改、删除、根据ID查询和查询所有

#### 步骤1:创建数据库及表

```sql
create database ssm_db character set utf8;
use ssm_db;
create table tbl_book(
  id int primary key auto_increment,
  type varchar(20),
  name varchar(50),
  description varchar(255)
)

insert  into `tbl_book`(`id`,`type`,`name`,`description`) values (1,'计算机理论','Spring实战 第五版','Spring入门经典教程，深入理解Spring原理技术内幕'),(2,'计算机理论','Spring 5核心原理与30个类手写实践','十年沉淀之作，手写Spring精华思想'),(3,'计算机理论','Spring 5设计模式','深入Spring源码刨析Spring源码中蕴含的10大设计模式'),(4,'计算机理论','Spring MVC+Mybatis开发从入门到项目实战','全方位解析面向Web应用的轻量级框架，带你成为Spring MVC开发高手'),(5,'计算机理论','轻量级Java Web企业应用实战','源码级刨析Spring框架，适合已掌握Java基础的读者'),(6,'计算机理论','Java核心技术 卷Ⅰ 基础知识(原书第11版)','Core Java第11版，Jolt大奖获奖作品，针对Java SE9、10、11全面更新'),(7,'计算机理论','深入理解Java虚拟机','5个纬度全面刨析JVM,大厂面试知识点全覆盖'),(8,'计算机理论','Java编程思想(第4版)','Java学习必读经典，殿堂级著作！赢得了全球程序员的广泛赞誉'),(9,'计算机理论','零基础学Java(全彩版)','零基础自学编程的入门图书，由浅入深，详解Java语言的编程思想和核心技术'),(10,'市场营销','直播就这么做:主播高效沟通实战指南','李子柒、李佳奇、薇娅成长为网红的秘密都在书中'),(11,'市场营销','直播销讲实战一本通','和秋叶一起学系列网络营销书籍'),(12,'市场营销','直播带货:淘宝、天猫直播从新手到高手','一本教你如何玩转直播的书，10堂课轻松实现带货月入3W+');
```

#### 步骤2:编写模型类

```java
public class Book {
    private Integer id;
    private String type;
    private String name;
    private String description;
    //getter...setter...toString省略
}
```

#### 步骤3:编写Dao接口

```java
public interface BookDao {

//    @Insert("insert into tbl_book values(null,#{type},#{name},#{description})")
    @Insert("insert into tbl_book (type,name,description) values(#{type},#{name},#{description})")
    public void save(Book book);

    @Update("update tbl_book set type = #{type}, name = #{name}, description = #{description} where id = #{id}")
    public void update(Book book);

    @Delete("delete from tbl_book where id = #{id}")
    public void delete(Integer id);

    @Select("select * from tbl_book where id = #{id}")
    public Book getById(Integer id);

    @Select("select * from tbl_book")
    public List<Book> getAll();
}
```

#### 步骤4:编写Service接口和实现类

```java
@Transactional
public interface BookService {
    /**
     * 保存
     * @param book
     * @return
     */
    public boolean save(Book book);

    /**
     * 修改
     * @param book
     * @return
     */
    public boolean update(Book book);

    /**
     * 按id删除
     * @param id
     * @return
     */
    public boolean delete(Integer id);

    /**
     * 按id查询
     * @param id
     * @return
     */
    public Book getById(Integer id);

    /**
     * 查询全部
     * @return
     */
    public List<Book> getAll();
}
```

```java
@Service
public class BookServiceImpl implements BookService {
    @Autowired
    private BookDao bookDao;

    public boolean save(Book book) {
        bookDao.save(book);
        return true;
    }

    public boolean update(Book book) {
        bookDao.update(book);
        return true;
    }

    public boolean delete(Integer id) {
        bookDao.delete(id);
        return true;
    }

    public Book getById(Integer id) {
        return bookDao.getById(id);
    }

    public List<Book> getAll() {
        return bookDao.getAll();
    }
}
```

**说明:**

* bookDao在Service中注入的会提示一个红线提示，为什么呢?

  * BookDao是一个接口，没有实现类，接口是不能创建对象的，所以最终注入的应该是代理对象
  * 代理对象是由Spring的IOC容器来创建管理的
  * IOC容器又是在Web服务器启动的时候才会创建
  * IDEA在检测依赖关系的时候，没有找到适合的类注入，所以会提示错误提示
  * 但是程序运行的时候，代理对象就会被创建，框架会使用DI进行注入，所以程序运行无影响。

* 如何解决上述问题?

  * 可以不用理会，因为运行是正常的

  * 设置错误提示级别

    ![](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day02/assets/1630600227357.png)



#### 步骤5:编写Contorller类

```java
@RestController
@RequestMapping("/books")
public class BookController {

    @Autowired
    private BookService bookService;

    @PostMapping
    public boolean save(@RequestBody Book book) {
        return bookService.save(book);
    }

    @PutMapping
    public boolean update(@RequestBody Book book) {
        return bookService.update(book);
    }

    @DeleteMapping("/{id}")
    public boolean delete(@PathVariable Integer id) {
        return bookService.delete(id);
    }

    @GetMapping("/{id}")
    public Book getById(@PathVariable Integer id) {
        return bookService.getById(id);
    }

    @GetMapping
    public List<Book> getAll() {
        return bookService.getAll();
    }
}
```

对于图书模块的增删改查就已经完成了编写，我们可以从后往前写也可以从前往后写，最终只需要能把功能实现即可。

接下来我们就先把业务层的代码使用`Spring整合Junit`的知识点进行单元测试:

### 1.4 单元测试

#### 步骤1:新建测试类

```java
@RunWith(SpringJUnit4ClassRunner.class)
@ContextConfiguration(classes = SpringConfig.class)
public class BookServiceTest {

}
```

#### 步骤2:注入Service类

```java
@RunWith(SpringJUnit4ClassRunner.class)
@ContextConfiguration(classes = SpringConfig.class)
public class BookServiceTest {

    @Autowired
    private BookService bookService;


}
```

#### 步骤3:编写测试方法

我们先来对查询进行单元测试。

```java
@RunWith(SpringJUnit4ClassRunner.class)
@ContextConfiguration(classes = SpringConfig.class)
public class BookServiceTest {

    @Autowired
    private BookService bookService;

    @Test
    public void testGetById(){
        Book book = bookService.getById(1);
        System.out.println(book);
    }

    @Test
    public void testGetAll(){
        List<Book> all = bookService.getAll();
        System.out.println(all);
    }

}
```

根据ID查询，测试的结果为:

![1630600844191](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day02/assets/1630600844191.png)

查询所有，测试的结果为:

![1630600927486](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day02/assets/1630600927486.png)

### 1.5 PostMan测试

#### 新增

`http://localhost/books`

```json
{
	"type":"类别测试数据",
    "name":"书名测试数据",
    "description":"描述测试数据"
}
```

![1630652582425](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day02/assets/1630652582425.png)

#### 修改

`http://localhost/books`

```json
{
    "id":13,
	"type":"类别测试数据",
    "name":"书名测试数据",
    "description":"描述测试数据"
}
```

![1630652758221](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day02/assets/1630652758221.png)

#### 删除

`http://localhost/books/14`

![1630652796605](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day02/assets/1630652796605.png)

#### 查询单个

`http://localhost/books/1`

![1630652837682](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day02/assets/1630652837682.png)

#### 查询所有

`http://localhost/books`

![1630652867493](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day02/assets/1630652867493.png)

## 2，统一结果封装

### 2.1 表现层与前端数据传输协议定义

SSM整合以及功能模块开发完成后，接下来，我们在上述案例的基础上分析下有哪些问题需要我们去解决下。首先第一个问题是:

* 在Controller层增删改返回给前端的是boolean类型数据

  ![1630653359533](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day02/assets/1630653359533.png)

* 在Controller层查询单个返回给前端的是对象

  ![1630653385377](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day02/assets/1630653385377.png)

* 在Controller层查询所有返回给前端的是集合对象

  ![1630653468887](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day02/assets/1630653468887.png)

目前我们就已经有三种数据类型返回给前端，如果随着业务的增长，我们需要返回的数据类型会越来越多。对于前端开发人员在解析数据的时候就比较凌乱了，所以对于前端来说，如果后台能够返回一个统一的数据结果，前端在解析的时候就可以按照一种方式进行解析。开发就会变得更加简单。

所以我们就想能不能将返回结果的数据进行统一，具体如何来做，大体的思路为:

* 为了封装返回的结果数据:==创建结果模型类，封装数据到data属性中==
* 为了封装返回的数据是何种操作及是否操作成功:==封装操作结果到code属性中==
* 操作失败后为了封装返回的错误信息:==封装特殊消息到message(msg)属性中==

![1630654293972](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day02/assets/1630654293972.png)

根据分析，我们可以设置统一数据返回结果类

```java
public class Result{
	private Object data;
	private Integer code;
	private String msg;
}
```

**注意:**Result类名及类中的字段并不是固定的，可以根据需要自行增减提供若干个构造方法，方便操作。

### 2.2 表现层与前端数据传输协议实现

前面我们已经分析了如何封装返回结果数据，具体在项目中该如何实现，我们通过个例子来操作一把

#### 2.2.1 环境准备

- 创建一个Web的Maven项目
- pom.xml添加SSM整合所需jar包
- 创建对应的配置类
- 编写Controller、Service接口、Service实现类、Dao接口和模型类
- resources下提供jdbc.properties配置文件

因为这个项目环境的内容和SSM整合的内容是一致的，所以我们就不在把代码粘出来了，大家在练习的时候可以在前面整合的例子案例环境下，进行本节内容的开发。

最终创建好的项目结构如下:

![1630654870632](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day02/assets/1630654870632.png)

#### 2.2.2 结果封装

对于结果封装，我们应该是在表现层进行处理，所以我们把结果类放在controller包下，当然你也可以放在domain包，这个都是可以的，具体如何实现结果封装，具体的步骤为:

##### 步骤1:创建Result类

```java
public class Result {
    //描述统一格式中的数据
    private Object data;
    //描述统一格式中的编码，用于区分操作，可以简化配置0或1表示成功失败
    private Integer code;
    //描述统一格式中的消息，可选属性
    private String msg;

    public Result() {
    }
	//构造方法是方便对象的创建
    public Result(Integer code,Object data) {
        this.data = data;
        this.code = code;
    }
	//构造方法是方便对象的创建
    public Result(Integer code, Object data, String msg) {
        this.data = data;
        this.code = code;
        this.msg = msg;
    }
	//setter...getter...省略
}
```

##### 步骤2:定义返回码Code类

```java
//状态码
public class Code {
    public static final Integer SAVE_OK = 20011;
    public static final Integer DELETE_OK = 20021;
    public static final Integer UPDATE_OK = 20031;
    public static final Integer GET_OK = 20041;

    public static final Integer SAVE_ERR = 20010;
    public static final Integer DELETE_ERR = 20020;
    public static final Integer UPDATE_ERR = 20030;
    public static final Integer GET_ERR = 20040;
}

```

**注意:**code类中的常量设计也不是固定的，可以根据需要自行增减，例如将查询再进行细分为GET_OK,GET_ALL_OK,GET_PAGE_OK等。

##### 步骤3:修改Controller类的返回值

```java
//统一每一个控制器方法返回值
@RestController
@RequestMapping("/books")
public class BookController {

    @Autowired
    private BookService bookService;

    @PostMapping
    public Result save(@RequestBody Book book) {
        boolean flag = bookService.save(book);
        return new Result(flag ? Code.SAVE_OK:Code.SAVE_ERR,flag);
    }

    @PutMapping
    public Result update(@RequestBody Book book) {
        boolean flag = bookService.update(book);
        return new Result(flag ? Code.UPDATE_OK:Code.UPDATE_ERR,flag);
    }

    @DeleteMapping("/{id}")
    public Result delete(@PathVariable Integer id) {
        boolean flag = bookService.delete(id);
        return new Result(flag ? Code.DELETE_OK:Code.DELETE_ERR,flag);
    }

    @GetMapping("/{id}")
    public Result getById(@PathVariable Integer id) {
        Book book = bookService.getById(id);
        Integer code = book != null ? Code.GET_OK : Code.GET_ERR;
        String msg = book != null ? "" : "数据查询失败，请重试！";
        return new Result(code,book,msg);
    }

    @GetMapping
    public Result getAll() {
        List<Book> bookList = bookService.getAll();
        Integer code = bookList != null ? Code.GET_OK : Code.GET_ERR;
        String msg = bookList != null ? "" : "数据查询失败，请重试！";
        return new Result(code,bookList,msg);
    }
}
```

##### 步骤4:启动服务测试

![1630656326477](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day02/assets/1630656326477.png)

至此，我们的返回结果就已经能以一种统一的格式返回给前端。前端根据返回的结果，先从中获取`code`,根据code判断，如果成功则取`data`属性的值，如果失败，则取`msg`中的值做提示。

## 3，统一异常处理

### 3.1 问题描述

在讲解这一部分知识点之前，我们先来演示个效果，修改BookController类的`getById`方法

```java
@GetMapping("/{id}")
public Result getById(@PathVariable Integer id) {
    //手动添加一个错误信息
    if(id==1){
        int i = 1/0;
    }
    Book book = bookService.getById(id);
    Integer code = book != null ? Code.GET_OK : Code.GET_ERR;
    String msg = book != null ? "" : "数据查询失败，请重试！";
    return new Result(code,book,msg);
}
```

重新启动运行项目，使用PostMan发送请求，当传入的id为1，则会出现如下效果：

![1630656982337](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day02/assets/1630656982337.png)

前端接收到这个信息后和之前我们约定的格式不一致，这个问题该如何解决?

在解决问题之前，我们先来看下异常的种类及出现异常的原因:

- 框架内部抛出的异常：因使用不合规导致
- 数据层抛出的异常：因外部服务器故障导致（例如：服务器访问超时）
- 业务层抛出的异常：因业务逻辑书写错误导致（例如：遍历业务书写操作，导致索引异常等）
- 表现层抛出的异常：因数据收集、校验等规则导致（例如：不匹配的数据类型间导致异常）
- 工具类抛出的异常：因工具类书写不严谨不够健壮导致（例如：必要释放的连接长期未释放等）

看完上面这些出现异常的位置，你会发现，在我们开发的任何一个位置都有可能出现异常，而且这些异常是不能避免的。所以我们就得将异常进行处理。

**思考**

1. 各个层级均出现异常，异常处理代码书写在哪一层?

   ==所有的异常均抛出到表现层进行处理==

2. 异常的种类很多，表现层如何将所有的异常都处理到呢?

   ==异常分类==

3. 表现层处理异常，每个方法中单独书写，代码书写量巨大且意义不强，如何解决?

   ==AOP==

对于上面这些问题及解决方案，SpringMVC已经为我们提供了一套解决方案:

* 异常处理器:

  * 集中的、统一的处理项目中出现的异常。

    ![1630657791653](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day02/assets/1630657791653.png)

### 3.2 异常处理器的使用

#### 3.2.1 环境准备

- 创建一个Web的Maven项目
- pom.xml添加SSM整合所需jar包
- 创建对应的配置类
- 编写Controller、Service接口、Service实现类、Dao接口和模型类
- resources下提供jdbc.properties配置文件

内容参考前面的项目或者直接使用前面的项目进行本节内容的学习。

最终创建好的项目结构如下:

![1630657972564](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day02/assets/1630657972564.png)

#### 3.2.2 使用步骤

##### 步骤1:创建异常处理器类

```java
//@RestControllerAdvice用于标识当前类为REST风格对应的异常处理器
@RestControllerAdvice
public class ProjectExceptionAdvice {
    //除了自定义的异常处理器，保留对Exception类型的异常处理，用于处理非预期的异常
    @ExceptionHandler(Exception.class)
    public void doException(Exception ex){
      	System.out.println("嘿嘿,异常你哪里跑！")
    }
}

```

==确保SpringMvcConfig能够扫描到异常处理器类==

##### 步骤2:让程序抛出异常

修改`BookController`的getById方法，添加`int i = 1/0`.

```java
@GetMapping("/{id}")
public Result getById(@PathVariable Integer id) {
  	int i = 1/0;
    Book book = bookService.getById(id);
    Integer code = book != null ? Code.GET_OK : Code.GET_ERR;
    String msg = book != null ? "" : "数据查询失败，请重试！";
    return new Result(code,book,msg);
}
```

##### 步骤3:运行程序，测试

![1630658350945](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day02/assets/1630658350945.png)

说明异常已经被拦截并执行了`doException`方法。

##### 异常处理器类返回结果给前端

```java
//@RestControllerAdvice用于标识当前类为REST风格对应的异常处理器
@RestControllerAdvice
public class ProjectExceptionAdvice {
    //除了自定义的异常处理器，保留对Exception类型的异常处理，用于处理非预期的异常
    @ExceptionHandler(Exception.class)
    public Result doException(Exception ex){
      	System.out.println("嘿嘿,异常你哪里跑！")
        return new Result(666,null,"嘿嘿,异常你哪里跑！");
    }
}

```

启动运行程序，测试

![1630658606549](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day02/assets/1630658606549.png)

至此，就算后台执行的过程中抛出异常，最终也能按照我们和前端约定好的格式返回给前端。

#### 知识点1：@RestControllerAdvice

| 名称 | @RestControllerAdvice              |
| ---- | ---------------------------------- |
| 类型 | ==类注解==                         |
| 位置 | Rest风格开发的控制器增强类定义上方 |
| 作用 | 为Rest风格开发的控制器类做增强     |

**说明:**此注解自带@ResponseBody注解与@Component注解，具备对应的功能

![1630659060451](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day02/assets/1630659060451.png)

#### 知识点2：@ExceptionHandler

| 名称 | @ExceptionHandler                                            |
| ---- | ------------------------------------------------------------ |
| 类型 | ==方法注解==                                                 |
| 位置 | 专用于异常处理的控制器方法上方                               |
| 作用 | 设置指定异常的处理方案，功能等同于控制器方法，<br/>出现异常后终止原始控制器执行,并转入当前方法执行 |

**说明：**此类方法可以根据处理的异常不同，制作多个方法分别处理对应的异常

### 3.3 项目异常处理方案

#### 3.3.1 异常分类

异常处理器我们已经能够使用了，那么在咱们的项目中该如何来处理异常呢?

因为异常的种类有很多，如果每一个异常都对应一个@ExceptionHandler，那得写多少个方法来处理各自的异常，所以我们在处理异常之前，需要对异常进行一个分类:

- 业务异常（BusinessException）

  - 规范的用户行为产生的异常

    - 用户在页面输入内容的时候未按照指定格式进行数据填写，如在年龄框输入的是字符串

      ![1630659599983](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day02/assets/1630659599983.png)

  - 不规范的用户行为操作产生的异常

    - 如用户故意传递错误数据

      ![1630659622958](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day02/assets/1630659622958.png)

- 系统异常（SystemException）

  - 项目运行过程中可预计但无法避免的异常
    - 比如数据库或服务器宕机

- 其他异常（Exception）

  - 编程人员未预期到的异常，如:用到的文件不存在

    ![1630659690341](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day02/assets/1630659690341.png)

将异常分类以后，针对不同类型的异常，要提供具体的解决方案:

#### 3.3.2 异常解决方案

- 业务异常（BusinessException）
  - 发送对应消息传递给用户，提醒规范操作
    - 大家常见的就是提示用户名已存在或密码格式不正确等
- 系统异常（SystemException）
  - 发送固定消息传递给用户，安抚用户
    - 系统繁忙，请稍后再试
    - 系统正在维护升级，请稍后再试
    - 系统出问题，请联系系统管理员等
  - 发送特定消息给运维人员，提醒维护
    - 可以发送短信、邮箱或者是公司内部通信软件
  - 记录日志
    - 发消息和记录日志对用户来说是不可见的，属于后台程序
- 其他异常（Exception）
  - 发送固定消息传递给用户，安抚用户
  - 发送特定消息给编程人员，提醒维护（纳入预期范围内）
    - 一般是程序没有考虑全，比如未做非空校验等
  - 记录日志

#### 3.3.3 异常解决方案的具体实现

> 思路:
>
> 1.先通过自定义异常，完成BusinessException和SystemException的定义
>
> 2.将其他异常包装成自定义异常类型
>
> 3.在异常处理器类中对不同的异常进行处理

##### 步骤1:自定义异常类

```java
//自定义异常处理器，用于封装异常信息，对异常进行分类
public class SystemException extends RuntimeException{
    private Integer code;

    public Integer getCode() {
        return code;
    }

    public void setCode(Integer code) {
        this.code = code;
    }

    public SystemException(Integer code, String message) {
        super(message);
        this.code = code;
    }

    public SystemException(Integer code, String message, Throwable cause) {
        super(message, cause);
        this.code = code;
    }

}

//自定义异常处理器，用于封装异常信息，对异常进行分类
public class BusinessException extends RuntimeException{
    private Integer code;

    public Integer getCode() {
        return code;
    }

    public void setCode(Integer code) {
        this.code = code;
    }

    public BusinessException(Integer code, String message) {
        super(message);
        this.code = code;
    }

    public BusinessException(Integer code, String message, Throwable cause) {
        super(message, cause);
        this.code = code;
    }

}


```

**说明:**

* 让自定义异常类继承`RuntimeException`的好处是，后期在抛出这两个异常的时候，就不用在try...catch...或throws了
* 自定义异常类中添加`code`属性的原因是为了更好的区分异常是来自哪个业务的

##### 步骤2:将其他异常包成自定义异常

假如在BookServiceImpl的getById方法抛异常了，该如何来包装呢?

```java
public Book getById(Integer id) {
    //模拟业务异常，包装成自定义异常
    if(id == 1){
        throw new BusinessException(Code.BUSINESS_ERR,"请不要使用你的技术挑战我的耐性!");
    }
    //模拟系统异常，将可能出现的异常进行包装，转换成自定义异常
    try{
        int i = 1/0;
    }catch (Exception e){
        throw new SystemException(Code.SYSTEM_TIMEOUT_ERR,"服务器访问超时，请重试!",e);
    }
    return bookDao.getById(id);
}
```

具体的包装方式有：

* 方式一:`try{}catch(){}`在catch中重新throw我们自定义异常即可。
* 方式二:直接throw自定义异常即可

上面为了使`code`看着更专业些，我们在Code类中再新增需要的属性

```java
//状态码
public class Code {
    public static final Integer SAVE_OK = 20011;
    public static final Integer DELETE_OK = 20021;
    public static final Integer UPDATE_OK = 20031;
    public static final Integer GET_OK = 20041;

    public static final Integer SAVE_ERR = 20010;
    public static final Integer DELETE_ERR = 20020;
    public static final Integer UPDATE_ERR = 20030;
    public static final Integer GET_ERR = 20040;
    public static final Integer SYSTEM_ERR = 50001;
    public static final Integer SYSTEM_TIMEOUT_ERR = 50002;
    public static final Integer SYSTEM_UNKNOW_ERR = 59999;

    public static final Integer BUSINESS_ERR = 60002;
}

```

##### 步骤3:处理器类中处理自定义异常

```java
//@RestControllerAdvice用于标识当前类为REST风格对应的异常处理器
@RestControllerAdvice
public class ProjectExceptionAdvice {
    //@ExceptionHandler用于设置当前处理器类对应的异常类型
    @ExceptionHandler(SystemException.class)
    public Result doSystemException(SystemException ex){
        //记录日志
        //发送消息给运维
        //发送邮件给开发人员,ex对象发送给开发人员
        return new Result(ex.getCode(),null,ex.getMessage());
    }

    @ExceptionHandler(BusinessException.class)
    public Result doBusinessException(BusinessException ex){
        return new Result(ex.getCode(),null,ex.getMessage());
    }

    //除了自定义的异常处理器，保留对Exception类型的异常处理，用于处理非预期的异常
    @ExceptionHandler(Exception.class)
    public Result doOtherException(Exception ex){
        //记录日志
        //发送消息给运维
        //发送邮件给开发人员,ex对象发送给开发人员
        return new Result(Code.SYSTEM_UNKNOW_ERR,null,"系统繁忙，请稍后再试！");
    }
}
```

##### 步骤4:运行程序

根据ID查询，

如果传入的参数为1，会报`BusinessException`

![1630661162758](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day02/assets/1630661162758.png)

如果传入的是其他参数，会报`SystemException`

![1630661192383](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day02/assets/1630661192383.png)

对于异常我们就已经处理完成了，不管后台哪一层抛出异常，都会以我们与前端约定好的方式进行返回，前端只需要把信息获取到，根据返回的正确与否来展示不同的内容即可。

**小结**

以后项目中的异常处理方式为:

![1630658821746](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day02/assets/1630658821746.png)

## 4，前后台协议联调

### 4.1 环境准备

- 创建一个Web的Maven项目
- pom.xml添加SSM整合所需jar包
- 创建对应的配置类
- 编写Controller、Service接口、Service实现类、Dao接口和模型类
- resources下提供jdbc.properties配置文件

内容参考前面的项目或者直接使用前面的项目进行本节内容的学习。

最终创建好的项目结构如下:

![1630661781776](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day02/assets/1630661781776.png)

1. 将`资料\SSM功能页面`下面的静态资源拷贝到webapp下。

![1630663662691](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day02/assets/1630663662691.png)

2. 因为添加了静态资源，SpringMVC会拦截，所有需要在SpringConfig的配置类中将静态资源进行放行。

* 新建SpringMvcSupport

  ```java
  @Configuration
  public class SpringMvcSupport extends WebMvcConfigurationSupport {
      @Override
      protected void addResourceHandlers(ResourceHandlerRegistry registry) {
          registry.addResourceHandler("/pages/**").addResourceLocations("/pages/");
          registry.addResourceHandler("/css/**").addResourceLocations("/css/");
          registry.addResourceHandler("/js/**").addResourceLocations("/js/");
          registry.addResourceHandler("/plugins/**").addResourceLocations("/plugins/");
      }
  }
  ```

* 在SpringMvcConfig中扫描SpringMvcSupport

  ```java
  @Configuration
  @ComponentScan({"com.itheima.controller","com.itheima.config"})
  @EnableWebMvc
  public class SpringMvcConfig {
  }
  ```

接下来我们就需要将所有的列表查询、新增、修改、删除等功能一个个来实现下。

### 4.2 列表功能

![1630670317859](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day02/assets/1630670317859.png)

> 需求:页面加载完后发送异步请求到后台获取列表数据进行展示。
>
> 1.找到页面的钩子函数，`created()`
>
> 2.`created()`方法中调用了`this.getAll()`方法
>
> 3.在getAll()方法中使用axios发送异步请求从后台获取数据
>
> 4.访问的路径为`http://localhost/books`
>
> 5.返回数据

返回数据res.data的内容如下:

```json
{
    "data": [
        {
            "id": 1,
            "type": "计算机理论",
            "name": "Spring实战 第五版",
            "description": "Spring入门经典教程，深入理解Spring原理技术内幕"
        },
        {
            "id": 2,
            "type": "计算机理论",
            "name": "Spring 5核心原理与30个类手写实践",
            "description": "十年沉淀之作，手写Spring精华思想"
        },...
    ],
    "code": 20041,
    "msg": ""
}
```

发送方式:

```js
getAll() {
    //发送ajax请求
    axios.get("/books").then((res)=>{
        this.dataList = res.data.data;
    });
}
```

![1630666787456](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day02/assets/1630666787456.png)

### 4.3 添加功能

![1630670332168](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day02/assets/1630670332168.png)

> 需求:完成图片的新增功能模块
>
> 1.找到页面上的`新建`按钮，按钮上绑定了`@click="handleCreate()"`方法
>
> 2.在method中找到`handleCreate`方法，方法中打开新增面板
>
> 3.新增面板中找到`确定`按钮,按钮上绑定了`@click="handleAdd()"`方法
>
> 4.在method中找到`handleAdd`方法
>
> 5.在方法中发送请求和数据，响应成功后将新增面板关闭并重新查询数据

`handleCreate`打开新增面板

```js
handleCreate() {
    this.dialogFormVisible = true;
},
```

`handleAdd`方法发送异步请求并携带数据

```js
handleAdd () {
    //发送ajax请求
    //this.formData是表单中的数据，最后是一个json数据
    axios.post("/books",this.formData).then((res)=>{
        this.dialogFormVisible = false;
        this.getAll();
    });
}
```

### 4.4 添加功能状态处理

基础的新增功能已经完成，但是还有一些问题需要解决下:

> 需求:新增成功是关闭面板，重新查询数据，那么新增失败以后该如何处理?
>
> 1.在handlerAdd方法中根据后台返回的数据来进行不同的处理
>
> 2.如果后台返回的是成功，则提示成功信息，并关闭面板
>
> 3.如果后台返回的是失败，则提示错误信息

(1)修改前端页面

```js
handleAdd () {
    //发送ajax请求
    axios.post("/books",this.formData).then((res)=>{
        //如果操作成功，关闭弹层，显示数据
        if(res.data.code == 20011){
            this.dialogFormVisible = false;
            this.$message.success("添加成功");
        }else if(res.data.code == 20010){
            this.$message.error("添加失败");
        }else{
            this.$message.error(res.data.msg);
        }
    }).finally(()=>{
        this.getAll();
    });
}
```

(2)后台返回操作结果，将Dao层的增删改方法返回值从`void`改成`int`

```java
public interface BookDao {

//    @Insert("insert into tbl_book values(null,#{type},#{name},#{description})")
    @Insert("insert into tbl_book (type,name,description) values(#{type},#{name},#{description})")
    public int save(Book book);

    @Update("update tbl_book set type = #{type}, name = #{name}, description = #{description} where id = #{id}")
    public int update(Book book);

    @Delete("delete from tbl_book where id = #{id}")
    public int delete(Integer id);

    @Select("select * from tbl_book where id = #{id}")
    public Book getById(Integer id);

    @Select("select * from tbl_book")
    public List<Book> getAll();
}
```

(3)在BookServiceImpl中，增删改方法根据DAO的返回值来决定返回true/false

```java
@Service
public class BookServiceImpl implements BookService {
    @Autowired
    private BookDao bookDao;

    public boolean save(Book book) {
        return bookDao.save(book) > 0;
    }

    public boolean update(Book book) {
        return bookDao.update(book) > 0;
    }

    public boolean delete(Integer id) {
        return bookDao.delete(id) > 0;
    }

    public Book getById(Integer id) {
        if(id == 1){
            throw new BusinessException(Code.BUSINESS_ERR,"请不要使用你的技术挑战我的耐性!");
        }
//        //将可能出现的异常进行包装，转换成自定义异常
//        try{
//            int i = 1/0;
//        }catch (Exception e){
//            throw new SystemException(Code.SYSTEM_TIMEOUT_ERR,"服务器访问超时，请重试!",e);
//        }
        return bookDao.getById(id);
    }

    public List<Book> getAll() {
        return bookDao.getAll();
    }
}

```

(4)测试错误情况，将图书类别长度设置超出范围即可

![1630668954348](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day02/assets/1630668954348.png)

处理完新增后，会发现新增还存在一个问题，

新增成功后，再次点击`新增`按钮会发现之前的数据还存在，这个时候就需要在新增的时候将表单内容清空。

```js
resetForm(){
	this.formData = {};
}
handleCreate() {
    this.dialogFormVisible = true;
    this.resetForm();
}
```

### 4.5 修改功能

![1630670367812](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day02/assets/1630670367812.png)

>需求:完成图书信息的修改功能
>
>1.找到页面中的`编辑`按钮，该按钮绑定了`@click="handleUpdate(scope.row)"`
>
>2.在method的`handleUpdate`方法中发送异步请求根据ID查询图书信息
>
>3.根据后台返回的结果，判断是否查询成功
>
>​	如果查询成功打开修改面板回显数据，如果失败提示错误信息
>
>4.修改完成后找到修改面板的`确定`按钮，该按钮绑定了`@click="handleEdit()"`
>
>5.在method的`handleEdit`方法中发送异步请求提交修改数据
>
>6.根据后台返回的结果，判断是否修改成功
>
>​	如果成功提示错误信息，关闭修改面板，重新查询数据，如果失败提示错误信息

scope.row代表的是当前行的行数据，也就是说,scope.row就是选中行对应的json数据，如下:

```json
{
    "id": 1,
    "type": "计算机理论",
    "name": "Spring实战 第五版",
    "description": "Spring入门经典教程，深入理解Spring原理技术内幕"
}
```

修改`handleUpdate`方法

```js
//弹出编辑窗口
handleUpdate(row) {
    // console.log(row);   //row.id 查询条件
    //查询数据，根据id查询
    axios.get("/books/"+row.id).then((res)=>{
        if(res.data.code == 20041){
            //展示弹层，加载数据
            this.formData = res.data.data;
            this.dialogFormVisible4Edit = true;
        }else{
            this.$message.error(res.data.msg);
        }
    });
}
```

修改`handleEdit`方法

```js
handleEdit() {
    //发送ajax请求
    axios.put("/books",this.formData).then((res)=>{
        //如果操作成功，关闭弹层，显示数据
        if(res.data.code == 20031){
            this.dialogFormVisible4Edit = false;
            this.$message.success("修改成功");
        }else if(res.data.code == 20030){
            this.$message.error("修改失败");
        }else{
            this.$message.error(res.data.msg);
        }
    }).finally(()=>{
        this.getAll();
    });
}
```

至此修改功能就已经完成。

### 4.6 删除功能

![1630673984385](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day02/assets/1630673984385.png)

> 需求:完成页面的删除功能。
>
> 1.找到页面的删除按钮，按钮上绑定了`@click="handleDelete(scope.row)"`
>
> 2.method的`handleDelete`方法弹出提示框
>
> 3.用户点击取消,提示操作已经被取消。
>
> 4.用户点击确定，发送异步请求并携带需要删除数据的主键ID
>
> 5.根据后台返回结果做不同的操作
>
> ​	如果返回成功，提示成功信息，并重新查询数据
>
> ​	如果返回失败，提示错误信息，并重新查询数据

修改`handleDelete`方法

```js
handleDelete(row) {
    //1.弹出提示框
    this.$confirm("此操作永久删除当前数据，是否继续？","提示",{
        type:'info'
    }).then(()=>{
        //2.做删除业务
        axios.delete("/books/"+row.id).then((res)=>{
            if(res.data.code == 20021){
                this.$message.success("删除成功");
            }else{
                this.$message.error("删除失败");
            }
        }).finally(()=>{
            this.getAll();
        });
    }).catch(()=>{
        //3.取消删除
        this.$message.info("取消删除操作");
    });
}
```

接下来，下面是一个完整页面

```html
<!DOCTYPE html>

<html>

    <head>

        <!-- 页面meta -->

        <meta charset="utf-8">

        <meta http-equiv="X-UA-Compatible" content="IE=edge">

        <title>SpringMVC案例</title>

        <meta content="width=device-width,initial-scale=1,maximum-scale=1,user-scalable=no" name="viewport">

        <!-- 引入样式 -->

        <link rel="stylesheet" href="../plugins/elementui/index.css">

        <link rel="stylesheet" href="../plugins/font-awesome/css/font-awesome.min.css">

        <link rel="stylesheet" href="../css/style.css">

    </head>

    <body class="hold-transition">

        <div id="app">

            <div class="content-header">

                <h1>图书管理</h1>

            </div>

            <div class="app-container">

                <div class="box">

                    <div class="filter-container">

                        <el-input placeholder="图书名称" v-model="pagination.queryString" style="width: 200px;" class="filter-item"></el-input>

                        <el-button @click="getAll()" class="dalfBut">查询</el-button>

                        <el-button type="primary" class="butT" @click="handleCreate()">新建</el-button>

                    </div>

                    <el-table size="small" current-row-key="id" :data="dataList" stripe highlight-current-row>

                        <el-table-column type="index" align="center" label="序号"></el-table-column>

                        <el-table-column prop="type" label="图书类别" align="center"></el-table-column>

                        <el-table-column prop="name" label="图书名称" align="center"></el-table-column>

                        <el-table-column prop="description" label="描述" align="center"></el-table-column>

                        <el-table-column label="操作" align="center">

                            <template slot-scope="scope">

                                <el-button type="primary" size="mini" @click="handleUpdate(scope.row)">编辑</el-button>

                                <el-button type="danger" size="mini" @click="handleDelete(scope.row)">删除</el-button>

                            </template>

                        </el-table-column>

                    </el-table>

                    <!-- 新增标签弹层 -->

                    <div class="add-form">

                        <el-dialog title="新增图书" :visible.sync="dialogFormVisible">

                            <el-form ref="dataAddForm" :model="formData" :rules="rules" label-position="right" label-width="100px">

                                <el-row>

                                    <el-col :span="12">

                                        <el-form-item label="图书类别" prop="type">

                                            <el-input v-model="formData.type"/>

                                        </el-form-item>

                                    </el-col>

                                    <el-col :span="12">

                                        <el-form-item label="图书名称" prop="name">

                                            <el-input v-model="formData.name"/>

                                        </el-form-item>

                                    </el-col>

                                </el-row>


                                <el-row>

                                    <el-col :span="24">

                                        <el-form-item label="描述">

                                            <el-input v-model="formData.description" type="textarea"></el-input>

                                        </el-form-item>

                                    </el-col>

                                </el-row>

                            </el-form>

                            <div slot="footer" class="dialog-footer">

                                <el-button @click="dialogFormVisible = false">取消</el-button>

                                <el-button type="primary" @click="handleAdd()">确定</el-button>

                            </div>

                        </el-dialog>

                    </div>

                    <!-- 编辑标签弹层 -->

                    <div class="add-form">

                        <el-dialog title="编辑检查项" :visible.sync="dialogFormVisible4Edit">

                            <el-form ref="dataEditForm" :model="formData" :rules="rules" label-position="right" label-width="100px">

                                <el-row>

                                    <el-col :span="12">

                                        <el-form-item label="图书类别" prop="type">

                                            <el-input v-model="formData.type"/>

                                        </el-form-item>

                                    </el-col>

                                    <el-col :span="12">

                                        <el-form-item label="图书名称" prop="name">

                                            <el-input v-model="formData.name"/>

                                        </el-form-item>

                                    </el-col>

                                </el-row>

                                <el-row>

                                    <el-col :span="24">

                                        <el-form-item label="描述">

                                            <el-input v-model="formData.description" type="textarea"></el-input>

                                        </el-form-item>

                                    </el-col>

                                </el-row>

                            </el-form>

                            <div slot="footer" class="dialog-footer">

                                <el-button @click="dialogFormVisible4Edit = false">取消</el-button>

                                <el-button type="primary" @click="handleEdit()">确定</el-button>

                            </div>

                        </el-dialog>

                    </div>

                </div>

            </div>

        </div>

    </body>

    <!-- 引入组件库 -->

    <script src="../js/vue.js"></script>

    <script src="../plugins/elementui/index.js"></script>

    <script type="text/javascript" src="../js/jquery.min.js"></script>

    <script src="../js/axios-0.18.0.js"></script>

    <script>
        var vue = new Vue({

            el: '#app',
            data:{
                pagination: {},
				dataList: [],//当前页要展示的列表数据
                formData: {},//表单数据
                dialogFormVisible: false,//控制表单是否可见
                dialogFormVisible4Edit:false,//编辑表单是否可见
                rules: {//校验规则
                    type: [{ required: true, message: '图书类别为必填项', trigger: 'blur' }],
                    name: [{ required: true, message: '图书名称为必填项', trigger: 'blur' }]
                }
            },

            //钩子函数，VUE对象初始化完成后自动执行
            created() {
                this.getAll();
            },

            methods: {
                //列表
                getAll() {
                    //发送ajax请求
                    axios.get("/books").then((res)=>{
                        this.dataList = res.data.data;
                    });
                },

                //弹出添加窗口
                handleCreate() {
                    this.dialogFormVisible = true;
                    this.resetForm();
                },

                //重置表单
                resetForm() {
                    this.formData = {};
                },

                //添加
                handleAdd () {
                    //发送ajax请求
                    axios.post("/books",this.formData).then((res)=>{
                        console.log(res.data);
                        //如果操作成功，关闭弹层，显示数据
                        if(res.data.code == 20011){
                            this.dialogFormVisible = false;
                            this.$message.success("添加成功");
                        }else if(res.data.code == 20010){
                            this.$message.error("添加失败");
                        }else{
                            this.$message.error(res.data.msg);
                        }
                    }).finally(()=>{
                        this.getAll();
                    });
                },

                //弹出编辑窗口
                handleUpdate(row) {
                    // console.log(row);   //row.id 查询条件
                    //查询数据，根据id查询
                    axios.get("/books/"+row.id).then((res)=>{
                        // console.log(res.data.data);
                        if(res.data.code == 20041){
                            //展示弹层，加载数据
                            this.formData = res.data.data;
                            this.dialogFormVisible4Edit = true;
                        }else{
                            this.$message.error(res.data.msg);
                        }
                    });
                },

                //编辑
                handleEdit() {
                    //发送ajax请求
                    axios.put("/books",this.formData).then((res)=>{
                        //如果操作成功，关闭弹层，显示数据
                        if(res.data.code == 20031){
                            this.dialogFormVisible4Edit = false;
                            this.$message.success("修改成功");
                        }else if(res.data.code == 20030){
                            this.$message.error("修改失败");
                        }else{
                            this.$message.error(res.data.msg);
                        }
                    }).finally(()=>{
                        this.getAll();
                    });
                },

                // 删除
                handleDelete(row) {
                    //1.弹出提示框
                    this.$confirm("此操作永久删除当前数据，是否继续？","提示",{
                        type:'info'
                    }).then(()=>{
                        //2.做删除业务
                        axios.delete("/books/"+row.id).then((res)=>{
                            if(res.data.code == 20021){
                                this.$message.success("删除成功");
                            }else{
                                this.$message.error("删除失败");
                            }
                        }).finally(()=>{
                            this.getAll();
                        });
                    }).catch(()=>{
                        //3.取消删除
                        this.$message.info("取消删除操作");
                    });
                }
            }
        })

    </script>

</html>
```

## 5，拦截器

对于拦截器这节的知识，我们需要学习如下内容:

* 拦截器概念
* 入门案例
* 拦截器参数
* 拦截器工作流程分析

### 5.1 拦截器概念

讲解拦截器的概念之前，我们先看一张图:

![1630676280170](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day02/assets/1630676280170.png)

(1)浏览器发送一个请求会先到Tomcat的web服务器

(2)Tomcat服务器接收到请求以后，会去判断请求的是静态资源还是动态资源

(3)如果是静态资源，会直接到Tomcat的项目部署目录下去直接访问

(4)如果是动态资源，就需要交给项目的后台代码进行处理

(5)在找到具体的方法之前，我们可以去配置过滤器(可以配置多个)，按照顺序进行执行

(6)然后进入到到中央处理器(SpringMVC中的内容)，SpringMVC会根据配置的规则进行拦截

(7)如果满足规则，则进行处理，找到其对应的controller类中的方法进行执行,完成后返回结果

(8)如果不满足规则，则不进行处理

(9)这个时候，如果我们需要在每个Controller方法执行的前后添加业务，具体该如何来实现?

这个就是拦截器要做的事。

* 拦截器（Interceptor）是一种动态拦截方法调用的机制，在SpringMVC中动态拦截控制器方法的执行
* 作用:
  * 在指定的方法调用前后执行预先设定的代码
  * 阻止原始方法的执行
  * 总结：拦截器就是用来做增强

看完以后，大家会发现

* 拦截器和过滤器在作用和执行顺序上也很相似

所以这个时候，就有一个问题需要思考:拦截器和过滤器之间的区别是什么?

- 归属不同：Filter属于Servlet技术，Interceptor属于SpringMVC技术
- 拦截内容不同：Filter对所有访问进行增强，Interceptor仅针对SpringMVC的访问进行增强

![1630676903190](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day02/assets/1630676903190.png)

### 5.2 拦截器入门案例

#### 5.2.1 环境准备

- 创建一个Web的Maven项目

- pom.xml添加SSM整合所需jar包

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  
  <project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
  
    <groupId>com.itheima</groupId>
    <artifactId>springmvc_12_interceptor</artifactId>
    <version>1.0-SNAPSHOT</version>
    <packaging>war</packaging>
  
    <dependencies>
      <dependency>
        <groupId>javax.servlet</groupId>
        <artifactId>javax.servlet-api</artifactId>
        <version>3.1.0</version>
        <scope>provided</scope>
      </dependency>
      <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-webmvc</artifactId>
        <version>5.2.10.RELEASE</version>
      </dependency>
      <dependency>
        <groupId>com.fasterxml.jackson.core</groupId>
        <artifactId>jackson-databind</artifactId>
        <version>2.9.0</version>
      </dependency>
    </dependencies>
  
    <build>
      <plugins>
        <plugin>
          <groupId>org.apache.tomcat.maven</groupId>
          <artifactId>tomcat7-maven-plugin</artifactId>
          <version>2.1</version>
          <configuration>
            <port>80</port>
            <path>/</path>
          </configuration>
        </plugin>
          <plugin>
              <groupId>org.apache.maven.plugins</groupId>
              <artifactId>maven-compiler-plugin</artifactId>
              <configuration>
                  <source>8</source>
                  <target>8</target>
              </configuration>
          </plugin>
      </plugins>
    </build>
  </project>
  
  ```

- 创建对应的配置类

  ```java
  public class ServletContainersInitConfig extends AbstractAnnotationConfigDispatcherServletInitializer {
      protected Class<?>[] getRootConfigClasses() {
          return new Class[0];
      }
  
      protected Class<?>[] getServletConfigClasses() {
          return new Class[]{SpringMvcConfig.class};
      }
  
      protected String[] getServletMappings() {
          return new String[]{"/"};
      }
  
      //乱码处理
      @Override
      protected Filter[] getServletFilters() {
          CharacterEncodingFilter filter = new CharacterEncodingFilter();
          filter.setEncoding("UTF-8");
          return new Filter[]{filter};
      }
  }
  
  @Configuration
  @ComponentScan({"com.itheima.controller"})
  @EnableWebMvc
  public class SpringMvcConfig{
     
  }
  ```

- 创建模型类Book

  ```java
  public class Book {
      private String name;
      private double price;
  
      public String getName() {
          return name;
      }
  
      public void setName(String name) {
          this.name = name;
      }
  
      public double getPrice() {
          return price;
      }
  
      public void setPrice(double price) {
          this.price = price;
      }
  
      @Override
      public String toString() {
          return "Book{" +
                  "书名='" + name + '\'' +
                  ", 价格=" + price +
                  '}';
      }
  }
  ```

- 编写Controller

  ```java
  @RestController
  @RequestMapping("/books")
  public class BookController {
  
      @PostMapping
      public String save(@RequestBody Book book){
          System.out.println("book save..." + book);
          return "{'module':'book save'}";
      }
  
      @DeleteMapping("/{id}")
      public String delete(@PathVariable Integer id){
          System.out.println("book delete..." + id);
          return "{'module':'book delete'}";
      }
  
      @PutMapping
      public String update(@RequestBody Book book){
          System.out.println("book update..."+book);
          return "{'module':'book update'}";
      }
  
      @GetMapping("/{id}")
      public String getById(@PathVariable Integer id){
          System.out.println("book getById..."+id);
          return "{'module':'book getById'}";
      }
  
      @GetMapping
      public String getAll(){
          System.out.println("book getAll...");
          return "{'module':'book getAll'}";
      }
  }
  ```

最终创建好的项目结构如下:

![1630677370998](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day02/assets/1630677370998.png)

#### 5.2.2 拦截器开发

##### 步骤1:创建拦截器类

让类实现HandlerInterceptor接口，重写接口中的三个方法。

```java
@Component
//定义拦截器类，实现HandlerInterceptor接口
//注意当前类必须受Spring容器控制
public class ProjectInterceptor implements HandlerInterceptor {
    @Override
    //原始方法调用前执行的内容
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
        System.out.println("preHandle...");
        return true;
    }

    @Override
    //原始方法调用后执行的内容
    public void postHandle(HttpServletRequest request, HttpServletResponse response, Object handler, ModelAndView modelAndView) throws Exception {
        System.out.println("postHandle...");
    }

    @Override
    //原始方法调用完成后执行的内容
    public void afterCompletion(HttpServletRequest request, HttpServletResponse response, Object handler, Exception ex) throws Exception {
        System.out.println("afterCompletion...");
    }
}
```

**注意:**拦截器类要被SpringMVC容器扫描到。

##### 步骤2:配置拦截器类

```java
@Configuration
public class SpringMvcSupport extends WebMvcConfigurationSupport {
    @Autowired
    private ProjectInterceptor projectInterceptor;

    @Override
    protected void addResourceHandlers(ResourceHandlerRegistry registry) {
        registry.addResourceHandler("/pages/**").addResourceLocations("/pages/");
    }

    @Override
    protected void addInterceptors(InterceptorRegistry registry) {
        //配置拦截器
        registry.addInterceptor(projectInterceptor).addPathPatterns("/books" );
    }
}
```

##### 步骤3:SpringMVC添加SpringMvcSupport包扫描

```java
@Configuration
@ComponentScan({"com.itheima.controller","com.itheima.config"})
@EnableWebMvc
public class SpringMvcConfig{
   
}
```

##### 步骤4:运行程序测试

使用PostMan发送`http://localhost/books`

![1630678114224](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day02/assets/1630678114224.png)

如果发送`http://localhost/books/100`会发现拦截器没有被执行，原因是拦截器的`addPathPatterns`方法配置的拦截路径是`/books`,我们现在发送的是`/books/100`，所以没有匹配上，因此没有拦截，拦截器就不会执行。

##### 步骤5:修改拦截器拦截规则

```java
@Configuration
public class SpringMvcSupport extends WebMvcConfigurationSupport {
    @Autowired
    private ProjectInterceptor projectInterceptor;

    @Override
    protected void addResourceHandlers(ResourceHandlerRegistry registry) {
        registry.addResourceHandler("/pages/**").addResourceLocations("/pages/");
    }

    @Override
    protected void addInterceptors(InterceptorRegistry registry) {
        //配置拦截器
        registry.addInterceptor(projectInterceptor).addPathPatterns("/books","/books/*" );
    }
}
```

这个时候，如果再次访问`http://localhost/books/100`，拦截器就会被执行。

最后说一件事，就是拦截器中的`preHandler`方法，如果返回true,则代表放行，会执行原始Controller类中要请求的方法，如果返回false，则代表拦截，后面的就不会再执行了。

##### 步骤6:简化SpringMvcSupport的编写

```java
@Configuration
@ComponentScan({"com.itheima.controller"})
@EnableWebMvc
//实现WebMvcConfigurer接口可以简化开发，但具有一定的侵入性
public class SpringMvcConfig implements WebMvcConfigurer {
    @Autowired
    private ProjectInterceptor projectInterceptor;

    @Override
    public void addInterceptors(InterceptorRegistry registry) {
        //配置多拦截器
        registry.addInterceptor(projectInterceptor).addPathPatterns("/books","/books/*");
    }
}
```

此后咱们就不用再写`SpringMvcSupport`类了。

最后我们来看下拦截器的执行流程:

![1630679464294](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day02/assets/1630679464294.png)

当有拦截器后，请求会先进入preHandle方法，

​	如果方法返回true，则放行继续执行后面的handle[controller的方法]和后面的方法

​	如果返回false，则直接跳过后面方法的执行。

### 5.3 拦截器参数

#### 5.3.1 前置处理方法

原始方法之前运行preHandle

```java
public boolean preHandle(HttpServletRequest request,
                         HttpServletResponse response,
                         Object handler) throws Exception {
    System.out.println("preHandle");
    return true;
}
```

* request:请求对象
* response:响应对象
* handler:被调用的处理器对象，本质上是一个方法对象，对反射中的Method对象进行了再包装

使用request对象可以获取请求数据中的内容，如获取请求头的`Content-Type`

```java
public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
    String contentType = request.getHeader("Content-Type");
    System.out.println("preHandle..."+contentType);
    return true;
}
```

使用handler参数，可以获取方法的相关信息

```java
public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
    HandlerMethod hm = (HandlerMethod)handler;
    String methodName = hm.getMethod().getName();//可以获取方法的名称
    System.out.println("preHandle..."+methodName);
    return true;
}
```

#### 5.3.2 后置处理方法

原始方法运行后运行，如果原始方法被拦截，则不执行  

```java
public void postHandle(HttpServletRequest request,
                       HttpServletResponse response,
                       Object handler,
                       ModelAndView modelAndView) throws Exception {
    System.out.println("postHandle");
}
```

前三个参数和上面的是一致的。

modelAndView:如果处理器执行完成具有返回结果，可以读取到对应数据与页面信息，并进行调整

因为咱们现在都是返回json数据，所以该参数的使用率不高。

#### 5.3.3 完成处理方法

拦截器最后执行的方法，无论原始方法是否执行

```java
public void afterCompletion(HttpServletRequest request,
                            HttpServletResponse response,
                            Object handler,
                            Exception ex) throws Exception {
    System.out.println("afterCompletion");
}
```

前三个参数与上面的是一致的。

ex:如果处理器执行过程中出现异常对象，可以针对异常情况进行单独处理  

因为我们现在已经有全局异常处理器类，所以该参数的使用率也不高。

这三个方法中，最常用的是==preHandle==,在这个方法中可以通过返回值来决定是否要进行放行，我们可以把业务逻辑放在该方法中，如果满足业务则返回true放行，不满足则返回false拦截。

### 5.4 拦截器链配置

目前，我们在项目中只添加了一个拦截器，如果有多个，该如何配置?配置多个后，执行顺序是什么?

#### 5.4.1 配置多个拦截器

##### 步骤1:创建拦截器类

实现接口，并重写接口中的方法

```java
@Component
public class ProjectInterceptor2 implements HandlerInterceptor {
    @Override
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
        System.out.println("preHandle...222");
        return false;
    }

    @Override
    public void postHandle(HttpServletRequest request, HttpServletResponse response, Object handler, ModelAndView modelAndView) throws Exception {
        System.out.println("postHandle...222");
    }

    @Override
    public void afterCompletion(HttpServletRequest request, HttpServletResponse response, Object handler, Exception ex) throws Exception {
        System.out.println("afterCompletion...222");
    }
}
```

##### 步骤2:配置拦截器类

```java
@Configuration
@ComponentScan({"com.itheima.controller"})
@EnableWebMvc
//实现WebMvcConfigurer接口可以简化开发，但具有一定的侵入性
public class SpringMvcConfig implements WebMvcConfigurer {
    @Autowired
    private ProjectInterceptor projectInterceptor;
    @Autowired
    private ProjectInterceptor2 projectInterceptor2;

    @Override
    public void addInterceptors(InterceptorRegistry registry) {
        //配置多拦截器
        registry.addInterceptor(projectInterceptor).addPathPatterns("/books","/books/*");
        registry.addInterceptor(projectInterceptor2).addPathPatterns("/books","/books/*");
    }
}
```

步骤3:运行程序，观察顺序

![1630680435269](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day02/assets/1630680435269.png)

拦截器执行的顺序是和配置顺序有关。就和前面所提到的运维人员进入机房的案例，先进后出。

* 当配置多个拦截器时，形成拦截器链
* 拦截器链的运行顺序参照拦截器添加顺序为准
* 当拦截器中出现对原始处理器的拦截，后面的拦截器均终止运行
* 当拦截器运行中断，仅运行配置在前面的拦截器的afterCompletion操作

![1630680579735](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/SpringMVC笔记/SpringMVC_day02/assets/1630680579735.png)

preHandle：与配置顺序相同，必定运行

postHandle:与配置顺序相反，可能不运行

afterCompletion:与配置顺序相反，可能不运行。

这个顺序不太好记，最终只需要把握住一个原则即可:==以最终的运行结果为准==

# Maven高级

**今日目标**

> * 理解并实现分模块开发
> * 能够使用聚合工程快速构建项目
> * 能够使用继承简化项目配置
> * 能够根据需求配置生成、开发、测试环境，并在各个环境间切换运行
> * 了解Maven的私服

## 1，分模块开发

### 1.1 分模块开发设计

(1)按照功能拆分

我们现在的项目都是在一个模块中，比如前面的SSM整合开发。虽然这样做功能也都实现了，但是也存在了一些问题，我们拿银行的项目为例来聊聊这个事。

* 网络没有那么发达的时候，我们需要到银行柜台或者取款机进行业务操作
* 随着互联网的发展,我们有了电脑以后，就可以在网页上登录银行网站使用U盾进行业务操作
* 再来就是随着智能手机的普及，我们只需要用手机登录APP就可以进行业务操作

上面三个场景出现的时间是不相同的，如果非要把三个场景的模块代码放入到一个项目，那么当其中某一个模块代码出现问题，就会导致整个项目无法正常启动，从而导致银行的多个业务都无法正常班理。所以我们会==按照功能==将项目进行拆分。

(2)按照模块拆分

比如电商的项目中，有订单和商品两个模块，订单中需要包含商品的详细信息，所以需要商品的模型类，商品模块也会用到商品的模型类，这个时候如果两个模块中都写模型类，就会出现重复代码，后期的维护成本就比较高。我们就想能不能将它们公共的部分抽取成一个独立的模块，其他模块要想使用可以像添加第三方jar包依赖一样来使用我们自己抽取的模块，这样就解决了代码重复的问题,这种拆分方式就说我们所说的==按照模块==拆分。

![1630768703430](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Maven高级笔记/assets/1630768703430.png)

经过两个案例的分析，我们就知道:

* 将原始模块按照功能拆分成若干个子模块，方便模块间的相互调用，接口共享。

刚刚我们说了可以将domain层进行拆分，除了domain层，我们也可以将其他的层也拆成一个个对立的模块，如:

![1630768869208](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Maven高级笔记/assets/1630768869208.png)

这样的话，项目中的每一层都可以单独维护，也可以很方便的被别人使用。关于分模块开发的意义，我们就说完了，说了这么多好处，那么该如何实现呢?

### 1.2 分模块开发实现

前面我们已经完成了SSM整合，接下来，咱们就基于SSM整合的项目来实现对项目的拆分。

#### 1.2.1 环境准备

将`资料\maven_02_ssm`部署到IDEA中，将环境快速准备好，部署成功后，项目的格式如下:

![1630769969416](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Maven高级笔记/assets/1630769969416.png)

#### 1.2.2 抽取domain层

##### 步骤1:创建新模块

创建一个名称为`maven_03_pojo`的jar项目,为什么项目名是从02到03这样创建，原因后面我们会提到，这块的名称可以任意。

![1630771178137](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Maven高级笔记/assets/1630771178137.png)

##### 步骤2:项目中创建domain包

在`maven_03_pojo`项目中创建`com.itheima.domain`包，并将`maven_02_ssm`中Book类拷贝到该包中

![1630771371487](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Maven高级笔记/assets/1630771371487.png)

##### 步骤3:删除原项目中的domain包

删除后，`maven_02_ssm`项目中用到`Book`的类中都会有红色提示，如下:

![1630771505703](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Maven高级笔记/assets/1630771505703.png)

**说明:**出错的原因是`maven_02_ssm`中已经将Book类删除，所以该项目找不到Book类，所以报错

要想解决上述问题，我们需要在`maven_02_ssm`中添加`maven_03_pojo`的依赖。

##### 步骤4:建立依赖关系

在`maven_02_ssm`项目的pom.xml添加`maven_03_pojo`的依赖

```xml
<dependency>
    <groupId>com.itheima</groupId>
    <artifactId>maven_03_pojo</artifactId>
    <version>1.0-SNAPSHOT</version>
</dependency>
```

因为添加了依赖，所以在`maven_02_ssm`中就已经能找到Book类，所以刚才的报红提示就会消失。

##### 步骤5:编译`maven_02_ssm`项目

编译`maven_02_ssm`你会在控制台看到如下错误

![1630771987325](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Maven高级笔记/assets/1630771987325.png)

错误信息为：不能解决`maven_02_ssm`项目的依赖问题，找不到`maven_03_pojo`这个jar包。

为什么找不到呢?

原因是Maven会从本地仓库找对应的jar包，但是本地仓库又不存在该jar包所以会报错。

在IDEA中是有`maven_03_pojo`这个项目，所以我们只需要将`maven_03_pojo`项目安装到本地仓库即可。

##### 步骤6:将项目安装本地仓库

将需要被依赖的项目`maven_03_pojo`，使用maven的install命令，把其安装到Maven的本地仓库中。

![1630773180969](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Maven高级笔记/assets/1630773180969.png)

安装成功后，在对应的路径下就看到安装好的jar包

![1630773262441](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Maven高级笔记/assets/1630773262441.png)

**说明:**具体安装在哪里，和你们自己电脑上Maven的本地仓库配置的位置有关。

当再次执行`maven_02_ssm`的compile的命令后，就已经能够成功编译。

#### 1.2.3 抽取Dao层

##### 步骤1:创建新模块

创建一个名称为`maven_04_dao`的jar项目

![1630773580067](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Maven高级笔记/assets/1630773580067.png)

##### 步骤2:项目中创建dao包

在`maven_04_dao`项目中创建`com.itheima.dao`包，并将`maven_02_ssm`中BookDao类拷贝到该包中

![1630773695062](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Maven高级笔记/assets/1630773695062.png)

在`maven_04_dao`中会有如下几个问题需要解决下:

![1630773958756](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Maven高级笔记/assets/1630773958756.png)

* 项目`maven_04_dao`的BookDao接口中Book类找不到报错

  * 解决方案在`maven_04_dao`项目的pom.xml中添加`maven_03_pojo`项目

    ```xml
    <dependencies>
        <dependency>
            <groupId>com.itheima</groupId>
            <artifactId>maven_03_pojo</artifactId>
            <version>1.0-SNAPSHOT</version>
        </dependency>
    </dependencies>
    ```

* 项目`maven_04_dao`的BookDao接口中，Mybatis的增删改查注解报错

  * 解决方案在`maven_04_dao`项目的pom.xml中添加`mybatis`的相关依赖

    ```xml
    <dependencies>
        <dependency>
            <groupId>org.mybatis</groupId>
            <artifactId>mybatis</artifactId>
            <version>3.5.6</version>
        </dependency>
    
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>5.1.47</version>
        </dependency>
    </dependencies>
    ```

##### 步骤3:删除原项目中的dao包

删除Dao包以后，因为`maven_02_ssm`中的BookServiceImpl类中有使用到Dao的内容，所以需要在`maven_02_ssm`的pom.xml添加`maven_04_dao`的依赖

```xml
<dependency>
    <groupId>com.itheima</groupId>
    <artifactId>maven_04_dao</artifactId>
    <version>1.0-SNAPSHOT</version>
</dependency>
```

此时在`maven_02_ssm`项目中就已经添加了`maven_03_pojo`和`maven_04_dao`包

![1630774696344](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Maven高级笔记/assets/1630774696344.png)

再次对`maven_02_ssm`项目进行编译，又会报错，如下:

![1630774780211](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Maven高级笔记/assets/1630774780211.png)

和刚才的错误原因是一样的，maven在仓库中没有找到`maven_04_dao`,所以此时我们只需要将`maven_04_dao`安装到Maven的本地仓库即可。

##### 步骤4:将项目安装到本地仓库

将需要被依赖的项目`maven_04_dao`，使用maven的install命令，把其安装到Maven的本地仓库中。

![1630774917743](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Maven高级笔记/assets/1630774917743.png)

安装成功后，在对应的路径下就看到了安装好对应的jar包

![1630774946856](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Maven高级笔记/assets/1630774946856.png)

当再次执行`maven_02_ssm`的compile的指令后，就已经能够成功编译。

#### 1.2.4 运行测试并总结

将抽取后的项目进行运行，测试之前的增删改查功能依然能够使用。

所以对于项目的拆分，大致会有如下几个步骤:

(1) 创建Maven模块

(2) 书写模块代码

分模块开发需要先针对模块功能进行设计，再进行编码。不会先将工程开发完毕，然后进行拆分。拆分方式可以按照功能拆也可以按照模块拆。

(3)通过maven指令安装模块到本地仓库(install 指令)

团队内部开发需要发布模块功能到团队内部可共享的仓库中(私服)，私服我们后面会讲解。

## 2，依赖管理

我们现在已经能把项目拆分成一个个独立的模块，当在其他项目中想要使用独立出来的这些模块，只需要在其pom.xml使用<dependency>标签来进行jar包的引入即可。

<dependency>其实就是依赖，关于依赖管理里面都涉及哪些内容，我们就一个个来学习下:

* 依赖传递
* 可选依赖
* 排除依赖

我们先来说说什么是依赖:

依赖指当前项目运行所需的jar，一个项目可以设置多个依赖。

格式为:

```xml
<!--设置当前项目所依赖的所有jar-->
<dependencies>
    <!--设置具体的依赖-->
    <dependency>
        <!--依赖所属群组id-->
        <groupId>org.springframework</groupId>
        <!--依赖所属项目id-->
        <artifactId>spring-webmvc</artifactId>
        <!--依赖版本号-->
        <version>5.2.10.RELEASE</version>
    </dependency>
</dependencies>
```

### 2.1 依赖传递与冲突问题

回到我们刚才的项目案例中，打开Maven的面板，你会发现:

![](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Maven高级笔记/assets/1630818930387.png)

在项目所依赖的这些jar包中，有一个比较大的区别就是**有的依赖前面有箭头`>`,有的依赖前面没有。**

那么这个箭头所代表的含义是什么?

打开前面的箭头，你会发现这个jar包下面还包含有其他的jar包

![1630819455928](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Maven高级笔记/assets/1630819455928.png)

你会发现有两个`maven_03_pojo`的依赖被加载到Dependencies中，那么`maven_04_dao`中的`maven_03_pojo`能不能使用呢?

要想验证非常简单，只需要把`maven_02_ssm`项目中pom.xml关于`maven_03_pojo`的依赖注释或删除掉

![1630819768305](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Maven高级笔记/assets/1630819768305.png)

在Dependencies中移除自己所添加`maven_03_pojo`依赖后，打开BookServiceImpl的类，你会发现Book类依然存在，可以被正常使用

![1630819826163](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Maven高级笔记/assets/1630819826163.png)

这个特性其实就是我们要讲解的==依赖传递==。

依赖是具有传递性的:

![1630853726532](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Maven高级笔记/assets/1630853726532.png)

**说明:**A代表自己的项目；B,C,D,E,F,G代表的是项目所依赖的jar包；D1和D2 E1和E2代表是相同jar包的不同版本

(1) A依赖了B和C,B和C有分别依赖了其他jar包，所以在A项目中就可以使用上面所有jar包，这就是所说的依赖传递

(2) 依赖传递有直接依赖和间接依赖

* 相对于A来说，A直接依赖B和C,间接依赖了D1,E1,G，F,D2和E2
* 相对于B来说，B直接依赖了D1和E1,间接依赖了G
* 直接依赖和间接依赖是一个相对的概念

(3)因为有依赖传递的存在，就会导致jar包在依赖的过程中出现冲突问题，具体什么是冲突?Maven是如何解决冲突的?

这里所说的==依赖冲突==是指项目依赖的某一个jar包，有多个不同的版本，因而造成类包版本冲突。

情况一: 在`maven_02_ssm`的pom.xml中添加两个不同版本的Junit依赖:

```xml
<dependencies>
    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>4.12</version>
      <scope>test</scope>
    </dependency>

    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>4.11</version>
      <scope>test</scope>
    </dependency>
</dependencies>
```

![1630820964663](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Maven高级笔记/assets/1630820964663.png)

通过对比，会发现一个结论

* 特殊优先：当同级配置了相同资源的不同版本，后配置的覆盖先配置的。

情况二: 路径优先：当依赖中出现相同的资源时，层级越深，优先级越低，层级越浅，优先级越高

* A通过B间接依赖到E1
* A通过C间接依赖到E2
* A就会间接依赖到E1和E2,Maven会按照层级来选择，E1是2度，E2是3度，所以最终会选择E1

情况三: 声明优先：当资源在相同层级被依赖时，配置顺序靠前的覆盖配置顺序靠后的

* A通过B间接依赖到D1
* A通过C间接依赖到D2
* D1和D2都是两度，这个时候就不能按照层级来选择，需要按照声明来，谁先声明用谁，也就是说B在C之前声明，这个时候使用的是D1，反之则为D2

但是对应上面这些结果，大家不需要刻意去记它。因为不管Maven怎么选，最终的结果都会在Maven的`Dependencies`面板中展示出来，展示的是哪个版本，也就是说它选择的就是哪个版本，如:

![1630853443920](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Maven高级笔记/assets/1630853443920.png)

如果想更全面的查看Maven中各个坐标的依赖关系，可以点击Maven面板中的`show Dependencies`

![1630853519736](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Maven高级笔记/assets/1630853519736.png)

在这个视图中就能很明显的展示出jar包之间的相互依赖关系。

### 2.2 可选依赖和排除依赖

依赖传递介绍完以后，我们来思考一个问题，

![1630854436435](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Maven高级笔记/assets/1630854436435.png)

* maven_02_ssm 依赖了 maven_04_dao
* maven_04_dao 依赖了 maven_03_pojo
* 因为现在有依赖传递，所以maven_02_ssm能够使用到maven_03_pojo的内容
* 如果说现在不想让maven_02_ssm依赖到maven_03_pojo，有哪些解决方案?

**说明:**在真实使用的过程中，maven_02_ssm中是需要用到maven_03_pojo的，我们这里只是用这个例子描述我们的需求。因为有时候，maven_04_dao出于某些因素的考虑，就是不想让别人使用自己所依赖的maven_03_pojo。

#### 方案一:可选依赖

* 可选依赖指对外隐藏当前所依赖的资源---不透明

在`maven_04_dao`的pom.xml,在引入`maven_03_pojo`的时候，添加`optional`

```xml
<dependency>
    <groupId>com.itheima</groupId>
    <artifactId>maven_03_pojo</artifactId>
    <version>1.0-SNAPSHOT</version>
    <!--可选依赖是隐藏当前工程所依赖的资源，隐藏后对应资源将不具有依赖传递-->
    <optional>true</optional>
</dependency>
```

此时BookServiceImpl就已经报错了,说明由于maven_04_dao将maven_03_pojo设置成可选依赖，导致maven_02_ssm无法引用到maven_03_pojo中的内容，导致Book类找不到。

![1630854923484](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Maven高级笔记/assets/1630854923484.png)

#### 方案二:排除依赖

* 排除依赖指主动断开依赖的资源，被排除的资源无需指定版本---不需要

前面我们已经通过可选依赖实现了阻断maven_03_pojo的依赖传递，对于排除依赖，则指的是已经有依赖的事实，也就是说maven_02_ssm项目中已经通过依赖传递用到了maven_03_pojo，此时我们需要做的是将其进行排除，所以接下来需要修改maven_02_ssm的pom.xml

```xml
<dependency>
    <groupId>com.itheima</groupId>
    <artifactId>maven_04_dao</artifactId>
    <version>1.0-SNAPSHOT</version>
    <!--排除依赖是隐藏当前资源对应的依赖关系-->
    <exclusions>
        <exclusion>
            <groupId>com.itheima</groupId>
            <artifactId>maven_03_pojo</artifactId>
        </exclusion>
    </exclusions>
</dependency>
```

这样操作后，BookServiceImpl中的Book类一样也会报错。

当然`exclusions`标签带`s`说明我们是可以依次排除多个依赖到的jar包，比如maven_04_dao中有依赖junit和mybatis,我们也可以一并将其排除。

```xml
<dependency>
    <groupId>com.itheima</groupId>
    <artifactId>maven_04_dao</artifactId>
    <version>1.0-SNAPSHOT</version>
    <!--排除依赖是隐藏当前资源对应的依赖关系-->
    <exclusions>
        <exclusion>
            <groupId>com.itheima</groupId>
            <artifactId>maven_03_pojo</artifactId>
        </exclusion>
        <exclusion>
            <groupId>log4j</groupId>
            <artifactId>log4j</artifactId>
        </exclusion>
        <exclusion>
            <groupId>org.mybatis</groupId>
            <artifactId>mybatis</artifactId>
        </exclusion>
    </exclusions>
</dependency>
```

介绍我这两种方式后，简单来梳理下，就是

* `A依赖B,B依赖C`,`C`通过依赖传递会被`A`使用到，现在要想办法让`A`不去依赖`C`
* 可选依赖是在B上设置`<optional>`,`A`不知道有`C`的存在，
* 排除依赖是在A上设置`<exclusions>`,`A`知道有`C`的存在，主动将其排除掉。

## 3，聚合和继承

我们的项目已经从以前的单模块，变成了现在的多模块开发。项目一旦变成了多模块开发以后，就会引发一些问题，在这一节中我们主要会学习两个内容`聚合`和`继承`，用这两个知识来解决下分模块后的一些问题。

### 3.1 聚合

![1630858596147](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Maven高级笔记/assets/1630858596147.png)

* 分模块开发后，需要将这四个项目都安装到本地仓库，目前我们只能通过项目Maven面板的`install`来安装，并且需要安装四个，如果我们的项目足够多，那么一个个安装起来还是比较麻烦的
* 如果四个项目都已经安装成功，当ssm_pojo发生变化后，我们就得将ssm_pojo重新安装到maven仓库，但是为了确保我们对ssm_pojo的修改不会影响到其他项目模块，我们需要对所有的模块进行重新编译，那又需要将所有的模块再来一遍

项目少的话还好，但是如果项目多的话，一个个操作项目就容易出现漏掉或重复操作的问题，所以我们就想能不能抽取一个项目，把所有的项目管理起来，以后我们要想操作这些项目，只需要操作这一个项目，其他所有的项目都走一样的流程，这个不就很省事省力。

这就用到了我们接下来要讲解的==聚合==，

* 所谓聚合:将多个模块组织成一个整体，同时进行项目构建的过程称为聚合
* 聚合工程：通常是一个不具有业务功能的"空"工程（有且仅有一个pom文件）
* 作用：使用聚合工程可以将多个工程编组，通过对聚合工程进行构建，实现对所包含的模块进行同步构建
  * 当工程中某个模块发生更新（变更）时，必须保障工程中与已更新模块关联的模块同步更新，此时可以使用聚合工程来解决批量模块同步构建的问题。

关于聚合具体的实现步骤为:

#### 步骤1:创建一个空的maven项目

![1630859532119](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Maven高级笔记/assets/1630859532119.png)

#### 步骤2:将项目的打包方式改为pom

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.itheima</groupId>
    <artifactId>maven_01_parent</artifactId>
    <version>1.0-RELEASE</version>
    <packaging>pom</packaging>
    
</project>
```

**说明:**项目的打包方式，我们接触到的有三种，分别是

* jar:默认情况，说明该项目为java项目
* war:说明该项目为web项目
* pom:说明该项目为聚合或继承(后面会讲)项目

#### 步骤3:pom.xml添加所要管理的项目

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.itheima</groupId>
    <artifactId>maven_01_parent</artifactId>
    <version>1.0-RELEASE</version>
    <packaging>pom</packaging>
    
    <!--设置管理的模块名称-->
    <modules>
        <module>../maven_02_ssm</module>
        <module>../maven_03_pojo</module>
        <module>../maven_04_dao</module>
    </modules>
</project>
```

#### 步骤4:使用聚合统一管理项目

![1630859797123](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Maven高级笔记/assets/1630859797123.png)

测试发现，当`maven_01_parent`的`compile`被点击后，所有被其管理的项目都会被执行编译操作。这就是聚合工程的作用。

**说明：**聚合工程管理的项目在进行运行的时候，会按照项目与项目之间的依赖关系来自动决定执行的顺序和配置的顺序无关。

聚合的知识我们就讲解完了，最后总结一句话就是，**聚合工程主要是用来管理项目**。

### 3.2 继承

我们已经完成了使用聚合工程去管理项目，聚合工程进行某一个构建操作，其他被其管理的项目也会执行相同的构建操作。那么接下来，我们再来分析下，多模块开发存在的另外一个问题，`重复配置`的问题，我们先来看张图:

![1630860344968](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Maven高级笔记/assets/1630860344968.png)

* `spring-webmvc`、`spring-jdbc`在三个项目模块中都有出现，这样就出现了重复的内容
* `spring-test`只在ssm_crm和ssm_goods中出现，而在ssm_order中没有，这里是部分重复的内容
* 我们使用的spring版本目前是`5.2.10.RELEASE`,假如后期要想升级spring版本，所有跟Spring相关jar包都得被修改，涉及到的项目越多，维护成本越高

面对上面的这些问题，我们就得用到接下来要学习的==继承==

* 所谓继承:描述的是两个工程间的关系，与java中的继承相似，子工程可以继承父工程中的配置信息，常见于依赖关系的继承。
* 作用：
  - 简化配置
  - 减少版本冲突

接下来，我们到程序中去看看继承该如何实现?

#### 步骤1:创建一个空的Maven项目并将其打包方式设置为pom

因为这一步和前面maven创建聚合工程的方式是一摸一样，所以我们可以单独创建一个新的工程，也可以直接和聚合公用一个工程。实际开发中，聚合和继承一般也都放在同一个项目中，但是这两个的功能是不一样的。

#### 步骤2:在子项目中设置其父工程

分别在`maven_02_ssm`,`maven_03_pojo`,`maven_04_dao`的pom.xml中添加其父项目为`maven_01_parent`

```xml
<!--配置当前工程继承自parent工程-->
<parent>
    <groupId>com.itheima</groupId>
    <artifactId>maven_01_parent</artifactId>
    <version>1.0-RELEASE</version>
    <!--设置父项目pom.xml位置路径-->
    <relativePath>../maven_01_parent/pom.xml</relativePath>
</parent>
```

#### 步骤3:优化子项目共有依赖导入问题

1. 将子项目共同使用的jar包都抽取出来，维护在父项目的pom.xml中

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.itheima</groupId>
    <artifactId>maven_01_parent</artifactId>
    <version>1.0-RELEASE</version>
    <packaging>pom</packaging>
    
    <!--设置管理的模块名称-->
    <modules>
        <module>../maven_02_ssm</module>
        <module>../maven_03_pojo</module>
        <module>../maven_04_dao</module>
    </modules>
    <dependencies>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-core</artifactId>
            <version>5.2.10.RELEASE</version>
        </dependency>

        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-webmvc</artifactId>
            <version>5.2.10.RELEASE</version>
        </dependency>

        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-jdbc</artifactId>
            <version>5.2.10.RELEASE</version>
        </dependency>

        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-test</artifactId>
            <version>5.2.10.RELEASE</version>
        </dependency>

        <dependency>
            <groupId>org.mybatis</groupId>
            <artifactId>mybatis</artifactId>
            <version>3.5.6</version>
        </dependency>

        <dependency>
            <groupId>org.mybatis</groupId>
            <artifactId>mybatis-spring</artifactId>
            <version>1.3.0</version>
        </dependency>

        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>5.1.47</version>
        </dependency>

        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>druid</artifactId>
            <version>1.1.16</version>
        </dependency>

        <dependency>
            <groupId>javax.servlet</groupId>
            <artifactId>javax.servlet-api</artifactId>
            <version>3.1.0</version>
            <scope>provided</scope>
        </dependency>

        <dependency>
            <groupId>com.fasterxml.jackson.core</groupId>
            <artifactId>jackson-databind</artifactId>
            <version>2.9.0</version>
        </dependency>
    </dependencies>
</project>
```

2. 删除子项目中已经被抽取到父项目的pom.xml中的jar包，如在`maven_02_ssm`的pom.xml中将已经出现在父项目的jar包删除掉

```xml
<?xml version="1.0" encoding="UTF-8"?>

<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <groupId>com.itheima</groupId>
  <artifactId>maven_02_ssm</artifactId>
  <version>1.0-SNAPSHOT</version>
  <packaging>war</packaging>

  <!--配置当前工程继承自parent工程-->
  <parent>
    <groupId>com.itheima</groupId>
    <artifactId>maven_01_parent</artifactId>
    <version>1.0-RELEASE</version>
    <relativePath>../maven_01_parent/pom.xml</relativePath>
  </parent>
  <dependencies>
    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>4.12</version>
      <scope>test</scope>
    </dependency>

    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>4.11</version>
      <scope>test</scope>
    </dependency>

    <dependency>
      <groupId>com.itheima</groupId>
      <artifactId>maven_04_dao</artifactId>
      <version>1.0-SNAPSHOT</version>
      <!--排除依赖是隐藏当前资源对应的依赖关系-->
      <exclusions>
        <exclusion>
          <groupId>log4j</groupId>
          <artifactId>log4j</artifactId>
        </exclusion>
        <exclusion>
          <groupId>org.mybatis</groupId>
          <artifactId>mybatis</artifactId>
        </exclusion>
      </exclusions>
    </dependency>

  </dependencies>

  <build>
    <plugins>
      <plugin>
        <groupId>org.apache.tomcat.maven</groupId>
        <artifactId>tomcat7-maven-plugin</artifactId>
        <version>2.1</version>
        <configuration>
          <port>80</port>
          <path>/</path>
        </configuration>
      </plugin>
    </plugins>
  </build>
</project>


```

删除完后，你会发现父项目中有依赖对应的jar包，子项目虽然已经将重复的依赖删除掉了，但是刷新的时候，子项目中所需要的jar包依然存在。

当项目的`<parent>`标签被移除掉，会发现多出来的jar包依赖也会随之消失。

3. 将`maven_04_dao`项目的pom.xml中的所有依赖删除，然后添加上`maven_01_parent`的父项目坐标

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.itheima</groupId>
    <artifactId>maven_04_dao</artifactId>
    <version>1.0-SNAPSHOT</version>

    <!--配置当前工程继承自parent工程-->
    <parent>
        <groupId>com.itheima</groupId>
        <artifactId>maven_01_parent</artifactId>
        <version>1.0-RELEASE</version>
        <relativePath>../maven_01_parent/pom.xml</relativePath>
    </parent>
</project>
```

刷新并查看Maven的面板，会发现maven_04_dao同样引入了父项目中的所有依赖。

![1630862406709](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Maven高级笔记/assets/1630862406709.png)

这样我们就可以解决刚才提到的第一个问题，将子项目中的公共jar包抽取到父工程中进行统一添加依赖，这样做的可以简化配置，并且当父工程中所依赖的jar包版本发生变化，所有子项目中对应的jar包版本也会跟着更新。

![1630943390187](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Maven高级笔记/assets/1630943390187.png)

#### 步骤4:优化子项目依赖版本问题

如果把所有用到的jar包都管理在父项目的pom.xml，看上去更简单些，但是这样就会导致有很多项目引入了过多自己不需要的jar包。如上面看到的这张图:

![](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Maven高级笔记/assets/1630860344968.png)

如果把所有的依赖都放在了父工程中进行统一维护，就会导致ssm_order项目中多引入了`spring-test`的jar包，如果这样的jar包过多的话，对于ssm_order来说也是一种"负担"。

那针对于这种部分项目有的jar包，我们该如何管理优化呢?

1. 在父工程mavne_01_parent的pom.xml来定义依赖管理

```xml
<!--定义依赖管理-->
<dependencyManagement>
    <dependencies>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.12</version>
            <scope>test</scope>
        </dependency>
    </dependencies>
</dependencyManagement>
```

2. 将maven_02_ssm的pom.xml中的junit依赖删除掉，刷新Maven

![1630944335419](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Maven高级笔记/assets/1630944335419.png)

刷新完会发现，在maven_02_ssm项目中的junit依赖并没有出现，所以我们得到一个结论:

==`<dependencyManagement>`标签不真正引入jar包，而是配置可供子项目选择的jar包依赖==

子项目要想使用它所提供的这些jar包，需要自己添加依赖，并且不需要指定`<version>`

3. 在maven_02_ssm的pom.xml添加junit的依赖

```xml
<dependency>
    <groupId>junit</groupId>
    <artifactId>junit</artifactId>
    <scope>test</scope>
</dependency>
```

**注意：这里就不需要添加版本了，这样做的好处就是当父工程dependencyManagement标签中的版本发生变化后，子项目中的依赖版本也会跟着发生变化**

4. 在maven_04_dao的pom.xml添加junit的依赖

```xml
<dependency>
    <groupId>junit</groupId>
    <artifactId>junit</artifactId>
    <scope>test</scope>
</dependency>
```

这个时候，maven_02_ssm和maven_04_dao这两个项目中的junit版本就会跟随着父项目中的标签dependencyManagement中junit的版本发生变化而变化。不需要junit的项目就不需要添加对应的依赖即可。

至此继承就已经学习完了，总结来说，继承可以帮助做两件事

* 将所有项目公共的jar包依赖提取到父工程的pom.xml中，子项目就可以不用重复编写，简化开发
* 将所有项目的jar包配置到父工程的dependencyManagement标签下，实现版本管理，方便维护
  * ==dependencyManagement标签不真正引入jar包，只是管理jar包的版本==
  * 子项目在引入的时候，只需要指定groupId和artifactId，不需要加version
  * 当dependencyManagement标签中jar包版本发生变化，所有子项目中有用到该jar包的地方对应的版本会自动随之更新

最后总结一句话就是，**父工程主要是用来快速配置依赖jar包和管理项目中所使用的资源**。

**小结**

继承的实现步骤:

* 创建Maven模块，设置打包类型为pom

  ```xml
  <packaging>pom</packaging>
  ```

* 在父工程的pom文件中配置依赖关系(子工程将沿用父工程中的依赖关系),一般只抽取子项目中公有的jar包

  ```xml
  <dependencies>
      <dependency>
          <groupId>org.springframework</groupId>
          <artifactId>spring-webmvc</artifactId>
          <version>5.2.10.RELEASE</version>
      </dependency>
      ...
  </dependencies>
  ```

* 在父工程中配置子工程中可选的依赖关系

  ```xml
  <dependencyManagement>
      <dependencies>
          <dependency>
              <groupId>com.alibaba</groupId>
              <artifactId>druid</artifactId>
              <version>1.1.16</version>
          </dependency>
      </dependencies>
      ...
  </dependencyManagement>
  ```

* 在子工程中配置当前工程所继承的父工程

  ```xml
  <!--定义该工程的父工程-->
  <parent>
      <groupId>com.itheima</groupId>
      <artifactId>maven_01_parent</artifactId>
      <version>1.0-RELEASE</version>
      <!--填写父工程的pom文件,可以不写-->
      <relativePath>../maven_01_parent/pom.xml</relativePath>
  </parent>
  ```

* 在子工程中配置使用父工程中可选依赖的坐标

  ```xml
  <dependencies>
      <dependency>
          <groupId>com.alibaba</groupId>
          <artifactId>druid</artifactId>
      </dependency>
  </dependencies>
  ```

  注意事项:

  1.子工程中使用父工程中的可选依赖时，仅需要提供群组id和项目id，无需提供版本，版本由父工程统一提供，避免版本冲突

  2.子工程中还可以定义父工程中没有定义的依赖关系,只不过不能被父工程进行版本统一管理。

### 3.3 聚合与继承的区别

#### 3.3.1 聚合与继承的区别

两种之间的作用:

* 聚合用于快速构建项目，对项目进行管理
* 继承用于快速配置和管理子项目中所使用jar包的版本

聚合和继承的相同点:

* 聚合与继承的pom.xml文件打包方式均为pom，可以将两种关系制作到同一个pom文件中
* 聚合与继承均属于设计型模块，并无实际的模块内容

聚合和继承的不同点:

* 聚合是在当前模块中配置关系，聚合可以感知到参与聚合的模块有哪些
* 继承是在子模块中配置关系，父模块无法感知哪些子模块继承了自己

相信到这里，大家已经能区分开什么是聚合和继承，但是有一个稍微麻烦的地方就是聚合和继承的工程构建，需要在聚合项目中手动添加`modules`标签，需要在所有的子项目中添加`parent`标签，万一写错了咋办?

#### 3.3.2 IDEA构建聚合与继承工程

其实对于聚合和继承工程的创建，IDEA已经能帮助我们快速构建，具体的实现步骤为:

##### 步骤1:创建一个Maven项目

创建一个空的Maven项目，可以将项目中的`src`目录删除掉，这个项目作为聚合工程和父工程。

![1630946592924](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Maven高级笔记/assets/1630946592924.png)

##### 步骤2:创建子项目

该项目可以被聚合工程管理，同时会继承父工程。

![1630947082716](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Maven高级笔记/assets/1630947082716.png)

创建成功后，maven_parent即是聚合工程又是父工程，maven_web中也有parent标签，继承的就是maven_parent,对于难以配置的内容都自动生成。

按照上面这种方式，大家就可以根据自己的需要来构建分模块项目。

## 4，属性

在这一章节内容中，我们将学习两个内容，分别是

* 属性
* 版本管理

属性中会继续解决分模块开发项目存在的问题，版本管理主要是认识下当前主流的版本定义方式。

### 4.1 属性

#### 4.1.1 问题分析

讲解内容之前，我们还是先来分析问题:

前面我们已经在父工程中的dependencyManagement标签中对项目中所使用的jar包版本进行了统一的管理，但是如果在标签中有如下的内容:

![1630947403475](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Maven高级笔记/assets/1630947403475.png)

你会发现，如果我们现在想更新Spring的版本，你会发现我们依然需要更新多个jar包的版本，这样的话还是有可能出现漏改导致程序出问题，而且改起来也是比较麻烦。

问题清楚后，我们需要解决的话，就可以参考咱们java基础所学习的变量，声明一个变量，在其他地方使用该变量，当变量的值发生变化后，所有使用变量的地方，就会跟着修改，即:

![1630947749661](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Maven高级笔记/assets/1630947749661.png)

#### 4.1.2 解决步骤

##### 步骤1:父工程中定义属性

```xml
<properties>
    <spring.version>5.2.10.RELEASE</spring.version>
    <junit.version>4.12</junit.version>
    <mybatis-spring.version>1.3.0</mybatis-spring.version>
</properties>
```

##### 步骤2:修改依赖的version

```xml
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-core</artifactId>
    <version>${spring.version}</version>
</dependency>
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-webmvc</artifactId>
    <version>${spring.version}</version>
</dependency>
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-jdbc</artifactId>
    <version>${spring.version}</version>
</dependency>
```

此时，我们只需要更新父工程中properties标签中所维护的jar包版本，所有子项目中的版本也就跟着更新。当然除了将spring相关版本进行维护，我们可以将其他的jar包版本也进行抽取，这样就可以对项目中所有jar包的版本进行统一维护，如:

```xml
<!--定义属性-->
<properties>
    <spring.version>5.2.10.RELEASE</spring.version>
    <junit.version>4.12</junit.version>
    <mybatis-spring.version>1.3.0</mybatis-spring.version>
</properties>
```

### 4.2 配置文件加载属性

Maven中的属性我们已经介绍过了，现在也已经能够通过Maven来集中管理Maven中依赖jar包的版本。但是又有新的需求，就是想让Maven对于属性的管理范围能更大些，比如我们之前项目中的`jdbc.properties`，这个配置文件中的属性，能不能也来让Maven进行管理呢?

答案是肯定的，具体的实现步骤为:

##### 步骤1:父工程定义属性

```xml
<properties>
   <jdbc.url>jdbc:mysql://127.1.1.1:3306/ssm_db</jdbc.url>
</properties>
```

##### 步骤2:jdbc.properties文件中引用属性

在jdbc.properties，将jdbc.url的值直接获取Maven配置的属性

```properties
jdbc.driver=com.mysql.jdbc.Driver
jdbc.url=${jdbc.url}
jdbc.username=root
jdbc.password=root
```

##### 步骤3:设置maven过滤文件范围

Maven在默认情况下是从当前项目的`src\main\resources`下读取文件进行打包。现在我们需要打包的资源文件是在maven_02_ssm下,需要我们通过配置来指定下具体的资源目录。

```xml
<build>
    <resources>
        <!--设置资源目录-->
        <resource>
            <directory>../maven_02_ssm/src/main/resources</directory>
            <!--设置能够解析${}，默认是false -->
            <filtering>true</filtering>
        </resource>
    </resources>
</build>
```

**说明:**directory路径前要添加`../`的原因是maven_02_ssm相对于父工程的pom.xml路径是在其上一层的目录中，所以需要添加。

修改完后，注意maven_02_ssm项目的resources目录就多了些东西，如下:

![1630977419627](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Maven高级笔记/assets/1630977419627.png)



##### 步骤4:测试是否生效

测试的时候，只需要将maven_02_ssm项目进行打包，然后观察打包结果中最终生成的内容是否为Maven中配置的内容。

![1630977885030](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Maven高级笔记/assets/1630977885030.png)

上面的属性管理就已经完成，但是有一个问题没有解决，因为不只是maven_02_ssm项目需要有属性被父工程管理，如果有多个项目需要配置，该如何实现呢?

方式一:

```xml
<build>
    <resources>
        <!--设置资源目录，并设置能够解析${}-->
        <resource>
            <directory>../maven_02_ssm/src/main/resources</directory>
            <filtering>true</filtering>
        </resource>
        <resource>
            <directory>../maven_03_pojo/src/main/resources</directory>
            <filtering>true</filtering>
        </resource>
        ...
    </resources>
</build>
```

可以配，但是如果项目够多的话，这个配置也是比较繁琐

方式二:

```xml
<build>
    <resources>
        <!--
			${project.basedir}: 当前项目所在目录,子项目继承了父项目，
			相当于所有的子项目都添加了资源目录的过滤
		-->
        <resource>
            <directory>${project.basedir}/src/main/resources</directory>
            <filtering>true</filtering>
        </resource>
    </resources>
</build>
```

**说明:**打包的过程中如果报如下错误:

![1630948929828](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Maven高级笔记/assets/1630948929828.png)

原因就是Maven发现你的项目为web项目，就会去找web项目的入口web.xml[配置文件配置的方式]，发现没有找到，就会报错。

解决方案1：在maven_02_ssm项目的`src\main\webapp\WEB-INF\`添加一个web.xml文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_3_1.xsd"
         version="3.1">
</web-app>
```

解决方案2: 配置maven打包war时，忽略web.xml检查

```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-war-plugin</artifactId>
            <version>3.2.3</version>
            <configuration>
                <failOnMissingWebXml>false</failOnMissingWebXml>
            </configuration>
        </plugin>
    </plugins>
</build>
```

上面我们所使用的都是Maven的自定义属性，除了${project.basedir},它属于Maven的内置系统属性。

在Maven中的属性分为:

- 自定义属性（常用）
- 内置属性
- Setting属性
- Java系统属性
- 环境变量属性

![1630981519370](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Maven高级笔记/assets/1630981519370.png)

具体如何查看这些属性:

在cmd命令行中输入`mvn help:system`

![1630981585748](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Maven高级笔记/assets/1630981585748.png)

具体使用，就是使用 `${key}`来获取，key为等号左边的，值为等号右边的，比如获取红线的值，对应的写法为 `${java.runtime.name}`。

### 4.3 版本管理

关于这个版本管理解决的问题是，在Maven创建项目和引用别人项目的时候，我们都看到过如下内容:

![1630982018031](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Maven高级笔记/assets/1630982018031.png)

这里面有两个单词，SNAPSHOT和RELEASE，它们所代表的含义是什么呢?

我们打开Maven仓库地址`https://mvnrepository.com/`

![1630983148662](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Maven高级笔记/assets/1630983148662.png)

在我们jar包的版本定义中，有两个工程版本用的比较多:

- SNAPSHOT（快照版本）
  - 项目开发过程中临时输出的版本，称为快照版本
  - 快照版本会随着开发的进展不断更新
- RELEASE（发布版本）
  - 项目开发到一定阶段里程碑后，向团队外部发布较为稳定的版本，这种版本所对应的构件文件是稳定的
  - 即便进行功能的后续开发，也不会改变当前发布版本内容，这种版本称为发布版本

除了上面的工程版本，我们还经常能看到一些发布版本:

* alpha版:内测版，bug多不稳定内部版本不断添加新功能
* beta版:公测版，不稳定(比alpha稳定些)，bug相对较多不断添加新功能
* 纯数字版

对于这些版本，大家只需要简单认识下即可。

## 5，多环境配置与应用

这一节中，我们会讲两个内容，分别是`多环境开发`和`跳过测试`

### 5.1 多环境开发

![1630983617755](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Maven高级笔记/assets/1630983617755.png)

* 我们平常都是在自己的开发环境进行开发，
* 当开发完成后，需要把开发的功能部署到测试环境供测试人员进行测试使用，
* 等测试人员测试通过后，我们会将项目部署到生成环境上线使用。
* 这个时候就有一个问题是，不同环境的配置是不相同的，如不可能让三个环境都用一个数据库，所以就会有三个数据库的url配置，
* 我们在项目中如何配置?
* 要想实现不同环境之间的配置切换又该如何来实现呢?

maven提供配置多种环境的设定，帮助开发者在使用过程中快速切换环境。具体实现步骤:

#### 步骤1:父工程配置多个环境,并指定默认激活环境

```xml
<profiles>
    <!--开发环境-->
    <profile>
        <id>env_dep</id>
        <properties>
            <jdbc.url>jdbc:mysql://127.1.1.1:3306/ssm_db</jdbc.url>
        </properties>
        <!--设定是否为默认启动环境-->
        <activation>
            <activeByDefault>true</activeByDefault>
        </activation>
    </profile>
    <!--生产环境-->
    <profile>
        <id>env_pro</id>
        <properties>
            <jdbc.url>jdbc:mysql://127.2.2.2:3306/ssm_db</jdbc.url>
        </properties>
    </profile>
    <!--测试环境-->
    <profile>
        <id>env_test</id>
        <properties>
            <jdbc.url>jdbc:mysql://127.3.3.3:3306/ssm_db</jdbc.url>
        </properties>
    </profile>
</profiles>
```

#### 步骤2:执行安装查看env_dep环境是否生效

![1630983967960](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Maven高级笔记/assets/1630983967960.png)

查看到的结果为:

![](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Maven高级笔记/assets/1630977885030.png)

#### 步骤3:切换默认环境为生产环境

```xml
<profiles>
    <!--开发环境-->
    <profile>
        <id>env_dep</id>
        <properties>
            <jdbc.url>jdbc:mysql://127.1.1.1:3306/ssm_db</jdbc.url>
        </properties>
    </profile>
    <!--生产环境-->
    <profile>
        <id>env_pro</id>
        <properties>
            <jdbc.url>jdbc:mysql://127.2.2.2:3306/ssm_db</jdbc.url>
        </properties>
        <!--设定是否为默认启动环境-->
        <activation>
            <activeByDefault>true</activeByDefault>
        </activation>
    </profile>
    <!--测试环境-->
    <profile>
        <id>env_test</id>
        <properties>
            <jdbc.url>jdbc:mysql://127.3.3.3:3306/ssm_db</jdbc.url>
        </properties>
    </profile>
</profiles>
```

#### 步骤4:执行安装并查看env_pro环境是否生效

查看到的结果为`jdbc:mysql://127.2.2.2:3306/ssm_db`

![](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Maven高级笔记/assets/1630977885031.png)

虽然已经能够实现不同环境的切换，但是每次切换都是需要手动修改，如何来实现在不改变代码的前提下完成环境的切换呢?

#### 步骤5:命令行实现环境切换

![1630984476202](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Maven高级笔记/assets/1630984476202.png)

#### 步骤6:执行安装并查看env_test环境是否生效

查看到的结果为`jdbc:mysql://127.3.3.3:3306/ssm_db`

![](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Maven高级笔记/assets/1630977885032.png)

所以总结来说，对于多环境切换只需要两步即可:

* 父工程中定义多环境

  ```xml
  <profiles>
  	<profile>
      	<id>环境名称</id>
          <properties>
          	<key>value</key>
          </properties>
          <activation>
          	<activeByDefault>true</activeByDefault>
          </activation>
      </profile>
      ...
  </profiles>
  ```

* 使用多环境(构建过程)

  ```
  mvn 指令 -P 环境定义ID[环境定义中获取]
  ```

### 5.2 跳过测试

前面在执行`install`指令的时候，Maven都会按照顺序从上往下依次执行，每次都会执行`test`,

对于`test`来说有它存在的意义，

* 可以确保每次打包或者安装的时候，程序的正确性，假如测试已经通过在我们没有修改程序的前提下再次执行打包或安装命令，由于顺序执行，测试会被再次执行，就有点耗费时间了。
* 功能开发过程中有部分模块还没有开发完毕，测试无法通过，但是想要把其中某一部分进行快速打包，此时由于测试环境失败就会导致打包失败。

遇到上面这些情况的时候，我们就想跳过测试执行下面的构建命令，具体实现方式有很多：

#### 方式一:IDEA工具实现跳过测试

![1630985300814](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Maven高级笔记/assets/1630985300814.png)

图中的按钮为`Toggle 'Skip Tests' Mode`,

Toggle翻译为切换的意思，也就是说在测试与不测试之间进行切换。

点击一下，出现测试画横线的图片，如下:

![1630985411766](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Maven高级笔记/assets/1630985411766.png)

说明测试已经被关闭，再次点击就会恢复。

这种方式最简单，但是有点"暴力"，会把所有的测试都跳过，如果我们想更精细的控制哪些跳过哪些不跳过，就需要使用配置插件的方式。

#### 方式二:配置插件实现跳过测试

在父工程中的pom.xml中添加测试插件配置

```xml
<build>
    <plugins>
        <plugin>
            <artifactId>maven-surefire-plugin</artifactId>
            <version>2.12.4</version>
            <configuration>
                <skipTests>false</skipTests>
                <!--排除掉不参与测试的内容-->
                <excludes>
                    <exclude>**/BookServiceTest.java</exclude>
                </excludes>
            </configuration>
        </plugin>
    </plugins>
</build>
```

skipTests:如果为true，则跳过所有测试，如果为false，则不跳过测试

excludes：哪些测试类不参与测试，即排除，针对skipTests为false来设置的

includes: 哪些测试类要参与测试，即包含,针对skipTests为true来设置的

#### 方式三:命令行跳过测试

![1630986926124](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Maven高级笔记/assets/1630986926124.png)

使用Maven的命令行，`mvn 指令 -D skipTests`

注意事项:

* 执行的项目构建指令必须包含测试生命周期，否则无效果。例如执行compile生命周期，不经过test生命周期。
* 该命令可以不借助IDEA，直接使用cmd命令行进行跳过测试，需要注意的是cmd要在pom.xml所在目录下进行执行。

## 6，私服

这一节，我们主要学习的内容是:

* 私服简介
* 私服仓库分类
* 资源上传与下载

首先来说一说什么是私服?

### 6.1 私服简介

团队开发现状分析

![1630987192620](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Maven高级笔记/assets/1630987192620.png)

(1)张三负责ssm_crm的开发，自己写了一个ssm_pojo模块，要想使用直接将ssm_pojo安装到本地仓库即可

(2)李四负责ssm_order的开发，需要用到张三所写的ssm_pojo模块，这个时候如何将张三写的ssm_pojo模块交给李四呢?

(3)如果直接拷贝，那么团队之间的jar包管理会非常混乱而且容器出错，这个时候我们就想能不能将写好的项目上传到中央仓库，谁想用就直接联网下载即可

(4)Maven的中央仓库不允许私人上传自己的jar包,那么我们就得换种思路，自己搭建一个类似于中央仓库的东西，把自己的内容上传上去，其他人就可以从上面下载jar包使用

(5)这个类似于中央仓库的东西就是我们接下来要学习的==私服==

所以到这就有两个概念，一个是私服，一个是中央仓库

私服:公司内部搭建的用于存储Maven资源的服务器

远程仓库:Maven开发团队维护的用于存储Maven资源的服务器

所以说:

* 私服是一台独立的服务器，用于解决团队内部的资源共享与资源同步问题

搭建Maven私服的方式有很多，我们来介绍其中一种使用量比较大的实现方式:

* Nexus
  * Sonatype公司的一款maven私服产品
  * 下载地址：https://help.sonatype.com/repomanager3/download

### 6.2 私服安装

#### 步骤1:下载解压

将`资料\latest-win64.zip`解压到一个空目录下。

![1630988572349](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Maven高级笔记/assets/1630988572349.png)

#### 步骤2:启动Nexus

![1630988673245](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Maven高级笔记/assets/1630988673245.png)

使用cmd进入到解压目录下的`nexus-3.30.1-01\bin`,执行如下命令:

```
nexus.exe /run nexus
```

看到如下内容，说明启动成功。

![1630988939301](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Maven高级笔记/assets/1630988939301.png)

#### 步骤3:浏览器访问

访问地址为:

```
http://localhost:8081
```

![1630988857125](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Maven高级笔记/assets/1630988857125.png)

#### 步骤4:首次登录重置密码

![1630988983159](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Maven高级笔记/assets/1630988983159.png)

输入用户名和密码进行登录，登录成功后，出现如下页面

![1630989052183](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Maven高级笔记/assets/1630989052183.png)

点击下一步，需要重新输入新密码，为了和后面的保持一致，密码修改为`admin`

![1630989094756](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Maven高级笔记/assets/1630989094756.png)

设置是否运行匿名访问

![1630989122737](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Maven高级笔记/assets/1630989122737.png)

点击完成

![1630989136097](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Maven高级笔记/assets/1630989136097.png)

至此私服就已经安装成功。如果要想修改一些基础配置信息，可以使用:

- 修改基础配置信息
  - 安装路径下etc目录中nexus-default.properties文件保存有nexus基础配置信息，例如默认访问端口。
- 修改服务器运行配置信息
  - 安装路径下bin目录中nexus.vmoptions文件保存有nexus服务器启动对应的配置信息，例如默认占用内存空间。

### 6.3 私服仓库分类

私服资源操作流程分析:

![1630989320979](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Maven高级笔记/assets/1630989320979.png)

(1)在没有私服的情况下，我们自己创建的服务都是安装在Maven的本地仓库中

(2)私服中也有仓库，我们要把自己的资源上传到私服，最终也是放在私服的仓库中

(3)其他人要想使用你所上传的资源，就需要从私服的仓库中获取

(4)当我们要使用的资源不是自己写的，是远程中央仓库有的第三方jar包，这个时候就需要从远程中央仓库下载，每个开发者都去远程中央仓库下速度比较慢(中央仓库服务器在国外)

(5)私服就再准备一个仓库，用来专门存储从远程中央仓库下载的第三方jar包，第一次访问没有就会去远程中央仓库下载，下次再访问就直接走私服下载

(6)前面在介绍版本管理的时候提到过有`SNAPSHOT`和`RELEASE`，如果把这两类的都放到同一个仓库，比较混乱，所以私服就把这两个种jar包放入不同的仓库

(7)上面我们已经介绍了有三种仓库，一种是存放`SNAPSHOT`的，一种是存放`RELEASE`还有一种是存放从远程仓库下载的第三方jar包，那么我们在获取资源的时候要从哪个仓库种获取呢?

(8)为了方便获取，我们将所有的仓库编成一个组，我们只需要访问仓库组去获取资源。

所有私服仓库总共分为三大类:

宿主仓库hosted 

- 保存无法从中央仓库获取的资源
  - 自主研发
  - 第三方非开源项目,比如Oracle,因为是付费产品，所以中央仓库没有

代理仓库proxy 

- 代理远程仓库，通过nexus访问其他公共仓库，例如中央仓库

仓库组group 

- 将若干个仓库组成一个群组，简化配置
- 仓库组不能保存资源，属于设计型仓库

![1630990244010](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Maven高级笔记/assets/1630990244010.png)

### 6.4 本地仓库访问私服配置

* 我们通过IDEA将开发的模块上传到私服，中间是要经过本地Maven的
* 本地Maven需要知道私服的访问地址以及私服访问的用户名和密码
* 私服中的仓库很多，Maven最终要把资源上传到哪个仓库?
* Maven下载的时候，又需要携带用户名和密码到私服上找对应的仓库组进行下载，然后再给IDEA

![1630990538229](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Maven高级笔记/assets/1630990538229.png)

上面所说的这些内容，我们需要在本地Maven的配置文件`settings.xml`中进行配置。

#### 步骤1:私服上配置仓库

![1630991211000](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Maven高级笔记/assets/1630991211000.png)

**说明:**

第5，6步骤是创建itheima-snapshot仓库

第7，8步骤是创建itheima-release仓库

#### 步骤2:配置本地Maven对私服的访问权限

```xml
<servers>
    <server>
        <id>itheima-snapshot</id>
        <username>admin</username>
        <password>admin</password>
    </server>
    <server>
        <id>itheima-release</id>
        <username>admin</username>
        <password>admin</password>
    </server>
</servers>
```

#### 步骤3:配置私服的访问路径

```xml
<mirrors>
    <mirror>
        <!--配置仓库组的ID-->
        <id>maven-public</id>
        <!--*代表所有内容都从私服获取-->
        <mirrorOf>*</mirrorOf>
        <!--私服仓库组maven-public的访问路径-->
        <url>http://localhost:8081/repository/maven-public/</url>
    </mirror>
</mirrors>
```

为了避免阿里云Maven私服地址的影响，建议先将之前配置的阿里云Maven私服镜像地址注释掉，等练习完后，再将其恢复。

![1630991535107](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Maven高级笔记/assets/1630991535107.png)

至此本地仓库就能与私服进行交互了。

### 6.5 私服资源上传与下载

本地仓库与私服已经建立了连接，接下来我们就需要往私服上上传资源和下载资源，具体的实现步骤为:

#### 步骤1:配置工程上传私服的具体位置

```xml
 <!--配置当前工程保存在私服中的具体位置-->
<distributionManagement>
    <repository>
        <!--和maven/settings.xml中server中的id一致，表示使用该id对应的用户名和密码-->
        <id>itheima-release</id>
         <!--release版本上传仓库的具体地址-->
        <url>http://localhost:8081/repository/itheima-release/</url>
    </repository>
    <snapshotRepository>
        <!--和maven/settings.xml中server中的id一致，表示使用该id对应的用户名和密码-->
        <id>itheima-snapshot</id>
        <!--snapshot版本上传仓库的具体地址-->
        <url>http://localhost:8081/repository/itheima-snapshot/</url>
    </snapshotRepository>
</distributionManagement>
```

#### 步骤2:发布资源到私服

![1630992305191](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Maven高级笔记/assets/1630992305191.png)

或者执行Maven命令

```
mvn deploy
```

**注意:**

要发布的项目都需要配置`distributionManagement`标签，要么在自己的pom.xml中配置，要么在其父项目中配置，然后子项目中继承父项目即可。

发布成功，在私服中就能看到:

![1630992513299](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Maven高级笔记/assets/1630992513299.png)

现在发布是在itheima-snapshot仓库中，如果想发布到itheima-release仓库中就需要将项目pom.xml中的version修改成RELEASE即可。

如果想删除已经上传的资源，可以在界面上进行删除操作:

![1630992952378](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Maven高级笔记/assets/1630992952378.png)

如果私服中没有对应的jar，会去中央仓库下载，速度很慢。可以配置让私服去阿里云中下载依赖。

![1630993028454](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Maven高级笔记/assets/1630993028454.png)

至此私服的搭建就已经完成，相对来说有点麻烦，但是步骤都比较固定，后期大家如果需要的话，就可以参考上面的步骤一步步完成搭建即可。



# MyBatisPlus

**今日目标**

> 基于MyBatisPlus完成标准Dao的增删改查功能
>
> 掌握MyBatisPlus中的分页及条件查询构建
>
> 掌握主键ID的生成策略
>
> 了解MyBatisPlus的代码生成器

## 1，MyBatisPlus入门案例与简介

这一节我们来学习下MyBatisPlus的入门案例与简介，这个和其他课程都不太一样，其他的课程都是先介绍概念，然后再写入门案例。而对于MyBatisPlus的学习，我们将顺序做了调整，主要的原因MyBatisPlus主要是对MyBatis的简化，所有我们先体会下它简化在哪，然后再学习它是什么，以及它帮我们都做哪些事。

### 1.1 入门案例

* MybatisPlus(简称MP)是基于MyBatis框架基础上开发的增强型工具，旨在简化开发、提供效率。

* 开发方式
  * 基于MyBatis使用MyBatisPlus
  * 基于Spring使用MyBatisPlus
  * ==基于SpringBoot使用MyBatisPlus==

SpringBoot刚刚我们学习完成，它能快速构建Spring开发环境用以整合其他技术，使用起来是非常简单，对于MP的学习，我们也基于SpringBoot来构建学习。

学习之前，我们先来回顾下，SpringBoot整合Mybatis的开发过程:

* 创建SpringBoot工程

  ![1630997819698](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Mybatisplus笔记/assets/1630997819698.png)

* 勾选配置使用的技术，能够实现自动添加起步依赖包

  ![1630997860020](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Mybatisplus笔记/assets/1630997860020.png)

* 设置dataSource相关属性(JDBC参数)

  ![1630997901479](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Mybatisplus笔记/assets/1630997901479.png)

* 定义数据层接口映射配置

  ![1630997929891](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Mybatisplus笔记/assets/1630997929891.png)

我们可以参考着上面的这个实现步骤把SpringBoot整合MyBatisPlus来快速实现下，具体的实现步骤为:

#### 步骤1:创建数据库及表

```sql
create database if not exists mybatisplus_db character set utf8;
use mybatisplus_db;
CREATE TABLE user (
    id bigint(20) primary key auto_increment,
    name varchar(32) not null,
    password  varchar(32) not null,
    age int(3) not null ,
    tel varchar(32) not null
);
insert into user values(1,'Tom','tom',3,'18866668888');
insert into user values(2,'Jerry','jerry',4,'16688886666');
insert into user values(3,'Jock','123456',41,'18812345678');
insert into user values(4,'传智播客','itcast',15,'4006184000');
```

#### 步骤2:创建SpringBoot工程

![1630998241426](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Mybatisplus笔记/assets/1630998241426.png)

#### 步骤3:勾选配置使用技术

![1630998321660](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Mybatisplus笔记/assets/1630998321660.png)

**说明:**

* 由于MP并未被收录到idea的系统内置配置，无法直接选择加入，需要手动在pom.xml中配置添加

#### 步骤4:pom.xml补全依赖

```xml
<dependency>
    <groupId>com.baomidou</groupId>
    <artifactId>mybatis-plus-boot-starter</artifactId>
    <version>3.4.1</version>
</dependency>
<dependency>
    <groupId>com.alibaba</groupId>
    <artifactId>druid</artifactId>
    <version>1.1.16</version>
</dependency>
```

**说明:**

* druid数据源可以加也可以不加，SpringBoot有内置的数据源，可以配置成使用Druid数据源

* 从MP的依赖关系可以看出，通过依赖传递已经将MyBatis与MyBatis整合Spring的jar包导入，我们不需要额外在添加MyBatis的相关jar包

  ![1631206757758](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Mybatisplus笔记/assets/1631206757758.png)

#### 步骤5:添加MP的相关配置信息

resources默认生成的是properties配置文件，可以将其替换成yml文件，并在文件中配置数据库连接的相关信息:`application.yml`

```yml
spring:
  datasource:
    type: com.alibaba.druid.pool.DruidDataSource
    driver-class-name: com.mysql.cj.jdbc.Driver
    url: jdbc:mysql://localhost:3306/mybatisplus_db?serverTimezone=UTC 
    username: root
    password: root
```

**说明:**==serverTimezone是用来设置时区，UTC是标准时区，和咱们的时间差8小时，所以可以将其修改为`Asia/Shanghai`==

#### 步骤6:根据数据库表创建实体类

```java
public class User {   
    private Long id;
    private String name;
    private String password;
    private Integer age;
    private String tel;
    //setter...getter...toString方法略
}
```

#### 步骤7:创建Dao接口

```java
@Mapper
public interface UserDao extends BaseMapper<User>{
}
```

#### 步骤8:编写引导类

```java
@SpringBootApplication
//@MapperScan("com.itheima.dao")
public class Mybatisplus01QuickstartApplication {
    public static void main(String[] args) {
        SpringApplication.run(Mybatisplus01QuickstartApplication.class, args);
    }

}
```

**说明:**Dao接口要想被容器扫描到，有两种解决方案:

* 方案一:在Dao接口上添加`@Mapper`注解，并且确保Dao处在引导类所在包或其子包中
  * 该方案的缺点是需要在每一Dao接口中添加注解
* 方案二:在引导类上添加`@MapperScan`注解，其属性为所要扫描的Dao所在包
  * 该方案的好处是只需要写一次，则指定包下的所有Dao接口都能被扫描到，`@Mapper`就可以不写。

#### 步骤9:编写测试类

```java
@SpringBootTest
class MpDemoApplicationTests {

	@Autowired
	private UserDao userDao;
	@Test
	public void testGetAll() {
		List<User> userList = userDao.selectList(null);
		System.out.println(userList);
	}
}
```

**说明:**

userDao注入的时候下面有红线提示的原因是什么?

* UserDao是一个接口，不能实例化对象

* 只有在服务器启动IOC容器初始化后，由框架创建DAO接口的代理对象来注入
* 现在服务器并未启动，所以代理对象也未创建，IDEA查找不到对应的对象注入，所以提示报红
* 一旦服务启动，就能注入其代理对象，所以该错误提示不影响正常运行。

查看运行结果:

![1630999646096](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Mybatisplus笔记/assets/1630999646096.png)

跟之前整合MyBatis相比，你会发现我们不需要在DAO接口中编写方法和SQL语句了，只需要继承`BaseMapper`接口即可。整体来说简化很多。

### 1.2 MybatisPlus简介

MyBatisPlus（简称MP）是基于MyBatis框架基础上开发的增强型工具，旨在==简化开发、提高效率==

通过刚才的案例，相信大家能够体会简化开发和提高效率这两个方面的优点。

MyBatisPlus的官网为:`https://mp.baomidou.com/`

**说明:**

![1631011942323](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Mybatisplus笔记/assets/1631011942323.png)

现在的页面中，这一行已经被删除，现在再去访问`https://mybatis.plus`会发现访问不到，这个就有很多可能性供我们猜想了，所以大家使用baomidou的网址进行访问即可。

官方文档中有一张很多小伙伴比较熟悉的图片:

![1631012174092](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Mybatisplus笔记/assets/1631012174092.png)

从这张图中我们可以看出MP旨在成为MyBatis的最好搭档，而不是替换MyBatis,所以可以理解为MP是MyBatis的一套增强工具，它是在MyBatis的基础上进行开发的，我们虽然使用MP但是底层依然是MyBatis的东西，也就是说我们也可以在MP中写MyBatis的内容。

对于MP的学习，大家可以参考着官方文档来进行学习，里面都有详细的代码案例。

MP的特性:

- 无侵入：只做增强不做改变，不会对现有工程产生影响
- 强大的 CRUD 操作：内置通用 Mapper，少量配置即可实现单表CRUD 操作
- 支持 Lambda：编写查询条件无需担心字段写错
- 支持主键自动生成
- 内置分页插件
- ……

## 2，标准数据层开发

在这一节中我们重点学习的是数据层标准的CRUD(增删改查)的实现与分页功能。代码比较多，我们一个个来学习。

### 2.1 标准CRUD使用

对于标准的CRUD功能都有哪些以及MP都提供了哪些方法可以使用呢?

我们先来看张图:

![1631018877517](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Mybatisplus笔记/assets/1631018877517.png)

对于这张图的方法，我们挨个来演示下:

首先说下，案例中的环境就是咱们入门案例的内容，第一个先来完成`新增`功能

### 2.2 新增

在进行新增之前，我们可以分析下新增的方法:

```java
int insert (T t)
```

* T:泛型，新增用来保存新增数据

* int:返回值，新增成功后返回1，没有新增成功返回的是0

在测试类中进行新增操作:

```java
@SpringBootTest
class Mybatisplus01QuickstartApplicationTests {

    @Autowired
    private UserDao userDao;

    @Test
    void testSave() {
        User user = new User();
        user.setName("黑马程序员");
        user.setPassword("itheima");
        user.setAge(12);
        user.setTel("4006184000");
        userDao.insert(user);
    }
}
```

执行测试后，数据库表中就会添加一条数据。

![1631013124310](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Mybatisplus笔记/assets/1631013124310.png)

但是数据中的主键ID，有点长，那这个主键ID是如何来的?我们更想要的是主键自增，应该是5才对，这个是我们后面要学习的主键ID生成策略，这块的这个问题，我们暂时先放放。

### 2.3 删除

在进行删除之前，我们可以分析下删除的方法:

```java
int deleteById (Serializable id)
```

* Serializable：参数类型

  * 思考:参数类型为什么是一个序列化类?

    ![1631013655771](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Mybatisplus笔记/assets/1631013655771.png)

    从这张图可以看出，

    * String和Number是Serializable的子类，
    * Number又是Float,Double,Integer等类的父类，
    * 能作为主键的数据类型都已经是Serializable的子类，
    * MP使用Serializable作为参数类型，就好比我们可以用Object接收任何数据类型一样。

* int:返回值类型，数据删除成功返回1，未删除数据返回0。

在测试类中进行新增操作:

```java
 @SpringBootTest
class Mybatisplus01QuickstartApplicationTests {

    @Autowired
    private UserDao userDao;

    @Test
    void testDelete() {
        userDao.deleteById(1401856123725713409L);
    }
}

```

### 2.4 修改

在进行修改之前，我们可以分析下修改的方法:

```java
int updateById(T t);
```

- T:泛型，需要修改的数据内容，注意因为是根据ID进行修改，所以传入的对象中需要有ID属性值

- int:返回值，修改成功后返回1，未修改数据返回0

在测试类中进行新增操作:

```java
@SpringBootTest
class Mybatisplus01QuickstartApplicationTests {

    @Autowired
    private UserDao userDao;

    @Test
    void testUpdate() {
        User user = new User();
        user.setId(1L);
        user.setName("Tom888");
        user.setPassword("tom888");
        userDao.updateById(user);
    }
}
```

**说明:**修改的时候，只修改实体对象中有值的字段。

### 2.5 根据ID查询

在进行根据ID查询之前，我们可以分析下根据ID查询的方法:

```java
T selectById (Serializable id)
```

- Serializable：参数类型,主键ID的值
- T:根据ID查询只会返回一条数据

在测试类中进行新增操作:

```java
@SpringBootTest
class Mybatisplus01QuickstartApplicationTests {

    @Autowired
    private UserDao userDao;
    
    @Test
    void testGetById() {
        User user = userDao.selectById(2L);
        System.out.println(user);
    }
}
```

### 2.6 查询所有

在进行查询所有之前，我们可以分析下查询所有的方法:

```java
List<T> selectList(Wrapper<T> queryWrapper)
```

- Wrapper：用来构建条件查询的条件，目前我们没有可直接传为Null
- List<T>:因为查询的是所有，所以返回的数据是一个集合

在测试类中进行新增操作:

```java
@SpringBootTest
class Mybatisplus01QuickstartApplicationTests {

    @Autowired
    private UserDao userDao;
    
    @Test
    void testGetAll() {
        List<User> userList = userDao.selectList(null);
        System.out.println(userList);
    }
}
```

我们所调用的方法都是来自于DAO接口继承的BaseMapper类中。里面的方法有很多，我们后面会慢慢去学习里面的内容。

### 2.7 Lombok

代码写到这，我们会发现DAO接口类的编写现在变成最简单的了，里面什么都不用写。反过来看看模型类的编写都需要哪些内容:

* 私有属性
* setter...getter...方法
* toString方法
* 构造函数

虽然这些内容不难，同时也都是通过IDEA工具生成的，但是过程还是必须得走一遍，那么对于模型类的编写有没有什么优化方法?就是我们接下来要学习的Lombok。

#### 概念

* Lombok，一个Java类库，提供了一组注解，简化POJO实体类开发。

#### 使用步骤

##### 步骤1:添加lombok依赖

```xml
<dependency>
    <groupId>org.projectlombok</groupId>
    <artifactId>lombok</artifactId>
    <!--<version>1.18.12</version>-->
</dependency>
```

**注意：**版本可以不用写，因为SpringBoot中已经管理了lombok的版本。

##### 步骤2:安装Lombok的插件

==新版本IDEA已经内置了该插件，如果删除setter和getter方法程序有报红，则需要安装插件==

![1631016543648](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Mybatisplus笔记/assets/1631016543648.png)

如果在IDEA中找不到lombok插件，可以访问如下网站

`https://plugins.jetbrains.com/plugin/6317-lombok/versions`

根据自己IDEA的版本下载对应的lombok插件，下载成功后，在IDEA中采用离线安装的方式进行安装。

![1631016876641](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Mybatisplus笔记/assets/1631016876641.png)

##### 步骤3:模型类上添加注解

Lombok常见的注解有:

* @Setter:为模型类的属性提供setter方法
* @Getter:为模型类的属性提供getter方法
* @ToString:为模型类的属性提供toString方法
* @EqualsAndHashCode:为模型类的属性提供equals和hashcode方法
* ==@Data:是个组合注解，包含上面的注解的功能==
* ==@NoArgsConstructor:提供一个无参构造函数==
* ==@AllArgsConstructor:提供一个包含所有参数的构造函数==

Lombok的注解还有很多，上面标红的三个是比较常用的，其他的大家后期用到了，再去补充学习。

```java
@Data
@AllArgsConstructor
@NoArgsConstructor
public class User {
    private Long id;
    private String name;
    private String password;
    private Integer age;
    private String tel;
}
```

**说明:**

Lombok只是简化模型类的编写，我们之前的方法也能用，比如有人会问:我如果只想要有name和password的构造函数，该如何编写?

```java
@Data
@AllArgsConstructor
@NoArgsConstructor
public class User {
    private Long id;
    private String name;
    private String password;
    private Integer age;
    private String tel;

    public User(String name, String password) {
        this.name = name;
        this.password = password;
    }
}
```

这种方式是被允许的。

### 2.8 分页功能

基础的增删改查就已经学习完了，刚才我们在分析基础开发的时候，有一个分页功能还没有实现，在MP中如何实现分页功能，就是咱们接下来要学习的内容。

分页查询使用的方法是:

```java
IPage<T> selectPage(IPage<T> page, Wrapper<T> queryWrapper)
```

- IPage:用来构建分页查询条件
- Wrapper：用来构建条件查询的条件，目前我们没有可直接传为Null
- IPage:返回值，你会发现构建分页条件和方法的返回值都是IPage

IPage是一个接口，我们需要找到它的实现类来构建它，具体的实现类，可以进入到IPage类中按ctrl+h,会找到其有一个实现类为`Page`。

#### 步骤1:调用方法传入参数获取返回值

```java
@SpringBootTest
class Mybatisplus01QuickstartApplicationTests {

    @Autowired
    private UserDao userDao;
    
    //分页查询
    @Test
    void testSelectPage(){
        //1 创建IPage分页对象,设置分页参数,1为当前页码，3为每页显示的记录数
        IPage<User> page=new Page<>(1,3);
        //2 执行分页查询
        userDao.selectPage(page,null);
        //3 获取分页结果
        System.out.println("当前页码值："+page.getCurrent());
        System.out.println("每页显示数："+page.getSize());
        System.out.println("一共多少页："+page.getPages());
        System.out.println("一共多少条数据："+page.getTotal());
        System.out.println("数据："+page.getRecords());
    }
}
```

#### 步骤2:设置分页拦截器

这个拦截器MP已经为我们提供好了，我们只需要将其配置成Spring管理的bean对象即可。

```java
@Configuration
public class MybatisPlusConfig {
    
    @Bean
    public MybatisPlusInterceptor mybatisPlusInterceptor(){
        //1 创建MybatisPlusInterceptor拦截器对象
        MybatisPlusInterceptor mpInterceptor=new MybatisPlusInterceptor();
        //2 添加分页拦截器
        mpInterceptor.addInnerInterceptor(new PaginationInnerInterceptor());
        return mpInterceptor;
    }
}
```

**说明:**上面的代码记不住咋办呢?

这些内容在MP的官方文档中有详细的说明，我们可以查看官方文档类配置

![1631208030131](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Mybatisplus笔记/assets/1631208030131.png)

#### 步骤3:运行测试程序

![1631019660480](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Mybatisplus笔记/assets/1631019660480.png)

如果想查看MP执行的SQL语句，可以修改application.yml配置文件，

```yml
mybatis-plus:
  configuration:
    log-impl: org.apache.ibatis.logging.stdout.StdOutImpl #打印SQL日志到控制台
```

打开日志后，就可以在控制台打印出对应的SQL语句，开启日志功能性能就会受到影响，调试完后记得关闭。

![1631019896688](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Mybatisplus笔记/assets/1631019896688.png)

## 3，DQL编程控制

增删改查四个操作中，查询是非常重要的也是非常复杂的操作，这块需要我们重点学习下，这节我们主要学习的内容有:

* 条件查询方式
* 查询投影
* 查询条件设定
* 字段映射与表名映射

### 3.1 条件查询

#### 3.1.1 条件查询的类

* MyBatisPlus将书写复杂的SQL查询条件进行了封装，使用编程的形式完成查询条件的组合。

这个我们在前面都有见过，比如查询所有和分页查询的时候，都有看到过一个`Wrapper`类，这个类就是用来构建查询条件的，如下图所示:

![1631020283701](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Mybatisplus笔记/assets/1631020283701.png)

那么条件查询如何使用Wrapper来构建呢?

#### 3.1.2 环境构建

在构建条件查询之前，我们先来准备下环境

* 创建一个SpringBoot项目

* pom.xml中添加对应的依赖

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
      <modelVersion>4.0.0</modelVersion>
      <parent>
          <groupId>org.springframework.boot</groupId>
          <artifactId>spring-boot-starter-parent</artifactId>
          <version>2.5.0</version>
      </parent>
      <groupId>com.itheima</groupId>
      <artifactId>mybatisplus_02_dql</artifactId>
      <version>0.0.1-SNAPSHOT</version>
      <properties>
          <java.version>1.8</java.version>
      </properties>
      <dependencies>
  
          <dependency>
              <groupId>com.baomidou</groupId>
              <artifactId>mybatis-plus-boot-starter</artifactId>
              <version>3.4.1</version>
          </dependency>
  
          <dependency>
              <groupId>org.springframework.boot</groupId>
              <artifactId>spring-boot-starter</artifactId>
          </dependency>
  
          <dependency>
              <groupId>com.alibaba</groupId>
              <artifactId>druid</artifactId>
              <version>1.1.16</version>
          </dependency>
  
          <dependency>
              <groupId>mysql</groupId>
              <artifactId>mysql-connector-java</artifactId>
              <scope>runtime</scope>
          </dependency>
  
          <dependency>
              <groupId>org.springframework.boot</groupId>
              <artifactId>spring-boot-starter-test</artifactId>
              <scope>test</scope>
          </dependency>
  
          <dependency>
              <groupId>org.projectlombok</groupId>
              <artifactId>lombok</artifactId>
          </dependency>
  
      </dependencies>
  
      <build>
          <plugins>
              <plugin>
                  <groupId>org.springframework.boot</groupId>
                  <artifactId>spring-boot-maven-plugin</artifactId>
              </plugin>
          </plugins>
      </build>
  
  </project>
  
  ```

* 编写UserDao接口

  ```java
  @Mapper
  public interface UserDao extends BaseMapper<User> {
  }
  ```

* 编写模型类

  ```java
  @Data
  public class User {
      private Long id;
      private String name;
      private String password;
      private Integer age;
      private String tel;
  }
  ```

* 编写引导类

  ```java
  @SpringBootApplication
  public class Mybatisplus02DqlApplication {
  
      public static void main(String[] args) {
          SpringApplication.run(Mybatisplus02DqlApplication.class, args);
      }
  
  }
  ```

* 编写配置文件

  ```yml
  # dataSource
  spring:
    datasource:
      type: com.alibaba.druid.pool.DruidDataSource
      driver-class-name: com.mysql.cj.jdbc.Driver
      url: jdbc:mysql://localhost:3306/mybatisplus_db?serverTimezone=UTC
      username: root
      password: root
  # mp日志
  mybatis-plus:
    configuration:
      log-impl: org.apache.ibatis.logging.stdout.StdOutImpl
  ```

* 编写测试类

  ```java
  @SpringBootTest
  class Mybatisplus02DqlApplicationTests {
  
      @Autowired
      private UserDao userDao;
      
      @Test
      void testGetAll(){
          List<User> userList = userDao.selectList(null);
          System.out.println(userList);
      }
  }
  ```

  最终创建的项目结构为:

  ![1631033477792](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Mybatisplus笔记/assets/1631033477792.png)

* 测试的时候，控制台打印的日志比较多，速度有点慢而且不利于查看运行结果，所以接下来我们把这个日志处理下:

  * 取消初始化spring日志打印，resources目录下添加logback.xml，名称固定，内容如下:

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>
    </configuration>
    ```

    **说明:**logback.xml的配置内容，不是我们学习的重点，如果有兴趣可以自行百度查询。

  * 取消MybatisPlus启动banner图标

    ![1631021315906](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Mybatisplus笔记/assets/1631021315906.png)

    application.yml添加如下内容:

    ```yml
    # mybatis-plus日志控制台输出
    mybatis-plus:
      configuration:
        log-impl: org.apache.ibatis.logging.stdout.StdOutImpl
      global-config:
        banner: off # 关闭mybatisplus启动图标
    ```

  * 取消SpringBoot的log打印

    ![1631021269422](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Mybatisplus笔记/assets/1631021269422.png)

    application.yml添加如下内容:

    ```yml
    spring:
      main:
        banner-mode: off # 关闭SpringBoot启动图标(banner)
    ```

解决控制台打印日志过多的相关操作可以不用去做，一般会被用来方便我们查看程序运行的结果。

#### 3.1.3 构建条件查询

在进行查询的时候，我们的入口是在Wrapper这个类上，因为它是一个接口，所以我们需要去找它对应的实现类，关于实现类也有很多，说明我们有多种构建查询条件对象的方式，

![1631021942869](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Mybatisplus笔记/assets/1631021942869.png)

1. 先来看第一种:==QueryWrapper==

```java
@SpringBootTest
class Mybatisplus02DqlApplicationTests {

    @Autowired
    private UserDao userDao;
    
    @Test
    void testGetAll(){
        QueryWrapper qw = new QueryWrapper();
        qw.lt("age",18);
        List<User> userList = userDao.selectList(qw);
        System.out.println(userList);
    }
}
```

* lt: 小于(<) ,最终的sql语句为

  ```sql
  SELECT id,name,password,age,tel FROM user WHERE (age < ?)
  ```

第一种方式介绍完后，有个小问题就是在写条件的时候，容易出错，比如age写错，就会导致查询不成功

2. 接着来看第二种:==QueryWrapper的基础上使用lambda==

```java
@SpringBootTest
class Mybatisplus02DqlApplicationTests {

    @Autowired
    private UserDao userDao;
    
    @Test
    void testGetAll(){
        QueryWrapper<User> qw = new QueryWrapper<User>();
        qw.lambda().lt(User::getAge, 10);//添加条件
        List<User> userList = userDao.selectList(qw);
        System.out.println(userList);
    }
}
```

* User::getAget,为lambda表达式中的，类名::方法名，最终的sql语句为:

```sql
SELECT id,name,password,age,tel FROM user WHERE (age < ?)
```

**注意:**构建LambdaQueryWrapper的时候泛型不能省。

此时我们再次编写条件的时候，就不会存在写错名称的情况，但是qw后面多了一层lambda()调用

3. 接着来看第三种:==LambdaQueryWrapper==

```java
@SpringBootTest
class Mybatisplus02DqlApplicationTests {

    @Autowired
    private UserDao userDao;
    
    @Test
    void testGetAll(){
        LambdaQueryWrapper<User> lqw = new LambdaQueryWrapper<User>();
        lqw.lt(User::getAge, 10);
        List<User> userList = userDao.selectList(lqw);
        System.out.println(userList);
    }
}
```

这种方式就解决了上一种方式所存在的问题。

#### 3.1.4 多条件构建

学完了三种构建查询对象的方式，每一种都有自己的特点，所以用哪一种都行，刚才都是一个条件，那如果有多个条件该如何构建呢?

> 需求:查询数据库表中，年龄在10岁到30岁之间的用户信息

```java
@SpringBootTest
class Mybatisplus02DqlApplicationTests {

    @Autowired
    private UserDao userDao;
    
    @Test
    void testGetAll(){
        LambdaQueryWrapper<User> lqw = new LambdaQueryWrapper<User>();
        lqw.lt(User::getAge, 30);
        lqw.gt(User::getAge, 10);
        List<User> userList = userDao.selectList(lqw);
        System.out.println(userList);
    }
}
```

* gt：大于(>),最终的SQL语句为

  ```sql
  SELECT id,name,password,age,tel FROM user WHERE (age < ? AND age > ?)
  ```

* 构建多条件的时候，可以支持链式编程

  ```java
  LambdaQueryWrapper<User> lqw = new LambdaQueryWrapper<User>();
  lqw.lt(User::getAge, 30).gt(User::getAge, 10);
  List<User> userList = userDao.selectList(lqw);
  System.out.println(userList);
  ```

> 需求:查询数据库表中，年龄小于10或年龄大于30的数据

```java
@SpringBootTest
class Mybatisplus02DqlApplicationTests {

    @Autowired
    private UserDao userDao;
    
    @Test
    void testGetAll(){
        LambdaQueryWrapper<User> lqw = new LambdaQueryWrapper<User>();
        lqw.lt(User::getAge, 10).or().gt(User::getAge, 30);
        List<User> userList = userDao.selectList(lqw);
        System.out.println(userList);
    }
}
```

* or()就相当于我们sql语句中的`or`关键字,不加默认是`and`，最终的sql语句为:

  ```sql
  SELECT id,name,password,age,tel FROM user WHERE (age < ? OR age > ?)
  ```

#### 3.1.5 null判定

先来看一张图，

![1631023641992](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Mybatisplus笔记/assets/1631023641992.png)

* 我们在做条件查询的时候，一般会有很多条件可以供用户进行选择查询。
* 这些条件用户可以选择使用也可以选择不使用，比如我要查询价格在8000以上的手机
* 在输入条件的时候，价格有一个区间范围，按照需求只需要在第一个价格输入框中输入8000
* 后台在做价格查询的时候，一般会让 price>值1 and price <值2
* 因为前端没有输入值2，所以如果不处理的话，就会出现 price>8000 and price < null问题
* 这个时候查询的结果就会出问题，具体该如何解决?

![1631024145264](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Mybatisplus笔记/assets/1631024145264.png)

> 需求:查询数据库表中，根据输入年龄范围来查询符合条件的记录
>
> 用户在输入值的时候，
>
> ​	如果只输入第一个框，说明要查询大于该年龄的用户
>
> ​	如果只输入第二个框，说明要查询小于该年龄的用户
>
> ​    如果两个框都输入了，说明要查询年龄在两个范围之间的用户

思考第一个问题：后台如果想接收前端的两个数据，该如何接收?

我们可以使用两个简单数据类型，也可以使用一个模型类，但是User类中目前只有一个age属性,如:

```java
@Data
public class User {
    private Long id;
    private String name;
    private String password;
    private Integer age;
    private String tel;
}
```

使用一个age属性，如何去接收页面上的两个值呢?这个时候我们有两个解决方案

方案一:添加属性age2,这种做法可以但是会影响到原模型类的属性内容

```java
@Data
public class User {
    private Long id;
    private String name;
    private String password;
    private Integer age;
    private String tel;
    private Integer age2;
}
```

方案二:新建一个模型类,让其继承User类，并在其中添加age2属性，UserQuery在拥有User属性后同时添加了age2属性。

```java
@Data
public class User {
    private Long id;
    private String name;
    private String password;
    private Integer age;
    private String tel;
}

@Data
public class UserQuery extends User {
    private Integer age2;
}
```

环境准备好后，我们来实现下刚才的需求：

```java
@SpringBootTest
class Mybatisplus02DqlApplicationTests {

    @Autowired
    private UserDao userDao;
    
    @Test
    void testGetAll(){
        //模拟页面传递过来的查询数据
        UserQuery uq = new UserQuery();
        uq.setAge(10);
        uq.setAge2(30);
        LambdaQueryWrapper<User> lqw = new LambdaQueryWrapper<User>();
        if(null != uq.getAge2()){
            lqw.lt(User::getAge, uq.getAge2());
        }
        if( null != uq.getAge()) {
            lqw.gt(User::getAge, uq.getAge());
        }
        List<User> userList = userDao.selectList(lqw);
        System.out.println(userList);
    }
}
```

上面的写法可以完成条件为非空的判断，但是问题很明显，如果条件多的话，每个条件都需要判断，代码量就比较大，来看MP给我们提供的简化方式：

```java
@SpringBootTest
class Mybatisplus02DqlApplicationTests {

    @Autowired
    private UserDao userDao;
    
    @Test
    void testGetAll(){
        //模拟页面传递过来的查询数据
        UserQuery uq = new UserQuery();
        uq.setAge(10);
        uq.setAge2(30);
        LambdaQueryWrapper<User> lqw = new LambdaQueryWrapper<User>();
        lqw.lt(null!=uq.getAge2(),User::getAge, uq.getAge2());
        lqw.gt(null!=uq.getAge(),User::getAge, uq.getAge());
        List<User> userList = userDao.selectList(lqw);
        System.out.println(userList);
    }
}
```

* lt()方法

  ![1631025068317](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Mybatisplus笔记/assets/1631025068317.png)

  condition为boolean类型，返回true，则添加条件，返回false则不添加条件

### 3.2 查询投影

#### 3.2.1 查询指定字段

目前我们在查询数据的时候，什么都没有做默认就是查询表中所有字段的内容，我们所说的查询投影即不查询所有字段，只查询出指定内容的数据。

具体如何来实现?

```java
@SpringBootTest
class Mybatisplus02DqlApplicationTests {

    @Autowired
    private UserDao userDao;
    
    @Test
    void testGetAll(){
        LambdaQueryWrapper<User> lqw = new LambdaQueryWrapper<User>();
        lqw.select(User::getId,User::getName,User::getAge);
        List<User> userList = userDao.selectList(lqw);
        System.out.println(userList);
    }
}
```

* select(...)方法用来设置查询的字段列，可以设置多个，最终的sql语句为:

  ```sql
  SELECT id,name,age FROM user
  ```

* 如果使用的不是lambda，就需要手动指定字段

  ```java
  @SpringBootTest
  class Mybatisplus02DqlApplicationTests {
  
      @Autowired
      private UserDao userDao;
      
      @Test
      void testGetAll(){
          QueryWrapper<User> lqw = new QueryWrapper<User>();
          lqw.select("id","name","age","tel");
          List<User> userList = userDao.selectList(lqw);
          System.out.println(userList);
      }
  }
  ```

  * 最终的sql语句为:SELECT id,name,age,tel FROM user

#### 3.2.2 聚合查询

> 需求:聚合函数查询，完成count、max、min、avg、sum的使用
>
> count:总记录数
>
> max:最大值
>
> min:最小值
>
> avg:平均值
>
> sum:求和

```java
@SpringBootTest
class Mybatisplus02DqlApplicationTests {

    @Autowired
    private UserDao userDao;
    
    @Test
    void testGetAll(){
        QueryWrapper<User> lqw = new QueryWrapper<User>();
        //lqw.select("count(*) as count");
        //SELECT count(*) as count FROM user
        //lqw.select("max(age) as maxAge");
        //SELECT max(age) as maxAge FROM user
        //lqw.select("min(age) as minAge");
        //SELECT min(age) as minAge FROM user
        //lqw.select("sum(age) as sumAge");
        //SELECT sum(age) as sumAge FROM user
        lqw.select("avg(age) as avgAge");
        //SELECT avg(age) as avgAge FROM user
        List<Map<String, Object>> userList = userDao.selectMaps(lqw);
        System.out.println(userList);
    }
}
```

为了在做结果封装的时候能够更简单，我们将上面的聚合函数都起了个名称，方面后期来获取这些数据

#### 3.2.3 分组查询

> 需求:分组查询，完成 group by的查询使用

```java
@SpringBootTest
class Mybatisplus02DqlApplicationTests {

    @Autowired
    private UserDao userDao;
    
    @Test
    void testGetAll(){
        QueryWrapper<User> lqw = new QueryWrapper<User>();
        lqw.select("count(*) as count,tel");
        lqw.groupBy("tel");
        List<Map<String, Object>> list = userDao.selectMaps(lqw);
        System.out.println(list);
    }
}
```

* groupBy为分组，最终的sql语句为

  ```sql
  SELECT count(*) as count,tel FROM user GROUP BY tel
  ```

**注意:**

* 聚合与分组查询，无法使用lambda表达式来完成
* MP只是对MyBatis的增强，如果MP实现不了，我们可以直接在DAO接口中使用MyBatis的方式实现

### 3.3 查询条件

前面我们只使用了lt()和gt(),除了这两个方法外，MP还封装了很多条件对应的方法，这一节我们重点把MP提供的查询条件方法进行学习下。

MP的查询条件有很多:

* 范围匹配（> 、 = 、between）
* 模糊匹配（like）
* 空判定（null）
* 包含性匹配（in）
* 分组（group）
* 排序（order）
* ……

#### 3.3.1 等值查询

> 需求:根据用户名和密码查询用户信息

```java
@SpringBootTest
class Mybatisplus02DqlApplicationTests {

    @Autowired
    private UserDao userDao;
    
    @Test
    void testGetAll(){
        LambdaQueryWrapper<User> lqw = new LambdaQueryWrapper<User>();
        lqw.eq(User::getName, "Jerry").eq(User::getPassword, "jerry");
        User loginUser = userDao.selectOne(lqw);
        System.out.println(loginUser);
    }
}
```

* eq()： 相当于 `=`,对应的sql语句为

  ```sql
  SELECT id,name,password,age,tel FROM user WHERE (name = ? AND password = ?)
  ```

* selectList：查询结果为多个或者单个

* selectOne:查询结果为单个

#### 3.3.2 范围查询

> 需求:对年龄进行范围查询，使用lt()、le()、gt()、ge()、between()进行范围查询

```java
@SpringBootTest
class Mybatisplus02DqlApplicationTests {

    @Autowired
    private UserDao userDao;
    
    @Test
    void testGetAll(){
        LambdaQueryWrapper<User> lqw = new LambdaQueryWrapper<User>();
        lqw.between(User::getAge, 10, 30);
        //SELECT id,name,password,age,tel FROM user WHERE (age BETWEEN ? AND ?)
        List<User> userList = userDao.selectList(lqw);
        System.out.println(userList);
    }
}
```

* gt():大于(>)
* ge():大于等于(>=)
* lt():小于(<)
* lte():小于等于(<=)
* between():between ? and ?

#### 3.3.3 模糊查询

> 需求:查询表中name属性的值以`J`开头的用户信息,使用like进行模糊查询

```java
@SpringBootTest
class Mybatisplus02DqlApplicationTests {

    @Autowired
    private UserDao userDao;
    
    @Test
    void testGetAll(){
        LambdaQueryWrapper<User> lqw = new LambdaQueryWrapper<User>();
        lqw.likeLeft(User::getName, "J");
        //SELECT id,name,password,age,tel FROM user WHERE (name LIKE ?)
        List<User> userList = userDao.selectList(lqw);
        System.out.println(userList);
    }
}
```

* like():前后加百分号,如 %J%
* likeLeft():前面加百分号,如 %J
* likeRight():后面加百分号,如 J%

#### 3.3.4 排序查询

> 需求:查询所有数据，然后按照id降序

```java
@SpringBootTest
class Mybatisplus02DqlApplicationTests {

    @Autowired
    private UserDao userDao;
    
    @Test
    void testGetAll(){
        LambdaQueryWrapper<User> lwq = new LambdaQueryWrapper<>();
        /**
         * condition ：条件，返回boolean，
         		当condition为true，进行排序，如果为false，则不排序
         * isAsc:是否为升序，true为升序，false为降序
         * columns：需要操作的列
         */
        lwq.orderBy(true,false, User::getId);

        userDao.selectList(lw
    }
}
```

除了上面演示的这种实现方式，还有很多其他的排序方法可以被调用，如图:

![1631209838333](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Mybatisplus笔记/assets/1631209838333.png)

* orderBy排序
  * condition:条件，true则添加排序，false则不添加排序
  * isAsc:是否为升序，true升序，false降序
  * columns:排序字段，可以有多个
* orderByAsc/Desc(单个column):按照指定字段进行升序/降序
* orderByAsc/Desc(多个column):按照多个字段进行升序/降序
* orderByAsc/Desc
  * condition:条件，true添加排序，false不添加排序
  * 多个columns：按照多个字段进行排序

除了上面介绍的这几种查询条件构建方法以外还会有很多其他的方法，比如isNull,isNotNull,in,notIn等等方法可供选择，具体参考官方文档的条件构造器来学习使用，具体的网址为:

`https://mp.baomidou.com/guide/wrapper.html#abstractwrapper`

### 3.4 映射匹配兼容性

前面我们已经能从表中查询出数据，并将数据封装到模型类中，这整个过程涉及到一张表和一个模型类:

![1631030296965](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Mybatisplus笔记/assets/1631030296965.png)

之所以数据能够成功的从表中获取并封装到模型对象中，原因是表的字段列名和模型类的属性名一样。

那么问题就来了:

#### 问题1:表字段与编码属性设计不同步

当表的列名和模型类的属性名发生不一致，就会导致数据封装不到模型对象，这个时候就需要其中一方做出修改，那如果前提是两边都不能改又该如何解决?

MP给我们提供了一个注解`@TableField`,使用该注解可以实现模型类属性名和表的列名之间的映射关系

![1631030550100](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Mybatisplus笔记/assets/1631030550100.png)

#### 问题2:编码中添加了数据库中未定义的属性

当模型类中多了一个数据库表不存在的字段，就会导致生成的sql语句中在select的时候查询了数据库不存在的字段，程序运行就会报错，错误信息为:

==Unknown column '多出来的字段名称' in 'field list'==

具体的解决方案用到的还是`@TableField`注解，它有一个属性叫`exist`，设置该字段是否在数据库表中存在，如果设置为false则不存在，生成sql语句查询的时候，就不会再查询该字段了。

![1631031054206](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Mybatisplus笔记/assets/1631031054206.png)

#### 问题3：采用默认查询开放了更多的字段查看权限

查询表中所有的列的数据，就可能把一些敏感数据查询到返回给前端，这个时候我们就需要限制哪些字段默认不要进行查询。解决方案是`@TableField`注解的一个属性叫`select`，该属性设置默认是否需要查询该字段的值，true(默认值)表示默认查询该字段，false表示默认不查询该字段。

![1631031270558](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Mybatisplus笔记/assets/1631031270558.png)

#### 知识点1：@TableField

| 名称     | @TableField                                                  |
| -------- | ------------------------------------------------------------ |
| 类型     | ==属性注解==                                                 |
| 位置     | 模型类属性定义上方                                           |
| 作用     | 设置当前属性对应的数据库表中的字段关系                       |
| 相关属性 | value(默认)：设置数据库表字段名称<br/>exist:设置属性在数据库表字段中是否存在，默认为true，此属性不能与value合并使用<br/>select:设置属性是否参与查询，此属性与select()映射配置不冲突 |

#### 问题4:表名与编码开发设计不同步

该问题主要是表的名称和模型类的名称不一致，导致查询失败，这个时候通常会报如下错误信息:

==Table 'databaseName.tableNaem' doesn't exist==,翻译过来就是数据库中的表不存在。

![1631031828378](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Mybatisplus笔记/assets/1631031828378.png)

解决方案是使用MP提供的另外一个注解`@TableName`来设置表与模型类之间的对应关系。

![1631031915632](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Mybatisplus笔记/assets/1631031915632.png)

#### 知识点2：@TableName

| 名称     | @TableName                    |
| -------- | ----------------------------- |
| 类型     | ==类注解==                    |
| 位置     | 模型类定义上方                |
| 作用     | 设置当前类对应于数据库表关系  |
| 相关属性 | value(默认)：设置数据库表名称 |

#### 代码演示

接下来我们使用案例的方式把刚才的知识演示下:

##### 步骤1:修改数据库表user为tbl_user

直接查询会报错，原因是MP默认情况下会使用模型类的类名首字母小写当表名使用。

![1631032123894](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Mybatisplus笔记/assets/1631032123894.png)

##### 步骤2:模型类添加@TableName注解

```java
@Data
@TableName("tbl_user")
public class User {
    private Long id;
    private String name;
    private String password;
    private Integer age;
    private String tel;
}
```

##### 步骤3:将字段password修改成pwd

直接查询会报错，原因是MP默认情况下会使用模型类的属性名当做表的列名使用

![1631032283147](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Mybatisplus笔记/assets/1631032283147.png)

##### 步骤4：使用@TableField映射关系

```java
@Data
@TableName("tbl_user")
public class User {
    private Long id;
    private String name;
    @TableField(value="pwd")
    private String password;
    private Integer age;
    private String tel;
}
```

##### 步骤5:添加一个数据库表不存在的字段

```java
@Data
@TableName("tbl_user")
public class User {
    private Long id;
    private String name;
    @TableField(value="pwd")
    private String password;
    private Integer age;
    private String tel;
    private Integer online;
}
```

直接查询会报错，原因是MP默认情况下会查询模型类的所有属性对应的数据库表的列，而online不存在

![1631032450558](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Mybatisplus笔记/assets/1631032450558.png)

##### 步骤6：使用@TableField排除字段

```java
@Data
@TableName("tbl_user")
public class User {
    private Long id;
    private String name;
    @TableField(value="pwd")
    private String password;
    private Integer age;
    private String tel;
    @TableField(exist=false)
    private Integer online;
}
```

##### 步骤7:查询时将pwd隐藏

```java
@Data
@TableName("tbl_user")
public class User {
    private Long id;
    private String name;
    @TableField(value="pwd",select=false)
    private String password;
    private Integer age;
    private String tel;
    @TableField(exist=false)
    private Integer online;
}
```

## 4，DML编程控制

查询相关的操作我们已经介绍完了，紧接着我们需要对另外三个，增删改进行内容的讲解。挨个来说明下，首先是新增(insert)中的内容。

### 4.1 id生成策略控制

前面我们在新增的时候留了一个问题，就是新增成功后，主键ID是一个很长串的内容，我们更想要的是按照数据库表字段进行自增长，在解决这个问题之前，我们先来分析下ID该如何选择:

* 不同的表应用不同的id生成策略
  * 日志：自增（1,2,3,4，……）
  * 购物订单：特殊规则（FQ23948AK3843）
  * 外卖单：关联地区日期等信息（10 04 20200314 34 91）
  * 关系表：可省略id
  * ……

不同的业务采用的ID生成方式应该是不一样的，那么在MP中都提供了哪些主键生成策略，以及我们该如何进行选择?

在这里我们又需要用到MP的一个注解叫`@TableId`

#### 知识点1：@TableId

| 名称     | @TableId                                                     |
| -------- | ------------------------------------------------------------ |
| 类型     | ==属性注解==                                                 |
| 位置     | 模型类中用于表示主键的属性定义上方                           |
| 作用     | 设置当前类中主键属性的生成策略                               |
| 相关属性 | value(默认)：设置数据库表主键名称<br/>type:设置主键属性的生成策略，值查照IdType的枚举值 |

#### 4.1.1 环境构建

在构建条件查询之前，我们先来准备下环境

- 创建一个SpringBoot项目

- pom.xml中添加对应的依赖

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
      <modelVersion>4.0.0</modelVersion>
      <parent>
          <groupId>org.springframework.boot</groupId>
          <artifactId>spring-boot-starter-parent</artifactId>
          <version>2.5.0</version>
          <relativePath/> <!-- lookup parent from repository -->
      </parent>
      <groupId>com.itheima</groupId>
      <artifactId>mybatisplus_03_dml</artifactId>
      <version>0.0.1-SNAPSHOT</version>
      <properties>
          <java.version>1.8</java.version>
      </properties>
      <dependencies>
  
          <dependency>
              <groupId>com.baomidou</groupId>
              <artifactId>mybatis-plus-boot-starter</artifactId>
              <version>3.4.1</version>
          </dependency>
  
          <dependency>
              <groupId>org.springframework.boot</groupId>
              <artifactId>spring-boot-starter</artifactId>
          </dependency>
  
          <dependency>
              <groupId>com.alibaba</groupId>
              <artifactId>druid</artifactId>
              <version>1.1.16</version>
          </dependency>
  
          <dependency>
              <groupId>mysql</groupId>
              <artifactId>mysql-connector-java</artifactId>
              <scope>runtime</scope>
          </dependency>
  
          <dependency>
              <groupId>org.springframework.boot</groupId>
              <artifactId>spring-boot-starter-test</artifactId>
              <scope>test</scope>
          </dependency>
  
          <dependency>
              <groupId>org.projectlombok</groupId>
              <artifactId>lombok</artifactId>
              <version>1.18.12</version>
          </dependency>
  
      </dependencies>
  
      <build>
          <plugins>
              <plugin>
                  <groupId>org.springframework.boot</groupId>
                  <artifactId>spring-boot-maven-plugin</artifactId>
              </plugin>
          </plugins>
      </build>
  
  </project>
  
  ```

- 编写UserDao接口

  ```java
  @Mapper
  public interface UserDao extends BaseMapper<User> {
  }
  ```

- 编写模型类

  ```java
  @Data
  @TableName("tbl_user")
  public class User {
      private Long id;
      private String name;
      @TableField(value="pwd",select=false)
      private String password;
      private Integer age;
      private String tel;
      @TableField(exist=false)
      private Integer online;
  }
  ```

- 编写引导类

  ```java
  @SpringBootApplication
  public class Mybatisplus03DqlApplication {
  
      public static void main(String[] args) {
          SpringApplication.run(Mybatisplus03DqlApplication.class, args);
      }
  
  }
  ```

- 编写配置文件

  ```yml
  # dataSource
  spring:
    datasource:
      type: com.alibaba.druid.pool.DruidDataSource
      driver-class-name: com.mysql.cj.jdbc.Driver
      url: jdbc:mysql://localhost:3306/mybatisplus_db?serverTimezone=UTC
      username: root
      password: root
  # mp日志
  mybatis-plus:
    configuration:
      log-impl: org.apache.ibatis.logging.stdout.StdOutImpl
  ```

- 编写测试类

  ```java
  @SpringBootTest
  class Mybatisplus02DqlApplicationTests {
  
      @Autowired
      private UserDao userDao;
      
      @Test
      void testGetAll(){
          List<User> userList = userDao.selectList(null);
          System.out.println(userList);
      }
  }
  ```

- 测试

  ```java
  @SpringBootTest
  class Mybatisplus03DqlApplicationTests {
  
      @Autowired
      private UserDao userDao;
  	
      @Test
      void testSave(){
          User user = new User();
          user.setName("黑马程序员");
          user.setPassword("itheima");
          user.setAge(12);
          user.setTel("4006184000");
          userDao.insert(user);
      }
      @Test
      void testDelete(){
          userDao.deleteById(1401856123925713409L)
      }
      @Test
      void testUpdate(){
          User user = new User();
          user.setId(3L);
          user.setName("Jock666");
          user.setVersion(1);
          userDao.updateById(user);
      }
  }
  ```

- 最终创建的项目结构为:

  ![1631033634879](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Mybatisplus笔记/assets/1631033634879.png)

#### 4.1.2 代码演示

##### AUTO策略

###### 步骤1:设置生成策略为AUTO

```java
@Data
@TableName("tbl_user")
public class User {
    @TableId(type = IdType.AUTO)
    private Long id;
    private String name;
    @TableField(value="pwd",select=false)
    private String password;
    private Integer age;
    private String tel;
    @TableField(exist=false)
    private Integer online;
}
```

###### 步骤2:删除测试数据并修改自增值

* 删除测试数据

  ![1631211291677](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Mybatisplus笔记/assets/1631211291677.png)

* 因为之前生成主键ID的值比较长，会把MySQL的自动增长的值变的很大，所以需要将其调整为目前最新的id值。

![1631211080703](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Mybatisplus笔记/assets/1631211080703.png)

###### 步骤3:运行新增方法  

会发现，新增成功，并且主键id也是从5开始

![1631211383421](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Mybatisplus笔记/assets/1631211383421.png)

经过这三步的演示，会发现`AUTO`的作用是==使用数据库ID自增==，在使用该策略的时候一定要确保对应的数据库表设置了ID主键自增，否则无效。

接下来，我们可以进入源码查看下ID的生成策略有哪些?

打开源码后，你会发现并没有看到中文注释，这就需要我们点击右上角的`Download Sources`,会自动帮你把这个类的java文件下载下来，我们就能看到具体的注释内容。因为这个技术是国人制作的，所以他代码中的注释还是比较容易看懂的。

![1631211697712](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Mybatisplus笔记/assets/1631211697712.png)

当把源码下载完后，就可以看到如下内容:

![1631211902833](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Mybatisplus笔记/assets/1631211902833.png)

从源码中可以看到，除了AUTO这个策略以外，还有如下几种生成策略:

* NONE: 不设置id生成策略
* INPUT:用户手工输入id
* ASSIGN_ID:雪花算法生成id(可兼容数值型与字符串型)
* ASSIGN_UUID:以UUID生成算法作为id生成策略
* 其他的几个策略均已过时，都将被ASSIGN_ID和ASSIGN_UUID代替掉。

**拓展:**

分布式ID是什么?

* 当数据量足够大的时候，一台数据库服务器存储不下，这个时候就需要多台数据库服务器进行存储
* 比如订单表就有可能被存储在不同的服务器上
* 如果用数据库表的自增主键，因为在两台服务器上所以会出现冲突
* 这个时候就需要一个全局唯一ID,这个ID就是分布式ID。

##### INPUT策略

###### 步骤1:设置生成策略为INPUT

```java
@Data
@TableName("tbl_user")
public class User {
    @TableId(type = IdType.INPUT)
    private Long id;
    private String name;
    @TableField(value="pwd",select=false)
    private String password;
    private Integer age;
    private String tel;
    @TableField(exist=false)
    private Integer online;
}
```

**注意:**这种ID生成策略，需要将表的自增策略删除掉

![1631212246124](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Mybatisplus笔记/assets/1631212246124.png)

###### 步骤2:添加数据手动设置ID

```java
@SpringBootTest
class Mybatisplus03DqlApplicationTests {

    @Autowired
    private UserDao userDao;
	
    @Test
    void testSave(){
        User user = new User();
        //设置主键ID的值
        user.setId(666L);
        user.setName("黑马程序员");
        user.setPassword("itheima");
        user.setAge(12);
        user.setTel("4006184000");
        userDao.insert(user);
    }
}
```

###### 步骤3:运行新增方法

如果没有设置主键ID的值，则会报错，错误提示就是主键ID没有给值:

![1631212469974](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Mybatisplus笔记/assets/1631212469974.png)

如果设置了主键ID,则数据添加成功，如下:

![1631212421137](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Mybatisplus笔记/assets/1631212421137.png)

##### ASSIGN_ID策略

###### 步骤1:设置生成策略为ASSIGN_ID

```java
@Data
@TableName("tbl_user")
public class User {
    @TableId(type = IdType.ASSIGN_ID)
    private Long id;
    private String name;
    @TableField(value="pwd",select=false)
    private String password;
    private Integer age;
    private String tel;
    @TableField(exist=false)
    private Integer online;
}
```

###### 步骤2:添加数据不设置ID

```java
@SpringBootTest
class Mybatisplus03DqlApplicationTests {

    @Autowired
    private UserDao userDao;
	
    @Test
    void testSave(){
        User user = new User();
        user.setName("黑马程序员");
        user.setPassword("itheima");
        user.setAge(12);
        user.setTel("4006184000");
        userDao.insert(user);
    }
}
```

**注意:**这种生成策略，不需要手动设置ID，如果手动设置ID，则会使用自己设置的值。

###### 步骤3:运行新增方法  

![1631242753467](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Mybatisplus笔记/assets/1631242753467.png)

生成的ID就是一个Long类型的数据。

##### ASSIGN_UUID策略

###### 步骤1:设置生成策略为ASSIGN_UUID

使用uuid需要注意的是，主键的类型不能是Long，而应该改成String类型

```java
@Data
@TableName("tbl_user")
public class User {
    @TableId(type = IdType.ASSIGN_UUID)
    private String id;
    private String name;
    @TableField(value="pwd",select=false)
    private String password;
    private Integer age;
    private String tel;
    @TableField(exist=false)
    private Integer online;
}
```

###### 步骤2:修改表的主键类型

![1631243694870](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Mybatisplus笔记/assets/1631243694870.png)

主键类型设置为varchar，长度要大于32，因为UUID生成的主键为32位，如果长度小的话就会导致插入失败。

###### 步骤3:添加数据不设置ID

```java
@SpringBootTest
class Mybatisplus03DqlApplicationTests {

    @Autowired
    private UserDao userDao;
	
    @Test
    void testSave(){
        User user = new User();
        user.setName("黑马程序员");
        user.setPassword("itheima");
        user.setAge(12);
        user.setTel("4006184000");
        userDao.insert(user);
    }
}
```

###### 步骤4:运行新增方法

![1631243810974](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Mybatisplus笔记/assets/1631243810974.png)



接下来我们来聊一聊雪花算法:

雪花算法(SnowFlake),是Twitter官方给出的算法实现 是用Scala写的。其生成的结果是一个64bit大小整数，它的结构如下图:

![1631243987800](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Mybatisplus笔记/assets/1631243987800.png)

1. 1bit,不用,因为二进制中最高位是符号位，1表示负数，0表示正数。生成的id一般都是用整数，所以最高位固定为0。
2. 41bit-时间戳，用来记录时间戳，毫秒级
3. 10bit-工作机器id，用来记录工作机器id,其中高位5bit是数据中心ID其取值范围0-31，低位5bit是工作节点ID其取值范围0-31，两个组合起来最多可以容纳1024个节点
4. 序列号占用12bit，每个节点每毫秒0开始不断累加，最多可以累加到4095，一共可以产生4096个ID

#### 4.1.3 ID生成策略对比

介绍了这些主键ID的生成策略，我们以后该用哪个呢?

* NONE: 不设置id生成策略，MP不自动生成，约等于INPUT,所以这两种方式都需要用户手动设置，但是手动设置第一个问题是容易出现相同的ID造成主键冲突，为了保证主键不冲突就需要做很多判定，实现起来比较复杂
* AUTO:数据库ID自增,这种策略适合在数据库服务器只有1台的情况下使用,不可作为分布式ID使用
* ASSIGN_UUID:可以在分布式的情况下使用，而且能够保证唯一，但是生成的主键是32位的字符串，长度过长占用空间而且还不能排序，查询性能也慢
* ASSIGN_ID:可以在分布式的情况下使用，生成的是Long类型的数字，可以排序性能也高，但是生成的策略和服务器时间有关，如果修改了系统时间就有可能导致出现重复主键
* 综上所述，每一种主键策略都有自己的优缺点，根据自己项目业务的实际情况来选择使用才是最明智的选择。

#### 4.1.4 简化配置

前面我们已经完成了表关系映射、数据库主键策略的设置，接下来对于这两个内容的使用，我们再讲下他们的简化配置:

##### 模型类主键策略设置

对于主键ID的策略已经介绍完，但是如果要在项目中的每一个模型类上都需要使用相同的生成策略，如:![1631245676125](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Mybatisplus笔记/assets/1631245676125.png)

确实是稍微有点繁琐，我们能不能在某一处进行配置，就能让所有的模型类都可以使用该主键ID策略呢?

答案是肯定有，我们只需要在配置文件中添加如下内容:

```yml
mybatis-plus:
  global-config:
    db-config:
    	id-type: assign_id
```

配置完成后，每个模型类的主键ID策略都将成为assign_id.

##### 数据库表与模型类的映射关系

MP会默认将模型类的类名名首字母小写作为表名使用，假如数据库表的名称都以`tbl_`开头，那么我们就需要将所有的模型类上添加`@TableName`，如:

![1631245757169](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Mybatisplus笔记/assets/1631245757169.png)

配置起来还是比较繁琐，简化方式为在配置文件中配置如下内容:

```yml
mybatis-plus:
  global-config:
    db-config:
    	table-prefix: tbl_
```

设置表的前缀内容，这样MP就会拿 `tbl_`加上模型类的首字母小写，就刚好组装成数据库的表名。

### 4.2 多记录操作

先来看下问题:

![1631246166514](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Mybatisplus笔记/assets/1631246166514.png)

之前添加了很多商品到购物车，过了几天发现这些东西又不想要了，该怎么办呢?

很简单删除掉，但是一个个删除的话还是比较慢和费事的，所以一般会给用户一个批量操作，也就是前面有一个复选框，用户一次可以勾选多个也可以进行全选，然后删一次就可以将购物车清空，这个就需要用到`批量删除`的操作了。

具体该如何实现多条删除，我们找找对应的API方法

```java
int deleteBatchIds(@Param(Constants.COLLECTION) Collection<? extends Serializable> idList);
```

翻译方法的字面意思为:删除（根据ID 批量删除）,参数是一个集合，可以存放多个id值。

> 需求:根据传入的id集合将数据库表中的数据删除掉。

```java
@SpringBootTest
class Mybatisplus03DqlApplicationTests {

    @Autowired
    private UserDao userDao;
	
    @Test
    void testDelete(){
        //删除指定多条数据
        List<Long> list = new ArrayList<>();
        list.add(1402551342481838081L);
        list.add(1402553134049501186L);
        list.add(1402553619611430913L);
        userDao.deleteBatchIds(list);
    }
}
```

执行成功后，数据库表中的数据就会按照指定的id进行删除。

除了按照id集合进行批量删除，也可以按照id集合进行批量查询，还是先来看下API

```java
List<T> selectBatchIds(@Param(Constants.COLLECTION) Collection<? extends Serializable> idList);
```

方法名称翻译为:查询（根据ID 批量查询），参数是一个集合，可以存放多个id值。

> 需求：根据传入的ID集合查询用户信息

```java
@SpringBootTest
class Mybatisplus03DqlApplicationTests {

    @Autowired
    private UserDao userDao;
	
    @Test
    void testGetByIds(){
        //查询指定多条数据
        List<Long> list = new ArrayList<>();
        list.add(1L);
        list.add(3L);
        list.add(4L);
        userDao.selectBatchIds(list);
    }
}
```

查询结果就会按照指定传入的id值进行查询

![1631246688218](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Mybatisplus笔记/assets/1631246688218.png)

### 4.3 逻辑删除

接下来要讲解是删除中比较重要的一个操作，逻辑删除，先来分析下问题:

![1631246806130](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Mybatisplus笔记/assets/1631246806130.png)

* 这是一个员工和其所签的合同表，关系是一个员工可以签多个合同，是一个一(员工)对多(合同)的表

* 员工ID为1的张业绩，总共签了三个合同，如果此时他离职了，我们需要将员工表中的数据进行删除，会执行delete操作

* 如果表在设计的时候有主外键关系，那么同时也得将合同表中的前三条数据也删除掉

  ![1631246997190](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Mybatisplus笔记/assets/1631246997190.png)

* 后期要统计所签合同的总金额，就会发现对不上，原因是已经将员工1签的合同信息删除掉了

* 如果只删除员工不删除合同表数据，那么合同的员工编号对应的员工信息不存在，那么就会出现垃圾数据，就会出现无主合同，根本不知道有张业绩这个人的存在

* 所以经过分析，我们不应该将表中的数据删除掉，而是需要进行保留，但是又得把离职的人和在职的人进行区分，这样就解决了上述问题，如:

  ![1631247188218](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Mybatisplus笔记/assets/1631247188218.png)

* 区分的方式，就是在员工表中添加一列数据`deleted`，如果为0说明在职员工，如果离职则将其改完1，（0和1所代表的含义是可以自定义的）

所以对于删除操作业务问题来说有:

* 物理删除:业务数据从数据库中丢弃，执行的是delete操作
* 逻辑删除:为数据设置是否可用状态字段，删除时设置状态字段为不可用状态，数据保留在数据库中，执行的是update操作

MP中逻辑删除具体该如何实现?

#### 步骤1:修改数据库表添加`deleted`列

字段名可以任意，内容也可以自定义，比如`0`代表正常，`1`代表删除，可以在添加列的同时设置其默认值为`0`正常。

![1631247439168](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Mybatisplus笔记/assets/1631247439168.png)

#### 步骤2:实体类添加属性

(1)添加与数据库表的列对应的一个属性名，名称可以任意，如果和数据表列名对不上，可以使用@TableField进行关系映射，如果一致，则会自动对应。

(2)标识新增的字段为逻辑删除字段，使用`@TableLogic`

```java
@Data
//@TableName("tbl_user") 可以不写是因为配置了全局配置
public class User {
    @TableId(type = IdType.ASSIGN_UUID)
    private String id;
    private String name;
    @TableField(value="pwd",select=false)
    private String password;
    private Integer age;
    private String tel;
    @TableField(exist=false)
    private Integer online;
    @TableLogic(value="0",delval="1")
    //value为正常数据的值，delval为删除数据的值
    private Integer deleted;
}
```

#### 步骤3:运行删除方法

```java
@SpringBootTest
class Mybatisplus03DqlApplicationTests {

    @Autowired
    private UserDao userDao;
	
    @Test
    void testDelete(){
       userDao.deleteById(1L);
    }
}
```

![1631247818327](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Mybatisplus笔记/assets/1631247818327.png)

从测试结果来看，逻辑删除最后走的是update操作，会将指定的字段修改成删除状态对应的值。

**思考**

逻辑删除，对查询有没有影响呢?

* 执行查询操作

  ```java
  @SpringBootTest
  class Mybatisplus03DqlApplicationTests {
  
      @Autowired
      private UserDao userDao;
  	
      @Test
      void testFind(){
         System.out.println(userDao.selectList(null));
      }
  }
  ```

  运行测试，会发现打印出来的sql语句中会多一个查询条件，如:

  ![1631248019999](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Mybatisplus笔记/assets/1631248019999.png)

  可想而知，MP的逻辑删除会将所有的查询都添加一个未被删除的条件，也就是已经被删除的数据是不应该被查询出来的。

* 如果还是想把已经删除的数据都查询出来该如何实现呢?

  ```java
  @Mapper
  public interface UserDao extends BaseMapper<User> {
      //查询所有数据包含已经被删除的数据
      @Select("select * from tbl_user")
      public List<User> selectAll();
  }
  ```

* 如果每个表都要有逻辑删除，那么就需要在每个模型类的属性上添加`@TableLogic`注解，如何优化?

  在配置文件中添加全局配置，如下:

  ```yml
  mybatis-plus:
    global-config:
      db-config:
        # 逻辑删除字段名
        logic-delete-field: deleted
        # 逻辑删除字面值：未删除为0
        logic-not-delete-value: 0
        # 逻辑删除字面值：删除为1
        logic-delete-value: 1
  ```

介绍完逻辑删除，逻辑删除的本质为:

**逻辑删除的本质其实是修改操作。如果加了逻辑删除字段，查询数据时也会自动带上逻辑删除字段。**

执行的SQL语句为:

UPDATE tbl_user SET ==deleted===1 where id = ? AND ==deleted===0

执行数据结果为:

![1631248494929](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Mybatisplus笔记/assets/1631248494929.png)



#### 知识点1：@TableLogic

| 名称     | @TableLogic                               |
| -------- | ----------------------------------------- |
| 类型     | ==属性注解==                              |
| 位置     | 模型类中用于表示删除字段的属性定义上方    |
| 作用     | 标识该字段为进行逻辑删除的字段            |
| 相关属性 | value：逻辑未删除值<br/>delval:逻辑删除值 |

### 4.4 乐观锁

#### 4.4.1 概念

在讲解乐观锁之前，我们还是先来分析下问题:

业务并发现象带来的问题:==秒杀==

* 假如有100个商品或者票在出售，为了能保证每个商品或者票只能被一个人购买，如何保证不会出现超买或者重复卖
* 对于这一类问题，其实有很多的解决方案可以使用
* 第一个最先想到的就是锁，锁在一台服务器中是可以解决的，但是如果在多台服务器下锁就没有办法控制，比如12306有两台服务器在进行卖票，在两台服务器上都添加锁的话，那也有可能会导致在同一时刻有两个线程在进行卖票，还是会出现并发问题
* 我们接下来介绍的这种方式是针对于小型企业的解决方案，因为数据库本身的性能就是个瓶颈，如果对其并发量超过2000以上的就需要考虑其他的解决方案了。

简单来说，乐观锁主要解决的问题是当要更新一条记录的时候，希望这条记录没有被别人更新。

#### 4.4.2 实现思路

乐观锁的实现方式:

> * 数据库表中添加version列，比如默认值给1
> * 第一个线程要修改数据之前，取出记录时，获取当前数据库中的version=1
> * 第二个线程要修改数据之前，取出记录时，获取当前数据库中的version=1
> * 第一个线程执行更新时，set version = newVersion where version = oldVersion
>   * newVersion = version+1  [2]
>   * oldVersion = version  [1]
> * 第二个线程执行更新时，set version = newVersion where version = oldVersion
>   * newVersion = version+1  [2]
>   * oldVersion = version  [1]
> * 假如这两个线程都来更新数据，第一个和第二个线程都可能先执行
>   * 假如第一个线程先执行更新，会把version改为2，
>   * 第二个线程再更新的时候，set version = 2 where version = 1,此时数据库表的数据version已经为2，所以第二个线程会修改失败
>   * 假如第二个线程先执行更新，会把version改为2，
>   * 第一个线程再更新的时候，set version = 2 where version = 1,此时数据库表的数据version已经为2，所以第一个线程会修改失败
>   * 不管谁先执行都会确保只能有一个线程更新数据，这就是MP提供的乐观锁的实现原理分析。

上面所说的步骤具体该如何实现呢?

#### 4.4.3 实现步骤

分析完步骤后，具体的实现步骤如下:

##### 步骤1:数据库表添加列

列名可以任意，比如使用`version`,给列设置默认值为`1`

![1631249913103](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Mybatisplus笔记/assets/1631249913103.png)

##### 步骤2:在模型类中添加对应的属性

根据添加的字段列名，在模型类中添加对应的属性值

```java
@Data
//@TableName("tbl_user") 可以不写是因为配置了全局配置
public class User {
    @TableId(type = IdType.ASSIGN_UUID)
    private String id;
    private String name;
    @TableField(value="pwd",select=false)
    private String password;
    private Integer age;
    private String tel;
    @TableField(exist=false)
    private Integer online;
    private Integer deleted;
    @Version
    private Integer version;
}
```

##### 步骤3:添加乐观锁的拦截器

```java
@Configuration
public class MpConfig {
    @Bean
    public MybatisPlusInterceptor mpInterceptor() {
        //1.定义Mp拦截器
        MybatisPlusInterceptor mpInterceptor = new MybatisPlusInterceptor();
        //2.添加乐观锁拦截器
        mpInterceptor.addInnerInterceptor(new OptimisticLockerInnerInterceptor());
        return mpInterceptor;
    }
}
```

##### 步骤4:执行更新操作

```java
@SpringBootTest
class Mybatisplus03DqlApplicationTests {

    @Autowired
    private UserDao userDao;
	
    @Test
    void testUpdate(){
       User user = new User();
        user.setId(3L);
        user.setName("Jock666");
        userDao.updateById(user);
    }
}
```

![1631252305080](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Mybatisplus笔记/assets/1631252305080.png)

你会发现，这次修改并没有更新version字段，原因是没有携带version数据。

添加version数据

```java
@SpringBootTest
class Mybatisplus03DqlApplicationTests {

    @Autowired
    private UserDao userDao;
	
    @Test
    void testUpdate(){
        User user = new User();
        user.setId(3L);
        user.setName("Jock666");
        user.setVersion(1);
        userDao.updateById(user);
    }
}
```

![1631252393659](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Mybatisplus笔记/assets/1631252393659.png)

你会发现，我们传递的是1，MP会将1进行加1，然后，更新回到数据库表中。

所以要想实现乐观锁，首先第一步应该是拿到表中的version，然后拿version当条件在将version加1更新回到数据库表中，所以我们在查询的时候，需要对其进行查询

```java
@SpringBootTest
class Mybatisplus03DqlApplicationTests {

    @Autowired
    private UserDao userDao;
	
    @Test
    void testUpdate(){
        //1.先通过要修改的数据id将当前数据查询出来
        User user = userDao.selectById(3L);
        //2.将要修改的属性逐一设置进去
        user.setName("Jock888");
        userDao.updateById(user);
    }
}
```

![1631252667865](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Mybatisplus笔记/assets/1631252667865.png)

大概分析完乐观锁的实现步骤以后，我们来模拟一种加锁的情况，看看能不能实现多个人修改同一个数据的时候，只能有一个人修改成功。

```java
@SpringBootTest
class Mybatisplus03DqlApplicationTests {

    @Autowired
    private UserDao userDao;
	
    @Test
    void testUpdate(){
       //1.先通过要修改的数据id将当前数据查询出来
        User user = userDao.selectById(3L);     //version=3
        User user2 = userDao.selectById(3L);    //version=3
        user2.setName("Jock aaa");
        userDao.updateById(user2);              //version=>4
        user.setName("Jock bbb");
        userDao.updateById(user);               //verion=3?条件还成立吗？
    }
}
```

运行程序，分析结果：

![1631253302587](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Mybatisplus笔记/assets/1631253302587.png)

乐观锁就已经实现完成了，如果对于上面的这些步骤记不住咋办呢?

参考官方文档来实现:

`https://mp.baomidou.com/guide/interceptor-optimistic-locker.html#optimisticlockerinnerinterceptor`

![1631253387845](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Mybatisplus笔记/assets/1631253387845.png)

## 5，快速开发

### 5.1 代码生成器原理分析

造句:![1631253928893](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Mybatisplus笔记/assets/1631253928893.png)

我们可以往空白内容进行填词造句，比如:![1631253971409](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Mybatisplus笔记/assets/1631253971409.png)

在比如:![1631253994782](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Mybatisplus笔记/assets/1631253994782.png)

观察我们之前写的代码，会发现其中也会有很多重复内容，比如:

![1631254075651](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Mybatisplus笔记/assets/1631254075651.png)

那我们就想，如果我想做一个Book模块的开发，是不是只需要将红色部分的内容全部更换成`Book`即可，如：

![1631254119948](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Mybatisplus笔记/assets/1631254119948.png)

所以我们会发现，做任何模块的开发，对于这段代码，基本上都是对红色部分的调整，所以我们把去掉红色内容的东西称之为==模板==，红色部分称之为==参数==，以后只需要传入不同的参数，就可以根据模板创建出不同模块的dao代码。

除了Dao可以抽取模块，其实我们常见的类都可以进行抽取，只要他们有公共部分即可。再来看下模型类的模板：

![1631254344180](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Mybatisplus笔记/assets/1631254344180.png)

* ① 可以根据数据库表的表名来填充
* ② 可以根据用户的配置来生成ID生成策略
* ③到⑨可以根据数据库表字段名称来填充

所以只要我们知道是对哪张表进行代码生成，这些内容我们都可以进行填充。

分析完后，我们会发现，要想完成代码自动生成，我们需要有以下内容:

* 模板: MyBatisPlus提供，可以自己提供，但是麻烦，不建议
* 数据库相关配置:读取数据库获取表和字段信息
* 开发者自定义配置:手工配置，比如ID生成策略

### 5.2 代码生成器实现

#### 步骤1:创建一个Maven项目

#### 代码2:导入对应的jar包

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.5.1</version>
    </parent>
    <groupId>com.itheima</groupId>
    <artifactId>mybatisplus_04_generator</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <properties>
        <java.version>1.8</java.version>
    </properties>
    <dependencies>
        <!--spring webmvc-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>

        <!--mybatisplus-->
        <dependency>
            <groupId>com.baomidou</groupId>
            <artifactId>mybatis-plus-boot-starter</artifactId>
            <version>3.4.1</version>
        </dependency>

        <!--druid-->
        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>druid</artifactId>
            <version>1.1.16</version>
        </dependency>

        <!--mysql-->
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <scope>runtime</scope>
        </dependency>

        <!--test-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>

        <!--lombok-->
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <version>1.18.12</version>
        </dependency>

        <!--代码生成器-->
        <dependency>
            <groupId>com.baomidou</groupId>
            <artifactId>mybatis-plus-generator</artifactId>
            <version>3.4.1</version>
        </dependency>

        <!--velocity模板引擎-->
        <dependency>
            <groupId>org.apache.velocity</groupId>
            <artifactId>velocity-engine-core</artifactId>
            <version>2.3</version>
        </dependency>

    </dependencies>

    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>

</project>

```

#### 步骤3:编写引导类

```java
@SpringBootApplication
public class Mybatisplus04GeneratorApplication {

    public static void main(String[] args) {
        SpringApplication.run(Mybatisplus04GeneratorApplication.class, args);
    }

}
```

#### 步骤4:创建代码生成类

```java
public class CodeGenerator {
    public static void main(String[] args) {
        //1.获取代码生成器的对象
        AutoGenerator autoGenerator = new AutoGenerator();

        //设置数据库相关配置
        DataSourceConfig dataSource = new DataSourceConfig();
        dataSource.setDriverName("com.mysql.cj.jdbc.Driver");
        dataSource.setUrl("jdbc:mysql://localhost:3306/mybatisplus_db?serverTimezone=UTC");
        dataSource.setUsername("root");
        dataSource.setPassword("root");
        autoGenerator.setDataSource(dataSource);

        //设置全局配置
        GlobalConfig globalConfig = new GlobalConfig();
        globalConfig.setOutputDir(System.getProperty("user.dir")+"/mybatisplus_04_generator/src/main/java");    //设置代码生成位置
        globalConfig.setOpen(false);    //设置生成完毕后是否打开生成代码所在的目录
        globalConfig.setAuthor("黑马程序员");    //设置作者
        globalConfig.setFileOverride(true);     //设置是否覆盖原始生成的文件
        globalConfig.setMapperName("%sDao");    //设置数据层接口名，%s为占位符，指代模块名称
        globalConfig.setIdType(IdType.ASSIGN_ID);   //设置Id生成策略
        autoGenerator.setGlobalConfig(globalConfig);

        //设置包名相关配置
        PackageConfig packageInfo = new PackageConfig();
        packageInfo.setParent("com.aaa");   //设置生成的包名，与代码所在位置不冲突，二者叠加组成完整路径
        packageInfo.setEntity("domain");    //设置实体类包名
        packageInfo.setMapper("dao");   //设置数据层包名
        autoGenerator.setPackageInfo(packageInfo);

        //策略设置
        StrategyConfig strategyConfig = new StrategyConfig();
        strategyConfig.setInclude("tbl_user");  //设置当前参与生成的表名，参数为可变参数
        strategyConfig.setTablePrefix("tbl_");  //设置数据库表的前缀名称，模块名 = 数据库表名 - 前缀名  例如： User = tbl_user - tbl_
        strategyConfig.setRestControllerStyle(true);    //设置是否启用Rest风格
        strategyConfig.setVersionFieldName("version");  //设置乐观锁字段名
        strategyConfig.setLogicDeleteFieldName("deleted");  //设置逻辑删除字段名
        strategyConfig.setEntityLombokModel(true);  //设置是否启用lombok
        autoGenerator.setStrategy(strategyConfig);
        //2.执行生成操作
        autoGenerator.execute();
    }
}
```

对于代码生成器中的代码内容，我们可以直接从官方文档中获取代码进行修改，

`https://mp.baomidou.com/guide/generator.html`

#### 步骤5:运行程序

运行成功后，会在当前项目中生成很多代码，代码包含`controller`,`service`，`mapper`和`entity`

![1631255110375](D:/BaiduNetdiskDownload/课程笔记/基础框架笔记/基础框架8笔记/Mybatisplus笔记/assets/1631255110375.png)

至此代码生成器就已经完成工作，我们能快速根据数据库表来创建对应的类，简化我们的代码开发。

### 5.3 MP中Service的CRUD

回顾我们之前业务层代码的编写，编写接口和对应的实现类:

```java
public interface UserService{
	
}

@Service
public class UserServiceImpl implements UserService{

}
```

接口和实现类有了以后，需要在接口和实现类中声明方法

```java
public interface UserService{
	public List<User> findAll();
}

@Service
public class UserServiceImpl implements UserService{
    @Autowired
    private UserDao userDao;
    
	public List<User> findAll(){
        return userDao.selectList(null);
    }
}
```

MP看到上面的代码以后就说这些方法也是比较固定和通用的，那我来帮你抽取下，所以MP提供了一个Service接口和实现类，分别是:`IService`和`ServiceImpl`,后者是对前者的一个具体实现。

以后我们自己写的Service就可以进行如下修改:

```java
public interface UserService extends IService<User>{
	
}

@Service
public class UserServiceImpl extends ServiceImpl<UserDao, User> implements UserService{

}
```

修改以后的好处是，MP已经帮我们把业务层的一些基础的增删改查都已经实现了，可以直接进行使用。

编写测试类进行测试:

```java
@SpringBootTest
class Mybatisplus04GeneratorApplicationTests {

    private IUserService userService;

    @Test
    void testFindAll() {
        List<User> list = userService.list();
        System.out.println(list);
    }

}
```

**注意:**mybatisplus_04_generator项目中对于MyBatis的环境是没有进行配置，如果想要运行，需要提取将配置文件中的内容进行完善后在运行。

思考:在MP封装的Service层都有哪些方法可以用?

查看官方文档:`https://mp.baomidou.com/guide/crud-interface.html`,这些提供的方法大家可以参考官方文档进行学习使用，方法的名称可能有些变化，但是方法对应的参数和返回值基本类似。

# SpringBoot

**今日目标：**

> * 掌握基于SpringBoot框架的程序开发步骤
> * 熟练使用SpringBoot配置信息修改服务器配置
> * 基于SpringBoot的完成SSM整合项目开发

## 1，SpringBoot简介

`SpringBoot` 是由 `Pivotal` 团队提供的全新框架，其设计目的是用来==简化== `Spring` 应用的==初始搭建==以及==开发过程==。

使用了 `Spring` 框架后已经简化了我们的开发。而 `SpringBoot` 又是对 `Spring` 开发进行简化的，可想而知 `SpringBoot` 使用的简单及广泛性。既然 `SpringBoot` 是用来简化 `Spring` 开发的，那我们就先回顾一下，以 `SpringMVC` 开发为例：

1. **创建工程，并在 `pom.xml` 配置文件中配置所依赖的坐标**

<img src="D:\BaiduNetdiskDownload\课程笔记\基础框架笔记\基础框架8笔记\SpringBoot笔记\assets\image-20210911132335452.png" alt="image-20210911132335452" style="zoom:50%;" />

2. **编写 `web3.0` 的配置类**

   作为 `web` 程序，`web3.0` 的配置类不能缺少，而这个配置类还是比较麻烦的，代码如下

<img src="D:\BaiduNetdiskDownload\课程笔记\基础框架笔记\基础框架8笔记\SpringBoot笔记\assets\image-20210911133112602.png" alt="image-20210911133112602" style="zoom:50%;" />

3. **编写 `SpringMVC` 的配置类**

<img src="D:\BaiduNetdiskDownload\课程笔记\基础框架笔记\基础框架8笔记\SpringBoot笔记\assets\image-20210911133219847.png" alt="image-20210911133219847" style="zoom:50%;" />

​	做到这只是将工程的架子搭起来。要想被外界访问，最起码还需要提供一个 `Controller` 类，在该类中提供一个方法。

4. **编写 `Controller` 类**

<img src="D:\BaiduNetdiskDownload\课程笔记\基础框架笔记\基础框架8笔记\SpringBoot笔记\assets\image-20210911133532151.png" alt="image-20210911133532151" style="zoom:50%;" />

从上面的 `SpringMVC` 程序开发可以看到，前三步都是在搭建环境，而且这三步基本都是固定的。`SpringBoot` 就是对这三步进行简化了。接下来我们通过一个入门案例来体现 `SpingBoot` 简化 `Spring` 开发。

### 1.1  SpringBoot快速入门

#### 1.1.1  开发步骤

`SpringBoot` 开发起来特别简单，分为如下几步：

* 创建新模块，选择Spring初始化，并配置模块相关基础信息
* 选择当前模块需要使用的技术集
* 开发控制器类
* 运行自动生成的Application类

知道了 `SpringBoot` 的开发步骤后，接下来我们进行具体的操作

##### 1.1.1.1  创建新模块

* 点击 `+` 选择 `New Module` 创建新模块

<img src="D:\BaiduNetdiskDownload\课程笔记\基础框架笔记\基础框架8笔记\SpringBoot笔记\assets\image-20210911155135008.png" alt="image-20210911155135008" style="zoom:60%;" />

* 选择 `Spring Initializr` ，用来创建 `SpringBoot` 工程

  以前我们选择的是 `Maven` ，今天选择 `Spring Initializr` 来快速构建 `SpringBoot` 工程。而在 `Module SDK` 这一项选择我们安装的 `JDK` 版本。

<img src="D:\BaiduNetdiskDownload\课程笔记\基础框架笔记\基础框架8笔记\SpringBoot笔记\assets\image-20210911155249493.png" alt="image-20210911155249493" style="zoom:60%;" />

* 对 `SpringBoot` 工程进行相关的设置

  我们使用这种方式构建的 `SpringBoot` 工程其实也是 `Maven` 工程，而该方式只是一种快速构建的方式而已。

  <img src="D:\BaiduNetdiskDownload\课程笔记\基础框架笔记\基础框架8笔记\SpringBoot笔记\assets\image-20210911155916899.png" alt="image-20210911155916899" style="zoom:67%;" />

  > ==注意：打包方式这里需要设置为 `Jar`==

* 选中 `Web`，然后勾选 `Spring Web`

  由于我们需要开发一个 `web` 程序，使用到了 `SpringMVC` 技术，所以按照下图红框进行勾选

<img src="D:\BaiduNetdiskDownload\课程笔记\基础框架笔记\基础框架8笔记\SpringBoot笔记\assets\image-20210911160040328.png" alt="image-20210911160040328" style="zoom:60%;" />

* 下图界面不需要任何修改，直接点击 `Finish` 完成 `SpringBoot` 工程的构建

<img src="D:\BaiduNetdiskDownload\课程笔记\基础框架笔记\基础框架8笔记\SpringBoot笔记\assets\image-20210911160353534.png" alt="image-20210911160353534" style="zoom:70%;" />

经过以上步骤后就创建了如下结构的模块，它会帮我们自动生成一个 `Application` 类，而该类一会再启动服务器时会用到

<img src="D:\BaiduNetdiskDownload\课程笔记\基础框架笔记\基础框架8笔记\SpringBoot笔记\assets\image-20210911160541833.png" alt="image-20210911160541833" style="zoom:80%;" />

> ==注意：==
>
> 1. 在创建好的工程中不需要创建配置类
>
> 2. 创建好的项目会自动生成其他的一些文件，而这些文件目前对我们来说没有任何作用，所以可以将这些文件删除。
>
>    可以删除的目录和文件如下：
>
>    * `.mvn`	
>    * `.gitignore`
>    * `HELP.md`
>    * `mvnw`
>    * `mvnw.cmd`

##### 1.1.1.2  创建 `Controller`

在  `com.itheima.controller` 包下创建 `BookController` ，代码如下：

```java
@RestController
@RequestMapping("/books")
public class BookController {

    @GetMapping("/{id}")
    public String getById(@PathVariable Integer id){
        System.out.println("id ==> "+id);
        return "hello , spring boot!";
    }
}
```

##### 1.1.1.3  启动服务器

运行 `SpringBoot` 工程不需要使用本地的 `Tomcat` 和 插件，只运行项目 `com.itheima` 包下的 `Application` 类，我们就可以在控制台看出如下信息

![image-20210911165642280](D:\BaiduNetdiskDownload\课程笔记\基础框架笔记\基础框架8笔记\SpringBoot笔记\assets\image-20210911165642280.png)

##### 1.1.1.4  进行测试

使用 `Postman` 工具来测试我们的程序

![image-20210911160850121](D:\BaiduNetdiskDownload\课程笔记\基础框架笔记\基础框架8笔记\SpringBoot笔记\assets\image-20210911160850121.png)

通过上面的入门案例我们可以看到使用 `SpringBoot` 进行开发，使整个开发变得很简单，那它是如何做到的呢？

要研究这个问题，我们需要看看 `Application` 类和 `pom.xml` 都书写了什么。先看看 `Applicaion` 类，该类内容如下：

```java
@SpringBootApplication
public class Application {
    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }
}
```

这个类中的东西很简单，就在类上添加了一个 `@SpringBootApplication` 注解，而在主方法中就一行代码。我们在启动服务器时就是执行的该类中的主方法。

再看看 `pom.xml` 配置文件中的内容

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    
    <!--指定了一个父工程，父工程中的东西在该工程中可以继承过来使用-->
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.5.0</version>
    </parent>
    <groupId>com.itheima</groupId>
    <artifactId>springboot_01_quickstart</artifactId>
    <version>0.0.1-SNAPSHOT</version>

    <!--JDK 的版本-->
    <properties>
        <java.version>8</java.version>
    </properties>
    
    <dependencies>
        <!--该依赖就是我们在创建 SpringBoot 工程勾选的那个 Spring Web 产生的-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
		<!--这个是单元测试的依赖，我们现在没有进行单元测试，所以这个依赖现在可以没有-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
    </dependencies>

    <build>
        <plugins>
            <!--这个插件是在打包时需要的，而这里暂时还没有用到-->
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>
</project>
```

我们代码之所以能简化，就是因为指定的父工程和 `Spring Web` 依赖实现的。具体的我们后面在聊。

#### 1.1.2  对比

做完 `SpringBoot` 的入门案例后，接下来对比一下 `Spring` 程序和 `SpringBoot` 程序。如下图

<img src="D:\BaiduNetdiskDownload\课程笔记\基础框架笔记\基础框架8笔记\SpringBoot笔记\assets\image-20210911172200292.png" alt="image-20210911172200292" style="zoom:60%;" />

* **坐标**

  `Spring` 程序中的坐标需要自己编写，而且坐标非常多

  `SpringBoot` 程序中的坐标是我们在创建工程时进行勾选自动生成的

* **web3.0配置类**

  `Spring` 程序需要自己编写这个配置类。这个配置类大家之前编写过，肯定感觉很复杂

  `SpringBoot` 程序不需要我们自己书写

* **配置类**

  `Spring/SpringMVC` 程序的配置类需要自己书写。而 `SpringBoot`  程序则不需要书写。

> ==注意：基于Idea的 `Spring Initializr` 快速构建 `SpringBoot` 工程时需要联网。== 

#### 1.1.3  官网构建工程

在入门案例中之所以能快速构建 `SpringBoot` 工程，是因为 `Idea` 使用了官网提供了快速构建 `SpringBoot` 工程的组件实现的。那如何在官网进行工程构建呢？通过如下步骤构建

##### 1.1.3.1  进入SpringBoot官网

官网地址如下：

```
https://spring.io/projects/spring-boot
```

进入到 `SpringBoot` 官网后拖到最下方就可以看到如下内容

<img src="D:\BaiduNetdiskDownload\课程笔记\基础框架笔记\基础框架8笔记\SpringBoot笔记\assets\image-20210911173712014.png" alt="image-20210911173712014" style="zoom:60%;" />

然后点击 `Spring Initializr` 超链接就会跳转到如下页面

![image-20210911174110687](D:\BaiduNetdiskDownload\课程笔记\基础框架笔记\基础框架8笔记\SpringBoot笔记\assets\image-20210911174110687.png)

这个页面内容是不是感觉很眼熟的，这和我们使用 `Idea` 快速构建 `SpringBoot` 工程的界面基本相同。在上面页面输入对应的信息

##### 1.1.3.2  选择依赖

选择 `Spring Web` 可以点击上图右上角的 `ADD DEPENDENCIES... CTRL + B` 按钮，就会出现如下界面

![image-20210911174650679](D:\BaiduNetdiskDownload\课程笔记\基础框架笔记\基础框架8笔记\SpringBoot笔记\assets\image-20210911174650679.png)

##### 1.1.3.3  生成工程

以上步骤完成后就可以生成 `SpringBoot` 工程了。在页面的最下方点击 `GENERATE CTRL + 回车` 按钮生成工程并下载到本地，如下图所示

![image-20210911175222857](D:\BaiduNetdiskDownload\课程笔记\基础框架笔记\基础框架8笔记\SpringBoot笔记\assets\image-20210911175222857.png)

打开下载好的压缩包可以看到工程结构和使用 `Idea` 生成的一模一样，如下图

<img src="D:\BaiduNetdiskDownload\课程笔记\基础框架笔记\基础框架8笔记\SpringBoot笔记\assets\image-20210911175502834.png" alt="image-20210911175502834" style="zoom:80%;" />

而打开 `pom.xml` 文件，里面也包含了父工程和 `Spring Web` 的依赖。

通过上面官网的操作，我们知道 `Idea` 中快速构建 `SpringBoot` 工程其实就是使用的官网的快速构建组件，那以后即使没有 `Idea` 也可以使用官网的方式构建 `SpringBoot` 工程。

#### 1.1.4  SpringBoot工程快速启动

##### 1.1.4.1  问题导入

<img src="D:\BaiduNetdiskDownload\课程笔记\基础框架笔记\基础框架8笔记\SpringBoot笔记\assets\image-20210911180828611.png" alt="image-20210911180828611" style="zoom:50%;" />

以后我们和前端开发人员协同开发，而前端开发人员需要测试前端程序就需要后端开启服务器，这就受制于后端开发人员。为了摆脱这个受制，前端开发人员尝试着在自己电脑上安装 `Tomcat` 和 `Idea` ，在自己电脑上启动后端程序，这显然不现实。

我们后端可以将 `SpringBoot` 工程打成 `jar` 包，该 `jar` 包运行不依赖于 `Tomcat` 和 `Idea` 这些工具也可以正常运行，只是这个 `jar` 包在运行过程中连接和我们自己程序相同的 `Mysql` 数据库即可。这样就可以解决这个问题，如下图

<img src="D:\BaiduNetdiskDownload\课程笔记\基础框架笔记\基础框架8笔记\SpringBoot笔记\assets\image-20210911181714437.png" alt="image-20210911181714437" style="zoom:50%;" />

那现在问题是如何打包呢？

##### 1.1.4.2  打包

由于我们在构建 `SpringBoot` 工程时已经在 `pom.xml` 中配置了如下插件

```xml
<plugin>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-maven-plugin</artifactId>
</plugin>
```

所以我们只需要使用 `Maven` 的 `package` 指令打包就会在 `target` 目录下生成对应的 `Jar` 包。

> ==注意：该插件必须配置，不然打好的 `jar` 包也是有问题的。==

##### 1.1.4.3  启动

进入 `jar` 包所在位置，在 `命令提示符` 中输入如下命令

```shell
jar -jar springboot_01_quickstart-0.0.1-SNAPSHOT.jar
```

执行上述命令就可以看到 `SpringBoot` 运行的日志信息

<img src="D:\BaiduNetdiskDownload\课程笔记\基础框架笔记\基础框架8笔记\SpringBoot笔记\assets\image-20210911182956629.png" alt="image-20210911182956629" style="zoom:60%;" />

### 1.2  SpringBoot概述

`SpringBoot` 是由Pivotal团队提供的全新框架，其设计目的是用来==简化==Spring应用的==初始搭建==以及==开发过程==。

大家已经感受了 `SpringBoot` 程序，回过头看看 `SpringBoot` 主要作用是什么，就是简化 `Spring` 的搭建过程和开发过程。

原始 `Spring` 环境搭建和开发存在以下问题：

* 配置繁琐
* 依赖设置繁琐

`SpringBoot` 程序优点恰巧就是针对 `Spring` 的缺点

* 自动配置。这个是用来解决 `Spring` 程序配置繁琐的问题
* 起步依赖。这个是用来解决 `Spring` 程序依赖设置繁琐的问题
* 辅助功能（内置服务器,...）。我们在启动 `SpringBoot` 程序时既没有使用本地的 `tomcat` 也没有使用 `tomcat` 插件，而是使用 `SpringBoot` 内置的服务器。

接下来我们来说一下 `SpringBoot` 的起步依赖

#### 1.2.1  起步依赖

我们使用 `Spring Initializr`  方式创建的 `Maven` 工程的的 `pom.xml` 配置文件中自动生成了很多包含 `starter` 的依赖，如下图

<img src="D:\BaiduNetdiskDownload\课程笔记\基础框架笔记\基础框架8笔记\SpringBoot笔记\assets\image-20210918220338109.png" alt="image-20210918220338109" style="zoom:70%;" />

这些依赖就是==启动依赖==，接下来我们探究一下他是如何实现的。

##### 1.2.1.1  探索父工程

从上面的文件中可以看到指定了一个父工程，我们进入到父工程，发现父工程中又指定了一个父工程，如下图所示

<img src="D:\BaiduNetdiskDownload\课程笔记\基础框架笔记\基础框架8笔记\SpringBoot笔记\assets\image-20210918220855024.png" alt="image-20210918220855024" style="zoom:80%;" />

再进入到该父工程中，在该工程中我们可以看到配置内容结构如下图所示

<img src="D:\BaiduNetdiskDownload\课程笔记\基础框架笔记\基础框架8笔记\SpringBoot笔记\assets\image-20210918221042947.png" alt="image-20210918221042947" style="zoom:80%;" />

上图中的 `properties` 标签中定义了各个技术软件依赖的版本，避免了我们在使用不同软件技术时考虑版本的兼容问题。在 `properties` 中我们找 `servlet`  和 `mysql` 的版本如下图

<img src="D:\BaiduNetdiskDownload\课程笔记\基础框架笔记\基础框架8笔记\SpringBoot笔记\assets\image-20210918221511249.png" alt="image-20210918221511249" style="zoom:80%;" />

`dependencyManagement` 标签是进行依赖版本锁定，但是并没有导入对应的依赖；如果我们工程需要那个依赖只需要引入依赖的 `groupid` 和 `artifactId` 不需要定义 `version`。

而 `build` 标签中也对插件的版本进行了锁定，如下图

<img src="D:\BaiduNetdiskDownload\课程笔记\基础框架笔记\基础框架8笔记\SpringBoot笔记\assets\image-20210918221942453.png" alt="image-20210918221942453" style="zoom:80%;" />

看完了父工程中 `pom.xml` 的配置后不难理解我们工程的的依赖为什么都没有配置 `version`。

##### 1.2.1.2  探索依赖

在我们创建的工程中的 `pom.xml` 中配置了如下依赖

<img src="D:\BaiduNetdiskDownload\课程笔记\基础框架笔记\基础框架8笔记\SpringBoot笔记\assets\image-20210918222321402.png" alt="image-20210918222321402" style="zoom:80%;" />

进入到该依赖，查看 `pom.xml` 的依赖会发现它引入了如下的依赖

<img src="D:\BaiduNetdiskDownload\课程笔记\基础框架笔记\基础框架8笔记\SpringBoot笔记\assets\image-20210918222607469.png" alt="image-20210918222607469" style="zoom:80%;" />

里面的引入了 `spring-web` 和 `spring-webmvc` 的依赖，这就是为什么我们的工程中没有依赖这两个包还能正常使用 `springMVC` 中的注解的原因。

而依赖 `spring-boot-starter-tomcat` ，从名字基本能确认内部依赖了 `tomcat`，所以我们的工程才能正常启动。

==结论：以后需要使用技术，只需要引入该技术对应的起步依赖即可==

##### 1.2.1.3  小结

**starter**

* `SpringBoot` 中常见项目名称，定义了当前项目使用的所有项目坐标，以达到减少依赖配置的目的

**parent**

* 所有 `SpringBoot` 项目要继承的项目，定义了若干个坐标版本号（依赖管理，而非依赖），以达到减少依赖冲突的目的

* `spring-boot-starter-parent`（2.5.0）与 `spring-boot-starter-parent`（2.4.6）共计57处坐标版本不同

**实际开发**

* 使用任意坐标时，仅书写GAV中的G和A，V由SpringBoot提供

  > G：groupid
  >
  > A：artifactId
  >
  > V：version

* 如发生坐标错误，再指定version（要小心版本冲突）

#### 1.2.2  程序启动

创建的每一个 `SpringBoot` 程序时都包含一个类似于下面的类，我们将这个类称作引导类

```java
@SpringBootApplication
public class Springboot01QuickstartApplication {
    
    public static void main(String[] args) {
        SpringApplication.run(Springboot01QuickstartApplication.class, args);
    }
}
```

==注意：==

* `SpringBoot` 在创建项目时，采用jar的打包方式

* `SpringBoot` 的引导类是项目的入口，运行 `main` 方法就可以启动项目

  因为我们在 `pom.xml` 中配置了 `spring-boot-starter-web` 依赖，而该依赖通过前面的学习知道它依赖 `tomcat` ，所以运行 `main` 方法就可以使用 `tomcat` 启动咱们的工程。

#### 1.2.3  切换web服务器

现在我们启动工程使用的是 `tomcat` 服务器，那能不能不使用 `tomcat` 而使用 `jetty` 服务器，`jetty` 在我们 `maven` 高级时讲 `maven` 私服使用的服务器。而要切换 `web` 服务器就需要将默认的 `tomcat` 服务器给排除掉，怎么排除呢？使用 `exclusion` 标签

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
    <exclusions>
        <exclusion>
            <artifactId>spring-boot-starter-tomcat</artifactId>
            <groupId>org.springframework.boot</groupId>
        </exclusion>
    </exclusions>
</dependency>
```

现在我们运行引导类可以吗？运行一下试试，打印的日志信息如下

![image-20210918232512707](D:\BaiduNetdiskDownload\课程笔记\基础框架笔记\基础框架8笔记\SpringBoot笔记\assets\image-20210918232512707.png)

程序直接停止了，为什么呢？那是因为排除了 `tomcat` 服务器，程序中就没有服务器了。所以此时不光要排除 `tomcat` 服务器，还要引入 `jetty` 服务器。在 `pom.xml` 中因为 `jetty` 的起步依赖

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-jetty</artifactId>
</dependency>
```

接下来再次运行引导类，在日志信息中就可以看到使用的是 `jetty` 服务器

![image-20210918232904623](D:\BaiduNetdiskDownload\课程笔记\基础框架笔记\基础框架8笔记\SpringBoot笔记\assets\image-20210918232904623.png)

**小结：**

通过切换服务器，我们不难发现在使用 `SpringBoot` 换技术时只需要导入该技术的起步依赖即可。

## 2，配置文件

### 2.1  配置文件格式

我们现在启动服务器默认的端口号是 `8080`，访问路径可以书写为

```
http://localhost:8080/books/1
```

在线上环境我们还是希望将端口号改为 `80`，这样在访问的时候就可以不写端口号了，如下

```
http://localhost/books/1
```

而 `SpringBoot` 程序如何修改呢？`SpringBoot` 提供了多种属性配置方式

* `application.properties`

  ```
  server.port=80
  ```

* `application.yml`

  ```yaml
  server:
  	port: 81
  ```

* `application.yaml`

  ```yaml
  server:
  	port: 82
  ```

> ==注意：`SpringBoot` 程序的配置文件名必须是 `application` ，只是后缀名不同而已。==

#### 2.1.1  环境准备

创建一个新工程 `springboot_02_base_config` 用来演示不同的配置文件，工程环境和入门案例一模一样，结构如下：

<img src="D:\BaiduNetdiskDownload\课程笔记\基础框架笔记\基础框架8笔记\SpringBoot笔记\assets\image-20210917151314753.png" alt="image-20210917151314753" style="zoom:80%;" />

在该工程中的 `com.itheima.controller` 包下创建一个名为 `BookController` 的控制器。内容如下：

```java
@RestController
@RequestMapping("/books")
public class BookController {

    @GetMapping("/{id}")
    public String getById(@PathVariable Integer id){
        System.out.println("id ==> "+id);
        return "hello , spring boot!";
    }
}
```

#### 2.1.2  不同配置文件演示

* **application.properties配置文件**

现在需要进行配置，配合文件必须放在 `resources` 目录下，而该目录下有一个名为 `application.properties` 的配置文件，我们就可以在该配置文件中修改端口号，在该配置文件中书写 `port` ，`Idea` 就会提示，如下

<img src="D:\BaiduNetdiskDownload\课程笔记\基础框架笔记\基础框架8笔记\SpringBoot笔记\assets\image-20210917161422535.png" alt="image-20210917161422535" style="zoom:80%;" />

`application.properties` 配置文件内容如下：

```properties
server.port=80
```

启动服务，会在控制台打印出日志信息，从日志信息中可以看到绑定的端口号已经修改了

<img src="D:\BaiduNetdiskDownload\课程笔记\基础框架笔记\基础框架8笔记\SpringBoot笔记\assets\image-20210917161720855.png" alt="image-20210917161720855" style="zoom:80%;" />

* **application.yml配置文件**

删除 `application.properties` 配置文件中的内容。在 `resources` 下创建一个名为 `application.yml` 的配置文件，在该文件中书写端口号的配置项，格式如下：

```yaml
server:
	port: 81
```

> ==注意： 在`:`后，数据前一定要加空格。==

而在 `yml` 配置文件中也是有提示功能的，我们也可以在该文件中书写 `port` ，然后 `idea` 就会提示并书写成上面的格式

<img src="D:\BaiduNetdiskDownload\课程笔记\基础框架笔记\基础框架8笔记\SpringBoot笔记\assets\image-20210917162512646.png" alt="image-20210917162512646" style="zoom:80%;" />

启动服务，可以在控制台看到绑定的端口号是 `81`

![image-20210917162700711](D:\BaiduNetdiskDownload\课程笔记\基础框架笔记\基础框架8笔记\SpringBoot笔记\assets\image-20210917162700711.png)

* **application.yaml配置文件**

删除 `application.yml` 配置文件和 `application.properties` 配置文件内容，然后在 `resources` 下创建名为 `application.yaml` 的配置文件，配置内容和后缀名为 `yml` 的配置文件中的内容相同，只是使用了不同的后缀名而已

`application.yaml` 配置文件内容如下：

```yaml
server:
	port: 83
```

启动服务，在控制台可以看到绑定的端口号

![image-20210917163335913](D:\BaiduNetdiskDownload\课程笔记\基础框架笔记\基础框架8笔记\SpringBoot笔记\assets\image-20210917163335913.png)

==注意：在配合文件中如果没有提示，可以使用一下方式解决==

* 点击 `File` 选中 `Project Structure`

<img src="D:\BaiduNetdiskDownload\课程笔记\基础框架笔记\基础框架8笔记\SpringBoot笔记\assets\image-20210917163557071.png" alt="image-20210917163557071" style="zoom:80%;" />

* 弹出如下窗口，按图中标记红框进行选择

<img src="D:\BaiduNetdiskDownload\课程笔记\基础框架笔记\基础框架8笔记\SpringBoot笔记\assets\image-20210917163736458.png" alt="image-20210917163736458" style="zoom:70%;" />

* 通过上述操作，会弹出如下窗口

<img src="D:\BaiduNetdiskDownload\课程笔记\基础框架笔记\基础框架8笔记\SpringBoot笔记\assets\image-20210917163818051.png" alt="image-20210917163818051" style="zoom:80%;" />

* 点击上图的 `+` 号，弹出选择该模块的配置文件

<img src="D:\BaiduNetdiskDownload\课程笔记\基础框架笔记\基础框架8笔记\SpringBoot笔记\assets\image-20210917163828518.png" alt="image-20210917163828518" style="zoom:80%;" />

* 通过上述几步后，就可以看到如下界面。`properties` 类型的配合文件有一个，`ymal` 类型的配置文件有两个

<img src="D:\BaiduNetdiskDownload\课程笔记\基础框架笔记\基础框架8笔记\SpringBoot笔记\assets\image-20210917163846243.png" alt="image-20210917163846243" style="zoom:80%;" />

#### 2.1.3  三种配合文件的优先级

在三种配合文件中分别配置不同的端口号，启动服务查看绑定的端口号。用这种方式就可以看到哪个配置文件的优先级更高一些

`application.properties` 文件内容如下：

```properties
server.port=80
```

`application.yml` 文件内容如下：

```yaml
server:
	port: 81
```

`application.yaml` 文件内容如下：

```yaml
server:
	port: 82
```

启动服务，在控制台可以看到使用的端口号是 `80`。说明 `application.properties` 的优先级最高

注释掉 `application.properties` 配置文件内容。再次启动服务，在控制台可以看到使用的端口号是 `81`，说明 `application.yml` 配置文件为第二优先级。

从上述的验证结果可以确定三种配置文件的优先级是：

==`application.properties`  >  `application.yml`   >  `application.yaml`==

> ==注意：==
>
> * `SpringBoot` 核心配置文件名为 `application`
>
> * `SpringBoot` 内置属性过多，且所有属性集中在一起修改，在使用时，通过提示键+关键字修改属性
>
>   例如要设置日志的级别时，可以在配置文件中书写 `logging`，就会提示出来。配置内容如下
>
>   ```yaml
>   logging:
>     level:
>       root: info
>   ```

### 2.2  yaml格式

上面讲了三种不同类型的配置文件，而 `properties` 类型的配合文件之前我们学习过，接下来我们重点学习 `yaml` 类型的配置文件。

**YAML（YAML Ain't Markup Language），一种数据序列化格式。**这种格式的配置文件在近些年已经占有主导地位，那么这种配置文件和前期使用的配置文件是有一些优势的，我们先看之前使用的配置文件。

最开始我们使用的是 `xml` ，格式如下：

```xml
<enterprise>
    <name>itcast</name>
    <age>16</age>
    <tel>4006184000</tel>
</enterprise>
```

而 `properties` 类型的配置文件如下

```properties
enterprise.name=itcast
enterprise.age=16
enterprise.tel=4006184000
```

`yaml` 类型的配置文件内容如下

```yaml
enterprise:
	name: itcast
	age: 16
	tel: 4006184000
```

**优点：**

* 容易阅读

  `yaml` 类型的配置文件比 `xml` 类型的配置文件更容易阅读，结构更加清晰

* 容易与脚本语言交互

* 以数据为核心，重数据轻格式

  `yaml` 更注重数据，而 `xml` 更注重格式

**YAML 文件扩展名：**

* `.yml` (主流)
* `.yaml`

上面两种后缀名都可以，以后使用更多的还是 `yml` 的。

#### 2.2.1  语法规则

* 大小写敏感

* 属性层级关系使用多行描述，每行结尾使用冒号结束

* 使用缩进表示层级关系，同层级左侧对齐，只允许使用空格（不允许使用Tab键）

  空格的个数并不重要，只要保证同层级的左侧对齐即可。

* 属性值前面添加空格（属性名与属性值之间使用冒号+空格作为分隔）

* \# 表示注释

==核心规则：数据前面要加空格与冒号隔开==

数组数据在数据书写位置的下方使用减号作为数据开始符号，每行书写一个数据，减号与数据间空格分隔，例如

```yaml
enterprise:
  name: itcast
  age: 16
  tel: 4006184000
  subject:
    - Java
    - 前端
    - 大数据
```

### 2.3  yaml配置文件数据读取

#### 2.3.1  环境准备

新创建一个名为 `springboot_03_read_data` 的 `SpringBoot` 工程，目录结构如下

<img src="D:\BaiduNetdiskDownload\课程笔记\基础框架笔记\基础框架8笔记\SpringBoot笔记\assets\image-20210917172736484.png" alt="image-20210917172736484" style="zoom:80%;" />

在 `com.itheima.controller` 包写创建名为 `BookController` 的控制器，内容如下

```java
@RestController
@RequestMapping("/books")
public class BookController {

    @GetMapping("/{id}")
    public String getById(@PathVariable Integer id){
        System.out.println("id ==> "+id);
        return "hello , spring boot!";
    }
}
```

在 `com.itheima.domain` 包下创建一个名为 `Enterprise` 的实体类等会用来封装数据，内容如下

```java
public class Enterprise {
    private String name;
    private int age;
    private String tel;
    private String[] subject;
    
    //setter and getter
    
    //toString
}
```

在 `resources` 下创建一个名为 `application.yml` 的配置文件，里面配置了不同的数据，内容如下

```yaml
lesson: SpringBoot

server:
  port: 80

enterprise:
  name: itcast
  age: 16
  tel: 4006184000
  subject:
    - Java
    - 前端
    - 大数据
```

#### 2.3.2  读取配置数据

##### 2.3.2.1  使用 @Value注解

使用 `@Value("表达式")` 注解可以从配合文件中读取数据，注解中用于读取属性名引用方式是：`${一级属性名.二级属性名……}`

我们可以在 `BookController` 中使用 `@Value`  注解读取配合文件数据，如下

```java
@RestController
@RequestMapping("/books")
public class BookController {
    
    @Value("${lesson}")
    private String lesson;
    @Value("${server.port}")
    private Integer port;
    @Value("${enterprise.subject[0]}")
    private String subject_00;

    @GetMapping("/{id}")
    public String getById(@PathVariable Integer id){
        System.out.println(lesson);
        System.out.println(port);
        System.out.println(subject_00);
        return "hello , spring boot!";
    }
}
```

##### 2.3.2.2  Environment对象

上面方式读取到的数据特别零散，`SpringBoot` 还可以使用 `@Autowired` 注解注入 `Environment` 对象的方式读取数据。这种方式 `SpringBoot` 会将配置文件中所有的数据封装到 `Environment` 对象中，如果需要使用哪个数据只需要通过调用 `Environment` 对象的 `getProperty(String name)` 方法获取。具体代码如下：

```java
@RestController
@RequestMapping("/books")
public class BookController {
    
    @Autowired
    private Environment env;
    
    @GetMapping("/{id}")
    public String getById(@PathVariable Integer id){
        System.out.println(env.getProperty("lesson"));
        System.out.println(env.getProperty("enterprise.name"));
        System.out.println(env.getProperty("enterprise.subject[0]"));
        return "hello , spring boot!";
    }
}
```

> ==注意：这种方式，框架内容大量数据，而在开发中我们很少使用。==

##### 2.3.2.3  自定义对象

`SpringBoot` 还提供了将配置文件中的数据封装到我们自定义的实体类对象中的方式。具体操作如下：

* 将实体类 `bean` 的创建交给 `Spring` 管理。

  在类上添加 `@Component` 注解

* 使用 `@ConfigurationProperties` 注解表示加载配置文件

  在该注解中也可以使用 `prefix` 属性指定只加载指定前缀的数据

* 在 `BookController` 中进行注入

**具体代码如下：**

`Enterprise` 实体类内容如下：

```java
@Component
@ConfigurationProperties(prefix = "enterprise")
public class Enterprise {
    private String name;
    private int age;
    private String tel;
    private String[] subject;

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
        this.age = age;
    }

    public String getTel() {
        return tel;
    }

    public void setTel(String tel) {
        this.tel = tel;
    }

    public String[] getSubject() {
        return subject;
    }

    public void setSubject(String[] subject) {
        this.subject = subject;
    }

    @Override
    public String toString() {
        return "Enterprise{" +
                "name='" + name + '\'' +
                ", age=" + age +
                ", tel='" + tel + '\'' +
                ", subject=" + Arrays.toString(subject) +
                '}';
    }
}
```

`BookController` 内容如下：

```java
@RestController
@RequestMapping("/books")
public class BookController {
    
    @Autowired
    private Enterprise enterprise;

    @GetMapping("/{id}")
    public String getById(@PathVariable Integer id){
        System.out.println(enterprise.getName());
        System.out.println(enterprise.getAge());
        System.out.println(enterprise.getSubject());
        System.out.println(enterprise.getTel());
        System.out.println(enterprise.getSubject()[0]);
        return "hello , spring boot!";
    }
}
```

==注意：==

使用第三种方式，在实体类上有如下警告提示

<img src="D:\BaiduNetdiskDownload\课程笔记\基础框架笔记\基础框架8笔记\SpringBoot笔记\assets\image-20210917180919390.png" alt="image-20210917180919390" style="zoom:70%;" />

这个警告提示解决是在 `pom.xml` 中添加如下依赖即可

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-configuration-processor</artifactId>
    <optional>true</optional>
</dependency>
```

### 2.4  多环境配置

以后在工作中，对于开发环境、测试环境、生产环境的配置肯定都不相同，比如我们开发阶段会在自己的电脑上安装 `mysql` ，连接自己电脑上的 `mysql` 即可，但是项目开发完毕后要上线就需要该配置，将环境的配置改为线上环境的。

<img src="D:\BaiduNetdiskDownload\课程笔记\基础框架笔记\基础框架8笔记\SpringBoot笔记\assets\image-20210917185253557.png" alt="image-20210917185253557" style="zoom:60%;" />

来回的修改配置会很麻烦，而 `SpringBoot` 给开发者提供了多环境的快捷配置，需要切换环境时只需要改一个配置即可。不同类型的配置文件多环境开发的配置都不相同，接下来对不同类型的配置文件进行说明

#### 2.4.1  yaml文件

在 `application.yml` 中使用 `---` 来分割不同的配置，内容如下

```yaml
#开发
spring:
  profiles: dev #给开发环境起的名字
server:
  port: 80
---
#生产
spring:
  profiles: pro #给生产环境起的名字
server:
  port: 81
---
#测试
spring:
  profiles: test #给测试环境起的名字
server:
  port: 82
---
```

上面配置中 `spring.profiles` 是用来给不同的配置起名字的。而如何告知 `SpringBoot` 使用哪段配置呢？可以使用如下配置来启用都一段配置

```yaml
#设置启用的环境
spring:
  profiles:
    active: dev  #表示使用的是开发环境的配置
```

综上所述，`application.yml` 配置文件内容如下

```yaml
#设置启用的环境
spring:
  profiles:
    active: dev

---
#开发
spring:
  profiles: dev
server:
  port: 80
---
#生产
spring:
  profiles: pro
server:
  port: 81
---
#测试
spring:
  profiles: test
server:
  port: 82
---
```

==注意：==

在上面配置中给不同配置起名字的 `spring.profiles` 配置项已经过时。最新用来起名字的配置项是 

```yaml
#开发
spring:
  config:
    activate:
      on-profile: dev
```

#### 2.4.2  properties文件

`properties` 类型的配置文件配置多环境需要定义不同的配置文件

* `application-dev.properties` 是开发环境的配置文件。我们在该文件中配置端口号为 `80`

  ```properties
  server.port=80
  ```

* `application-test.properties` 是测试环境的配置文件。我们在该文件中配置端口号为 `81`

  ```properties
  server.port=81
  ```

* `application-pro.properties` 是生产环境的配置文件。我们在该文件中配置端口号为 `82`

  ```properties
  server.port=82
  ```

`SpringBoot` 只会默认加载名为 `application.properties` 的配置文件，所以需要在 `application.properties` 配置文件中设置启用哪个配置文件，配置如下:

```properties
spring.profiles.active=pro
```

#### 2.4.3  命令行启动参数设置

使用 `SpringBoot` 开发的程序以后都是打成 `jar` 包，通过 `java -jar xxx.jar` 的方式启动服务的。那么就存在一个问题，如何切换环境呢？因为配置文件打到的jar包中了。

我们知道 `jar` 包其实就是一个压缩包，可以解压缩，然后修改配置，最后再打成jar包就可以了。这种方式显然有点麻烦，而 `SpringBoot` 提供了在运行 `jar` 时设置开启指定的环境的方式，如下

```shell
java –jar xxx.jar –-spring.profiles.active=test
```

那么这种方式能不能临时修改端口号呢？也是可以的，可以通过如下方式

```shell
java –jar xxx.jar –-server.port=88
```

当然也可以同时设置多个配置，比如即指定启用哪个环境配置，又临时指定端口，如下

```shell
java –jar springboot.jar –-server.port=88 –-spring.profiles.active=test
```

大家进行测试后就会发现命令行设置的端口号优先级高（也就是使用的是命令行设置的端口号），配置的优先级其实 `SpringBoot` 官网已经进行了说明，参见 :

```
https://docs.spring.io/spring-boot/docs/current/reference/html/spring-boot-features.html#boot-features-external-config
```

进入上面网站后会看到如下页面

![image-20210917193910191](D:\BaiduNetdiskDownload\课程笔记\基础框架笔记\基础框架8笔记\SpringBoot笔记\assets\image-20210917193910191.png)

如果使用了多种方式配合同一个配置项，优先级高的生效。

### 2.5  配置文件分类

<img src="D:\BaiduNetdiskDownload\课程笔记\基础框架笔记\基础框架8笔记\SpringBoot笔记\assets\image-20210917194941597.png" alt="image-20210917194941597" style="zoom:70%;" />

有这样的场景，我们开发完毕后需要测试人员进行测试，由于测试环境和开发环境的很多配置都不相同，所以测试人员在运行我们的工程时需要临时修改很多配置，如下

```shell
java –jar springboot.jar –-spring.profiles.active=test --server.port=85 --server.servlet.context-path=/heima --server.tomcat.connection-timeout=-1 …… …… …… …… ……
```

针对这种情况，`SpringBoot` 定义了配置文件不同的放置的位置；而放在不同位置的优先级时不同的。

`SpringBoot` 中4级配置文件放置位置：

* 1级：classpath：application.yml  
* 2级：classpath：config/application.yml
* 3级：file ：application.yml
* 4级：file ：config/application.yml 

> ==说明：==级别越高优先级越高

#### 2.5.1  代码演示

在这里我们只演示不同级别配置文件放置位置的优先级。

##### 2.5.1.1  环境准备

创建一个名为 `springboot_06_config_file` 的 `SpringBoot` 工程，目录结构如下

<img src="D:\BaiduNetdiskDownload\课程笔记\基础框架笔记\基础框架8笔记\SpringBoot笔记\assets\image-20210917200241282.png" alt="image-20210917200241282" style="zoom:80%;" />

在 `resources` 下创建一个名为 `config` 的目录，在该目录中创建 `application.yml` 配置文件，而在该配置文件中将端口号设置为 `81`，内容如下

```yaml
server:
  port: 81
```

而在 `resources` 下创建的 `application.yml` 配置文件中并将端口号设置为 `80`，内容如下

```yaml
server:
  port: 80
```

##### 2.5.1.2  验证1级和2级的优先级

运行启动引导类，可以在控制台看到如下日志信息

![image-20210917200805389](D:\BaiduNetdiskDownload\课程笔记\基础框架笔记\基础框架8笔记\SpringBoot笔记\assets\image-20210917200805389.png)

通过这个结果可以得出==类路径下的 `config` 下的配置文件优先于类路径下的配置文件。==

##### 2.5.1.3  验证2级和4级的优先级

要验证4级，按照以下步骤完成

* 将工程打成 `jar` 包

  点击工程的 `package` 来打 `jar` 包

  <img src="D:\BaiduNetdiskDownload\课程笔记\基础框架笔记\基础框架8笔记\SpringBoot笔记\assets\image-20210917201243721.png" alt="image-20210917201243721" style="zoom:80%;" />

* 在硬盘上找到 `jar` 包所在位置

  <img src="D:\BaiduNetdiskDownload\课程笔记\基础框架笔记\基础框架8笔记\SpringBoot笔记\assets\image-20210917201523669.png" alt="image-20210917201523669" style="zoom:70%;" />

* 在 `jar` 包所在位置创建 `config` 文件夹，在该文件夹下创建 `application.yml` 配置文件，而在该配合文件中将端口号设置为 `82` 

* 在命令行使用以下命令运行程序

  ```shell
  java -jar springboot_06_config_file-0.0.1-SNAPSHOT.jar
  ```

  运行后日志信息如下

  ![image-20210917201922831](D:\BaiduNetdiskDownload\课程笔记\基础框架笔记\基础框架8笔记\SpringBoot笔记\assets\image-20210917201922831.png)

  通过这个结果可以得出==file： `config` 下的配置文件优先于类路径下的配置文件。==

> ==注意：==
>
> SpringBoot 2.5.0版本存在一个bug，我们在使用这个版本时，需要在 `jar` 所在位置的 `config` 目录下创建一个任意名称的文件夹

## 3，SpringBoot整合junit

回顾 `Spring` 整合 `junit`

```java
@RunWith(SpringJUnit4ClassRunner.class)
@ContextConfiguration(classes = SpringConfig.class)
public class UserServiceTest {
    
    @Autowired
    private BookService bookService;
    
    @Test
    public void testSave(){
        bookService.save();
    }
}
```

使用 `@RunWith` 注解指定运行器，使用 `@ContextConfiguration` 注解来指定配置类或者配置文件。而 `SpringBoot` 整合 `junit` 特别简单，分为以下三步完成

* 在测试类上添加 `SpringBootTest` 注解
* 使用 `@Autowired` 注入要测试的资源
* 定义测试方法进行测试

### 3.1  环境准备

创建一个名为 `springboot_07_test` 的 `SpringBoot` 工程，工程目录结构如下

<img src="D:\BaiduNetdiskDownload\课程笔记\基础框架笔记\基础框架8笔记\SpringBoot笔记\assets\image-20210917213556673.png" alt="image-20210917213556673" style="zoom:80%;" />

在 `com.itheima.service` 下创建 `BookService` 接口，内容如下

```java
public interface BookService {
    public void save();
}
```

在 `com.itheima.service.impl` 包写创建一个 `BookServiceImpl` 类，使其实现 `BookService` 接口，内容如下

```java
@Service
public class BookServiceImpl implements BookService {
    @Override
    public void save() {
        System.out.println("book service is running ...");
    }
}
```

### 3.2  编写测试类

在 `test/java` 下创建 `com.itheima` 包，在该包下创建测试类，将 `BookService` 注入到该测试类中

```java
@SpringBootTest
class Springboot07TestApplicationTests {

    @Autowired
    private BookService bookService;

    @Test
    public void save() {
        bookService.save();
    }
}
```

> ==注意：==这里的引导类所在包必须是测试类所在包及其子包。
>
> 例如：
>
> * 引导类所在包是 `com.itheima`
> * 测试类所在包是 `com.itheima`
>
> 如果不满足这个要求的话，就需要在使用 `@SpringBootTest` 注解时，使用 `classes` 属性指定引导类的字节码对象。如 `@SpringBootTest(classes = Springboot07TestApplication.class)`

## 4，SpringBoot整合mybatis

### 4.1  回顾Spring整合Mybatis

`Spring` 整合 `Mybatis` 需要定义很多配置类

* `SpringConfig` 配置类

  * 导入 `JdbcConfig` 配置类

  * 导入 `MybatisConfig` 配置类

    ```java
    @Configuration
    @ComponentScan("com.itheima")
    @PropertySource("classpath:jdbc.properties")
    @Import({JdbcConfig.class,MyBatisConfig.class})
    public class SpringConfig {
    }
    
    ```

* `JdbcConfig` 配置类

  * 定义数据源（加载properties配置项：driver、url、username、password）

    ```java
    public class JdbcConfig {
        @Value("${jdbc.driver}")
        private String driver;
        @Value("${jdbc.url}")
        private String url;
        @Value("${jdbc.username}")
        private String userName;
        @Value("${jdbc.password}")
        private String password;
    
        @Bean
        public DataSource getDataSource(){
            DruidDataSource ds = new DruidDataSource();
            ds.setDriverClassName(driver);
            ds.setUrl(url);
            ds.setUsername(userName);
            ds.setPassword(password);
            return ds;
        }
    }
    ```

* `MybatisConfig` 配置类

  * 定义 `SqlSessionFactoryBean`

  * 定义映射配置

    ```java
    @Bean
    public MapperScannerConfigurer getMapperScannerConfigurer(){
        MapperScannerConfigurer msc = new MapperScannerConfigurer();
        msc.setBasePackage("com.itheima.dao");
        return msc;
    }
    
    @Bean
    public SqlSessionFactoryBean getSqlSessionFactoryBean(DataSource dataSource){
        SqlSessionFactoryBean ssfb = new SqlSessionFactoryBean();
        ssfb.setTypeAliasesPackage("com.itheima.domain");
        ssfb.setDataSource(dataSource);
        return ssfb;
    }
    
    ```

### 4.2  SpringBoot整合mybatis

#### 4.2.1  创建模块

* 创建新模块，选择 `Spring Initializr`，并配置模块相关基础信息

<img src="D:\BaiduNetdiskDownload\课程笔记\基础框架笔记\基础框架8笔记\SpringBoot笔记\assets\image-20210917215913779.png" alt="image-20210917215913779" style="zoom:80%;" />

* 选择当前模块需要使用的技术集（MyBatis、MySQL）

  <img src="D:\BaiduNetdiskDownload\课程笔记\基础框架笔记\基础框架8笔记\SpringBoot笔记\assets\image-20210917215958091.png" alt="image-20210917215958091" style="zoom:80%;" />

#### 4.2.2  定义实体类

在 `com.itheima.domain` 包下定义实体类 `Book`，内容如下

```java
public class Book {
    private Integer id;
    private String name;
    private String type;
    private String description;
    
    //setter and  getter
    
    //toString
}
```

#### 4.2.3  定义dao接口

在 `com.itheima.dao` 包下定义 `BookDao` 接口，内容如下

```java
public interface BookDao {
    @Select("select * from tbl_book where id = #{id}")
    public Book getById(Integer id);
}
```

#### 4.2.4  定义测试类

在 `test/java` 下定义包 `com.itheima` ，在该包下测试类，内容如下

```java
@SpringBootTest
class Springboot08MybatisApplicationTests {

	@Autowired
	private BookDao bookDao;

	@Test
	void testGetById() {
		Book book = bookDao.getById(1);
		System.out.println(book);
	}
}
```

#### 4.2.5  编写配置

我们代码中并没有指定连接哪儿个数据库，用户名是什么，密码是什么。所以这部分需要在 `SpringBoot` 的配置文件中进行配合。

在 `application.yml` 配置文件中配置如下内容

```yml
spring:
  datasource:
    driver-class-name: com.mysql.jdbc.Driver
    url: jdbc:mysql://localhost:3306/ssm_db
    username: root
    password: root
```

#### 4.2.6  测试

运行测试方法，我们会看到如下错误信息

<img src="D:\BaiduNetdiskDownload\课程笔记\基础框架笔记\基础框架8笔记\SpringBoot笔记\assets\image-20210917221427930.png" alt="image-20210917221427930" style="zoom:70%;" />

错误信息显示在 `Spring` 容器中没有 `BookDao` 类型的 `bean`。为什么会出现这种情况呢？

原因是 `Mybatis` 会扫描接口并创建接口的代码对象交给 `Spring` 管理，但是现在并没有告诉 `Mybatis` 哪个是 `dao` 接口。而我们要解决这个问题需要在`BookDao` 接口上使用 `@Mapper` ，`BookDao` 接口改进为

```java
@Mapper
public interface BookDao {
    @Select("select * from tbl_book where id = #{id}")
    public Book getById(Integer id);
}
```

> ==注意：==
>
> `SpringBoot` 版本低于2.4.3(不含)，Mysql驱动版本大于8.0时，需要在url连接串中配置时区 `jdbc:mysql://localhost:3306/ssm_db?serverTimezone=UTC`，或在MySQL数据库端配置时区解决此问题

#### 4.2.7  使用Druid数据源

现在我们并没有指定数据源，`SpringBoot` 有默认的数据源，我们也可以指定使用 `Druid` 数据源，按照以下步骤实现

* 导入 `Druid` 依赖

  ```xml
  <dependency>
      <groupId>com.alibaba</groupId>
      <artifactId>druid</artifactId>
      <version>1.1.16</version>
  </dependency>
  ```

* 在 `application.yml` 配置文件配置

  可以通过 `spring.datasource.type` 来配置使用什么数据源。配置文件内容可以改进为

  ```yaml
  spring:
    datasource:
      driver-class-name: com.mysql.cj.jdbc.Driver
      url: jdbc:mysql://localhost:3306/ssm_db?serverTimezone=UTC
      username: root
      password: root
      type: com.alibaba.druid.pool.DruidDataSource
  ```

## 5，案例

`SpringBoot` 到这就已经学习完毕，接下来我们将学习 `SSM` 时做的三大框架整合的案例用 `SpringBoot` 来实现一下。我们完成这个案例基本是将之前做的拷贝过来，修改成 `SpringBoot` 的即可，主要从以下几部分完成

1. pom.xml

   配置起步依赖，必要的资源坐标(druid)

2. application.yml

   设置数据源、端口等

3. 配置类

   全部删除

4. dao

   设置@Mapper

5. 测试类

6. 页面

   放置在resources目录下的static目录中

### 5.1  创建工程

创建 `SpringBoot` 工程，在创建工程时需要勾选 `web`、`mysql`、`mybatis`，工程目录结构如下

<img src="D:\BaiduNetdiskDownload\课程笔记\基础框架笔记\基础框架8笔记\SpringBoot笔记\assets\image-20210917225019868.png" alt="image-20210917225019868" style="zoom:80%;" />

由于我们工程中使用到了 `Druid` ，所以需要导入 `Druid` 的坐标

```xml
<dependency>
    <groupId>com.alibaba</groupId>
    <artifactId>druid</artifactId>
    <version>1.1.16</version>
</dependency>
```

### 5.2  代码拷贝

将 `springmvc_11_page` 工程中的 `java` 代码及测试代码连同包拷贝到 `springboot_09_ssm` 工程，按照下图进行拷贝

<img src="D:\BaiduNetdiskDownload\课程笔记\基础框架笔记\基础框架8笔记\SpringBoot笔记\assets\image-20210917225715519.png" alt="image-20210917225715519" style="zoom:70%;" />

需要修改的内容如下：

* `Springmvc_11_page` 中 `config` 包下的是配置类，而 `SpringBoot` 工程不需要这些配置类，所以这些可以直接删除

* `dao` 包下的接口上在拷贝到 `springboot_09-ssm` 工程中需要在接口中添加 `@Mapper` 注解

* `BookServiceTest` 测试需要改成 `SpringBoot` 整合 `junit` 的

  ```java
  @SpringBootTest
  public class BookServiceTest {
  
      @Autowired
      private BookService bookService;
  
      @Test
      public void testGetById(){
          Book book = bookService.getById(2);
          System.out.println(book);
      }
  
      @Test
      public void testGetAll(){
          List<Book> all = bookService.getAll();
          System.out.println(all);
      }
  }
  ```

### 5.3  配置文件

在 `application.yml` 配置文件中需要配置如下内容

* 服务的端口号
* 连接数据库的信息
* 数据源

```yaml
server:
  port: 80

spring:
  datasource:
    type: com.alibaba.druid.pool.DruidDataSource
    driver-class-name: com.mysql.cj.jdbc.Driver
    url: jdbc:mysql://localhost:3306/ssm_db #?servierTimezone=UTC
    username: root
    password: root
```

### 5.4  静态资源

在 `SpringBoot` 程序中是没有 `webapp` 目录的，那么在 `SpringBoot` 程序中静态资源需要放在什么位置呢？

静态资源需要放在 `resources` 下的 `static` 下，如下图所示

<img src="D:\BaiduNetdiskDownload\课程笔记\基础框架笔记\基础框架8笔记\SpringBoot笔记\assets\image-20210917230702072.png" alt="image-20210917230702072" style="zoom:80%;" />





