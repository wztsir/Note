# Maven&MyBatis

**目标**

> * 能够使用Maven进行项目的管理
> * 能够完成Mybatis代理方式查询数据
> * 能够理解Mybatis核心配置文件的配置

## 1，Maven

Maven是专门用于管理和构建Java项目的工具，它的主要功能有：

* 提供了一套标准化的项目结构

* 提供了一套标准化的构建流程（编译，测试，打包，发布……）

* 提供了一套依赖管理机制

**标准化的项目结构：**

项目结构都知道，每一个开发工具（IDE）都有自己不同的项目结构，它们互相之间不通用。我再eclipse中创建的目录，无法在idea中进行使用，这就造成了很大的不方便，如下图:前两个是以后开发经常使用的开发工具

<img src="D:/download/downloadFromMicsoft/day04-Maven&MyBatis/day04-1-Maven/ppt/assets/image-20210726153521381.png" alt="image-20210726153521381" style="zoom:80%;" />

而Maven提供了一套标准化的项目结构，所有的IDE使用Maven构建的项目完全一样，所以IDE创建的Maven项目可以通用。如下图右边就是Maven构建的项目结构。

<img src="D:/download/downloadFromMicsoft/day04-Maven&MyBatis/day04-1-Maven/ppt/assets/image-20210726153815028.png" alt="image-20210726153815028" style="zoom:80%;" />



**标准化的构建流程：**

<img src="D:/download/downloadFromMicsoft/day04-Maven&MyBatis/day04-1-Maven/ppt/assets/image-20210726154144488.png" alt="image-20210726154144488" style="zoom:80%;" />

如上图所示开发了一套系统，代码需要进行编译、测试、打包、发布，这些操作如果需要反复进行就显得特别麻烦，而Maven提供了一套简单的命令来完成项目构建。

**依赖管理：**

依赖管理其实就是管理你项目所依赖的第三方资源（jar包、插件）。如之前项目中需要使用JDBC和Druid的话，就需要去网上下载对应的依赖包（当前之前是老师已经下载好提供给大家了），复制到项目中，还要将jar包加入工作环境这一系列的操作。如下图所示

<img src="D:/download/downloadFromMicsoft/day04-Maven&MyBatis/day04-1-Maven/ppt/assets/image-20210726154753631.png" alt="image-20210726154753631" style="zoom:80%;" />

而Maven使用标准的 ==坐标== 配置来管理各种依赖，只需要简单的配置就可以完成依赖管理。

<img src="D:/download/downloadFromMicsoft/day04-Maven&MyBatis/day04-1-Maven/ppt/assets/image-20210726154922337.png" alt="image-20210726154922337" style="zoom:80%;" />

如上图右边所示就是mysql驱动包的坐标，在项目中只需要写这段配置，其他都不需要担心，Maven都帮进行操作了。

市面上有很多构建工具，而Maven依旧还是主流构建工具，如下图是常用构建工具的使用占比

![image-20210726155212733](D:/download/downloadFromMicsoft/day04-Maven&MyBatis/day04-1-Maven/ppt/assets/image-20210726155212733.png)

### 1.1  Maven简介

> ==Apache Maven== 是一个项目管理和构建==工具==，它基于项目对象模型(POM)的概念，通过一小段描述信息来管理项目的构建、报告和文档。
>
> 官网 ：http://maven.apache.org/ 

通过上面的描述大家只需要知道Maven是一个工具即可。Apache 是一个开源组织，将来会学习很多Apache提供的项目。

#### 1.1.1  Maven模型

* 项目对象模型 (Project Object Model)
* 依赖管理模型(Dependency)
* 插件(Plugin)



<img src="D:/download/downloadFromMicsoft/day04-Maven&MyBatis/day04-1-Maven/ppt/assets/image-20210726155759621.png" alt="image-20210726155759621" style="zoom:80%;" />

如上图所示就是Maven的模型，而先看紫色框框起来的部分，他就是用来完成 `标准化构建流程` 。如需要编译，Maven提供了一个编译插件供使用，需要打包，Maven就提供了一个打包插件提供使用等。

<img src="D:/download/downloadFromMicsoft/day04-Maven&MyBatis/day04-1-Maven/ppt/assets/image-20210726160928515.png" alt="image-20210726160928515" style="zoom:80%;" />

上图中紫色框起来的部分，项目对象模型就是将自己抽象成一个对象模型，有自己专属的坐标，如下图所示是一个Maven项目：

<img src="D:/download/downloadFromMicsoft/day04-Maven&MyBatis/day04-1-Maven/ppt/assets/image-20210726161340796.png" alt="image-20210726161340796" style="zoom:80%;" />

依赖管理模型则是使用坐标来描述当前项目依赖哪儿些第三方jar包，如下图所示

![image-20210726161616034](D:/download/downloadFromMicsoft/day04-Maven&MyBatis/day04-1-Maven/ppt/assets/image-20210726161616034.png)

上述Maven模型图中还有一部分是仓库。如何理解仓库呢？

#### 1.1.2  仓库

大家想想这样的场景，创建Maven项目，在项目中使用坐标来指定项目的依赖，那么依赖的jar包到底存储在什么地方呢？其实依赖jar包是存储在的本地仓库中。而项目运行时从本地仓库中拿需要的依赖jar包。

**仓库分类：**

* 本地仓库：自己计算机上的一个目录

* 中央仓库：由Maven团队维护的全球唯一的仓库

  * 地址： https://repo1.maven.org/maven2/

* 远程仓库(私服)：一般由公司团队搭建的私有仓库

  今天只学习远程仓库的使用，并不会搭建。

当项目中使用坐标引入对应依赖jar包后，首先会查找本地仓库中是否有对应的jar包：

* 如果有，则在项目直接引用;

* 如果没有，则去中央仓库中下载对应的jar包到本地仓库。

<img src="D:/download/downloadFromMicsoft/day04-Maven&MyBatis/day04-1-Maven/ppt/assets/image-20210726162605394.png" alt="image-20210726162605394" style="zoom:70%;" />

如果还可以搭建远程仓库，将来jar包的查找顺序则变为：

> 本地仓库 --> 远程仓库--> 中央仓库

<img src="D:/download/downloadFromMicsoft/day04-Maven&MyBatis/day04-1-Maven/ppt/assets/image-20210726162815045.png" alt="image-20210726162815045" style="zoom:70%;" />

### 1.2  Maven安装配置

* 解压 apache-maven-3.6.1.rar 既安装完成

  <img src="D:/download/downloadFromMicsoft/day04-Maven&MyBatis/day04-1-Maven/ppt/assets/image-20210726163219682.png" alt="image-20210726163219682" style="zoom:90%;" />

  > 建议解压缩到没有中文、特殊字符的路径下。如课程中解压缩到 `D:\software` 下。

  解压缩后的目录结构如下：

  <img src="D:/download/downloadFromMicsoft/day04-Maven&MyBatis/day04-1-Maven/ppt/assets/image-20210726163518885.png" alt="image-20210726163518885" style="zoom:80%;" />

  * bin目录 ： 存放的是可执行命令。mvn 命令重点关注。
  * conf目录 ：存放Maven的配置文件。`settings.xml` 配置文件后期需要修改。
  * lib目录 ：存放Maven依赖的jar包。Maven也是使用java开发的，所以它也依赖其他的jar包。

* 配置环境变量 MAVEN_HOME 为安装路径的bin目录

  `此电脑` 右键  -->  `高级系统设置`  -->  `高级`  -->  `环境变量`

  在系统变量处新建一个变量 `MAVEN_HOME`

  <img src="D:/download/downloadFromMicsoft/day04-Maven&MyBatis/day04-1-Maven/ppt/assets/image-20210726164058589.png" alt="image-20210726164058589" style="zoom:80%;" />

  在 `Path` 中进行配置

  <img src="D:/download/downloadFromMicsoft/day04-Maven&MyBatis/day04-1-Maven/ppt/assets/image-20210726164146832.png" alt="image-20210726164146832" style="zoom:80%;" />

  打开命令提示符进行验证，出现如图所示表示安装成功

  <img src="D:/download/downloadFromMicsoft/day04-Maven&MyBatis/day04-1-Maven/ppt/assets/image-20210726164306480.png" alt="image-20210726164306480" style="zoom:80%;" />

* 配置本地仓库

  修改 conf/settings.xml 中的 <localRepository> 为一个指定目录作为本地仓库，用来存储jar包。

  <img src="D:/download/downloadFromMicsoft/day04-Maven&MyBatis/day04-1-Maven/ppt/assets/image-20210726164348048.png" alt="image-20210726164348048" style="zoom:60%;" />

* 配置阿里云私服

  中央仓库在国外，所以下载jar包速度可能比较慢，而阿里公司提供了一个远程仓库，里面基本也都有开源项目的jar包。

  修改 conf/settings.xml 中的 <mirrors>标签，为其添加如下子标签：

  ```xml
  <mirror>  
      <id>alimaven</id>  
      <name>aliyun maven</name>  
      <url>http://maven.aliyun.com/nexus/content/groups/public/</url>
      <mirrorOf>central</mirrorOf>          
  </mirror>
  ```



### 1.3  Maven基本使用

#### 1.3.1  Maven 常用命令

> * compile ：编译
>
> * clean：清理
>
> * test：测试
>
> * package：打包
>
> * install：安装

**命令演示：**

在 `资料\代码\maven-project` 提供了一个使用Maven构建的项目，项目结构如下：

<img src="D:/download/downloadFromMicsoft/day04-Maven&MyBatis/day04-1-Maven/ppt/assets/image-20210726170404545.png" alt="image-20210726170404545" style="zoom:70%;" />

而使用上面命令需要在磁盘上进入到项目的 `pom.xml` 目录下，打开命令提示符

<img src="D:/download/downloadFromMicsoft/day04-Maven&MyBatis/day04-1-Maven/ppt/assets/image-20210726170549907.png" alt="image-20210726170549907" style="zoom:70%;" />

**编译命令演示：**

```java
compile ：编译
```

执行上述命令可以看到：

* 从阿里云下载编译需要的插件的jar包，在本地仓库也能看到下载好的插件
* 在项目下会生成一个 `target` 目录

<img src="D:/download/downloadFromMicsoft/day04-Maven&MyBatis/day04-1-Maven/ppt/assets/image-20210726171047324.png" alt="image-20210726171047324" style="zoom:80%;" />

同时在项目下会出现一个 `target` 目录，编译后的字节码文件就放在该目录下

<img src="D:/download/downloadFromMicsoft/day04-Maven&MyBatis/day04-1-Maven/ppt/assets/image-20210726171346824.png" alt="image-20210726171346824" style="zoom:80%;" />

**清理命令演示：**

```
mvn clean
```

执行上述命令可以看到

* 从阿里云下载清理需要的插件jar包
* 删除项目下的 `target` 目录

<img src="D:/download/downloadFromMicsoft/day04-Maven&MyBatis/day04-1-Maven/ppt/assets/image-20210726171558786.png" alt="image-20210726171558786" style="zoom:80%;" />

**打包命令演示：**

```
mvn package
```

执行上述命令可以看到：

* 从阿里云下载打包需要的插件jar包
* 在项目的 `terget` 目录下有一个jar包（将当前项目打成的jar包）

<img src="D:/download/downloadFromMicsoft/day04-Maven&MyBatis/day04-1-Maven/ppt/assets/image-20210726171747125.png" alt="image-20210726171747125" style="zoom:80%;" />

**测试命令演示：**

```
mvn test  
```

该命令会执行所有的测试代码。执行上述命令效果如下

<img src="D:/download/downloadFromMicsoft/day04-Maven&MyBatis/day04-1-Maven/ppt/assets/image-20210726172343933.png" alt="image-20210726172343933" style="zoom:80%;" />

**安装命令演示：**

```
mvn install
```

该命令会将当前项目打成jar包，并安装到本地仓库。执行完上述命令后到本地仓库查看结果如下：

<img src="D:/download/downloadFromMicsoft/day04-Maven&MyBatis/day04-1-Maven/ppt/assets/image-20210726172709112.png" alt="image-20210726172709112" style="zoom:80%;" />

#### 1.3.2  Maven 生命周期

Maven 构建项目生命周期描述的是一次构建过程经历经历了多少个事件

Maven 对项目构建的生命周期划分为3套：

* clean ：清理工作。
* default ：核心工作，例如编译，测试，打包，安装等。
* site ： 产生报告，发布站点等。这套声明周期一般不会使用。

同一套生命周期内，执行后边的命令，前面的所有命令会自动执行。例如默认（default）生命周期如下：

<img src="D:/download/downloadFromMicsoft/day04-Maven&MyBatis/day04-1-Maven/ppt/assets/image-20210726173153576.png" alt="image-20210726173153576" style="zoom:80%;" />

当执行 `install`（安装）命令时，它会先执行 `compile`命令，再执行 `test ` 命令，再执行 `package` 命令，最后执行 `install` 命令。

当执行 `package` （打包）命令时，它会先执行 `compile` 命令，再执行 `test` 命令，最后执行 `package` 命令。

默认的生命周期也有对应的很多命令，其他的一般都不会使用，只关注常用的：

<img src="D:/download/downloadFromMicsoft/day04-Maven&MyBatis/day04-1-Maven/ppt/assets/image-20210726173619353.png" alt="image-20210726173619353" style="zoom:80%;" />



### 1.4  IDEA使用Maven

以后开发中肯定会在高级开发工具中使用Maven管理项目，而常用的高级开发工具是IDEA，所以接下来会讲解Maven在IDEA中的使用。

#### 1.4.1  IDEA配置Maven环境

需要先在IDEA中配置Maven环境：

* 选择 IDEA中 File --> Settings

  <img src="D:/download/downloadFromMicsoft/day04-Maven&MyBatis/day04-1-Maven/ppt/assets/image-20210726174202898.png" alt="image-20210726174202898" style="zoom:80%;" />

* 搜索 maven 

  <img src="D:/download/downloadFromMicsoft/day04-Maven&MyBatis/day04-1-Maven/ppt/assets/image-20210726174229396.png" alt="image-20210726174229396" style="zoom:80%;" />

* 设置 IDEA 使用本地安装的 Maven，并修改配置文件路径

  <img src="D:/download/downloadFromMicsoft/day04-Maven&MyBatis/day04-1-Maven/ppt/assets/image-20210726174248050.png" alt="image-20210726174248050" style="zoom:70%;" />

#### 1.4.2  Maven 坐标详解

**什么是坐标？**

* Maven 中的坐标是==资源的唯一标识==
* 使用坐标来定义项目或引入项目中需要的依赖

**Maven 坐标主要组成**

* groupId：定义当前Maven项目隶属组织名称（通常是域名反写，例如：com.itheima）
* artifactId：定义当前Maven项目名称（通常是模块名称，例如 order-service、goods-service）
* version：定义当前项目版本号

如下图就是使用坐标表示一个项目：

![image-20210726174718176](D:/download/downloadFromMicsoft/day04-Maven&MyBatis/day04-1-Maven/ppt/assets/image-20210726174718176.png)

> ==注意：==
>
> * 上面所说的资源可以是插件、依赖、当前项目。
> * 的项目如果被其他的项目依赖时，也是需要坐标来引入的。

#### 1.4.3  IDEA 创建 Maven项目

* 创建模块，选择Maven，点击Next

  <img src="D:/download/downloadFromMicsoft/day04-Maven&MyBatis/day04-1-Maven/ppt/assets/image-20210726175049876.png" alt="image-20210726175049876" style="zoom:90%;" />

* 填写模块名称，坐标信息，点击finish，创建完成

  <img src="D:/download/downloadFromMicsoft/day04-Maven&MyBatis/day04-1-Maven/ppt/assets/image-20210726175109822.png" alt="image-20210726175109822" style="zoom:80%;" />

  创建好的项目目录结构如下：

  ![image-20210726175244826](D:/download/downloadFromMicsoft/day04-Maven&MyBatis/day04-1-Maven/ppt/assets/image-20210726175244826.png)

* 编写 HelloWorld，并运行

#### 1.4.4  IDEA 导入 Maven项目

大家在学习时可能需要看老师的代码，当然也就需要将老师的代码导入到自己的IDEA中。可以通过以下步骤进行项目的导入：

* 选择右侧Maven面板，点击 + 号

  <img src="D:/download/downloadFromMicsoft/day04-Maven&MyBatis/day04-1-Maven/ppt/assets/image-20210726182702336.png" alt="image-20210726182702336" style="zoom:70%;" />

* 选中对应项目的pom.xml文件，双击即可

  <img src="D:/download/downloadFromMicsoft/day04-Maven&MyBatis/day04-1-Maven/ppt/assets/image-20210726182648891.png" alt="image-20210726182648891" style="zoom:70%;" />

* 如果没有Maven面板，选择

  View --> Appearance --> Tool Window Bars

  <img src="D:/download/downloadFromMicsoft/day04-Maven&MyBatis/day04-1-Maven/ppt/assets/image-20210726182634466.png" alt="image-20210726182634466" style="zoom:80%;" />



可以通过下图所示进行命令的操作：

<img src="D:/download/downloadFromMicsoft/day04-Maven&MyBatis/day04-1-Maven/ppt/assets/image-20210726182902961.png" alt="image-20210726182902961" style="zoom:80%;" />

**配置 Maven-Helper 插件** 

* 选择 IDEA中 File --> Settings

  <img src="D:/download/downloadFromMicsoft/day04-Maven&MyBatis/day04-1-Maven/ppt/assets/image-20210726192212026.png" alt="image-20210726192212026" style="zoom:80%;" />

* 选择 Plugins

  <img src="D:/download/downloadFromMicsoft/day04-Maven&MyBatis/day04-1-Maven/ppt/assets/image-20210726192224914.png" alt="image-20210726192224914" style="zoom:80%;" />

* 搜索 Maven，选择第一个 Maven Helper，点击Install安装，弹出面板中点击Accept

  <img src="D:/download/downloadFromMicsoft/day04-Maven&MyBatis/day04-1-Maven/ppt/assets/image-20210726192244567.png" alt="image-20210726192244567" style="zoom:80%;" />

* 重启 IDEA

安装完该插件后可以通过 选中项目右键进行相关命令操作，如下图所示：

<img src="D:/download/downloadFromMicsoft/day04-Maven&MyBatis/day04-1-Maven/ppt/assets/image-20210726192430371.png" alt="image-20210726192430371" style="zoom:80%;" />

### 1.5  依赖管理

#### 1.5.1  使用坐标引入jar包

**使用坐标引入jar包的步骤：**

* 在项目的 pom.xml 中编写 <dependencies> 标签

* 在 <dependencies> 标签中 使用 <dependency> 引入坐标

* 定义坐标的 groupId，artifactId，version

  <img src="D:/download/downloadFromMicsoft/day04-Maven&MyBatis/day04-1-Maven/ppt/assets/image-20210726193105765.png" alt="image-20210726193105765" style="zoom:70%;" />

* 点击刷新按钮，使坐标生效

  <img src="D:/download/downloadFromMicsoft/day04-Maven&MyBatis/day04-1-Maven/ppt/assets/image-20210726193121384.png" alt="image-20210726193121384" style="zoom:60%;" />

>  注意：
>
>  * 具体的坐标可以到如下网站进行搜索
>  * https://mvnrepository.com/

**快捷方式导入jar包的坐标：**

每次需要引入jar包，都去对应的网站进行搜索是比较麻烦的，接下来给大家介绍一种快捷引入坐标的方式

* 在 pom.xml 中 按 alt + insert，选择 Dependency

  <img src="D:/download/downloadFromMicsoft/day04-Maven&MyBatis/day04-1-Maven/ppt/assets/image-20210726193603724.png" alt="image-20210726193603724" style="zoom:60%;" />

* 在弹出的面板中搜索对应坐标，然后双击选中对应坐标

  <img src="D:/download/downloadFromMicsoft/day04-Maven&MyBatis/day04-1-Maven/ppt/assets/image-20210726193625229.png" alt="image-20210726193625229" style="zoom:60%;" />

* 点击刷新按钮，使坐标生效

  <img src="D:/download/downloadFromMicsoft/day04-Maven&MyBatis/day04-1-Maven/ppt/assets/image-20210726193121384.png" alt="image-20210726193121384" style="zoom:60%;" />

**自动导入设置：**

上面每次操作都需要点击刷新按钮，让引入的坐标生效。当然也可以通过设置让其自动完成

* 选择 IDEA中 File --> Settings

  <img src="D:/download/downloadFromMicsoft/day04-Maven&MyBatis/day04-1-Maven/ppt/assets/image-20210726193854438.png" alt="image-20210726193854438" style="zoom:60%;" />

* 在弹出的面板中找到 Build Tools

  <img src="D:/download/downloadFromMicsoft/day04-Maven&MyBatis/day04-1-Maven/ppt/assets/image-20210726193909276.png" alt="image-20210726193909276" style="zoom:80%;" />

* 选择 Any changes，点击 ok 即可生效

#### 1.5.2  依赖范围

通过设置坐标的依赖范围(scope)，可以设置 对应jar包的作用范围：编译环境、测试环境、运行环境。

如下图所示给 `junit` 依赖通过 `scope` 标签指定依赖的作用范围。 那么这个依赖就只能作用在测试环境，其他环境下不能使用。

<img src="D:/download/downloadFromMicsoft/day04-Maven&MyBatis/day04-1-Maven/ppt/assets/image-20210726194703845.png" alt="image-20210726194703845" style="zoom:70%;" />

那么 `scope` 都可以有哪些取值呢？

| **依赖范围** | 编译classpath | 测试classpath | 运行classpath | 例子              |
| ------------ | ------------- | ------------- | ------------- | ----------------- |
| **compile**  | Y             | Y             | Y             | logback           |
| **test**     | -             | Y             | -             | Junit             |
| **provided** | Y             | Y             | -             | servlet-api       |
| **runtime**  | -             | Y             | Y             | jdbc驱动          |
| **system**   | Y             | Y             | -             | 存储在本地的jar包 |

* compile ：作用于编译环境、测试环境、运行环境。
* test ： 作用于测试环境。典型的就是Junit坐标，以后使用Junit时，都会将scope指定为该值
* provided ：作用于编译环境、测试环境。后面会学习 `servlet-api` ，在使用它时，必须将 `scope` 设置为该值，不然运行时就会报错
* runtime  ： 作用于测试环境、运行环境。jdbc驱动一般将 `scope` 设置为该值，当然不设置也没有任何问题 

> 注意：
>
> * 如果引入坐标不指定 `scope` 标签时，默认就是 compile  值。以后大部分jar包都是使用默认值。

## 1.6设置本地Maven

右侧Maven->工具->setting   （更改本地maven的位置）

或者

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220427102010717.png" alt="image-20220427102010717" style="zoom: 50%;" />

build tools中也可以调整setting



## 2，Mybatis

### 2.1  Mybatis概述

#### 2.1.1  Mybatis概念

> * MyBatis 是一款优秀的==持久层框架==，用于简化 JDBC 开发
>
> * MyBatis 本是 Apache 的一个开源项目iBatis, 2010年这个项目由apache software foundation 迁移到了google code，并且改名为MyBatis 。2013年11月迁移到Github
>
> * 官网：https://mybatis.org/mybatis-3/zh/index.html 

**持久层：**

* 负责将数据到保存到数据库的那一层代码。

  以后开发会将操作数据库的Java代码作为持久层。而Mybatis就是对jdbc代码进行了封装。

* JavaEE三层架构：表现层、业务层、持久层

  三层架构在后期会给大家进行讲解，今天先简单的了解下即可。

**框架：**

* 框架就是一个半成品软件，是一套可重用的、通用的、软件基础代码模型
* 在框架的基础之上构建软件编写更加高效、规范、通用、可扩展

举例给大家简单的解释一下什么是半成品软件。大家小时候应该在公园见过给石膏娃娃涂鸦

<img src="D:/download/downloadFromMicsoft/day04-Maven&MyBatis/day04-1-Maven/ppt/assets/image-20210726202410311.png" alt="image-20210726202410311" style="zoom:70%;" />

如下图所示有一个石膏娃娃，这个就是一个半成品。你可以在这个半成品的基础上进行不同颜色的涂鸦

<img src="D:/download/downloadFromMicsoft/day04-Maven&MyBatis/day04-1-Maven/ppt/assets/image-20210726202858441.png" alt="image-20210726202858441" style="zoom:70%;" />

了解了什么是Mybatis后，接下来说说以前 `JDBC代码` 的缺点以及Mybatis又是如何解决的。

#### 2.1.2  JDBC 缺点

下面是 JDBC 代码，通过该代码分析都存在什么缺点：

<img src="D:/download/downloadFromMicsoft/day04-Maven&MyBatis/day04-1-Maven/ppt/assets/image-20210726203656847.png" alt="image-20210726203656847" style="zoom:70%;" />

* 硬编码

  * 注册驱动、获取连接

    上图标1的代码有很多字符串，而这些是连接数据库的四个基本信息，以后如果要将Mysql数据库换成其他的关系型数据库的话，这四个地方都需要修改，如果放在此处就意味着要修改的源代码。

  * SQL语句

    上图标2的代码。如果表结构发生变化，SQL语句就要进行更改。这也不方便后期的维护。

* 操作繁琐

  * 手动设置参数

  * 手动封装结果集

    上图标4的代码是对查询到的数据进行封装，而这部分代码是没有什么技术含量，而且特别耗费时间的。

#### 2.1.3  Mybatis 优化

* 硬编码可以配置到==配置文件==
* 操作繁琐的地方mybatis都==自动完成==

如图所示

<img src="D:/download/downloadFromMicsoft/day04-Maven&MyBatis/day04-1-Maven/ppt/assets/image-20210726204849309.png" alt="image-20210726204849309" style="zoom:80%;" />

下图是持久层框架的使用占比。

<img src="D:/download/downloadFromMicsoft/day04-Maven&MyBatis/day04-1-Maven/ppt/assets/image-20210726205328999.png" alt="image-20210726205328999" style="zoom:80%;" />

### 2.2  Mybatis快速入门

同jdbc的区别：jdbc只写一个类就可以完成全部工作，但是可以方便后期维护，硬编码可以简单的更改

最后配置的文件结果



<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220417124405373.png" alt="image-20220417124405373" style="zoom: 67%;" />



[代码详解](D:\Project\Java\jdbc\mybatis-demo)



**需求：查询user表中所有的数据**

#### 创建user表，添加数据

```sql
create database mybatis;
use mybatis;

drop table if exists tb_user;

create table tb_user(
	id int primary key auto_increment,
	username varchar(20),
	password varchar(20),
	gender char(1),
	addr varchar(30)
);

INSERT INTO tb_user VALUES (1, 'zhangsan', '123', '男', '北京');
INSERT INTO tb_user VALUES (2, '李四', '234', '女', '天津');
INSERT INTO tb_user VALUES (3, '王五', '11', '男', '西安');
```

#### 创建模块，导入坐标

在创建好的模块中的 pom.xml 配置文件中添加依赖的坐标

```xml
<dependencies>
    <!--mybatis 依赖-->
    <dependency>
        <groupId>org.mybatis</groupId>
        <artifactId>mybatis</artifactId>
        <version>3.5.5</version>
    </dependency>

    <!--mysql 驱动-->
    <dependency>
        <groupId>mysql</groupId>
        <artifactId>mysql-connector-java</artifactId>
        <version>5.1.46</version>
    </dependency>

    <!--junit 单元测试-->
    <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
        <version>4.13</version>
        <scope>test</scope>
    </dependency>

    <!-- 添加slf4j日志api -->
    <dependency>
        <groupId>org.slf4j</groupId>
        <artifactId>slf4j-api</artifactId>
        <version>1.7.20</version>
    </dependency>
    <!-- 添加logback-classic依赖 -->
    <dependency>
        <groupId>ch.qos.logback</groupId>
        <artifactId>logback-classic</artifactId>
        <version>1.2.3</version>
    </dependency>
    <!-- 添加logback-core依赖 -->
    <dependency>
        <groupId>ch.qos.logback</groupId>
        <artifactId>logback-core</artifactId>
        <version>1.2.3</version>
    </dependency>
</dependencies>
```

注意：需要在项目的 resources 目录下创建logback的配置文件

#### 编写 MyBatis 核心配置文件 

-- > 替换连接信息 解决硬编码问题

在模块下的 resources 目录下创建mybatis的配置文件 `mybatis-config.xml`，内容如下：

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>

    <typeAliases>
        <package name="com.itheima.pojo"/>
    </typeAliases>
    
    <!--
    environments：配置数据库连接环境信息。可以配置多个environment，通过default属性切换不同的environment
    -->
    <environments default="development">
        <environment id="development">
            <transactionManager type="JDBC"/>
            <dataSource type="POOLED">
                <!--数据库连接信息-->
                <property name="driver" value="com.mysql.jdbc.Driver"/>
                <property name="url" value="jdbc:mysql:///mybatis?useSSL=false"/>
                <property name="username" value="root"/>
                <property name="password" value="1234"/>
            </dataSource>
        </environment>

        <environment id="test">
            <transactionManager type="JDBC"/>
            <dataSource type="POOLED">
                <!--数据库连接信息-->
                <property name="driver" value="com.mysql.jdbc.Driver"/>
                <property name="url" value="jdbc:mysql:///mybatis?useSSL=false"/>
                <property name="username" value="root"/>
                <property name="password" value="1234"/>
            </dataSource>
        </environment>
    </environments>
    <mappers>
       <!--加载sql映射文件-->
       <mapper resource="UserMapper.xml"/>
    </mappers>
</configuration>
```

#### 编写映射文件mapper

 --> 统一管理sql语句，解决硬编码问题

在模块的 `resources` 目录下创建映射配置文件 `UserMapper.xml`，内容如下：

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN" "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="test">
    <select id="selectAll" resultType="com.itheima.pojo.User">
        select * from tb_user;
    </select>
</mapper>
```

#### 编码

* 在 `com.itheima.pojo` 包下创建 User类

  ```java
  public class User {
      private int id;
      private String username;
      private String password;
      private String gender;
      private String addr;
      
      //省略了 setter 和 getter
  }
  ```

* 在 `com.itheima` 包下编写 MybatisDemo 测试类

  

  加载核心配置文件，不用记忆，核心代码就是执行sql语句的代码

  ```java
  public class MyBatisDemo {
  
      public static void main(String[] args) throws IOException {
          //1. 加载mybatis的核心配置文件，获取 SqlSessionFactory
          String resource = "mybatis-config.xml";
          InputStream inputStream = Resources.getResourceAsStream(resource);
          SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);
  
          //2. 获取SqlSession对象，用它来执行sql
          SqlSession sqlSession = sqlSessionFactory.openSession();
          //3. 执行sql
          List<User> users = sqlSession.selectList("test.selectAll"); 
          //参数是一个字符串，该字符串必须是映射配置文件的namespace.id
          System.out.println(users);
          //4. 释放资源
          sqlSession.close();
      }
  }
  ```

**解决SQL映射文件的警告提示：**

在入门案例映射配置文件中存在报红的情况。问题如下：

<img src="D:/download/downloadFromMicsoft/day04-Maven&MyBatis/day04-1-Maven/ppt/assets/image-20210726212621722.png" alt="image-20210726212621722" style="zoom:80%;" />

* 产生的原因：Idea和数据库没有建立连接，不识别表信息。但是大家一定要记住，它并不影响程序的执行。
* 解决方式：在Idea中配置MySQL数据库连接。

### 2.3配置MySQL数据库连接

* 点击IDEA右边框的 `Database` ，在展开的界面点击 `+` 选择 `Data Source` ，再选择 `MySQL`

  <img src="D:/download/downloadFromMicsoft/day04-Maven&MyBatis/day04-1-Maven/ppt/assets/image-20210726213046072.png" alt="image-20210726213046072" style="zoom:80%;" />

* 在弹出的界面进行基本信息的填写

  <img src="D:/download/downloadFromMicsoft/day04-Maven&MyBatis/day04-1-Maven/ppt/assets/image-20210726213305893.png" alt="image-20210726213305893" style="zoom:80%;" />

* 点击完成后就能看到如下界面

  <img src="D:/download/downloadFromMicsoft/day04-Maven&MyBatis/day04-1-Maven/ppt/assets/image-20210726213541418.png" alt="image-20210726213541418" style="zoom:80%;" />

  而此界面就和 `navicat` 工具一样可以进行数据库的操作。也可以编写SQL语句

<img src="D:/download/downloadFromMicsoft/day04-Maven&MyBatis/day04-1-Maven/ppt/assets/image-20210726213857620.png" alt="image-20210726213857620" style="zoom:80%;" />

### 2.4  Mapper代理开发

#### 2.4.1  Mapper代理开发概述

之前写的代码是基本使用方式，它也存在硬编码的问题，如下：

<img src="D:/download/downloadFromMicsoft/day04-Maven&MyBatis/day04-1-Maven/ppt/assets/image-20210726214648112.png" alt="image-20210726214648112" style="zoom:80%;" />

这里调用 `selectList()` 方法传递的参数是映射配置文件中的 namespace.id值。这样写也不便于后期的维护。如果使用 Mapper 代理方式（如下图）则不存在硬编码问题。

<img src="D:/download/downloadFromMicsoft/day04-Maven&MyBatis/day04-1-Maven/ppt/assets/image-20210726214636108.png" alt="image-20210726214636108" style="zoom:80%;" />

通过上面的描述可以看出 Mapper 代理方式的目的：

* 解决原生方式中的硬编码
* 简化后期执行SQL

Mybatis 官网也是推荐使用 Mapper 代理的方式。下图是截止官网的图片

![image-20210726215339568](D:/download/downloadFromMicsoft/day04-Maven&MyBatis/day04-1-Maven/ppt/assets/image-20210726215339568.png)



使用maybatisX擦插件

#### 2.4.2  使用Mapper代理要求

使用Mapper代理方式，必须满足以下要求：

* 定义与SQL映射文件同名的Mapper接口，并且将Mapper接口和SQL映射文件放置在同一目录下。如下图：

  <img src="D:/download/downloadFromMicsoft/day04-Maven&MyBatis/day04-1-Maven/ppt/assets/image-20210726215946951.png" alt="image-20210726215946951" style="zoom:80%;" />

* 设置SQL映射文件的namespace属性为Mapper接口全限定名

  <img src="D:/download/downloadFromMicsoft/day04-Maven&MyBatis/day04-1-Maven/ppt/assets/image-20210726220053883.png" alt="image-20210726220053883" style="zoom:80%;" />

* 在 Mapper 接口中定义方法，方法名就是SQL映射文件中sql语句的id，并保持参数类型和返回值类型一致

  <img src="D:/download/downloadFromMicsoft/day04-Maven&MyBatis/day04-1-Maven/ppt/assets/image-20210726223216517.png" alt="image-20210726223216517" style="zoom:70%;" />

#### 2.4.3  案例代码实现

* 在 `com.itheima.mapper` 包下创建 UserMapper接口，代码如下：

  ```java
  public interface UserMapper {
      List<User> selectAll();
      User selectById(int id);
  }
  ```

* 在 `resources` 下创建 `com/itheima/mapper` 目录，并在该目录下创建 UserMapper.xml 映射配置文件

  ```xml
  <!--
      namespace:名称空间。必须是对应接口的全限定名
  -->
  <mapper namespace="com.itheima.mapper.UserMapper">
      <select id="selectAll" resultType="com.itheima.pojo.User">
          select *
          from tb_user;
      </select>
  </mapper>
  ```

* 在 `com.itheima` 包下创建 MybatisDemo2 测试类，代码如下：

  ```java
  /**
   * Mybatis 代理开发
   */
  public class MyBatisDemo2 {
  
      public static void main(String[] args) throws IOException {
  
          //1. 加载mybatis的核心配置文件，获取 SqlSessionFactory
          String resource = "mybatis-config.xml";
          InputStream inputStream = Resources.getResourceAsStream(resource);
          SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);
  
          //2. 获取SqlSession对象，用它来执行sql
          SqlSession sqlSession = sqlSessionFactory.openSession();
          //3. 执行sql
          //3.1 获取UserMapper接口的代理对象
       	//接口本身不能产生对象  
          UserMapper userMapper = sqlSession.getMapper(UserMapper.class);
          List<User> users = userMapper.selectAll();
  
          System.out.println(users);
          //4. 释放资源
          sqlSession.close();
      }
  }
  ```

==注意：==

如果Mapper接口名称和SQL映射文件名称相同，并在同一目录下，则可以使用包扫描的方式简化SQL映射文件的加载。也就是将核心配置文件的加载映射配置文件的配置修改为

```xml
<mappers>
    <!--加载sql映射文件-->
    <!-- <mapper resource="com/itheima/mapper/UserMapper.xml"/>-->
    <!--Mapper代理方式-->
    <package name="com.itheima.mapper"/>
</mappers>
```



### 2.5  核心配置文件

核心配置文件中现有的配置之前已经给大家进行了解释，而核心配置文件中还可以配置很多内容。可以通过查询官网看可以配置的内容

<img src="D:/download/downloadFromMicsoft/day04-Maven&MyBatis/day04-1-Maven/ppt/assets/image-20210726221454927.png" alt="image-20210726221454927" style="zoom:80%;" />

接下来先对里面的一些配置进行讲解。

#### 2.5.1  多环境配置

在核心配置文件的 `environments` 标签中其实是可以配置多个 `environment` ，使用 `id` 给每段环境起名，在 `environments` 中使用 `default='环境id'` 来指定使用哪儿段配置。一般就配置一个 `environment` 即可。

```xml
<environments default="development">
    <environment id="development">
        <transactionManager type="JDBC"/>
        <dataSource type="POOLED">
            <!--数据库连接信息-->
            <property name="driver" value="com.mysql.jdbc.Driver"/>
            <property name="url" value="jdbc:mysql:///mybatis?useSSL=false"/>
            <property name="username" value="root"/>
            <property name="password" value="1234"/>
        </dataSource>
    </environment>

    <environment id="test">
        <transactionManager type="JDBC"/>
        <dataSource type="POOLED">
            <!--数据库连接信息-->
            <property name="driver" value="com.mysql.jdbc.Driver"/>
            <property name="url" value="jdbc:mysql:///mybatis?useSSL=false"/>
            <property name="username" value="root"/>
            <property name="password" value="1234"/>
        </dataSource>
    </environment>
</environments>=
```

#### 2.4.2  类型别名

在映射配置文件中的 `resultType` 属性需要配置数据封装的类型（类的全限定名）。而每次这样写是特别麻烦的，Mybatis 提供了 `类型别名`(typeAliases) 可以简化这部分的书写。

首先需要现在核心配置文件中配置类型别名，也就意味着给pojo包下所有的类起了别名（别名就是类名），不区分大小写。内容如下：

```xml
<typeAliases>
    <!--name属性的值是实体类所在包-->
    <package name="com.itheima.pojo"/> 
</typeAliases>
```

通过上述的配置，就可以简化映射配置文件中 `resultType` 属性值的编写

```xml
<mapper namespace="com.itheima.mapper.UserMapper">
    <select id="selectAll" resultType="user">
        select * from tb_user;
    </select>
</mapper>
```

# Mybatis练习

**目标**

> * 能够使用映射配置文件实现CRUD操作
> * 能够使用注解实现CRUD操作

## 1，配置文件实现CRUD

![image-20210729111159534](D:/download/downloadFromMicsoft/day05-Mybatis/ppt/assets/image-20210729111159534.png)

如上图所示产品原型，里面包含了品牌数据的 `查询` 、`按条件查询`、`添加`、`删除`、`批量删除`、`修改` 等功能，而这些功能其实就是对数据库表中的数据进行CRUD操作。接下来就使用Mybatis完成品牌数据的增删改查操作。以下是要完成功能列表：

> * 查询
>   * 查询所有数据
>   * 查询详情
>   * 条件查询
> * 添加
> * 修改
>   * 修改全部字段
>   * 修改动态字段
> * 删除
>   * 删除一个
>   * 批量删除

先将必要的环境准备一下。

### 1.1  环境准备

* 数据库表（tb_brand）及数据准备

  ```sql
  -- 删除tb_brand表
  drop table if exists tb_brand;
  -- 创建tb_brand表
  create table tb_brand
  (
      -- id 主键
      id           int primary key auto_increment,
      -- 品牌名称
      brand_name   varchar(20),
      -- 企业名称
      company_name varchar(20),
      -- 排序字段
      ordered      int,
      -- 描述信息
      description  varchar(100),
      -- 状态：0：禁用  1：启用
      status       int
  );
  -- 添加数据
  insert into tb_brand (brand_name, company_name, ordered, description, status)
  values ('三只松鼠', '三只松鼠股份有限公司', 5, '好吃不上火', 0),
         ('华为', '华为技术有限公司', 100, '华为致力于把数字世界带入每个人、每个家庭、每个组织，构建万物互联的智能世界', 1),
         ('小米', '小米科技有限公司', 50, 'are you ok', 1);
  ```

* 实体类 Brand

  在 `com.itheima.pojo` 包下创建 Brand 实体类。

  ```java
  public class Brand {
      // id 主键
      private Integer id;
      // 品牌名称
      private String brandName;
      // 企业名称
      private String companyName;
      // 排序字段
      private Integer ordered;
      // 描述信息
      private String description;
      // 状态：0：禁用  1：启用
      private Integer status;
      
      //省略 setter and getter。自己写时要补全这部分代码
  }
  ```

* 编写测试用例

  测试代码需要在 `test/java` 目录下创建包及测试用例。项目结构如下：

  <img src="D:/download/downloadFromMicsoft/day05-Mybatis/ppt/assets/image-20210729112907106.png" alt="image-20210729112907106" style="zoom:80%;" />

* 安装 MyBatisX 插件

  * MybatisX 是一款基于 IDEA 的快速开发插件，为效率而生。

  * 主要功能

    * XML映射配置文件 和 接口方法 间相互跳转
    * 根据接口方法生成 statement 

  * 安装方式

    点击 `file` ，选择 `settings` ，就能看到如下图所示界面

    <img src="D:/download/downloadFromMicsoft/day05-Mybatis/ppt/assets/image-20210729113304743.png" alt="image-20210729113304743" style="zoom:80%;" />

    > 注意：安装完毕后需要重启IDEA

  * 插件效果

    <img src="D:/download/downloadFromMicsoft/day05-Mybatis/ppt/assets/image-20210729164450524.png" alt="image-20210729164450524" style="zoom:70%;" />

    红色头绳的表示映射配置文件，蓝色头绳的表示mapper接口。在mapper接口点击红色头绳的小鸟图标会自动跳转到对应的映射配置文件，在映射配置文件中点击蓝色头绳的小鸟图标会自动跳转到对应的mapper接口。也可以在mapper接口中定义方法，自动生成映射配置文件中的 `statement` ，如图所示

    ![image-20210729165337223](D:/download/downloadFromMicsoft/day05-Mybatis/ppt/assets/image-20210729165337223.png)

### 1.2  查询所有数据

<img src="D:/download/downloadFromMicsoft/day05-Mybatis/ppt/assets/image-20210729165724838.png" alt="image-20210729165724838" style="zoom:80%;" />

如上图所示就页面上展示的数据，而这些数据需要从数据库进行查询。接下来就来讲查询所有数据功能，而实现该功能分以下步骤进行实现：

* 编写接口方法：Mapper接口

  * 参数：无

    查询所有数据功能是不需要根据任何条件进行查询的，所以此方法不需要参数。

    <img src="D:/download/downloadFromMicsoft/day05-Mybatis/ppt/assets/image-20210729171208737.png" alt="image-20210729171208737" style="zoom:80%;" />

  * 结果：List<Brand>

    会将查询出来的每一条数据封装成一个 `Brand` 对象，而多条数据封装多个 `Brand` 对象，需要将这些对象封装到List集合中返回。

    <img src="D:/download/downloadFromMicsoft/day05-Mybatis/ppt/assets/image-20210729171146911.png" alt="image-20210729171146911" style="zoom:80%;" />

  * 执行方法、测试

#### 1.2.1  编写接口方法

在 `com.itheima.mapper` 包写创建名为 `BrandMapper` 的接口。并在该接口中定义 `List<Brand> selectAll()` 方法。

```java
public interface BrandMapper {

    /**
     * 查询所有
     */
    List<Brand> selectAll();
}
```

#### 1.2.2  编写SQL语句

在 `reources` 下创建 `com/itheima/mapper` 目录结构，并在该目录下创建名为 `BrandMapper.xml` 的映射配置文件

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">

<mapper namespace="com.itheima.mapper.BrandMapper">
    <select id="selectAll" resultType="brand">
        select *
        from tb_brand;
    </select>
</mapper>
```

#### 1.2.3  编写测试方法

在 `MybatisTest` 类中编写测试查询所有的方法

```java
@Test
public void testSelectAll() throws IOException {
    //1. 获取SqlSessionFactory
    String resource = "mybatis-config.xml";
    InputStream inputStream = Resources.getResourceAsStream(resource);
    SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);

    //2. 获取SqlSession对象
    SqlSession sqlSession = sqlSessionFactory.openSession();

    //3. 获取Mapper接口的代理对象
    BrandMapper brandMapper = sqlSession.getMapper(BrandMapper.class);

    //4. 执行方法
    List<Brand> brands = brandMapper.selectAll();
    System.out.println(brands);

    //5. 释放资源
    sqlSession.close();

}
```

> 注意：现在感觉测试这部分代码写起来特别麻烦，可以先忍忍。以后只会写上面的第3步的代码，其他的都不需要来完成。

执行测试方法结果如下：

![image-20210729172544230](D:/download/downloadFromMicsoft/day05-Mybatis/ppt/assets/image-20210729172544230.png)

从上面结果看到了问题，有些数据封装成功了，而有些数据并没有封装成功。为什么这样呢？

这个问题可以通过两种方式进行解决：

* 给字段起别名
* 使用resultMap定义字段和属性的映射关系

#### 1.2.4  起别名解决上述问题

从上面结果可以看到 `brandName` 和 `companyName` 这两个属性的数据没有封装成功，查询 实体类 和 表中的字段 发现，在实体类中属性名是 `brandName` 和 `companyName` ，而表中的字段名为 `brand_name` 和 `company_name`，如下图所示 。那么只需要保持这两部分的名称一致这个问题就迎刃而解。

<img src="D:/download/downloadFromMicsoft/day05-Mybatis/ppt/assets/image-20210729173210433.png" alt="image-20210729173210433" style="zoom:80%;" />

可以在写sql语句时给这两个字段起别名，将别名定义成和属性名一致即可。

```xml
<select id="selectAll" resultType="brand">
    select
    id, brand_name as brandName, company_name as companyName, ordered, description, status
    from tb_brand;
</select>
```

而上面的SQL语句中的字段列表书写麻烦，如果表中还有更多的字段，同时其他的功能也需要查询这些字段时就显得的代码不够精炼。Mybatis提供了`sql` 片段可以提高sql的复用性。

**SQL片段：**

* 将需要复用的SQL片段抽取到 `sql` 标签中

  ```xml
  <sql id="brand_column">
  	id, brand_name as brandName, company_name as companyName, ordered, description, status
  </sql>
  ```

  id属性值是唯一标识，引用时也是通过该值进行引用。

* 在原sql语句中进行引用

  使用 `include` 标签引用上述的 SQL 片段，而 `refid` 指定上述 SQL 片段的id值。

  ```xml
  <select id="selectAll" resultType="brand">
      select
      <include refid="brand_column" />
      from tb_brand;
  </select>
  ```

#### 1.2.5  使用resultMap解决上述问题

起别名 + sql片段的方式可以解决上述问题，但是它也存在问题。如果还有功能只需要查询部分字段，而不是查询所有字段，那么就需要再定义一个 SQL 片段，这就显得不是那么灵活。

那么也可以使用resultMap来定义字段和属性的映射关系的方式解决上述问题。

* 在映射配置文件中使用resultMap定义 字段 和 属性 的映射关系

  ```xml
  <resultMap id="brandResultMap" type="brand">
      <!--
              id：完成主键字段的映射
                  column：表的列名
                  property：实体类的属性名
              result：完成一般字段的映射
                  column：表的列名
                  property：实体类的属性名
          -->
      <result column="brand_name" property="brandName"/>
      <result column="company_name" property="companyName"/>
  </resultMap>
  ```

  > 注意：在上面只需要定义 字段名 和 属性名 不一样的映射，而一样的则不需要专门定义出来。

* SQL语句正常编写

  ```xml
  <select id="selectAll" resultMap="brandResultMap">
      select *
      from tb_brand;
  </select>
  ```

#### 1.2.6  小结

实体类属性名 和 数据库表列名 不一致，不能自动封装数据

* ==起别名：==在SQL语句中，对不一样的列名起别名，别名和实体类属性名一样
  * 可以定义 <sql>片段，提升复用性 
* ==resultMap：==定义<resultMap> 完成不一致的属性名和列名的映射

而最终选择使用 resultMap的方式。查询映射配置文件中查询所有的 statement 书写如下：

```xml
 <resultMap id="brandResultMap" type="brand">
     <!--
            id：完成主键字段的映射
                column：表的列名
                property：实体类的属性名
            result：完成一般字段的映射
                column：表的列名
                property：实体类的属性名
        -->
     <result column="brand_name" property="brandName"/>
     <result column="company_name" property="companyName"/>
</resultMap>



<select id="selectAll" resultMap="brandResultMap">
    select *
    from tb_brand;
</select>
```



### 1.3  查询详情

<img src="D:/download/downloadFromMicsoft/day05-Mybatis/ppt/assets/image-20210729180118287.png" alt="image-20210729180118287" style="zoom:80%;" />

有些数据的属性比较多，在页面表格中无法全部实现，而只会显示部分，而其他属性数据的查询可以通过 `查看详情` 来进行查询，如上图所示。

查看详情功能实现步骤：

* 编写接口方法：Mapper接口

  <img src="D:/download/downloadFromMicsoft/day05-Mybatis/ppt/assets/image-20210729180604529.png" alt="image-20210729180604529" style="zoom:80%;" />

  * 参数：id

    查看详情就是查询某一行数据，所以需要根据id进行查询。而id以后是由页面传递过来。

  * 结果：Brand

    根据id查询出来的数据只要一条，而将一条数据封装成一个Brand对象即可

* 编写SQL语句：SQL映射文件

  <img src="D:/download/downloadFromMicsoft/day05-Mybatis/ppt/assets/image-20210729180709318.png" alt="image-20210729180709318" style="zoom:80%;" />

* 执行方法、进行测试

#### 1.3.1  编写接口方法

在 `BrandMapper` 接口中定义根据id查询数据的方法 

```java
/**
  * 查看详情：根据Id查询
  */
Brand selectById(int id);
```

#### 1.3.2  编写SQL语句

在 `BrandMapper.xml` 映射配置文件中编写 `statement`，使用 `resultMap` 而不是使用 `resultType`

resultMap完成表字段与类数据类型的对应

```xml
 <resultMap id="brandResultMap" type="brand">
     <!--
            id：完成主键字段的映射
                column：表的列名
                property：实体类的属性名
            result：完成一般字段的映射
                column：表的列名
                property：实体类的属性名
        -->
     <result column="brand_name" property="brandName"/>
     <result column="company_name" property="companyName"/>
</resultMap>
```



```xml
<select id="selectById"  resultMap="brandResultMap">
    select *
    from tb_brand where id = #{id};
</select>
```

> 注意：上述SQL中的 #{id}先这样写，一会再详细讲解

#### 1.3.3  编写测试方法

在 `test/java` 下的 `com.itheima.mapper`  包下的 `MybatisTest类中` 定义测试方法

```java
 @Test
public void testSelectById() throws IOException {
    //接收参数，该id以后需要传递过来
    int id = 1;

    //1. 获取SqlSessionFactory
    String resource = "mybatis-config.xml";
    InputStream inputStream = Resources.getResourceAsStream(resource);
    SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);

    //2. 获取SqlSession对象
    SqlSession sqlSession = sqlSessionFactory.openSession();

    //3. 获取Mapper接口的代理对象
    BrandMapper brandMapper = sqlSession.getMapper(BrandMapper.class);

    //4. 执行方法
    Brand brand = brandMapper.selectById(id);
    System.out.println(brand);

    //5. 释放资源
    sqlSession.close();
}
```

执行测试方法结果如下：

<img src="D:/download/downloadFromMicsoft/day05-Mybatis/ppt/assets/image-20210729182223137.png" alt="image-20210729182223137" style="zoom:70%;" />

### 知识速递

#### 1.3.4参数占位符

查询到的结果很好理解就是id为1的这行数据。而这里需要看控制台显示的SQL语句，能看到使用？进行占位。说明在映射配置文件中的写的 `#{id}` 最终会被？进行占位。接下来就聊聊映射配置文件中的参数占位符。

mybatis提供了两种参数占位符：

* #{} ：执行SQL时，会将 #{} 占位符替换为？，将来自动设置参数值。从上述例子可以看出使用#{} 底层使用的是 `PreparedStatement`

* ${} ：拼接SQL。底层使用的是 `Statement`，会存在SQL注入问题。如下图将 映射配置文件中的 #{} 替换成 ${} 来看效果

  ```xml
  <select id="selectById"  resultMap="brandResultMap">
      select *
      from tb_brand where id = ${id};
  </select>
  ```

  重新运行查看结果如下：

  <img src="D:/download/downloadFromMicsoft/day05-Mybatis/ppt/assets/image-20210729184156019.png" alt="image-20210729184156019" style="zoom:70%;" />

> ==注意：==从上面两个例子可以看出，以后开发使用 #{} 参数占位符。

#### 1.3.5  parameterType使用

对于有参数的mapper接口方法，在映射配置文件中应该配置 `ParameterType` 来指定参数类型。只不过该属性都可以省略。如下图：

```xml
<select id="selectById" parameterType="int" resultMap="brandResultMap">
    select *
    from tb_brand where id = ${id};
</select>
```

#### 1.3.6  SQL语句中特殊字段处理

以后肯定会在SQL语句中写一下特殊字符，比如某一个字段大于某个值，如下图

<img src="D:/download/downloadFromMicsoft/day05-Mybatis/ppt/assets/image-20210729184756094.png" alt="image-20210729184756094" style="zoom:80%;" />

可以看出报错了，因为映射配置文件是xml类型的问题，而 > < 等这些字符在xml中有特殊含义，所以此时需要将这些符号进行转义，可以使用以下两种方式进行转义

* 转义字符

  下图的 `&lt;` 就是 `<` 的转义字符。

  <img src="D:/download/downloadFromMicsoft/day05-Mybatis/ppt/assets/image-20210729185128686.png" alt="image-20210729185128686" style="zoom:60%;" />

* <![CDATA[内容]]>

  <img src="D:/download/downloadFromMicsoft/day05-Mybatis/ppt/assets/image-20210729185030318.png" alt="image-20210729185030318" style="zoom:60%;" />

### 1.4  多条件查询

![image-20210729203804276](D:/download/downloadFromMicsoft/day05-Mybatis/ppt/assets/image-20210729203804276.png)

经常会遇到如上图所示的多条件查询，将多条件查询的结果展示在下方的数据列表中。而做这个功能需要分析最终的SQL语句应该是什么样，思考两个问题

* 条件表达式
* 如何连接

条件字段 `企业名称`  和 `品牌名称` 需要进行模糊查询，所以条件应该是：

<img src="D:/download/downloadFromMicsoft/day05-Mybatis/ppt/assets/image-20210729204458815.png" alt="image-20210729204458815" style="zoom:70%;" />

简单的分析后，来看功能实现的步骤：

* 编写接口方法
  * 参数：所有查询条件
  * 结果：List<Brand>
* 在映射配置文件中编写SQL语句

* 编写测试方法并执行

#### 1.4.1  编写接口方法

在 `BrandMapper` 接口中定义多条件查询的方法。

而该功能有三个参数，就需要考虑定义接口时，参数应该如何定义。Mybatis针对多参数有多种实现

* 使用 `@Param("参数名称")` 标记每一个参数，在映射配置文件中就需要使用 `#{参数名称}` 进行占位

  ```java
  List<Brand> selectByCondition(@Param("status") int status, @Param("companyName") String companyName,@Param("brandName") String brandName);
  ```

* 将多个参数封装成一个 实体对象 ，将该实体对象作为接口的方法参数。该方式要求在映射配置文件的SQL中使用 `#{内容}` 时，里面的内容必须和实体类属性名保持一致。

  ```java
  List<Brand> selectByCondition(Brand brand);
  ```

* 将多个参数封装到map集合中，将map集合作为接口的方法参数。该方式要求在映射配置文件的SQL中使用 `#{内容}` 时，里面的内容必须和map集合中键的名称一致。

  ```
  List<Brand> selectByCondition(Map map);
  ```

#### 1.4.2  编写SQL语句

在 `BrandMapper.xml` 映射配置文件中编写 `statement`，使用 `resultMap` 而不是使用 `resultType`

```xml
<select id="selectByCondition" resultMap="brandResultMap">
    select *
    from tb_brand
    where status = #{status}
    and company_name like #{companyName}
    and brand_name like #{brandName}
</select>
```

#### 1.4.3  编写测试方法

在 `test/java` 下的 `com.itheima.mapper`  包下的 `MybatisTest类中` 定义测试方法

```java
@Test
public void testSelectByCondition() throws IOException {
    //接收参数
    int status = 1;
    String companyName = "华为";
    String brandName = "华为";

    // 处理参数
    companyName = "%" + companyName + "%";
    brandName = "%" + brandName + "%";

    //1. 获取SqlSessionFactory
    String resource = "mybatis-config.xml";
    InputStream inputStream = Resources.getResourceAsStream(resource);
    SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);
    //2. 获取SqlSession对象
    SqlSession sqlSession = sqlSessionFactory.openSession();
    //3. 获取Mapper接口的代理对象
    BrandMapper brandMapper = sqlSession.getMapper(BrandMapper.class);

    //4. 执行方法
	//方式一 ：接口方法参数使用 @Param 方式调用的方法
    //List<Brand> brands = brandMapper.selectByCondition(status, companyName, brandName);
    //方式二 ：接口方法参数是 实体类对象 方式调用的方法
     //封装对象
    /* Brand brand = new Brand();
        brand.setStatus(status);
        brand.setCompanyName(companyName);
        brand.setBrandName(brandName);*/
    
    //List<Brand> brands = brandMapper.selectByCondition(brand);
    
    //方式三 ：接口方法参数是 map集合对象 方式调用的方法
    Map map = new HashMap();
    map.put("status" , status);
    map.put("companyName", companyName);
    map.put("brandName" , brandName);
    List<Brand> brands = brandMapper.selectByCondition(map);
    System.out.println(brands);

    //5. 释放资源
    sqlSession.close();
}
```

#### 1.4.4  动态SQL

上述功能实现存在很大的问题。用户在输入条件时，肯定不会所有的条件都填写，这个时候的SQL语句就不能那样写的

例如用户只输入 当前状态 时，SQL语句就是

```sql
select * from tb_brand where status = #{status}
```

而用户如果只输入企业名称时，SQL语句就是

```sql
select * from tb_brand where company_name like #{companName}
```

而用户如果输入了 `当前状态` 和 `企业名称 ` 时，SQL语句又不一样

```sql
select * from tb_brand where status = #{status} and company_name like #{companName}
```

针对上述的需要，Mybatis对动态SQL有很强大的支撑：

> * if
>
> * choose (when, otherwise)
>
> * trim (where, set)
>
> * foreach

先学习 if 标签和 where 标签：

* if 标签：条件判断

  * test 属性：逻辑表达式

  ```xml
  <select id="selectByCondition" resultMap="brandResultMap">
      select *
      from tb_brand
      where
          <if test="status != null">
              and status = #{status}
          </if>
          <if test="companyName != null and companyName != '' ">
              and company_name like #{companyName}
          </if>
          <if test="brandName != null and brandName != '' ">
              and brand_name like #{brandName}
          </if>
  </select>
  ```

  如上的这种SQL语句就会根据传递的参数值进行动态的拼接。如果此时status和companyName有值那么就会值拼接这两个条件。

  执行结果如下：

  ![image-20210729212510291](D:/download/downloadFromMicsoft/day05-Mybatis/ppt/assets/image-20210729212510291.png)

  但是它也存在问题，如果此时给的参数值是

  ```java
  Map map = new HashMap();
  // map.put("status" , status);
  map.put("companyName", companyName);
  map.put("brandName" , brandName);
  ```

  拼接的SQL语句就变成了

  ```sql
  select * from tb_brand where and company_name like ? and brand_name like ?
  ```

  而上面的语句中 where 关键后直接跟 and 关键字，这就是一条错误的SQL语句。这个就可以使用 where 标签解决

* where 标签

  * 作用：
    * 替换where关键字
    * 会动态的去掉第一个条件前的 and 
    * 如果所有的参数没有值则不加where关键字

  ```xml
  <select id="selectByCondition" resultMap="brandResultMap">
      select *
      from tb_brand
      <where>
          <if test="status != null">
              and status = #{status}
          </if>
          <if test="companyName != null and companyName != '' ">
              and company_name like #{companyName}
          </if>
          <if test="brandName != null and brandName != '' ">
              and brand_name like #{brandName}
          </if>
      </where>
  </select>
  ```

  > 注意：需要给每个条件前都加上 and 关键字。

### 1.5 单个条件（动态SQL）

<img src="D:/download/downloadFromMicsoft/day05-Mybatis/ppt/assets/image-20210729213613029.png" alt="image-20210729213613029" style="zoom:80%;" />

如上图所示，在查询时只能选择 `品牌名称`、`当前状态`、`企业名称` 这三个条件中的一个，但是用户到底选择哪儿一个，并不能确定。这种就属于单个条件的动态SQL语句。 

这种需求需要使用到  `choose（when，otherwise）标签`  实现，  而 `choose` 标签类似于Java 中的switch语句。

通过一个案例来使用这些标签

#### 1.5.1  编写接口方法

在 `BrandMapper` 接口中定义单条件查询的方法。

```java
/**
  * 单条件动态查询
  * @param brand
  * @return
  */
List<Brand> selectByConditionSingle(Brand brand);
```

#### 1.5.2  编写SQL语句

在 `BrandMapper.xml` 映射配置文件中编写 `statement`，使用 `resultMap` 而不是使用 `resultType`

like是模糊匹配   

如代码,匹配任意包含wzt的字符串！！！

```xml
where name like '%wzt%';
```

```xml
<select id="selectByConditionSingle" resultMap="brandResultMap">
    select *
    from tb_brand
    <where>
        <choose><!--相当于switch-->
            <when test="status != null"><!--相当于case-->
                status = #{status}
            </when>
            <when test="companyName != null and companyName != '' "><!--相当于case-->
                company_name like #{companyName}
            </when>
            <when test="brandName != null and brandName != ''"><!--相当于case-->
                brand_name like #{brandName}
            </when>
        </choose>
    </where>
</select>
```

#### 1.5.3  编写测试方法

在 `test/java` 下的 `com.itheima.mapper`  包下的 `MybatisTest类中` 定义测试方法

```java
@Test
public void testSelectByConditionSingle() throws IOException {
    //接收参数
    int status = 1;
    String companyName = "华为";
    String brandName = "华为";

    // 处理参数
    //模糊匹配
    companyName = "%" + companyName + "%";
    brandName = "%" + brandName + "%";

    //封装对象
    Brand brand = new Brand();
    //brand.setStatus(status);
    brand.setCompanyName(companyName);
    //brand.setBrandName(brandName);

    //1. 获取SqlSessionFactory
    String resource = "mybatis-config.xml";
    InputStream inputStream = Resources.getResourceAsStream(resource);
    SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);
    //2. 获取SqlSession对象
    SqlSession sqlSession = sqlSessionFactory.openSession();
    //3. 获取Mapper接口的代理对象
    BrandMapper brandMapper = sqlSession.getMapper(BrandMapper.class);
    //4. 执行方法
    List<Brand> brands = brandMapper.selectByConditionSingle(brand);
    System.out.println(brands);

    //5. 释放资源
    sqlSession.close();
}
```

执行测试方法结果如下：

<img src="D:/download/downloadFromMicsoft/day05-Mybatis/ppt/assets/image-20210729214548756.png" alt="image-20210729214548756" style="zoom:70%;" />

### 1.6  添加数据

<img src="D:/download/downloadFromMicsoft/day05-Mybatis/ppt/assets/image-20210729214917317.png" alt="image-20210729214917317" style="zoom:70%;" />

如上图是平时在添加数据时展示的页面，而在该页面输入想要的数据后添加 `提交` 按钮，就会将这些数据添加到数据库中。接下来就来实现添加数据的操作。

* 编写接口方法

  <img src="D:/download/downloadFromMicsoft/day05-Mybatis/ppt/assets/image-20210729215351651.png" alt="image-20210729215351651" style="zoom:80%;" />

  参数：除了id之外的所有的数据。id对应的是表中主键值，而主键是 ==自动增长== 生成的。

* 编写SQL语句

  <img src="D:/download/downloadFromMicsoft/day05-Mybatis/ppt/assets/image-20210729215537167.png" alt="image-20210729215537167" style="zoom:80%;" />

* 编写测试方法并执行

明确了该功能实现的步骤后，接下来进行具体的操作。

#### 1.6.1  编写接口方法

在 `BrandMapper` 接口中定义添加方法。

```java
 /**
   * 添加
   */
void add(Brand brand);
```

#### 1.6.2  编写SQL语句

在 `BrandMapper.xml` 映射配置文件中编写添加数据的 `statement`

```xml
<insert id="add">
    insert into tb_brand (brand_name, company_name, ordered, description, status)
    values (#{brandName}, #{companyName}, #{ordered}, #{description}, #{status});
</insert>
```

#### 1.6.3  编写测试方法

在 `test/java` 下的 `com.itheima.mapper`  包下的 `MybatisTest类中` 定义测试方法

```java
@Test
public void testAdd() throws IOException {
    //接收参数
    int status = 1;
    String companyName = "波导手机";
    String brandName = "波导";
    String description = "手机中的战斗机";
    int ordered = 100;

    //封装对象
    Brand brand = new Brand();
    brand.setStatus(status);
    brand.setCompanyName(companyName);
    brand.setBrandName(brandName);
    brand.setDescription(description);
    brand.setOrdered(ordered);

    //1. 获取SqlSessionFactory
    String resource = "mybatis-config.xml";
    InputStream inputStream = Resources.getResourceAsStream(resource);
    SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);
    //2. 获取SqlSession对象
    SqlSession sqlSession = sqlSessionFactory.openSession();
    //SqlSession sqlSession = sqlSessionFactory.openSession(true); //设置自动提交事务，这种情况不需要手动提交事务了
    //3. 获取Mapper接口的代理对象
    BrandMapper brandMapper = sqlSession.getMapper(BrandMapper.class);
    //4. 执行方法
    brandMapper.add(brand);
    //提交事务
    sqlSession.commit();
    //5. 释放资源
    sqlSession.close();
}
```

执行结果如下：

![image-20210729220348255](D:/download/downloadFromMicsoft/day05-Mybatis/ppt/assets/image-20210729220348255.png)

#### 1.6.4  添加-主键返回

在数据添加成功后，有时候需要获取插入数据库数据的主键（主键是自增长）。

比如：添加订单和订单项，如下图就是京东上的订单

<img src="D:/download/downloadFromMicsoft/day05-Mybatis/ppt/assets/image-20210729221207962.png" alt="image-20210729221207962" style="zoom:80%;" />

订单数据存储在订单表中，订单项存储在订单项表中。

* 添加订单数据

  <img src="D:/download/downloadFromMicsoft/day05-Mybatis/ppt/assets/image-20210729221049462.png" alt="image-20210729221049462" style="zoom:80%;" />

* 添加订单项数据，订单项中需要设置所属订单的id

  <img src="D:/download/downloadFromMicsoft/day05-Mybatis/ppt/assets/image-20210729221058898.png" alt="image-20210729221058898" style="zoom:80%;" />

明白了什么时候 `主键返回` 。接下来简单模拟一下，在添加完数据后打印id属性值，能打印出来说明已经获取到了。

将上面添加品牌数据的案例中映射配置文件里 `statement` 进行修改，如下

```xml
<insert id="add" useGeneratedKeys="true" keyProperty="id">
    insert into tb_brand (brand_name, company_name, ordered, description, status)
    values (#{brandName}, #{companyName}, #{ordered}, #{description}, #{status});
</insert>
```

> 在 insert 标签上添加如下属性：
>
> * useGeneratedKeys：是够获取自动增长的主键值。true表示获取
> * keyProperty  ：指定将获取到的主键值封装到哪儿个属性里

### 1.7  修改（动态）

<img src="D:/download/downloadFromMicsoft/day05-Mybatis/ppt/assets/image-20210729222642700.png" alt="image-20210729222642700" style="zoom:80%;" />

如图所示是修改页面，用户在该页面书写需要修改的数据，点击 `提交` 按钮，就会将数据库中对应的数据进行修改。注意一点，如果哪儿个输入框没有输入内容，是将表中数据对应字段值替换为空白还是保留字段之前的值？答案肯定是保留之前的数据。

接下来就具体来实现

#### 1.7.1  编写接口方法

在 `BrandMapper` 接口中定义修改方法。

```java
 /**
   * 修改
   */
void update(Brand brand);
```

> 上述方法参数 Brand 就是封装了需要修改的数据，而id肯定是有数据的，这也是和添加方法的区别。

#### 1.7.2  编写SQL语句

在 `BrandMapper.xml` 映射配置文件中编写修改数据的 `statement`。

```xml
<update id="update">
    update tb_brand
    <set>
        <if test="brandName != null and brandName != ''">
            brand_name = #{brandName},
        </if>
        <if test="companyName != null and companyName != ''">
            company_name = #{companyName},
        </if>
        <if test="ordered != null">
            ordered = #{ordered},
        </if>
        <if test="description != null and description != ''">
            description = #{description},
        </if>
        <if test="status != null">
            status = #{status}
        </if>
    </set>
    where id = #{id};
</update>
```

> *set* 标签可以用于动态包含需要更新的列，忽略其它不更新的列。

#### 1.7.3  编写测试方法

在 `test/java` 下的 `com.itheima.mapper`  包下的 `MybatisTest类中` 定义测试方法

```java
@Test
public void testUpdate() throws IOException {
    //接收参数
    int status = 0;
    String companyName = "波导手机";
    String brandName = "波导";
    String description = "波导手机,手机中的战斗机";
    int ordered = 200;
    int id = 6;

    //封装对象
    Brand brand = new Brand();
    brand.setStatus(status);
    //        brand.setCompanyName(companyName);
    //        brand.setBrandName(brandName);
    //        brand.setDescription(description);
    //        brand.setOrdered(ordered);
    brand.setId(id);

    //1. 获取SqlSessionFactory
    String resource = "mybatis-config.xml";
    InputStream inputStream = Resources.getResourceAsStream(resource);
    SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);
    //2. 获取SqlSession对象
    SqlSession sqlSession = sqlSessionFactory.openSession();
    //SqlSession sqlSession = sqlSessionFactory.openSession(true);
    //3. 获取Mapper接口的代理对象
    BrandMapper brandMapper = sqlSession.getMapper(BrandMapper.class);
    //4. 执行方法
    int count = brandMapper.update(brand);
    System.out.println(count);
    //提交事务
    sqlSession.commit();
    //5. 释放资源
    sqlSession.close();
}
```

执行测试方法结果如下：

![image-20210729224205522](D:/download/downloadFromMicsoft/day05-Mybatis/ppt/assets/image-20210729224205522.png)

从结果中SQL语句可以看出，只修改了 `status`  字段值，因为给的数据中只给Brand实体对象的 `status` 属性设置值了。这就是 `set` 标签的作用。

### 1.8  删除一行数据

![image-20210729224549305](D:/download/downloadFromMicsoft/day05-Mybatis/ppt/assets/image-20210729224549305.png)

如上图所示，每行数据后面都有一个 `删除` 按钮，当用户点击了该按钮，就会将改行数据删除掉。那就需要思考，这种删除是根据什么进行删除呢？是通过主键id删除，因为id是表中数据的唯一标识。

接下来就来实现该功能。

#### 1.8.1  编写接口方法

在 `BrandMapper` 接口中定义根据id删除方法。

```java
/**
  * 根据id删除
  */
void deleteById(int id);
```

#### 1.8.2  编写SQL语句

在 `BrandMapper.xml` 映射配置文件中编写删除一行数据的 `statement`

```xml
<delete id="deleteById">
    delete from tb_brand where id = #{id};
</delete>
```

#### 1.8.3  编写测试方法

在 `test/java` 下的 `com.itheima.mapper`  包下的 `MybatisTest类中` 定义测试方法

```java
 @Test
public void testDeleteById() throws IOException {
    //接收参数
    int id = 6;

    //1. 获取SqlSessionFactory
    String resource = "mybatis-config.xml";
    InputStream inputStream = Resources.getResourceAsStream(resource);
    SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);
    //2. 获取SqlSession对象
    SqlSession sqlSession = sqlSessionFactory.openSession();
    //SqlSession sqlSession = sqlSessionFactory.openSession(true);
    //3. 获取Mapper接口的代理对象
    BrandMapper brandMapper = sqlSession.getMapper(BrandMapper.class);
    //4. 执行方法
    brandMapper.deleteById(id);
    //提交事务
    sqlSession.commit();
    //5. 释放资源
    sqlSession.close();
}
```

运行过程只要没报错，直接到数据库查询数据是否还存在。

### 1.9  批量删除

<img src="D:/download/downloadFromMicsoft/day05-Mybatis/ppt/assets/image-20210729225713894.png" alt="image-20210729225713894" style="zoom:70%;" />



如上图所示，用户可以选择多条数据，然后点击上面的 `删除` 按钮，就会删除数据库中对应的多行数据。



#### 1.9.1  编写接口方法

在 `BrandMapper` 接口中定义删除多行数据的方法。

```java
/**
  * 批量删除
  */
void deleteByIds(int[] ids);
```

> 参数是一个数组，数组中存储的是多条数据的id

#### 1.9.2  编写SQL语句

在 `BrandMapper.xml` 映射配置文件中编写删除多条数据的 `statement`。

编写SQL时需要遍历数组来拼接SQL语句。Mybatis 提供了 `foreach` 标签供使用

**foreach 标签**

用来迭代任何可迭代的对象（如数组，集合）。

* collection 属性：
  * mybatis会将数组参数，封装为一个Map集合。
    * 默认：array = 数组
    * 使用@Param注解改变map集合的默认key的名称
* item 属性：本次迭代获取到的元素。
* separator 属性：集合项迭代之间的分隔符。`foreach` 标签不会错误地添加多余的分隔符。也就是最后一次迭代不会加分隔符。
* open 属性：该属性值是在拼接SQL语句之前拼接的语句，只会拼接一次
* close 属性：该属性值是在拼接SQL语句拼接后拼接的语句，只会拼接一次

```xml
<delete id="deleteByIds">
    delete from tb_brand where id
    in
    <foreach collection="array" item="id" separator="," open="(" close=")">
        #{id}
    </foreach>
    ;
</delete>
```

> 假如数组中的id数据是{1,2,3}，那么拼接后的sql语句就是：
>
> ```sql
> delete from tb_brand where id in (1,2,3);
> ```

#### 1.9.3  编写测试方法

在 `test/java` 下的 `com.itheima.mapper`  包下的 `MybatisTest类中` 定义测试方法

```java
@Test
public void testDeleteByIds() throws IOException {
    //接收参数
    int[] ids = {5,7,8};

    //1. 获取SqlSessionFactory
    String resource = "mybatis-config.xml";
    InputStream inputStream = Resources.getResourceAsStream(resource);
    SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);
    //2. 获取SqlSession对象
    SqlSession sqlSession = sqlSessionFactory.openSession();
    //SqlSession sqlSession = sqlSessionFactory.openSession(true);
    //3. 获取Mapper接口的代理对象
    BrandMapper brandMapper = sqlSession.getMapper(BrandMapper.class);
    //4. 执行方法
    brandMapper.deleteByIds(ids);
    //提交事务
    sqlSession.commit();
    //5. 释放资源
    sqlSession.close();
}
```

### 1.10  Mybatis参数传递

Mybatis 接口方法中可以接收各种各样的参数，如下：

* 多个参数
* 单个参数：单个参数又可以是如下类型
  * POJO 类型
  * Map 集合类型
  * Collection 集合类型
  * List 集合类型
  * Array 类型
  * 其他类型

#### 1.10.1  多个参数

如下面的代码，就是接收两个参数，而接收多个参数需要使用 `@Param` 注解，那么为什么要加该注解呢？这个问题要弄明白就必须来研究Mybatis 底层对于这些参数是如何处理的。

```java
User select(@Param("username") String username,@Param("password") String password);
```

```xml
<select id="select" resultType="user">
	select *
    from tb_user
    where 
    	username=#{username}
    	and password=#{password}
</select>
```

在接口方法中定义多个参数，Mybatis 会将这些参数封装成 Map 集合对象，值就是参数值，而键在没有使用 `@Param` 注解时有以下命名规则：

* 以 arg 开头  ：第一个参数就叫 arg0，第二个参数就叫 arg1，以此类推。如：

  > map.put("arg0"，参数值1);
  >
  > map.put("arg1"，参数值2);

* 以 param 开头 ： 第一个参数就叫 param1，第二个参数就叫 param2，依次类推。如：

  > map.put("param1"，参数值1);
  >
  > map.put("param2"，参数值2);

**代码验证：**

* 在 `UserMapper` 接口中定义如下方法

  ```java
  User select(String username,String password);
  ```

* 在 `UserMapper.xml` 映射配置文件中定义SQL

  ```xml
  <select id="select" resultType="user">
  	select *
      from tb_user
      where 
      	username=#{arg0}
      	and password=#{arg1}
  </select>
  ```

  或者

  ```xml
  <select id="select" resultType="user">
  	select *
      from tb_user
      where 
      	username=#{param1}
      	and password=#{param2}
  </select>
  ```

* 运行代码结果如下

  <img src="D:/download/downloadFromMicsoft/day05-Mybatis/ppt/assets/image-20210805230303461.png" alt="image-20210805230303461" style="zoom:80%;" />

  在映射配合文件的SQL语句中使用用 `arg` 开头的和 `param` 书写，代码的可读性会变的特别差，此时可以使用 `@Param` 注解。

在接口方法参数上使用 `@Param` 注解，Mybatis 会将 `arg` 开头的键名替换为对应注解的属性值。

**代码验证：**

* 在 `UserMapper` 接口中定义如下方法，在 `username` 参数前加上 `@Param` 注解

  ```java
  User select(@Param("username") String username, String password);
  ```

  Mybatis 在封装 Map 集合时，键名就会变成如下：

  > map.put("username"，参数值1);
  >
  > map.put("arg1"，参数值2);
  >
  > map.put("param1"，参数值1);
  >
  > map.put("param2"，参数值2);

* 在 `UserMapper.xml` 映射配置文件中定义SQL

  ```xml
  <select id="select" resultType="user">
  	select *
      from tb_user
      where 
      	username=#{username}
      	and password=#{param2}
  </select>
  ```

* 运行程序结果没有报错。而如果将 `#{}` 中的 `username` 还是写成  `arg0` 

  ```xml
  <select id="select" resultType="user">
  	select *
      from tb_user
      where 
      	username=#{arg0}
      	and password=#{param2}
  </select>
  ```

* 运行程序则可以看到错误

  ![image-20210805231727206](D:/download/downloadFromMicsoft/day05-Mybatis/ppt/assets/image-20210805231727206.png)

==结论：以后接口参数是多个时，在每个参数上都使用 `@Param` 注解。这样代码的可读性更高。==

#### 1.10.2  单个参数

* POJO 类型

  直接使用。要求 `属性名` 和 `参数占位符名称` 一致

* Map 集合类型

  直接使用。要求 `map集合的键名` 和 `参数占位符名称` 一致

* Collection 集合类型

  Mybatis 会将集合封装到 map 集合中，如下：

  > map.put("arg0"，collection集合);
  >
  > map.put("collection"，collection集合;

  ==可以使用 `@Param` 注解替换map集合中默认的 arg 键名。==

* List 集合类型

  Mybatis 会将集合封装到 map 集合中，如下：

  > map.put("arg0"，list集合);
  >
  > map.put("collection"，list集合);
  >
  > map.put("list"，list集合);

  ==可以使用 `@Param` 注解替换map集合中默认的 arg 键名。==

* Array 类型

  Mybatis 会将集合封装到 map 集合中，如下：

  > map.put("arg0"，数组);
  >
  > map.put("array"，数组);

  ==可以使用 `@Param` 注解替换map集合中默认的 arg 键名。==

* 其他类型

  比如int类型，`参数占位符名称` 叫什么都可以。尽量做到见名知意

## 2，注解实现CRUD

使用注解开发会比配置文件开发更加方便。如下就是使用注解进行开发

```java
@Select(value = "select * from tb_user where id = #{id}")
public User select(int id);
```

> ==注意：==
>
> * 注解是用来替换映射配置文件方式配置的，所以使用了注解，就不需要再映射配置文件中书写对应的 `statement`

Mybatis 针对 CURD 操作都提供了对应的注解，已经做到见名知意。如下：

* 查询 ：@Select
* 添加 ：@Insert
* 修改 ：@Update
* 删除 ：@Delete

接下来做一个案例来使用 Mybatis 的注解开发

**代码实现：**

* 将之前案例中 `UserMapper.xml` 中的 根据id查询数据 的 `statement` 注释掉

  <img src="D:/download/downloadFromMicsoft/day05-Mybatis/ppt/assets/image-20210805235229938.png" alt="image-20210805235229938" style="zoom:70%;" />

* 在 `UserMapper` 接口的 `selectById` 方法上添加注解

  <img src="D:/download/downloadFromMicsoft/day05-Mybatis/ppt/assets/image-20210805235405070.png" alt="image-20210805235405070" style="zoom:70%;" />

* 运行测试程序也能正常查询到数据

课程上只演示这一个查询的注解开发，其他的同学们下来可以自己实现，都是比较简单。

==注意：==在官方文档中 `入门` 中有这样的一段话：

![image-20210805234302849](D:/download/downloadFromMicsoft/day05-Mybatis/ppt/assets/image-20210805234302849.png)

所以，==注解完成简单功能，配置文件完成复杂功能。==

而之前写的动态 SQL 就是复杂的功能，如果用注解使用的话，就需要使用到 Mybatis 提供的SQL构建器来完成，而对应的代码如下：

<img src="D:/download/downloadFromMicsoft/day05-Mybatis/ppt/assets/image-20210805234842497.png" alt="image-20210805234842497" style="zoom:70%;" />

上述代码将java代码和SQL语句融到了一块，使得代码的可读性大幅度降低。

# HTML&CSS

**今日目标：**

> * 能够掌握课程中讲解的标签的使用
> * 了解css的使用

## 1，HTML

### 1.1  介绍

HTML 是一门语言，所有的网页都是用HTML 这门语言编写出来的，也就是HTML是用来写网页的，像京东，12306等网站有很多网页。

![image-20210811151737929](D:/download/downloadFromMicsoft/day06-HTML&CSS/01-HTML/ppt/assets/image-20210811151737929.png)

<img src="D:/download/downloadFromMicsoft/day06-HTML&CSS/01-HTML/ppt/assets/image-20210811151658928.png" alt="image-20210811151658928" style="zoom:80%;" />

这些都是网页展示出来的效果。而HTML也有专业的解释

==HTML(HyperText Markup Language)：超文本标记语言：==

* 超文本：超越了文本的限制，比普通文本更强大。除了文字信息，还可以定义图片、音频、视频等内容

  如上图看到的页面，除了能看到一些文字，同时也有大量的图片展示；有些网页也有视频，音频等。这种展示效果超越了文本展示的限制。

* 标记语言：由标签构成的语言

  之前学习的XML就是标记语言，由一个一个的标签组成，HTML 也是由标签组成 。在浏览器页面右键可以查看页面的源代码，如下

  ![image-20210811152519471](D:/download/downloadFromMicsoft/day06-HTML&CSS/01-HTML/ppt/assets/image-20210811152519471.png)

  可以看到如下内容，就是由一个一个的标签组成的

  <img src="D:/download/downloadFromMicsoft/day06-HTML&CSS/01-HTML/ppt/assets/image-20210811152558939.png" alt="image-20210811152558939" style="zoom:80%;" />

这些标签不像XML那样可以自定义，==HTML中的标签都是预定义好的，运行在浏览器上并由浏览器解析，==然后展示出对应的效果。例如想在浏览器上展示出图片就需要使用预定义的 `img` 标签；想展示可以点击的链接的效果就可以使用预定义的 `a` 标签等。

HTML 预定义了很多标签，由于是Java工程师、是做后端开发，所以不会每个都学习，页面开发是有专门的前端工程来开发。那为什么还要学习呢？在公司中或多或少大家也会涉及到前端开发。

简单的给大家聊一下开发流程：

以后是通过Java程序从数据库中查询出来数据，然后交给页面进行展示，这样用户就能通过在浏览器通过页面看到数据。

==W3C标准：==

W3C是万维网联盟，这个组成是用来定义标准的。他们规定了一个网页是由三部分组成，分别是：

* 结构：对应的是 HTML 语言
* 表现：对应的是 CSS 语言
* 行为：对应的是 JavaScript 语言

HTML定义页面的整体结构；CSS是用来美化页面，让页面看起来更加美观；JavaScript可以使网页动起来，比如轮播图也就是多张图片自动的进行切换等效果。

为了更好的给大家表述这三种语言的作用。通过具体的页面给大家说明。

如下只是使用HTML语言编写的页面的结构：

![image-20210811155026210](D:/download/downloadFromMicsoft/day06-HTML&CSS/01-HTML/ppt/assets/image-20210811155026210.png)

可以看到页面是比较丑的，但是每一部分其实都已经包含了。接下来咱们加上 CSS 进行美化看到的效果如下：

![image-20210811155211181](D:/download/downloadFromMicsoft/day06-HTML&CSS/01-HTML/ppt/assets/image-20210811155211181.png)

瞬间感觉好看多了，这就是CSS的作用，用来美化页面的。接下来再加上JavaScript试试

![image-20210811155404506](D:/download/downloadFromMicsoft/day06-HTML&CSS/01-HTML/ppt/assets/image-20210811155404506.png)

在上图中可以看到多了轮播图，在浏览器上它是会自动切换图片的，并且切换的动态效果是很不错的。

看到了前端编写的这三个技术效果后，今天学习的是HTML，学习HTML其实就是学习预定义的这些标签。

### 1.2  快速入门

需求：编写如下图效果的页面

<img src="D:/download/downloadFromMicsoft/day06-HTML&CSS/01-HTML/ppt/assets/image-20210811160100054.png" alt="image-20210811160100054" style="zoom:80%;" />

要实现这个页面，需要从以下三步进行实现

* 新建文本文件，后缀名改为 .html

  页面文件的后缀名是 .html，所以需要该后缀名

* 编写 HTML 结构标签

  HTML 是由一个一个的标签组成的，但是它也用于表示结构的标签

  ```html
  <html>
  	<head>
      	<title> </title>
      </head>
      <body>
          
      </body>
  </html>
  ```

  html标签是根标签，下面有 `head` 标签和 `body` 标签这两个子标签。而 `head` 标签的 `title` 子标签是用来定义页面标题名称的，它定义的内容会展示在浏览器的标题位置，如下图红框标记

  <img src="D:/download/downloadFromMicsoft/day06-HTML&CSS/01-HTML/ppt/assets/image-20210811160719292.png" alt="image-20210811160719292" style="zoom:80%;" />

  `body` 标签的内容会被展示在内容区中，如下图红框标记

  <img src="D:/download/downloadFromMicsoft/day06-HTML&CSS/01-HTML/ppt/assets/image-20210811160839423.png" alt="image-20210811160839423" style="zoom:80%;" />

  

* 在<body>中定义文字

代码如下：

```html
<html>
	<head>
    	<title>html 快速入门</title>
    </head>
    <body>
        乾坤未定，你我皆是黑马~
    </body>
</html>
```

同学们在访问其他网站页面时会看到字体颜色是五颜六色的，可以该字体颜色吗？当然可以了

`font` 标签就可以使用，该标签有一个 `color` 属性可以设置字体颜色，如： <font color='red'></font> 就是将文字设置成了红颜色。那么只需要将需要变成红色的文字放在标签体部分就可以了，如下：

```html
<html>
	<head>
    	<title>html 快速入门</title>
    </head>
    <body>
        <font color='red'>乾坤未定，你我皆是黑马~</font>
    </body>
</html>
```

==总结：==

* HTML 文件以.htm或.html为扩展名

* HTML 结构标签

  <img src="D:/download/downloadFromMicsoft/day06-HTML&CSS/01-HTML/ppt/assets/image-20210811161810610.png" alt="image-20210811161810610" style="zoom:70%;" />

* HTML 标签不区分大小写

  如上案例中的 `font` 写成 `Font` 也是一样可以展示出对应的效果的。

* HTML 标签属性值 单双引皆可

  如上案例中的color属性值使用双引号也是可以的。<font color="red"></font> 

* HTML 语法松散

  比如 font 标签不加结束标签也是可以展示出效果的。但是建议同学们在写的时候还是不要这样做，严格按照要求去写。



### 1.3  基础标签

基础标签就是一些和文字相关的标签，如下：

<img src="D:/download/downloadFromMicsoft/day06-HTML&CSS/01-HTML/ppt/assets/image-20210811171740881.png" alt="image-20210811171740881" style="zoom:80%;" />

接下来挨个进行讲解

#### 1.3.1  标题标签

* 创建模块

  在 Idea 中创建模块，而现在不需要写java代码，所以 `src` 目录就可以删除掉。在模块下创建一个html文件夹，该今天的所以的页面文件所部放在该文件夹下。模块目录如下

  ![image-20210811172254664](D:/download/downloadFromMicsoft/day06-HTML&CSS/01-HTML/ppt/assets/image-20210811172254664.png)

* 创建页面文件

  选中 `html` 文件夹右键创建页面文件（01-基础标签.html）

  <img src="D:/download/downloadFromMicsoft/day06-HTML&CSS/01-HTML/ppt/assets/image-20210811172511287.png" alt="image-20210811172511287" style="zoom:80%;" />

  创建好后 idea 会自动加上结构标签，如下

  <img src="D:/download/downloadFromMicsoft/day06-HTML&CSS/01-HTML/ppt/assets/image-20210811172704525.png" alt="image-20210811172704525" style="zoom:80%;" />

  只需要在 `body` 标签中书写标签。

* 书写标题标签

  标题标签中 h1最大，h6最小。

  ```html
  <h1>我是标题 h1</h1>
  <h2>我是标题 h2</h2>
  <h3>我是标题 h3</h3>
  <h4>我是标题 h4</h4>
  <h5>我是标题 h5</h5>
  <h6>我是标题 h6</h6>
  ```

* 通过浏览器查看效果

  idea 提供了快捷的打开方式，如下图

  <img src="D:/download/downloadFromMicsoft/day06-HTML&CSS/01-HTML/ppt/assets/image-20210811172942861.png" alt="image-20210811172942861" style="zoom:80%;" />

  浏览器展示效果如下：

  <img src="D:/download/downloadFromMicsoft/day06-HTML&CSS/01-HTML/ppt/assets/image-20210811173034453.png" alt="image-20210811173034453" style="zoom:80%;" />

#### 1.3.2  hr标签

`hr` 标签在浏览器中呈现出 横线 的效果。

在页面文件中书写 hr 标签

```
<hr>
```

效果如下：

![image-20210811173605496](D:/download/downloadFromMicsoft/day06-HTML&CSS/01-HTML/ppt/assets/image-20210811173605496.png)



#### 1.3.3  字体标签

font：字体标签

* face 属性：用来设置字体。如 "楷体"、"宋体"等

* color 属性：设置文字颜色。颜色有三种表示方式

  * **英文单词**：red,pink,blue...

    这种方式表示的颜色特别有限，所以一般不用。

  * **rgb(值1,值2,值3)**：值的取值范围：0~255  

    此种方式也就是三原色（红绿蓝）设置方式。 例如： rgb(255,0,0)。

    这种书写起来比较麻烦，一般不用。

  * **#值1值2值3**：值的范围：00~FF

    这种方式是rgb方式的简化写法，以后基本都用此方式。

    值1表示红色的范围，值2表示绿色的范围，值3表示蓝色范围。例如： #ff0000

* size 属性：设置文字大小

代码演示：

```html
<font face="楷体" size="5" color="#ff0000">传智教育</font>
```

效果如下：

<img src="D:/download/downloadFromMicsoft/day06-HTML&CSS/01-HTML/ppt/assets/image-20210811175246763.png" alt="image-20210811175246763" style="zoom:80%;" /> 

> ==注意：==
>
> font 标签已经不建议使用了，以后如果要改变文字字体，大小，颜色可以使用 CSS 进行设置。

#### 1.3.4  换行标签

在页面文件中书写如下内容

```
刚察草原绿草如茵，沙柳河水流淌入湖。藏族牧民索南才让家中，茶几上摆着馓子、麻花和水果，炉子上刚煮开的奶茶香气四溢……

6月8日下午，习近平总书记来到青海省海北藏族自治州刚察县沙柳河镇果洛藏贡麻村，走进牧民索南才让家中，看望慰问藏族群众。
```

 在浏览器展示的效果如下：

![image-20210811175442896](D:/download/downloadFromMicsoft/day06-HTML&CSS/01-HTML/ppt/assets/image-20210811175442896.png)

可以看到并没有换行。如果要实现换行效果，需要使用 换行标签（br标签）。

修改页面文件内容如下：

```
刚察草原绿草如茵，沙柳河水流淌入湖。藏族牧民索南才让家中，茶几上摆着馓子、麻花和水果，炉子上刚煮开的奶茶香气四溢……<br>

6月8日下午，习近平总书记来到青海省海北藏族自治州刚察县沙柳河镇果洛藏贡麻村，走进牧民索南才让家中，看望慰问藏族群众。
```

浏览器打开效果如下：

<img src="D:/download/downloadFromMicsoft/day06-HTML&CSS/01-HTML/ppt/assets/image-20210811175649409.png" alt="image-20210811175649409" style="zoom:80%;" />

现在就有换行效果了。

#### 1.3.5  段落标签

上面文字展示的效果还是不太好，想让每一段上下都加空行。此时就需要使用段落标签（p标签）

在页面文件中书写如下内容：

```html
<p>
刚察草原绿草如茵，沙柳河水流淌入湖。藏族牧民索南才让家中，茶几上摆着馓子、麻花和水果，炉子上刚煮开的奶茶香气四溢……
</p>
<p>
6月8日下午，习近平总书记来到青海省海北藏族自治州刚察县沙柳河镇果洛藏贡麻村，走进牧民索南才让家中，看望慰问藏族群众。
</p>
```

在浏览器展示的效果如下：

<img src="D:/download/downloadFromMicsoft/day06-HTML&CSS/01-HTML/ppt/assets/image-20210811180041023.png" alt="image-20210811180041023" style="zoom:80%;" />

这种效果就会比之前的效果好一些，呈现出段落的效果。

#### 1.3.6  加粗、斜体、下划线标签

* b：加粗标签
* i：斜体标签
* u：下划线标签，在文字的下方有一条横线

代码如下：

```html
<b>沙柳河水流淌</b><br>
<i>沙柳河水流淌</i><br>
<u>沙柳河水流淌</u><br>
```

在浏览器展示的效果如下：

<img src="D:/download/downloadFromMicsoft/day06-HTML&CSS/01-HTML/ppt/assets/image-20210811180336928.png" alt="image-20210811180336928" style="zoom:80%;" />

#### 1.3.7  居中标签

center ：文本居中

代码如下：

```html
<hr>
<center>
    <b>沙柳河水流淌</b>
</center>
```

在浏览器效果如下：

![image-20210811180702247](D:/download/downloadFromMicsoft/day06-HTML&CSS/01-HTML/ppt/assets/image-20210811180702247.png)

#### 1.3.8  案例

实现如下图所示页面效果：

![image-20210811180755814](D:/download/downloadFromMicsoft/day06-HTML&CSS/01-HTML/ppt/assets/image-20210811180755814.png)

此案例同学们自己实现，用学过的基础标签。

> 注意：在上图页面中版权所有里有特殊字符，需要使用转义字符。有如下转义字符：
>
> <img src="D:/download/downloadFromMicsoft/day06-HTML&CSS/01-HTML/ppt/assets/image-20210811180929858.png" alt="image-20210811180929858" style="zoom:70%;" /> 

### 1.4  图片、音频、视频标签

<img src="D:/download/downloadFromMicsoft/day06-HTML&CSS/01-HTML/ppt/assets/image-20210811181303117.png" alt="image-20210811181303117" style="zoom:70%;" />

* img：定义图片

  * src：规定显示图像的 URL（统一资源定位符）

  * height：定义图像的高度

  * width：定义图像的宽度

* audio：定义音频。支持的音频格式：MP3、WAV、OGG 

  * src：规定音频的 URL

  * controls：显示播放控件

* video：定义视频。支持的音频格式：MP4, WebM、OGG
  * src：规定视频的 URL
  * controls：显示播放控件

**尺寸单位：**

height属性和width属性有两种设置方式：

* 像素：单位是px
* 百分比。占父标签的百分比。例如宽度设置为 50%，意思就是占它的父标签宽度的一般（50%）

**资源路径：**

图片，音频，视频标签都有src属性，而src是用来指定对应的图片，音频，视频文件的路径。此处的图片，音频，视频就称为资源。资源路径有如下两种设置方式：

* 绝对路径：完整路径

  这里的绝对路径是网络中的绝对路径。 格式为： 协议://ip地址:端口号/资源名称。

  如：

  ```
  <img src="https://th.bing.com/th/id/R33674725d9ae34f86e3835ae30b20afe?rik=Pb3C9e5%2b%2b3a9Vw&riu=http%3a%2f%2fwww.desktx.com%2fd%2ffile%2fwallpaper%2fscenery%2f20180626%2f4c8157d07c14a30fd76f9bc110b1314e.jpg&ehk=9tpmnrrRNi0eBGq3CnhwvuU8PPmKuy1Yma0zL%2ba14T0%3d&risl=&pid=ImgRaw" width="300" height="400">
  ```

  这里src属性的值就是网络中的绝对路径。

* 相对路径：相对位置关系

  找页面和其他资源的相对路径。

  > ./    表示当前路径
  >
  > ../   表示上一级路径
  >
  > ../../   表示上两级路径

  如模块目录结构如下：

  <img src="D:/download/downloadFromMicsoft/day06-HTML&CSS/01-HTML/ppt/assets/image-20210811190840184.png" alt="image-20210811190840184" style="zoom:80%;" />

  在 `01-基础标签.html` 里的标签中找不同的图片，路径写法不同

  ```html
  <!--在该页面找a.jpg，就需要先回到上一级目录，该级目录有img目录，进入该目录就可以找到 a.jpg图片-->
  <img src="../img/a.jpg" width="300" height="400">
  <!--该页面和aa.jpg 是在同一级下，所以可以直接写 图片的名称，也可以写成  ./aa.jpg-->
  <img src="aa.jpg" width="300" height="400">
  ```

使用这些标签的代码如下：

```html
<img src="../img/a.jpg" width="300" height="400">
<audio src="b.mp3" controls></audio>
<video src="c.mp4" controls width="500" height="300"></video>
```

在浏览器展示的效果如下：

![image-20210811191514642](D:/download/downloadFromMicsoft/day06-HTML&CSS/01-HTML/ppt/assets/image-20210811191514642.png)

### 1.5  超链接标签

在网页中可以看到很多超链接标签，如下

<img src="D:/download/downloadFromMicsoft/day06-HTML&CSS/01-HTML/ppt/assets/image-20210811191725308.png" alt="image-20210811191725308" style="zoom:80%;" />

上图红框中的都是超链接，当点击这些超链接时会跳转到其他的页面或者资源。而超链接使用的是 `a` 标签。

<img src="D:/download/downloadFromMicsoft/day06-HTML&CSS/01-HTML/ppt/assets/image-20210811191852726.png" alt="image-20210811191852726" style="zoom:70%;" />

`a` 标签属性：

* href：指定访问资源的URL 

* target：指定打开资源的方式
  * _self：默认值，在当前页面打开
  * _blank：在空白页面打开

**代码演示：**

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

效果图示：

<img src="D:/download/downloadFromMicsoft/day06-HTML&CSS/01-HTML/ppt/assets/image-20210811192332854.png" alt="image-20210811192332854" style="zoom:70%;" />

当将 `target` 属性值设置为 `_blank`，效果图示：

<img src="D:/download/downloadFromMicsoft/day06-HTML&CSS/01-HTML/ppt/assets/image-20210811192512960.png" alt="image-20210811192512960" style="zoom:70%;" />

### 1.6  列表标签

HTML 中列表分为

* 有序列表

  如下图，页面效果中是有标号对每一项进行标记的。

  <img src="D:/download/downloadFromMicsoft/day06-HTML&CSS/01-HTML/ppt/assets/image-20210811192825145.png" alt="image-20210811192825145" style="zoom:80%;" />

* 无序列表

  如下图，页面效果中没有标号对每一项进行标记，而是使用 点 进行标记。

  <img src="D:/download/downloadFromMicsoft/day06-HTML&CSS/01-HTML/ppt/assets/image-20210811192905834.png" alt="image-20210811192905834" style="zoom:80%;" />

**标签说明：**

<img src="D:/download/downloadFromMicsoft/day06-HTML&CSS/01-HTML/ppt/assets/image-20210811193105881.png" alt="image-20210811193105881" style="zoom:60%;" />

有序列表中的 `type` 属性用来指定标记的标号的类型（数字、字母、罗马数字等）

无序列表中的 `type` 属性用来指定标记的形状

**代码演示：**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <ol type="A">
        <li>咖啡</li>
        <li>茶</li>
        <li>牛奶</li>
    </ol>
    
    <ul type="circle">
        <li>咖啡</li>
        <li>茶</li>
        <li>牛奶</li>
    </ul>
</body>
</html>
```

### 1.7  表格标签

<img src="D:/download/downloadFromMicsoft/day06-HTML&CSS/01-HTML/ppt/assets/image-20210811193819851.png" alt="image-20210811193819851" style="zoom:80%;" />

如上图就是一个表格，表格可以使用如下标签定义

* table ：定义表格

  * border：规定表格边框的宽度

  * width ：规定表格的宽度

  * cellspacing：规定单元格之间的空白

* tr ：定义行

  * align：定义表格行的内容对齐方式

* td ：定义单元格

  * rowspan:规定单元格可横跨的行数

  * colspan:规定单元格可横跨的列数

* th：定义表头单元格

**代码演示：**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>

<table border="1" cellspacing="0" width="500">
    <tr>
        <th>序号</th>
        <th>品牌logo</th>
        <th>品牌名称</th>
        <th>企业名称</th>
    </tr>
    <tr align="center">
        <td>010</td>
        <td><img src="../img/三只松鼠.png" width="60" height="50"></td>
        <td>三只松鼠</td>
        <td>三只松鼠</td>
    </tr>

    <tr align="center">
        <td>009</td>
        <td><img src="../img/优衣库.png" width="60" height="50"></td>
        <td>优衣库</td>
        <td>优衣库</td>
    </tr>

    <tr align="center">
        <td>008</td>
        <td><img src="../img/小米.png" width="60" height="50"></td>
        <td>小米</td>
        <td>小米科技有限公司</td>
    </tr>
</table>
</body>
</html>
```

### 1.8  布局标签

<img src="D:/download/downloadFromMicsoft/day06-HTML&CSS/01-HTML/ppt/assets/image-20210811194410699.png" alt="image-20210811194410699" style="zoom:80%;" />

这两个标签，一般都是和css结合到一块使用来实现页面的布局。

`div`标签 在浏览器上会有换行的效果，而 `span` 标签在浏览器上没有换行效果。

**代码演示：**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <div>我是div</div>
    <div>我是div</div>
    <span>我是span</span>
    <span>我是span</span>
</body>
</html>
```

**浏览器效果如下：**

![image-20210811194739313](D:/download/downloadFromMicsoft/day06-HTML&CSS/01-HTML/ppt/assets/image-20210811194739313.png)

### 1.9  表单标签

表单标签效果大家其实都不陌生，像登陆页面、注册页面等都是表单。

<img src="D:/download/downloadFromMicsoft/day06-HTML&CSS/01-HTML/ppt/assets/image-20210812215311168.png" alt="image-20210812215311168" style="zoom:80%;" />

像这样的表单就是用来采集用户输入的数据，然后将数据发送到服务端，服务端会对数据库进行操作，比如注册就是将数据保存到数据库中，而登陆就是根据用户名和密码进行数据库的查询操作。

表单是很重要的标签，需要大家重点来学习。

#### 1.9.1  表单标签概述

> 表单：在网页中主要负责数据采集功能，使用<form>标签定义表单
>
> 表单项(元素)：不同类型的 input 元素、下拉列表、文本域等

<img src="D:/download/downloadFromMicsoft/day06-HTML&CSS/01-HTML/ppt/assets/image-20210812215704511.png" alt="image-20210812215704511" style="zoom:80%;" />

`form` 是表单标签，它在页面上没有任何展示的效果。需要借助于表单项标签来展示不同的效果。如下图就是不同的表单项标签展示出来的效果。

<img src="D:/download/downloadFromMicsoft/day06-HTML&CSS/01-HTML/ppt/assets/image-20210812215857298.png" alt="image-20210812215857298" style="zoom:70%;" />

#### 1.9.2  form标签属性

* **action：规定当提交表单时向何处发送表单数据，该属性值就是URL**

  以后会将数据提交到服务端，该属性需要书写服务端的URL。而今天可以书写 `#` ，表示提交到当前页面来看效果。

* **method ：规定用于发送表单数据的方式**

  method取值有如下两种：

  * get：默认值。如果不设置method属性则默认就是该值
    * 请求参数会拼接在URL后边
    * url的长度有限制 4KB
  * post：
    * 浏览器会将数据放到http请求消息体中
    * 请求参数无限制的

#### 1.9.3  代码演示

由于表单标签在页面上没有任何展示的效果，所以在演示的过程是会先使用 `input` 这个表单项标签展示输入框效果。

代码如下：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <form>
        <input type="text">
        <input type="submit">
    </form>
</body>
</html>
```

浏览器展示效果如下：

<img src="D:/download/downloadFromMicsoft/day06-HTML&CSS/01-HTML/ppt/assets/image-20210812220926114.png" alt="image-20210812220926114" style="zoom:90%;" /> 

从效果可以看到页面有一个输入框，用户可以在数据框中输入自己想输入的内容，点击提交按钮以后会将数据发送到服务端，当然现在肯定不能实现。现在可以将 `form` 标签的 `action` 属性值设置为 `#` ，将其将数据提交到当前页面。还需要注意一点，要想提交数据，`input` 输入框必须设置 `name` 属性。代码如下：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <form action="#">
        <input type="text" name="username">
        <input type="submit">
    </form>
</body>
</html>
```

浏览器展示效果如下：

<img src="D:/download/downloadFromMicsoft/day06-HTML&CSS/01-HTML/ppt/assets/image-20210812221656295.png" alt="image-20210812221656295" style="zoom:80%;" /> 

在输入框输入 `hehe` ，然后点击 `提交` 按钮，就能看到如下效果

<img src="D:/download/downloadFromMicsoft/day06-HTML&CSS/01-HTML/ppt/assets/image-20210812221801965.png" alt="image-20210812221801965" style="zoom:80%;" /> 

可以看到在浏览器的地址栏的URL后拼接了提交的数据。`username` 就是输入框 `name` 属性值，而 `hehe` 就是在输入框输入的内容。

接下来来聊 `method` 属性，默认是 `method = 'get'`，所以该取值就会将数据拼接到URL的后面。那将 `method` 属性值设置为 `post`，浏览器的效果如下：

<img src="D:/download/downloadFromMicsoft/day06-HTML&CSS/01-HTML/ppt/assets/image-20210812222334790.png" alt="image-20210812222334790" style="zoom:80%;" /> 

从上图可以看出数据并没有拼接到 URL 后，那怎么看提交的数据呢？可以使用浏览器的开发者工具来查看

![image-20210812222623912](D:/download/downloadFromMicsoft/day06-HTML&CSS/01-HTML/ppt/assets/image-20210812222623912.png)

按照如上步骤操作能看到如下页面

![image-20210812223004607](D:/download/downloadFromMicsoft/day06-HTML&CSS/01-HTML/ppt/assets/image-20210812223004607.png)

重新提交数据后，可以看到提交的数据，如下图

<img src="D:/download/downloadFromMicsoft/day06-HTML&CSS/01-HTML/ppt/assets/image-20210812223150373.png" alt="image-20210812223150373" style="zoom:80%;" />

### 1.10  表单项标签

表单项标签有很多，不同的表单项标签有不同的展示效果。表单项标签可以分为以下三个：

* \<input>：表单项，通过type属性控制输入形式

  `input` 标签有个 `type` 属性。 `type` 属性的取值不同，展示的效果也不一样

  <img src="D:/download/downloadFromMicsoft/day06-HTML&CSS/01-HTML/ppt/assets/image-20210812223956360.png" alt="image-20210812223956360" style="zoom:80%;" />

  

* \<select>：定义下拉列表，\<option> 定义列表项 

  如下图就是下拉列表的效果：

  <img src="D:/download/downloadFromMicsoft/day06-HTML&CSS/01-HTML/ppt/assets/image-20210812223708205.png" alt="image-20210812223708205" style="zoom:80%;" /> 

* \<textarea>：文本域

  如下图就是文本域效果。它可以输入多行文本，而 `input` 数据框只能输入一行文本。

  ![image-20210812223744522](D:/download/downloadFromMicsoft/day06-HTML&CSS/01-HTML/ppt/assets/image-20210812223744522.png) 

> ==注意：==
>
> * 以上标签项的内容要想提交，必须得定义 `name` 属性。
> * 每一个标签都有id属性，id属性值是唯一的标识。
> * 单选框、复选框、下拉列表需要使用 `value` 属性指定提交的值。

**代码演示：**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <form action="#" method="post">
        <input type="hidden" name="id" value="123">

        <label for="username">用户名：</label>
        <input type="text" name="username" id="username"><br>

        <label for="password">密码：</label>
        <input type="password" name="password" id="password"><br>

        性别：
        <input type="radio" name="gender" value="1" id="male"> <label for="male">男</label>
        <input type="radio" name="gender" value="2" id="female"> <label for="female">女</label>
        <br>

        爱好：
        <input type="checkbox" name="hobby" value="1"> 旅游
        <input type="checkbox" name="hobby" value="2"> 电影
        <input type="checkbox" name="hobby" value="3"> 游戏
        <br>

        头像：
        <input type="file"><br>

        城市:
        <select name="city">
            <option>北京</option>
            <option value="shanghai">上海</option>
            <option>广州</option>
        </select>
        <br>

        个人描述：
        <textarea cols="20" rows="5" name="desc"></textarea>
        <br>
        <br>
        <input type="submit" value="免费注册">
        <input type="reset" value="重置">
        <input type="button" value="一个按钮">
    </form>
</body>
</html>
```

在浏览器的效果如下：

<img src="D:/download/downloadFromMicsoft/day06-HTML&CSS/01-HTML/ppt/assets/image-20210812224152747.png" alt="image-20210812224152747" style="zoom:80%;" />

## 2，CSS

### 2.1  概述

==CSS 是一门语言，用于控制网页表现。==之前介绍过W3C标准。W3C标准规定了网页是由以下组成：

* 结构：HTML
* 表现：CSS
* 行为：JavaScript

CSS也有一个专业的名字：==Cascading Style Sheet（层叠样式表）。==

如下面的代码， `style` 标签中定义的就是css代码。该代码描述了将 div 标签的内容的字体颜色设置为 红色。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        div{
            color: red;
        }
    </style>
</head>
<body>
    <div>Hello CSS~</div>
</body>
</html>
```

在浏览器中的效果如下：

<img src="D:/download/downloadFromMicsoft/day06-HTML&CSS/01-HTML/ppt/assets/image-20210812225424174.png" alt="image-20210812225424174" style="zoom:60%;" />

### 2.2  css 导入方式

css 导入方式其实就是 css 代码和 html 代码的结合方式。CSS 导入 HTML有三种方式：

* 内联样式：在标签内部使用style属性，属性值是css属性键值对

  ```html
  <div style="color: red">Hello CSS~</div>
  ```

  > 给方式只能作用在这一个标签上，如果其他的标签也想使用同样的样式，那就需要在其他标签上写上相同的样式。复用性太差。

* 内部样式：定义<style>标签，在标签内部定义css样式

  ```html
  <style type="text/css">
  	div{
  		color: red;
      }
  </style>
  ```

  > 这种方式可以做到在该页面中复用。

* 外部样式：定义link标签，引入外部的css文件

  编写一个css文件。名为：demo.css，内容如下:

  ```css
  div{
  	color: red;
  }
  ```

  在html中引入 css 文件。

  ```html
  <link rel="stylesheet"  href="demo.css">
  ```

  > 这种方式可以在多个页面进行复用。其他的页面想使用同样的样式，只需要使用 `link` 标签引入该css文件。

**代码演示：**

项目目录结构如下：

<img src="D:/download/downloadFromMicsoft/day06-HTML&CSS/01-HTML/ppt/assets/image-20210812231514311.png" alt="image-20210812231514311" style="zoom:80%;" />

编写页面 `02-导入方式.html`，内容如下：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        span{
            color: red;
        }
    </style>
    <link href="../css/demo.css" rel="stylesheet">
</head>
<body>
    <div style="color: red">hello css</div>

    <span>hello css </span>

    <p>hello css</p>
</body>
</html>
```

### 2.3  css 选择器

css 选择器就是选取需设置样式的元素（标签），比如如下css代码：

```css
div {
	color:red;
}
```

如上代码中的 `div` 就是 css 中的选择器。只讲下面三种选择器：

* 元素选择器

  格式：

  ```css
  元素名称{color: red;}
  ```

  例子：

  ```
  div {color:red}  /*该代码表示将页面中所有的div标签的内容的颜色设置为红色*/
  ```

* id选择器

  格式：

  ```css
  #id属性值{color: red;}
  ```

  例子：

  html代码如下：

  ```html
  <div id="name">hello css2</div>
  ```

  css代码如下：

  ```css
  #name{color: red;}/*该代码表示将页面中所有的id属性值是 name 的标签的内容的颜色设置为红色*/
  ```

* 类选择器

  格式：

  ```css
  .class属性值{color: red;}
  ```

  例子：

  html代码如下：

  ```html
  <div class="cls">hello css3</div>
  ```

  css代码如下：

  ```css
  .cls{color: red;} /*该代码表示将页面中所有的class属性值是 cls 的标签的内容的颜色设置为红色*/
  ```

**代码演示：**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        div{
            color: red;
        }

        #name{
            color: blue;
        }

        .cls{
            color: pink;
        }
    </style>

</head>
<body>
    <div>div1</div>
    <div id="name">div2</div>
    <div class="cls">div3</div>
    <span class="cls">span</span>
</body>
</html>
```



### 2.4  css 属性

css属性不作为重点讲解。简单的看一下css的文档

![image-20210812233107495](D:/download/downloadFromMicsoft/day06-HTML&CSS/01-HTML/ppt/assets/image-20210812233107495.png)

css有很多css属性，你要想把它们都学会，需要花费很长的时间。而作为java程序员，不需要重点掌握这部分内容。对于网页三剑客中css是对要求最低的。给大家简单介绍一下文档怎么查看即可，如下看一个 `background-color` 属性

<img src="D:/download/downloadFromMicsoft/day06-HTML&CSS/01-HTML/ppt/assets/image-20210812233415060.png" alt="image-20210812233415060" style="zoom:80%;" />

点击进去后能看到下面界面

<img src="D:/download/downloadFromMicsoft/day06-HTML&CSS/01-HTML/ppt/assets/image-20210812233510734.png" alt="image-20210812233510734" style="zoom:70%;" />

上面就列举了该属性的具体的使用，你也可以点击下面的 `亲自试一试` 看效果。



# JavaScript

**今日目标**

> * 掌握 JavaScript 的基础语法
> * 掌握 JavaScript 的常用对象（Array、String）
> * 能根据需求灵活运用定时器及通过 js 代码进行页面跳转
> * 能通过DOM 对象对标签进行常规操作
> * 掌握常用的事件
> * 能独立完成表单校验案例

## 1，JavaScript简介

==JavaScript 是一门跨平台、面向对象的脚本语言==，而Java语言也是跨平台的、面向对象的语言，只不过Java是编译语言，是需要编译成字节码文件才能运行的；JavaScript是脚本语言，不需要编译，由浏览器直接解析并执行。

JavaScript 是用来控制网页行为的，它能使网页可交互；那么它可以做什么呢？如改变页面内容、修改指定元素的属性值、对表单进行校验等，下面是这些功能的效果展示：

* **改变页面内容**

  <img src="D:/download/downloadFromMicsoft/day07-JavaScript/ppt/assets/image-20210814173417834.png" alt="image-20210814173417834" style="zoom:80%;" />

  当我点击上面左图的 `点击我` 按钮，按钮上面的文本就改为上面右图内容，这就是js 改变页面内容的功能。

* **修改指定元素的属性值**

  <img src="D:/download/downloadFromMicsoft/day07-JavaScript/ppt/assets/image-20210814173719505.png" alt="image-20210814173719505" style="zoom:70%;" />

  当点击上图的 `开灯` 按钮，效果就是上面右图效果；当我点击 `关灯` 按钮，效果就是上面左图效果。其他这个功能中有两张灯泡的图片（使用img标签进行展示），通过修改 img 标签的 src 属性值改变展示的图片来实现。

* **对表单进行校验**

  <img src="D:/download/downloadFromMicsoft/day07-JavaScript/ppt/assets/image-20210814174242688.png" alt="image-20210814174242688" style="zoom:70%;" />

  在上面左图的输入框输入用户名，如果输入的用户名是不满足规则的就展示右图(上) 的效果；如果输入的用户名是满足规则的就展示右图(下) 的效果。

JavaScript 和 Java 是完全不同的语言，不论是概念还是设计，只是名字比较像而已。但是==基础语法类似==，所以有java的学习经验，再学习JavaScript 语言就相对比较容易些。

JavaScript（简称：JS） 在 1995 年由 Brendan Eich 发明，并于 1997 年成为一部 ECMA 标准。ECMA 规定了一套标准 就叫 `ECMAScript` ，所有的客户端校验语言必须遵守这个标准，当然 JavaScript 也遵守了这个标准。ECMAScript 6 (简称ES6) 是最新的 JavaScript 版本（发布于 2015 年)，的课程就是基于最新的 `ES6` 进行讲解。

## 2，JavaScript引入方式

JavaScript 引入方式就是 HTML 和 JavaScript 的结合方式。JavaScript引入方式有两种：

* 内部脚本：将 JS代码定义在HTML页面中
* 外部脚本：将 JS代码定义在外部 JS文件中，然后引入到 HTML页面中

### 2.1  内部脚本

在 HTML 中，JavaScript 代码必须位于 `<script>` 与 `</script>` 标签之间

**代码如下：**

`alert(数据)` 是 JavaScript 的一个方法，作用是将参数数据以浏览器弹框的形式输出出来。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>

<script>
    alert("hello js1");
</script>
</body>
</html>
```

**效果如下：**

<img src="D:/download/downloadFromMicsoft/day07-JavaScript/ppt/assets/image-20210814181419691.png" alt="image-20210814181419691" style="zoom:70%;" />

从结果可以看到 js 代码已经执行了。

> ==提示：==
>
> * 在 HTML 文档中可以在任意地方，放置任意数量的<script>标签。如下图
>
>   ```html
>   <!DOCTYPE html>
>   <html lang="en">
>   <head>
>       <meta charset="UTF-8">
>       <title>Title</title>
>       <script>
>           alert("hello js1");
>       </script>
>   </head>
>   <body>
>   
>   <script>
>       alert("hello js1");
>   </script>
>   
>   </body>
>   </html>
>   <script>
>       alert("hello js1");
>   </script>
>   ```
>
> * 一般把脚本置于 <body> 元素的底部，可改善显示速度
>
>   因为浏览器在加载页面的时候会从上往下进行加载并解析。 应该让用户看到页面内容，然后再展示动态的效果。

### 2.2  外部脚本

**第一步：定义外部 js 文件。如定义名为 demo.js的文件**

项目结构如下：

<img src="D:/download/downloadFromMicsoft/day07-JavaScript/ppt/assets/image-20210814182345236.png" alt="image-20210814182345236" style="zoom:80%;" />

demo.js 文件内容如下：

```js
alert("hello js");
```

**第二步：在页面中引入外部的js文件**

在页面使用 `script` 标签中使用 `src` 属性指定 js 文件的 URL 路径。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>

<script src="../js/demo.js"></script>
</body>
</html>
```

> ==注意：==
>
> * 外部脚本不能包含 `<script>` 标签
>
>   在js文件中直接写 js 代码即可，不要在 js文件 中写 `script` 标签
>
> * `<script>` 标签不能自闭合
>
>   在页面中引入外部js文件时，不能写成 `<script src="../js/demo.js" />`。

## 3，JavaScript基础语法

### 3.1  书写语法

* 区分大小写：与 Java 一样，变量名、函数名以及其他一切东西都是区分大小写的

* 每行结尾的分号可有可无

  如果一行上写多个语句时，必须加分号用来区分多个语句。

* 注释

  * 单行注释：// 注释内容
  * 多行注释：/* 注释内容 */

  > 注意：JavaScript 没有文档注释

* 大括号表示代码块

  下面语句大家肯定能看懂，和 java 一样 大括号表示代码块。

  ```js
  if (count == 3) { 
     alert(count); 
  } 
  ```

### 3.2  输出语句

js 可以通过以下方式进行内容的输出，只不过不同的语句输出到的位置不同

* **使用 window.alert() 写入警告框**

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>Title</title>
  </head>
  <body>
      
  <script>
      window.alert("hello js");//写入警告框
  </script>
  </body>
  </html>
  ```

  上面代码通过浏览器打开，可以看到如下图弹框效果

  <img src="D:/download/downloadFromMicsoft/day07-JavaScript/ppt/assets/image-20210814181419691.png" alt="image-20210814181419691" style="zoom:70%;" />

* **使用 document.write() 写入 HTML 输出**

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>Title</title>
  </head>
  <body>
      
  <script>
      document.write("hello js 2~");//写入html页面
  </script>
  </body>
  </html>
  ```

  上面代码通过浏览器打开，可以在页面上看到 `document.write(内容)` 输出的内容

  <img src="D:/download/downloadFromMicsoft/day07-JavaScript/ppt/assets/image-20210814190302845.png" alt="image-20210814190302845" style="zoom:80%;" />

* **使用 console.log() 写入浏览器控制台**

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>Title</title>
  </head>
  <body>
  
  <script>
      console.log("hello js 3");//写入浏览器的控制台
  </script>
  </body>
  </html>
  ```

  上面代码通过浏览器打开，可以在不能页面上看到  `console.log(内容)` 输出的内容，它是输出在控制台了，而怎么在控制台查看输出的内容呢？在浏览器界面按 `F12` 就可以看到下图的控制台

  ![image-20210814190906202](D:/download/downloadFromMicsoft/day07-JavaScript/ppt/assets/image-20210814190906202.png)

### 3.3  变量

JavaScript 中用 var 关键字（variable 的缩写）来声明变量。格式 `var 变量名 = 数据值;`。而在JavaScript 是一门弱类型语言，变量==可以存放不同类型的值==；如下在定义变量时赋值为数字数据，还可以将变量的值改为字符串类型的数

```js
var test = 20;
test = "张三";
```

js 中的变量名命名也有如下规则，和java语言基本都相同

* 组成字符可以是任何字母、数字、下划线（_）或美元符号（$）
* 数字不能开头
* 建议使用驼峰命名

JavaScript 中 `var` 关键字有点特殊，有以下地方和其他语言不一样

* 作用域：全局变量

  ```js
  {
      var age = 20;
  }
  alert(age);  // 在代码块中定义的age 变量，在代码块外边还可以使用
  ```

* 变量可以重复定义

  ```js
  {
      var age = 20;
      var age = 30;//JavaScript 会用 30 将之前 age 变量的 20 替换掉
  }
  alert(age); //打印的结果是 30
  ```

针对如上的问题，==ECMAScript 6 新增了 `let `关键字来定义变量。==它的用法类似于 `var`，但是所声明的变量，只在 `let` 关键字所在的代码块内有效，且不允许重复声明。

例如：

```js
{
    let age = 20;
}
alert(age); 
```

运行上面代码，浏览器并没有弹框输出结果，说明这段代码是有问题的。通过 `F12` 打开开发者模式可以看到如下错误信息

<img src="D:/download/downloadFromMicsoft/day07-JavaScript/ppt/assets/image-20210815170848426.png" alt="image-20210815170848426" style="zoom:80%;" />

而如果在代码块中定义两个同名的变量，IDEA 开发工具就直接报错了

> <img src="D:/download/downloadFromMicsoft/day07-JavaScript/ppt/assets/image-20210815170952829.png" alt="image-20210815170952829" style="zoom:80%;" />

==ECMAScript 6 新增了 const关键字，用来声明一个只读的常量。一旦声明，常量的值就不能改变。== 通过下面的代码看一下常用的特点就可以了

> <img src="D:/download/downloadFromMicsoft/day07-JavaScript/ppt/assets/image-20210815171128095.png" alt="image-20210815171128095" style="zoom:80%;" />

可以看到给 PI 这个常量重新赋值时报错了。

### 3.4  数据类型

JavaScript 中提供了两类数据类型：原始类型 和 引用类型。

> 使用 typeof 运算符可以获取数据类型
>
> `alert(typeof age);` 以弹框的形式将 age 变量的数据类型输出

原始数据类型：

* **number**：数字（整数、小数、NaN(Not a Number)）

  ```js
  var age = 20;
  var price = 99.8;
  
  alert(typeof age); // 结果是 ： number
  alert(typeof price);// 结果是 ： number
  ```

  > ==注意：== NaN是一个特殊的number类型的值，后面用到再说

* **string**：字符、字符串，单双引皆可

  ```js
  var ch = 'a';
  var name = '张三'; 
  var addr = "北京";
  
  alert(typeof ch); //结果是  string
  alert(typeof name); //结果是  string
  alert(typeof addr); //结果是  string
  ```

  > ==注意：==在 js 中 双引号和单引号都表示字符串类型的数据

* **boolean**：布尔。true，false

  ```js
  var flag = true;
  var flag2 = false;
  
  alert(typeof flag); //结果是 boolean
  alert(typeof flag2); //结果是 boolean
  ```

* **null**：对象为空

  ```js
  var obj = null;
  
  alert(typeof obj);//结果是 object
  ```

  为什么打印上面的 obj 变量的数据类型，结果是object；这个官方给出了解释，下面是从官方文档截的图

  <img src="D:/download/downloadFromMicsoft/day07-JavaScript/ppt/assets/image-20210815173003408.png" alt="image-20210815173003408" style="zoom:80%;" />

* **undefined**：当声明的变量未初始化时，该变量的默认值是 undefined

  ```js
  var a ;
  alert(typeof a); //结果是 undefined
  ```

### 3.5  运算符

JavaScript 提供了如下的运算符。大部分和 Java语言 都是一样的，不同的是 JS 关系运算符中的 `==` 和 `===`，一会只演示这两个的区别，其他运算符将不做演示

* 一元运算符：++，--

* 算术运算符：+，-，*，/，%

* 赋值运算符：=，+=，-=…

* 关系运算符：>，<，>=，<=，!=，\==，===…

* 逻辑运算符：&&，||，!

* 三元运算符：条件表达式 ? true_value : false_value 

#### 3.5.1  \==和===区别

**概述:**

* ==：

  1. 判断类型是否一样，如果不一样，则进行类型转换

  2. 再去比较其值

* ===：js 中的全等于

  1. 判断类型是否一样，如果不一样，直接返回false
  2. 再去比较其值

**代码：**

```js
var age1 = 20;
var age2 = "20";

alert(age1 == age2);// true
alert(age1 === age2);// false
```

#### 3.5.2  类型转换

上述讲解 `==` 运算符时，发现会进行类型转换，所以接下来来详细的讲解一下 JavaScript 中的类型转换。

* 其他类型转为number

  * string 转换为 number 类型：按照字符串的字面值，转为数字。如果字面值不是数字，则转为NaN

    将 string 转换为 number 有两种方式：

    * 使用 `+` 正号运算符：

      ```js
      var str = +"20";
      alert(str + 1) //21
      ```

    * 使用 `parseInt()` 函数(方法)：

      ```js
      var str = "20";
      alert(parseInt(str) + 1);
      ```

    > ==建议使用 `parseInt()` 函数进行转换。==

  * boolean 转换为 number 类型：true 转为1，false转为0

    ```js
    var flag = +false;
    alert(flag); // 0
    ```

* 其他类型转为boolean

  * number 类型转换为 boolean 类型：0和NaN转为false，其他的数字转为true
  * string 类型转换为 boolean 类型：空字符串转为false，其他的字符串转为true
  * null类型转换为 boolean 类型是 false
  * undefined 转换为 boolean 类型是 false

  **代码如下：**

  ```js
  // var flag = 3;
  // var flag = "";
  var flag = undefined;
  
  if(flag){
      alert("转为true");
  }else {
      alert("转为false");
  }
  ```

**使用场景：**

在 Java 中使用字符串前，一般都会先判断字符串不是null，并且不是空字符才会做其他的一些操作，JavaScript也有类型的操作，代码如下：

```js
var str = "abc";

//健壮性判断
if(str != null && str.length > 0){
    alert("转为true");
}else {
    alert("转为false");
}
```

但是由于 JavaScript 会自动进行类型转换，所以上述的判断可以进行简化，代码如下：

```js
var str = "abc";

//健壮性判断
if(str){
    alert("转为true");
}else {
    alert("转为false");
}
```



### 3.6  流程控制语句

JavaScript 中提供了和 Java 一样的流程控制语句，如下

* if 
* switch
* for
* while
* dowhile

#### 3.6.1  if 语句

```js
var count = 3;
if (count == 3) {
    alert(count);
}
```

#### 3.6.2  switch 语句

```js
var num = 3;
switch (num) {
    case 1:
        alert("星期一");
        break;
    case 2:
        alert("星期二");
        break;
    case 3:
        alert("星期三");
        break;
    case 4:
        alert("星期四");
        break;
    case 5:
        alert("星期五");
        break;
    case 6:
        alert("星期六");
        break;
    case 7:
        alert("星期日");
        break;
    default:
        alert("输入的星期有误");
        break;
}
```

#### 3.6.3  for 循环语句

```js
var sum = 0;
for (let i = 1; i <= 100; i++) { //建议for循环小括号中定义的变量使用let
    sum += i;
}
alert(sum);
```

#### 3.6.4  while 循环语句

```js
var sum = 0;
var i = 1;
while (i <= 100) {
    sum += i;
    i++;
}
alert(sum);
```

#### 3.6.5  dowhile 循环语句

```js
var sum = 0;
var i = 1;
do {
    sum += i;
    i++;
}
while (i <= 100);
alert(sum);
```

### 3.7  函数

函数（就是Java中的方法）是被设计为执行特定任务的代码块；JavaScript 函数通过 function 关键词进行定义。

#### 3.7.1  定义格式

函数定义格式有两种：

* 方式1

  ```js
  function 函数名(参数1,参数2..){
      要执行的代码
  }
  ```

* 方式2

  ```js
  var 函数名 = function (参数列表){
      要执行的代码
  }
  ```

> ==注意：==
>
> * 形式参数不需要类型。因为JavaScript是弱类型语言
>
>   ```js
>   function add(a, b){
>       return a + b;
>   }
>   ```
>
>   上述函数的参数 a 和 b 不需要定义数据类型，因为在每个参数前加上 var 也没有任何意义。
>
> * 返回值也不需要定义类型，可以在函数内部直接使用return返回即可

#### 3.7.2  函数调用

函数调用函数：

```js
函数名称(实际参数列表);
```

eg：

```js
let result = add(10,20);
```

> ==注意：==
>
> * JS中，函数调用可以传递任意个数参数
>
> * 例如  `let result = add(1,2,3);` 
>
>   它是将数据 1 传递给了变量a，将数据 2 传递给了变量 b，而数据 3 没有变量接收。

## 4，JavaScript常用对象

JavaScript 提供了很多对象供使用者来使用。这些对象总共分类三类

* 基本对象

  <img src="D:/download/downloadFromMicsoft/day07-JavaScript/ppt/assets/image-20210815183147297.png" alt="image-20210815183147297" style="zoom:80%;" />

* BOM 对象

  <img src="D:/download/downloadFromMicsoft/day07-JavaScript/ppt/assets/image-20210815183207660.png" alt="image-20210815183207660" style="zoom:80%;" />

* DOM对象

  DOM 中的对象就比较多了，下图只是截取部分

  <img src="D:/download/downloadFromMicsoft/day07-JavaScript/ppt/assets/image-20210815183225718.png" alt="image-20210815183225718" style="zoom:80%;" />

这小节先学习基本对象，而先学习 `Array` 数组对象和 `String` 字符串对象。

### 4.1  Array对象

JavaScript Array对象用于定义数组

#### 4.1.1  定义格式

数组的定义格式有两种：

* 方式1

  ```js
  var 变量名 = new Array(元素列表); 
  ```

  例如：

  ```js
  var arr = new Array(1,2,3); //1,2,3 是存储在数组中的数据（元素）
  ```

* 方式2

  ```js
  var 变量名 = [元素列表];
  ```

  例如：

  ```js
  var arr = [1,2,3]; //1,2,3 是存储在数组中的数据（元素）
  ```

  ==注意：Java中的数组静态初始化使用的是{}定义，而 JavaScript 中使用的是 [] 定义==

#### 4.1.2  元素访问

访问数组中的元素和 Java 语言的一样，格式如下：

```js
arr[索引] = 值;
```

**代码演示：**

```js
 // 方式一
var arr = new Array(1,2,3);
// alert(arr);

// 方式二
var arr2 = [1,2,3];
//alert(arr2);

// 访问
arr2[0] = 10;
alert(arr2)
```

#### 4.1.3  特点

JavaScript 中的数组相当于 Java 中集合。数组的长度是可以变化的，而 JavaScript 是弱类型，所以可以存储任意的类型的数据。

例如如下代码：

```js
// 变长
var arr3 = [1,2,3];
arr3[10] = 10;
alert(arr3[10]); // 10
alert(arr3[9]);  //undefined
```

上面代码在定义数组中给了三个元素，又给索引是 10 的位置添加了数据 10，那么 `索引3` 到 `索引9` 位置的元素是什么呢？之前就介绍了，在 JavaScript 中没有赋值的话，默认就是 `undefined`。

如果给 `arr3` 数组添加字符串的数据，也是可以添加成功的

```js
arr3[5] = "hello";
alert(arr3[5]); // hello
```

#### 4.1.4  属性

Array 对象提供了很多属性，如下图是官方文档截取的

<img src="D:/download/downloadFromMicsoft/day07-JavaScript/ppt/assets/image-20210815190319166.png" alt="image-20210815190319166" style="zoom:80%;" />

而只讲解 `length` 属性，该数组可以动态的获取数组的长度。而有这个属性，就可以遍历数组了

```js
var arr = [1,2,3];
for (let i = 0; i < arr.length; i++) {
    alert(arr[i]);
}
```

#### 4.1.5  方法

Array 对象同样也提供了很多方法，如下图是官方文档截取的

<img src="D:/download/downloadFromMicsoft/day07-JavaScript/ppt/assets/image-20210815190601340.png" alt="image-20210815190601340" style="zoom:80%;" />

而在课堂中只演示 `push` 函数和 `splice` 函数。

* push 函数：给数组添加元素，也就是在数组的末尾添加元素

  参数表示要添加的元素

  ```js
  // push:添加方法
  var arr5 = [1,2,3];
  arr5.push(10);
  alert(arr5);  //数组的元素是 {1,2,3,10}
  ```

* splice 函数：删除元素

  参数1：索引。表示从哪个索引位置删除

  参数2：个数。表示删除几个元素

  ```js
  // splice:删除元素
  var arr5 = [1,2,3];
  arr5.splice(0,1); //从 0 索引位置开始删除，删除一个元素 
  alert(arr5); // {2,3}
  ```

### 4.2  String对象

String对象的创建方式有两种

* 方式1：

  ```js
  var 变量名 = new String(s); 
  ```

* 方式2：

  ```js
  var 变量名 = "数组"; 
  ```

**属性：**

String对象提供了很多属性，下面给大家列举了一个属性 `length` ，该属性是用于动态的获取字符串的长度

<img src="D:/download/downloadFromMicsoft/day07-JavaScript/ppt/assets/image-20210815192504884.png" alt="image-20210815192504884" style="zoom:60%;" />

**函数：**

String对象提供了很多函数（方法），下面给大家列举了两个方法。

<img src="D:/download/downloadFromMicsoft/day07-JavaScript/ppt/assets/image-20210815192544172.png" alt="image-20210815192544172" style="zoom:70%;" />

String对象还有一个函数 `trim()` ，该方法在文档中没有体现，但是所有的浏览器都支持；它是用来去掉字符串两端的空格。

代码演示：

```js
var str4 = '  abc   ';
alert(1 + str4 + 1);
```

上面代码会输出内容 `1  abc  1`，很明显可以看到 abc 字符串左右两边是有空格的。接下来使用 `trim()` 函数

```js
var str4 = '  abc   ';
alert(1 + str4.trim() + 1);
```

输出的内容是 `1abc1` 。这就是 `trim()` 函数的作用。

`trim()` 函数在以后开发中还是比较常用的，例如下图所示是登陆界面

<img src="D:/download/downloadFromMicsoft/day07-JavaScript/ppt/assets/image-20210815193420418.png" alt="image-20210815193420418" style="zoom:80%;"/> 

用户在输入用户名和密码时，可能会习惯的输入一些空格，这样在后端程序中判断用户名和密码是否正确，结果肯定是失败。所以一般都会对用户输入的字符串数据进行去除前后空格的操作。

### 4.3  自定义对象

在 JavaScript 中自定义对象特别简单，下面就是自定义对象的格式：

```js
var 对象名称 = {
    属性名称1:属性值1,
    属性名称2:属性值2,
    ...,
    函数名称:function (形参列表){},
	...
};
```

调用属性的格式：

```js
对象名.属性名
```

调用函数的格式：

```js
对象名.函数名()
```

接下来通过代码演示一下，让大家体验一下 JavaScript 中自定义对象

```js
var person = {
        name : "zhangsan",
        age : 23,
        eat: function (){
            alert("干饭~");
        }
    };


alert(person.name);  //zhangsan
alert(person.age); //23

person.eat();  //干饭~
```

## 5，BOM

BOM：Browser Object Model 浏览器对象模型。也就是 JavaScript 将浏览器的各个组成部分封装为对象。

要操作浏览器的各个组成部分就可以通过操作 BOM 中的对象来实现。比如：我现在想将浏览器地址栏的地址改为 `https://www.itheima.com` 就可以通过使用 BOM 中定义的 `Location` 对象的 `href` 属性，代码： `location.href = "https://itheima.com";` 

 BOM 中包含了如下对象：

* Window：浏览器窗口对象
* Navigator：浏览器对象
* Screen：屏幕对象
* History：历史记录对象
* Location：地址栏对象

下图是 BOM 中的各个对象和浏览器的各个组成部分的对应关系

<img src="D:/download/downloadFromMicsoft/day07-JavaScript/ppt/assets/image-20210815194911914.png" alt="image-20210815194911914" style="zoom:70%;" />

BOM 中的 `Navigator` 对象和 `Screen` 对象基本不会使用，所以的课堂只对 `Window`、`History`、`Location` 对象进行讲解。

### 5.1  Window对象

window 对象是 JavaScript 对浏览器的窗口进行封装的对象。

#### 5.1.1  获取window对象

该对象不需要创建直接使用 `window`，其中 `window. ` 可以省略。比如之前使用的 `alert()` 函数，其实就是 `window` 对象的函数，在调用是可以写成如下两种

* 显式使用 `window` 对象调用

  ```js
  window.alert("abc");
  ```

* 隐式调用

  ```
  alert("abc")
  ```

#### 5.1.2  window对象属性

`window` 对象提供了用于获取其他 BOM 组成对象的属性

<img src="D:/download/downloadFromMicsoft/day07-JavaScript/ppt/assets/image-20210815200625592.png" alt="image-20210815200625592" style="zoom:80%;" />

也就是说，想使用 `Location` 对象的话，就可以使用 `window` 对象获取；写成 `window.location`，而 `window.` 可以省略，简化写成 `location` 来获取 `Location` 对象。

#### 5.1.3  window对象函数

`window` 对象提供了很多函数供使用，而很多都不常用；下面给大家列举了一些比较常用的函数

<img src="D:/download/downloadFromMicsoft/day07-JavaScript/ppt/assets/image-20210815201323329.png" alt="image-20210815201323329" style="zoom:80%;" />

> `setTimeout(function,毫秒值)` : 在一定的时间间隔后执行一个function，只执行一次
> `setInterval(function,毫秒值)` :在一定的时间间隔后执行一个function，循环执行

**confirm代码演示：**

```js
// confirm()，点击确定按钮，返回true，点击取消按钮，返回false
var flag = confirm("确认删除？");

alert(flag);
```

下图是 `confirm()` 函数的效果。当点击 `确定` 按钮，`flag` 变量值记录的就是 `true` ；当点击 `取消` 按钮，`flag` 变量值记录的就是 `false`。

<img src="D:/download/downloadFromMicsoft/day07-JavaScript/ppt/assets/image-20210815201600493.png" alt="image-20210815201600493" style="zoom:80%;" />

而以后在页面删除数据时候如下图每一条数据后都有 `删除` 按钮，有可能是用户的一些误操作，所以对于删除操作需要用户进行再次确认，此时就需要用到 `confirm()` 函数。

<img src="D:/download/downloadFromMicsoft/day07-JavaScript/ppt/assets/image-20210815202406490.png" alt="image-20210815202406490" style="zoom:70%;" />

**定时器代码演示：**

```js
setTimeout(function (){
    alert("hehe");
},3000);
```

当打开浏览器，3秒后才会弹框输出 `hehe`，并且只会弹出一次。

```js
setInterval(function (){
    alert("hehe");
},2000);
```

当打开浏览器，每隔2秒都会弹框输出 `hehe`。

#### 5.1.4  案例

**需求：每隔1秒，灯泡切换一次状态**

<img src="D:/download/downloadFromMicsoft/day07-JavaScript/ppt/assets/image-20210815203345262.png" alt="image-20210815203345262" style="zoom:70%;" />

需求说明：

有如下页面效果，实现定时进行开灯、关灯功能

<img src="D:/download/downloadFromMicsoft/day07-JavaScript/ppt/assets/image-20210815203623739.png" alt="image-20210815203623739" style="zoom:80%;" />

初始页面环境

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>JavaScript演示</title>
</head>
<body>

<input type="button" onclick="on()" value="开灯">
<img id="myImage" border="0" src="../imgs/off.gif" style="text-align:center;">
<input type="button" onclick="off()" value="关灯">

<script>
    function on(){
        document.getElementById('myImage').src='../imgs/on.gif';
    }

    function off(){
        document.getElementById('myImage').src='../imgs/off.gif'
    }

</script>
</body>
</html>
```

代码实现：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>JavaScript演示</title>
</head>
<body>

<input type="button" onclick="on()" value="开灯">
<img id="myImage" border="0" src="../imgs/off.gif" style="text-align:center;">
<input type="button" onclick="off()" value="关灯">

<script>
    function on(){
        document.getElementById('myImage').src='../imgs/on.gif';
    }

    function off(){
        document.getElementById('myImage').src='../imgs/off.gif'
    }
    
    //定义一个变量，用来记录灯的状态，偶数是开灯状态，奇数是关灯状态
    var x = 0;
    //使用循环定时器
    setInterval(function (){
        if(x % 2 == 0){//表示是偶数，开灯状态，调用 on() 函数
            on();
        }else {  //表示是奇数，关灯状态，调用 off() 函数
            off();
        }
        x ++;//改变变量的值
    },1000);

</script>
</body>
</html>
```

### 5.2  History对象

History 对象是 JavaScript 对历史记录进行封装的对象。

* History 对象的获取

  使用 window.history获取，其中window. 可以省略

* History 对象的函数

  <img src="D:/download/downloadFromMicsoft/day07-JavaScript/ppt/assets/image-20210815224826535.png" alt="image-20210815224826535" style="zoom:70%;" />

  这两个函数平时在访问其他的一些网站时经常使用对应的效果，如下图

  <img src="D:/download/downloadFromMicsoft/day07-JavaScript/ppt/assets/image-20210815225059114.png" alt="image-20210815225059114" style="zoom:80%;" />

  当点击向左的箭头，就跳转到前一个访问的页面，这就是 `back()` 函数的作用；当点击向右的箭头，就跳转到下一个访问的页面，这就是 `forward()` 函数的作用。

### 5.3  Location对象

<img src="D:/download/downloadFromMicsoft/day07-JavaScript/ppt/assets/image-20210815225243560.png" alt="image-20210815225243560" style="zoom:80%;" />

Location 对象是 JavaScript 对地址栏封装的对象。可以通过操作该对象，跳转到任意页面。

#### 5.3.1  获取Location对象

使用 window.location获取，其中window. 可以省略

```js
window.location.方法();
location.方法();
```



#### 5.3.2  Location对象属性

Location对象提供了很对属性。以后常用的只有一个属性 `href`

<img src="D:/download/downloadFromMicsoft/day07-JavaScript/ppt/assets/image-20210815225707580.png" alt="image-20210815225707580" style="zoom:80%;" />

**代码演示：**

```js
alert("要跳转了");
location.href = "https://www.baidu.com";
```

在浏览器首先会弹框显示 `要跳转了`，当点击了 `确定` 就会跳转到 百度 的首页。



#### 5.3.3  案例

**需求：3秒跳转到百度首页**

**分析：**

1. 3秒跳转，由此可以确定需要使用到定时器，而只跳转一次，所以使用 `setTimeOut()`
2. 要进行页面跳转，所以需要用到 `location` 对象的 `href` 属性实现

**代码实现：**

```js
document.write("3秒跳转到首页..."); 
setTimeout(function (){
    location.href = "https://www.baidu.com"
},3000);
```

## 6，DOM

### 6.1  概述

DOM：Document Object Model 文档对象模型。也就是 JavaScript 将 HTML 文档的各个组成部分封装为对象。

DOM 其实并不陌生，之前在学习 XML 就接触过，只不过 XML 文档中的标签需要写代码解析，而 HTML 文档是浏览器解析。封装的对象分为

* Document：整个文档对象
* Element：元素对象
* Attribute：属性对象
* Text：文本对象
* Comment：注释对象

如下图，左边是 HTML 文档内容，右边是 DOM 树

![image-20210815231028430](D:/download/downloadFromMicsoft/day07-JavaScript/ppt/assets/image-20210815231028430.png)

**作用：**

JavaScript 通过 DOM， 就能够对 HTML进行操作了

* 改变 HTML 元素的内容
* 改变 HTML 元素的样式（CSS）
* 对 HTML DOM 事件作出反应
* 添加和删除 HTML 元素

**DOM相关概念：**

DOM 是 W3C（万维网联盟）定义了访问 HTML 和 XML 文档的标准。该标准被分为 3 个不同的部分：

1. 核心 DOM：针对任何结构化文档的标准模型。 XML 和 HTML 通用的标准

   * Document：整个文档对象

   * Element：元素对象

   * Attribute：属性对象

   * Text：文本对象

   * Comment：注释对象

2. XML DOM： 针对 XML 文档的标准模型

3. HTML DOM： 针对 HTML 文档的标准模型

   该标准是在核心 DOM 基础上，对 HTML 中的每个标签都封装成了不同的对象

   * 例如：`<img>` 标签在浏览器加载到内存中时会被封装成 `Image` 对象，同时该对象也是 `Element` 对象。
   * 例如：`<input type='button'>` 标签在浏览器加载到内存中时会被封装成 `Button` 对象，同时该对象也是 `Element` 对象。

### 6.2  获取 Element对象

HTML 中的 Element 对象可以通过 `Document` 对象获取，而 `Document` 对象是通过 `window` 对象获取。

`Document` 对象中提供了以下获取 `Element` 元素对象的函数

* `getElementById()`：根据id属性值获取，返回单个Element对象
* `getElementsByTagName()`：根据标签名称获取，返回Element对象数组
* `getElementsByName()`：根据name属性值获取，返回Element对象数组
* `getElementsByClassName()`：根据class属性值获取，返回Element对象数组

**代码演示：**

下面有提前准备好的页面：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <img id="light" src="../imgs/off.gif"> <br>

    <div class="cls">传智教育</div>   <br>
    <div class="cls">黑马程序员</div> <br>

    <input type="checkbox" name="hobby"> 电影
    <input type="checkbox" name="hobby"> 旅游
    <input type="checkbox" name="hobby"> 游戏
    <br>
    <script>
		//在此处书写js代码
    </script>
</body>
</html>
```

1. 根据 `id` 属性值获取上面的 `img` 元素对象，返回单个对象

   ```js
   var img = document.getElementById("light");
   alert(img);
   ```

   结果如下：

   <img src="D:/download/downloadFromMicsoft/day07-JavaScript/ppt/assets/image-20210815233232924.png" alt="image-20210815233232924" style="zoom:80%;" />

   从弹框输出的内容，也可以看出是一个图片元素对象。

2. 根据标签名称获取所有的 `div` 元素对象

   ```js
   var divs = document.getElementsByTagName("div");// 返回一个数组，数组中存储的是 div 元素对象
   // alert(divs.length);  //输出 数组的长度
   //遍历数组
   for (let i = 0; i < divs.length; i++) {
       alert(divs[i]);
   }
   ```

3. 获取所有的满足 `name = 'hobby'` 条件的元素对象

   ```js
   //3. getElementsByName：根据name属性值获取，返回Element对象数组
   var hobbys = document.getElementsByName("hobby");
   for (let i = 0; i < hobbys.length; i++) {
       alert(hobbys[i]);
   }
   ```

4. 获取所有的满足 `class='cls'` 条件的元素对象

   ```js
   //4. getElementsByClassName：根据class属性值获取，返回Element对象数组
   var clss = document.getElementsByClassName("cls");
   for (let i = 0; i < clss.length; i++) {
       alert(clss[i]);
   }
   ```

### 6.3  HTML Element对象使用

HTML 中的 `Element` 元素对象有很多，不可能全部记住，以后是根据具体的需求查阅文档使用。

下面通过具体的案例给大家演示文档的查询和对象的使用；下面提前给大家准备好的页面

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <img id="light" src="../imgs/off.gif"> <br>

    <div class="cls">传智教育</div>   <br>
    <div class="cls">黑马程序员</div> <br>

    <input type="checkbox" name="hobby"> 电影
    <input type="checkbox" name="hobby"> 旅游
    <input type="checkbox" name="hobby"> 游戏
    <br>
    <script>
        //在此处写js低吗
    </script>
</body>
</html>
```

**需求：**

1. 点亮灯泡

   此案例由于需要改变 `img` 标签 的图片，所以查询文档，下图是查看文档的流程：

   <img src="D:/download/downloadFromMicsoft/day07-JavaScript/ppt/assets/查看文档.png" alt="image-20210815233232924" style="zoom:100%;" />

   代码实现：

   ```js
   //1，根据 id='light' 获取 img 元素对象
   var img = document.getElementById("light");
   //2，修改 img 对象的 src 属性来改变图片
   img.src = "../imgs/on.gif";
   ```

2. 将所有的 `div` 标签的标签体内容替换为 `呵呵`

   ```js
   //1，获取所有的 div 元素对象
   var divs = document.getElementsByTagName("div");
   /*
           style:设置元素css样式
           innerHTML：设置元素内容
       */
   //2，遍历数组，获取到每一个 div 元素对象，并修改元素内容
   for (let i = 0; i < divs.length; i++) {
       //divs[i].style.color = 'red';
       divs[i].innerHTML = "呵呵";
   }
   ```

3. 使所有的复选框呈现被选中的状态

   此案例需要看 复选框 元素对象有什么属性或者函数是来操作 复选框的选中状态。下图是文档的查看

   ![image-20210816000520457](D:/download/downloadFromMicsoft/day07-JavaScript/ppt/assets/image-20210816000520457.png)

   代码实现：

   ```js
   //1，获取所有的 复选框 元素对象
   var hobbys = document.getElementsByName("hobby");
   //2，遍历数组，通过将 复选框 元素对象的 checked 属性值设置为 true 来改变复选框的选中状态
   for (let i = 0; i < hobbys.length; i++) {
       hobbys[i].checked = true;
   }
   ```

## 7，事件监听

要想知道什么是事件监听，首先先聊聊什么是事件？

HTML 事件是发生在 HTML 元素上的“事情”。比如：页面上的 `按钮被点击`、`鼠标移动到元素之上`、`按下键盘按键` 等都是事件。

事件监听是JavaScript 可以在事件被侦测到时==执行一段逻辑代码。==例如下图当点击 `开灯` 按钮，就需要通过 js 代码实现替换图片

<img src="D:/download/downloadFromMicsoft/day07-JavaScript/ppt/assets/image-20210816194143246.png" alt="image-20210816194143246" style="zoom:80%;" />

再比如下图输入框，当输入了用户名 `光标离开` 输入框，就需要通过 js 代码对输入的内容进行校验，没通过校验就在输入框后提示 `用户名格式有误!`

<img src="D:/download/downloadFromMicsoft/day07-JavaScript/ppt/assets/image-20210816194333252.png" alt="image-20210816194333252" style="zoom:90%;" />

### 7.1  事件绑定

JavaScript 提供了两种事件绑定方式：

* 方式一：通过 HTML标签中的事件属性进行绑定

  如下面代码，有一个按钮元素，是在该标签上定义 `事件属性`，在事件属性中绑定函数。`onclick` 就是 `单击事件` 的事件属性。`onclick='on（）'` 表示该点击事件绑定了一个名为 `on()` 的函数

  ```html
  <input type="button" onclick='on()’>
  ```

  下面是点击事件绑定的 `on()` 函数

  ```js
  function on(){
  	alert("我被点了");
  }
  ```

* 方式二：通过 DOM 元素属性绑定

  如下面代码是按钮标签，在该标签上并没有使用 `事件属性`，绑定事件的操作需要在 js 代码中实现

  ```html
  <input type="button" id="btn">
  ```

  下面 js 代码是获取了 `id='btn'` 的元素对象，然后将 `onclick` 作为该对象的属性，并且绑定匿名函数。该函数是在事件触发后自动执行

  ```js
  document.getElementById("btn").onclick = function (){
      alert("我被点了");
  }
  ```

**代码演示：**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <!--方式1：在下面input标签上添加 onclick 属性，并绑定 on() 函数-->
    <input type="button" value="点我" onclick="on()"> <br>
    <input type="button" value="再点我" id="btn">

    <script>
        function on(){
            alert("我被点了");
        }
      	//方式2：获取 id="btn" 元素对象，通过调用 onclick 属性 绑定点击事件
        document.getElementById("btn").onclick = function (){
            alert("我被点了");
        }
    </script>
</body>
</html>
```

### 7.2  常见事件

上面案例中使用到了 `onclick` 事件属性，那都有哪些事件属性供使用呢？下面就给大家列举一些比较常用的事件属性

| 事件属性名  | 说明                     |
| ----------- | ------------------------ |
| onclick     | 鼠标单击事件             |
| onblur      | 元素失去焦点             |
| onfocus     | 元素获得焦点             |
| onload      | 某个页面或图像被完成加载 |
| onsubmit    | 当表单提交时触发该事件   |
| onmouseover | 鼠标被移到某元素之上     |
| onmouseout  | 鼠标从某元素移开         |

* `onfocus` 获得焦点事件。

  如下图，当点击了输入框后，输入框就获得了焦点。而下图示例是当获取焦点后会更改输入框的背景颜色。

  <img src="D:/download/downloadFromMicsoft/day07-JavaScript/ppt/assets/image-20210816214900928.png" alt="image-20210816214900928" style="zoom:80%;" />

* `onblur  ` 失去焦点事件。

  如下图，当点击了输入框后，输入框就获得了焦点；再点击页面其他位置，那输入框就失去焦点了。下图示例是将输入的文本转换为大写。

  <img src="D:/download/downloadFromMicsoft/day07-JavaScript/ppt/assets/image-20210816215235969.png" alt="image-20210816215235969" style="zoom:80%;" />

* `onmouseout  ` 鼠标移出事件。

* `onmouseover  `  鼠标移入事件。

  如下图，当鼠标移入到 苹果 图片上时，苹果图片变大；当鼠标移出 苹果图片时，苹果图片变小。

  <img src="D:/download/downloadFromMicsoft/day07-JavaScript/ppt/assets/image-20210816220149093.png" alt="image-20210816220149093" style="zoom:70%;" />

* `onsubmit  ` 表单提交事件

  如下是带有表单的页面

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>Title</title>
  </head>
  <body>
      <form id="register" action="#" >
          <input type="text" name="username" />
          <input type="submit" value="提交">
      </form>
      <script>
          
      </script>
  </body>
  </html>
  ```

  如上代码的表单，当点击 `提交` 按钮后，表单就会提交，此处默认使用的是 `GET` 提交方式，会将提交的数据拼接到 URL 后。现需要通过 js 代码实现阻止表单提交的功能，js 代码实现如下：

  1. 获取 `form` 表单元素对象。
  2. 给 `form` 表单元素对象绑定 `onsubmit` 事件，并绑定匿名函数。
  3. 该匿名函数如果返回的是true，提交表单；如果返回的是false，阻止表单提交。

  ```js
  document.getElementById("register").onsubmit = function (){
      //onsubmit 返回true，则表单会被提交，返回false，则表单不提交
      return true;
  }
  ```

## 8，表单验证案例

### 8.1  需求

<img src="D:/download/downloadFromMicsoft/day07-JavaScript/ppt/assets/image-20210816225925955.png" alt="image-20210816225925955" style="zoom:60%;" />

有如下注册页面，对表单进行校验，如果输入的用户名、密码、手机号符合规则，则允许提交；如果不符合规则，则不允许提交。

完成以下需求：

1. 当输入框失去焦点时，验证输入内容是否符合要求

2. 当点击注册按钮时，判断所有输入框的内容是否都符合要求，如果不合符则阻止表单提交

### 8.2  环境准备

下面是初始页面

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>欢迎注册</title>
    <link href="../css/register.css" rel="stylesheet">
</head>
<body>
    <div class="form-div">
        <div class="reg-content">
            <h1>欢迎注册</h1>
            <span>已有帐号？</span> <a href="#">登录</a>
        </div>
        <form id="reg-form" action="#" method="get">
            <table>
                <tr>
                    <td>用户名</td>
                    <td class="inputs">
                        <input name="username" type="text" id="username">
                        <br>
                        <span id="username_err" class="err_msg" style="display: none">用户名不太受欢迎</span>
                    </td>
                </tr>

                <tr>
                    <td>密码</td>
                    <td class="inputs">
                        <input name="password" type="password" id="password">
                        <br>
                        <span id="password_err" class="err_msg" style="display: none">密码格式有误</span>
                    </td>
                </tr>

                <tr>
                    <td>手机号</td>
                    <td class="inputs"><input name="tel" type="text" id="tel">
                        <br>
                        <span id="tel_err" class="err_msg" style="display: none">手机号格式有误</span>
                    </td>
                </tr>
            </table>
            <div class="buttons">
                <input value="注 册" type="submit" id="reg_btn">
            </div>
            <br class="clear">
        </form>

    </div>


    <script>

    </script>
</body>
</html>
```

### 8.3  验证输入框

此小节完成如下功能：

* 校验用户名。当用户名输入框失去焦点时，判断输入的内容是否符合 `长度是 6-12 位` 规则，不符合使 `id='username_err'` 的span标签显示出来，给出用户提示。
* 校验密码。当密码输入框失去焦点时，判断输入的内容是否符合 `长度是 6-12 位` 规则，不符合使 `id='password_err'` 的span标签显示出来，给出用户提示。
* 校验手机号。当手机号输入框失去焦点时，判断输入的内容是否符合 `长度是 11 位` 规则，不符合使 `id='tel_err'` 的span标签显示出来，给出用户提示。

代码如下：

```js
//1. 验证用户名是否符合规则
//1.1 获取用户名的输入框
var usernameInput = document.getElementById("username");

//1.2 绑定onblur事件 失去焦点
usernameInput.onblur = function () {
    //1.3 获取用户输入的用户名
    var username = usernameInput.value.trim();

    //1.4 判断用户名是否符合规则：长度 6~12
    if (username.length >= 6 && username.length <= 12) {
        //符合规则
        document.getElementById("username_err").style.display = 'none';
    } else {
        //不合符规则
        document.getElementById("username_err").style.display = '';
    }
}

//1. 验证密码是否符合规则
//1.1 获取密码的输入框
var passwordInput = document.getElementById("password");

//1.2 绑定onblur事件 失去焦点
passwordInput.onblur = function() {
    //1.3 获取用户输入的密码
    var password = passwordInput.value.trim();

    //1.4 判断密码是否符合规则：长度 6~12
    if (password.length >= 6 && password.length <= 12) {
        //符合规则
        document.getElementById("password_err").style.display = 'none';
    } else {
        //不合符规则
        document.getElementById("password_err").style.display = '';
    }
}

//1. 验证手机号是否符合规则
//1.1 获取手机号的输入框
var telInput = document.getElementById("tel");

//1.2 绑定onblur事件 失去焦点
telInput.onblur = function() {
    //1.3 获取用户输入的手机号
    var tel = telInput.value.trim();

    //1.4 判断手机号是否符合规则：长度 11
    if (tel.length == 11) {
        //符合规则
        document.getElementById("tel_err").style.display = 'none';
    } else {
        //不合符规则
        document.getElementById("tel_err").style.display = '';
    }
}
```

### 8.3  验证表单

当用户点击 `注册` 按钮时，需要同时对输入的 `用户名`、`密码`、`手机号` ，如果都符合规则，则提交表单；如果有一个不符合规则，则不允许提交表单。实现该功能需要获取表单元素对象，并绑定 `onsubmit` 事件

```js
//1. 获取表单对象
var regForm = document.getElementById("reg-form");

//2. 绑定onsubmit 事件
regForm.onsubmit = function () {
    
}
```

`onsubmit` 事件绑定的函数需要对输入的 `用户名`、`密码`、`手机号` 进行校验，这些校验之前都已经实现过了，这里还需要再校验一次吗？不需要，只需要对之前校验的代码进行改造，把每个校验的代码专门抽象到有名字的函数中，方便调用；并且每个函数都要返回结果来去决定是提交表单还是阻止表单提交，代码如下：

```js
//1. 验证用户名是否符合规则
//1.1 获取用户名的输入框
var usernameInput = document.getElementById("username");

//1.2 绑定onblur事件 失去焦点
usernameInput.onblur = checkUsername;

function checkUsername() {
    //1.3 获取用户输入的用户名
    var username = usernameInput.value.trim();

    //1.4 判断用户名是否符合规则：长度 6~12
    var flag = username.length >= 6 && username.length <= 12;
    if (flag) {
        //符合规则
        document.getElementById("username_err").style.display = 'none';
    } else {
        //不合符规则
        document.getElementById("username_err").style.display = '';
    }
    return flag;
}

//1. 验证密码是否符合规则
//1.1 获取密码的输入框
var passwordInput = document.getElementById("password");

//1.2 绑定onblur事件 失去焦点
passwordInput.onblur = checkPassword;

function checkPassword() {
    //1.3 获取用户输入的密码
    var password = passwordInput.value.trim();

    //1.4 判断密码是否符合规则：长度 6~12
    var flag = password.length >= 6 && password.length <= 12;
    if (flag) {
        //符合规则
        document.getElementById("password_err").style.display = 'none';
    } else {
        //不合符规则
        document.getElementById("password_err").style.display = '';
    }
    return flag;
}

//1. 验证手机号是否符合规则
//1.1 获取手机号的输入框
var telInput = document.getElementById("tel");

//1.2 绑定onblur事件 失去焦点
telInput.onblur = checkTel;

function checkTel() {
    //1.3 获取用户输入的手机号
    var tel = telInput.value.trim();

    //1.4 判断手机号是否符合规则：长度 11
    var flag = tel.length == 11;
    if (flag) {
        //符合规则
        document.getElementById("tel_err").style.display = 'none';
    } else {
        //不合符规则
        document.getElementById("tel_err").style.display = '';
    }
    return flag;
}
```

而 `onsubmit` 绑定的函数需要调用 `checkUsername()` 函数、`checkPassword()` 函数、`checkTel()` 函数。

```js
//1. 获取表单对象
var regForm = document.getElementById("reg-form");

//2. 绑定onsubmit 事件
regForm.onsubmit = function () {
    //挨个判断每一个表单项是否都符合要求，如果有一个不合符，则返回false

    var flag = checkUsername() && checkPassword() && checkTel();

    return flag;
}
```

## 9，RegExp对象

RegExp 是正则对象。正则对象是判断指定字符串是否符合规则。

如下图是百度贴吧中的帖子

<img src="D:/download/downloadFromMicsoft/day07-JavaScript/ppt/assets/image-20210816235112754.png" alt="image-20210816235112754" style="zoom:70%;" />

可以通过爬虫技术去爬取该页面源代码，然后获取页面中所有的邮箱，后期可以给这些邮箱地址发送推广的邮件。那么问题来了，如何才能知道页面内容中哪些事邮箱地址呢？这里就可以使用正则表达式来匹配邮箱。

在 js 中对正则表达式封装的对象就是正则对象。

### 9.1  正则对象使用

#### 9.1.1  创建对象

正则对象有两种创建方式：

* 直接量方式：注意不要加引号

  ```js
  var reg = /正则表达式/;
  ```

* 创建 RegExp 对象

  ```js
  var reg = new RegExp("正则表达式");
  ```

#### 9.1.2  函数

`test(str)` ：判断指定字符串是否符合规则，返回 true或 false

### 9.2  正则表达式

从上面创建正则对象的格式中可以看出不管哪种方式都需要正则表达式，那么什么是正则表达式呢？

正则表达式定义了字符串组成的规则。也就是判断指定的字符串是否符合指定的规则，如果符合返回true，如果不符合返回false。

正则表达式是和语言无关的。很多语言都支持正则表达式，Java语言也支持，只不过正则表达式在不同的语言中的使用方式不同，js 中需要使用正则对象来使用正则表达式。

正则表达式常用的规则如下：

* ^：表示开始

* $：表示结束

* [ ]：代表某个范围内的单个字符，比如： [0-9] 单个数字字符

* .：代表任意单个字符，除了换行和行结束符

* \w：代表单词字符：字母、数字、下划线(_)，相当于 [A-Za-z0-9_]

* \d：代表数字字符： 相当于 [0-9]

量词：

* +：至少一个

* *：零个或多个

* ？：零个或一个

* {x}：x个

* {m,}：至少m个

* {m,n}：至少m个，最多n个

**代码演示：**

```js
// 规则：单词字符，6~12
//1,创建正则对象，对正则表达式进行封装
var reg = /^\w{6,12}$/;

var str = "abcccc";
//2,判断 str 字符串是否符合 reg 封装的正则表达式的规则
var flag = reg.test(str);
alert(flag);
```

### 9.3  改进表单校验案例

表单校验案例中的规则是进行一系列的判断来实现的，现在学习了正则对象后，就可以使用正则对象来改进这个案例。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>欢迎注册</title>
    <link href="../css/register.css" rel="stylesheet">
</head>
<body>

<div class="form-div">
    <div class="reg-content">
        <h1>欢迎注册</h1>
        <span>已有帐号？</span> <a href="#">登录</a>
    </div>
    <form id="reg-form" action="#" method="get">

        <table>

            <tr>
                <td>用户名</td>
                <td class="inputs">
                    <input name="username" type="text" id="username">
                    <br>
                    <span id="username_err" class="err_msg" style="display: none">用户名不太受欢迎</span>
                </td>

            </tr>

            <tr>
                <td>密码</td>
                <td class="inputs">
                    <input name="password" type="password" id="password">
                    <br>
                    <span id="password_err" class="err_msg" style="display: none">密码格式有误</span>
                </td>
            </tr>


            <tr>
                <td>手机号</td>
                <td class="inputs"><input name="tel" type="text" id="tel">
                    <br>
                    <span id="tel_err" class="err_msg" style="display: none">手机号格式有误</span>
                </td>
            </tr>

        </table>

        <div class="buttons">
            <input value="注 册" type="submit" id="reg_btn">
        </div>
        <br class="clear">
    </form>

</div>


<script>

    //1. 验证用户名是否符合规则
    //1.1 获取用户名的输入框
    var usernameInput = document.getElementById("username");

    //1.2 绑定onblur事件 失去焦点
    usernameInput.onblur = checkUsername;

    function checkUsername() {
        //1.3 获取用户输入的用户名
        var username = usernameInput.value.trim();

        //1.4 判断用户名是否符合规则：长度 6~12,单词字符组成
        var reg = /^\w{6,12}$/;
        var flag = reg.test(username);

        //var flag = username.length >= 6 && username.length <= 12;
        if (flag) {
            //符合规则
            document.getElementById("username_err").style.display = 'none';
        } else {
            //不合符规则
            document.getElementById("username_err").style.display = '';
        }
        return flag;
    }

    //1. 验证密码是否符合规则
    //1.1 获取密码的输入框
    var passwordInput = document.getElementById("password");

    //1.2 绑定onblur事件 失去焦点
    passwordInput.onblur = checkPassword;

    function checkPassword() {
        //1.3 获取用户输入的密码
        var password = passwordInput.value.trim();

        //1.4 判断密码是否符合规则：长度 6~12
        var reg = /^\w{6,12}$/;
        var flag = reg.test(password);

        //var flag = password.length >= 6 && password.length <= 12;
        if (flag) {
            //符合规则
            document.getElementById("password_err").style.display = 'none';
        } else {
            //不合符规则
            document.getElementById("password_err").style.display = '';
        }
        return flag;
    }

    //1. 验证手机号是否符合规则
    //1.1 获取手机号的输入框
    var telInput = document.getElementById("tel");

    //1.2 绑定onblur事件 失去焦点
    telInput.onblur = checkTel;

    function checkTel() {
        //1.3 获取用户输入的手机号
        var tel = telInput.value.trim();

        //1.4 判断手机号是否符合规则：长度 11，数字组成，第一位是1
        //var flag = tel.length == 11;
        var reg = /^[1]\d{10}$/;
        var flag = reg.test(tel);
        if (flag) {
            //符合规则
            document.getElementById("tel_err").style.display = 'none';
        } else {
            //不合符规则
            document.getElementById("tel_err").style.display = '';
        
        return flag;
    }

    //1. 获取表单对象
    var regForm = document.getElementById("reg-form");

    //2. 绑定onsubmit 事件
    regForm.onsubmit = function () {
        //挨个判断每一个表单项是否都符合要求，如果有一个不合符，则返回false

        var flag = checkUsername() && checkPassword() && checkTel();

        return flag;
    }
</script>
</body>
</html>
```



# 	HTTP&Tomcat&Servlet

**今日目标：**

> * 了解JavaWeb开发的技术栈
> * 理解HTTP协议和HTTP请求与响应数据的格式
> * 掌握Tomcat的使用
> * 掌握在IDEA中使用Tomcat插件
> * 理解Servlet的执行流程和生命周期
> * 掌握Servlet的使用和相关配置

## 1，Web概述

### 1.1 Web和JavaWeb的概念

==Web是全球广域网，也称为万维网(www)，能够通过浏览器访问的网站。==
在日常的生活中，经常会使用浏览器去访问`百度`、`京东`、`传智官网`等这些网站，这些网站统称为Web网站。如下就是通过浏览器访问传智官网的界面: 

知道了什么是Web，那么JavaWeb又是什么呢？顾名思义==JavaWeb就是用Java技术来解决相关web互联网领域的技术栈。==
等学习完JavaWeb之后，同学们就可以使用Java语言开发上述所说的网站。而国内很多大型网站公司也是首选Java语言来解决web互联网相关的问题。那都有哪些公司的系统是使用Java语言的呢?
 ![](D:/download/downloadFromMicsoft/day08-HTTP&Tomcat&Servlet/ppt/assets/20210717183958532.png)
使用Java语言开发互联网系统是有很多技术栈需要大家了解，具体都有哪些呢?

### 1.2 JavaWeb技术栈

了解JavaWeb技术栈之前，有一个很重要的概念要介绍。

#### 1.2.1 B/S架构

什么是B/S架构?
B/S 架构：Browser/Server，浏览器/服务器 架构模式，它的特点是，客户端只需要浏览器，应用程序的逻辑和数据都存储在服务器端。浏览器只需要请求服务器，获取Web资源，服务器把Web资源发送给浏览器即可。大家可以通过下面这张图来回想下平常的上网过程:


* 打开浏览器访问百度首页，输入要搜索的内容，点击回车或百度一下，就可以获取和搜索相关的内容
* 思考下搜索的内容并不在自己的点上，那么这些内容从何而来？答案很明显是从百度服务器返回给的
* 日常百度的小细节，逢年过节百度的logo会更换不同的图片，服务端发生变化，客户端不需做任务事情就能获取最新内容
* 所以说B/S架构的好处:易于维护升级：服务器端升级后，客户端无需任何部署就可以使用到新的版本。
  了解了什么是B/S架构后，作为后台开发工程师的将来主要关注的是服务端的开发和维护工作。在服务端将来会放很多资源,都有哪些资源呢?

#### 1.2.2 静态资源

* 静态资源主要包含HTML、CSS、JavaScript、图片等，主要负责页面的展示。
* 之前已经学过前端网页制作`三剑客`(HTML+CSS+JavaScript),使用这些技术就可以制作出效果比较丰富的网页，将来展现给用户。但是由于做出来的这些内容都是静态的，这就会导致所有的人看到的内容将是一模一样。
* 在日常上网的过程中，除了看到这些好看的页面以外，还会碰到很多动态内容，比如常见的百度登录效果:
  ![1627037814180](D:/download/downloadFromMicsoft/day08-HTTP&Tomcat&Servlet/ppt/assets/1627037814180.png)
  `张三`登录以后在网页的右上角看到的是 `张三`，而`李四`登录以后看到的则是`李四`。所以不同的用户访问相同的资源看到的内容大多数是不一样的，要想实现这样的效果，光靠静态资源是无法实现的。

#### 1.2.3 动态资源

* 动态资源主要包含Servlet、JSP等，主要用来负责逻辑处理。
* 动态资源处理完逻辑后会把得到的结果交给静态资源来进行展示，动态资源和静态资源要结合一起使用。
* 动态资源虽然可以处理逻辑，但是当用户来登录百度的时候，就需要输入`用户名`和`密码`,这个时候就又需要解决的一个问题是，用户在注册的时候填入的用户名和密码、以及经常会访问到一些数据列表的内容展示(如下图所示)，这些数据都存储在哪里?需要的时候又是从哪里来取呢?

#### 1.2.4 数据库

* 数据库主要负责存储数据。
* 整个Web的访问过程就如下图所示:

(1)浏览器发送一个请求到服务端，去请求所需要的相关资源;
(2)资源分为动态资源和静态资源,动态资源可以是使用Java代码按照Servlet和JSP的规范编写的内容;
(3)在Java代码可以进行业务处理也可以从数据库中读取数据;
(4)拿到数据后，把数据交给HTML页面进行展示,再结合CSS和JavaScript使展示效果更好;
(5)服务端将静态资源响应给浏览器;
(6)浏览器将这些资源进行解析;
(7)解析后将效果展示在浏览器，用户就可以看到最终的结果。
在整个Web的访问过程中，会设计到很多技术，这些技术有已经学习过的，也有还未涉及到的内容，都有哪些还没有涉及到呢?

#### 1.2.5 HTTP协议

* HTTP协议:主要定义通信规则
* 浏览器发送请求给服务器，服务器响应数据给浏览器，这整个过程都需要遵守一定的规则，之前大家学习过TCP、UDP，这些都属于规则，这里需要使用的是HTTP协议，这也是一种规则。

#### 1.2.6 Web服务器

* Web服务器:负责解析 HTTP 协议，解析请求数据，并发送响应数据
* 浏览器按照HTTP协议发送请求和数据，后台就需要一个Web服务器软件来根据HTTP协议解析请求和数据，然后把处理结果再按照HTTP协议发送给浏览器
* Web服务器软件有很多，课程中将学习的是目前最为常用的==Tomcat==服务器

到这为止，关于JavaWeb中用到的技术栈就介绍完了，这里面就只有HTTP协议、Servlet、JSP以及Tomcat这些知识是没有学习过的，所以整个Web核心主要就是来学习这些技术。

### 1.3 Web核心课程安排



整个Web核心，总共有六天的学习内容，分别是:

* 第一天：HTTP、Tomcat、Servlet
* 第二天：Request(请求)、Response(响应)
* 第三天：JSP、会话技术(Cookie、Session)
* 第四天：Filter(过滤器)、Listener(监听器)
* 第五天：Ajax、Vue、ElementUI
* 第六天：综合案例

(1)Request是从客户端向服务端发出的请求对象，

(2)Response是从服务端响应给客户端的结果对象，

(3)JSP是动态网页技术,

(4)会话技术是用来存储客户端和服务端交互所产生的数据，

(5)过滤器是用来拦截客户端的请求,

(6)监听器是用来监听特定事件,

(7)Ajax、Vue、ElementUI都是属于前端技术

这些技术都该如何来使用，后面会一个个进行详细的讲解。接下来来学习下HTTP、Tomcat和Servlet。 

## 2, HTTP

### 2.1 简介

**HTTP概念**

HyperText Transfer Protocol，超文本传输协议，规定了浏览器和服务器之间==数据传输的规则==。

* 数据传输的规则指的是请求数据和响应数据需要按照指定的格式进行传输。
* 如果想知道具体的格式，可以打开浏览器，点击`F12`打开开发者工具，点击`Network`来查看某一次请求的请求数据和响应数据具体的格式内容



> 注意:在浏览器中如果看不到上述内容，需要清除浏览器的浏览数据。chrome浏览器可以使用ctrl+shift+Del进行清除。

==所以学习HTTP主要就是学习请求和响应数据的具体格式内容。==

**HTTP协议特点**

HTTP协议有它自己的一些特点，分别是:

* 基于TCP协议: 面向连接，安全

  TCP是一种面向连接的(建立连接之前是需要经过三次握手)、可靠的、基于字节流的传输层通信协议，在数据传输方面更安全。

* 基于请求-响应模型的:一次请求对应一次响应

  请求和响应是一一对应关系

* HTTP协议是无状态协议:对于事物处理没有记忆能力。每次请求-响应都是独立的

  无状态指的是客户端发送HTTP请求给服务端之后，服务端根据请求响应数据，响应完后，不会记录任何信息。这种特性有优点也有缺点，

  * 缺点:多次请求间不能共享数据
  * 优点:速度快

  请求之间无法共享数据会引发的问题，如:

  * 京东购物，`加入购物车`和`去购物车结算`是两次请求，
  * HTTP协议的无状态特性，加入购物车请求响应结束后，并未记录加入购物车是何商品
  * 发起去购物车结算的请求后，因为无法获取哪些商品加入了购物车，会导致此次请求无法正确展示数据

  具体使用的时候，发现京东是可以正常展示数据的，原因是Java早已考虑到这个问题，并提出了使用`会话技术(Cookie、Session)`来解决这个问题。具体如何来做，后面会详细讲到。刚才提到HTTP协议是规定了请求和响应数据的格式，那具体的格式是什么呢?

### 2.2 请求数据格式

#### 2.2.1 格式介绍

请求数据总共分为三部分内容，分别是==请求行==、==请求头==、==请求体==

![1627050004221](D:/download/downloadFromMicsoft/day08-HTTP&Tomcat&Servlet/ppt/assets/1627050004221.png)

* 请求行: HTTP请求中的第一行数据，请求行包含三块内容，分别是 GET[请求方式] /[请求URL路径] HTTP/1.1[HTTP协议及版本]

  请求方式有七种,最常用的是GET和POST

* 请求头: 第二行开始，格式为key: value形式

  请求头中会包含若干个属性，常见的HTTP请求头有:

  ```
  Host: 表示请求的主机名
  User-Agent: 浏览器版本,例如Chrome浏览器的标识类似Mozilla/5.0 ...Chrome/79，IE浏览器的标识类似Mozilla/5.0 (Windows NT ...)like Gecko；
  Accept：表示浏览器能接收的资源类型，如text/*，image/*或者*/*表示所有；
  Accept-Language：表示浏览器偏好的语言，服务器可以据此返回不同语言的网页；
  Accept-Encoding：表示浏览器可以支持的压缩类型，例如gzip, deflate等。
  ```

   ==这些数据有什么用处?==

  举例说明:服务端可以根据请求头中的内容来获取客户端的相关信息，有了这些信息服务端就可以处理不同的业务需求，比如:

  * 不同浏览器解析HTML和CSS标签的结果会有不一致，所以就会导致相同的代码在不同的浏览器会出现不同的效果
  * 服务端根据客户端请求头中的数据获取到客户端的浏览器类型，就可以根据不同的浏览器设置不同的代码来达到一致的效果
  * 这就是常说的浏览器兼容问题

* 请求体: POST请求的最后一部分，存储请求参数

  ![1627050930378](D:/download/downloadFromMicsoft/day08-HTTP&Tomcat&Servlet/ppt/assets/1627050930378.png)

  如上图红线框的内容就是请求体的内容，请求体和请求头之间是有一个空行隔开。此时浏览器发送的是POST请求，为什么不能使用GET呢?这时就需要回顾GET和POST两个请求之间的区别了:

  * **GET请求请求参数在请求行中，没有请求体，POST请求请求参数在请求体中**
  * **GET请求请求参数大小有限制，POST没有**

#### 2.2.2 实例演示

把 `代码\http` 拷贝到IDEA的工作目录中，比如`D:\workspace\web`目录，

![1627278511902](D:/download/downloadFromMicsoft/day08-HTTP&Tomcat&Servlet/ppt/assets/1627278511902.png)

使用IDEA打开

![1627278583127](D:/download/downloadFromMicsoft/day08-HTTP&Tomcat&Servlet/ppt/assets/1627278583127.png)

打开后，可以点击项目中的`html\19-表单验证.html`，使用浏览器打开，通过修改页面中form表单的method属性来测试GET请求和POST请求的参数携带方式。

![1627278725007](D:/download/downloadFromMicsoft/day08-HTTP&Tomcat&Servlet/ppt/assets/1627278725007.png)



**小结**:

1. 请求数据中包含三部分内容，分别是请求行、请求头和请求体

2. POST请求数据在请求体中，GET请求数据在请求行上

### 2.3 响应数据格式

#### 2.3.1 格式介绍

响应数据总共分为三部分内容，分别是==响应行==、==响应头==、==响应体==



* 响应行：响应数据的第一行,响应行包含三块内容，分别是 HTTP/1.1[HTTP协议及版本] 200[响应状态码] ok[状态码的描述]

* 响应头：第二行开始，格式为key：value形式

  响应头中会包含若干个属性，常见的HTTP响应头有:

  ```
  Content-Type：表示该响应内容的类型，例如text/html，image/jpeg；
  Content-Length：表示该响应内容的长度（字节数）；
  Content-Encoding：表示该响应压缩算法，例如gzip；
  Cache-Control：指示客户端应如何缓存，例如max-age=300表示可以最多缓存300秒
  ```

* 响应体： 最后一部分。存放响应数据

  上图中<html>...</html>这部分内容就是响应体，它和响应头之间有一个空行隔开。

#### 2.3.2 响应状态码

参考: 资料/1.HTTP/《响应状态码.md》

关于响应状态码，先主要认识三个状态码，其余的等后期用到了再去掌握:

* 200  ok 客户端请求成功
* 404  Not Found 请求资源不存在
* 500 Internal Server Error 服务端发生不可预期的错误

#### 2.3.3 自定义服务器

在前面导入到IDEA中的http项目中，有一个Server.java类，这里面就是自定义的一个服务器代码，主要使用到的是`ServerSocket`和`Socket`

```java
package com.itheima;

import sun.misc.IOUtils;

import java.io.*;
import java.net.ServerSocket;
import java.net.Socket;
import java.nio.charset.StandardCharsets;
import java.nio.file.Files;
/*
    自定义服务器
 */
public class Server {
    public static void main(String[] args) throws IOException {
        ServerSocket ss = new ServerSocket(8080); // 监听指定端口
        System.out.println("server is running...");
        while (true){
            Socket sock = ss.accept();
            System.out.println("connected from " + sock.getRemoteSocketAddress());
            Thread t = new Handler(sock);
            t.start();
        }
    }
}

class Handler extends Thread {
    Socket sock;

    public Handler(Socket sock) {
        this.sock = sock;
    }

    public void run() {
        try (InputStream input = this.sock.getInputStream()) {
            try (OutputStream output = this.sock.getOutputStream()) {
                handle(input, output);
            }
        } catch (Exception e) {
            try {
                this.sock.close();
            } catch (IOException ioe) {
            }
            System.out.println("client disconnected.");
        }
    }

    private void handle(InputStream input, OutputStream output) throws IOException {
        BufferedReader reader = new BufferedReader(new InputStreamReader(input, StandardCharsets.UTF_8));
        BufferedWriter writer = new BufferedWriter(new OutputStreamWriter(output, StandardCharsets.UTF_8));
        // 读取HTTP请求:
        boolean requestOk = false;
        String first = reader.readLine();
        if (first.startsWith("GET / HTTP/1.")) {
            requestOk = true;
        }
        for (;;) {
            String header = reader.readLine();
            if (header.isEmpty()) { // 读取到空行时, HTTP Header读取完毕
                break;
            }
            System.out.println(header);
        }
        System.out.println(requestOk ? "Response OK" : "Response Error");
        if (!requestOk) {
            // 发送错误响应:
            writer.write("HTTP/1.0 404 Not Found\r\n");
            writer.write("Content-Length: 0\r\n");
            writer.write("\r\n");
            writer.flush();
        } else {
            // 发送成功响应:

            //读取html文件，转换为字符串
            BufferedReader br = new BufferedReader(new FileReader("http/html/a.html"));
            StringBuilder data = new StringBuilder();
            String line = null;
            while ((line = br.readLine()) != null){
                data.append(line);
            }
            br.close();
            int length = data.toString().getBytes(StandardCharsets.UTF_8).length;

            writer.write("HTTP/1.1 200 OK\r\n");
            writer.write("Connection: keep-alive\r\n");
            writer.write("Content-Type: text/html\r\n");
            writer.write("Content-Length: " + length + "\r\n");
            writer.write("\r\n"); // 空行标识Header和Body的分隔
            writer.write(data.toString());
            writer.flush();
        }
    }
}
```

上面代码，大家不需要自己写，主要通过上述代码，只需要大家了解到服务器可以使用java完成编写，是可以接受页面发送的请求和响应数据给前端浏览器的，真正用到的Web服务器，不会自己写，都是使用目前比较流行的web服务器，比如==Tomcat==

**小结**

1. 响应数据中包含三部分内容，分别是响应行、响应头和响应体

2. 掌握200，404，500这三个响应状态码所代表含义，分布是成功、所访问资源不存在和服务的错误

## 3, Tomcat

### 3.1 简介

#### 3.1.1 什么是Web服务器

Web服务器是一个应用程序（==软件==），对HTTP协议的操作进行封装，使得程序员不必直接对协议进行操作，让Web开发更加便捷。主要功能是"提供网上信息浏览服务"。

![1627058356051](D:/download/downloadFromMicsoft/day08-HTTP&Tomcat&Servlet/ppt/assets/1627058356051.png)

 Web服务器是安装在服务器端的一款软件，将来把自己写的Web项目部署到Web Tomcat服务器软件中，当Web服务器软件启动后，部署在Web服务器软件中的页面就可以直接通过浏览器来访问了。

**Web服务器软件使用步骤**

* 准备静态资源
* 下载安装Web服务器软件
* 将静态资源部署到Web服务器上
* 启动Web服务器使用浏览器访问对应的资源

上述内容在演示的时候，使用的是Apache下的Tomcat软件，至于Tomcat软件如何使用，后面会详细的讲到。而对于Web服务器来说，实现的方案有很多，Tomcat只是其中的一种，而除了Tomcat以外，还有很多优秀的Web服务器，比如:







Tomcat就是一款软件，主要是以学习如何去使用为主。具体会从以下这些方向去学习:

1. 简介: 初步认识下Tomcat

2. 基本使用: 安装、卸载、启动、关闭、配置和项目部署，这些都是对Tomcat的基本操作

3. IDEA中如何创建Maven Web项目

4. IDEA中如何使用Tomcat,后面这两个都是以后开发经常会用到的方式

首选来认识下Tomcat。

**Tomcat**

Tomcat的相关概念:

* Tomcat是Apache软件基金会一个核心项目，是一个开源免费的轻量级Web服务器，支持Servlet/JSP少量JavaEE规范。

* 概念中提到了JavaEE规范，那什么又是JavaEE规范呢?

  JavaEE: Java Enterprise Edition,Java企业版。指Java企业级开发的技术规范总和。包含13项技术规范:JDBC、JNDI、EJB、RMI、JSP、Servlet、XML、JMS、Java IDL、JTS、JTA、JavaMail、JAF。

* 因为Tomcat支持Servlet/JSP规范，所以Tomcat也被称为Web容器、Servlet容器。Servlet需要依赖Tomcat才能运行。

* Tomcat的官网: https://tomcat.apache.org/ 从官网上可以下载对应的版本进行使用。

**Tomcat的LOGO**



**小结**

通过这一节的学习，需要掌握以下内容:

1. Web服务器的作用

> 封装HTTP协议操作，简化开发
>
> 可以将Web项目部署到服务器中，对外提供网上浏览服务

2. Tomcat是一个轻量级的Web服务器，支持Servlet/JSP少量JavaEE规范，也称为Web容器，Servlet容器。

### 3.2 基本使用

Tomcat总共分两部分学习，先来学习Tomcat的基本使用，包括Tomcat的==下载、安装、卸载、启动和关闭==。

#### 3.2.1 下载

直接从官网下载



大家可以自行下载，也可以直接使用资料中已经下载好的资源，

Tomcat的软件程序  资料/2. Tomcat/apache-tomcat-8.5.68-windows-x64.zip

Tomcat的源码	资料/2. Tomcat/tomcat源码/apache-tomcat-8.5.68-src.zip

#### 3.2.2 安装

Tomcat是绿色版,直接解压即可

* 在D盘的software目录下，将`apache-tomcat-8.5.68-windows-x64.zip`进行解压缩，会得到一个`apache-tomcat-8.5.68`的目录，Tomcat就已经安装成功。

  ==注意==，Tomcat在解压缩的时候，解压所在的目录可以任意，但最好解压到一个不包含中文和空格的目录，因为后期在部署项目的时候，如果路径有中文或者空格可能会导致程序部署失败。

* 打开`apache-tomcat-8.5.68`目录就能看到如下目录结构，每个目录中包含的内容需要认识下,

  ![1627178815892](D:/download/downloadFromMicsoft/day08-HTTP&Tomcat&Servlet/ppt/assets/1627178815892.png)

  bin:目录下有两类文件，一种是以`.bat`结尾的，是Windows系统的可执行文件，一种是以`.sh`结尾的，是Linux系统的可执行文件。

  webapps:就是以后项目部署的目录

  到此，Tomcat的安装就已经完成。

#### 3.2.3 卸载

卸载比较简单，可以直接删除目录即可

#### 3.2.4 启动

双击: bin\startup.bat

![1627179006011](D:/download/downloadFromMicsoft/day08-HTTP&Tomcat&Servlet/ppt/assets/1627179006011.png)

启动后，通过浏览器访问 `http://localhost:8080`能看到Apache Tomcat的内容就说明Tomcat已经启动成功。

![1627199957728](D:/download/downloadFromMicsoft/day08-HTTP&Tomcat&Servlet/ppt/assets/1627199957728.png)

==注意==: 启动的过程中，控制台有中文乱码，需要修改conf/logging.prooperties

![1627199827589](D:/download/downloadFromMicsoft/day08-HTTP&Tomcat&Servlet/ppt/assets/1627199827589.png)

#### 3.2.5 关闭

关闭有三种方式 

* 直接x掉运行窗口:强制关闭[不建议]
* bin\shutdown.bat：正常关闭
* ctrl+c： 正常关闭

#### 3.2.6 配置

**修改端口**

* Tomcat默认的端口是8080，要想修改Tomcat启动的端口号，需要修改 conf/server.xml

![1627200509883](D:/download/downloadFromMicsoft/day08-HTTP&Tomcat&Servlet/ppt/assets/1627200509883.png)

> 注: HTTP协议默认端口号为80，如果将Tomcat端口号改为80，则将来访问Tomcat时，将不用输入端口号。

**启动时可能出现的错误**

* Tomcat的端口号取值范围是0-65535之间任意未被占用的端口，如果设置的端口号被占用，启动的时候就会包如下的错误

  ![1627200780590](D:/download/downloadFromMicsoft/day08-HTTP&Tomcat&Servlet/ppt/assets/1627200780590.png)

* Tomcat启动的时候，启动窗口一闪而过: 需要检查JAVA_HOME环境变量是否正确配置

![1627201248802](D:/download/downloadFromMicsoft/day08-HTTP&Tomcat&Servlet/ppt/assets/1627201248802.png)

#### 3.2.7 部署

* Tomcat部署项目： 将项目放置到webapps目录下，即部署完成。

  * 将 `资料/2. Tomcat/hello` 目录拷贝到Tomcat的webapps目录下

  * 通过浏览器访问`http://localhost/hello/a.html`，能看到下面的内容就说明项目已经部署成功。

  * 如果没有更改端口号，需要通过 http://localhost:8080/hello/a.html 访问

    ![1627201572748](D:/download/downloadFromMicsoft/day08-HTTP&Tomcat&Servlet/ppt/assets/1627201572748.png)

    但是呢随着项目的增大，项目中的资源也会越来越多，项目在拷贝的过程中也会越来越费时间，该如何解决呢?

* 一般JavaWeb项目会被打包称==war==包，然后将war包放到Webapps目录下，Tomcat会自动解压缩war文件

  * 将 `资料/2. Tomcat/haha.war`目录拷贝到Tomcat的webapps目录下

  * Tomcat检测到war包后会自动完成解压缩，在webapps目录下就会多一个haha目录

  * 通过浏览器访问`http://localhost/haha/a.html`，能看到下面的内容就说明项目已经部署成功。

    ![1627201868752](D:/download/downloadFromMicsoft/day08-HTTP&Tomcat&Servlet/ppt/assets/1627201868752.png)

至此，Tomcat的部署就已经完成了，至于如何获得项目对应的war包，后期会借助于IDEA工具来生成。

### 3.3 Maven创建Web项目

介绍完Tomcat的基本使用后，来学习在IDEA中如何创建Maven Web项目，学习这种方式的原因是以后Tomcat中运行的绝大多数都是Web项目，而使用Maven工具能更加简单快捷的把Web项目给创建出来，所以Maven的Web项目具体如何来构建呢?

在真正创建Maven Web项目之前，先要知道Web项目长什么样子，具体的结构是什么?

#### 3.3.1 Web项目结构

Web项目的结构分为:开发中的项目和开发完可以部署的Web项目,这两种项目的结构是不一样的，一个个来介绍下:

* Maven Web项目结构: 开发中的项目

  ![1627202865978](D:/download/downloadFromMicsoft/day08-HTTP&Tomcat&Servlet/ppt/assets/1627202865978.png)

* 开发完成部署的Web项目

  ![1627202903750](D:/download/downloadFromMicsoft/day08-HTTP&Tomcat&Servlet/ppt/assets/1627202903750.png)

  * web-inf的内容全部放入war包中去
  * 开发项目通过执行Maven打包命令==package==,可以获取到部署的Web项目目录
  * 编译后的Java字节码文件和resources的资源文件，会被放到WEB-INF下的classes目录下
  * pom.xml中依赖坐标对应的jar包，会被放入WEB-INF下的lib目录下

#### 3.3.2 创建Maven Web项目

介绍完Maven Web的项目结构后，接下来使用Maven来创建Web项目，创建方式有两种:使用骨架和不使用骨架

##### **使用骨架**

> 具体的步骤包含:
>
> 1.创建Maven项目
>
> 2.选择使用Web项目骨架
>
> 3.输入Maven项目坐标创建项目
>
> 4.确认Maven相关的配置信息后，完成项目创建
>
> 5.删除pom.xml中多余内容
>
> 6.补齐Maven Web项目缺失的目录结构

1. 创建Maven项目

   ![1627227574092](D:/download/downloadFromMicsoft/day08-HTTP&Tomcat&Servlet/ppt/assets/1627227574092.png)

2. 选择使用Web项目骨架

   ![1627227650406](D:/download/downloadFromMicsoft/day08-HTTP&Tomcat&Servlet/ppt/assets/1627227650406.png)

3. 输入Maven项目坐标创建项目

   ![1627228065007](D:/download/downloadFromMicsoft/day08-HTTP&Tomcat&Servlet/ppt/assets/1627228065007.png)

4. 确认Maven相关的配置信息后，完成项目创建

   ![1627228413280](D:/download/downloadFromMicsoft/day08-HTTP&Tomcat&Servlet/ppt/assets/1627228413280.png)

5. 删除pom.xml中多余内容，只留下面的这些内容，注意打包方式 jar和war的区别

   ![1627228584625](D:/download/downloadFromMicsoft/day08-HTTP&Tomcat&Servlet/ppt/assets/1627228584625.png)

6. 补齐Maven Web项目缺失的目录结构，默认没有java和resources目录，需要手动完成创建补齐，最终的目录结果如下

   ![](D:/download/downloadFromMicsoft/day08-HTTP&Tomcat&Servlet/ppt/assets/1627228673162.png)



##### **不使用骨架**

>具体的步骤包含:
>
>1.创建Maven项目
>
>2.选择不使用Web项目骨架
>
>3.输入Maven项目坐标创建项目
>
>4.在pom.xml设置打包方式为war
>
>5.补齐Maven Web项目缺失webapp的目录结构
>
>6.补齐Maven Web项目缺失WEB-INF/web.xml的目录结构

1. 创建Maven项目

   ![1627229111549](D:/download/downloadFromMicsoft/day08-HTTP&Tomcat&Servlet/ppt/assets/1627229111549.png)

2. 选择不使用Web项目骨架

   ![1627229137316](D:/download/downloadFromMicsoft/day08-HTTP&Tomcat&Servlet/ppt/assets/1627229137316.png)

3. 输入Maven项目坐标创建项目

   ![1627229371251](D:/download/downloadFromMicsoft/day08-HTTP&Tomcat&Servlet/ppt/assets/1627229371251.png)

4. 在pom.xml设置打包方式为war,默认是不写代表打包方式为jar

   ![1627229428161](D:/download/downloadFromMicsoft/day08-HTTP&Tomcat&Servlet/ppt/assets/1627229428161.png)

5. 补齐Maven Web项目缺失webapp的目录结构

   ![1627229584134](D:/download/downloadFromMicsoft/day08-HTTP&Tomcat&Servlet/ppt/assets/1627229584134.png)

6. 补齐Maven Web项目缺失WEB-INF/web.xml的目录结构

   ![1627229676800](D:/download/downloadFromMicsoft/day08-HTTP&Tomcat&Servlet/ppt/assets/1627229676800.png)

7. 补充完后，最终的项目结构如下:

   

   

   ![1627229478030](D:/download/downloadFromMicsoft/day08-HTTP&Tomcat&Servlet/ppt/assets/1627229478030.png)

上述两种方式，创建的web项目，都不是很全，需要手动补充内容，至于最终采用哪种方式来创建Maven Web项目，都是可以的，根据各自的喜好来选择使用即可。

**小结**

1.掌握Maven Web项目的目录结构

2.掌握使用骨架的方式创建Maven Web项目

![1627204022604](D:/download/downloadFromMicsoft/day08-HTTP&Tomcat&Servlet/ppt/assets/1627204022604.png)

> 3.掌握不使用骨架的方式创建Maven Web项目

![1627204076090](D:/download/downloadFromMicsoft/day08-HTTP&Tomcat&Servlet/ppt/assets/1627204076090.png)

### 3.4 IDEA使用Tomcat

* 手动操作：Maven Web项目创建成功后，通过Maven的package命令可以将项目打包成war包，将war文件拷贝到Tomcat的webapps目录下，启动Tomcat就可以将项目部署成功，然后通过浏览器进行访问即可。
* 然而在开发的过程中，项目中的内容会经常发生变化，如果按照上面这种方式来部署测试，是非常不方便的
* 如何在IDEA中能快速使用Tomcat呢?

在IDEA中集成使用Tomcat有两种方式，分别是==集成本地Tomcat==和==Tomcat Maven插件==

#### 3.4.1 集成本地Tomcat

体验感：初始化配置，熟练了之后还行；但是无法忍耐的是简单的修改就要重启服务器



目标: 将刚才本地安装好的Tomcat8集成到IDEA中，完成项目部署，具体的实现步骤

1. 打开添加本地Tomcat的面板

   ![1627229992900](D:/download/downloadFromMicsoft/day08-HTTP&Tomcat&Servlet/ppt/assets/1627229992900.png)

2. 指定本地Tomcat的具体路径

   ![1627230313062](D:/download/downloadFromMicsoft/day08-HTTP&Tomcat&Servlet/ppt/assets/1627230313062.png)

3. 修改Tomcat的名称，此步骤可以不改，只是让名字看起来更有意义，HTTP port中的端口也可以进行修改，比如把8080改成80

   ![1627230366658](D:/download/downloadFromMicsoft/day08-HTTP&Tomcat&Servlet/ppt/assets/1627230366658.png)

4. 将开发项目部署项目到Tomcat中

   ![1627230913259](D:/download/downloadFromMicsoft/day08-HTTP&Tomcat&Servlet/ppt/assets/1627230913259.png)

   扩展内容： xxx.war和 xxx.war exploded这两种部署项目模式的区别?

   * war模式是将WEB工程打成war包，把war包发布到Tomcat服务器上

   * war exploded模式是将WEB工程以当前文件夹的位置关系发布到Tomcat服务器上
   * war模式部署成功后，Tomcat的webapps目录下会有部署的项目内容
   * war exploded模式部署成功后，Tomcat的webapps目录下没有，而使用的是项目的target目录下的内容进行部署
   * 建议大家都选war模式进行部署，更符合项目部署的实际情况

5. 部署成功后，就可以启动项目，为了能更好的看到启动的效果，可以在webapp目录下添加a.html页面

   ![1627233265351](D:/download/downloadFromMicsoft/day08-HTTP&Tomcat&Servlet/ppt/assets/1627233265351.png)

6. 启动成功后，可以通过浏览器进行访问测试

   ![1627232743706](D:/download/downloadFromMicsoft/day08-HTTP&Tomcat&Servlet/ppt/assets/1627232743706.png)

7. 最终的注意事项

   ![1627232916624](D:/download/downloadFromMicsoft/day08-HTTP&Tomcat&Servlet/ppt/assets/1627232916624.png)

   

至此，IDEA中集成本地Tomcat进行项目部署的内容就介绍完了，整体步骤如下，大家需要按照流程进行部署操作练习。

![1627205657117](D:/download/downloadFromMicsoft/day08-HTTP&Tomcat&Servlet/ppt/assets/1627205657117.png)





实操补充：自动生成target文件夹，自动打包好文件



 #### 3.4.2 Tomcat Maven插件

在IDEA中使用本地Tomcat进行项目部署，相对来说步骤比较繁琐，所以需要一种更简便的方式来替换它，那就是直接使用Maven中的Tomcat插件来部署项目，具体的实现步骤，只需要两步，分别是:

1. 在pom.xml中添加Tomcat插件

   ```xml
   <build>
       <plugins>
       	<!--Tomcat插件 -->
           <plugin>
               <groupId>org.apache.tomcat.maven</groupId>
               <artifactId>tomcat7-maven-plugin</artifactId>
               <version>2.2</version>
           </plugin>
       </plugins>
   </build>
   ```

2. 使用Maven Helper插件快速启动项目，选中项目，右键-->Run Maven --> tomcat7:run

![1627233963315](D:/download/downloadFromMicsoft/day08-HTTP&Tomcat&Servlet/ppt/assets/1627233963315.png)

==注意:==

* 如果选中项目并右键点击后，看不到Run Maven和Debug Maven，这个时候就需要在IDEA中下载Maven Helper插件，具体的操作方式为: File --> Settings --> Plugins --> Maven Helper ---> Install,安装完后按照提示重启IDEA，就可以看到了。

![1627234184076](D:/download/downloadFromMicsoft/day08-HTTP&Tomcat&Servlet/ppt/assets/1627234184076.png)

* Maven Tomcat插件目前只有Tomcat7版本，没有更高的版本可以使用
* 使用Maven Tomcat插件，要想修改Tomcat的端口和访问路径，可以直接修改pom.xml

```xml
<build>
    <plugins>
    	<!--Tomcat插件 -->
        <plugin>
            <groupId>org.apache.tomcat.maven</groupId>
            <artifactId>tomcat7-maven-plugin</artifactId>
            <version>2.2</version>
            <configuration>
            	<port>80</port><!--访问端口号 -->
                <!--项目访问路径
					未配置访问路径: http://localhost:80/tomcat-demo2/a.html
					配置/后访问路径: http://localhost:80/a.html
					如果配置成 /hello,访问路径会变成什么?
						答案: http://localhost:80/hello/a.html
				-->
                <path>/</path>
            </configuration>
        </plugin>
    </plugins>
</build>
```

**小结**

通过这一节的学习，大家要掌握在IDEA中使用Tomcat的两种方式，集成本地Tomcat和使用Maven的Tomcat插件。后者更简单，推荐大家使用，但是如果对于Tomcat的版本有比较高的要求，**要在Tomcat7以上，这个时候就只能用前者了。**

## 感悟

本地集成：访问目录 _war 其实是在Tomcat的web 的war包下

插件：配置更加迅速，插件访问直接就是项目目录，真香！！！缺点：前端页面会出现更改不到的情况

从本地集成到插件，注意将删除地址_war



## 4， Servlet

### 4.1 简介

![1627234763207](D:/download/downloadFromMicsoft/day08-HTTP&Tomcat&Servlet/ppt/assets/1627234763207.png)

* Servlet是JavaWeb最为核心的内容，它是Java提供的一门==动态==web资源开发技术。

* 使用Servlet就可以实现，根据不同的登录用户在页面上动态显示不同内容。

* Servlet是JavaEE规范之一，其实就是一个接口，将来需要定义Servlet类实现Servlet接口，并由web服务器运行Servlet

  ![1627234972853](D:/download/downloadFromMicsoft/day08-HTTP&Tomcat&Servlet/ppt/assets/1627234972853.png)

介绍完Servlet是什么以后，接下来就按照`快速入门`->`执行流程`->`生命周期`->`体系结构`->`urlPattern配置`->`XML配置`的学习步骤，一步步完成对Servlet的知识学习，首选来通过一个入门案例来快速把Servlet用起来。



servlet作用速览

什么是servlet ,servlet的作用
1、简单来说servlet是运行在服务器上的java程序
servlet由servlet容器管理，servlet容器也叫 servlet引擎，是servlet的运行环境，给发送的请求和响应之上提供网络服务

2、servlet的作用
通俗来讲servlet专门用来接收客户端的请求，专门接收客户端的请求数据，然后调用底层service处理数据并生成结果
浏览器http请求------》tomcat服务器-------》到达servlet-----》执行doget，dopost方法----》返回数据
<1>客户端发送请求到服务器端
<2>服务器将请求信息发送至Servlet 
<3>Servlet生成响应内容并将其传给服务器。
<4>服务器将响应返回给客户端。
3、servlet里的三大作用域：

-    request(请求)：它的作用范围是一次请求和响应，是三个作用域中最小的。
-    session（会话）：它的作用比request要大一点，一次会话过程中，它的作用域就一直存在，(默认是30分钟)
-    servletcontext：它作用范围最大，作用于整个服务器中。（Application）


### 4.2 快速入门

==需求分析: 编写一个Servlet类，并使用IDEA中Tomcat插件进行部署，最终通过浏览器访问所编写的Servlet程序。==

具体的实现步骤为:

1. 创建Web项目`web-demo`，导入Servlet依赖坐标

```xml
<dependency>
    <groupId>javax.servlet</groupId>
    <artifactId>javax.servlet-api</artifactId>
    <version>3.1.0</version>
    <!--
      此处为什么需要添加该标签?
      provided指的是在编译和测试过程中有效,最后生成的war包时不会加入
       因为Tomcat的lib目录中已经有servlet-api这个jar包，如果在生成war包的时候生效就会和Tomcat中的jar包冲突，导致报错
    -->
    <scope>provided</scope>
</dependency>
```

2. 创建:定义一个类，实现Servlet接口，并重写接口中所有方法，并在service方法中输入一句话

```java
package com.itheima.web;

import javax.servlet.*;
import java.io.IOException;

public class ServletDemo1 implements Servlet {

    public void service(ServletRequest servletRequest, ServletResponse servletResponse) throws ServletException, IOException {
        System.out.println("servlet hello world~");
    }
    public void init(ServletConfig servletConfig) throws ServletException {

    }

    public ServletConfig getServletConfig() {
        return null;
    }

    public String getServletInfo() {
        return null;
    }

    public void destroy() {

    }
}
```

3. 配置:在类上使用@WebServlet注解，配置该Servlet的访问路径

```java
@WebServlet("/demo1")
```

4. 访问:启动Tomcat,浏览器中输入URL地址访问该Servlet

```
http://localhost:8080/web-demo/demo1
```

5. 器访问后，在控制台会打印`servlet hello world~` 说明servlet程序已经成功运行。

至此，Servlet的入门案例就已经完成，大家可以按照上面的步骤进行练习了。

### 4.3 执行流程

Servlet程序已经能正常运行，但是需要思考个问题: 并没有创建ServletDemo1类的对象，也没有调用对象中的service方法，为什么在控制台就打印了`servlet hello world~`这句话呢?

要想回答上述问题，就需要对Servlet的执行流程进行一个学习。

![1627236923139](D:/download/downloadFromMicsoft/day08-HTTP&Tomcat&Servlet/ppt/assets/1627236923139.png)

* 浏览器发出`http://localhost:8080/web-demo/demo1`请求，从请求中可以解析出三部分内容，分别是`localhost:8080`、`web-demo`、`demo1`
  * 根据`localhost:8080`可以找到要访问的Tomcat Web服务器
  * 根据`web-demo`可以找到部署在Tomcat服务器上的web-demo项目
  * 根据`demo1`可以找到要访问的是项目中的哪个Servlet类，根据@WebServlet后面的值进行匹配
* 找到ServletDemo1这个类后，Tomcat Web服务器就会为ServletDemo1这个类创建一个对象，然后调用对象中的service方法
  * ServletDemo1实现了Servlet接口，所以类中必然会重写service方法供Tomcat Web服务器进行调用
  * service方法中有ServletRequest和ServletResponse两个参数，ServletRequest封装的是请求数据，ServletResponse封装的是响应数据，后期可以通过这两个参数实现前后端的数据交互

**小结**

介绍完Servlet的执行流程，需要大家掌握两个问题：

1. Servlet由谁创建?Servlet方法由谁调用?

> Servlet由web服务器创建，Servlet方法由web服务器调用

2. 服务器怎么知道Servlet中一定有service方法?

> 因为自定义的Servlet,必须实现Servlet接口并复写其方法，而Servlet接口中有service方法

### 4.4 生命周期

介绍完Servlet的执行流程后，知道Servlet是由Tomcat Web服务器帮创建的。

接下来咱们再来思考一个问题:==Tomcat什么时候创建的Servlet对象?==

要想回答上述问题，就需要对Servlet的生命周期进行一个学习。

* 生命周期: 对象的生命周期指一个对象从被创建到被销毁的整个过程。

* Servlet运行在Servlet容器(web服务器)中，其生命周期由容器来管理，分为4个阶段：

  1. ==加载和实例化==：默认情况下，当Servlet第一次被访问时，由容器创建Servlet对象

  ```xml
  默认情况，Servlet会在第一次访问被容器创建，但是如果创建Servlet比较耗时的话，那么第一个访问的人等待的时间就比较长，用户的体验就比较差，那么能不能把Servlet的创建放到服务器启动的时候来创建，具体如何来配置?
  
  @WebServlet(urlPatterns = "/demo1",loadOnStartup = 1)
  loadOnstartup的取值有两类情况
  	（1）负整数:第一次访问时创建Servlet对象
  	（2）0或正整数:服务器启动时创建Servlet对象，数字越小优先级越高
  ```

  ​		**数字越小优先级越高**

  

  2. ==初始化==：在Servlet实例化之后，容器将调用Servlet的==init()==方法初始化这个对象，完成一些如加载配置文件、创建连接等初始化的工作。该方法只==调用一次==
  3. ==请求处理==：==每次==请求Servlet时，Servlet容器都会调用Servlet的==service()==方法对请求进行处理
  4. ==服务终止==：当需要释放内存或者容器关闭时，容器就会调用Servlet实例的==destroy()==方法完成资源的释放。在destroy()方法调用之后，容器会释放这个Servlet实例，该实例随后会被Java的垃圾收集器所回收

* 通过案例演示下上述的生命周期

  ```java
  package com.itheima.web;
  
  import javax.servlet.*;
  import javax.servlet.annotation.WebServlet;
  import java.io.IOException;
  /**
  * Servlet生命周期方法
  */
  @WebServlet(urlPatterns = "/demo2",loadOnStartup = 1)
  public class ServletDemo2 implements Servlet {
  
      /**
       *  初始化方法
       *  1.调用时机：默认情况下，Servlet被第一次访问时，调用
       *      * loadOnStartup: 默认为-1，修改为0或者正整数，则会在服务器启动的时候，调用
       *  2.调用次数: 1次
       * @param config
       * @throws ServletException
       */
      public void init(ServletConfig config) throws ServletException {
          System.out.println("init...");
      }
  
      /**
       * 提供服务
       * 1.调用时机:每一次Servlet被访问时，调用
       * 2.调用次数: 多次
       * @param req
       * @param res
       * @throws ServletException
       * @throws IOException
       */
      public void service(ServletRequest req, ServletResponse res) throws ServletException, IOException {
          System.out.println("servlet hello world~");
      }
  
      /**
       * 销毁方法
       * 1.调用时机：内存释放或者服务器关闭的时候，Servlet对象会被销毁，调用
       * 2.调用次数: 1次
       */
      public void destroy() {
          System.out.println("destroy...");
      }
      public ServletConfig getServletConfig() {
          return null;
      }
  
      public String getServletInfo() {
          return null;
      }
  
  
  }
  ```

  ==注意:如何才能让Servlet中的destroy方法被执行？==

  ![1627239292226](D:/download/downloadFromMicsoft/day08-HTTP&Tomcat&Servlet/ppt/assets/1627239292226.png)

在Terminal命令行中，先使用`mvn tomcat7:run`启动，然后再使用`ctrl+c`关闭tomcat

即关闭Tomcat时执行destroy的指令

**小结**

这节中需要掌握的内容是:

1. Servlet对象在什么时候被创建的?

> 默认是第一次访问的时候被创建，可以使用@WebServlet(urlPatterns = "/demo2",loadOnStartup = 1)的loadOnStartup 修改成在服务器启动的时候创建。

2. Servlet生命周期中涉及到的三个方法，这三个方法是什么?什么时候被调用?调用几次?

>涉及到三个方法，分别是 init()、service()、destroy()
>
>init方法在Servlet对象被创建的时候执行，只执行1次
>
>service方法在Servlet被访问的时候调用，每访问1次就调用1次
>
>destroy方法在Servlet对象被销毁的时候调用，只执行1次





### 4.5 方法介绍

Servlet中总共有5个方法，已经介绍过其中的三个，剩下的两个方法作用分别是什么？

先来回顾下前面讲的三个方法，分别是:

* 初始化方法，在Servlet被创建时执行，只执行一次

```java
void init(ServletConfig config) 
```

* 提供服务方法， 每次Servlet被访问，都会调用该方法

```java
void service(ServletRequest req, ServletResponse res)
```

* 销毁方法，当Servlet被销毁时，调用该方法。在内存释放或服务器关闭时销毁Servlet

```java
void destroy() 
```

剩下的两个方法是:

* 获取Servlet信息

```java
String getServletInfo() 
//该方法用来返回Servlet的相关信息，没有什么太大的用处，一般返回一个空字符串即可
public String getServletInfo() {
    return "";
}
```

* 获取ServletConfig对象

```java
ServletConfig getServletConfig()
```

ServletConfig对象，在init方法的参数中有，而Tomcat Web服务器在创建Servlet对象的时候会调用init方法，必定会传入一个ServletConfig对象，只需要将服务器传过来的ServletConfig进行返回即可。具体如何操作?

```java
package com.itheima.web;

import javax.servlet.*;
import javax.servlet.annotation.WebServlet;
import java.io.IOException;

/**
 * Servlet方法介绍
 */
@WebServlet(urlPatterns = "/demo3",loadOnStartup = 1)
public class ServletDemo3 implements Servlet {

    private ServletConfig servletConfig;
    /**
     *  初始化方法
     *  1.调用时机：默认情况下，Servlet被第一次访问时，调用
     *      * loadOnStartup: 默认为-1，修改为0或者正整数，则会在服务器启动的时候，调用
     *  2.调用次数: 1次
     * @param config
     * @throws ServletException
     */
    public void init(ServletConfig config) throws ServletException {
        this.servletConfig = config;
        System.out.println("init...");
    }
    public ServletConfig getServletConfig() {
        return servletConfig;
    }
    
    /**
     * 提供服务
     * 1.调用时机:每一次Servlet被访问时，调用
     * 2.调用次数: 多次
     * @param req
     * @param res
     * @throws ServletException
     * @throws IOException
     */
    public void service(ServletRequest req, ServletResponse res) throws ServletException, IOException {
        System.out.println("servlet hello world~");
    }

    /**
     * 销毁方法
     * 1.调用时机：内存释放或者服务器关闭的时候，Servlet对象会被销毁，调用
     * 2.调用次数: 1次
     */
    public void destroy() {
        System.out.println("destroy...");
    }
    
    public String getServletInfo() {
        return "";
    }
}
```

getServletInfo()和getServletConfig()这两个方法使用的不是很多，大家了解下。

### 4.6 体系结构

通过上面的学习，知道要想编写一个Servlet就必须要实现Servlet接口，重写接口中的5个方法，虽然已经能完成要求，但是编写起来还是比较麻烦的，因为更关注的其实只有service方法，那有没有更简单方式来创建Servlet呢?

要想解决上面的问题，需要先对Servlet的体系结构进行下了解:

![1627240593506](D:/download/downloadFromMicsoft/day08-HTTP&Tomcat&Servlet/ppt/assets/1627240593506.png)

因为将来开发B/S架构的web项目，都是针对HTTP协议，所以自定义Servlet,会通过继承==HttpServlet==

具体的编写格式如下:

```java
@WebServlet("/demo4")
public class ServletDemo4 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //TODO GET 请求方式处理逻辑
        System.out.println("get...");
    }
    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //TODO Post 请求方式处理逻辑
        System.out.println("post...");
    }
}
```

* 要想发送一个GET请求，请求该Servlet，只需要通过浏览器发送`http://localhost:8080/web-demo/demo4`,就能看到doGet方法被执行了，默认就是GET请求
* 要想发送一个POST请求，请求该Servlet，单单通过浏览器是无法实现的，这个时候就需要编写一个form表单来发送请求，在webapp下创建一个`a.html`页面，内容如下:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <form action="/web-demo/demo4" method="post">
        <input name="username"/><input type="submit"/>
    </form>
</body>
</html>
```

启动测试，即可看到doPost方法被执行了。

Servlet的简化编写就介绍完了，接着需要思考两个问题:

1. HttpServlet中为什么要根据请求方式的不同，调用不同的方法?
2. 如何调用?

针对问题一，需要回顾之前的知识点==前端发送GET和POST请求的时候，参数的位置不一致，**GET请求参数在请求行中，POST请求参数在请求体中**==，为了能处理不同的请求方式，得在service方法中进行判断，然后写不同的业务处理，这样能实现，但是每个Servlet类中都将有相似的代码，针对这个问题，有什么可以优化的策略么?

```java
package com.itheima.web;

import javax.servlet.*;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;


@WebServlet("/demo5")
public class ServletDemo5 implements Servlet {

    public void init(ServletConfig config) throws ServletException {

    }

    public ServletConfig getServletConfig() {
        return null;
    }

    public void service(ServletRequest req, ServletResponse res) throws ServletException, IOException {
        //如何调用?
        //获取请求方式，根据不同的请求方式进行不同的业务处理
        HttpServletRequest request = (HttpServletRequest)req;
       //1. 获取请求方式
        String method = request.getMethod();
        //2. 判断
        if("GET".equals(method)){
            // get方式的处理逻辑
        }else if("POST".equals(method)){
            // post方式的处理逻辑
        }
    }

    public String getServletInfo() {
        return null;
    }

    public void destroy() {

    }
}

```

要解决上述问题，可以对Servlet接口进行继承封装，来简化代码开发。

```java
package com.itheima.web;

import javax.servlet.*;
import javax.servlet.http.HttpServletRequest;
import java.io.IOException;

public class MyHttpServlet implements Servlet {
    public void init(ServletConfig config) throws ServletException {

    }

    public ServletConfig getServletConfig() {
        return null;
    }

    public void service(ServletRequest req, ServletResponse res) throws ServletException, IOException {
        HttpServletRequest request = (HttpServletRequest)req;
        //1. 获取请求方式
        String method = request.getMethod();
        //2. 判断
        if("GET".equals(method)){
            // get方式的处理逻辑
            doGet(req,res);
        }else if("POST".equals(method)){
            // post方式的处理逻辑
            doPost(req,res);
        }
    }

    protected void doPost(ServletRequest req, ServletResponse res) {
    }

    protected void doGet(ServletRequest req, ServletResponse res) {
    }

    public String getServletInfo() {
        return null;
    }

    public void destroy() {

    }
}

```

有了MyHttpServlet这个类，以后再编写Servlet类的时候，只需要继承MyHttpServlet，重写父类中的doGet和doPost方法，就可以用来处理GET和POST请求的业务逻辑。接下来，可以把ServletDemo5代码进行改造

```java
@WebServlet("/demo5")
public class ServletDemo5 extends MyHttpServlet {

    @Override
    protected void doGet(ServletRequest req, ServletResponse res) {
        System.out.println("get...");
    }

    @Override
    protected void doPost(ServletRequest req, ServletResponse res) {
        System.out.println("post...");
    }
}

```

将来页面发送的是GET请求，则会进入到doGet方法中进行执行，如果是POST请求，则进入到doPost方法。这样代码在编写的时候就相对来说更加简单快捷。

类似MyHttpServlet这样的类Servlet中已经为提供好了，就是HttpServlet,翻开源码，大家可以搜索`service()`方法，你会发现HttpServlet做的事更多，不仅可以处理GET和POST还可以处理其他五种请求方式。

```java
protected void service(HttpServletRequest req, HttpServletResponse resp)
        throws ServletException, IOException
    {
        String method = req.getMethod();

        if (method.equals(METHOD_GET)) {
            long lastModified = getLastModified(req);
            if (lastModified == -1) {
                // servlet doesn't support if-modified-since, no reason
                // to go through further expensive logic
                doGet(req, resp);
            } else {
                long ifModifiedSince = req.getDateHeader(HEADER_IFMODSINCE);
                if (ifModifiedSince < lastModified) {
                    // If the servlet mod time is later, call doGet()
                    // Round down to the nearest second for a proper compare
                    // A ifModifiedSince of -1 will always be less
                    maybeSetLastModified(resp, lastModified);
                    doGet(req, resp);
                } else {
                    resp.setStatus(HttpServletResponse.SC_NOT_MODIFIED);
                }
            }

        } else if (method.equals(METHOD_HEAD)) {
            long lastModified = getLastModified(req);
            maybeSetLastModified(resp, lastModified);
            doHead(req, resp);

        } else if (method.equals(METHOD_POST)) {
            doPost(req, resp);
            
        } else if (method.equals(METHOD_PUT)) {
            doPut(req, resp);
            
        } else if (method.equals(METHOD_DELETE)) {
            doDelete(req, resp);
            
        } else if (method.equals(METHOD_OPTIONS)) {
            doOptions(req,resp);
            
        } else if (method.equals(METHOD_TRACE)) {
            doTrace(req,resp);
            
        } else {
            //
            // Note that this means NO servlet supports whatever
            // method was requested, anywhere on this server.
            //

            String errMsg = lStrings.getString("http.method_not_implemented");
            Object[] errArgs = new Object[1];
            errArgs[0] = method;
            errMsg = MessageFormat.format(errMsg, errArgs);
            
            resp.sendError(HttpServletResponse.SC_NOT_IMPLEMENTED, errMsg);
        }
    }
```

**小结**

通过这一节的学习，要掌握:

1. HttpServlet的使用步骤

> 继承HttpServlet
>
> 重写doGet和doPost方法

2. HttpServlet原理

> 获取请求方式，并根据不同的请求方式，调用不同的doXxx方法

### 4.7 urlPattern配置

Servlet类编写好后，要想被访问到，就需要配置其访问路径（==urlPattern==）

* 一个Servlet,可以配置多个urlPattern

  ![1627272805178](D:/download/downloadFromMicsoft/day08-HTTP&Tomcat&Servlet/ppt/assets/1627272805178.png)

  ```java
  package com.itheima.web;
  
  import javax.servlet.ServletRequest;
  import javax.servlet.ServletResponse;
  import javax.servlet.annotation.WebServlet;
  
  /**
  * urlPattern: 一个Servlet可以配置多个访问路径
  */
  @WebServlet(urlPatterns = {"/demo7","/demo8"})
  public class ServletDemo7 extends MyHttpServlet {
  
      @Override
      protected void doGet(ServletRequest req, ServletResponse res) {
          
          System.out.println("demo7 get...");
      }
      @Override
      protected void doPost(ServletRequest req, ServletResponse res) {
      }
  }
  ```

  在浏览器上输入`http://localhost:8080/web-demo/demo7`,`http://localhost:8080/web-demo/demo8`这两个地址都能访问到ServletDemo7的doGet方法。

* ==urlPattern配置规则==

  

  精确匹配

  ![1627273174144](D:/download/downloadFromMicsoft/day08-HTTP&Tomcat&Servlet/ppt/assets/1627273174144.png)

  ```java
  /**
   * UrlPattern:
   * * 精确匹配
   */
  @WebServlet(urlPatterns = "/user/select")
  public class ServletDemo8 extends MyHttpServlet {
  
      @Override
      protected void doGet(ServletRequest req, ServletResponse res) {
  
          System.out.println("demo8 get...");
      }
      @Override
      protected void doPost(ServletRequest req, ServletResponse res) {
      }
  }
  ```

  访问路径`http://localhost:8080/web-demo/user/select`

  目录匹配

  ![1627273184095](D:/download/downloadFromMicsoft/day08-HTTP&Tomcat&Servlet/ppt/assets/1627273184095.png)

  ```java
  package com.itheima.web;
  
  import javax.servlet.ServletRequest;
  import javax.servlet.ServletResponse;
  import javax.servlet.annotation.WebServlet;
  
  /**
   * UrlPattern:
   * * 目录匹配: /user/*
   */
  @WebServlet(urlPatterns = "/user/*")
  public class ServletDemo9 extends MyHttpServlet {
  
      @Override
      protected void doGet(ServletRequest req, ServletResponse res) {
  
          System.out.println("demo9 get...");
      }
      @Override
      protected void doPost(ServletRequest req, ServletResponse res) {
      }
  }
  ```

  访问路径`http://localhost:8080/web-demo/user/任意`

  ==思考:==

  1. 访问路径`http://localhost:8080/web-demo/user`是否能访问到demo9的doGet方法?
  2. 访问路径`http://localhost:8080/web-demo/user/a/b`是否能访问到demo9的doGet方法?
  3. 访问路径`http://localhost:8080/web-demo/user/select`是否能访问到demo9还是demo8的doGet方法?

  答案是: 能、能、demo8，进而可以得到的结论是`/user/*`中的`/*`代表的是零或多个层级访问目录同时精确匹配优先级要高于目录匹配。

  扩展名匹配

  ![1627273194118](D:/download/downloadFromMicsoft/day08-HTTP&Tomcat&Servlet/ppt/assets/1627273194118.png)

  ```java
  package com.itheima.web;
  
  import javax.servlet.ServletRequest;
  import javax.servlet.ServletResponse;
  import javax.servlet.annotation.WebServlet;
  
  /**
   * UrlPattern:
   * * 扩展名匹配: *.do
   */
  @WebServlet(urlPatterns = "*.do")
  public class ServletDemo10 extends MyHttpServlet {
  
      @Override
      protected void doGet(ServletRequest req, ServletResponse res) {
  
          System.out.println("demo10 get...");
      }
      @Override
      protected void doPost(ServletRequest req, ServletResponse res) {
      }
  }
  ```

  访问路径`http://localhost:8080/web-demo/任意.do`

  ==注意==:

  1. 如果路径配置的不是扩展名，那么在路径的前面就必须要加`/`否则会报错

  ![1627274483755](D:/download/downloadFromMicsoft/day08-HTTP&Tomcat&Servlet/ppt/assets/1627274483755.png)

  2. 如果路径配置的是`*.do`,那么在*.do的前面不能加`/`,否则会报错

  ![1627274368245](D:/download/downloadFromMicsoft/day08-HTTP&Tomcat&Servlet/ppt/assets/1627274368245.png)

  

  任意匹配

  ![1627273201370](D:/download/downloadFromMicsoft/day08-HTTP&Tomcat&Servlet/ppt/assets/1627273201370.png)

  ```java
  package com.itheima.web;
  
  import javax.servlet.ServletRequest;
  import javax.servlet.ServletResponse;
  import javax.servlet.annotation.WebServlet;
  
  /**
   * UrlPattern:
   * * 任意匹配： /
   */
  @WebServlet(urlPatterns = "/")
  public class ServletDemo11 extends MyHttpServlet {
  
      @Override
      protected void doGet(ServletRequest req, ServletResponse res) {
  
          System.out.println("demo11 get...");
      }
      @Override
      protected void doPost(ServletRequest req, ServletResponse res) {
      }
  }
  ```

  访问路径`http://localhost:8080/demo-web/任意`

  ```java
  package com.itheima.web;
  
  import javax.servlet.ServletRequest;
  import javax.servlet.ServletResponse;
  import javax.servlet.annotation.WebServlet;
  
  /**
   * UrlPattern:
   * * 任意匹配： /*
   */
  @WebServlet(urlPatterns = "/*")
  public class ServletDemo12 extends MyHttpServlet {
  
      @Override
      protected void doGet(ServletRequest req, ServletResponse res) {
  
          System.out.println("demo12 get...");
      }
      @Override
      protected void doPost(ServletRequest req, ServletResponse res) {
      }
  }
  
  ```

  访问路径`http://localhost:8080/demo-web/任意

  ==注意:==`/`和`/*`的区别?

  1. 当的项目中的Servlet配置了 "/",会覆盖掉tomcat中的DefaultServlet,当其他的url-pattern都匹配不上时都会走这个Servlet

  2. 当的项目中配置了"/*",意味着匹配任意访问路径

  3. DefaultServlet是用来处理静态资源，如果配置了"/"会把默认的覆盖掉，就会引发请求静态资源的时候没有走默认的而是走了自定义的Servlet类，最终导致静态资源不能被访问

**小结**

1. urlPattern总共有四种配置方式，分别是精确匹配、目录匹配、扩展名匹配、任意匹配

2. 五种配置的优先级为 精确匹配 > 目录匹配> 扩展名匹配 > /* > / ,无需记，以最终运行结果为准。

### 4.8 XML配置

前面对应Servlet的配置，都使用的是@WebServlet,这个是Servlet从3.0版本后开始支持注解配置，3.0版本前只支持XML配置文件的配置方法。

对于XML的配置步骤有两步:

* 编写Servlet类

```java
package com.itheima.web;

import javax.servlet.ServletRequest;
import javax.servlet.ServletResponse;
import javax.servlet.annotation.WebServlet;

public class ServletDemo13 extends MyHttpServlet {

    @Override
    protected void doGet(ServletRequest req, ServletResponse res) {

        System.out.println("demo13 get...");
    }
    @Override
    protected void doPost(ServletRequest req, ServletResponse res) {
    }
}
```

* 在web.xml中配置该Servlet

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">
    
    
    
    <!-- 
        Servlet 全类名
    -->
    <servlet>
        <!-- servlet的名称，名字任意-->
        <servlet-name>demo13</servlet-name>
        <!--servlet的类全名-->
        <servlet-class>com.itheima.web.ServletDemo13</servlet-class>
    </servlet>

    <!-- 
        Servlet 访问路径
    -->
    <servlet-mapping>
        <!-- servlet的名称，要和上面的名称一致-->
        <servlet-name>demo13</servlet-name>
        <!-- servlet的访问路径-->
        <url-pattern>/demo13</url-pattern>
    </servlet-mapping>
</web-app>
```

这种配置方式和注解比起来，确认麻烦很多，所以建议大家使用注解来开发。但是大家要认识上面这种配置方式，因为并不是所有的项目都是基于注解开发的。

# Request&Response

**今日目标**

>* 掌握Request对象的概念与使用
>* 掌握Response对象的概念与使用
>* 能够完成用户登录注册案例的实现
>* 能够完成SqlSessionFactory工具类的抽取

## 1，Request和Response的概述

==Request是请求对象，Response是响应对象。==这两个对象在使用Servlet的时候有看到：![1628735216156](D:/download/downloadFromMicsoft/day09-Request&Response/ppt/assets/1628735216156.png)

此时，就需要思考一个问题request和response这两个参数的作用是什么?

![1628735746602](D:/download/downloadFromMicsoft/day09-Request&Response/ppt/assets/1628735746602.png)

* request:==获取==请求数据
  * 浏览器会发送HTTP请求到后台服务器[Tomcat]
  * HTTP的请求中会包含很多请求数据[请求行+请求头+请求体]
  * 后台服务器[Tomcat]会对HTTP请求中的数据进行解析并把解析结果存入到一个对象中
  * 所存入的对象即为request对象，所以可以从request对象中获取请求的相关参数
  * 获取到数据后就可以继续后续的业务，比如获取用户名和密码就可以实现登录操作的相关业务
* response:==设置==响应数据
  * 业务处理完后，后台就需要给前端返回业务处理的结果即响应数据
  * 把响应数据封装到response对象中
  * 后台服务器[Tomcat]会解析response对象,按照[响应行+响应头+响应体]格式拼接结果
  * 浏览器最终解析结果，把内容展示在浏览器给用户浏览

对于上述所讲的内容，通过一个案例来初步体验下request和response对象的使用。

```java
@WebServlet("/demo3")
public class ServletDemo3 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //使用request对象 获取请求数据
        String name = request.getParameter("name");//url?name=zhangsan

        //使用response对象 设置响应数据
        response.setHeader("content-type","text/html;charset=utf-8");
        response.getWriter().write("<h1>"+name+",欢迎您！</h1>");
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        System.out.println("Post...");
    }
}
```

启动成功后就可以通过浏览器来访问，并且根据传入参数的不同就可以在页面上展示不同的内容:

![1628738273049](D:/download/downloadFromMicsoft/day09-Request&Response/ppt/assets/1628738273049.png)

**小结**

在这节中，主要认识了下request对象和reponse对象:

* request对象是用来封装请求数据的对象
* response对象是用来封装响应数据的对象

目前只知道这两个对象是用来干什么的，那么它们具体是如何实现的，就需要继续深入的学习。接下来，就先从Request对象来学习,主要学习下面这些内容:

* request继承体系

* request获取请求参数
* request请求转发

## 2，Request对象

### 2.1 Request继承体系

在学习这节内容之前，先思考一个问题，前面在介绍Request和Reponse对象的时候，比较细心的同学可能已经发现：

* 当的Servlet类实现的是Servlet接口的时候，service方法中的参数是ServletRequest和ServletResponse
* 当的Servlet类继承的是HttpServlet类的时候，doGet和doPost方法中的参数就变成HttpServletRequest和HttpServletReponse

那么，

* ServletRequest和HttpServletRequest的关系是什么?
* request对象是有谁来创建的?
* request提供了哪些API,这些API从哪里查?

首先，先来看下Request的继承体系:

![1628740441008](D:/download/downloadFromMicsoft/day09-Request&Response/ppt/assets/1628740441008.png)

从上图中可以看出，ServletRequest和HttpServletRequest都是Java提供的，所以可以打开JavaEE提供的API文档[参考: 资料/JavaEE7-api.chm],打开后可以看到:

![1628741839475](D:/download/downloadFromMicsoft/day09-Request&Response/ppt/assets/1628741839475.png)

所以ServletRequest和HttpServletRequest是继承关系，并且两个都是接口，接口是无法创建对象，这个时候就引发了下面这个问题:

![1628742224589](D:/download/downloadFromMicsoft/day09-Request&Response/ppt/assets/1628742224589.png)

这个时候，就需要用到Request继承体系中的`RequestFacade`:

* 该类实现了HttpServletRequest接口，也间接实现了ServletRequest接口。
* Servlet类中的service方法、doGet方法或者是doPost方法最终都是由Web服务器[Tomcat]来调用的，所以Tomcat提供了方法参数接口的具体实现类，并完成了对象的创建
* 要想了解RequestFacade中都提供了哪些方法，可以直接查看JavaEE的API文档中关于ServletRequest和HttpServletRequest的接口文档，因为RequestFacade实现了其接口就需要重写接口中的方法

对于上述结论，要想验证，可以编写一个Servlet，在方法中把request对象打印下，就能看到最终的对象是不是RequestFacade,代码如下:

```java
@WebServlet("/demo2")
public class ServletDemo2 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        System.out.println(request);
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
    }
}
```

启动服务器，运行访问`http://localhost:8080/request-demo/demo2`,得到运行结果:

![1628743040046](D:/download/downloadFromMicsoft/day09-Request&Response/ppt/assets/1628743040046.png)

**小结**

* Request的继承体系为ServletRequest-->HttpServletRequest-->RequestFacade
* Tomcat需要解析请求数据，封装为request对象,并且创建request对象传递到service方法
* 使用request对象，可以查阅JavaEE API文档的HttpServletRequest接口中方法说明

### 2.2 Request获取请求数据

HTTP请求数据总共分为三部分内容，分别是==请求行、请求头、请求体==，对于这三部分内容的数据，分别该如何获取，首先先来学习请求行数据如何获取?

#### 2.2.1 获取请求行数据

请求行包含三块内容，分别是`请求方式`、`请求资源路径`、`HTTP协议及版本`

![1628748240075](D:/download/downloadFromMicsoft/day09-Request&Response/ppt/assets/1628748240075.png)

对于这三部分内容，request对象都提供了对应的API方法来获取，具体如下:

* 获取请求方式: `GET`

```
String getMethod()
```

* 获取虚拟目录(项目访问路径): `/request-demo`

```
String getContextPath()
```

* 获取URL(统一资源定位符): `http://localhost:8080/request-demo/req1`

```
StringBuffer getRequestURL()
```

* 获取URI(统一资源标识符): `/request-demo/req1`

```
String getRequestURI()
```

URL是URI的子集，即URI长度更短

* 获取请求参数(GET方式): `username=zhangsan&password=123`

```
String getQueryString()
```

介绍完上述方法后，咱们通过代码把上述方法都使用下:

```java
/**
 * request 获取请求数据
 */
@WebServlet("/req1")
public class RequestDemo1 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        // String getMethod()：获取请求方式： GET
        String method = req.getMethod();
        System.out.println(method);//GET
        // String getContextPath()：获取虚拟目录(项目访问路径)：/request-demo
        String contextPath = req.getContextPath();
        System.out.println(contextPath);
        // StringBuffer getRequestURL(): 获取URL(统一资源定位符)：http://localhost:8080/request-demo/req1
        StringBuffer url = req.getRequestURL();
        System.out.println(url.toString());
        // String getRequestURI()：获取URI(统一资源标识符)： /request-demo/req1
        String uri = req.getRequestURI();
        System.out.println(uri);
        // String getQueryString()：获取请求参数（GET方式）： username=zhangsan
        String queryString = req.getQueryString();
        System.out.println(queryString);
    }
    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    }
}
```

启动服务器，访问`http://localhost:8080/request-demo/req1?username=zhangsan&passwrod=123`，获取的结果如下:

![1628762794935](D:/download/downloadFromMicsoft/day09-Request&Response/ppt/assets/1628762794935.png)

#### 2.2.2 获取请求头数据

对于请求头的数据，格式为`key: value`如下:

![1628768652535](D:/download/downloadFromMicsoft/day09-Request&Response/ppt/assets/1628768652535.png)

所以根据请求头名称获取对应值的方法为:

```
String getHeader(String name)
```

接下来，在代码中如果想要获取客户端浏览器的版本信息，则可以使用

```java
/**
 * request 获取请求数据
 */
@WebServlet("/req1")
public class RequestDemo1 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //获取请求头: user-agent: 浏览器的版本信息
        String agent = req.getHeader("user-agent");
		System.out.println(agent);
    }
    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    }
}

```

重新启动服务器后，`http://localhost:8080/request-demo/req1?username=zhangsan&passwrod=123`，获取的结果如下:

![1628769145524](D:/download/downloadFromMicsoft/day09-Request&Response/ppt/assets/1628769145524.png)

#### 2.2.3 获取请求体数据

浏览器在发送GET请求的时候是没有请求体的，所以需要把请求方式变更为POST，请求体中的数据格式如下:

![1628768665185](D:/download/downloadFromMicsoft/day09-Request&Response/ppt/assets/1628768665185.png)

对于请求体中的数据，Request对象提供了如下两种方式来获取其中的数据，分别是:

* 获取字节输入流，如果前端发送的是字节数据，比如传递的是文件数据，则使用该方法

```
ServletInputStream getInputStream()
该方法可以获取字节
```

* 获取字符输入流，如果前端发送的是纯文本数据，则使用该方法

```
BufferedReader getReader()
```

接下来，大家需要思考，要想获取到请求体的内容该如何实现?

>具体实现的步骤如下:
>
>1.准备一个页面，在页面中添加form表单,用来发送post请求
>
>2.在Servlet的doPost方法中获取请求体数据
>
>3.在doPost方法中使用request的getReader()或者getInputStream()来获取
>
>4.访问测试

1. 在项目的webapp目录下添加一个html页面，名称为：`req.html`

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<!-- 
    action:form表单提交的请求地址
    method:请求方式，指定为post
-->
<form action="/request-demo/req1" method="post">
    <input type="text" name="username">
    <input type="password" name="password">
    <input type="submit">
</form>
</body>
</html>
```

2. 在Servlet的doPost方法中获取数据

```java
/**
 * request 获取请求数据
 */
@WebServlet("/req1")
public class RequestDemo1 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    }
    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //在此处获取请求体中的数据
    }
}
```

3. 调用getReader()或者getInputStream()方法，因为目前前端传递的是纯文本数据，所以采用getReader()方法来获取

```java
/**
 * request 获取请求数据
 */
@WebServlet("/req1")
public class RequestDemo1 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    }
    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
         //获取post 请求体：请求参数
        //1. 获取字符输入流
        BufferedReader br = req.getReader();
        //2. 读取数据
        String line = br.readLine();
        System.out.println(line);
    }
}
```

==注意==

BufferedReader流是通过request对象来获取的，当请求完成后request对象就会被销毁，request对象被销毁后，BufferedReader流就会自动关闭，所以此处就不需要手动关闭流了。

4. 启动服务器，通过浏览器访问`http://localhost:8080/request-demo/req.html`

![1628770516387](D:/download/downloadFromMicsoft/day09-Request&Response/ppt/assets/1628770516387.png)

点击`提交`按钮后，就可以在控制台看到前端所发送的请求数据

![1628770585480](D:/download/downloadFromMicsoft/day09-Request&Response/ppt/assets/1628770585480.png)

**小结**

HTTP请求数据中包含了`请求行`、`请求头`和`请求体`，针对这三部分内容，Request对象都提供了对应的API方法来获取对应的值:

* 请求行
  * getMethod()获取请求方式
  * getContextPath()获取项目访问路径
  * getRequestURL()获取请求URL
  * getRequestURI()获取请求URI
  * getQueryString()获取GET请求方式的请求参数
* 请求头
  * getHeader(String name)根据请求头名称获取其对应的值
* 请求体
  * 注意: ==浏览器发送的POST请求才有请求体==
  * 如果是纯文本数据:getReader()
  * 如果是字节数据如文件数据:getInputStream()

#### 2.2.4 获取请求参数的通用方式

在学习下面内容之前，先提出两个问题:

* 什么是请求参数?
* 请求参数和请求数据的关系是什么?

1.什么是请求参数?

为了能更好的回答上述两个问题，拿用户登录的例子来说明

1.1 想要登录网址，需要进入登录页面

1.2 在登录页面输入用户名和密码

1.3 将用户名和密码提交到后台

1.4 后台校验用户名和密码是否正确

1.5 如果正确，则正常登录，如果不正确，则提示用户名或密码错误

上述例子中，用户名和密码其实就是所说的请求参数。

2.什么是请求数据?

请求数据则是包含请求行、请求头和请求体的所有数据

3.请求参数和请求数据的关系是什么?

3.1 请求参数是请求数据中的部分内容

3.2 如果是GET请求，请求参数在请求行中

3.3 如果是POST请求，请求参数一般在请求体中

对于请求参数的获取,常用的有以下两种:

* GET方式:

```
String getQueryString()
```

* POST方式:

```
BufferedReader getReader();
```

有了上述的知识储备，来实现一个案例需求:

（1）发送一个GET请求并携带用户名，后台接收后打印到控制台

（2）发送一个POST请求并携带用户名，后台接收后打印到控制台

此处大家需要注意的是GET请求和POST请求接收参数的方式不一样，具体实现的代码如下:

```java
@WebServlet("/req1")
public class RequestDemo1 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {

        String result = req.getQueryString();
        System.out.println(result);

    }
    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        BufferedReader br = req.getReader();
        String result = br.readLine();
        System.out.println(result);
    }
}
```

* 对于上述的代码，会存在什么问题呢?

![1628776252445](D:/download/downloadFromMicsoft/day09-Request&Response/ppt/assets/1628776252445.png)

* 如何解决上述重复代码的问题呢?

![1628776433318](D:/download/downloadFromMicsoft/day09-Request&Response/ppt/assets/1628776433318.png)

当然，也可以在doGet中调用doPost,在doPost中完成参数的获取和打印,另外需要注意的是，doGet和doPost方法都必须存在，不能删除任意一个。

==GET请求和POST请求获取请求参数的方式不一样，在获取请求参数这块该如何实现呢?==

要想实现，就需要==思考==:

GET请求方式和POST请求方式区别主要在于获取请求参数的方式不一样，是否可以提供一种==统一==获取请求参数的方式，从而==统一==doGet和doPost方法内的代码?

解决方案一:

```java
@WebServlet("/req1")
public class RequestDemo1 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //获取请求方式
        String method = req.getMethod();
        //获取请求参数
        String params = "";
        if("GET".equals(method)){
            params = req.getQueryString();
        }else if("POST".equals(method)){
            BufferedReader reader = req.getReader();
            params = reader.readLine();
        }
        //将请求参数进行打印控制台
        System.out.println(params);
      
    }
    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        this.doGet(req,resp);
    }
}
```

使用request的getMethod()来获取请求方式，根据请求方式的不同分别获取请求参数值，这样就可以解决上述问题，但是以后每个Servlet都需要这样写代码，实现起来比较麻烦，这种方案不采用

解决方案二:

request对象已经将上述获取请求参数的方法进行了封装，并且request提供的方法实现的功能更强大，以后只需要调用request提供的方法即可，在request的方法中都实现了哪些操作?

(1)根据不同的请求方式获取请求参数，获取的内容如下:

![1628778931277](D:/download/downloadFromMicsoft/day09-Request&Response/ppt/assets/1628778931277.png)

(2)把获取到的内容进行分割，内容如下:

![1628779067793](D:/download/downloadFromMicsoft/day09-Request&Response/ppt/assets/1628779067793.png)

(3)把分割后端数据，存入到一个Map集合中:

![1628779368501](D:/download/downloadFromMicsoft/day09-Request&Response/ppt/assets/1628779368501.png)

**注意**:因为参数的值可能是一个，也可能有多个，所以Map的值的类型为String数组。

基于上述理论，request对象为提供了如下方法:

* 获取所有参数Map集合

```
Map<String,String[]> getParameterMap()
```

* 根据名称获取参数值（数组）

```
String[] getParameterValues(String name)
```

* 根据名称获取参数值(单个值)

```
String getParameter(String name)
```

接下来，通过案例来把上述的三个方法进行实例演示:

1.修改req.html页面，添加爱好选项，爱好可以同时选多个

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<form action="/request-demo/req2" method="get">
    <input type="text" name="username"><br>
    <input type="password" name="password"><br>
    <input type="checkbox" name="hobby" value="1"> 游泳
    <input type="checkbox" name="hobby" value="2"> 爬山 <br>
    <input type="submit">

</form>
</body>
</html>
```

![1628780937599](D:/download/downloadFromMicsoft/day09-Request&Response/ppt/assets/1628780937599.png)

2.在Servlet代码中获取页面传递GET请求的参数值

 2.1获取GET方式的所有请求参数

```java
/**
 * request 通用方式获取请求参数
 */
@WebServlet("/req2")
public class RequestDemo2 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //GET请求逻辑
        System.out.println("get....");
        //1. 获取所有参数的Map集合
        Map<String, String[]> map = req.getParameterMap();
        for (String key : map.keySet()) {
            // username:zhangsan lisi
            System.out.print(key+":");

            //获取值
            String[] values = map.get(key);
            for (String value : values) {
                System.out.print(value + " ");
            }

            System.out.println();
        }
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    }
}
```

获取的结果为:

![1628780965283](D:/download/downloadFromMicsoft/day09-Request&Response/ppt/assets/1628780965283.png)

 2.2获取GET请求参数中的爱好，结果是数组值

```java
/**
 * request 通用方式获取请求参数
 */
@WebServlet("/req2")
public class RequestDemo2 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //GET请求逻辑
        //...
        System.out.println("------------");
        String[] hobbies = req.getParameterValues("hobby");
        for (String hobby : hobbies) {
            System.out.println(hobby);
        }
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    }
}
```

获取的结果为:

![1628781031437](D:/download/downloadFromMicsoft/day09-Request&Response/ppt/assets/1628781031437.png)

 2.3获取GET请求参数中的用户名和密码，结果是单个值

```java
/**
 * request 通用方式获取请求参数
 */
@WebServlet("/req2")
public class RequestDemo2 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //GET请求逻辑
        //...
        String username = req.getParameter("username");
        String password = req.getParameter("password");
        System.out.println(username);
        System.out.println(password);
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    }
}
```

获取的结果为:

![1628781176434](D:/download/downloadFromMicsoft/day09-Request&Response/ppt/assets/1628781176434.png)

3.在Servlet代码中获取页面传递POST请求的参数值

 3.1将req.html页面form表单的提交方式改成post

 3.2将doGet方法中的内容复制到doPost方法中即可

**小结**

* req.getParameter()方法使用的频率会比较高

* 以后再写代码的时候，就只需要按照如下格式来编写:

```
public class RequestDemo1 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
       //采用request提供的获取请求参数的通用方式来获取请求参数
       //编写其他的业务代码...
    }
    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        this.doGet(req,resp);
    }
}
```

### 2.3 IDEA快速创建Servlet

使用通用方式获取请求参数后，屏蔽了GET和POST的请求方式代码的不同，则代码可以定义如下格式:

![1628781419752](D:/download/downloadFromMicsoft/day09-Request&Response/ppt/assets/1628781419752.png)

由于格式固定，所以可以使用IDEA提供的模板来制作一个Servlet的模板，这样后期在创建Servlet的时候就会更高效，具体如何实现:

(1)按照自己的需求，修改Servlet创建的模板内容

![1628781545912](D:/download/downloadFromMicsoft/day09-Request&Response/ppt/assets/1628781545912.png)

（2）使用servlet模板创建Servlet类

![1628782117420](D:/download/downloadFromMicsoft/day09-Request&Response/ppt/assets/1628782117420.png)

### 2.4 请求参数中文乱码问题

问题展示:

(1)将req.html页面的请求方式修改为get

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<form action="/request-demo/req2" method="get">
    <input type="text" name="username"><br>
    <input type="password" name="password"><br>
    <input type="checkbox" name="hobby" value="1"> 游泳
    <input type="checkbox" name="hobby" value="2"> 爬山 <br>
    <input type="submit">

</form>
</body>
</html>
```

(2)在Servlet方法中获取参数，并打印

```java
/**
 * 中文乱码问题解决方案
 */
@WebServlet("/req4")
public class RequestDemo4 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
       //1. 获取username
       String username = request.getParameter("username");
       System.out.println(username);
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doGet(request, response);
    }
}
```

（3）启动服务器，页面上输入中文参数

![1628784323297](D:/download/downloadFromMicsoft/day09-Request&Response/ppt/assets/1628784323297.png)

（4）查看控制台打印内容

![1628784356157](D:/download/downloadFromMicsoft/day09-Request&Response/ppt/assets/1628784356157.png)

（5）把req.html页面的请求方式改成post,再次发送请求和中文参数

![1628784425182](D:/download/downloadFromMicsoft/day09-Request&Response/ppt/assets/1628784425182.png)

（6）查看控制台打印内容，依然为乱码

![1628784356157](D:/download/downloadFromMicsoft/day09-Request&Response/ppt/assets/1628784356157.png)

通过上面的案例，会发现，不管是GET还是POST请求，在发送的请求参数中如果有中文，在后台接收的时候，都会出现中文乱码的问题。具体该如何解决呢？

#### 2.4.1 POST请求解决方案

* 分析出现中文乱码的原因：
  * POST的请求参数是通过request的getReader()来获取流中的数据
  * TOMCAT在获取流的时候采用的编码是ISO-8859-1
  * ISO-8859-1编码是不支持中文的，所以会出现乱码
* 解决方案：
  * 页面设置的编码格式为UTF-8
  * 把TOMCAT在获取流数据之前的编码设置为UTF-8
  * 通过request.setCharacterEncoding("UTF-8")设置编码,UTF-8也可以写成小写

修改后的代码为:

```java
/**
 * 中文乱码问题解决方案
 */
@WebServlet("/req4")
public class RequestDemo4 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //1. 解决乱码: POST getReader()
        //设置字符输入流的编码，设置的字符集要和页面保持一致
        request.setCharacterEncoding("UTF-8");
       //2. 获取username
       String username = request.getParameter("username");
       System.out.println(username);
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doGet(request, response);
    }
}
```

重新发送POST请求，就会在控制台看到正常展示的中文结果。

至此POST请求中文乱码的问题就已经解决，但是这种方案不适用于GET请求，这个原因是什么呢，咱们下面再分析。

#### 2.4.2 GET请求解决方案

刚才提到一个问题是`POST请求的中文乱码解决方案为什么不适用GET请求？`

* GET请求获取请求参数的方式是`request.getQueryString()`
* POST请求获取请求参数的方式是`request.getReader()`
* request.setCharacterEncoding("utf-8")是设置request处理流的编码
* getQueryString方法并没有通过流的方式获取数据

所以GET请求不能用设置编码的方式来解决中文乱码问题，那问题又来了，如何解决GET请求的中文乱码呢? 

1. 首先需要先分析下GET请求出现乱码的原因:

 ![1628829610823](D:/download/downloadFromMicsoft/day09-Request&Response/ppt/assets/1628829610823.png)

(1)浏览器通过HTTP协议发送请求和数据给后台服务器（Tomcat)

(2)浏览器在发送HTTP的过程中会对中文数据进行URL==编码==

(3)在进行URL编码的时候会采用页面`<meta>`标签指定的UTF-8的方式进行编码，`张三`编码后的结果为`%E5%BC%A0%E4%B8%89`

(4)后台服务器(Tomcat)接收到`%E5%BC%A0%E4%B8%89`后会默认按照`ISO-8859-1`进行URL==解码==

(5)由于前后编码与解码采用的格式不一样，就会导致后台获取到的数据为乱码。

思考: 如果把`req.html`页面的`<meta>`标签的charset属性改成`ISO-8859-1`,后台不做操作，能解决中文乱码问题么?

答案是否定的，因为`ISO-8859-1`本身是不支持中文展示的，所以改了<meta>标签的charset属性后，会导致页面上的中文内容都无法正常展示。

分析完上面的问题后，会发现，其中有两个不熟悉的内容就是==URL编码==和==URL解码==，什么是URL编码，什么又是URL解码呢?

**URL编码**

这块知识只需要了解下即可,具体编码过程分两步，分别是:

(1)将字符串按照编码方式转为二进制

(2)每个字节转为2个16进制数并在前边加上%

`张三`按照UTF-8的方式转换成二进制的结果为:

```
1110 0101 1011 1100 1010 0000 1110 0100 1011 1000 1000 1001
```

这个结果是如何计算的?

使用`http://www.mytju.com/classcode/tools/encode_utf8.asp`，输入`张三`

![1628833310473](D:/download/downloadFromMicsoft/day09-Request&Response/ppt/assets/1628833310473.png)

就可以获取张和三分别对应的10进制，然后在使用计算器，选择程序员模式，计算出对应的二进制数据结果:

![1628833496171](D:/download/downloadFromMicsoft/day09-Request&Response/ppt/assets/1628833496171.png)

在计算的十六进制结果中，每两位前面加一个%,就可以获取到`%E5%BC%A0%E4%B8%89`。

当然你从上面所提供的网站中就已经能看到编码16进制的结果了:

![1628833310473](D:/download/downloadFromMicsoft/day09-Request&Response/ppt/assets/1628833310474.png)

但是对于上面的计算过程，如果没有工具，纯手工计算的话，相对来说还是比较复杂的，也不需要进行手动计算，在Java中已经为提供了编码和解码的API工具类可以让更快速的进行编码和解码:

编码:

```java
java.net.URLEncoder.encode("需要被编码的内容","字符集(UTF-8)")
```

解码:

```java
java.net.URLDecoder.decode("需要被解码的内容","字符集(UTF-8)")
```

接下来咱们对`张三`来进行编码和解码

```
public class URLDemo {

  public static void main(String[] args) throws UnsupportedEncodingException {
        String username = "张三";
        //1. URL编码
        String encode = URLEncoder.encode(username, "utf-8");
        System.out.println(encode); //打印:%E5%BC%A0%E4%B8%89

       //2. URL解码
       //String decode = URLDecoder.decode(encode, "utf-8");//打印:张三
       String decode = URLDecoder.decode(encode, "ISO-8859-1");//打印:`å¼ ä¸ `
       System.out.println(decode);
    }
}

```

到这，就可以分析出GET请求中文参数出现乱码的原因了，

* 浏览器把中文参数按照`UTF-8`进行URL编码
* Tomcat对获取到的内容进行了`ISO-8859-1`的URL解码
* 在控制台就会出现类上`å¼ ä¸`的乱码，最后一位是个空格

2. 清楚了出现乱码的原因，接下来就需要想办法进行解决

![1628846824194](D:/download/downloadFromMicsoft/day09-Request&Response/ppt/assets/1628846824194.png)

从上图可以看住，

* 在进行编码和解码的时候，不管使用的是哪个字符集，他们对应的`%E5%BC%A0%E4%B8%89`是一致的

* 那他们对应的二进制值也是一样的，为:

  * ```
    1110 0101 1011 1100 1010 0000 1110 0100 1011 1000 1000 1001
    ```

* 为所以可以考虑把`å¼ ä¸`转换成字节，在把字节转换成`张三`，在转换的过程中是它们的编码一致，就可以解决中文乱码问题。

具体的实现步骤为:

>1.按照ISO-8859-1编码获取乱码`å¼ ä¸`对应的字节数组
>
>2.按照UTF-8编码获取字节数组对应的字符串

实现代码如下:

```
public class URLDemo {

  public static void main(String[] args) throws UnsupportedEncodingException {
        String username = "张三";
        //1. URL编码
        String encode = URLEncoder.encode(username, "utf-8");
        System.out.println(encode);
        //2. URL解码
        String decode = URLDecoder.decode(encode, "ISO-8859-1");

        System.out.println(decode); //此处打印的是对应的乱码数据

        //3. 转换为字节数据,编码
        byte[] bytes = decode.getBytes("ISO-8859-1");
        for (byte b : bytes) {
            System.out.print(b + " ");
        }
		//此处打印的是:-27 -68 -96 -28 -72 -119
        //4. 将字节数组转为字符串，解码
        String s = new String(bytes, "utf-8");
        System.out.println(s); //此处打印的是张三
    }
}
```

**说明**:在第18行中打印的数据是`-27 -68 -96 -28 -72 -119`和`张三`转换成的二进制数据`1110 0101 1011 1100 1010 0000 1110 0100 1011 1000 1000 1001`为什么不一样呢？

其实打印出来的是十进制数据，只需要使用计算机换算下就能得到他们的对应关系，如下图:

![1628849231208](D:/download/downloadFromMicsoft/day09-Request&Response/ppt/assets/1628849231208.png)

至此对于GET请求中文乱码的解决方案，就已经分析完了，最后在代码中去实现下:

```java
/**
 * 中文乱码问题解决方案
 */
@WebServlet("/req4")
public class RequestDemo4 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //1. 解决乱码：POST，getReader()
        //request.setCharacterEncoding("UTF-8");//设置字符输入流的编码

        //2. 获取username
        String username = request.getParameter("username");
        System.out.println("解决乱码前："+username);

        //3. GET,获取参数的方式：getQueryString
        // 乱码原因：tomcat进行URL解码，默认的字符集ISO-8859-1
       /* //3.1 先对乱码数据进行编码：转为字节数组
        byte[] bytes = username.getBytes(StandardCharsets.ISO_8859_1);
        //3.2 字节数组解码
        username = new String(bytes, StandardCharsets.UTF_8);*/

        username  = new String(username.getBytes(StandardCharsets.ISO_8859_1),StandardCharsets.UTF_8);

        System.out.println("解决乱码后："+username);

    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doGet(request, response);
    }
}
```

**注意**

* 把`request.setCharacterEncoding("UTF-8")`代码注释掉后，会发现GET请求参数乱码解决方案同时也可也把POST请求参数乱码的问题也解决了
* 只不过对于POST请求参数一般都会比较多，采用这种方式解决乱码起来比较麻烦，所以对于POST请求还是建议使用设置编码的方式进行。

另外需要说明一点的是==Tomcat8.0之后，已将GET请求乱码问题解决，设置默认的解码方式为UTF-8==

**小结**

1. 中文乱码解决方案

* POST请求和GET请求的参数中如果有中文，后台接收数据就会出现中文乱码问题

  GET请求在Tomcat8.0以后的版本就不会出现了

* POST请求解决方案是:设置输入流的编码

  ```
  request.setCharacterEncoding("UTF-8");
  注意:设置的字符集要和页面保持一致
  ```

* 通用方式（GET/POST）：需要先解码，再编码

  ```
  new String(username.getBytes("ISO-8859-1"),"UTF-8");
  ```

2. URL编码实现方式:

* 编码:

  ```
  URLEncoder.encode(str,"UTF-8");
  ```

* 解码:

  ```
  URLDecoder.decode(s,"ISO-8859-1");
  ```

### 2.5 Request请求转发

1. ==请求转发(forward):一种在服务器内部的资源跳转方式。==

![1628851404283](D:/download/downloadFromMicsoft/day09-Request&Response/ppt/assets/1628851404283.png)

(1)浏览器发送请求给服务器，服务器中对应的资源A接收到请求

(2)资源A处理完请求后将请求发给资源B

(3)资源B处理完后将结果响应给浏览器

(4)请求从资源A到资源B的过程就叫==请求转发==

2. 请求转发的实现方式:

```
req.getRequestDispatcher("资源B路径").forward(req,resp);
```

具体如何来使用，先来看下需求:

![1628854783523](D:/download/downloadFromMicsoft/day09-Request&Response/ppt/assets/1628854783523.png)

针对上述需求，具体的实现步骤为:

>1.创建一个RequestDemo5类，接收/req5的请求，在doGet方法中打印`demo5`
>
>2.创建一个RequestDemo6类，接收/req6的请求，在doGet方法中打印`demo6`
>
>3.在RequestDemo5的方法中使用
>
>​	req.getRequestDispatcher("/req6").forward(req,resp)进行请求转发
>
>4.启动测试

(1)创建RequestDemo5类

```java
/**
 * 请求转发
 */
@WebServlet("/req5")
public class RequestDemo5 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        System.out.println("demo5...");
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doGet(request, response);
    }
}
```

(2)创建RequestDemo6类

```java
/**
 * 请求转发
 */
@WebServlet("/req6")
public class RequestDemo6 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        System.out.println("demo6...");
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doGet(request, response);
    }
}
```

(3)在RequestDemo5的doGet方法中进行请求转发

```java
/**
 * 请求转发
 */
@WebServlet("/req5")
public class RequestDemo5 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        System.out.println("demo5...");
        //请求转发
        request.getRequestDispatcher("/req6").forward(request,response);
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doGet(request, response);
    }
}
```

(4)启动测试

访问`http://localhost:8080/request-demo/req5`,就可以在控制台看到如下内容:

![1628855192876](D:/download/downloadFromMicsoft/day09-Request&Response/ppt/assets/1628855192876.png)

说明请求已经转发到了`/req6`

3. 请求转发资源间共享数据:使用Request对象

此处主要解决的问题是把请求从`/req5`转发到`/req6`的时候，如何传递数据给`/req6`。

需要使用request对象提供的三个方法:

* 存储数据到request域[范围,数据是存储在request对象]中

```
void setAttribute(String name,Object o);
```

* 根据key获取值

```
Object getAttribute(String name);
```

* 根据key删除该键值对

```
void removeAttribute(String name);
```

接着上个需求来:

![1628856995417](D:/download/downloadFromMicsoft/day09-Request&Response/ppt/assets/1628856995417.png)

> 1.在RequestDemo5的doGet方法中转发请求之前，将数据存入request域对象中
>
> 2.在RequestDemo6的doGet方法从request域对象中获取数据，并将数据打印到控制台
>
> 3.启动访问测试

(1)修改RequestDemo5中的方法

```java
@WebServlet("/req5")
public class RequestDemo5 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        System.out.println("demo5...");
        //存储数据
        request.setAttribute("msg","hello");
        //请求转发
        request.getRequestDispatcher("/req6").forward(request,response);

    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doGet(request, response);
    }
}
```

(2)修改RequestDemo6中的方法

```java
/**
 * 请求转发
 */
@WebServlet("/req6")
public class RequestDemo6 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        System.out.println("demo6...");
        //获取数据
        Object msg = request.getAttribute("msg");
        System.out.println(msg);

    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doGet(request, response);
    }
}
```

(3)启动测试

访问`http://localhost:8080/request-demo/req5`,就可以在控制台看到如下内容:

![1628857213364](D:/download/downloadFromMicsoft/day09-Request&Response/ppt/assets/1628857213364.png)

此时就可以实现在转发多个资源之间共享数据。

4. 请求转发的特点

* 浏览器地址栏路径不发生变化

  虽然后台从`/req5`转发到`/req6`,但是浏览器的地址一直是`/req5`,未发生变化

  ![1628857365153](D:/download/downloadFromMicsoft/day09-Request&Response/ppt/assets/1628857365153.png)

* 只能转发到当前服务器的内部资源

  不能从一个服务器通过转发访问另一台服务器

* 一次请求，可以在转发资源间使用request共享数据

  虽然后台从`/req5`转发到`/req6`，但是这个==只有一次请求==

## 3，Response对象

前面讲解完Request对象，接下来回到刚开始的那张图:

![1628857632899](D:/download/downloadFromMicsoft/day09-Request&Response/ppt/assets/1628857632899.png)

* Request:使用request对象来==获取==请求数据
* Response:使用response对象来==设置==响应数据

Reponse的继承体系和Request的继承体系也非常相似:

![1628857761317](D:/download/downloadFromMicsoft/day09-Request&Response/ppt/assets/1628857761317.png)

 介绍完Response的相关体系结构后，接下来对于Response需要学习如下内容:

* Response设置响应数据的功能介绍
* Response完成重定向
* Response响应字符数据
* Response响应字节数据

### 3.1 Response设置响应数据功能介绍

HTTP响应数据总共分为三部分内容，分别是==响应行、响应头、响应体==，对于这三部分内容的数据，respone对象都提供了哪些方法来进行设置?

1. 响应行

![1628858926498](D:/download/downloadFromMicsoft/day09-Request&Response/ppt/assets/1628858926498.png)

对于响应头，比较常用的就是设置响应状态码:

```
void setStatus(int sc);
```

2. 响应头

![1628859051368](D:/download/downloadFromMicsoft/day09-Request&Response/ppt/assets/1628859051368.png)

设置响应头键值对：

```
void setHeader(String name,String value);
```

3. 响应体

![1628859268095](D:/download/downloadFromMicsoft/day09-Request&Response/ppt/assets/1628859268095.png)

对于响应体，是通过字符、字节输出流的方式往浏览器写，

获取字符输出流:

```
PrintWriter getWriter();
```

获取字节输出流

```
ServletOutputStream getOutputStream();
```

介绍完这些方法后，后面会通过案例把这些方法都用一用，首先先来完成下重定向的功能开发。

### 3.2 Respones请求重定向

1. ==Response重定向(redirect):一种资源跳转方式。==

![1628859860279](D:/download/downloadFromMicsoft/day09-Request&Response/ppt/assets/1628859860279.png)

(1)浏览器发送请求给服务器，服务器中对应的资源A接收到请求

(2)资源A现在无法处理该请求，就会给浏览器响应一个302的状态码+location的一个访问资源B的路径

(3)浏览器接收到响应状态码为302就会重新发送请求到location对应的访问地址去访问资源B

(4)资源B接收到请求后进行处理并最终给浏览器响应结果，这整个过程就叫==重定向==

2. 重定向的实现方式:

```
resp.setStatus(302);
resp.setHeader("location","资源B的访问路径");
```

具体如何来使用，先来看下需求:

![1628861030429](D:/download/downloadFromMicsoft/day09-Request&Response/ppt/assets/1628861030429.png)

针对上述需求，具体的实现步骤为:

> 1.创建一个ResponseDemo1类，接收/resp1的请求，在doGet方法中打印`resp1....`
>
> 2.创建一个ResponseDemo2类，接收/resp2的请求，在doGet方法中打印`resp2....`
>
> 3.在ResponseDemo1的方法中使用
>
> ​	response.setStatus(302);
>
> ​	response.setHeader("Location","/request-demo/resp2") 来给前端响应结果数据
>
> 4.启动测试

(1)创建ResponseDemo1类

```java
@WebServlet("/resp1")
public class ResponseDemo1 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        System.out.println("resp1....");
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doGet(request, response);
    }
}
```

(2)创建ResponseDemo2类

```java
@WebServlet("/resp2")
public class ResponseDemo2 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        System.out.println("resp2....");
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doGet(request, response);
    }
}
```

(3)在ResponseDemo1的doGet方法中给前端响应数据

```java
@WebServlet("/resp1")
public class ResponseDemo1 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        System.out.println("resp1....");
        //重定向
        //1.设置响应状态码 302
        response.setStatus(302);
        //2. 设置响应头 Location
        response.setHeader("Location","/request-demo/resp2");
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doGet(request, response);
    }
}
```

(4)启动测试

访问`http://localhost:8080/request-demo/resp1`,就可以在控制台看到如下内容:

![1628861404699](D:/download/downloadFromMicsoft/day09-Request&Response/ppt/assets/1628861404699.png)

说明`/resp1`和`/resp2`都被访问到了。到这重定向就已经完成了。

虽然功能已经实现，但是从设置重定向的两行代码来看，会发现除了重定向的地址不一样，其他的内容都是一模一样，所以request对象给提供了简化的编写方式为:

```
resposne.sendRedirect("/request-demo/resp2")
```

所以第3步中的代码就可以简化为：

```java
@WebServlet("/resp1")
public class ResponseDemo1 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        System.out.println("resp1....");
        //重定向
        resposne.sendRedirect("/request-demo/resp2")；
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doGet(request, response);
    }
}
```

3. 重定向的特点

* 浏览器地址栏路径发送变化

  当进行重定向访问的时候，由于是由浏览器发送的两次请求，所以地址会发生变化

  ![1628861893130](D:/download/downloadFromMicsoft/day09-Request&Response/ppt/assets/1628861893130.png)

* 可以重定向到任何位置的资源(服务内容、外部均可)

  因为第一次响应结果中包含了浏览器下次要跳转的路径，所以这个路径是可以任意位置资源。

* 两次请求，不能在多个资源使用request共享数据

  因为浏览器发送了两次请求，是两个不同的request对象，就无法通过request对象进行共享数据

介绍完==请求重定向==和==请求转发==以后，接下来需要把这两个放在一块对比下:

![1628862170296](D:/download/downloadFromMicsoft/day09-Request&Response/ppt/assets/1628862170296.png)

以后到底用哪个，还是需要根据具体的业务来决定。

### 3.3 路径问题虚拟地址



1. 问题1：转发的时候路径上没有加`/request-demo`而重定向加了，那么到底什么时候需要加，什么时候不需要加呢?

![1628862652700](D:/download/downloadFromMicsoft/day09-Request&Response/ppt/assets/1628862652700.png)

其实判断的依据很简单，只需要记住下面的规则即可:

* 浏览器使用:需要加虚拟目录(项目访问路径)
* 服务端使用:不需要加虚拟目录

对于转发来说，因为是在服务端进行的，所以不需要加虚拟目录

对于重定向来说，路径最终是由浏览器来发送请求，就需要添加虚拟目录。

掌握了这个规则，接下来就通过一些练习来强化下知识的学习:

* `<a href='路劲'>`
* `<form action='路径'>`
* req.getRequestDispatcher("路径")
* resp.sendRedirect("路径")

答案:

```
1.超链接，从浏览器发送，需要加
2.表单，从浏览器发送，需要加
3.转发，是从服务器内部跳转，不需要加
4.重定向，是由浏览器进行跳转，需要加。
```

2. 问题2：在重定向的代码中，`/request-demo`是固定编码的，如果后期通过Tomcat插件配置了项目的访问路径，那么所有需要重定向的地方都需要重新修改，该如何优化?

![1628863270545](D:/download/downloadFromMicsoft/day09-Request&Response/ppt/assets/1628863270545.png)

答案也比较简单，可以在代码中动态去获取项目访问的虚拟目录，具体如何获取，可以借助前面咱们所学习的request对象中的getContextPath()方法，修改后的代码如下:

```java
@WebServlet("/resp1")
public class ResponseDemo1 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        System.out.println("resp1....");

        //简化方式完成重定向
        //动态获取虚拟目录
        String contextPath = request.getContextPath();
        response.sendRedirect(contextPath+"/resp2");
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doGet(request, response);
    }
}
```

重新启动访问测试，功能依然能够实现，此时就可以动态获取项目访问的虚拟路径，从而降低代码的耦合度。

### 3.4 Response响应字符数据

要想将字符数据写回到浏览器，需要两个步骤:

* 通过Response对象获取字符输出流： PrintWriter writer = resp.getWriter();

* 通过字符输出流写数据: writer.write("aaa");

接下来，实现通过些案例把响应字符数据给实际应用下:

1. 返回一个简单的字符串`aaa`

```java
/**
 * 响应字符数据：设置字符数据的响应体
 */
@WebServlet("/resp3")
public class ResponseDemo3 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        response.setContentType("text/html;charset=utf-8");
        //1. 获取字符输出流
        PrintWriter writer = response.getWriter();
		 writer.write("aaa");
    }
    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doGet(request, response);
    }
}
```

![1628863905362](D:/download/downloadFromMicsoft/day09-Request&Response/ppt/assets/1628863905362.png)

2. 返回一串html字符串，并且能被浏览器解析

```
PrintWriter writer = response.getWriter();
//content-type，告诉浏览器返回的数据类型是HTML类型数据，这样浏览器才会解析HTML标签
response.setHeader("content-type","text/html");
writer.write("<h1>aaa</h1>");
```

![1628864140820](D:/download/downloadFromMicsoft/day09-Request&Response/ppt/assets/1628864140820.png)

==注意:==一次请求响应结束后，response对象就会被销毁掉，所以不要手动关闭流。

3. 返回一个中文的字符串`你好`，需要注意设置响应数据的编码为`utf-8`

```
//设置响应的数据格式及数据的编码
response.setContentType("text/html;charset=utf-8");
writer.write("你好");
```

![1628864390263](D:/download/downloadFromMicsoft/day09-Request&Response/ppt/assets/1628864390263.png)

### 3.3 Response响应字节数据

要想将字节数据写回到浏览器，需要两个步骤:

- 通过Response对象获取字节输出流：ServletOutputStream outputStream = resp.getOutputStream();

- 通过字节输出流写数据: outputStream.write(字节数据);

接下来，实现通过些案例把响应字符数据给实际应用下:

1. 返回一个图片文件到浏览器

```java
/**
 * 响应字节数据：设置字节数据的响应体
 */
@WebServlet("/resp4")
public class ResponseDemo4 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //1. 读取文件
        FileInputStream fis = new FileInputStream("d://a.jpg");
        //2. 获取response字节输出流
        ServletOutputStream os = response.getOutputStream();
        //3. 完成流的copy
        byte[] buff = new byte[1024];
        int len = 0;
        while ((len = fis.read(buff))!= -1){
            os.write(buff,0,len);
        }
        fis.close();
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doGet(request, response);
    }
}
```

![1628864883564](D:/download/downloadFromMicsoft/day09-Request&Response/ppt/assets/1628864883564.png)

上述代码中，对于流的copy的代码还是比较复杂的，所以可以使用别人提供好的方法来简化代码的开发，具体的步骤是:

(1)pom.xml添加依赖

```xml
<dependency>
    <groupId>commons-io</groupId>
    <artifactId>commons-io</artifactId>
    <version>2.6</version>
</dependency>
```

(2)调用工具类方法

```
//fis:输入流
//os:输出流
IOUtils.copy(fis,os);
```

优化后的代码:

```java
/**
 * 响应字节数据：设置字节数据的响应体
 */
@WebServlet("/resp4")
public class ResponseDemo4 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //1. 读取文件
        FileInputStream fis = new FileInputStream("d://a.jpg");
        //2. 获取response字节输出流
        ServletOutputStream os = response.getOutputStream();
        //3. 完成流的copy
      	IOUtils.copy(fis,os);
        fis.close();
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doGet(request, response);
    }
}
```

## 4，用户注册登录案例

接下来通过两个比较常见的案例，一个是==注册==，一个是==登录==来对今天学习的内容进行一个实战演练，首先来实现用户登录。

### 4.1 用户登录

#### 4.1.1 需求分析

![1628865728305](D:/download/downloadFromMicsoft/day09-Request&Response/ppt/assets/1628865728305.png)

1. 用户在登录页面输入用户名和密码，提交请求给LoginServlet
2. 在LoginServlet中接收请求和数据[用户名和密码]
3. 在LoginServlt中通过Mybatis实现调用UserMapper来根据用户名和密码查询数据库表
4. 将查询的结果封装到User对象中进行返回
5. 在LoginServlet中判断返回的User对象是否为null
6. 如果为nul，说明根据用户名和密码没有查询到用户，则登录失败，返回"登录失败"数据给前端
7. 如果不为null,则说明用户存在并且密码正确，则登录成功，返回"登录成功"数据给前端

#### 4.1.2 环境准备

环境配置预览

- 复制资料中的静态页面到项目的webapp目录下
- 创建db1数据库，创建tb_user表，创建User实体类
- 在项目的pom.xml导入Mybatis和Mysql驱动坐标
- 创建mybatis-config.xml核心配置文件，UserMapper.xml映射文件,UserMapper接口



第四步的实现目录结构

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220417131840005.png" alt="image-20220417131840005" style="zoom: 67%;" />



1. 复制资料中的静态页面到项目的webapp目录下

参考`资料\1. 登陆注册案例\1. 静态页面`,拷贝完效果如下:

![1628866248169](D:/download/downloadFromMicsoft/day09-Request&Response/ppt/assets/1628866248169.png)

2. 创建db1数据库，创建tb_user表，创建User实体类

2.1 将`资料\1. 登陆注册案例\2. MyBatis环境\tb_user.sql`中的sql语句执行下:

![1628866403891](D:/download/downloadFromMicsoft/day09-Request&Response/ppt/assets/1628866403891.png)

 2.2 将`资料\1. 登陆注册案例\2. MyBatis环境\User.java`拷贝到com.itheima.pojo

![1628866560738](D:/download/downloadFromMicsoft/day09-Request&Response/ppt/assets/1628866560738.png)

3. 在项目的pom.xml导入Mybatis和Mysql驱动坐标

```xml
<dependency>
    <groupId>org.mybatis</groupId>
    <artifactId>mybatis</artifactId>
    <version>3.5.5</version>
</dependency>

<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>5.1.34</version>
</dependency>
```

4. 创建mybatis-config.xml核心配置文件，UserMapper.xml映射文件,UserMapper接口

4.1  将`资料\1. 登陆注册案例\2. MyBatis环境\mybatis-config.xml`拷贝到resources目录下

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
    <!--起别名-->
    <typeAliases>
        <package name="com.itheima.pojo"/>
    </typeAliases>

    <environments default="development">
        <environment id="development">
            <transactionManager type="JDBC"/>
            <dataSource type="POOLED">
                <property name="driver" value="com.mysql.jdbc.Driver"/>
                <!--
                    useSSL:关闭SSL安全连接 性能更高
                    useServerPrepStmts:开启预编译功能
                    &amp; 等同于 & ,xml配置文件中不能直接写 &符号
                -->
                <property name="url" value="jdbc:mysql:///db1?useSSL=false&amp;useServerPrepStmts=true"/>
                <property name="username" value="root"/>
                <property name="password" value="1234"/>
            </dataSource>
        </environment>
    </environments>
    <mappers>
        <!--扫描mapper-->
        <package name="com.itheima.mapper"/>
    </mappers>
</configuration>
```

4.2 在com.itheima.mapper包下创建UserMapper接口

```java
public interface UserMapper {

}
```

4.3 将`资料\1. 登陆注册案例\2. MyBatis环境\UserMapper.xml`拷贝到resources目录下

==注意：在resources下创建UserMapper.xml的目录时，要使用/分割==

![1628867237329](D:/download/downloadFromMicsoft/day09-Request&Response/ppt/assets/1628867237329.png)

至此所需要的环境就都已经准备好了，具体该如何实现?

#### 4.1.3 代码实现

1. 在UserMapper接口中提供一个根据用户名和密码查询用户对象的方法

```java
/**
     * 根据用户名和密码查询用户对象
     * @param username
     * @param password
     * @return
     */
    @Select("select * from tb_user where username = #{username} and password = #{password}")
    User select(@Param("username") String username,@Param("password")  String password);
```

**说明**

@Param注解的作用:用于传递参数,是方法的参数可以与SQL中的字段名相对应。

2. 修改loign.html

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <title>login</title>
    <link href="css/login.css" rel="stylesheet">
</head>

<body>
<div id="loginDiv">
    <form action="/request-demo/loginServlet" method="post" id="form">
        <h1 id="loginMsg">LOGIN IN</h1>
        <p>Username:<input id="username" name="username" type="text"></p>

        <p>Password:<input id="password" name="password" type="password"></p>

        <div id="subDiv">
            <input type="submit" class="button" value="login up">
            <input type="reset" class="button" value="reset">&nbsp;&nbsp;&nbsp;
            <a href="register.html">没有账号？点击注册</a>
        </div>
    </form>
</div>

</body>
</html>
```

3. 编写LoginServlet

```java
@WebServlet("/loginServlet")
public class LoginServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //1. 接收用户名和密码
        String username = request.getParameter("username");
        String password = request.getParameter("password");

        //2. 调用MyBatis完成查询
        //2.1 获取SqlSessionFactory对象
        String resource = "mybatis-config.xml";
        InputStream inputStream = Resources.getResourceAsStream(resource);
        SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);
        //2.2 获取SqlSession对象
        SqlSession sqlSession = sqlSessionFactory.openSession();
        //2.3 获取Mapper
        UserMapper userMapper = sqlSession.getMapper(UserMapper.class);
        //2.4 调用方法
        User user = userMapper.select(username, password);
        //2.5 释放资源
        sqlSession.close();


        //获取字符输出流，并设置content type
        response.setContentType("text/html;charset=utf-8");
        PrintWriter writer = response.getWriter();
        //3. 判断user释放为null
        if(user != null){
            // 登陆成功
            writer.write("登陆成功");
        }else {
            // 登陆失败
            writer.write("登陆失败");
        }
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doGet(request, response);
    }
}
```

4. 启动服务器测试

4.1 如果用户名和密码输入错误，则

![1628867761245](D:/download/downloadFromMicsoft/day09-Request&Response/ppt/assets/1628867761245.png)

4.2 如果用户名和密码输入正确，则

![1628867801708](D:/download/downloadFromMicsoft/day09-Request&Response/ppt/assets/1628867801708.png)

至此用户的登录功能就已经完成了~



成功的喜悦可以让人奋发向上，加油啊，wzt

![image-20220417164951760](C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220417164951760.png)





### 4.2 用户注册

#### 4.2.1 需求分析

![1628867904783](D:/download/downloadFromMicsoft/day09-Request&Response/ppt/assets/1628867904783.png)

1. 用户在注册页面输入用户名和密码，提交请求给RegisterServlet
2. 在RegisterServlet中接收请求和数据[用户名和密码]
3. 在RegisterServlet中通过Mybatis实现调用UserMapper来根据用户名查询数据库表
4. 将查询的结果封装到User对象中进行返回
5. 在RegisterServlet中判断返回的User对象是否为null
6. 如果为nul，说明根据用户名可用，则调用UserMapper来实现添加用户
7. 如果不为null,则说明用户不可以，返回"用户名已存在"数据给前端

#### 4.2.2 代码编写

1. 编写UserMapper提供根据用户名查询用户数据方法和添加用户方法

```java
/**
* 根据用户名查询用户对象
* @param username
* @return
*/
@Select("select * from tb_user where username = #{username}")
User selectByUsername(String username);

/**
* 添加用户
* @param user
*/
@Insert("insert into tb_user values(null,#{username},#{password})")
void add(User user);
```

2. 修改register.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>欢迎注册</title>
    <link href="css/register.css" rel="stylesheet">
</head>
<body>

<div class="form-div">
    <div class="reg-content">
        <h1>欢迎注册</h1>
        <span>已有帐号？</span> <a href="login.html">登录</a>
    </div>
    <form id="reg-form" action="/request-demo/registerServlet" method="post">

        <table>

            <tr>
                <td>用户名</td>
                <td class="inputs">
                    <input name="username" type="text" id="username">
                    <br>
                    <span id="username_err" class="err_msg" style="display: none">用户名不太受欢迎</span>
                </td>

            </tr>

            <tr>
                <td>密码</td>
                <td class="inputs">
                    <input name="password" type="password" id="password">
                    <br>
                    <span id="password_err" class="err_msg" style="display: none">密码格式有误</span>
                </td>
            </tr>

        </table>

        <div class="buttons">
            <input value="注 册" type="submit" id="reg_btn">
        </div>
        <br class="clear">
    </form>

</div>
</body>
</html>
```

3. 创建RegisterServlet类

```java
@WebServlet("/registerServlet")
public class RegisterServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //1. 接收用户数据
        String username = request.getParameter("username");
        String password = request.getParameter("password");

        //封装用户对象
        User user = new User();
        user.setUsername(username);
        user.setPassword(password);

        //2. 调用mapper 根据用户名查询用户对象
        //2.1 获取SqlSessionFactory对象
        String resource = "mybatis-config.xml";
        InputStream inputStream = Resources.getResourceAsStream(resource);
        SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);
        //2.2 获取SqlSession对象
        SqlSession sqlSession = sqlSessionFactory.openSession();
        //2.3 获取Mapper
        UserMapper userMapper = sqlSession.getMapper(UserMapper.class);

        //2.4 调用方法
        User u = userMapper.selectByUsername(username);

        //3. 判断用户对象释放为null
        if( u == null){
            // 用户名不存在，添加用户
            userMapper.add(user);

            // 提交事务
            sqlSession.commit();
            // 释放资源
            sqlSession.close();
        }else {
            // 用户名存在，给出提示信息
            response.setContentType("text/html;charset=utf-8");
            response.getWriter().write("用户名已存在");
        }

    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doGet(request, response);
    }
}
```

4. 启动服务器进行测试

4.1 如果测试成功，则在数据库中就能查看到新注册的数据

4.2 如果用户已经存在，则在页面上展示 `用户名已存在` 的提示信息



### 个人理解

实现案例之后心得体会：

mybatis:建立数据库连接，

mapper映射，用来操作数据库

servlet部署在服务器上，用来根据request回复响应的response





### 4.3 SqlSessionFactory工具类抽取

上面两个功能已经实现，但是在写Servlet的时候，因为需要使用Mybatis来完成数据库的操作，所以对于Mybatis的基础操作就出现了些重复代码，如下

```java
String resource = "mybatis-config.xml";
InputStream inputStream = Resources.getResourceAsStream(resource);
SqlSessionFactory sqlSessionFactory = new 
	SqlSessionFactoryBuilder().build(inputStream);
```

有了这些重复代码就会造成一些问题:

* 重复代码不利于后期的维护
* SqlSessionFactory工厂类进行重复创建
  * 就相当于每次买手机都需要重新创建一个手机生产工厂来给你制造一个手机一样，资源消耗非常大但性能却非常低。所以这么做是不允许的。

那如何来优化呢？

* 代码重复可以抽取工具类
* 对指定代码只需要执行一次可以使用静态代码块

有了这两个方向后，代码具体该如何编写?

```java
public class SqlSessionFactoryUtils {

    private static SqlSessionFactory sqlSessionFactory;

    static {
        //静态代码块会随着类的加载而自动执行，且只执行一次
        try {
            String resource = "mybatis-config.xml";
            InputStream inputStream = Resources.getResourceAsStream(resource);
            sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }


    public static SqlSessionFactory getSqlSessionFactory(){
        return sqlSessionFactory;
    }
}
```

工具类抽取以后，以后在对Mybatis的SqlSession进行操作的时候，就可以直接使用

```java
SqlSessionFactory sqlSessionFactory =SqlSessionFactoryUtils.getSqlSessionFactory();
```

这样就可以很好的解决上面所说的代码重复和重复创建工厂导致性能低的问题了。



这三行代码同SqlSessionFactory名字，是SqlSession的工厂

# JSP

**今日目标：**

> * 理解 JSP 及 JSP 原理
> * 能在 JSP中使用 `EL表达式` 和 `JSTL标签`
> * 理解 `MVC模式` 和 `三层架构`
> * 能完成品牌数据的增删改查功能

## 1，JSP 概述

==JSP（全称：Java Server Pages）：Java 服务端页面。==是一种动态的网页技术，其中既可以定义 HTML、JS、CSS等静态内容，还可以定义 Java代码的动态内容，也就是 `JSP = HTML + Java`。如下就是jsp代码

```jsp
<html>
    <head>
        <title>Title</title>
    </head>
    <body>
        <h1>JSP,Hello World</h1>
        <%
        	System.out.println("hello,jsp~");
        %>
    </body>
</html>
```

上面代码 `h1` 标签内容是展示在页面上，而 Java 的输出语句是输出在 idea 的控制台。

那么，JSP 能做什么呢？现在只用 `servlet` 实现功能，看存在什么问题。如下图所示，当登陆成功后，需要在页面上展示用户名

<img src="D:/download/downloadFromMicsoft/day10-JSP/ppt/assets/image-20210818101320935.png" alt="image-20210818101320935" style="zoom:70%;" /> 

上图的用户名是动态展示，也就是谁登陆就展示谁的用户名。只用 `servlet` 如何实现呢？在今天的资料里已经提供好了一个 `LoginServlet` ，该 `servlet` 就是实现这个功能的，现将资料中的 `LoginServlet.java` 拷贝到 `request-demo` 项目中来演示。接下来启动服务器并访问登陆页面

<img src="D:/download/downloadFromMicsoft/day10-JSP/ppt/assets/image-20210818102205544.png" alt="image-20210818102205544" style="zoom:80%;" />

输入了 `zhangsan` 用户的登陆信息后点击 `登陆` 按钮，就能看到如下图效果

![image-20210818102313898](D:/download/downloadFromMicsoft/day10-JSP/ppt/assets/image-20210818102313898.png)

当然如果是 `lisi` 登陆的，在该页面展示的就是 `lisi,欢迎您`，动态的展示效果就实现了。那么 `LoginServlet` 到底是如何实现的，看看它里面的内容

<img src="D:/download/downloadFromMicsoft/day10-JSP/ppt/assets/image-20210818102506754.png" alt="image-20210818102506754" style="zoom:70%;" />

上面的代码有大量使用到 `writer` 对象向页面写标签内容，这样的代码就显得很麻烦；将来如果展示的效果出现了问题，排错也显得有点力不从心。而 JSP 是如何解决这个问题的呢？在资料中也提供了一个 `login.jsp` 页面，该页面也能实现该功能，现将该页面拷贝到项目的 `webapp`下，需要修改 `login.html` 中表单数据提交的路径为下图

<img src="D:/download/downloadFromMicsoft/day10-JSP/ppt/assets/image-20210818103127245.png" alt="image-20210818103127245" style="zoom:80%;" />



重新启动服务器并进行测试，发现也可以实现同样的功能。那么 `login.jsp` 又是如何实现的呢？那来看看 `login.jsp` 的代码

<img src="D:/download/downloadFromMicsoft/day10-JSP/ppt/assets/image-20210818103352432.png" alt="image-20210818103352432" style="zoom:70%;" />

上面代码可以看到里面基本都是 `HTML` 标签，而动态数据使用 Java 代码进行展示；这样操作看起来要比用 `servlet` 实现要舒服很多。

JSP 作用：简化开发，避免了在Servlet中直接输出HTML标签。

## 2，JSP 快速入门

接下来做一个简单的快速入门代码。

### 2.1  搭建环境

创建一个maven的 web 项目，项目结构如下：

<img src="D:/download/downloadFromMicsoft/day10-JSP/ppt/assets/image-20210818104316457.png" alt="image-20210818104316457" style="zoom:80%;" />

`pom.xml` 文件内容如下：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>org.example</groupId>
    <artifactId>jsp-demo</artifactId>
    <version>1.0-SNAPSHOT</version>
    <packaging>war</packaging>

    <properties>
        <maven.compiler.source>8</maven.compiler.source>
        <maven.compiler.target>8</maven.compiler.target>
    </properties>

    <dependencies>
      <dependency>
            <groupId>javax.servlet</groupId>
            <artifactId>javax.servlet-api</artifactId>
            <version>3.1.0</version>
            <scope>provided</scope>
        </dependency>
    </dependencies>

    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.tomcat.maven</groupId>
                <artifactId>tomcat7-maven-plugin</artifactId>
                <version>2.2</version>
            </plugin>
        </plugins>
    </build>
</project>
```

### 2.2  导入 JSP 依赖

在 `dependencies` 标签中导入 JSP 的依赖，如下

```xml
<dependency>
    <groupId>javax.servlet.jsp</groupId>
    <artifactId>jsp-api</artifactId>
    <version>2.2</version>
    <scope>provided</scope>
</dependency>
```

该依赖的 `scope` 必须设置为 `provided`，因为 tomcat 中有这个jar包了，所以在打包时是不希望将该依赖打进到工程的war包中。

### 2.3  创建 jsp 页面

在项目的 `webapp` 下创建jsp页面

<img src="D:/download/downloadFromMicsoft/day10-JSP/ppt/assets/image-20210818105519970.png" alt="image-20210818105519970" style="zoom:70%;" />

通过上面方式创建一个名为 `hello.jsp` 的页面。

### 2.4  编写代码

在 `hello.jsp` 页面中书写 `HTML` 标签和 `Java` 代码，如下

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
    <h1>hello jsp</h1>

    <%
        System.out.println("hello,jsp~");
    %>
</body>
</html>
```

### 2.5  测试

启动服务器并在浏览器地址栏输入 `http://localhost:8080/jsp-demo/hello.jsp`，可以在页面上看到如下内容

<img src="D:/download/downloadFromMicsoft/day10-JSP/ppt/assets/image-20210818110122438.png" alt="image-20210818110122438" style="zoom:70%;" />

同时也可以看到在 `idea` 的控制台看到输出的 `hello,jsp~` 内容。

## 3，JSP 原理

之前说 JSP 就是一个页面，那么在 JSP 中写 `html` 标签，能理解，但是为什么还可以写 `Java` 代码呢？

因为 ==JSP 本质上就是一个 Servlet。==接下来聊聊访问jsp时的流程

<img src="D:/download/downloadFromMicsoft/day10-JSP/ppt/assets/image-20210818111039350.png" alt="image-20210818111039350" style="zoom:70%;" />

1. 浏览器第一次访问 `hello.jsp` 页面
2. `tomcat` 会将 `hello.jsp` 转换为名为 `hello_jsp.java` 的一个 `Servlet`
3. `tomcat` 再将转换的 `servlet` 编译成字节码文件 `hello_jsp.class`
4. `tomcat` 会执行该字节码文件，向外提供服务

可以到项目所在磁盘目录下找 `target\tomcat\work\Tomcat\localhost\jsp-demo\org\apache\jsp` 目录，而这个目录下就能看到转换后的 `servlet`

<img src="D:/download/downloadFromMicsoft/day10-JSP/ppt/assets/image-20210818112613589.png" alt="image-20210818112613589" style="zoom:80%;" />

打开 `hello_jsp.java` 文件，来查看里面的代码

<img src="D:/download/downloadFromMicsoft/day10-JSP/ppt/assets/image-20210818112724462.png" alt="image-20210818112724462" style="zoom:80%;" />

由上面的类的继承关系可以看到继承了名为 `HttpJspBase` 这个类，那在看该类的继承关系。到资料中的找如下目录： `资料\tomcat源码\apache-tomcat-8.5.68-src\java\org\apache\jasper\runtime` ，该目录下就有 `HttpJspBase` 类，查看该类的继承关系

<img src="D:/download/downloadFromMicsoft/day10-JSP/ppt/assets/image-20210818113118802.png" alt="image-20210818113118802" style="zoom:80%;" />

可以看到该类继承了 `HttpServlet` ；那么 `hello_jsp` 这个类就间接的继承了 `HttpServlet` ，也就说明 `hello_jsp` 是一个 `servlet`。

继续阅读 `hello_jsp` 类的代码，可以看到有一个名为 `_jspService()` 的方法，该方法就是每次访问 `jsp` 时自动执行的方法，和 `servlet` 中的 `service` 方法一样 。

而在 `_jspService()` 方法中可以看到往浏览器写标签的代码：

<img src="D:/download/downloadFromMicsoft/day10-JSP/ppt/assets/image-20210818114008998.png" alt="image-20210818114008998" style="zoom:80%;" />

以前自己写 `servlet` 时，这部分代码是由自己来写，现在有了 `jsp` 后，由tomcat完成这部分功能。

## 4，JSP 脚本

JSP脚本用于在 JSP页面内定义 Java代码。在之前的入门案例中就在 JSP 页面定义的 Java 代码就是 JSP 脚本。

### 4.1  JSP 脚本分类

JSP 脚本有如下三个分类：

* <%...%>：内容会直接放到_jspService()方法之中

可以理解为C++的main函数

* <%=…%>：内容会放到out.print()中，作为out.print()的参数

将会直接展示到前端页面中

* <%!…%>：内容会放到_jspService()方法之外，被类直接包含

其他的全局类

**代码演示：**

在 `hello.jsp` 中书写

```jsp
<%
    System.out.println("hello,jsp~");
    int i = 3;
%>
```

通过浏览器访问 `hello.jsp` 后，查看转换的 `hello_jsp.java` 文件，i 变量定义在了 `_jspService()` 方法中

<img src="D:/download/downloadFromMicsoft/day10-JSP/ppt/assets/image-20210818123606231.png" alt="image-20210818123606231" style="zoom:80%;" />

在 `hello.jsp` 中书写

```jsp
<%="hello"%>
<%=i%>
```

通过浏览器访问 `hello.jsp` 后，查看转换的 `hello_jsp.java` 文件，该脚本的内容被放在了 `out.print()` 中，作为参数

<img src="D:/download/downloadFromMicsoft/day10-JSP/ppt/assets/image-20210818123820571.png" alt="image-20210818123820571" style="zoom:80%;" />

在 `hello.jsp` 中书写

```jsp
<%!
    void  show(){}
	String name = "zhangsan";
%>
```

通过浏览器访问 `hello.jsp` 后，查看转换的 `hello_jsp.java` 文件，该脚本的内容被放在了成员位置

<img src="D:/download/downloadFromMicsoft/day10-JSP/ppt/assets/image-20210818123946272.png" alt="image-20210818123946272" style="zoom:80%;" />

### 4.2  案例

#### 4.2.1  需求

使用JSP脚本展示品牌数据

<img src="D:/download/downloadFromMicsoft/day10-JSP/ppt/assets/image-20210818125203390.png" alt="image-20210818125203390" style="zoom:80%;" />

说明：

* 在资料 `资料\1. JSP案例素材` 中提供了 `brand.html` 静态页面
* 在该案例中数据不从数据库中查询，而是在 JSP 页面上写死

#### 4.2.2  实现

* 将资料 `资料\1. JSP案例素材` 中的 `Brand.java` 文件放置到项目的 `com.itheima.pojo` 包下

* 在项目的 `webapp` 中创建 `brand.jsp` ，并将 `brand.html`页面中的内容拷贝过来。`brand.jsp` 内容如下

  ```jsp
  <%@ page contentType="text/html;charset=UTF-8" language="java" %>
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>Title</title>
  </head>
  <body>
  <input type="button" value="新增"><br>
  <hr>
      <table border="1" cellspacing="0" width="800">
          <tr>
              <th>序号</th>
              <th>品牌名称</th>
              <th>企业名称</th>
              <th>排序</th>
              <th>品牌介绍</th>
              <th>状态</th>
              <th>操作</th>
  
          </tr>
          <tr align="center">
              <td>1</td>
              <td>三只松鼠</td>
              <td>三只松鼠</td>
              <td>100</td>
              <td>三只松鼠，好吃不上火</td>
              <td>启用</td>
              <td><a href="#">修改</a> <a href="#">删除</a></td>
          </tr>
  
          <tr align="center">
              <td>2</td>
              <td>优衣库</td>
              <td>优衣库</td>
              <td>10</td>
              <td>优衣库，服适人生</td>
              <td>禁用</td>
  
              <td><a href="#">修改</a> <a href="#">删除</a></td>
          </tr>
  
          <tr align="center">
              <td>3</td>
              <td>小米</td>
              <td>小米科技有限公司</td>
              <td>1000</td>
              <td>为发烧而生</td>
              <td>启用</td>
  
              <td><a href="#">修改</a> <a href="#">删除</a></td>
          </tr>
      </table>
  </body>
  </html>
  ```

  现在页面中的数据都是假数据。

* 在 `brand.jsp` 中准备一些数据

  ```jsp
  <%
      // 查询数据库
      List<Brand> brands = new ArrayList<Brand>();
      brands.add(new Brand(1,"三只松鼠","三只松鼠",100,"三只松鼠，好吃不上火",1));
      brands.add(new Brand(2,"优衣库","优衣库",200,"优衣库，服适人生",0));
      brands.add(new Brand(3,"小米","小米科技有限公司",1000,"为发烧而生",1));
  %>
  ```

  > ==注意：==这里的类是需要导包的

* 将 `brand.jsp` 页面中的 `table` 标签中的数据改为动态的

  ```jsp
  <table border="1" cellspacing="0" width="800">
      <tr>
          <th>序号</th>
          <th>品牌名称</th>
          <th>企业名称</th>
          <th>排序</th>
          <th>品牌介绍</th>
          <th>状态</th>
          <th>操作</th>
  
      </tr>
      
      <%
       for (int i = 0; i < brands.size(); i++) {
           //获取集合中的 每一个 Brand 对象
           Brand brand = brands.get(i);
       }
      %>
      <tr align="center">
          <td>1</td>
          <td>三只松鼠</td>
          <td>三只松鼠</td>
          <td>100</td>
          <td>三只松鼠，好吃不上火</td>
          <td>启用</td>
          <td><a href="#">修改</a> <a href="#">删除</a></td>
      </tr>
  </table>
  ```

  上面的for循环需要将 `tr` 标签包裹起来，这样才能实现循环的效果，代码改进为

  ```jsp
  <table border="1" cellspacing="0" width="800">
      <tr>
          <th>序号</th>
          <th>品牌名称</th>
          <th>企业名称</th>
          <th>排序</th>
          <th>品牌介绍</th>
          <th>状态</th>
          <th>操作</th>
  
      </tr>
      
      <%
       for (int i = 0; i < brands.size(); i++) {
           //获取集合中的 每一个 Brand 对象
           Brand brand = brands.get(i);
      %>
      	 <tr align="center">
              <td>1</td>
              <td>三只松鼠</td>
              <td>三只松鼠</td>
              <td>100</td>
              <td>三只松鼠，好吃不上火</td>
              <td>启用</td>
              <td><a href="#">修改</a> <a href="#">删除</a></td>
          </tr>
      <%
       }
      %>
     
  </table>
  ```

  > 注意：<%%> 里面写的是 Java 代码，而外边写的是 HTML 标签

  上面代码中的 `td` 标签中的数据都需要是动态的，所以还需要改进

  ```jsp
  <table border="1" cellspacing="0" width="800">
      <tr>
          <th>序号</th>
          <th>品牌名称</th>
          <th>企业名称</th>
          <th>排序</th>
          <th>品牌介绍</th>
          <th>状态</th>
          <th>操作</th>
  
      </tr>
      
      <%
       for (int i = 0; i < brands.size(); i++) {
           //获取集合中的 每一个 Brand 对象
           Brand brand = brands.get(i);
      %>
      	 <tr align="center">
              <td><%=brand.getId()%></td>
              <td><%=brand.getBrandName()%></td>
              <td><%=brand.getCompanyName()%></td>
              <td><%=brand.getOrdered()%></td>
              <td><%=brand.getDescription()%></td>
              <td><%=brand.getStatus() == 1 ? "启用":"禁用"%></td>
              <td><a href="#">修改</a> <a href="#">删除</a></td>
          </tr>
      <%
       }
      %>
     
  </table>
  ```

#### 4.2.3  成品代码

```jsp
<%@ page import="com.itheima.pojo.Brand" %>
<%@ page import="java.util.List" %>
<%@ page import="java.util.ArrayList" %>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>

<%
    // 查询数据库
    List<Brand> brands = new ArrayList<Brand>();
    brands.add(new Brand(1,"三只松鼠","三只松鼠",100,"三只松鼠，好吃不上火",1));
    brands.add(new Brand(2,"优衣库","优衣库",200,"优衣库，服适人生",0));
    brands.add(new Brand(3,"小米","小米科技有限公司",1000,"为发烧而生",1));

%>


<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<input type="button" value="新增"><br>
<hr>
<table border="1" cellspacing="0" width="800">
    <tr>
        <th>序号</th>
        <th>品牌名称</th>
        <th>企业名称</th>
        <th>排序</th>
        <th>品牌介绍</th>
        <th>状态</th>
        <th>操作</th>
    </tr>
    <%
        for (int i = 0; i < brands.size(); i++) {
            Brand brand = brands.get(i);
    %>

    <tr align="center">
        <td><%=brand.getId()%></td>
        <td><%=brand.getBrandName()%></td>
        <td><%=brand.getCompanyName()%></td>
        <td><%=brand.getOrdered()%></td>
        <td><%=brand.getDescription()%></td>
		<td><%=brand.getStatus() == 1 ? "启用":"禁用"%></td>
        <td><a href="#">修改</a> <a href="#">删除</a></td>
    </tr>

    <%
        }
    %>
</table>
</body>
</html>
```

#### 4.2.4  测试

在浏览器地址栏输入 `http://localhost:8080/jsp-demo/brand.jsp` ，页面展示效果如下

<img src="D:/download/downloadFromMicsoft/day10-JSP/ppt/assets/image-20210818145450748.png" alt="image-20210818145450748" style="zoom:70%;" />

### 4.3  JSP 缺点

通过上面的案例，可以看到 JSP 的很多缺点。

由于 JSP页面内，既可以定义 HTML 标签，又可以定义 Java代码，造成了以下问题：

* 书写麻烦：特别是复杂的页面

  既要写 HTML 标签，还要写 Java 代码

* 阅读麻烦

  上面案例的代码，相信你后期再看这段代码时还需要花费很长的时间去梳理

* 复杂度高：运行需要依赖于各种环境，JRE，JSP容器，JavaEE…

* 占内存和磁盘：JSP会自动生成.java和.class文件占磁盘，运行的是.class文件占内存

* 调试困难：出错后，需要找到自动生成的.java文件进行调试

* 不利于团队协作：前端人员不会 Java，后端人员不精 HTML

  如果页面布局发生变化，前端工程师对静态页面进行修改，然后再交给后端工程师，由后端工程师再将该页面改为 JSP 页面

由于上述的问题， ==JSP 已逐渐退出历史舞台，==以后开发更多的是使用 ==HTML +  Ajax== 来替代。Ajax 是后续会重点学习的技术。有个这个技术后，前端工程师负责前端页面开发，而后端工程师只负责前端代码开发。下来对技术的发展进行简单的说明

<img src="D:/download/downloadFromMicsoft/day10-JSP/ppt/assets/image-20210818150346332.png" alt="image-20210818150346332" style="zoom:80%;" />

1. 第一阶段：使用 `servlet` 即实现逻辑代码编写，也对页面进行拼接。这种模式之前也接触过

2. 第二阶段：随着技术的发展，出现了 `JSP` ，人们发现 `JSP` 使用起来比 `Servlet` 方便很多，但是还是要在 `JSP` 中嵌套 `Java` 代码，也不利于后期的维护

3. 第三阶段：使用 `Servlet` 进行逻辑代码开发，而使用 `JSP` 进行数据展示

   <img src="D:/download/downloadFromMicsoft/day10-JSP/ppt/assets/image-20210818151232955.png" alt="image-20210818151232955" style="zoom:67%;" />

4. 第四阶段：使用 `servlet` 进行后端逻辑代码开发，而使用 `HTML` 进行数据展示。而这里面就存在问题，`HTML` 是静态页面，怎么进行动态数据展示呢？这就是 `ajax` 的作用了。

那既然 JSP 已经逐渐的退出历史舞台，那为什么还要学习 `JSP` 呢？原因有两点：

* 一些公司可能有些老项目还在用 `JSP` ，所以要求必须动 `JSP`
* 如果不经历这些复杂的过程，就不能体现后面阶段开发的简单

接下来来学习第三阶段，使用 `EL表达式` 和 `JSTL` 标签库替换 `JSP` 中的 `Java` 代码。

## 5，EL 表达式

### 5.1  概述

EL（全称Expression Language ）表达式语言，用于简化 JSP 页面内的 Java 代码。

EL 表达式的主要作用是 ==获取数据==。其实就是从域对象中获取数据，然后将数据展示在页面上。

而 EL 表达式的语法也比较简单，==${expression}== 。例如：${brands} 就是获取域中存储的 key 为 brands 的数据。

### 5.2  代码演示

* 定义servlet，在 servlet 中封装一些数据并存储到 request 域对象中并转发到 `el-demo.jsp` 页面。

  ```java
  @WebServlet("/demo1")
  public class ServletDemo1 extends HttpServlet {
      @Override
      protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
          //1. 准备数据
          List<Brand> brands = new ArrayList<Brand>();
          brands.add(new Brand(1,"三只松鼠","三只松鼠",100,"三只松鼠，好吃不上火",1));
          brands.add(new Brand(2,"优衣库","优衣库",200,"优衣库，服适人生",0));
          brands.add(new Brand(3,"小米","小米科技有限公司",1000,"为发烧而生",1));
  
          //2. 存储到request域中
          request.setAttribute("brands",brands);
  
          //3. 转发到 el-demo.jsp
          request.getRequestDispatcher("/el-demo.jsp").forward(request,response);
      }
  
      @Override
      protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
          this.doGet(request, response);
      }
  }
  ```

  > ==注意：== 此处需要用转发，因为转发才可以使用 request 对象作为域对象进行数据共享

* 在 `el-demo.jsp` 中通过 EL表达式 获取数据

  ```jsp
  <%@ page contentType="text/html;charset=UTF-8" language="java" %>
  <html>
  <head>
      <title>Title</title>
  </head>
  <body>
      ${brands}
  </body>
  </html>
  ```

* 在浏览器的地址栏输入 `http://localhost:8080/jsp-demo/demo1` ，页面效果如下：

  <img src="D:/download/downloadFromMicsoft/day10-JSP/ppt/assets/image-20210818152536484.png" alt="image-20210818152536484" style="zoom:80%;" />

### 5.3  域对象

JavaWeb中有四大域对象，分别是：

* page：当前页面有效
* request：当前请求有效
* session：当前会话有效
* application：当前应用有效

el 表达式获取数据，会依次从这4个域中寻找，直到找到为止。而这四个域对象的作用范围如下图所示

<img src="D:/download/downloadFromMicsoft/day10-JSP/ppt/assets/image-20210818152857407.png" alt="image-20210818152857407" style="zoom:60%;" />

例如： ${brands}，el 表达式获取数据，会先从page域对象中获取数据，如果没有再到 requet 域对象中获取数据，如果再没有再到 session 域对象中获取，如果还没有才会到 application 中获取数据。

## 6，JSTL标签

！！！！使用jstl与el表达式共同写前端页面

### 6.1  概述

JSP标准标签库(Jsp Standarded Tag Library) ，使用标签取代JSP页面上的Java代码。如下代码就是JSTL标签

```jsp
<c:if test="${flag == 1}">
    男
</c:if>
<c:if test="${flag == 2}">
    女
</c:if>
```

上面代码看起来是不是比 JSP 中嵌套 Java 代码看起来舒服好了。而且前端工程师对标签是特别敏感的，他们看到这段代码是能看懂的。

JSTL 提供了很多标签，如下图

<img src="D:/download/downloadFromMicsoft/day10-JSP/ppt/assets/image-20210818153646575.png" alt="image-20210818153646575" style="zoom:80%;" />

只对两个最常用的标签进行讲解，`<c:forEach>` 标签和 `<c:if>` 标签。



JSTL 使用也是比较简单的，分为如下步骤：

* 导入坐标

  ```xml
  <dependency>
      <groupId>jstl</groupId>
      <artifactId>jstl</artifactId>
      <version>1.2</version>
  </dependency>
  <dependency>
      <groupId>taglibs</groupId>
      <artifactId>standard</artifactId>
      <version>1.1.2</version>
  </dependency>
  ```

* 在JSP页面上引入JSTL标签库

  ```jsp
  <%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %> 
  ```

* 使用标签

### 6.2  if 标签

`<c:if>`：相当于 if 判断

* 属性：test，用于定义条件表达式

```jsp
<c:if test="${flag == 1}">
    男
</c:if>
<c:if test="${flag == 2}">
    女
</c:if>
```

**代码演示：**

* 定义一个 `servlet` ，在该 `servlet` 中向 request 域对象中添加 键是 `status` ，值为 `1` 的数据

  ```java
  @WebServlet("/demo2")
  public class ServletDemo2 extends HttpServlet {
      @Override
      protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
          //1. 存储数据到request域中
          request.setAttribute("status",1);
  
          //2. 转发到 jstl-if.jsp
          数据request.getRequestDispatcher("/jstl-if.jsp").forward(request,response);
      }
  
      @Override
      protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
          this.doGet(request, response);
      }
  }
  ```

* 定义 `jstl-if.jsp` 页面，在该页面使用 `<c:if>` 标签

  ```jsp
  <%@ page contentType="text/html;charset=UTF-8" language="java" %>
  <%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
  <html>
  <head>
      <title>Title</title>
  </head>
  <body>
      <%--
          c:if：来完成逻辑判断，替换java  if else
      --%>
      <c:if test="${status ==1}">
          启用
      </c:if>
  
      <c:if test="${status ==0}">
          禁用
      </c:if>
  </body>
  </html>
  ```

  > ==注意：== 在该页面已经要引入 JSTL核心标签库
  >
  > `<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>`

### 6.3  forEach 标签

`<c:forEach>`：相当于 for 循环。java中有增强for循环和普通for循环，JSTL 中的 `<c:forEach>` 也有两种用法

#### 6.3.1  用法一

类似于 Java 中的增强for循环。涉及到的 `<c:forEach>` 中的属性如下

* items：被遍历的容器

* var：遍历产生的临时变量

* varStatus：遍历状态对象

如下代码，是从域对象中获取名为 brands 数据，该数据是一个集合；遍历遍历，并给该集合中的每一个元素起名为 `brand`，是 Brand对象。在循环里面使用 EL表达式获取每一个Brand对象的属性值

```jsp
<c:forEach items="${brands}" var="brand">
    <tr align="center">
        <td>${brand.id}</td>
        <td>${brand.brandName}</td>
        <td>${brand.companyName}</td>
        <td>${brand.description}</td>
    </tr>
</c:forEach>
```

**代码演示：**

* `servlet` 还是使用之前的名为 `ServletDemo1` 。

* 定义名为 `jstl-foreach.jsp` 页面，内容如下：

  ```jsp
  <%@ page contentType="text/html;charset=UTF-8" language="java" %>
  <%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
  
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>Title</title>
  </head>
  <body>
  <input type="button" value="新增"><br>
  <hr>
  <table border="1" cellspacing="0" width="800">
      <tr>
          <th>序号</th>
          <th>品牌名称</th>
          <th>企业名称</th>
          <th>排序</th>
          <th>品牌介绍</th>
          <th>状态</th>
          <th>操作</th>
      </tr>
  
      <c:forEach items="${brands}" var="brand" varStatus="status">
          <tr align="center">
              <%--<td>${brand.id}</td>--%>
              <td>${status.count}</td>
              <td>${brand.brandName}</td>
              <td>${brand.companyName}</td>
              <td>${brand.ordered}</td>
              <td>${brand.description}</td>
              <c:if test="${brand.status == 1}">
                  <td>启用</td>
              </c:if>
              <c:if test="${brand.status != 1}">
                  <td>禁用</td>
              </c:if>
              <td><a href="#">修改</a> <a href="#">删除</a></td>
          </tr>
      </c:forEach>
  </table>
  </body>
  </html>
  ```

#### 6.3.2  用法二

类似于 Java 中的普通for循环。涉及到的 `<c:forEach>` 中的属性如下

* begin：开始数

* end：结束数

* step：步长

实例代码：

从0循环到10，变量名是 `i` ，每次自增1

```jsp
<c:forEach begin="0" end="10" step="1" var="i">
    ${i}
</c:forEach>
```

## 7，MVC模式和三层架构

MVC 模式和三层架构是一些理论的知识，将来使用了它们进行代码开发会让代码维护性和扩展性更好。

### 7.1  MVC模式

MVC 是一种分层开发的模式，其中：

* M：Model，业务模型，处理业务

* V：View，视图，界面展示

* C：Controller，控制器，处理请求，调用模型和视图

<img src="D:/download/downloadFromMicsoft/day10-JSP/ppt/assets/image-20210818163348642.png" alt="image-20210818163348642" style="zoom:70%;" />

控制器（serlvlet）用来接收浏览器发送过来的请求，控制器调用模型（JavaBean）来获取数据，比如从数据库查询数据；控制器获取到数据后再交由视图（JSP）进行数据展示。

**MVC 好处：**

* 职责单一，互不影响。每个角色做它自己的事，各司其职。

* 有利于分工协作。

* 有利于组件重用

### 7.2  三层架构

三层架构是将的项目分成了三个层面，分别是 `表现层`、`业务逻辑层`、`数据访问层`。

<img src="D:/download/downloadFromMicsoft/day10-JSP/ppt/assets/image-20210818164301154.png" alt="image-20210818164301154" style="zoom:60%;" />

* 数据访问层：对数据库的CRUD基本操作
* 业务逻辑层：对业务逻辑进行封装，组合数据访问层层中基本功能，形成复杂的业务逻辑功能。例如 `注册业务功能` ，会先调用 `数据访问层` 的 `selectByName()` 方法判断该用户名是否存在，如果不存在再调用 `数据访问层` 的 `insert()` 方法进行数据的添加操作
* 表现层：接收请求，封装数据，调用业务逻辑层，响应数据

而整个流程是，浏览器发送请求，表现层的Servlet接收请求并调用业务逻辑层的方法进行业务逻辑处理，而业务逻辑层方法调用数据访问层方法进行数据的操作，依次返回到serlvet，然后servlet将数据交由 JSP 进行展示。

三层架构的每一层都有特有的包名称：

* 表现层： `com.itheima.controller` 或者 `com.itheima.web`
* 业务逻辑层：`com.itheima.service`
* 数据访问层：`com.itheima.dao` 或者 `com.itheima.mapper`

后期还会学习一些框架，不同的框架是对不同层进行封装的

<img src="D:/download/downloadFromMicsoft/day10-JSP/ppt/assets/image-20210818165439826.png" alt="image-20210818165439826" style="zoom:60%;" />

### 7.3  MVC 和 三层架构

通过 MVC 和 三层架构 的学习，有些人肯定混淆了。那他们有什么区别和联系？

<img src="D:/download/downloadFromMicsoft/day10-JSP/ppt/assets/image-20210818165808589.png" alt="image-20210818165808589" style="zoom:60%;" />

如上图上半部分是 MVC 模式，上图下半部分是三层架构。 `MVC 模式` 中的 C（控制器）和 V（视图）就是 `三层架构` 中的表现层，而 `MVC 模式` 中的 M（模型）就是 `三层架构` 中的 业务逻辑层 和 数据访问层。

可以将 `MVC 模式` 理解成是一个大的概念，而 `三层架构` 是对 `MVC 模式` 实现架构的思想。 那么以后按照要求将不同层的代码写在不同的包下，每一层里功能职责做到单一，将来如果将表现层的技术换掉，而业务逻辑层和数据访问层的代码不需要发生变化。

## 8，案例

**需求：完成品牌数据的增删改查操作**

<img src="D:/download/downloadFromMicsoft/day10-JSP/ppt/assets/image-20210818171702401.png" alt="image-20210818171702401" style="zoom:70%;" />

这个功能之前一直在做，而这个案例是将今天学习的所有的内容（包含 MVC模式 和 三层架构）进行应用，并将整个流程贯穿起来。

### 8.1  环境准备

环境准备工作，分以下步骤实现：

* 创建新的模块 brand_demo，引入坐标

* 创建三层架构的包结构

* 数据库表 tb_brand

* 实体类 Brand

* MyBatis 基础环境

  * Mybatis-config.xml

  * BrandMapper.xml

  * BrandMapper接口

#### 8.1.1  创建工程

创建新的模块 brand_demo，引入坐标。只要分析出要用到哪儿些技术，那么需要哪儿些坐标也就明确了

* 需要操作数据库。mysql的驱动包
* 要使用mybatis框架。mybaits的依赖包
* web项目需要用到servlet和jsp。servlet和jsp的依赖包
* 需要使用 jstl 进行数据展示。jstl的依赖包

`pom.xml` 内容如下：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <groupId>org.example</groupId>
    <artifactId>brand-demo</artifactId>
    <version>1.0-SNAPSHOT</version>
    <packaging>war</packaging>

    <properties>
        <maven.compiler.source>8</maven.compiler.source>
        <maven.compiler.target>8</maven.compiler.target>
    </properties>

    <dependencies>
        <!-- mybatis -->
        <dependency>
            <groupId>org.mybatis</groupId>
            <artifactId>mybatis</artifactId>
            <version>3.5.5</version>
        </dependency>

        <!--mysql-->
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>5.1.34</version>
        </dependency>

        <!--servlet-->
        <dependency>
            <groupId>javax.servlet</groupId>
            <artifactId>javax.servlet-api</artifactId>
            <version>3.1.0</version>
            <scope>provided</scope>
        </dependency>

        <!--jsp-->
        <dependency>
            <groupId>javax.servlet.jsp</groupId>
            <artifactId>jsp-api</artifactId>
            <version>2.2</version>
            <scope>provided</scope>
        </dependency>

        <!--jstl-->
        <dependency>
            <groupId>jstl</groupId>
            <artifactId>jstl</artifactId>
            <version>1.2</version>
        </dependency>
        <dependency>
            <groupId>taglibs</groupId>
            <artifactId>standard</artifactId>
            <version>1.1.2</version>
        </dependency>
    </dependencies>

    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.tomcat.maven</groupId>
                <artifactId>tomcat7-maven-plugin</artifactId>
                <version>2.2</version>
            </plugin>
        </plugins>
    </build>
</project>
```

#### 8.1.2  创建包

创建不同的包结构，用来存储不同的类。包结构如下

<img src="D:/download/downloadFromMicsoft/day10-JSP/ppt/assets/image-20210818173155335.png" alt="image-20210818173155335" style="zoom:80%;" />

#### 8.1.3  创建表

```sql
-- 删除tb_brand表
drop table if exists tb_brand;
-- 创建tb_brand表
create table tb_brand
(
    -- id 主键
    id           int primary key auto_increment,
    -- 品牌名称
    brand_name   varchar(20),
    -- 企业名称
    company_name varchar(20),
    -- 排序字段
    ordered      int,
    -- 描述信息
    description  varchar(100),
    -- 状态：0：禁用  1：启用
    status       int
);
-- 添加数据
insert into tb_brand (brand_name, company_name, ordered, description, status)
values ('三只松鼠', '三只松鼠股份有限公司', 5, '好吃不上火', 0),
       ('华为', '华为技术有限公司', 100, '华为致力于把数字世界带入每个人、每个家庭、每个组织，构建万物互联的智能世界', 1),
       ('小米', '小米科技有限公司', 50, 'are you ok', 1);
```

#### 8.1.4  创建实体类

在 `pojo` 包下创建名为 `Brand` 的类。

```java
public class Brand {
    // id 主键
    private Integer id;
    // 品牌名称
    private String brandName;
    // 企业名称
    private String companyName;
    // 排序字段
    private Integer ordered;
    // 描述信息
    private String description;
    // 状态：0：禁用  1：启用
    private Integer status;


    public Brand() {
    }

    public Brand(Integer id, String brandName, String companyName, String description) {
        this.id = id;
        this.brandName = brandName;
        this.companyName = companyName;
        this.description = description;
    }

    public Brand(Integer id, String brandName, String companyName, Integer ordered, String description, Integer status) {
        this.id = id;
        this.brandName = brandName;
        this.companyName = companyName;
        this.ordered = ordered;
        this.description = description;
        this.status = status;
    }

    public Integer getId() {
        return id;
    }

    public void setId(Integer id) {
        this.id = id;
    }

    public String getBrandName() {
        return brandName;
    }

    public void setBrandName(String brandName) {
        this.brandName = brandName;
    }

    public String getCompanyName() {
        return companyName;
    }

    public void setCompanyName(String companyName) {
        this.companyName = companyName;
    }

    public Integer getOrdered() {
        return ordered;
    }

    public void setOrdered(Integer ordered) {
        this.ordered = ordered;
    }

    public String getDescription() {
        return description;
    }

    public void setDescription(String description) {
        this.description = description;
    }

    public Integer getStatus() {
        return status;
    }

    public void setStatus(Integer status) {
        this.status = status;
    }

    @Override
    public String toString() {
        return "Brand{" +
                "id=" + id +
                ", brandName='" + brandName + '\'' +
                ", companyName='" + companyName + '\'' +
                ", ordered=" + ordered +
                ", description='" + description + '\'' +
                ", status=" + status +
                '}';
    }
}

```

#### 8.1.5   准备mybatis环境

定义核心配置文件 `Mybatis-config.xml` ，并将该文件放置在 `resources` 下

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
    <!--起别名-->
    <typeAliases>
        <package name="com.itheima.pojo"/>
    </typeAliases>

    <environments default="development">
        <environment id="development">
            <transactionManager type="JDBC"/>
            <dataSource type="POOLED">
                <property name="driver" value="com.mysql.jdbc.Driver"/>
                <property name="url" value="jdbc:mysql:///db1?useSSL=false&amp;useServerPrepStmts=true"/>
                <property name="username" value="root"/>
                <property name="password" value="1234"/>
            </dataSource>
        </environment>
    </environments>
    <mappers>
        <!--扫描mapper-->
        <package name="com.itheima.mapper"/>
    </mappers>
</configuration>
```

在 `resources` 下创建放置映射配置文件的目录结构 `com/itheima/mapper`，并在该目录下创建映射配置文件 `BrandMapper.xml`

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.itheima.mapper.BrandMapper">
    
</mapper>
```

### 8.2  查询所有

![image-20210818174441917](D:/download/downloadFromMicsoft/day10-JSP/ppt/assets/image-20210818174441917.png)

当点击 `index.html` 页面中的 `查询所有` 这个超链接时，就能查询到上图右半部分的数据。

对于上述的功能，点击 `查询所有` 超链接是需要先请后端的 `servlet` ，由 `servlet` 跳转到对应的页面进行数据的动态展示。而整个流程如下图：

！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！

<img src="D:/download/downloadFromMicsoft/day10-JSP/ppt/assets/image-20210818174800783.png" alt="image-20210818174800783" style="zoom:60%;" />



![image-20220418195133716](C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220418195133716.png)

多一层Service，提高代码的复用性，将多种功能封装

#### 8.2.1  编写BrandMapper

在 `mapper` 包下创建创建 `BrandMapper` 接口，在接口中定义 `selectAll()` 方法

```java
/**
  * 查询所有
  * @return
  */
@Select("select * from tb_brand")
List<Brand> selectAll();
```

#### 8.2.2  编写工具类

在 `com.itheima` 包下创建 `utils` 包，并在该包下创建名为 `SqlSessionFactoryUtils` 工具类

```java
public class SqlSessionFactoryUtils {

    private static SqlSessionFactory sqlSessionFactory;

    static {
        //静态代码块会随着类的加载而自动执行，且只执行一次
        try {
            String resource = "mybatis-config.xml";
            InputStream inputStream = Resources.getResourceAsStream(resource);
            sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    public static SqlSessionFactory getSqlSessionFactory(){
        return sqlSessionFactory;
    }
}
```

#### 8.2.3  编写BrandService

在 `service` 包下创建 `BrandService` 类

```java
public class BrandService {
    SqlSessionFactory factory = SqlSessionFactoryUtils.getSqlSessionFactory();

    /**
     * 查询所有
     * @return
     */
    public List<Brand> selectAll(){
        //调用BrandMapper.selectAll()

        //2. 获取SqlSession
        SqlSession sqlSession = factory.openSession();
        //3. 获取BrandMapper
        BrandMapper mapper = sqlSession.getMapper(BrandMapper.class);

        //4. 调用方法
        List<Brand> brands = mapper.selectAll();

        sqlSession.close();

        return brands;
    }
}
```

#### 8.2.4  编写Servlet

在 `web` 包下创建名为 `SelectAllServlet` 的 `servlet`，该 `servlet` 的逻辑如下：

* 调用 `BrandService` 的 `selectAll()` 方法进行业务逻辑处理，并接收返回的结果
* 将上一步返回的结果存储到 `request` 域对象中
* 跳转到 `brand.jsp` 页面进行数据的展示

具体的代码如下：

```java
@WebServlet("/selectAllServlet")
public class SelectAllServlet extends HttpServlet {
    private  BrandService service = new BrandService();

    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

        //1. 调用BrandService完成查询
        List<Brand> brands = service.selectAll();
        //2. 存入request域中
        request.setAttribute("brands",brands);
        //3. 转发到brand.jsp
        request.getRequestDispatcher("/brand.jsp").forward(request,response);
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doGet(request, response);
    }
}
```

#### 8.2.5  编写brand.jsp页面

将资料 `资料\2. 品牌增删改查案例\静态页面` 下的 `brand.html` 页面拷贝到项目的 `webapp` 目录下，并将该页面改成 `brand.jsp` 页面，而 `brand.jsp` 页面在表格中使用 `JSTL` 和 `EL表达式` 从request域对象中获取名为 `brands` 的集合数据并展示出来。页面内容如下：

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<hr>
<table border="1" cellspacing="0" width="80%">
    <tr>
        <th>序号</th>
        <th>品牌名称</th>
        <th>企业名称</th>
        <th>排序</th>
        <th>品牌介绍</th>
        <th>状态</th>
        <th>操作</th>
    </tr>

    <c:forEach items="${brands}" var="brand" varStatus="status">
        <tr align="center">
            <%--<td>${brand.id}</td>--%>
            <td>${status.count}</td>
            <td>${brand.brandName}</td>
            <td>${brand.companyName}</td>
            <td>${brand.ordered}</td>
            <td>${brand.description}</td>
            <c:if test="${brand.status == 1}">
                <td>启用</td>
            </c:if>
            <c:if test="${brand.status != 1}">
                <td>禁用</td>
            </c:if>
            <td><a href="/brand-demo/selectByIdServlet?id=${brand.id}">修改</a> <a href="#">删除</a></td>
        </tr>
    </c:forEach>
</table>
</body>
</html>
```

#### 8.2.6  测试

启动服务器，并在浏览器输入 `http://localhost:8080/brand-demo/index.html`，看到如下 `查询所有` 的超链接，点击该链接就可以查询出所有的品牌数据

![image-20210818182952394](D:/download/downloadFromMicsoft/day10-JSP/ppt/assets/image-20210818182952394.png)

为什么出现这个问题呢？是因为查询到的字段名和实体类对象的属性名没有一一对应。相比看到这大家一定会解决了，就是在映射配置文件中使用 `resultMap` 标签定义映射关系。映射配置文件内容如下：

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.itheima.mapper.BrandMapper">

    <resultMap id="brandResultMap" type="brand">
        <result column="brand_name" property="brandName"></result>
        <result column="company_name" property="companyName"></result>
    </resultMap>
</mapper>
```

并且在 `BrandMapper` 接口中的 `selectAll()` 上使用 `@ResuleMap` 注解指定使用该映射

```java
/**
  * 查询所有
  * @return
  */
@Select("select * from tb_brand")
@ResultMap("brandResultMap")
List<Brand> selectAll();
```

重启服务器，再次访问就能看到想要的数据了

![image-20210819190221889](D:/download/downloadFromMicsoft/day10-JSP/ppt/assets/image-20210819190221889.png)

### 8.3  添加

![image-20210819192049571](D:/download/downloadFromMicsoft/day10-JSP/ppt/assets/image-20210819192049571.png)

上图是做 添加 功能流程。点击 `新增` 按钮后，会先跳转到 `addBrand.jsp` 新增页面，在该页面输入要添加的数据，输入完毕后点击 `提交` 按钮，需要将数据提交到后端，而后端进行数据添加操作，并重新将所有的数据查询出来。整个流程如下：

![image-20210819192737982](D:/download/downloadFromMicsoft/day10-JSP/ppt/assets/image-20210819192737982.png)

接下来根据流程来实现功能：

#### 8.3.1  编写BrandMapper方法

在 `BrandMapper` 接口，在接口中定义 `add(Brand brand)` 方法

```java
@Insert("insert into tb_brand values(null,#{brandName},#{companyName},#{ordered},#{description},#{status})")
void add(Brand brand);
```

#### 8.3.2  编写BrandService方法

在 `BrandService` 类中定义添加品牌数据方法 `add(Brand brand)`

```java
 	/**
     * 添加
     * @param brand
     */
    public void add(Brand brand){

        //2. 获取SqlSession
        SqlSession sqlSession = factory.openSession();
        //3. 获取BrandMapper
        BrandMapper mapper = sqlSession.getMapper(BrandMapper.class);

        //4. 调用方法
        mapper.add(brand);

        //提交事务
        sqlSession.commit();
        //释放资源
        sqlSession.close();
    }
```

#### 8.3.3  改进brand.jsp页面

需要在该页面表格的上面添加 `新增` 按钮

```html
<input type="button" value="新增" id="add"><br>
```

并给该按钮绑定单击事件，当点击了该按钮需要跳转到 `brand.jsp` 添加品牌数据的页面

```html
<script>
    document.getElementById("add").onclick = function (){
        location.href = "/brand-demo/addBrand.jsp";
    }
</script>
```

> ==注意：==该 `script` 标签建议放在 `body` 结束标签前面。

#### 8.3.4  编写addBrand.jsp页面

从资料 `资料\2. 品牌增删改查案例\静态页面` 中将 `addBrand.html` 页面拷贝到项目的 `webapp` 下，并改成 `addBrand.jsp` 动态页面

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <title>添加品牌</title>
</head>
<body>
<h3>添加品牌</h3>
<form action="/brand-demo/addServlet" method="post">
    品牌名称：<input name="brandName"><br>
    企业名称：<input name="companyName"><br>
    排序：<input name="ordered"><br>
    描述信息：<textarea rows="5" cols="20" name="description"></textarea><br>
    状态：
    <input type="radio" name="status" value="0">禁用
    <input type="radio" name="status" value="1">启用<br>

    <input type="submit" value="提交">
</form>
</body>
</html>
```

#### 8.3.5  编写servlet

在 `web` 包下创建 `AddServlet` 的 `servlet`，该 `servlet` 的逻辑如下:

* 设置处理post请求乱码的字符集
* 接收客户端提交的数据
* 将接收到的数据封装到 `Brand` 对象中
* 调用 `BrandService` 的`add()` 方法进行添加的业务逻辑处理
* 跳转到 `selectAllServlet` 资源重新查询数据

具体的代码如下：

```java
@WebServlet("/addServlet")
public class AddServlet extends HttpServlet {
    private BrandService service = new BrandService();


    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

        //处理POST请求的乱码问题
        request.setCharacterEncoding("utf-8");

        //1. 接收表单提交的数据，封装为一个Brand对象
        String brandName = request.getParameter("brandName");
        String companyName = request.getParameter("companyName");
        String ordered = request.getParameter("ordered");
        String description = request.getParameter("description");
        String status = request.getParameter("status");

        //封装为一个Brand对象
        Brand brand = new Brand();
        brand.setBrandName(brandName);
        brand.setCompanyName(companyName);
        brand.setOrdered(Integer.parseInt(ordered));
        brand.setDescription(description);
        brand.setStatus(Integer.parseInt(status));

        //2. 调用service 完成添加
        service.add(brand);

        //3. 转发到查询所有Servlet
        request.getRequestDispatcher("/selectAllServlet").forward(request,response);
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doGet(request, response);
    }
}
```

#### 8.3.6  测试

 点击 `brand.jsp` 页面的 `新增` 按钮，会跳转到 `addBrand.jsp`页面

<img src="D:/download/downloadFromMicsoft/day10-JSP/ppt/assets/image-20210819220701121.png" alt="image-20210819220701121" style="zoom:70%;" />

点击 `提交` 按钮，就能看到如下页面，里面就包含刚添加的数据

![image-20210819220738074](D:/download/downloadFromMicsoft/day10-JSP/ppt/assets/image-20210819220738074.png)

### 8.4  修改 

![image-20210819223202473](D:/download/downloadFromMicsoft/day10-JSP/ppt/assets/image-20210819223202473.png)

点击每条数据后面的 `编辑` 按钮会跳转到修改页面，如下图：

![image-20210819223314230](D:/download/downloadFromMicsoft/day10-JSP/ppt/assets/image-20210819223314230.png)

在该修改页面可以看到将 `编辑` 按钮所在行的数据 ==回显== 到表单，然后需要修改那个数据在表单中进行修改，然后点击 `提交` 的按钮将数据提交到后端，后端再将数据存储到数据库中。

从上面的例子知道 `修改` 功能需要从两方面进行实现，数据回显和修改操作。

#### 8.4.1  回显数据

![image-20210819223830713](D:/download/downloadFromMicsoft/day10-JSP/ppt/assets/image-20210819223830713.png)

上图就是回显数据的效果。要实现这个效果，那当点击 `修改` 按钮时不能直接跳转到 `update.jsp` 页面，而是需要先带着当前行数据的 `id` 请求后端程序，后端程序根据 `id` 查询数据，将数据存储到域对象中跳转到 `update.jsp` 页面进行数据展示。整体流程如下

<img src="D:/download/downloadFromMicsoft/day10-JSP/ppt/assets/image-20210819224243778.png" alt="image-20210819224243778" style="zoom:70%;" />

##### 8.4.1.1  编写BrandMapper方法

在 `BrandMapper` 接口，在接口中定义 `selectById(int id)` 方法

```java
	/**
     * 根据id查询
     * @param id
     * @return
     */
    @Select("select * from tb_brand where id = #{id}")
    @ResultMap("brandResultMap")
    Brand selectById(int id);
```

##### 8.4.1.2  编写BrandService方法

在 `BrandService` 类中定义根据id查询数据方法 `selectById(int id)` 

```java
    /**
     * 根据id查询
     * @return
     */
    public Brand selectById(int id){
        //调用BrandMapper.selectAll()
        //2. 获取SqlSession
        SqlSession sqlSession = factory.openSession();
        //3. 获取BrandMapper
        BrandMapper mapper = sqlSession.getMapper(BrandMapper.class);
        //4. 调用方法
        Brand brand = mapper.selectById(id);
        sqlSession.close();
        return brand;
    }
```

##### 8.4.1.3  编写servlet

在 `web` 包下创建 `SelectByIdServlet` 的 `servlet`，该 `servlet` 的逻辑如下:

* 获取请求数据 `id`
* 调用 `BrandService` 的 `selectById()` 方法进行数据查询的业务逻辑
* 将查询到的数据存储到 request 域对象中
* 跳转到 `update.jsp` 页面进行数据真实

具体代码如下：

```java
@WebServlet("/selectByIdServlet")
public class SelectByIdServlet extends HttpServlet {
    private  BrandService service = new BrandService();

    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //1. 接收id
        String id = request.getParameter("id");
        //2. 调用service查询
        Brand brand = service.selectById(Integer.parseInt(id));
        //3. 存储到request中
        request.setAttribute("brand",brand);
        //4. 转发到update.jsp
        request.getRequestDispatcher("/update.jsp").forward(request,response);
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doGet(request, response);
    }
}
```

##### 8.4.1.4  编写update.jsp页面

拷贝 `addBrand.jsp` 页面，改名为 `update.jsp` 并做出以下修改：

* `title` 标签内容改为 `修改品牌`

* `form` 标签的 `action` 属性值改为 `/brand-demo/updateServlet`

* `input` 标签要进行数据回显，需要设置 `value` 属性

  ```jsp
  品牌名称：<input name="brandName" value="${brand.brandName}"><br>
  企业名称：<input name="companyName" value="${brand.companyName}"><br>
  排序：<input name="ordered" value="${brand.ordered}"><br>
  ```

* `textarea` 标签要进行数据回显，需要在标签体中使用 `EL表达式`

  ```jsp
  描述信息：<textarea rows="5" cols="20" name="description">${brand.description} </textarea><br>
  ```

* 单选框使用 `if` 标签需要判断 `brand.status` 的值是 1 还是 0 在指定的单选框上使用 `checked` 属性，表示被选中状态

  ```jsp
  状态：
  <c:if test="${brand.status == 0}">
      <input type="radio" name="status" value="0" checked>禁用
      <input type="radio" name="status" value="1">启用<br>
  </c:if>
  
  <c:if test="${brand.status == 1}">
      <input type="radio" name="status" value="0" >禁用
      <input type="radio" name="status" value="1" checked>启用<br>
  </c:if>
  ```

综上，`update.jsp` 代码如下：

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>修改品牌</title>
</head>
<body>
<h3>修改品牌</h3>
<form action="/brand-demo/updateServlet" method="post">

    品牌名称：<input name="brandName" value="${brand.brandName}"><br>
    企业名称：<input name="companyName" value="${brand.companyName}"><br>
    排序：<input name="ordered" value="${brand.ordered}"><br>
    描述信息：<textarea rows="5" cols="20" name="description">${brand.description} </textarea><br>
    状态：
    <c:if test="${brand.status == 0}">
        <input type="radio" name="status" value="0" checked>禁用
        <input type="radio" name="status" value="1">启用<br>
    </c:if>

    <c:if test="${brand.status == 1}">
        <input type="radio" name="status" value="0" >禁用
        <input type="radio" name="status" value="1" checked>启用<br>
    </c:if>

    <input type="submit" value="提交">
</form>
</body>
</html>
```

#### 8.4.2  修改数据

做完回显数据后，接下来要做修改数据了，而下图是修改数据的效果：

![image-20210819225948187](D:/download/downloadFromMicsoft/day10-JSP/ppt/assets/image-20210819225948187.png)

在修改页面进行数据修改，点击 `提交` 按钮，会将数据提交到后端程序，后端程序会对表中的数据进行修改操作，然后重新进行数据的查询操作。整体流程如下：

<img src="D:/download/downloadFromMicsoft/day10-JSP/ppt/assets/image-20210819230242938.png" alt="image-20210819230242938" style="zoom:70%;" />

##### 8.4.2.1  编写BrandMapper方法

在 `BrandMapper` 接口，在接口中定义 `update(Brand brand)` 方法

```java
/**
  * 修改
  * @param brand
  */
@Update("update tb_brand set brand_name = #{brandName},company_name = #{companyName},ordered = #{ordered},description = #{description},status = #{status} where id = #{id}")
void update(Brand brand);
```

##### 8.4.2.2  编写BrandService方法

在 `BrandService` 类中定义根据id查询数据方法 `update(Brand brand)` 

```java
	/**
     * 修改
     * @param brand
     */
    public void update(Brand brand){
        //2. 获取SqlSession
        SqlSession sqlSession = factory.openSession();
        //3. 获取BrandMapper
        BrandMapper mapper = sqlSession.getMapper(BrandMapper.class);
        //4. 调用方法
        mapper.update(brand);
        //提交事务
        sqlSession.commit();
        //释放资源
        sqlSession.close();
    }
```

##### 8.4.2.3  编写servlet

在 `web` 包下创建 `AddServlet` 的 `servlet`，该 `servlet` 的逻辑如下:

* 设置处理post请求乱码的字符集
* 接收客户端提交的数据
* 将接收到的数据封装到 `Brand` 对象中
* 调用 `BrandService` 的`update()` 方法进行添加的业务逻辑处理
* 跳转到 `selectAllServlet` 资源重新查询数据

具体的代码如下：

```java
@WebServlet("/updateServlet")
public class UpdateServlet extends HttpServlet {
    private BrandService service = new BrandService();

    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

        //处理POST请求的乱码问题
        request.setCharacterEncoding("utf-8");
        //1. 接收表单提交的数据，封装为一个Brand对象
        String id = request.getParameter("id");
        String brandName = request.getParameter("brandName");
        String companyName = request.getParameter("companyName");
        String ordered = request.getParameter("ordered");
        String description = request.getParameter("description");
        String status = request.getParameter("status");

        //封装为一个Brand对象
        Brand brand = new Brand();
        brand.setId(Integer.parseInt(id));
        brand.setBrandName(brandName);
        brand.setCompanyName(companyName);
        brand.setOrdered(Integer.parseInt(ordered));
        brand.setDescription(description);
        brand.setStatus(Integer.parseInt(status));

        //2. 调用service 完成修改
        service.update(brand);

        //3. 转发到查询所有Servlet
        request.getRequestDispatcher("/selectAllServlet").forward(request,response);
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doGet(request, response);
    }
}
```

==存在问题：update.jsp 页面提交数据时是没有携带主键数据的，而后台修改数据需要根据主键进行修改。==

针对这个问题，不希望页面将主键id展示给用户看，但是又希望在提交数据时能将主键id提交到后端。此时就想到了在学习 HTML 时学习的隐藏域，在 `update.jsp` 页面的表单中添加如下代码：

```jsp
<%--隐藏域，提交id--%>
<input type="hidden" name="id" value="${brand.id}">
```

`update.jsp` 页面的最终代码如下：

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>修改品牌</title>
</head>
<body>
<h3>修改品牌</h3>
<form action="/brand-demo/updateServlet" method="post">

    <%--隐藏域，提交id--%>
    <input type="hidden" name="id" value="${brand.id}">

    品牌名称：<input name="brandName" value="${brand.brandName}"><br>
    企业名称：<input name="companyName" value="${brand.companyName}"><br>
    排序：<input name="ordered" value="${brand.ordered}"><br>
    描述信息：<textarea rows="5" cols="20" name="description">${brand.description} </textarea><br>
    状态：
    <c:if test="${brand.status == 0}">
        <input type="radio" name="status" value="0" checked>禁用
        <input type="radio" name="status" value="1">启用<br>
    </c:if>

    <c:if test="${brand.status == 1}">
        <input type="radio" name="status" value="0" >禁用
        <input type="radio" name="status" value="1" checked>启用<br>
    </c:if>
    <input type="submit" value="提交">
</form>
</body>
</html>
```







### 案例体验

用jsp写java代码，没有代码提示，还是需要手撸，有敲错都风险

实现的视图逻辑

<img src="D:\download\downloadFromMicsoft\day10-JSP\ppt\assets\01.jpg" alt="01" style="zoom:200%;" />



# 会话技术

**今日目标** 

> * 理解什么是会话跟踪技术
>
> * 掌握Cookie的使用
> * 掌握Session的使用
> * 完善用户登录注册案例的功能

## 1，会话跟踪技术的概述

对于`会话跟踪`这四个词，需要拆开来进行解释，首先要理解什么是`会话`，然后再去理解什么是`会话跟踪`:

* 会话:用户打开浏览器，访问web服务器的资源，会话建立，直到有一方断开连接，会话结束。在一次会话中可以包含==多次==请求和响应。

  * 从浏览器发出请求到服务端响应数据给前端之后，一次会话(在浏览器和服务器之间)就被建立了
  * 会话被建立后，如果浏览器或服务端都没有被关闭，则会话就会持续建立着
  * 浏览器和服务器就可以继续使用该会话进行请求发送和响应，上述的整个过程就被称之为==会话==。

  用实际场景来理解下会话，比如在访问京东的时候，当打开浏览器进入京东首页后，浏览器和京东的服务器之间就建立了一次会话，后面的搜索商品,查看商品的详情,加入购物车等都是在这一次会话中完成。

  思考:下图中总共建立了几个会话?

  ![1629382713180](D:/download/downloadFromMicsoft/day11-会话技术/ppt/assets/1629382713180.png)

  每个浏览器都会与服务端建立了一个会话，加起来总共是==3==个会话。

* 会话跟踪:一种维护浏览器状态的方法，服务器需要识别多次请求是否来自于同一浏览器，以便在同一次会话的多次请求间==共享数据==。

  * 服务器会收到多个请求，这多个请求可能来自多个浏览器，如上图中的6个请求来自3个浏览器
  * 服务器需要用来识别请求是否来自同一个浏览器
  * 服务器用来识别浏览器的过程，这个过程就是==会话跟踪==
  * 服务器识别浏览器后就可以在同一个会话中多次请求之间来共享数据

  那么又有一个问题需要思考，一个会话中的多次请求为什么要共享数据呢?有了这个数据共享功能后能实现哪些功能呢?

  * 购物车: `加入购物车`和`去购物车结算`是两次请求，但是后面这次请求要想展示前一次请求所添加的商品，就需要用到数据共享。

    ![1629383655260](D:/download/downloadFromMicsoft/day11-会话技术/ppt/assets/1629383655260.png)

  * 页面展示用户登录信息:很多网站，登录后访问多个功能发送多次请求后，浏览器上都会有当前登录用户的信息[用户名]，比如百度、京东、码云等。

    ![1629383767654](D:/download/downloadFromMicsoft/day11-会话技术/ppt/assets/1629383767654.png)

  * 网站登录页面的`记住我`功能:当用户登录成功后，勾选`记住我`按钮后下次再登录的时候，网站就会自动填充用户名和密码，简化用户的登录操作，多次登录就会有多次请求，他们之间也涉及到共享数据

    ![1629383921990](D:/download/downloadFromMicsoft/day11-会话技术/ppt/assets/1629383921990.png)

  * 登录页面的验证码功能:生成验证码和输入验证码点击注册这也是两次请求，这两次请求的数据之间要进行对比，相同则允许注册，不同则拒绝注册，该功能的实现也需要在同一次会话中共享数据。

    ![1629384004179](D:/download/downloadFromMicsoft/day11-会话技术/ppt/assets/1629384004179.png)

通过这几个例子的讲解，相信大家对`会话追踪`技术已经有了一定的理解，该技术在实际开发中也非常重要。那么接下来就需要去学习下`会话跟踪`技术，在学习这些技术之前，需要思考:为什么现在浏览器和服务器不支持数据共享呢?

* 浏览器和服务器之间使用的是HTTP请求来进行数据传输
* HTTP协议是==无状态==的，每次浏览器向服务器请求时，服务器都会将该请求视为==新的==请求
* HTTP协议设计成无状态的目的是让每次请求之间相互独立，互不影响
* 请求与请求之间独立后，就无法实现多次请求之间的数据共享

分析完具体的原因后，那么该如何实现会话跟踪技术呢? 具体的实现方式有:

(1)客户端会话跟踪技术：==Cookie==

(2)服务端会话跟踪技术：==Session==

这两个技术都可以实现会话跟踪，它们之间最大的区别:==Cookie是存储在浏览器端而Session是存储在服务器端==

具体的学习思路为:

* CooKie的基本使用、原理、使用细节
* Session的基本使用、原理、使用细节
* Cookie和Session的综合案例

**小结**

在这节中，主要介绍了下什么是会话和会话跟踪技术，需要注意的是:

* HTTP协议是无状态的，靠HTTP协议是无法实现会话跟踪
* 想要实现会话跟踪，就需要用到Cookie和Session

这个Cookie和Session具体该如何使用，接下来就先从Cookie来学起。

## 2，Cookie

学习Cookie，主要解决下面几个问题:

* 什么是Cookie?
* Cookie如何来使用?
* Cookie是如何实现的?
* Cookie的使用注意事项有哪些?

### 2.1 Cookie的基本使用

**1.概念**

==Cookie==：客户端会话技术，将数据保存到客户端，以后每次请求都携带Cookie数据进行访问。

**2.Cookie的工作流程**

![1629386230207](D:/download/downloadFromMicsoft/day11-会话技术/ppt/assets/1629386230207.png)

* 服务端提供了两个Servlet，分别是ServletA和ServletB
* 浏览器发送HTTP请求1给服务端，服务端ServletA接收请求并进行业务处理
* 服务端ServletA在处理的过程中可以创建一个Cookie对象并将`name=zs`的数据存入Cookie
* 服务端ServletA在响应数据的时候，会把Cookie对象响应给浏览器
* 浏览器接收到响应数据，会把Cookie对象中的数据存储在浏览器内存中，此时浏览器和服务端就==建立了一次会话==
* ==在同一次会话==中浏览器再次发送HTTP请求2给服务端ServletB，浏览器会携带Cookie对象中的所有数据
* ServletB接收到请求和数据后，就可以获取到存储在Cookie对象中的数据，这样同一个会话中的多次请求之间就实现了数据共享

**3.Cookie的基本使用**

对于Cookie的使用，更关注的应该是后台代码如何操作Cookie，对于Cookie的操作主要分两大类，本别是==发送Cookie==和==获取Cookie==,对于上面这两块内容，分别该如何实现呢?

3.1 发送Cookie

* 创建Cookie对象，并设置数据

```
Cookie cookie = new Cookie("key","value");
```

* 发送Cookie到客户端：使用==response==对象

```
response.addCookie(cookie);
```

介绍完发送Cookie对应的步骤后，接下面通过一个案例来完成Cookie的发送，具体实现步骤为:

> 需求:在Servlet中生成Cookie对象并存入数据，然后将数据发送给浏览器
>
> 1.创建Maven项目,项目名称为cookie-demo，并在pom.xml添加依赖
>
> 2.编写Servlet类，名称为AServlet
>
> 3.在AServlet中创建Cookie对象，存入数据，发送给前端
>
> 4.启动测试，在浏览器查看Cookie对象中的值

(1)创建Maven项目cookie-demo，并在pom.xml添加依赖

```xml
<properties>
    <maven.compiler.source>8</maven.compiler.source>
    <maven.compiler.target>8</maven.compiler.target>
</properties>

<dependencies>
    <!--servlet-->
    <dependency>
        <groupId>javax.servlet</groupId>
        <artifactId>javax.servlet-api</artifactId>
        <version>3.1.0</version>
        <scope>provided</scope>
    </dependency>
    <!--jsp-->
    <dependency>
        <groupId>javax.servlet.jsp</groupId>
        <artifactId>jsp-api</artifactId>
        <version>2.2</version>
        <scope>provided</scope>
    </dependency>
    <!--jstl-->
    <dependency>
        <groupId>jstl</groupId>
        <artifactId>jstl</artifactId>
        <version>1.2</version>
    </dependency>
    <dependency>
        <groupId>taglibs</groupId>
        <artifactId>standard</artifactId>
        <version>1.1.2</version>
    </dependency>
</dependencies>
<build>
    <plugins>
        <plugin>
            <groupId>org.apache.tomcat.maven</groupId>
            <artifactId>tomcat7-maven-plugin</artifactId>
            <version>2.2</version>
        </plugin>
    </plugins>
</build>
```

(2)编写Servlet类，名称为AServlet

```java
@WebServlet("/aServlet")
public class AServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doGet(request, response);
    }
}
```

(3)在Servlet中创建Cookie对象，存入数据，发送给前端

```java
@WebServlet("/aServlet")
public class AServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //发送Cookie
        //1. 创建Cookie对象
        Cookie cookie = new Cookie("username","zs");
        //2. 发送Cookie，response
        response.addCookie(cookie);
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doGet(request, response);
    }
}
```

（4）启动测试，在浏览器查看Cookie对象中的值

访问`http://localhost:8080/cookie-demo/aServlet`

chrome浏览器查看Cookie的值，有两种方式,分布式:

方式一:

![1629389317463](D:/download/downloadFromMicsoft/day11-会话技术/ppt/assets/1629389317463.png)

方式二:选中打开开发者工具或者 使用快捷键F12 或者 Ctrl+Shift+I

![1629390237936](D:/download/downloadFromMicsoft/day11-会话技术/ppt/assets/1629390237936.png)

3.2 获取Cookie

- 获取客户端携带的所有Cookie，使用==request==对象

```
Cookie[] cookies = request.getCookies();
```

- 遍历数组，获取每一个Cookie对象：for
- 使用Cookie对象方法获取数据

```
cookie.getName();
cookie.getValue();
```

介绍完获取Cookie对应的步骤后，接下面再通过一个案例来完成Cookie的获取，具体实现步骤为:

> 需求:在Servlet中获取前一个案例存入在Cookie对象中的数据
>
> 1.编写一个新Servlet类，名称为BServlet
>
> 2.在BServlet中使用request对象获取Cookie数组，遍历数组，从数据中获取指定名称对应的值
>
> 3.启动测试，在控制台打印出获取的值

(1)编写一个新Servlet类，名称为BServlet

```java
@WebServlet("/bServlet")
public class BServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doGet(request, response);
    }
}
```

（2）在BServlet中使用request对象获取Cookie数组，遍历数组，从数据中获取指定名称对应的值

```java
@WebServlet("/bServlet")
public class BServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //获取Cookie
        //1. 获取Cookie数组
        Cookie[] cookies = request.getCookies();
        //2. 遍历数组
        for (Cookie cookie : cookies) {
            //3. 获取数据
            String name = cookie.getName();
            if("username".equals(name)){
                String value = cookie.getValue();
                System.out.println(name+":"+value);
                break;
            }
        }

    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doGet(request, response);
    }
}
```

（3）启动测试，在控制台打印出获取的值

访问`http://localhost:8080/cookie-demo/bServlet`

![1629391020081](D:/download/downloadFromMicsoft/day11-会话技术/ppt/assets/1629391020081.png)

在IDEA控制台就能看到输出的结果:

![1629391061140](D:/download/downloadFromMicsoft/day11-会话技术/ppt/assets/1629391061140.png)

==思考:==测试的时候

* 在访问AServlet和BServlet的中间把关闭浏览器,重启浏览器后访问BServlet能否获取到Cookie中的数据?

这个问题，会在Cookie的使用细节中讲，大家可以动手先试下。

**小结**

在这节中，主要讲解了Cookie的基本使用,包含两部分内容

- 发送Cookie:
  - 创建Cookie对象，并设置值:Cookie cookie = new Cookie("key","value");
  - 发送Cookie到客户端使用的是Reponse对象:response.addCookie(cookie);
- 获取Cookie:
  - 使用Request对象获取Cookie数组:Cookie[] cookies = request.getCookies();
  - 遍历数组
  - 获取数组中每个Cookie对象的值:cookie.getName()和cookie.getValue()

介绍完Cookie的基本使用之后，那么Cookie的底层到底是如何实现一次会话两次请求之间的数据共享呢?

### 2.2 Cookie的原理分析

对于Cookie的实现原理是基于HTTP协议的,其中设计到HTTP协议中的两个请求头信息:

* 响应头:set-cookie
* 请求头: cookie

![1629393289338](D:/download/downloadFromMicsoft/day11-会话技术/ppt/assets/1629393289338.png)

* 前面的案例中已经能够实现，AServlet给前端发送Cookie,BServlet从request中获取Cookie的功能
* 对于AServlet响应数据的时候，Tomcat服务器都是基于HTTP协议来响应数据
* 当Tomcat发现后端要返回的是一个Cookie对象之后，Tomcat就会在响应头中添加一行数据==`Set-Cookie:username=zs`==
* 浏览器获取到响应结果后，从响应头中就可以获取到`Set-Cookie`对应值`username=zs`,并将数据存储在浏览器的内存中
* 浏览器再次发送请求给BServlet的时候，浏览器会自动在请求头中添加==`Cookie: username=zs`==发送给服务端BServlet
* Request对象会把请求头中cookie对应的值封装成一个个Cookie对象，最终形成一个数组
* BServlet通过Request对象获取到Cookie[]后，就可以从中获取自己需要的数据

接下来，使用刚才的案例，把上述结论验证下:

(1)访问AServlet对应的地址`http://localhost:8080/cookie-demo/aServlet`

使用Chrom浏览器打开开发者工具(F12或Crtl+Shift+I)进行查看==响应头==中的数据

![1629393428733](D:/download/downloadFromMicsoft/day11-会话技术/ppt/assets/1629393428733.png)

（2）访问BServlet对应的地址`http://localhost:8080/cookie-demo/bServlet

使用Chrom浏览器打开开发者工具(F12或Crtl+Shift+I)进行查看==请求头==中的数据

![1629393578667](D:/download/downloadFromMicsoft/day11-会话技术/ppt/assets/1629393578667.png)

### 2.3 Cookie的使用细节

在这节主要讲解两个知识，第一个是Cookie的存活时间，第二个是Cookie如何存储中文，首先来学习下Cookie的存活时间。

#### 2.3.1 Cookie的存活时间

前面让大家思考过一个问题:

![1629423321737](D:/download/downloadFromMicsoft/day11-会话技术/ppt/assets/1629423321737.png)

(1)浏览器发送请求给AServlet,AServlet会响应一个存有`usernanme=zs`的Cookie对象给浏览器

(2)浏览器接收到响应数据将cookie存入到浏览器内存中

(3)当浏览器再次发送请求给BServlet,BServlet就可以使用Request对象获取到Cookie数据

(4)在发送请求到BServlet之前，如果把浏览器关闭再打开进行访问，BServlet能否获取到Cookie数据?

==注意：浏览器关闭再打开不是指打开一个新的选显卡，而且必须是先关闭再打开，顺序不能变。==

针对上面这个问题，通过演示，会发现，BServlet中无法再获取到Cookie数据，这是为什么呢?

* 默认情况下，Cookie存储在浏览器内存中，当浏览器关闭，内存释放，则Cookie被销毁

这个结论就印证了上面的演示效果，但是如果使用这种默认情况下的Cookie,有些需求就无法实现，比如:

![1629423629887](D:/download/downloadFromMicsoft/day11-会话技术/ppt/assets/1629423629887.png)

上面这个网站的登录页面上有一个`记住我`的功能，这个功能大家都比较熟悉

* 第一次输入用户名和密码并勾选`记住我`然后进行登录
* 下次再登陆的时候，用户名和密码就会被自动填充，不需要再重新输入登录
* 比如`记住我`这个功能需要记住用户名和密码一个星期，那么使用默认情况下的Cookie就会出现问题
* 因为默认情况，浏览器一关，Cookie就会从浏览器内存中删除，对于`记住我`功能就无法实现

所以现在就遇到一个难题是如何将Cookie持久化存储?

Cookie其实已经为提供好了对应的API来完成这件事，这个API就是==setMaxAge==,

* 设置Cookie存活时间

```
setMaxAge(int seconds)
```

参数值为:

1.正数：将Cookie写入浏览器所在电脑的硬盘，持久化存储。到时间自动删除

2.负数：默认值，Cookie在当前浏览器内存中，当浏览器关闭，则Cookie被销毁

3.零：删除对应Cookie

接下来，咱们就在AServlet中去设置Cookie的存活时间。

```java
@WebServlet("/aServlet")
public class AServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //发送Cookie
        //1. 创建Cookie对象
        Cookie cookie = new Cookie("username","zs");
        //设置存活时间   ，1周 7天
        cookie.setMaxAge(60*60*24*7); //易阅读，需程序计算
		//cookie.setMaxAge(604800); //不易阅读(可以使用注解弥补)，程序少进行一次计算
        //2. 发送Cookie，response
        response.addCookie(cookie);
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doGet(request, response);
    }
}
```

修改完代码后，启动测试，访问`http://localhost:8080/cookie-demo/aServlet`

* 访问一个AServlet后，把浏览器关闭重启后，再去访问`http://localhost:8080/cookie-demo/bServet`,能在控制台打印出`username:zs`,说明Cookie没有随着浏览器关闭而被销毁
* 通过浏览器查看Cookie的内容，会发现Cookie的相关信息

![1629424844041](D:/download/downloadFromMicsoft/day11-会话技术/ppt/assets/1629424844041.png)

#### 2.3.2 Cookie存储中文

首先，先来演示一个效果，将之前`username=zs`的值改成`username=张三`，把汉字`张三`存入到Cookie中，看是什么效果:

```java
@WebServlet("/aServlet")
public class AServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
 		//发送Cookie
        String value = "张三";
        Cookie cookie = new Cookie("username",value);
        //设置存活时间   ，1周 7天
        cookie.setMaxAge(60*60*24*7);
        //2. 发送Cookie，response
        response.addCookie(cookie);
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doGet(request, response);
    }
}
```

启动访问测试，访问`http://localhost:8080/cookie-demo/aServlet`会发现浏览器会提示错误信息

![1629425945465](D:/download/downloadFromMicsoft/day11-会话技术/ppt/assets/1629425945465.png)

通过上面的案例演示，得到一个结论:

* Cookie不能直接存储中文

Cookie不能存储中文，但是如果有这方面的需求，这个时候该如何解决呢?

这个时候，可以使用之前学过的一个知识点叫`URL编码`，所以如果需要存储中文，就需要进行转码，具体的实现思路为:

> 1.在AServlet中对中文进行URL编码，采用URLEncoder.encode()，将编码后的值存入Cookie中
>
> 2.在BServlet中获取Cookie中的值,获取的值为URL编码后的值
>
> 3.将获取的值在进行URL解码,采用URLDecoder.decode()，就可以获取到对应的中文值

(1)在AServlet中对中文进行URL编码

```java
@WebServlet("/aServlet")
public class AServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //发送Cookie
        String value = "张三";
        //对中文进行URL编码
        value = URLEncoder.encode(value, "UTF-8");
        System.out.println("存储数据："+value);
        //将编码后的值存入Cookie中
        Cookie cookie = new Cookie("username",value);
        //设置存活时间   ，1周 7天
        cookie.setMaxAge(60*60*24*7);
        //2. 发送Cookie，response
        response.addCookie(cookie);
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doGet(request, response);
    }
}
```

(2)在BServlet中获取值，并对值进行解码

```java
@WebServlet("/bServlet")
public class BServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //获取Cookie
        //1. 获取Cookie数组
        Cookie[] cookies = request.getCookies();
        //2. 遍历数组
        for (Cookie cookie : cookies) {
            //3. 获取数据
            String name = cookie.getName();
            if("username".equals(name)){
                String value = cookie.getValue();//获取的是URL编码后的值 %E5%BC%A0%E4%B8%89
                //URL解码
                value = URLDecoder.decode(value,"UTF-8");
                System.out.println(name+":"+value);//value解码后为 张三
                break;
            }
        }

    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doGet(request, response);
    }
}
```

至此，就可以将中文存入Cookie中进行使用。

**小结**

Cookie的使用细节中，讲了Cookie的`存活时间`和`存储中文`:

* 存活时间，需要掌握setMaxAage()API的使用

* 存储中文，需要掌握URL编码和解码的使用



### 使用体验

首先servlet，服务器响应，在浏览器中设置cookie，浏览器再次发送亲求时，默认会自带上cookie，servlet要对发送过来的cookie做一个name与value匹配，只有特定的name才有价值，至于其他的cookie猜测是建立连接时用到的。





## 3，Session

Cookie已经能完成一次会话多次请求之间的数据共享，之前还提到过Session也可以实现，那么:

- 什么是Session?
- Session如何来使用?
- Session是如何实现的?
- Session的使用注意事项有哪些?

### 3.1 Session的基本使用

**1.概念**

==Session==：服务端会话跟踪技术：将数据保存到服务端。

* Session是存储在服务端而Cookie是存储在客户端
* 存储在客户端的数据容易被窃取和截获，存在很多不安全的因素
* 存储在服务端的数据相比于客户端来说就更安全

**2.Session的工作流程**

 ![1629427173389](D:/download/downloadFromMicsoft/day11-会话技术/ppt/assets/1629427173389.png)

* 在服务端的AServlet获取一个Session对象，把数据存入其中
* 在服务端的BServlet获取到相同的Session对象，从中取出数据
* 就可以实现一次会话中多次请求之间的数据共享了
* 现在最大的问题是如何保证AServlet和BServlet使用的是同一个Session对象(在原理分析会讲解)?

**3.Session的基本使用**

在JavaEE中提供了HttpSession接口，来实现一次会话的多次请求之间数据共享功能。

具体的使用步骤为:

* 获取Session对象,使用的是request对象

```
HttpSession session = request.getSession();
```

* Session对象提供的功能:

  * 存储数据到 session 域中

    ```
    void setAttribute(String name, Object o)
    ```

  * 根据 key，获取值

    ```
    Object getAttribute(String name)
    ```

  * 根据 key，删除该键值对

    ```
    void removeAttribute(String name)
    ```

介绍完Session相关的API后，接下来通过一个案例来完成对Session的使用，具体实现步骤为:

> 需求:在一个Servlet中往Session中存入数据，在另一个Servlet中获取Session中存入的数据
>
> 1.创建名为SessionDemo1的Servlet类
>
> 2.创建名为SessionDemo2的Servlet类
>
> 3.在SessionDemo1的方法中:获取Session对象、存储数据
>
> 4.在SessionDemo2的方法中:获取Session对象、获取数据
>
> 5.启动测试

(1)创建名为SessionDemo1的Servlet类

```java
@WebServlet("/demo1")
public class SessionDemo1 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
    
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doGet(request, response);
    }
}
```

(2)创建名为SessionDemo2的Servlet类

```java
@WebServlet("/demo2")
public class SessionDemo2 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
    
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doGet(request, response);
    }
}
```

(3)SessionDemo1:获取Session对象、存储数据

```java
@WebServlet("/demo1")
public class SessionDemo1 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
    	//存储到Session中
        //1. 获取Session对象
        HttpSession session = request.getSession();
        //2. 存储数据
        session.setAttribute("username","zs");
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doGet(request, response);
    }
}
```

(4)SessionDemo2:获取Session对象、获取数据

```java
@WebServlet("/demo2")
public class SessionDemo2 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //获取数据，从session中
        //1. 获取Session对象
        HttpSession session = request.getSession();
        //2. 获取数据
        Object username = session.getAttribute("username");
        System.out.println(username);
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doGet(request, response);
    }
}
```

(5)启动测试，

* 先访问`http://localhost:8080/cookie-demo/demo1`,将数据存入Session
* 在访问`http://localhost:8080/cookie-demo/demo2`,从Session中获取数据
* 查看控制台

![1629428292373](D:/download/downloadFromMicsoft/day11-会话技术/ppt/assets/1629428292373.png)

通过案例的效果，能看到Session是能够在一次会话中两次请求之间共享数据。

**小结**

至此Session的基本使用就已经完成了，重点要掌握的是:

* Session的获取

  ```
  HttpSession session = request.getSession();
  ```

* Session常用方法的使用

  ```
  void setAttribute(String name, Object o)
  Object getAttribute(String name)
  ```

  **注意:**Session中可以存储的是一个Object类型的数据，也就是说Session中可以存储任意数据类型。

介绍完Session的基本使用之后，那么Session的底层到底是如何实现一次会话两次请求之间的数据共享呢?

### 3.2 Session的原理分析



### Session原理的个人分析：

session是存储在服务器的，也就更加安全，和cookie存在显著不同，session一开始就设置在服务器，

如代码：

```
  //1. 获取Session对象
        HttpSession session = request.getSession();
```

再添加数据进去，代码：

```
 session.setAttribute("username","wzt");
```



思考，怎么判断session属于谁呢，也就是说，怎么在多次请求中共享同一个session，非多次请求，不是同一个session，答案：要给访问者一个标识

服务器会额外做一件事，服务器会给session唯一标识，如id:10，当服务器检查这个请求没有携带标识，就会创建一个新的sessinon，并把session的唯一标识id:10当做一个 cookie，添加Set-Cookie:JESSIONID=10到响应头中，并响应给浏览器，当浏览器再次访问时，携带了标识，就会之前拿到存储在服务器的session数据了



* Session是基于Cookie实现的

这句话其实不太能详细的说明Session的底层实现，接下来，咱们一步步来分析下Session的具体实现原理:

(1)前提条件

![1629429063101](D:/download/downloadFromMicsoft/day11-会话技术/ppt/assets/1629429063101.png)

Session要想实现一次会话多次请求之间的数据共享，就必须要保证多次请求获取Session的对象是同一个。

那么它们是一个对象么？要验证这个结论也很简单，只需要在上面案例中的两个Servlet中分别打印下Session对象

SessionDemo1

```java
@WebServlet("/demo1")
public class SessionDemo1 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
    	//存储到Session中
        //1. 获取Session对象
        HttpSession session = request.getSession();
        System.out.println(session);
        //2. 存储数据
        session.setAttribute("username","zs");
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doGet(request, response);
    }
}
```

SessionDemo2

```java
@WebServlet("/demo2")
public class SessionDemo2 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //获取数据，从session中
        //1. 获取Session对象
        HttpSession session = request.getSession();
        System.out.println(session);
        //2. 获取数据
        Object username = session.getAttribute("username");
        System.out.println(username);
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doGet(request, response);
    }
}
```

启动测试，分别访问

`http://localhost:8080/cookie-demo/demo1`

`http://localhost:8080/cookie-demo/demo2`

![1629429239409](D:/download/downloadFromMicsoft/day11-会话技术/ppt/assets/1629429239409.png)

通过打印可以得到如下结论:

* 两个Servlet类中获取的Session对象是同一个
* 把demo1和demo2请求刷新多次，控制台最终打印的结果都是同一个

那么问题又来了，如果新开一个浏览器，访问demo1或者demo2,打印在控制台的Session还是同一个对象么?

![1629429788264](D:/download/downloadFromMicsoft/day11-会话技术/ppt/assets/1629429788264.png)

==注意:在一台电脑上演示的时候，如果是相同的浏览器必须要把浏览器全部关掉重新打开，才算新开的一个浏览器。==

当然也可以使用不同的浏览器进行测试，就不需要把之前的浏览器全部关闭。

测试的结果：如果是不同浏览器或者重新打开浏览器后，打印的Session就不一样了。

所以Session实现的也是一次会话中的多次请求之间的数据共享。

那么最主要的问题就来了，Session是如何保证在一次会话中获取的Session对象是同一个呢?

![1629430754825](D:/download/downloadFromMicsoft/day11-会话技术/ppt/assets/1629430754825.png)

(1)demo1在第一次获取session对象的时候，session对象会有一个唯一的标识，假如是`id:10`

(2)demo1在session中存入其他数据并处理完成所有业务后，需要通过Tomcat服务器响应结果给浏览器

(3)Tomcat服务器发现业务处理中使用了session对象，就会把session的唯一标识`id:10`当做一个cookie，添加`Set-Cookie:JESSIONID=10`到响应头中，并响应给浏览器

(4)浏览器接收到响应结果后，会把响应头中的coookie数据存储到浏览器的内存中

(5)浏览器在同一会话中访问demo2的时候，会把cookie中的数据按照`cookie: JESSIONID=10`的格式添加到请求头中并发送给服务器Tomcat

(6)demo2获取到请求后，从请求头中就读取cookie中的JSESSIONID值为10，然后就会到服务器内存中寻找`id:10`的session对象，如果找到了，就直接返回该对象，如果没有则新创建一个session对象

(7)关闭打开浏览器后，因为浏览器的cookie已被销毁，所以就没有JESSIONID的数据，服务端获取到的session就是一个全新的session对象

至此，`Session是基于Cookie来实现的`这就话，就解释完了，接下来通过实例来演示下:

(1)使用chrome浏览器访问`http://localhost:8080/cookie-demo/demo1`,打开开发者模式(F12或Ctrl+Shift+I),查看==响应头(Response Headers)==数据:

![1629430891071](D:/download/downloadFromMicsoft/day11-会话技术/ppt/assets/1629430891071.png)

(2)使用chrome浏览器再次访问`http://localhost:8080/cookie-demo/demo2`，查看==请求头(Request Headers)==数据:

![1629431299195](D:/download/downloadFromMicsoft/day11-会话技术/ppt/assets/1629431299195.png)

**小结**

介绍完Session的原理，只需要记住

* Session是基于Cookie来实现的

### 3.3 Session的使用细节

这节会主要讲解两个知识，第一个是Session的钝化和活化，第二个是Session的销毁，首先来学习什么是Session的钝化和活化？

#### 3.3.1 Session钝化与活化

首先需要大家思考的问题是: 

* 服务器重启后，Session中的数据是否还在?

要想回答这个问题，可以先看下下面这幅图，

![1629438984314](D:/download/downloadFromMicsoft/day11-会话技术/ppt/assets/1629438984314.png) 

(1)服务器端AServlet和BServlet共用的session对象应该是存储在服务器的内存中

(2)服务器重新启动后，内存中的数据应该是已经被释放，对象也应该都销毁了

所以session数据应该也已经不存在了。但是如果session不存在会引发什么问题呢?

举个例子说明下，

(1)用户把需要购买的商品添加到购物车，因为要实现同一个会话多次请求数据共享，所以假设把数据存入Session对象中

(2)用户正要付钱的时候接到一个电话，付钱的动作就搁浅了

(3)正在用户打电话的时候，购物网站因为某些原因需要重启

(4)重启后session数据被销毁，购物车中的商品信息也就会随之而消失

(5)用户想再次发起支付，就会出为问题

所以说对于session的数据，应该做到就算服务器重启了，也应该能把数据保存下来才对。

分析了这么多，那么Tomcat服务器在重启的时候，session数据到底会不会保存以及是如何保存的，可以通过实际案例来演示下:

==注意:这里所说的关闭和启动应该要确保是正常的关闭和启动。==

那如何才是正常关闭Tomcat服务器呢?

需要使用命令行的方式来启动和停止Tomcat服务器:

==启动==:进入到项目pom.xml所在目录，执行`tomcat7:run`

![1629439800328](D:/download/downloadFromMicsoft/day11-会话技术/ppt/assets/1629439800328.png)

==停止==:在启动的命令行界面，输入`ctrl+c`

![1629439879596](D:/download/downloadFromMicsoft/day11-会话技术/ppt/assets/1629439879596.png)

有了上述两个正常启动和关闭的方式后，接下来的测试流程是:

(1)先启动Tomcat服务器

(2)访问`http://localhost:8080/cookie-demo/demo1`将数据存入session中

(3)正确停止Tomcat服务器

(4)再次重新启动Tomcat服务器

(5)访问`http://localhost:8080/cookie-demo/demo2` 查看是否能获取到session中的数据

![1629440018238](D:/download/downloadFromMicsoft/day11-会话技术/ppt/assets/1629440018238.png)

经过测试，会发现只要服务器是正常关闭和启动，session中的数据是可以被保存下来的。

那么Tomcat服务器到底是如何做到的呢?

具体的原因就是:Session的钝化和活化:

* 钝化：在服务器正常关闭后，Tomcat会自动将Session数据写入硬盘的文件中

  * 钝化的数据路径为:`项目目录\target\tomcat\work\Tomcat\localhost\项目名称\SESSIONS.ser`

    ![1629440576828](D:/download/downloadFromMicsoft/day11-会话技术/ppt/assets/1629440576828.png)

* 活化：再次启动服务器后，从文件中加载数据到Session中

  * 数据加载到Session中后，路径中的`SESSIONS.ser`文件会被删除掉

对于上述的整个过程，大家只需要了解下即可。因为所有的过程都是Tomcat自己完成的，不需要参与。

**小结**

Session的钝化和活化介绍完后，需要注意的是:

* session数据存储在服务端，服务器重启后，session数据会被保存

* 浏览器被关闭启动后，重新建立的连接就已经是一个全新的会话，获取的session数据也是一个新的对象

* session的数据要想共享，浏览器不能关闭，所以session数据不能长期保存数据
* cookie是存储在客户端，是可以长期保存

#### 3.3.2 Session销毁

session的销毁会有两种方式:

* 默认情况下，无操作，30分钟自动销毁

  * 对于这个失效时间，是可以通过配置进行修改的

    * 在项目的web.xml中配置

      ```xml
      <?xml version="1.0" encoding="UTF-8"?>
      <web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
               xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
               xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_3_1.xsd"
               version="3.1">
      
          <session-config>
              <session-timeout>100</session-timeout>
          </session-config>
      </web-app>
      ```

    * 如果没有配置，默认是30分钟，默认值是在Tomcat的web.xml配置文件中写死的

      ![1629441687613](D:/download/downloadFromMicsoft/day11-会话技术/ppt/assets/1629441687613.png)

* 调用Session对象的invalidate()进行销毁

  * 在SessionDemo2类中添加session销毁的方法

    ```java
    @WebServlet("/demo2")
    public class SessionDemo2 extends HttpServlet {
        @Override
        protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
            //获取数据，从session中
    
            //1. 获取Session对象
            HttpSession session = request.getSession();
            System.out.println(session);
    
            // 销毁
            session.invalidate();
            //2. 获取数据
            Object username = session.getAttribute("username");
            System.out.println(username);
        }
    
        @Override
        protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
            this.doGet(request, response);
        }
    }
    ```

  * 启动访问测试，先访问demo1将数据存入到session，再次访问demo2从session中获取数据

    ![1629441900843](D:/download/downloadFromMicsoft/day11-会话技术/ppt/assets/1629441900843.png)

  * 该销毁方法一般会在用户退出的时候，需要将session销毁掉。

**Cookie和Session小结**

* Cookie 和 Session 都是来完成一次会话内多次请求间==数据共享==的。

所需两个对象放在一块，就需要思考:

Cookie和Session的区别是什么?

Cookie和Session的应用场景分别是什么?

* 区别:
  * 存储位置：Cookie 是将数据存储在客户端，Session 将数据存储在服务端
  * 安全性：Cookie不安全，Session安全
  * 数据大小：Cookie最大3KB，Session无大小限制
  * 存储时间：Cookie可以通过setMaxAge()长期存储，Session默认30分钟
  * 服务器性能：Cookie不占服务器资源，Session占用服务器资源
* 应用场景:
  * 购物车:使用Cookie来存储
  * 以登录用户的名称展示:使用Session来存储
  * 记住我功能:使用Cookie来存储
  * 验证码:使用session来存储
* 结论
  * Cookie是用来保证用户在未登录情况下的身份识别
  * Session是用来保存用户登录后的数据

介绍完Cookie和Session以后，具体用哪个还是需要根据具体的业务进行具体分析。

## 4，用户登录注册案例

### 4.1 需求分析

 需求说明：

1. 完成用户登录功能，如果用户勾选“记住用户” ，则下次访问登录页面==自动==填充用户名密码

2. 完成注册功能，并实现==验证码==功能

![1629442826981](D:/download/downloadFromMicsoft/day11-会话技术/ppt/assets/1629442826981.png)

### 4.2 用户登录功能

1. 需求:

![1629443152010](D:/download/downloadFromMicsoft/day11-会话技术/ppt/assets/1629443152010.png)

* 用户登录成功后，跳转到列表页面，并在页面上展示当前登录的用户名称
* 用户登录失败后，跳转回登录页面，并在页面上展示对应的错误信息

2. 实现流程分析

![1629443379531](D:/download/downloadFromMicsoft/day11-会话技术/ppt/assets/1629443379531.png)

(1)前端通过表单发送请求和数据给Web层的LoginServlet

(2)在LoginServlet中接收请求和数据[用户名和密码]

(3)LoginServlet接收到请求和数据后，调用Service层完成根据用户名和密码查询用户对象

(4)在Service层需要编写UserService类，在类中实现login方法，方法中调用Dao层的UserMapper

(5)在UserMapper接口中，声明一个根据用户名和密码查询用户信息的方法

(6)Dao层把数据查询出来以后，将返回数据封装到User对象，将对象交给Service层

(7)Service层将数据返回给Web层

(8)Web层获取到User对象后，判断User对象，如果为Null,则将错误信息响应给登录页面，如果不为Null，则跳转到列表页面，并把当前登录用户的信息存入Session携带到列表页面。

3. 具体实现

(1)完成Dao层的代码编写

(1.1)将`04-资料\1. 登录注册案例\2. MyBatis环境\UserMapper.java`放到com.itheima.mapper`包下:

```java
public interface UserMapper {
    /**
     * 根据用户名和密码查询用户对象
     * @param username
     * @param password
     * @return
     */
    @Select("select * from tb_user where username = #{username} and password = #{password}")
    User select(@Param("username") String username,@Param("password")  String password);

    /**
     * 根据用户名查询用户对象
     * @param username
     * @return
     */
    @Select("select * from tb_user where username = #{username}")
    User selectByUsername(String username);

    /**
     * 添加用户
     * @param user
     */
    @Insert("insert into tb_user values(null,#{username},#{password})")
    void add(User user);
}
```

(1.2)将`04-资料\1. 登录注册案例\2. MyBatis环境\User.java`放到`com.itheima.pojo`包下:

```java
public class User {

    private Integer id;
    private String username;
    private String password;

    public Integer getId() {
        return id;
    }

    public void setId(Integer id) {
        this.id = id;
    }

    public String getUsername() {
        return username;
    }

    public void setUsername(String username) {
        this.username = username;
    }

    public String getPassword() {
        return password;
    }

    public void setPassword(String password) {
        this.password = password;
    }

    @Override
    public String toString() {
        return "User{" +
                "id=" + id +
                ", username='" + username + '\'' +
                ", password='" + password + '\'' +
                '}';
    }
}
```

(1.3)将`04-资料\1. 登录注册案例\2. MyBatis环境\UserMapper.xml`放入到resources/com/itheima/mapper`目录下:

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.itheima.mapper.UserMapper">

</mapper>
```

(2)完成Service层的代码编写

(2.1)在`com.itheima.service`包下，创建UserService类

```java
public class UserService {
    //1.使用工具类获取SqlSessionFactory
    SqlSessionFactory factory = SqlSessionFactoryUtils.getSqlSessionFactory();
    /**
     * 登录方法
     * @param username
     * @param password
     * @return
     */
    public User login(String username,String password){
        //2. 获取SqlSession
        SqlSession sqlSession = factory.openSession();
        //3. 获取UserMapper
        UserMapper mapper = sqlSession.getMapper(UserMapper.class);
        //4. 调用方法
        User user = mapper.select(username, password);
        //释放资源
        sqlSession.close();

        return  user;
    }
}
```

(3)完成页面和Web层的代码编写

(3.1)将`04-资料\1. 登录注册案例\1. 静态页面`拷贝到项目的`webapp`目录下:

![1629444649629](D:/download/downloadFromMicsoft/day11-会话技术/ppt/assets/1629444649629.png)

(3.2)将login.html内容修改成login.jsp

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <title>login</title>
    <link href="css/login.css" rel="stylesheet">
</head>

<body>
<div id="loginDiv" style="height: 350px">
    <form action="/brand-demo/loginServlet" method="post" id="form">
        <h1 id="loginMsg">LOGIN IN</h1>
        <div id="errorMsg">用户名或密码不正确</div>
        <p>Username:<input id="username" name="username" type="text"></p>
        <p>Password:<input id="password" name="password" type="password"></p>
        <p>Remember:<input id="remember" name="remember" type="checkbox"></p>
        <div id="subDiv">
            <input type="submit" class="button" value="login up">
            <input type="reset" class="button" value="reset">&nbsp;&nbsp;&nbsp;
            <a href="register.html">没有账号？</a>
        </div>
    </form>
</div>
</body>
</html>
```

(3.3)创建LoginServlet类

```java
@WebServlet("/loginServlet")
public class LoginServlet extends HttpServlet {
    private UserService service = new UserService();

    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //1. 获取用户名和密码
        String username = request.getParameter("username");
        String password = request.getParameter("password");
   
        //2. 调用service查询
        User user = service.login(username, password);

        //3. 判断
        if(user != null){
            //登录成功，跳转到查询所有的BrandServlet
            
            //将登陆成功后的user对象，存储到session
            HttpSession session = request.getSession();
            session.setAttribute("user",user);
            
            String contextPath = request.getContextPath();
            response.sendRedirect(contextPath+"/selectAllServlet");
        }else {
            // 登录失败,
            // 存储错误信息到request
            request.setAttribute("login_msg","用户名或密码错误");
            // 跳转到login.jsp
            request.getRequestDispatcher("/login.jsp").forward(request,response);

        }
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doGet(request, response);
    }
}
```

(3.4)在brand.jsp中<body>标签下添加欢迎当前用户的提示信息:

```jsp
<h1>${user.username},欢迎您</h1>
```

(3.5) 修改login.jsp，将错误信息使用EL表达式来获取

```jsp
修改前内容:<div id="errorMsg">用户名或密码不正确</div>
修改后内容: <div id="errorMsg">${login_msg}</div>
```

(4)启动，访问测试

(4.1) 进入登录页面，输入错误的用户名或密码

![1629445376407](D:/download/downloadFromMicsoft/day11-会话技术/ppt/assets/1629445376407.png)

(4.2)输入正确的用户和密码信息

![1629445415216](D:/download/downloadFromMicsoft/day11-会话技术/ppt/assets/1629445415216.png)

**小结**

* 在LoginServlet中，将登录成功的用户数据存入session中，方法在列表页面中获取当前登录用户信息进行展示
* 在LoginServlet中，将登录失败的错误信息存入到request中，如果存入到session中就会出现这次会话的所有请求都有登录失败的错误信息，这个是不需要的，所以不用存入到session中

### 4.3 记住我-设置Cookie

1. 需求:

如果用户勾选“记住用户” ，则下次访问登陆页面自动填充用户名密码。这样可以提升用户的体验。

![1629445835281](D:/download/downloadFromMicsoft/day11-会话技术/ppt/assets/1629445835281.png)

对应上面这个需求，最大的问题就是: 如何自动填充用户名和密码?

2. 实现流程分析

因为`记住我`功能要实现的效果是，就算用户把浏览器关闭过几天再来访问也能自动填充，所以需要将登陆信息存入一个可以长久保存，并且能够在浏览器关闭重新启动后依然有效的地方，就是前面讲的==Cookie==,所以:

* 将用户名和密码写入==Cookie==中，并且持久化存储Cookie,下次访问浏览器会自动携带Cookie

* 在页面获取Cookie数据后，设置到用户名和密码框中

* 何时写入Cookie?
  * 用户必须登陆成功后才需要写
  * 用户必须在登录页面勾选了`记住我`的复选框

![1629446248511](D:/download/downloadFromMicsoft/day11-会话技术/ppt/assets/1629446248511.png)

(1)前端需要在发送请求和数据的时候，多携带一个用户是否勾选`Remember`的数据

(2)LoginServlet获取到数据后，调用Service完成用户名和密码的判定

(3)登录成功，并且用户在前端勾选了`记住我`，需要往Cookie中写入用户名和密码的数据，并设置Cookie存活时间

(4)设置成功后，将数据响应给前端

3. 具体实现

(1)在login.jsp为复选框设置值

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <title>login</title>
    <link href="css/login.css" rel="stylesheet">
</head>

<body>
<div id="loginDiv" style="height: 350px">
    <form action="/brand-demo/loginServlet" method="post" id="form">
        <h1 id="loginMsg">LOGIN IN</h1>
        <div id="errorMsg">${login_msg}</div>
        <p>Username:<input id="username" name="username" type="text"></p>
        <p>Password:<input id="password" name="password" type="password"></p>
        <p>Remember:<input id="remember" name="remember" value="1" type="checkbox"></p>
        <div id="subDiv">
            <input type="submit" class="button" value="login up">
            <input type="reset" class="button" value="reset">&nbsp;&nbsp;&nbsp;
            <a href="register.html">没有账号？</a>
        </div>
    </form>
</div>
</body>
</html>
```

(2)在LoginServlet获取复选框的值并在登录成功后进行设置Cookie

```java
@WebServlet("/loginServlet")
public class LoginServlet extends HttpServlet {
    private UserService service = new UserService();

    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //1. 获取用户名和密码
        String username = request.getParameter("username");
        String password = request.getParameter("password");

        //获取复选框数据
        String remember = request.getParameter("remember");

        //2. 调用service查询
        User user = service.login(username, password);

        //3. 判断
        if(user != null){
            //登录成功，跳转到查询所有的BrandServlet

            //判断用户是否勾选记住我，字符串写前面是为了避免出现空指针异常
            if("1".equals(remember)){
                //勾选了，发送Cookie
                //1. 创建Cookie对象
                Cookie c_username = new Cookie("username",username);
                Cookie c_password = new Cookie("password",password);
                // 设置Cookie的存活时间
                c_username.setMaxAge( 60 * 60 * 24 * 7);
                c_password.setMaxAge( 60 * 60 * 24 * 7);
                //2. 发送
                response.addCookie(c_username);
                response.addCookie(c_password);
            }

            //将登陆成功后的user对象，存储到session
            HttpSession session = request.getSession();
            session.setAttribute("user",user);

            String contextPath = request.getContextPath();
            response.sendRedirect(contextPath+"/selectAllServlet");
        }else {
            // 登录失败,

            // 存储错误信息到request
            request.setAttribute("login_msg","用户名或密码错误");

            // 跳转到login.jsp
            request.getRequestDispatcher("/login.jsp").forward(request,response);

        }
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doGet(request, response);
    }
}
```

(3)启动访问测试，

只有当前用户名和密码输入正确，并且勾选了Remeber的复选框，在响应头中才可以看得cookie的相关数据

![1629447232217](D:/download/downloadFromMicsoft/day11-会话技术/ppt/assets/1629447232217.png)

### 4.4 记住我-获取Cookie

1. 需求

登录成功并勾选了Remeber后，后端返回给前端的Cookie数据就已经存储好了，接下来就需要在页面获取Cookie中的数据，并把数据设置到登录页面的用户名和密码框中。

![1629449100282](D:/download/downloadFromMicsoft/day11-会话技术/ppt/assets/1629449100282.png)

如何在页面直接获取Cookie中的值呢?

2. 实现流程分析

在页面可以使用EL表达式，${cookie.==key==.value}

key:指的是存储在cookie中的键名称

![1629449234735](D:/download/downloadFromMicsoft/day11-会话技术/ppt/assets/1629449234735.png)

(1)在login.jsp用户名的表单输入框使用value值给表单元素添加默认值，value可以使用`${cookie.username.value}`

(2)在login.jsp密码的表单输入框使用value值给表单元素添加默认值，value可以使用`${cookie.password.value}`

3. 具体实现

(1)修改login.jsp页面

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <title>login</title>
    <link href="css/login.css" rel="stylesheet">
</head>

<body>
<div id="loginDiv" style="height: 350px">
    <form action="/brand-demo/loginServlet" method="post" id="form">
        <h1 id="loginMsg">LOGIN IN</h1>
        <div id="errorMsg">${login_msg}</div>
        <p>Username:<input id="username" name="username" value="${cookie.username.value}" type="text"></p>

        <p>Password:<input id="password" name="password" value="${cookie.password.value}" type="password"></p>
        <p>Remember:<input id="remember" name="remember" value="1" type="checkbox"></p>
        <div id="subDiv">
            <input type="submit" class="button" value="login up">
            <input type="reset" class="button" value="reset">&nbsp;&nbsp;&nbsp;
            <a href="register.html">没有账号？</a>
        </div>
    </form>
</div>
</body>
</html>
```

4. 访问测试，重新访问登录页面，就可以看得用户和密码已经被填充。

![1629449530886](D:/download/downloadFromMicsoft/day11-会话技术/ppt/assets/1629449530886.png)

### 4.5 用户注册功能

1. 需求

* 注册功能：保存用户信息到数据库
* 验证码功能
  * 展示验证码：展示验证码图片，并可以点击切换
  * 校验验证码：验证码填写不正确，则注册失败

![1629449648793](D:/download/downloadFromMicsoft/day11-会话技术/ppt/assets/1629449648793.png)

2. 实现流程分析

![1629449720005](D:/download/downloadFromMicsoft/day11-会话技术/ppt/assets/1629449720005.png)

(1)前端通过表单发送请求和数据给Web层的RegisterServlet

(2)在RegisterServlet中接收请求和数据[用户名和密码]

(3)RegisterServlet接收到请求和数据后，调用Service层完成用户信息的保存

(4)在Service层需要编写UserService类，在类中实现register方法，需要判断用户是否已经存在，如果不存在，则完成用户数据的保存

(5)在UserMapper接口中，声明两个方法，一个是根据用户名查询用户信息方法，另一个是保存用户信息方法

(6)在UserService类中保存成功则返回true，失败则返回false,将数据返回给Web层

(7)Web层获取到结果后，如果返回的是true,则提示`注册成功`，并转发到登录页面，如果返回false则提示`用户名已存在`并转发到注册页面

3. 具体实现

(1)Dao层代码参考资料中的内容完成

(2)编写Service层代码

```java
public class UserService {
    //1.使用工具类获取SqlSessionFactory
    SqlSessionFactory factory = SqlSessionFactoryUtils.getSqlSessionFactory();
    /**
     * 注册方法
     * @return
     */

    public boolean register(User user){
        //2. 获取SqlSession
        SqlSession sqlSession = factory.openSession();
        //3. 获取UserMapper
        UserMapper mapper = sqlSession.getMapper(UserMapper.class);
        //4. 判断用户名是否存在
        User u = mapper.selectByUsername(user.getUsername());

        if(u == null){
            // 用户名不存在，注册
            mapper.add(user);
            sqlSession.commit();
        }
        sqlSession.close();

        return u == null;

    }
}
```

(3)完成页面和Web层的代码编写

(3.1)将register.html内容修改成register.jsp

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>欢迎注册</title>
    <link href="css/register.css" rel="stylesheet">
</head>
<body>
<div class="form-div">
    <div class="reg-content">
        <h1>欢迎注册</h1>
        <span>已有帐号？</span> <a href="login.html">登录</a>
    </div>
    <form id="reg-form" action="/brand-demo/registerServlet" method="post">
        <table>
            <tr>
                <td>用户名</td>
                <td class="inputs">
                    <input name="username" type="text" id="username">
                    <br>
                    <span id="username_err" class="err_msg" style="display:none">用户名不太受欢迎</span>
                </td>
            </tr>
            <tr>
                <td>密码</td>
                <td class="inputs">
                    <input name="password" type="password" id="password">
                    <br>
                    <span id="password_err" class="err_msg" style="display: none">密码格式有误</span>
                </td>
            </tr>
            <tr>
                <td>验证码</td>
                <td class="inputs">
                    <input name="checkCode" type="text" id="checkCode">
                    <img src="imgs/a.jpg">
                    <a href="#" id="changeImg" >看不清？</a>
                </td>
            </tr>
        </table>
        <div class="buttons">
            <input value="注 册" type="submit" id="reg_btn">
        </div>
        <br class="clear">
    </form>
</div>
</body>
</html>
```

(3.2)编写RegisterServlet

```java
@WebServlet("/registerServlet")
public class RegisterServlet extends HttpServlet {
    private UserService service = new UserService();

    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
       //1. 获取用户名和密码数据
        String username = request.getParameter("username");
        String password = request.getParameter("password");
        
        User user = new User();
        user.setUsername(username);
        user.setPassword(password);

        //2. 调用service 注册
        boolean flag = service.register(user);
        //3. 判断注册成功与否
        if(flag){
             //注册功能，跳转登陆页面
            request.setAttribute("register_msg","注册成功，请登录");
            request.getRequestDispatcher("/login.jsp").forward(request,response);
        }else {
            //注册失败，跳转到注册页面

            request.setAttribute("register_msg","用户名已存在");
            request.getRequestDispatcher("/register.jsp").forward(request,response);
        }


    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doGet(request, response);
    }
}
```

(3.3)需要在页面上展示后台返回的错误信息，需要修改register.jsp

```jsp
修改前:<span id="username_err" class="err_msg" style="display:none">用户名不太受欢迎</span>
修改后:<span id="username_err" class="err_msg">${register_msg}</span>
```

(3.4)如果注册成功，需要把成功信息展示在登录页面，所以也需要修改login.jsp

```jsp
修改前:<div id="errorMsg">${login_msg}</div>
修改后:<div id="errorMsg">${login_msg} ${register_msg}</div>
```

(3.5)修改login.jsp，将注册跳转地址修改为register.jsp

```jsp
修改前：<a href="register.html">没有账号？</a>
修改后: <a href="register.jsp">没有账号？</a>
```

(3.6)启动测试，

如果是注册的用户信息已经存在:

![1629451535605](D:/download/downloadFromMicsoft/day11-会话技术/ppt/assets/1629451535605.png)

如果注册的用户信息不存在，注册成功:

![1629451567428](D:/download/downloadFromMicsoft/day11-会话技术/ppt/assets/1629451567428.png)

### 4.6 验证码-展示

1. 需求分析

展示验证码：展示验证码图片，并可以点击切换

![1629451646831](D:/download/downloadFromMicsoft/day11-会话技术/ppt/assets/1629451646831.png)

验证码的生成是通过工具类来实现的，具体的工具类参考

`04-资料\1. 登录注册案例\CheckCodeUtil.java`

在该工具类中编写main方法进行测试:

```java
public static void main(String[] args) throws IOException {
    //生成验证码的图片位置
    OutputStream fos = new FileOutputStream("d://a.jpg");
    //checkCode为最终验证码的数据
    String checkCode = CheckCodeUtil.outputVerifyImage(100, 50, fos, 4);
    System.out.println(checkCode);
}

```

生成完验证码以后，就可以知晓:

* 验证码就是使用Java代码生成的一张图片
* 验证码的作用:防止机器自动注册，攻击服务器

2. 实现流程分析

![1629452623289](D:/download/downloadFromMicsoft/day11-会话技术/ppt/assets/1629452623289.png)

(1)前端发送请求给CheckCodeServlet

(2)CheckCodeServlet接收到请求后，生成验证码图片，将图片用Reponse对象的输出流写回到前端

思考:如何将图片写回到前端浏览器呢?

(1)Java中已经有工具类生成验证码图片，测试类中只是把图片生成到磁盘上
(2)生成磁盘的过程中使用的是OutputStream流，如何把这个图片生成在页面呢?
(3)前面在将Reponse对象的时候，它有一个方法可以获取其字节输出流，getOutputStream()
(4)综上所述，可以把写往磁盘的流对象更好成Response的字节流，即可完成图片响应给前端

3. 具体实现

(1)修改Register.jsp页面，将验证码的图片从后台获取

```jsp
<tr>
    <td>验证码</td>
        <td class="inputs">
        <input name="checkCode" type="text" id="checkCode">
        <img id="checkCodeImg" src="/brand-demo/checkCodeServlet">
        <a href="#" id="changeImg" >看不清？</a>
    </td>
</tr>

<script>
    document.getElementById("changeImg").onclick = function () {
       	//路径后面添加时间戳的目的是避免浏览器进行缓存静态资源
        document.getElementById("checkCodeImg").src = "/brand-demo/checkCodeServlet?"+new Date().getMilliseconds();
    }
</script>
```

(2)编写CheckCodeServlet类，用来接收请求生成验证码

```java
@WebServlet("/checkCodeServlet")
public class CheckCodeServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        // 生成验证码
        ServletOutputStream os = response.getOutputStream();
        String checkCode = CheckCodeUtil.outputVerifyImage(100, 50, os, 4);
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doGet(request, response);
    }
}
```

### 4.7验证码-校验

1. 需求

* 判断程序生成的验证码 和 用户输入的验证码 是否一样，如果不一样，则阻止注册
* 验证码图片访问和提交注册表单是==两次==请求，所以要将程序生成的验证码存入Session中

![1629452835571](D:/download/downloadFromMicsoft/day11-会话技术/ppt/assets/1629452835571.png)

思考:为什么要把验证码数据存入到Session中呢?

* 生成验证码和校验验证码是两次请求，此处就需要在一个会话的两次请求之间共享数据
* 验证码属于安全数据类的，所以选中Session来存储验证码数据。

2. 实现流程分析

![1629452966499](D:/download/downloadFromMicsoft/day11-会话技术/ppt/assets/1629452966499.png)

(1)在CheckCodeServlet中生成验证码的时候，将验证码数据存入Session对象

(2)前端将验证码和注册数据提交到后台，交给RegisterServlet类

(3)RegisterServlet类接收到请求和数据后，其中就有验证码，和Session中的验证码进行对比

(4)如果一致，则完成注册，如果不一致，则提示错误信息

3. 具体实现

(1)修改CheckCodeServlet类，将验证码存入Session对象

```java
@WebServlet("/checkCodeServlet")
public class CheckCodeServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

        // 生成验证码
        ServletOutputStream os = response.getOutputStream();
        String checkCode = CheckCodeUtil.outputVerifyImage(100, 50, os, 4);

        // 存入Session
        HttpSession session = request.getSession();
        session.setAttribute("checkCodeGen",checkCode);


    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doGet(request, response);
    }
}
```

(2)在RegisterServlet中，获取页面的和session对象中的验证码，进行对比

```java
package com.itheima.web;

import com.itheima.pojo.User;
import com.itheima.service.UserService;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.*;
import java.io.IOException;

@WebServlet("/registerServlet")
public class RegisterServlet extends HttpServlet {
    private UserService service = new UserService();

    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
       //1. 获取用户名和密码数据
        String username = request.getParameter("username");
        String password = request.getParameter("password");

        User user = new User();
        user.setUsername(username);
        user.setPassword(password);

        // 获取用户输入的验证码
        String checkCode = request.getParameter("checkCode");

        // 程序生成的验证码，从Session获取
        HttpSession session = request.getSession();
        String checkCodeGen = (String) session.getAttribute("checkCodeGen");

        // 比对
        if(!checkCodeGen.equalsIgnoreCase(checkCode)){

            request.setAttribute("register_msg","验证码错误");
            request.getRequestDispatcher("/register.jsp").forward(request,response);

            // 不允许注册
            return;
        }
        //2. 调用service 注册
        boolean flag = service.register(user);
        //3. 判断注册成功与否
        if(flag){
             //注册功能，跳转登陆页面

            request.setAttribute("register_msg","注册成功，请登录");
            request.getRequestDispatcher("/login.jsp").forward(request,response);
        }else {
            //注册失败，跳转到注册页面

            request.setAttribute("register_msg","用户名已存在");
            request.getRequestDispatcher("/register.jsp").forward(request,response);
        }


    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doGet(request, response);
    }
}
```

至此，用户的注册登录功能就已经完成了。

(8)





### 案例感受

首先，环境的初始化，文件的摆放的位置，dao层，mybatis,mapper,service

配置放在resources,逻辑代码放在java ,前端页面放在webapp;



# Filter&Listener&Ajax

**今日目标：**

> * 能够使用 Filter 完成登陆状态校验功能
> * 能够使用 axios 发送 ajax 请求
> * 熟悉 json 格式，并能使用 Fastjson 完成 java 对象和 json 串的相互转换
> * 使用 axios + json 完成综合案例

## 1，Filter

### 1.1  Filter概述

Filter 表示过滤器，是 JavaWeb 三大组件(Servlet、Filter、Listener)之一。Servlet 之前都已经学习过了，Filter和Listener 今天都会进行学习。

过滤器可以把对资源的请求==拦截==下来，从而实现一些特殊的功能。

如下图所示，浏览器可以访问服务器上的所有的资源（servlet、jsp、html等）

<img src="D:/download/downloadFromMicsoft/day12-Filter&Listener&Ajax（补充资料）/day12-Filter&Listener&Ajax/assets/image-20210823184519509.png" alt="image-20210823184519509" style="zoom:50%;" />

而在访问到这些资源之前可以使过滤器拦截来下，也就是说在访问资源之前会先经过 Filter，如下图

<img src="D:/download/downloadFromMicsoft/day12-Filter&Listener&Ajax（补充资料）/day12-Filter&Listener&Ajax/assets/image-20210823184657328.png" alt="image-20210823184657328" style="zoom:57%;" />

拦截器拦截到后可以做什么功能呢？

==过滤器一般完成一些通用的操作。==比如每个资源都要写一些代码完成某个功能，总不能在每个资源中写这样的代码吧，而此时可以将这些代码写在过滤器中，因为请求每一个资源都要经过过滤器。

之前做的品牌数据管理的案例中就已经做了登陆的功能，而如果不登录能不能访问到数据呢？可以在浏览器直接访问首页 ，可以看到 `查询所有` 的超链接

<img src="D:/download/downloadFromMicsoft/day12-Filter&Listener&Ajax（补充资料）/day12-Filter&Listener&Ajax/assets/image-20210823185720197.png" alt="image-20210823185720197" style="zoom:70%;" />

当我点击该按钮，居然可以看到品牌的数据

<img src="D:/download/downloadFromMicsoft/day12-Filter&Listener&Ajax（补充资料）/day12-Filter&Listener&Ajax/assets/image-20210823185932418.png" alt="image-20210823185932418" style="zoom:70%;" />

这显然和的要求不符。希望实现的效果是用户如果登陆过了就跳转到品牌数据展示的页面；如果没有登陆就跳转到登陆页面让用户进行登陆，要实现这个效果需要在每一个资源中都写上这段逻辑，而像这种通用的操作，就可以放在过滤器中进行实现。这个就是==权限控制==，以后还会进行细粒度权限控制。过滤器还可以做 `统一编码处理`、 `敏感字符处理` 等等…

### 1.2  Filter快速入门

#### 1.2.1  开发步骤

进行 `Filter` 开发分成以下三步实现

* 定义类，实现 Filter接口，并重写其所有方法

  <img src="D:/download/downloadFromMicsoft/day12-Filter&Listener&Ajax（补充资料）/day12-Filter&Listener&Ajax/assets/image-20210823191006878.png" alt="image-20210823191006878" style="zoom:60%;" />

* 配置Filter拦截资源的路径：在类上定义 `@WebFilter` 注解。而注解的 `value` 属性值 `/*` 表示拦截所有的资源

  <img src="D:/download/downloadFromMicsoft/day12-Filter&Listener&Ajax（补充资料）/day12-Filter&Listener&Ajax/assets/image-20210823191037163.png" alt="image-20210823191037163" style="zoom:67%;" />

* 在doFilter方法中输出一句话，并放行

  <img src="D:/download/downloadFromMicsoft/day12-Filter&Listener&Ajax（补充资料）/day12-Filter&Listener&Ajax/assets/image-20210823191200201.png" alt="image-20210823191200201" style="zoom:60%;" />

  > 上述代码中的 `chain.doFilter(request,response);` 就是放行，也就是让其访问本该访问的资源。

#### 1.2.2  代码演示

创建一个项目，项目下有一个 `hello.jsp` 页面，项目结构如下：

<img src="D:/download/downloadFromMicsoft/day12-Filter&Listener&Ajax（补充资料）/day12-Filter&Listener&Ajax/assets/image-20210823191855765.png" alt="image-20210823191855765" style="zoom:80%;" />

`pom.xml` 配置文件内容如下：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>org.example</groupId>
    <artifactId>filter-demo</artifactId>
    <version>1.0-SNAPSHOT</version>
    <packaging>war</packaging>

    <properties>
        <maven.compiler.source>8</maven.compiler.source>
        <maven.compiler.target>8</maven.compiler.target>
    </properties>

    <dependencies>
        <dependency>
            <groupId>javax.servlet</groupId>
            <artifactId>javax.servlet-api</artifactId>
            <version>3.1.0</version>
            <scope>provided</scope>
        </dependency>
    </dependencies>

    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.tomcat.maven</groupId>
                <artifactId>tomcat7-maven-plugin</artifactId>
                <version>2.2</version>
                <configuration>
                    <port>80</port>
                </configuration>
            </plugin>
        </plugins>
    </build>
</project>
```

`hello.jsp` 页面内容如下：

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
    <h1>hello JSP~</h1>
</body>
</html>
```

现在在浏览器输入 `http://localhost/filter-demo/hello.jsp` 访问 `hello.jsp` 页面，这里是可以访问到 `hello.jsp` 页面内容的。

<img src="D:/download/downloadFromMicsoft/day12-Filter&Listener&Ajax（补充资料）/day12-Filter&Listener&Ajax/assets/image-20210823192353031.png" alt="image-20210823192353031" style="zoom:67%;" />

接下来编写过滤器。过滤器是 Web 三大组件之一，所以将 `filter` 创建在 `com.itheima.web.filter` 包下，起名为 `FilterDemo`

```java
@WebFilter("/*")
public class FilterDemo implements Filter {

    @Override
    public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain) throws IOException, ServletException {
        System.out.println("FilterDemo...");
    }

    @Override
    public void init(FilterConfig filterConfig) throws ServletException {
    }

    @Override
    public void destroy() {
    }
}

```

重启启动服务器，再次重新访问 `hello.jsp` 页面，这次发现页面没有任何效果，但是在 `idea` 的控制台可以看到如下内容

<img src="D:/download/downloadFromMicsoft/day12-Filter&Listener&Ajax（补充资料）/day12-Filter&Listener&Ajax/assets/image-20210823193759365.png" alt="image-20210823193759365" style="zoom:70%;" />

上述效果说明 `FilterDemo` 这个过滤器的 `doFilter()` 方法执行了，但是为什么在浏览器上看不到 `hello.jsp` 页面的内容呢？这是因为在 `doFilter()` 方法中添加放行的方法才能访问到 `hello.jsp` 页面。那就在 `doFilter()` 方法中添加放行的代码

```java
//放行
 chain.doFilter(request,response);
```

再次重启服务器并访问 `hello.jsp` 页面，发现这次就可以在浏览器上看到页面效果。

**`FilterDemo` 过滤器完整代码如下：**

```java
@WebFilter("/*")
public class FilterDemo implements Filter {

    @Override
    public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain) throws IOException, ServletException {
        System.out.println("1.FilterDemo...");
        //放行
        chain.doFilter(request,response);
    }

    @Override
    public void init(FilterConfig filterConfig) throws ServletException {
    }

    @Override
    public void destroy() {
    }
}

```

### 1.3  Filter执行流程！！

<img src="D:/download/downloadFromMicsoft/day12-Filter&Listener&Ajax（补充资料）/day12-Filter&Listener&Ajax/assets/image-20210823194830074.png" alt="image-20210823194830074" style="zoom:70%;" />

如上图是使用过滤器的流程，通过以下问题来研究过滤器的执行流程：

* 放行后访问对应资源，资源访问完成后，还会回到Filter中吗？

  从上图就可以看出肯定 ==会== 回到Filter中

* 如果回到Filter中，是重头执行还是执行放行后的逻辑呢？

  如果是重头执行的话，就意味着 `放行前逻辑` 会被执行两次，肯定不会这样设计了；所以访问完资源后，会回到 `放行后逻辑`，执行该部分代码。

通过上述的说明，就可以总结Filter的执行流程如下：

<img src="D:/download/downloadFromMicsoft/day12-Filter&Listener&Ajax（补充资料）/day12-Filter&Listener&Ajax/assets/image-20210823195434581.png" alt="image-20210823195434581" style="zoom:70%;" />

接下来通过代码验证一下，在 `doFilter()` 方法前后都加上输出语句，如下

<img src="D:/download/downloadFromMicsoft/day12-Filter&Listener&Ajax（补充资料）/day12-Filter&Listener&Ajax/assets/image-20210823195828596.png" alt="image-20210823195828596" style="zoom:70%;" />

同时在 `hello.jsp` 页面加上输出语句，如下

<img src="D:/download/downloadFromMicsoft/day12-Filter&Listener&Ajax（补充资料）/day12-Filter&Listener&Ajax/assets/image-20210823200028284.png" alt="image-20210823200028284" style="zoom:70%;" />

执行访问该资源打印的顺序是按照标记的标号进行打印的话，说明上边总结出来的流程是没有问题的。启动服务器访问 `hello.jsp` 页面，在控制台打印的内容如下：

<img src="D:/download/downloadFromMicsoft/day12-Filter&Listener&Ajax（补充资料）/day12-Filter&Listener&Ajax/assets/image-20210823200202153.png" alt="image-20210823200202153" style="zoom:80%;" />

以后可以将对请求进行处理的代码放在放行之前进行处理，而如果请求完资源后还要对响应的数据进行处理时可以在放行后进行逻辑处理。



根据Filter的执行顺序，在放行前对requset的数据进行处理，在放行后对response的数据进行处理

### 1.4  Filter拦截路径配置

拦截路径表示 Filter 会对请求的哪些资源进行拦截，使用 `@WebFilter` 注解进行配置。如：`@WebFilter("拦截路径")` 

！！！！！servlet也是资源，访问也会被阻拦，并且，注意，filter中没有放行如

```
  chain.doFilter(request,response);
```

则前端无法访问到资源（页面.jsp无法展示，servlet无法运行）





拦截路径有如下四种配置方式：

* 拦截具体的资源：/index.jsp：只有访问index.jsp时才会被拦截
* 目录拦截：/user/*：访问/user下的所有资源，都会被拦截
* 后缀名拦截：*.jsp：访问后缀名为jsp的资源，都会被拦截
* 拦截所有：/*：访问所有资源，都会被拦截

通过上面拦截路径的学习，大家会发现拦截路径的配置方式和 `Servlet` 的请求资源路径配置方式一样，但是表示的含义不同。

### 1.5  过滤器链

#### 1.5.1  概述

过滤器链是指在一个Web应用，可以配置多个过滤器，这多个过滤器称为过滤器链。

如下图就是一个过滤器链，学习过滤器链主要是学习过滤器链执行的流程

<img src="D:/download/downloadFromMicsoft/day12-Filter&Listener&Ajax（补充资料）/day12-Filter&Listener&Ajax/assets/image-20210823215835812.png" alt="image-20210823215835812" style="zoom:70%;" />

上图中的过滤器链执行是按照以下流程执行：

1. 执行 `Filter1` 的放行前逻辑代码
2. 执行 `Filter1` 的放行代码
3. 执行 `Filter2` 的放行前逻辑代码
4. 执行 `Filter2` 的放行代码
5. 访问到资源
6. 执行 `Filter2` 的放行后逻辑代码
7. 执行 `Filter1` 的放行后逻辑代码

以上流程串起来就像一条链子，故称之为过滤器链。

#### 1.5.2  代码演示

* 编写第一个过滤器 `FilterDemo` ，配置成拦截所有资源

  ```java
  @WebFilter("/*")
  public class FilterDemo implements Filter {
  
      @Override
      public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain) throws IOException, ServletException {
  
          //1. 放行前，对 request数据进行处理
          System.out.println("1.FilterDemo...");
          //放行
          chain.doFilter(request,response);
          //2. 放行后，对Response 数据进行处理
          System.out.println("3.FilterDemo...");
      }
  
      @Override
      public void init(FilterConfig filterConfig) throws ServletException {
      }
  
      @Override
      public void destroy() {
      }
  }
  ```

* 编写第二个过滤器 `FilterDemo2` ，配置炒年糕拦截所有资源

  ```java
  @WebFilter("/*")
  public class FilterDemo2 implements Filter {
  
      @Override
      public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain) throws IOException, ServletException {
  
          //1. 放行前，对 request数据进行处理
          System.out.println("2.FilterDemo...");
          //放行
          chain.doFilter(request,response);
          //2. 放行后，对Response 数据进行处理
          System.out.println("4.FilterDemo...");
      }
  
      @Override
      public void init(FilterConfig filterConfig) throws ServletException {
      }
  
      @Override
      public void destroy() {
      }
  }
  
  ```

* 修改 `hello.jsp` 页面中脚本的输出语句

  ```jsp
  <%@ page contentType="text/html;charset=UTF-8" language="java" %>
  <html>
  <head>
      <title>Title</title>
  </head>
  <body>
      <h1>hello JSP~</h1>
      <%
          System.out.println("3.hello jsp");
      %>
  </body>
  </html>
  ```

* 启动服务器，在浏览器输入 `http://localhost/filter-demo/hello.jsp` 进行测试，在控制台打印内容如下

  <img src="D:/download/downloadFromMicsoft/day12-Filter&Listener&Ajax（补充资料）/day12-Filter&Listener&Ajax/assets/image-20210823221222468.png" alt="image-20210823221222468" style="zoom:70%;" />

  

  从结果可以看到确实是按照之前说的执行流程进行执行的。

#### 1.5.3  问题

上面代码中为什么是先执行 `FilterDemo` ，后执行 `FilterDemo2` 呢？

现在使用的是注解配置Filter，而这种配置方式的优先级是按照过滤器类名(字符串)的自然排序。

比如有如下两个名称的过滤器 ： `BFilterDemo` 和 `AFilterDemo` 。那一定是 `AFilterDemo` 过滤器先执行。

### 1.6  案例

#### 1.6.1  需求

访问服务器资源时，需要先进行登录验证，如果没有登录，则自动跳转到登录页面

#### 1.6.2  分析

要实现该功能是在每一个资源里加入登陆状态校验的代码吗？显然是不需要的，只需要写一个 `Filter` ，在该过滤器中进行登陆状态校验即可。而在该 `Filter` 中逻辑如下：

<img src="D:/download/downloadFromMicsoft/day12-Filter&Listener&Ajax（补充资料）/day12-Filter&Listener&Ajax/assets/image-20210823223214525.png" alt="image-20210823223214525" style="zoom:70%;" />

#### 1.6.3  代码实现

##### 1.6.3.1  创建Filter

在 `brand-demo` 工程创建 `com.itheima.web.filter`  包，在该下创建名为 `LoginFilter` 的过滤器

```java
@WebFilter("/*")
public class LoginFilter implements Filter {
    @Override
    public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain) throws ServletException, IOException {
      
    }

    public void init(FilterConfig config) throws ServletException {
    }

    public void destroy() {
    }
}
```

##### 1.6.3.2  编写逻辑代码

在 `doFilter()` 方法中编写登陆状态校验的逻辑代码。

首先需要从 `session` 对象中获取用户信息，但是 `ServletRequest` 类型的 requset 对象没有获取 session 对象的方法，所以此时需要将 request对象强转成 `HttpServletRequest` 对象。

```java
HttpServletRequest req = (HttpServletRequest) request;
```

然后完成以下逻辑

* 获取Session对象
* 从Session对象中获取名为 `user` 的数据
* 判断获取到的数据是否是 null
  * 如果不是，说明已经登陆，放行
  * 如果是，说明尚未登陆，将提示信息存储到域对象中并跳转到登陆页面

代码如下：

```java
@WebFilter("/*")
public class LoginFilter implements Filter {
    @Override
    public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain) throws ServletException, IOException {
        HttpServletRequest req = (HttpServletRequest) request;
   
        //1. 判断session中是否有user
        HttpSession session = req.getSession();
        Object user = session.getAttribute("user");

        //2. 判断user是否为null
        if(user != null){
            // 登录过了
            //放行
            chain.doFilter(request, response);
        }else {
            // 没有登陆，存储提示信息，跳转到登录页面

            req.setAttribute("login_msg","您尚未登陆！");
            req.getRequestDispatcher("/login.jsp").forward(req,response);
        }
    }

    public void init(FilterConfig config) throws ServletException {
    }

    public void destroy() {
    }
}
```

##### 1.6.3.3  测试并抛出问题

在浏览器上输入 `http://localhost:8080/brand-demo/` ，可以看到如下页面效果

<img src="D:/download/downloadFromMicsoft/day12-Filter&Listener&Ajax（补充资料）/day12-Filter&Listener&Ajax/assets/image-20210823224843179.png" alt="image-20210823224843179" style="zoom:60%;" />

从上面效果可以看出没有登陆确实是跳转到登陆页面了，但是登陆页面为什么展示成这种效果了呢？

##### 1.6.3.4  问题分析及解决

因为登陆页面需要 `css/login.css` 这个文件进行样式的渲染，下图是登陆页面引入的css文件图解

<img src="D:/download/downloadFromMicsoft/day12-Filter&Listener&Ajax（补充资料）/day12-Filter&Listener&Ajax/assets/image-20210823225411925.png" alt="image-20210823225411925" style="zoom:70%;" />

而在请求这个css资源时被过滤器拦截，就相当于没有加载到样式文件导致的。解决这个问题，只需要对所以的登陆相关的资源进行放行即可。还有一种情况就是当我没有用户信息时需要进行注册，而注册时也希望被过滤器放行。

综上，需要在判断session中是否包含用户信息之前，应该加上对登陆及注册相关资源放行的逻辑处理

```java
//判断访问资源路径是否和登录注册相关
//1,在数组中存储登陆和注册相关的资源路径
String[] urls = {"/login.jsp","/imgs/","/css/","/loginServlet","/register.jsp","/registerServlet","/checkCodeServlet"};
//2,获取当前访问的资源路径
String url = req.getRequestURL().toString(); 

//3,遍历数组，获取到每一个需要放行的资源路径
for (String u : urls) {
    //4,判断当前访问的资源路径字符串是否包含要放行的的资源路径字符串
    /*
    	比如当前访问的资源路径是  /brand-demo/login.jsp
    	而字符串 /brand-demo/login.jsp 包含了  字符串 /login.jsp ，所以这个字符串就需要放行
    */
    if(url.contains(u)){
        //找到了，放行
        chain.doFilter(request, response);
        //break;
        return;
    }
}
```

##### 1.6.3.5  过滤器完整代码

```java
@WebFilter("/*")
public class LoginFilter implements Filter {
    @Override
    public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain) throws ServletException, IOException {
        HttpServletRequest req = (HttpServletRequest) request;
        
        //判断访问资源路径是否和登录注册相关
        //1,在数组中存储登陆和注册相关的资源路径
        String[] urls = {"/login.jsp","/imgs/","/css/","/loginServlet","/register.jsp","/registerServlet","/checkCodeServlet"};
        //2,获取当前访问的资源路径
        String url = req.getRequestURL().toString(); 

        //3,遍历数组，获取到每一个需要放行的资源路径
        for (String u : urls) {
            //4,判断当前访问的资源路径字符串是否包含要放行的的资源路径字符串
            /*
                比如当前访问的资源路径是  /brand-demo/login.jsp
                而字符串 /brand-demo/login.jsp 包含了  字符串 /login.jsp ，所以这个字符串就需要放行
            */
            if(url.contains(u)){
                //找到了，放行
                chain.doFilter(request, response);
                //break;
                return;
            }
        }
   
        //1. 判断session中是否有user
        HttpSession session = req.getSession();
        Object user = session.getAttribute("user");

        //2. 判断user是否为null
        if(user != null){
            // 登录过了
            //放行
            chain.doFilter(request, response);
        }else {
            // 没有登陆，存储提示信息，跳转到登录页面

            req.setAttribute("login_msg","您尚未登陆！");
            req.getRequestDispatcher("/login.jsp").forward(req,response);
        }
    }

    public void init(FilterConfig config) throws ServletException {
    }

    public void destroy() {
    }
}
```

## 2，Listener

### 2.1  概述

* Listener 表示监听器，是 JavaWeb 三大组件(Servlet、Filter、Listener)之一。

* 监听器可以监听就是在 `application`，`session`，`request` 三个对象创建、销毁或者往其中添加修改删除属性时自动执行代码的功能组件。

  request 和 session 学习过。而 `application` 是 `ServletContext` 类型的对象。

  `ServletContext` 代表整个web应用，在服务器启动的时候，tomcat会自动创建该对象。在服务器关闭时会自动销毁该对象。

### 2.2  分类

JavaWeb 提供了8个监听器：

<img src="D:/download/downloadFromMicsoft/day12-Filter&Listener&Ajax（补充资料）/day12-Filter&Listener&Ajax/assets/image-20210823230820586.png" alt="image-20210823230820586" style="zoom:80%;" />

这里面只有 `ServletContextListener` 这个监听器后期会接触到，`ServletContextListener` 是用来监听 `ServletContext` 对象的创建和销毁。

`ServletContextListener` 接口中有以下两个方法

* `void contextInitialized(ServletContextEvent sce)`：`ServletContext` 对象被创建了会自动执行的方法
* `void contextDestroyed(ServletContextEvent sce)`：`ServletContext` 对象被销毁时会自动执行的方法

### 2.3  代码演示

只演示一下 `ServletContextListener` 监听器

* 定义一个类，实现`ServletContextListener` 接口
* 重写所有的抽象方法
* 使用 `@WebListener` 进行配置

代码如下：

```java
@WebListener
public class ContextLoaderListener implements ServletContextListener {
    @Override
    public void contextInitialized(ServletContextEvent sce) {
        //加载资源
        System.out.println("ContextLoaderListener...");
    }

    @Override
    public void contextDestroyed(ServletContextEvent sce) {
        //释放资源
    }
}
```

启动服务器，就可以在启动的日志信息中看到 `contextInitialized()` 方法输出的内容，同时也说明了 `ServletContext` 对象在服务器启动的时候被创建了。

## 3，Ajax

### 3.1  概述

==`AJAX` (Asynchronous JavaScript And XML)：异步的 JavaScript 和 XML。==

先来说概念中的 `JavaScript` 和 `XML`，`JavaScript` 表明该技术和前端相关；`XML` 是指以此进行数据交换。而这两个之前都学习过。

#### 3.1.1  作用

AJAX 作用有以下两方面：

1. **与服务器进行数据交换**：通过AJAX可以给服务器发送请求，服务器将数据直接响应回给浏览器。如下图

先来看之前做功能的流程，如下图：

<img src="D:/download/downloadFromMicsoft/day12-Filter&Listener&Ajax（补充资料）/day12-Filter&Listener&Ajax/assets/image-20210823235114367.png" alt="image-20210823235114367" style="zoom:70%;" />

如上图，`Servlet` 调用完业务逻辑层后将数据存储到域对象中，然后跳转到指定的 `jsp` 页面，在页面上使用 `EL表达式` 和 `JSTL` 标签库进行数据的展示。

而学习了AJAX 后，就可以==使用AJAX和服务器进行通信，以达到使用 HTML+AJAX来替换JSP页面==了。如下图，浏览器发送请求servlet，servlet 调用完业务逻辑层后将数据直接响应回给浏览器页面，页面使用 HTML 来进行数据展示。

<img src="D:/download/downloadFromMicsoft/day12-Filter&Listener&Ajax（补充资料）/day12-Filter&Listener&Ajax/assets/image-20210823235006847.png" alt="image-20210823235006847" style="zoom:70%;" />

2. **异步交互**：可以在==不重新加载整个页面==的情况下，与服务器交换数据并==更新部分网页==的技术，如：搜索联想、用户名是否可用校验，等等…

<img src="D:/download/downloadFromMicsoft/day12-Filter&Listener&Ajax（补充资料）/day12-Filter&Listener&Ajax/assets/image-20210824000706401.png" alt="image-20210824000706401" style="zoom:80%;" />

上图所示的效果经常见到，在输入一些关键字（例如 `奥运`）后就会在下面联想出相关的内容，而联想出来的这部分数据肯定是存储在百度的服务器上，而并没有看出页面重新刷新，这就是 ==更新局部页面== 的效果。再如下图：

<img src="D:/download/downloadFromMicsoft/day12-Filter&Listener&Ajax（补充资料）/day12-Filter&Listener&Ajax/assets/image-20210824001015706.png" alt="image-20210824001015706" style="zoom:80%;" />

在用户名的输入框输入用户名，当输入框一失去焦点，如果用户名已经被占用就会在下方展示提示的信息；在这整个过程中也没有页面的刷新，只是在局部展示出了提示信息，这就是 ==更新局部页面== 的效果。

#### 3.1.2  同步和异步

知道了局部刷新后，接下来再聊聊同步和异步:

* 同步发送请求过程如下

<img src="D:/download/downloadFromMicsoft/day12-Filter&Listener&Ajax（补充资料）/day12-Filter&Listener&Ajax/assets/image-20210824001443897.png" alt="image-20210824001443897" style="zoom:80%;" />

​	浏览器页面在发送请求给服务器，在服务器处理请求的过程中，浏览器页面不能做其他的操作。只能等到服务器响应结束后才能，浏览器页面才能继续做其他的操作。

* 异步发送请求过程如下

  <img src="D:/download/downloadFromMicsoft/day12-Filter&Listener&Ajax（补充资料）/day12-Filter&Listener&Ajax/assets/image-20210824001608916.png" alt="image-20210824001608916" style="zoom:80%;" />

  浏览器页面发送请求给服务器，在服务器处理请求的过程中，浏览器页面还可以做其他的操作。

### 3.2  快速入门

#### 3.2.1 服务端实现

在项目的创建 `com.itheima.web.servlet` ，并在该包下创建名为  `AjaxServlet` 的servlet

```java
@WebServlet("/ajaxServlet")
public class AjaxServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //1. 响应数据
        response.getWriter().write("hello ajax~");
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doGet(request, response);
    }
}
```

#### 3.2.2  客户端实现

在 `webapp` 下创建名为 `01-ajax-demo1.html` 的页面，在该页面书写 `ajax` 代码

* 创建核心对象，不同的浏览器创建的对象是不同的

  ```js
   var xhttp;
  if (window.XMLHttpRequest) {
      xhttp = new XMLHttpRequest();
  } else {
      // code for IE6, IE5
      xhttp = new ActiveXObject("Microsoft.XMLHTTP");
  }
  ```

* 发送请求

  ```js
  //建立连接
  xhttp.open("GET", "http://localhost:8080/ajax-demo/ajaxServlet");
  //发送请求
  xhttp.send();
  ```

* 获取响应

  ```js
  xhttp.onreadystatechange = function() {
      if (this.readyState == 4 && this.status == 200) {
          // 通过 this.responseText 可以获取到服务端响应的数据
          alert(this.responseText);
      }
  };
  ```

**完整代码如下：**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>

<script>
    //1. 创建核心对象
    var xhttp;
    if (window.XMLHttpRequest) {
        xhttp = new XMLHttpRequest();
    } else {
        // code for IE6, IE5
        xhttp = new ActiveXObject("Microsoft.XMLHTTP");
    }
    //2. 发送请求
    xhttp.open("GET", "http://localhost:8080/ajax-demo/ajaxServlet");
    xhttp.send();

    //3. 获取响应
    xhttp.onreadystatechange = function() {
        if (this.readyState == 4 && this.status == 200) {
            alert(this.responseText);
        }
    };
</script>
</body>
</html>
```

#### 3.2.3  测试

在浏览器地址栏输入 `http://localhost:8080/ajax-demo/01-ajax-demo1.html` ，在 `01-ajax-demo1.html`加载的时候就会发送 `ajax` 请求，效果如下

<img src="D:/download/downloadFromMicsoft/day12-Filter&Listener&Ajax（补充资料）/day12-Filter&Listener&Ajax/assets/image-20210824005956117.png" alt="image-20210824005956117" style="zoom:67%;" />

可以通过 `开发者模式` 查看发送的 AJAX 请求。在浏览器上按 `F12` 快捷键

<img src="D:/download/downloadFromMicsoft/day12-Filter&Listener&Ajax（补充资料）/day12-Filter&Listener&Ajax/assets/image-20210824010247642.png" alt="image-20210824010247642" style="zoom:80%;" />

这个是查看所有的请求，如果只是想看 异步请求的话，点击上图中 `All` 旁边的 `XHR`，会发现只展示 Type 是 `xhr` 的请求。如下图：

<img src="D:/download/downloadFromMicsoft/day12-Filter&Listener&Ajax（补充资料）/day12-Filter&Listener&Ajax/assets/image-20210824010438260.png" alt="image-20210824010438260" style="zoom:80%;" /> 

### 3.3 案例

需求：在完成用户注册时，当用户名输入框失去焦点时，校验用户名是否在数据库已存在

<img src="D:/download/downloadFromMicsoft/day12-Filter&Listener&Ajax（补充资料）/day12-Filter&Listener&Ajax/assets/image-20210824201415745.png" alt="image-20210824201415745" style="zoom:60%;" />

#### 3.3.1  分析

* **前端完成的逻辑**
  1.  给用户名输入框绑定光标失去焦点事件 `onblur`
  2.  发送 ajax请求，携带username参数
  3.  处理响应：是否显示提示信息
* **后端完成的逻辑**
  1. 接收用户名
  2. 调用service查询User。此案例是为了演示前后端异步交互，所以此处不做业务逻辑处理
  3. 返回标记

整体流程如下：

<img src="D:/download/downloadFromMicsoft/day12-Filter&Listener&Ajax（补充资料）/day12-Filter&Listener&Ajax/assets/image-20210829183854285.png" alt="image-20210829183854285" style="zoom:80%;" />

#### 3.3.2  后端实现

在 `com.ithiema.web.servlet` 包中定义名为 `SelectUserServlet`  的servlet。代码如下：

```java
@WebServlet("/selectUserServlet")
public class SelectUserServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //1. 接收用户名
        String username = request.getParameter("username");
        //2. 调用service查询User对象，此处不进行业务逻辑处理，直接给 flag 赋值为 true，表明用户名占用
        boolean flag = true;
        //3. 响应标记
        response.getWriter().write("" + flag);
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doGet(request, response);
    }
}
```

#### 3.3.3  前端实现

将 `04-资料\1. 验证用户名案例\1. 静态页面` 下的文件整体拷贝到项目下 `webapp` 下。并在 `register.html` 页面的 `body` 结束标签前编写 `script` 标签，在该标签中实现如下逻辑

**第一步：给用户名输入框绑定光标失去焦点事件 `onblur`**

```js
//1. 给用户名输入框绑定 失去焦点事件
document.getElementById("username").onblur = function () {
    
}
```

**第二步：发送 ajax请求，携带username参数**

在 `第一步` 绑定的匿名函数中书写发送 ajax 请求的代码

```js
//2. 发送ajax请求
//2.1. 创建核心对象
var xhttp;
if (window.XMLHttpRequest) {
    xhttp = new XMLHttpRequest();
} else {
    // code for IE6, IE5
    xhttp = new ActiveXObject("Microsoft.XMLHTTP");
}
//2.2. 发送请求
xhttp.open("GET", "http://localhost:8080/ajax-demo/selectUserServlet);
xhttp.send();

//2.3. 获取响应
xhttp.onreadystatechange = function() {
    if (this.readyState == 4 && this.status == 200) {
        //处理响应的结果
    }
};
```

由于发送的是 GET 请求，所以需要在 URL 后拼接从输入框获取的用户名数据。而在 `第一步` 绑定的匿名函数中通过以下代码可以获取用户名数据

```js
// 获取用户名的值
var username = this.value;  //this ： 给谁绑定的事件，this就代表谁
```

而携带数据需要将 URL 修改为：

```js
xhttp.open("GET", "http://localhost:8080/ajax-demo/selectUserServlet?username="+username);
```

**第三步：处理响应：是否显示提示信息**

当 `this.readyState == 4 && this.status == 200` 条件满足时，说明已经成功响应数据了。

此时需要判断响应的数据是否是 "true" 字符串，如果是说明用户名已经占用给出错误提示；如果不是说明用户名未被占用清除错误提示。代码如下

```js
//判断
if(this.responseText == "true"){
    //用户名存在，显示提示信息
    document.getElementById("username_err").style.display = '';
}else {
    //用户名不存在 ，清楚提示信息
    document.getElementById("username_err").style.display = 'none';
}
```

**综上所述，前端完成代码如下：**

```js
//1. 给用户名输入框绑定 失去焦点事件
document.getElementById("username").onblur = function () {
    //2. 发送ajax请求
    // 获取用户名的值
    var username = this.value;

    //2.1. 创建核心对象
    var xhttp;
    if (window.XMLHttpRequest) {
        xhttp = new XMLHttpRequest();
    } else {
        // code for IE6, IE5
        xhttp = new ActiveXObject("Microsoft.XMLHTTP");
    }
    //2.2. 发送请求
    xhttp.open("GET", "http://localhost:8080/ajax-demo/selectUserServlet?username="+username);
    xhttp.send();

    //2.3. 获取响应
    xhttp.onreadystatechange = function() {
        if (this.readyState == 4 && this.status == 200) {
            //alert(this.responseText);
            //判断
            if(this.responseText == "true"){
                //用户名存在，显示提示信息
                document.getElementById("username_err").style.display = '';
            }else {
                //用户名不存在 ，清楚提示信息
                document.getElementById("username_err").style.display = 'none';
            }
        }
    };
}
```

## 4，axios

Axios 对原生的AJAX进行封装，简化书写。

Axios官网是：`https://www.axios-http.cn`

### 4.1  基本使用

axios 使用是比较简单的，分为以下两步：

* 引入 axios 的 js 文件

  ```html
  <script src="js/axios-0.18.0.js"></script>
  ```

* 使用axios 发送请求，并获取响应结果

  * 发送 get 请求

    ```js
    axios({
        method:"get",
        url:"http://localhost:8080/ajax-demo1/aJAXDemo1?username=zhangsan"
    }).then(function (resp){
        alert(resp.data);
    })
    ```

  * 发送 post 请求

    ```js
    axios({
        method:"post",
        url:"http://localhost:8080/ajax-demo1/aJAXDemo1",
        data:"username=zhangsan"
    }).then(function (resp){
        alert(resp.data);
    });
    ```

`axios()` 是用来发送异步请求的，小括号中使用 js 对象传递请求相关的参数：

* `method` 属性：用来设置请求方式的。取值为 `get` 或者 `post`。
* `url` 属性：用来书写请求的资源路径。如果是 `get` 请求，需要将请求参数拼接到路径的后面，格式为： `url?参数名=参数值&参数名2=参数值2`。
* `data` 属性：作为请求体被发送的数据。也就是说如果是 `post` 请求的话，数据需要作为 `data` 属性的值。

`then()` 需要传递一个匿名函数。将 `then()` 中传递的匿名函数称为 ==回调函数==，意思是该匿名函数在发送请求时不会被调用，而是在成功响应后调用的函数。而该回调函数中的 `resp` 参数是对响应的数据进行封装的对象，通过 `resp.data` 可以获取到响应的数据。

### 4.2  快速入门

#### 4.2.1  后端实现

定义一个用于接收请求的servlet，代码如下：

```java
@WebServlet("/axiosServlet")
public class AxiosServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        System.out.println("get...");
        //1. 接收请求参数
        String username = request.getParameter("username");
        System.out.println(username);
        //2. 响应数据
        response.getWriter().write("hello Axios~");
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        System.out.println("post...");
        this.doGet(request, response);
    }
}
```

#### 4.2.2  前端实现

* 引入 js 文件

  ```js
  <script src="js/axios-0.18.0.js"></script>
  ```

* 发送 ajax 请求

  * get 请求

    ```js
    axios({
        method:"get",
        url:"http://localhost:8080/ajax-demo/axiosServlet?username=zhangsan"
    }).then(function (resp) {
        alert(resp.data);
    })
    ```

  * post 请求

    ```js
    axios({
        method:"post",
        url:"http://localhost:8080/ajax-demo/axiosServlet",
        data:"username=zhangsan"
    }).then(function (resp) {
        alert(resp.data);
    })
    ```

**整体页面代码如下：**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>

<script src="js/axios-0.18.0.js"></script>
<script>
    //1. get
   /* axios({
        method:"get",
        url:"http://localhost:8080/ajax-demo/axiosServlet?username=zhangsan"
    }).then(function (resp) {
        alert(resp.data);
    })*/

    //2. post  在js中{} 表示一个js对象，而这个js对象中有三个属性
    axios({
        method:"post",
        url:"http://localhost:8080/ajax-demo/axiosServlet",
        data:"username=zhangsan"
    }).then(function (resp) {
        alert(resp.data);
    })
</script>
</body>
</html>
```

### 4.3  请求方法别名

为了方便起见， Axios 已经为所有支持的请求方法提供了别名。如下：

* `get` 请求 ： `axios.get(url[,config])`

* `delete` 请求 ： `axios.delete(url[,config])`

* `head` 请求 ： `axios.head(url[,config])`

* `options` 请求 ： `axios.option(url[,config])`

* `post` 请求：`axios.post(url[,data[,config])`

* `put` 请求：`axios.put(url[,data[,config])`

* `patch` 请求：`axios.patch(url[,data[,config])`

而只关注 `get` 请求和 `post` 请求。

入门案例中的 `get` 请求代码可以改为如下：

```js
axios.get("http://localhost:8080/ajax-demo/axiosServlet?username=zhangsan").then(function (resp) {
    alert(resp.data);
});
```

入门案例中的 `post` 请求代码可以改为如下：

```js
axios.post("http://localhost:8080/ajax-demo/axiosServlet","username=zhangsan").then(function (resp) {
    alert(resp.data);
})
```

## 5，JSON

### 5.1  概述

==概念：`JavaScript Object Notation`。JavaScript 对象表示法.==

如下是 `JavaScript` 对象的定义格式：

```js
{
	name:"zhangsan",
	age:23,
	city:"北京"
}
```

接下来再看看 `JSON` 的格式：

```json
{
	"name":"zhangsan",
	"age":23,
	"city":"北京"
}
```

通过上面 js 对象格式和 json 格式进行对比，发现两个格式特别像。只不过 js 对象中的属性名可以使用引号（可以是单引号，也可以是双引号）；而 `json` 格式中的键要求必须使用双引号括起来，这是 `json` 格式的规定。`json` 格式的数据有什么作用呢？

作用：由于其语法格式简单，层次结构鲜明，现多用于作为==数据载体==，在网络中进行数据传输。如下图所示就是服务端给浏览器响应的数据，这个数据比较简单，如果现需要将 JAVA 对象中封装的数据响应回给浏览器的话，应该以何种数据传输呢？

<img src="D:/download/downloadFromMicsoft/day12-Filter&Listener&Ajax（补充资料）/day12-Filter&Listener&Ajax/assets/image-20210830232718632.png" alt="image-20210830232718632" style="zoom:80%;" />

大家还记得 `ajax` 的概念吗？ 是 ==异步的 JavaScript 和 xml==。这里的 xml就是以前进行数据传递的方式，如下：

```xml
<student>
    <name>张三</name>
    <age>23</age>
    <city>北京</city>
</student>
```

再看 `json` 描述以上数据的写法：

```json
{	
	"name":"张三",
    "age":23,
    "city":"北京"
}
```

上面两种格式进行对比后就会发现 `json` 格式数据的简单，以及所占的字节数少等优点。

### 5.2  JSON 基础语法

#### 5.2.1  定义格式

`JSON` 本质就是一个字符串，但是该字符串内容是有一定的格式要求的。 定义格式如下：

```js
var 变量名 = '{"key":value,"key":value,...}';
```

`JSON` 串的键要求必须使用双引号括起来，而值根据要表示的类型确定。value 的数据类型分为如下

* 数字（整数或浮点数）
* 字符串（使用双引号括起来）
* 逻辑值（true或者false）
* 数组（在方括号中）
* 对象（在花括号中）
* null

示例：

```js
var jsonStr = '{"name":"zhangsan","age":23,"addr":["北京","上海","西安"]}'
```

#### 5.2.2  代码演示

创建一个页面，在该页面的 `<script>` 标签中定义json字符串

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<script>
    //1. 定义JSON字符串
    var jsonStr = '{"name":"zhangsan","age":23,"addr":["北京","上海","西安"]}'
    alert(jsonStr);

</script>
</body>
</html>
```

通过浏览器打开，页面效果如下图所示

<img src="D:/download/downloadFromMicsoft/day12-Filter&Listener&Ajax（补充资料）/day12-Filter&Listener&Ajax/assets/image-20210831223339530.png" alt="image-20210831223339530" style="zoom:80%;" />

现在需要获取到该 `JSON` 串中的 `name` 属性值，应该怎么处理呢？

如果它是一个 js 对象，就可以通过 `js对象.属性名` 的方式来获取数据。JS 提供了一个对象 `JSON` ，该对象有如下两个方法：

* `parse(str)` ：将 JSON串转换为 js 对象。使用方式是： ==`var jsObject = JSON.parse(jsonStr);`==
* `stringify(obj)` ：将 js 对象转换为 JSON 串。使用方式是：==`var jsonStr = JSON.stringify(jsObject)`==

代码演示：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<script>
    //1. 定义JSON字符串
    var jsonStr = '{"name":"zhangsan","age":23,"addr":["北京","上海","西安"]}'
    alert(jsonStr);

    //2. 将 JSON 字符串转为 JS 对象
    let jsObject = JSON.parse(jsonStr);
    alert(jsObject)
    alert(jsObject.name)
    //3. 将 JS 对象转换为 JSON 字符串
    let jsonStr2 = JSON.stringify(jsObject);
    alert(jsonStr2)
</script>
</body>
</html>
```

#### 5.2.3  发送异步请求携带参数

后面使用 `axios` 发送请求时，如果要携带复杂的数据时都会以 `JSON` 格式进行传递，如下

```js
axios({
    method:"post",
    url:"http://localhost:8080/ajax-demo/axiosServlet",
    data:"username=zhangsan"
}).then(function (resp) {
    alert(resp.data);
})
```

请求参数不可能由自己拼接字符串吧？肯定不用，可以提前定义一个 js 对象，用来封装需要提交的参数，然后使用 `JSON.stringify(js对象)` 转换为 `JSON` 串，再将该 `JSON` 串作为 `axios` 的 `data` 属性值进行请求参数的提交。如下：

```js
var jsObject = {name:"张三"};

axios({
    method:"post",
    url:"http://localhost:8080/ajax-demo/axiosServlet",
    data: JSON.stringify(jsObject)
}).then(function (resp) {
    alert(resp.data);
})
```

而 `axios` 是一个很强大的工具。只需要将需要提交的参数封装成 js 对象，并将该 js 对象作为 `axios` 的 `data` 属性值进行，它会自动将 js 对象转换为 `JSON` 串进行提交。如下：

```js
var jsObject = {name:"张三"};

axios({
    method:"post",
    url:"http://localhost:8080/ajax-demo/axiosServlet",
    data:jsObject  //这里 axios 会将该js对象转换为 json 串的
}).then(function (resp) {
    alert(resp.data);
})
```

> ==注意：==
>
> * js 提供的 `JSON` 对象只需要了解一下即可。因为 `axios` 会自动对 js 对象和 `JSON` 串进行想换转换。
> * 发送异步请求时，如果请求参数是 `JSON` 格式，那请求方式必须是 `POST`。因为 `JSON` 串需要放在请求体中。

### 5.3  JSON串和Java对象的相互转换

学习完 json 后，接下来聊聊 json 的作用。以后会以 json 格式的数据进行前后端交互。前端发送请求时，如果是复杂的数据就会以 json 提交给后端；而后端如果需要响应一些复杂的数据时，也需要以 json 格式将数据响应回给浏览器。

<img src="D:/download/downloadFromMicsoft/day12-Filter&Listener&Ajax（补充资料）/day12-Filter&Listener&Ajax/assets/image-20210831104901912.png" alt="image-20210831104901912" style="zoom:70%;" />

在后端就需要重点学习以下两部分操作：

* 请求数据：JSON字符串转为Java对象
* 响应数据：Java对象转为JSON字符串

接下来给大家介绍一套 API，可以实现上面两部分操作。这套 API 就是 `Fastjson`

#### 5.3.1  Fastjson 概述

`Fastjson` 是阿里巴巴提供的一个Java语言编写的高性能功能完善的 `JSON` 库，是目前Java语言中最快的 `JSON` 库，可以实现 `Java` 对象和 `JSON` 字符串的相互转换。

#### 5.3.2  Fastjson 使用

`Fastjson` 使用也是比较简单的，分为以下三步完成

1. **导入坐标**

   ```xml
   <dependency>
       <groupId>com.alibaba</groupId>
       <artifactId>fastjson</artifactId>
       <version>1.2.62</version>
   </dependency>
   ```

2. **Java对象转JSON**

   ```java
   String jsonStr = JSON.toJSONString(obj);
   ```

   将 Java 对象转换为 JSON 串，只需要使用 `Fastjson` 提供的 `JSON` 类中的 `toJSONString()` 静态方法即可。

3. **JSON字符串转Java对象**

   ```java
   User user = JSON.parseObject(jsonStr, User.class);
   ```

   将 json 转换为 Java 对象，只需要使用 `Fastjson` 提供的 `JSON` 类中的 `parseObject()` 静态方法即可。

#### 5.3.3  代码演示

* 引入坐标

* 创建一个类，专门用来测试 Java 对象和 JSON 串的相互转换，代码如下：

  ```java
  public class FastJsonDemo {
  
      public static void main(String[] args) {
          //1. 将Java对象转为JSON字符串
          User user = new User();
          user.setId(1);
          user.setUsername("zhangsan");
          user.setPassword("123");
  
          String jsonString = JSON.toJSONString(user);
          System.out.println(jsonString);//{"id":1,"password":"123","username":"zhangsan"}
  
  
          //2. 将JSON字符串转为Java对象
          User u = JSON.parseObject("{\"id\":1,\"password\":\"123\",\"username\":\"zhangsan\"}", User.class);
          System.out.println(u);
      }
  }
  ```

  

## 6，案例

### 6.1  需求

使用Axios + JSON 完成品牌列表数据查询和添加。页面效果还是下图所示：

<img src="D:/download/downloadFromMicsoft/day12-Filter&Listener&Ajax（补充资料）/day12-Filter&Listener&Ajax/assets/image-20210830234803335.png" alt="image-20210830234803335" style="zoom:60%;" />

### 6.2  查询所有功能

![image-20210831085332612](D:/download/downloadFromMicsoft/day12-Filter&Listener&Ajax（补充资料）/day12-Filter&Listener&Ajax/assets/image-20210831085332612.png)

如上图所示就该功能的整体流程。前后端需以 JSON 格式进行数据的传递；由于此功能是查询所有的功能，前端发送 ajax 请求不需要携带参数，而后端响应数据需以如下格式的 json 数据

![image-20210831090839336](D:/download/downloadFromMicsoft/day12-Filter&Listener&Ajax（补充资料）/day12-Filter&Listener&Ajax/assets/image-20210831090839336.png)

#### 6.2.1  环境准备

将 `02-AJAX\04-资料\3. 品牌列表案例\初始工程` 下的 `brand-demo` 工程拷贝到自己 `工作空间` ，然后再将项目导入到自己的 Idea 中。工程目录结构如下：

<img src="D:/download/downloadFromMicsoft/day12-Filter&Listener&Ajax（补充资料）/day12-Filter&Listener&Ajax/assets/image-20210831091604457.png" alt="image-20210831091604457" style="zoom:80%;" />

==注意：==

* 在给定的原始工程中已经给定一些代码。而在此案例中只关注前后端交互代码实现
* 要根据自己的数据库环境去修改连接数据库的信息，在 `mybatis-config.xml` 核心配置文件中修改

#### 6.2.2  后端实现

在 `com.itheima.web` 包下创建名为 `SelectAllServlet` 的 `servlet`，具体的逻辑如下：

* 调用 service 的 `selectAll()` 方法进行查询所有的逻辑处理
* 将查询到的集合数据转换为 json 数据。将此过程称为 ==序列化==；如果是将 json 数据转换为 Java 对象，称之为 ==反序列化==
* 将 json 数据响应回给浏览器。这里一定要设置响应数据的类型及字符集 `response.setContentType("text/json;charset=utf-8");`

`SelectAllServlet` 代码如下：

```java
@WebServlet("/selectAllServlet")
public class SelectAllServlet extends HttpServlet {
    private BrandService brandService = new BrandService();

    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //1. 调用Service查询
        List<Brand> brands = brandService.selectAll();

        //2. 将集合转换为JSON数据   序列化
        String jsonString = JSON.toJSONString(brands);

        //3. 响应数据  application/json   text/json
        response.setContentType("text/json;charset=utf-8");
        response.getWriter().write(jsonString);
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doGet(request, response);
    }
}
```



#### 6.2.3  前端实现

1. **引入 js 文件**

在 `brand.html` 页面引入 `axios` 的 js 文件

```html
<script src="js/axios-0.18.0.js"></script>
```

2. **绑定 `页面加载完毕` 事件**

在 `brand.html` 页面绑定加载完毕事件，该事件是在页面加载完毕后被触发，代码如下

```js
window.onload = function() {
	
}
```

3. **发送异步请求**

在页面加载完毕事件绑定的匿名函数中发送异步请求，代码如下：

```js
 //2. 发送ajax请求
axios({
    method:"get",
    url:"http://localhost:8080/brand-demo/selectAllServlet"
}).then(function (resp) {

});
```

4. **处理响应数据**

在 `then` 中的回调函数中通过 `resp.data` 可以获取响应回来的数据，而数据格式如下

<img src="D:/download/downloadFromMicsoft/day12-Filter&Listener&Ajax（补充资料）/day12-Filter&Listener&Ajax/assets/image-20210831093617083.png" alt="image-20210831093617083" style="zoom:80%;" />

现在需要拼接字符串，将下面表格中的所有的 `tr` 拼接到一个字符串中，然后使用 `document.getElementById("brandTable").innerHTML = 拼接好的字符串`  就可以动态的展示出用户想看到的数据

<img src="D:/download/downloadFromMicsoft/day12-Filter&Listener&Ajax（补充资料）/day12-Filter&Listener&Ajax/assets/image-20210831093938057.png" alt="image-20210831093938057" style="zoom:70%;" />

而表头行是固定的，所以先定义初始值是表头行数据的字符串，如下

```js
//获取数据
let brands = resp.data;
let tableData = " <tr>\n" +
    "        <th>序号</th>\n" +
    "        <th>品牌名称</th>\n" +
    "        <th>企业名称</th>\n" +
    "        <th>排序</th>\n" +
    "        <th>品牌介绍</th>\n" +
    "        <th>状态</th>\n" +
    "        <th>操作</th>\n" +
    "    </tr>";
```

接下来遍历响应回来的数据 `brands` ，拿到每一条品牌数据

```js
for (let i = 0; i < brands.length ; i++) {
    let brand = brands[i];
	
}
```

紧接着就是从 `brand` 对象中获取数据并且拼接 `数据行`，累加到 `tableData` 字符串变量中

```js
tableData += "\n" +
    "    <tr align=\"center\">\n" +
    "        <td>"+(i+1)+"</td>\n" +
    "        <td>"+brand.brandName+"</td>\n" +
    "        <td>"+brand.companyName+"</td>\n" +
    "        <td>"+brand.ordered+"</td>\n" +
    "        <td>"+brand.description+"</td>\n" +
    "        <td>"+brand.status+"</td>\n" +
    "\n" +
    "        <td><a href=\"#\">修改</a> <a href=\"#\">删除</a></td>\n" +
    "    </tr>";
```

最后再将拼接好的字符串写到表格中

```js
// 设置表格数据
document.getElementById("brandTable").innerHTML = tableData;
```

**整体页面代码如下：**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<a href="addBrand.html"><input type="button" value="新增"></a><br>
<hr>
<table id="brandTable" border="1" cellspacing="0" width="100%">
   
</table>

<script src="js/axios-0.18.0.js"></script>

<script>
    //1. 当页面加载完成后，发送ajax请求
    window.onload = function () {
        //2. 发送ajax请求
        axios({
            method:"get",
            url:"http://localhost:8080/brand-demo/selectAllServlet"
        }).then(function (resp) {
            //获取数据
            let brands = resp.data;
            let tableData = " <tr>\n" +
                "        <th>序号</th>\n" +
                "        <th>品牌名称</th>\n" +
                "        <th>企业名称</th>\n" +
                "        <th>排序</th>\n" +
                "        <th>品牌介绍</th>\n" +
                "        <th>状态</th>\n" +
                "        <th>操作</th>\n" +
                "    </tr>";

            for (let i = 0; i < brands.length ; i++) {
                let brand = brands[i];

                tableData += "\n" +
                    "    <tr align=\"center\">\n" +
                    "        <td>"+(i+1)+"</td>\n" +
                    "        <td>"+brand.brandName+"</td>\n" +
                    "        <td>"+brand.companyName+"</td>\n" +
                    "        <td>"+brand.ordered+"</td>\n" +
                    "        <td>"+brand.description+"</td>\n" +
                    "        <td>"+brand.status+"</td>\n" +
                    "\n" +
                    "        <td><a href=\"#\">修改</a> <a href=\"#\">删除</a></td>\n" +
                    "    </tr>";
            }
            // 设置表格数据
            document.getElementById("brandTable").innerHTML = tableData;
        })
    }
</script>
</body>
</html>
```

### 6.3  添加品牌功能

![image-20210831100117014](D:/download/downloadFromMicsoft/day12-Filter&Listener&Ajax（补充资料）/day12-Filter&Listener&Ajax/assets/image-20210831100117014.png)

如上所示，当点击 `新增` 按钮，会跳转到 `addBrand.html` 页面。在 `addBrand.html` 页面输入数据后点击 `提交` 按钮，就会将数据提交到后端，而后端将数据保存到数据库中。

具体的前后端交互的流程如下：

![image-20210831100329698](D:/download/downloadFromMicsoft/day12-Filter&Listener&Ajax（补充资料）/day12-Filter&Listener&Ajax/assets/image-20210831100329698.png)

==说明：==

前端需要将用户输入的数据提交到后端，这部分数据需要以 json 格式进行提交，数据格式如下：

![image-20210831101234467](D:/download/downloadFromMicsoft/day12-Filter&Listener&Ajax（补充资料）/day12-Filter&Listener&Ajax/assets/image-20210831101234467.png)

#### 6.3.1  后端实现

在 `com.itheima.web` 包下创建名为 `AddServlet` 的 `servlet`，具体的逻辑如下：

* 获取请求参数

  由于前端提交的是 json 格式的数据，所以不能使用 `request.getParameter()` 方法获取请求参数

  * 如果提交的数据格式是 `username=zhangsan&age=23` ，后端就可以使用 `request.getParameter()` 方法获取
  * 如果提交的数据格式是 json，后端就需要通过 request 对象获取输入流，再通过输入流读取数据 

* 将获取到的请求参数（json格式的数据）转换为 `Brand` 对象

* 调用 service 的 `add()` 方法进行添加数据的逻辑处理

* 将 json 数据响应回给浏览器。

`AddServlet` 代码如下：

```java
@WebServlet("/addServlet")
public class AddServlet extends HttpServlet {

    private BrandService brandService = new BrandService();

    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

        //1. 接收数据,request.getParameter 不能接收json的数据
       /* String brandName = request.getParameter("brandName");
        System.out.println(brandName);*/

        // 获取请求体数据
        BufferedReader br = request.getReader();
        String params = br.readLine();
        // 将JSON字符串转为Java对象
        Brand brand = JSON.parseObject(params, Brand.class);
        //2. 调用service 添加
        brandService.add(brand);
        //3. 响应成功标识
        response.getWriter().write("success");
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doGet(request, response);
    }
}
```

#### 6.3.2  前端实现

在 `addBrand.html` 页面给 `提交` 按钮绑定点击事件，并在绑定的匿名函数中发送异步请求，代码如下：

```js
//1. 给按钮绑定单击事件
document.getElementById("btn").onclick = function () {
    //2. 发送ajax请求
    axios({
        method:"post",
        url:"http://localhost:8080/brand-demo/addServlet",
        data:???
    }).then(function (resp) {
        // 判断响应数据是否为 success
        if(resp.data == "success"){
            location.href = "http://localhost:8080/brand-demo/brand.html";
        }
    })
}
```

现在只需要考虑如何获取页面上用户输入的数据即可。

首先先定义如下的一个 js 对象，该对象是用来封装页面上输入的数据，并将该对象作为上面发送异步请求时 `data` 属性的值。

```js
// 将表单数据转为json
var formData = {
    brandName:"",
    companyName:"",
    ordered:"",
    description:"",
    status:"",
};
```

接下来获取输入框输入的数据，并将获取到的数据赋值给 `formData` 对象指定的属性。比如获取用户名的输入框数据，并把该数据赋值给 `formData` 对象的 `brandName` 属性

```js
// 获取表单数据
let brandName = document.getElementById("brandName").value;
// 设置数据
formData.brandName = brandName;
```

==说明：其他的输入框都用同样的方式获取并赋值。==但是有一个比较特殊，就是状态数据，如下图是页面内容

<img src="D:/download/downloadFromMicsoft/day12-Filter&Listener&Ajax（补充资料）/day12-Filter&Listener&Ajax/assets/image-20210831103843798.png" alt="image-20210831103843798" style="zoom:80%;" />

需要判断哪儿个被选中，再将选中的单选框数据赋值给 `formData` 对象的 `status` 属性，代码实现如下：

```js
let status = document.getElementsByName("status");
for (let i = 0; i < status.length; i++) {
    if(status[i].checked){
        //
        formData.status = status[i].value ;
    }
}
```

**整体页面代码如下：**

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <title>添加品牌</title>
</head>
<body>
<h3>添加品牌</h3>
<form action="" method="post">
    品牌名称：<input id="brandName" name="brandName"><br>
    企业名称：<input id="companyName" name="companyName"><br>
    排序：<input id="ordered" name="ordered"><br>
    描述信息：<textarea rows="5" cols="20" id="description" name="description"></textarea><br>
    状态：
    <input type="radio" name="status" value="0">禁用
    <input type="radio" name="status" value="1">启用<br>

    <input type="button" id="btn"  value="提交">
</form>

<script src="js/axios-0.18.0.js"></script>

<script>
    //1. 给按钮绑定单击事件
    document.getElementById("btn").onclick = function () {
        // 将表单数据转为json
        var formData = {
            brandName:"",
            companyName:"",
            ordered:"",
            description:"",
            status:"",
        };
        // 获取表单数据
        let brandName = document.getElementById("brandName").value;
        // 设置数据
        formData.brandName = brandName;

        // 获取表单数据
        let companyName = document.getElementById("companyName").value;
        // 设置数据
        formData.companyName = companyName;

        // 获取表单数据
        let ordered = document.getElementById("ordered").value;
        // 设置数据
        formData.ordered = ordered;

        // 获取表单数据
        let description = document.getElementById("description").value;
        // 设置数据
        formData.description = description;

        let status = document.getElementsByName("status");
        for (let i = 0; i < status.length; i++) {
            if(status[i].checked){
                //
                formData.status = status[i].value ;
            }
        }
        //console.log(formData);
        //2. 发送ajax请求
        axios({
            method:"post",
            url:"http://localhost:8080/brand-demo/addServlet",
            data:formData
        }).then(function (resp) {
            // 判断响应数据是否为 success
            if(resp.data == "success"){
                location.href = "http://localhost:8080/brand-demo/brand.html";
            }
        })
    }
</script>
</body>
</html>
```

==说明：==

`查询所有` 功能和 `添加品牌` 功能就全部实现，大家肯定会感觉前端的代码很复杂；而这只是暂时的，后面学习了 `vue` 前端框架后，这部分前端代码就可以进行很大程度的简化。



# VUE&Element

**今日目标：**

> * 能够使用VUE中常用指令和插值表达式
> * 能够使用VUE生命周期函数 mounted
> * 能够进行简单的 Element 页面修改
> * 能够完成查询所有功能
> * 能够完成添加功能

## 1，VUE

### 1.1  概述

接下来学习一款前端的框架，就是 VUE。

==Vue 是一套前端框架，免除原生JavaScript中的DOM操作，简化书写。==

之前也学习过后端的框架 `Mybatis` ，`Mybatis` 是用来简化 `jdbc` 代码编写的；而 `VUE` 是前端的框架，是用来简化 `JavaScript` 代码编写的。前一天做了一个综合性的案例，里面进行了大量的DOM操作，如下

<img src="D:/download/downloadFromMicsoft/day13-Vue&Element/01-Vue&ElementUI/ppt/assets/image-20210831112115508.png" alt="image-20210831112115508" style="zoom:70%;" />

学习了 `VUE` 后，这部分代码就不需要再写了。那么 `VUE` 是如何简化 DOM 书写呢？

==基于MVVM(Model-View-ViewModel)思想，实现数据的双向绑定，将编程的关注点放在数据上。==之前是将关注点放在了 DOM 操作上；而要了解 `MVVM` 思想，必须先聊聊 `MVC` 思想，如下图就是 `MVC` 思想图解

<img src="D:/download/downloadFromMicsoft/day13-Vue&Element/01-Vue&ElementUI/ppt/assets/image-20210831113940588.png" alt="image-20210831113940588" style="zoom:70%;" />

C 就是咱们 js 代码，M 就是数据，而 V 是页面上展示的内容，如下图是之前写的代码

<img src="D:/download/downloadFromMicsoft/day13-Vue&Element/01-Vue&ElementUI/ppt/assets/image-20210831114227585.png" alt="image-20210831114227585" style="zoom:70%;" />

`MVC` 思想是没法进行双向绑定的。双向绑定是指当数据模型数据发生变化时，页面展示的会随之发生变化，而如果表单数据发生变化，绑定的模型数据也随之发生变化。接下来聊聊 `MVVM` 思想，如下图是三个组件图解

<img src="D:/download/downloadFromMicsoft/day13-Vue&Element/01-Vue&ElementUI/ppt/assets/image-20210831114805052.png" alt="image-20210831114805052" style="zoom:80%;" />

图中的 `Model` 就是的数据，`View` 是视图，也就是页面标签，用户可以通过浏览器看到的内容；`Model` 和 `View` 是通过 `ViewModel` 对象进行双向绑定的，而 `ViewModel` 对象是 `Vue` 提供的。接下来让大家看一下双向绑定的效果，下图是提前准备的代码，输入框绑定了 `username` 模型数据，而在页面上也使用 `{{}}` 绑定了 `username` 模型数据

<img src="D:/download/downloadFromMicsoft/day13-Vue&Element/01-Vue&ElementUI/ppt/assets/image-20210831115645528.png" alt="image-20210831115645528" style="zoom:70%;" />

通过浏览器打开该页面可以看到如下页面

<img src="D:/download/downloadFromMicsoft/day13-Vue&Element/01-Vue&ElementUI/ppt/assets/image-20210831115902537.png" alt="image-20210831115902537" style="zoom:80%;" />

当在输入框中输入内容，而输入框后面随之实时的展示输入的内容，这就是双向绑定的效果。

### 1.2  快速入门

Vue 使用起来是比较简单的，总共分为如下三步：

1. **新建 HTML 页面，引入 Vue.js文件**

   ```html
   <script src="js/vue.js"></script>
   ```

2. **在JS代码区域，创建Vue核心对象，进行数据绑定**

   ```js
   new Vue({
       el: "#app",
       data() {
           return {
               username: ""
           }
       }
   });
   ```

   创建 Vue 对象时，需要传递一个 js 对象，而该对象中需要如下属性：

   * `el` ： 用来指定哪儿些标签受 Vue 管理。 该属性取值 `#app` 中的 `app` 需要是受管理的标签的id属性值
   * `data` ：用来定义数据模型
   * `methods` ：用来定义函数。这个在后面就会用到

3. **编写视图**

   ```html
   <div id="app">
       <input name="username" v-model="username" >
       {{username}}
   </div>
   ```

   `{{}}` 是 Vue 中定义的 `插值表达式` ，在里面写数据模型，到时候会将该模型的数据值展示在这个位置。

**整体代码如下：**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<div id="app">
    <input v-model="username">
    <!--插值表达式-->
    {{username}}
</div>
<script src="js/vue.js"></script>
<script>
    //1. 创建Vue核心对象
    new Vue({
        el:"#app",
        data(){  // data() 是 ECMAScript 6 版本的新的写法
            return {
                username:""
            }
        }

        /*data: function () {
            return {
                username:""
            }
        }*/
    });

</script>
</body>
</html>
```

### 1.3  Vue 指令

**指令：**HTML 标签上带有 v- 前缀的特殊属性，不同指令具有不同含义。例如：v-if，v-for…

常用的指令有：

| **指令**  | **作用**                                            |
| --------- | --------------------------------------------------- |
| v-bind    | 为HTML标签绑定属性值，如设置  href , css样式等      |
| v-model   | 在表单元素上创建双向数据绑定                        |
| v-on      | 为HTML标签绑定事件                                  |
| v-if      | 条件性的渲染某元素，判定为true时渲染,否则不渲染     |
| v-else    |                                                     |
| v-else-if |                                                     |
| v-show    | 根据条件展示某元素，区别在于切换的是display属性的值 |
| v-for     | 列表渲染，遍历容器的元素或者对象的属性              |

接下来挨个学习这些指令

#### 1.3.1  v-bind & v-model 指令

<img src="D:/download/downloadFromMicsoft/day13-Vue&Element/01-Vue&ElementUI/ppt/assets/image-20210831150101736.png" alt="image-20210831150101736" style="zoom:70%;" />

* **v-bind**

  该指令可以给标签原有属性绑定模型数据。这样模型数据发生变化，标签属性值也随之发生变化

  例如：

  ```html
  <a v-bind:href="url">百度一下</a>
  ```

  上面的 `v-bind:"`  可以简化写成 `:`  ，如下：

  ```html
  <!--
  	v-bind 可以省略
  -->
  <a :href="url">百度一下</a>
  ```

* **v-model**

  该指令可以给表单项标签绑定模型数据。这样就能实现双向绑定效果。例如：

  ```html
  <input name="username" v-model="username">
  ```

**代码演示：**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<div id="app">
    <a v-bind:href="url">点击一下</a>
    <a :href="url">点击一下</a>
    <input v-model="url">
</div>

<script src="js/vue.js"></script>
<script>
    //1. 创建Vue核心对象
    new Vue({
        el:"#app",
        data(){
            return {
                username:"",
                url:"https://www.baidu.com"
            }
        }
    });
</script>
</body>
</html>
```

通过浏览器打开上面页面，并且使用检查查看超链接的路径，该路径会根据输入框输入的路径变化而变化，这是因为超链接和输入框绑定的是同一个模型数据

<img src="D:/download/downloadFromMicsoft/day13-Vue&Element/01-Vue&ElementUI/ppt/assets/image-20210831150945931.png" alt="image-20210831150945931" style="zoom:80%;" />

#### 1.3.2  v-on 指令

<img src="D:/download/downloadFromMicsoft/day13-Vue&Element/01-Vue&ElementUI/ppt/assets/image-20210831151231955.png" alt="image-20210831151231955" style="zoom:70%;" />

在页面定义一个按钮，并给该按钮使用 `v-on` 指令绑定单击事件，html代码如下

```html
<input type="button" value="一个按钮" v-on:click="show()">
```

而使用 `v-on` 时还可以使用简化的写法，将 `v-on:` 替换成 `@`，html代码如下

```html
<input type="button" value="一个按钮" @click="show()">
```

上面代码绑定的 `show()` 需要在 Vue 对象中的 `methods` 属性中定义出来

```js
new Vue({
    el: "#app",
    methods: {
        show(){
            alert("我被点了");
        }
    }
});
```

> ==注意：`v-on:` 后面的事件名称是之前原生事件属性名去掉on。==
>
> 例如：
>
> * 单击事件 ： 事件属性名是 onclick，而在vue中使用是 `v-on:click`
> * 失去焦点事件：事件属性名是 onblur，而在vue中使用时 `v-on:blur`

**整体页面代码如下：**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<div id="app">
    <input type="button" value="一个按钮" v-on:click="show()"><br>
    <input type="button" value="一个按钮" @click="show()">
</div>
<script src="js/vue.js"></script>
<script>
    //1. 创建Vue核心对象
    new Vue({
        el:"#app",
        data(){
            return {
                username:"",
            }
        },
        methods:{
            show(){
                alert("我被点了...");
            }
        }
    });
</script>
</body>
</html>
```

#### 1.3.3  条件判断指令

<img src="D:/download/downloadFromMicsoft/day13-Vue&Element/01-Vue&ElementUI/ppt/assets/image-20210831151904081.png" alt="image-20210831151904081" style="zoom:70%;" />

接下来通过代码演示一下。在 Vue中定义一个 `count` 的数据模型，如下

```js
//1. 创建Vue核心对象
new Vue({
    el:"#app",
    data(){
        return {
            count:3
        }
    }
});
```

现在要实现，当 `count` 模型的数据是3时，在页面上展示 `div1` 内容；当 `count` 模型的数据是4时，在页面上展示 `div2` 内容；`count` 模型数据是其他值时，在页面上展示 `div3`。这里为了动态改变模型数据 `count` 的值，再定义一个输入框绑定 `count` 模型数据。html 代码如下：

```html
<div id="app">
    <div v-if="count == 3">div1</div>
    <div v-else-if="count == 4">div2</div>
    <div v-else>div3</div>
    <hr>
    <input v-model="count">
</div>
```

**整体页面代码如下：**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<div id="app">
    <div v-if="count == 3">div1</div>
    <div v-else-if="count == 4">div2</div>
    <div v-else>div3</div>
    <hr>
    <input v-model="count">
</div>

<script src="js/vue.js"></script>
<script>
    //1. 创建Vue核心对象
    new Vue({
        el:"#app",
        data(){
            return {
                count:3
            }
        }
    });
</script>
</body>
</html>
```

通过浏览器打开页面并在输入框输入不同的值，效果如下

<img src="D:/download/downloadFromMicsoft/day13-Vue&Element/01-Vue&ElementUI/ppt/assets/image-20210831154300325.png" alt="image-20210831154300325" style="zoom:80%;" />

然后在看看 `v-show` 指令的效果，如果模型数据 `count ` 的值是3时，展示 `div v-show` 内容，否则不展示，html页面代码如下

```html
<div v-show="count == 3">div v-show</div>
<br>
<input v-model="count">
```

浏览器打开效果如下：

<img src="D:/download/downloadFromMicsoft/day13-Vue&Element/01-Vue&ElementUI/ppt/assets/image-20210831154547780.png" alt="image-20210831154547780" style="zoom:80%;" />

通过上面的演示，发现 `v-show` 和 `v-if` 效果一样，那它们到底有什么区别呢？根据浏览器的检查功能查看源代码

<img src="D:/download/downloadFromMicsoft/day13-Vue&Element/01-Vue&ElementUI/ppt/assets/image-20210831154759672.png" alt="image-20210831154759672" style="zoom:80%;" />

通过上图可以看出 `v-show` 不展示的原理是给对应的标签添加 `display` css属性，并将该属性值设置为 `none` ，这样就达到了隐藏的效果。而 `v-if` 指令是条件不满足时根本就不会渲染。

#### 1.3.4  v-for 指令

<img src="D:/download/downloadFromMicsoft/day13-Vue&Element/01-Vue&ElementUI/ppt/assets/image-20210831155204829.png" alt="image-20210831155204829" style="zoom:80%;" />

这个指令看到名字就知道是用来遍历的，该指令使用的格式如下：

```html
<标签 v-for="变量名 in 集合模型数据">
    {{变量名}}
</标签>
```

> ==注意：需要循环那个标签，`v-for` 指令就写在那个标签上。==

如果在页面需要使用到集合模型数据的索引，就需要使用如下格式：

```html
<标签 v-for="(变量名,索引变量) in 集合模型数据">
    <!--索引变量是从0开始，所以要表示序号的话，需要手动的加1-->
   {{索引变量 + 1}} {{变量名}}
</标签>
```

**代码演示：**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<div id="app">
    <div v-for="addr in addrs">
        {{addr}} <br>
    </div>

    <hr>
    <div v-for="(addr,i) in addrs">
        {{i+1}}--{{addr}} <br>
    </div>
</div>

<script src="js/vue.js"></script>
<script>

    //1. 创建Vue核心对象
    new Vue({
        el:"#app",
        data(){
            return {
                addrs:["北京","上海","西安"]
            }
        }
    });
</script>
</body>
</html>
```

通过浏览器打开效果如下

<img src="D:/download/downloadFromMicsoft/day13-Vue&Element/01-Vue&ElementUI/ppt/assets/image-20210831155837801.png" alt="image-20210831155837801" style="zoom:80%;" />

### 1.4  生命周期 

生命周期的八个阶段：每触发一个生命周期事件，会自动执行一个生命周期方法，这些生命周期方法也被称为钩子方法。

<img src="D:/download/downloadFromMicsoft/day13-Vue&Element/01-Vue&ElementUI/ppt/assets/image-20210831160239294.png" alt="image-20210831160239294" style="zoom:80%;" />

下图是 Vue 官网提供的从创建 Vue 到效果 Vue 对象的整个过程及各个阶段对应的钩子函数

<img src="D:/download/downloadFromMicsoft/day13-Vue&Element/01-Vue&ElementUI/ppt/assets/image-20210831160335496.png" alt="image-20210831160335496" style="zoom:80%;" />

看到上面的图，大家无需过多的关注这张图。这些钩子方法只关注 `mounted` 就行了。

`mounted`：挂载完成，Vue初始化成功，HTML页面渲染成功。而以后会在该方法中==发送异步请求，加载数据。==

### 1.5  案例

#### 1.5.1  需求

使用 Vue 简化在前一天ajax学完后做的品牌列表数据查询和添加功能

<img src="D:/download/downloadFromMicsoft/day13-Vue&Element/01-Vue&ElementUI/ppt/assets/image-20210831161040800.png" alt="image-20210831161040800" style="zoom:80%;" />

此案例只是使用 Vue 对前端代码进行优化，后端代码无需修改。

#### 1.5.2  查询所有功能

<img src="D:/download/downloadFromMicsoft/day13-Vue&Element/01-Vue&ElementUI/ppt/assets/image-20210831161346678.png" alt="image-20210831161346678" style="zoom:80%;" />

1. **在 brand.html 页面引入 vue 的js文件**

   ```html
   <script src="js/vue.js"></script>
   ```

2. **创建 Vue 对象**

   * 在 Vue 对象中定义模型数据
   * 在钩子函数中发送异步请求，并将响应的数据赋值给数据模型

   ```js
   new Vue({
       el: "#app",
       data(){
           return{
               brands:[]
           }
       },
       mounted(){
           // 页面加载完成后，发送异步请求，查询数据
           var _this = this;
           axios({
               method:"get",
               url:"http://localhost:8080/brand-demo/selectAllServlet"
           }).then(function (resp) {
               _this.brands = resp.data;
           })
       }
   })
   ```

3. **修改视图**

   * 定义 `<div id="app"></div>` ，指定该 `div` 标签受 Vue 管理

   * 将 `body` 标签中所有的内容拷贝作为上面 `div` 标签中

   * 删除表格的多余数据行，只留下一个

   * 在表格中的数据行上使用 `v-for` 指令遍历

     ```html
     <tr v-for="(brand,i) in brands" align="center">
         <td>{{i + 1}}</td>
         <td>{{brand.brandName}}</td>
         <td>{{brand.companyName}}</td>
         <td>{{brand.ordered}}</td>
         <td>{{brand.description}}</td>
         <td>{{brand.statusStr}}</td>
         <td><a href="#">修改</a> <a href="#">删除</a></td>
     </tr>
     ```

**整体页面代码如下：**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<div id="app">
    <a href="addBrand.html"><input type="button" value="新增"></a><br>
    <hr>
    <table id="brandTable" border="1" cellspacing="0" width="100%">
        <tr>
            <th>序号</th>
            <th>品牌名称</th>
            <th>企业名称</th>
            <th>排序</th>
            <th>品牌介绍</th>
            <th>状态</th>
            <th>操作</th>
        </tr>
        <!--
            使用v-for遍历tr
        -->
        <tr v-for="(brand,i) in brands" align="center">
            <td>{{i + 1}}</td>
            <td>{{brand.brandName}}</td>
            <td>{{brand.companyName}}</td>
            <td>{{brand.ordered}}</td>
            <td>{{brand.description}}</td>
            <td>{{brand.statusStr}}</td>
            <td><a href="#">修改</a> <a href="#">删除</a></td>
        </tr>
    </table>
</div>
<script src="js/axios-0.18.0.js"></script>
<script src="js/vue.js"></script>

<script>
    new Vue({
        el: "#app",
        data(){
            return{
                brands:[]
            }
        },
        mounted(){
            // 页面加载完成后，发送异步请求，查询数据
            var _this = this;
            axios({
                method:"get",
                url:"http://localhost:8080/brand-demo/selectAllServlet"
            }).then(function (resp) {
                _this.brands = resp.data;
            })
        }
    })
</script>
</body>
</html>
```

#### 1.5.3  添加功能

页面操作效果如下：

<img src="D:/download/downloadFromMicsoft/day13-Vue&Element/01-Vue&ElementUI/ppt/assets/image-20210831163001830.png" alt="image-20210831163001830" style="zoom:80%;" />

整体流程如下

<img src="D:/download/downloadFromMicsoft/day13-Vue&Element/01-Vue&ElementUI/ppt/assets/image-20210831163035298.png" alt="image-20210831163035298" style="zoom:70%;" />

> ==注意：前端代码的关键点在于使用 `v-model` 指令给标签项绑定模型数据，利用双向绑定特性，在发送异步请求时提交数据。==

1. **在 addBrand.html 页面引入 vue 的js文件**

   ```html
   <script src="js/vue.js"></script>
   ```

2. **创建 Vue 对象**

   * 在 Vue 对象中定义模型数据 `brand` 
   * 定义一个 `submitForm()` 函数，用于给 `提交` 按钮提供绑定的函数
   * 在 `submitForm()` 函数中发送 ajax 请求，并将模型数据 `brand` 作为参数进行传递

   ```js
   new Vue({
       el: "#app",
       data(){
           return {
               brand:{}
           }
       },
       methods:{
           submitForm(){
               // 发送ajax请求，添加
               var _this = this;
               axios({
                   method:"post",
                   url:"http://localhost:8080/brand-demo/addServlet",
                   data:_this.brand
               }).then(function (resp) {
                   // 判断响应数据是否为 success
                   if(resp.data == "success"){
                       location.href = "http://localhost:8080/brand-demo/brand.html";
                   }
               })
   
           }
       }
   })
   ```

3. **修改视图**

   * 定义 `<div id="app"></div>` ，指定该 `div` 标签受 Vue 管理

   * 将 `body` 标签中所有的内容拷贝作为上面 `div` 标签中

   * 给每一个表单项标签绑定模型数据。最后这些数据要被封装到 `brand` 对象中

     ```html
     <div id="app">
         <h3>添加品牌</h3>
         <form action="" method="post">
             品牌名称：<input id="brandName" v-model="brand.brandName" name="brandName"><br>
             企业名称：<input id="companyName" v-model="brand.companyName" name="companyName"><br>
             排序：<input id="ordered" v-model="brand.ordered" name="ordered"><br>
             描述信息：<textarea rows="5" cols="20" id="description" v-model="brand.description" name="description"></textarea><br>
             状态：
             <input type="radio" name="status" v-model="brand.status" value="0">禁用
             <input type="radio" name="status" v-model="brand.status" value="1">启用<br>
     
             <input type="button" id="btn" @click="submitForm" value="提交">
         </form>
     </div>
     ```

**整体页面代码如下：**

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <title>添加品牌</title>
</head>
<body>
<div id="app">
    <h3>添加品牌</h3>
    <form action="" method="post">
        品牌名称：<input id="brandName" v-model="brand.brandName" name="brandName"><br>
        企业名称：<input id="companyName" v-model="brand.companyName" name="companyName"><br>
        排序：<input id="ordered" v-model="brand.ordered" name="ordered"><br>
        描述信息：<textarea rows="5" cols="20" id="description" v-model="brand.description" name="description"></textarea><br>
        状态：
        <input type="radio" name="status" v-model="brand.status" value="0">禁用
        <input type="radio" name="status" v-model="brand.status" value="1">启用<br>

        <input type="button" id="btn" @click="submitForm" value="提交">
    </form>
</div>
<script src="js/axios-0.18.0.js"></script>
<script src="js/vue.js"></script>
<script>
    new Vue({
        el: "#app",
        data(){
            return {
                brand:{}
            }
        },
        methods:{
            submitForm(){
                // 发送ajax请求，添加
                var _this = this;
                axios({
                    method:"post",
                    url:"http://localhost:8080/brand-demo/addServlet",
                    data:_this.brand
                }).then(function (resp) {
                    // 判断响应数据是否为 success
                    if(resp.data == "success"){
                        location.href = "http://localhost:8080/brand-demo/brand.html";
                    }
                })
            }
        }
    })
</script>
</body>
</html>
```

通过上面的优化，前端代码确实简化了不少。但是页面依旧是不怎么好看，那么接下来学习 Element，它可以美化页面。

## 2，Element

Element：是饿了么公司前端开发团队提供的一套基于 Vue 的网站组件库，用于快速构建网页。

Element 提供了很多组件（组成网页的部件）供使用。例如 超链接、按钮、图片、表格等等~

如下图左边的是编写页面看到的按钮，上图右边的是 Element 提供的页面效果，效果一目了然。

<img src="D:/download/downloadFromMicsoft/day13-Vue&Element/01-Vue&ElementUI/ppt/assets/image-20210831170943892.png" alt="image-20210831170943892" style="zoom:80%;" />

学习 Element 其实就是学习怎么从官网拷贝组件到自己的页面并进行修改，官网网址是

```
https://element.eleme.cn/#/zh-CN
```

进入官网能看到如下页面

![image-20210831171456559](D:/download/downloadFromMicsoft/day13-Vue&Element/01-Vue&ElementUI/ppt/assets/image-20210831171456559.png)

接下来直接点击 `组件` ，页面如下

![image-20210831171552844](D:/download/downloadFromMicsoft/day13-Vue&Element/01-Vue&ElementUI/ppt/assets/image-20210831171552844.png)

### 2.1  快速入门

1. 将资源 `04-资料\02-element` 下的 `element-ui` 文件夹直接拷贝到项目的 `webapp` 下。目录结构如下

   <img src="D:/download/downloadFromMicsoft/day13-Vue&Element/01-Vue&ElementUI/ppt/assets/image-20210831171856768.png" alt="image-20210831171856768" style="zoom:80%;" />

2. 创建页面，并在页面引入Element 的css、js文件 和 Vue.js

   ```html
   <script src="vue.js"></script>
   <script src="element-ui/lib/index.js"></script>
   <link rel="stylesheet" href="element-ui/lib/theme-chalk/index.css">
   ```

3. .创建Vue核心对象

   Element 是基于 Vue 的，所以使用Element时必须要创建 Vue 对象

   ```html
   <script>
       new Vue({
           el:"#app"
       })
   </script>
   ```

4. 官网复制Element组件代码

   <img src="D:/download/downloadFromMicsoft/day13-Vue&Element/01-Vue&ElementUI/ppt/assets/image-20210831180730287.png" alt="image-20210831180730287" style="zoom:70%;" />

   在左菜单栏找到 `Button 按钮` ，然后找到自己喜欢的按钮样式，点击 `显示代码` ，在下面就会展示出对应的代码，将这些代码拷贝到自己的页面即可。

**整体页面代码如下：**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<div id="app">


    <el-row>
     	<el-button>默认按钮</el-button>
        <el-button type="primary">主要按钮</el-button>
        <el-button type="success">成功按钮</el-button>
        <el-button type="info">信息按钮</el-button>
        <el-button type="warning">警告按钮</el-button>
        <el-button type="danger">删除</el-button>
    </el-row>
    <el-row>
        <el-button plain>朴素按钮</el-button>
        <el-button type="primary" plain>主要按钮</el-button>
        <el-button type="success" plain>成功按钮</el-button>
        <el-button type="info" plain>信息按钮</el-button>
        <el-button type="warning" plain>警告按钮</el-button>
        <el-button type="danger" plain>危险按钮</el-button>
    </el-row>

    <el-row>
        <el-button round>圆角按钮</el-button>
        <el-button type="primary" round>主要按钮</el-button>
        <el-button type="success" round>成功按钮</el-button>
        <el-button type="info" round>信息按钮</el-button>
        <el-button type="warning" round>警告按钮</el-button>
        <el-button type="danger" round>危险按钮</el-button>
    </el-row>

    <el-row>
        <el-button icon="el-icon-search" circle></el-button>
        <el-button type="primary" icon="el-icon-edit" circle></el-button>
        <el-button type="success" icon="el-icon-check" circle></el-button>
        <el-button type="info" icon="el-icon-message" circle></el-button>
        <el-button type="warning" icon="el-icon-star-off" circle></el-button>
        <el-button type="danger" icon="el-icon-delete" circle></el-button>
    </el-row>
</div>

<script src="js/vue.js"></script>
<script src="element-ui/lib/index.js"></script>
<link rel="stylesheet" href="element-ui/lib/theme-chalk/index.css">

<script>
    new Vue({
        el:"#app"
    })
</script>

</body>
</html>
```

### 2.2  Element 布局

Element 提供了两种布局方式，分别是：

* Layout 布局
* Container 布局容器

#### 2.2.1  Layout 局部

通过基础的 24 分栏，迅速简便地创建布局。也就是默认将一行分为 24 栏，根据页面要求给每一列设置所占的栏数。

<img src="D:/download/downloadFromMicsoft/day13-Vue&Element/01-Vue&ElementUI/ppt/assets/image-20210831182349672.png" alt="image-20210831182349672" style="zoom:70%;" />

在左菜单栏找到 `Layout 布局` ，然后找到自己喜欢的按钮样式，点击 `显示代码` ，在下面就会展示出对应的代码，显示出的代码中有样式，有html标签。将样式拷贝自己页面的 `head` 标签内，将html标签拷贝到  `<div id="app"></div>` 标签内。

**整体页面代码如下：**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>

    <style>
        .el-row {
            margin-bottom: 20px;
        }
        .el-col {
            border-radius: 4px;
        }
        .bg-purple-dark {
            background: #99a9bf;
        }
        .bg-purple {
            background: #d3dce6;
        }
        .bg-purple-light {
            background: #e5e9f2;
        }
        .grid-content {
            border-radius: 4px;
            min-height: 36px;
        }
        .row-bg {
            padding: 10px 0;
            background-color: #f9fafc;
        }
    </style>
</head>
<body>
<div id="app">
    <el-row>
        <el-col :span="24"><div class="grid-content bg-purple-dark"></div></el-col>
    </el-row>
    <el-row>
        <el-col :span="12"><div class="grid-content bg-purple"></div></el-col>
        <el-col :span="12"><div class="grid-content bg-purple-light"></div></el-col>
    </el-row>
    <el-row>
        <el-col :span="8"><div class="grid-content bg-purple"></div></el-col>
        <el-col :span="8"><div class="grid-content bg-purple-light"></div></el-col>
        <el-col :span="8"><div class="grid-content bg-purple"></div></el-col>
    </el-row>
    <el-row>
        <el-col :span="6"><div class="grid-content bg-purple"></div></el-col>
        <el-col :span="6"><div class="grid-content bg-purple-light"></div></el-col>
        <el-col :span="6"><div class="grid-content bg-purple"></div></el-col>
        <el-col :span="6"><div class="grid-content bg-purple-light"></div></el-col>
    </el-row>
    <el-row>
        <el-col :span="4"><div class="grid-content bg-purple"></div></el-col>
        <el-col :span="4"><div class="grid-content bg-purple-light"></div></el-col>
        <el-col :span="4"><div class="grid-content bg-purple"></div></el-col>
        <el-col :span="4"><div class="grid-content bg-purple-light"></div></el-col>
        <el-col :span="4"><div class="grid-content bg-purple"></div></el-col>
        <el-col :span="4"><div class="grid-content bg-purple-light"></div></el-col>
    </el-row>
</div>
<script src="js/vue.js"></script>
<script src="element-ui/lib/index.js"></script>
<link rel="stylesheet" href="element-ui/lib/theme-chalk/index.css">

<script>
    new Vue({
        el:"#app"
    })
</script>
</body>
</html>
```

现在需要添加一行，要求该行显示8个格子，通过计算每个格子占 3 栏，具体的html 代码如下

```html
<!--
添加一行，8个格子  24/8 = 3
-->
<el-row>
    <el-col :span="3"><div class="grid-content bg-purple"></div></el-col>
    <el-col :span="3"><div class="grid-content bg-purple-light"></div></el-col>
    <el-col :span="3"><div class="grid-content bg-purple"></div></el-col>
    <el-col :span="3"><div class="grid-content bg-purple-light"></div></el-col>
    <el-col :span="3"><div class="grid-content bg-purple"></div></el-col>
    <el-col :span="3"><div class="grid-content bg-purple-light"></div></el-col>
    <el-col :span="3"><div class="grid-content bg-purple"></div></el-col>
    <el-col :span="3"><div class="grid-content bg-purple-light"></div></el-col>
</el-row>
```

#### 2.2.2  Container 布局容器

用于布局的容器组件，方便快速搭建页面的基本结构。如下图就是布局容器效果。

如下图是官网提供的 Container 布局容器实例：

<img src="D:/download/downloadFromMicsoft/day13-Vue&Element/01-Vue&ElementUI/ppt/assets/image-20210831183433892.png" alt="image-20210831183433892" style="zoom:70%;" />

该效果代码中包含了样式、页面标签、模型数据。将里面的样式 `<style>` 拷贝到自己页面的 `head` 标签中；将html标签拷贝到 `<div id="app"></div>` 标签中，再将数据模型拷贝到 `vue` 对象的 `data()` 中。

**整体页面代码如下：**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>

    <style>
        .el-header {
            background-color: #B3C0D1;
            color: #333;
            line-height: 60px;
        }

        .el-aside {
            color: #333;
        }
    </style>
</head>
<body>
<div id="app">
    <el-container style="height: 500px; border: 1px solid #eee">
        <el-aside width="200px" style="background-color: rgb(238, 241, 246)">
            <el-menu :default-openeds="['1', '3']">
                <el-submenu index="1">
                    <template slot="title"><i class="el-icon-message"></i>导航一</template>
                    <el-menu-item-group>
                        <template slot="title">分组一</template>
                        <el-menu-item index="1-1">选项1</el-menu-item>
                        <el-menu-item index="1-2">选项2</el-menu-item>
                    </el-menu-item-group>
                    <el-menu-item-group title="分组2">
                        <el-menu-item index="1-3">选项3</el-menu-item>
                    </el-menu-item-group>
                    <el-submenu index="1-4">
                        <template slot="title">选项4</template>
                        <el-menu-item index="1-4-1">选项4-1</el-menu-item>
                    </el-submenu>
                </el-submenu>
                <el-submenu index="2">
                    <template slot="title"><i class="el-icon-menu"></i>导航二</template>
                    <el-submenu index="2-1">
                        <template slot="title">选项1</template>
                        <el-menu-item index="2-1-1">选项1-1</el-menu-item>
                    </el-submenu>
                </el-submenu>
                <el-submenu index="3">
                    <template slot="title"><i class="el-icon-setting"></i>导航三</template>
                    <el-menu-item-group>
                        <template slot="title">分组一</template>
                        <el-menu-item index="3-1">选项1</el-menu-item>
                        <el-menu-item index="3-2">选项2</el-menu-item>
                    </el-menu-item-group>
                    <el-menu-item-group title="分组2">
                        <el-menu-item index="3-3">选项3</el-menu-item>
                    </el-menu-item-group>
                    <el-submenu index="3-4">
                        <template slot="title">选项4</template>
                        <el-menu-item index="3-4-1">选项4-1</el-menu-item>
                    </el-submenu>
                </el-submenu>
            </el-menu>
        </el-aside>

        <el-container>
            <el-header style="text-align: right; font-size: 12px">
                <el-dropdown>
                    <i class="el-icon-setting" style="margin-right: 15px"></i>
                    <el-dropdown-menu slot="dropdown">
                        <el-dropdown-item>查看</el-dropdown-item>
                        <el-dropdown-item>新增</el-dropdown-item>
                        <el-dropdown-item>删除</el-dropdown-item>
                    </el-dropdown-menu>
                </el-dropdown>
                <span>王小虎</span>
            </el-header>

            <el-main>
                <el-table :data="tableData">
                    <el-table-column prop="date" label="日期" width="140">
                    </el-table-column>
                    <el-table-column prop="name" label="姓名" width="120">
                    </el-table-column>
                    <el-table-column prop="address" label="地址">
                    </el-table-column>
                </el-table>
            </el-main>
        </el-container>
    </el-container>
</div>
<script src="js/vue.js"></script>
<script src="element-ui/lib/index.js"></script>
<link rel="stylesheet" href="element-ui/lib/theme-chalk/index.css">

<script>
    new Vue({
        el:"#app",
        data() {
            const item = {
                date: '2016-05-02',
                name: '王小虎',
                address: '上海市普陀区金沙江路 1518 弄'
            };
            return {
                tableData: Array(20).fill(item)
            }
        }
    })
</script>
</body>
</html>
```

### 2.3  案例

其他的组件通过完成一个页面来学习。

要完成如下页面效果

<img src="D:/download/downloadFromMicsoft/day13-Vue&Element/01-Vue&ElementUI/ppt/assets/image-20210831185223141.png" alt="image-20210831185223141" style="zoom:80%;" />

要完成该页面，需要先对这个页面进行分析，看页面由哪儿几部分组成，然后到官网进行拷贝并修改。页面总共有如下组成部分

![image-20210831185505106](D:/download/downloadFromMicsoft/day13-Vue&Element/01-Vue&ElementUI/ppt/assets/image-20210831185505106.png)

还有一个是当点击 `新增` 按钮，会在页面正中间弹出一个对话框，如下

<img src="D:/download/downloadFromMicsoft/day13-Vue&Element/01-Vue&ElementUI/ppt/assets/image-20210831185612905.png" alt="image-20210831185612905" style="zoom:60%;" />

#### 2.3.1  准备基本页面

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<div id="app">
	
</div>

<script src="js/vue.js"></script>
<script src="element-ui/lib/index.js"></script>
<link rel="stylesheet" href="element-ui/lib/theme-chalk/index.css">

<script>
    new Vue({
        el: "#app"
    })
</script>
</body>
</html>
```

#### 2.3.2  完成表格展示

使用 Element 整体的思路就是 ==拷贝 + 修改==。

##### 2.3.2.1  拷贝

![image-20210831185937618](D:/download/downloadFromMicsoft/day13-Vue&Element/01-Vue&ElementUI/ppt/assets/image-20210831185937618.png)

在左菜单栏找到 `Table 表格`并点击，右边主体就会定位到表格这一块，找到需要的表格效果（如上图），点击 `显示代码` 就可以看到这个表格的代码了。

将html标签拷贝到 `<div id="app"></div>` 中，如下：

<img src="D:/download/downloadFromMicsoft/day13-Vue&Element/01-Vue&ElementUI/ppt/assets/image-20210831190328825.png" alt="image-20210831190328825" style="zoom:80%;" />

将css样式拷贝到页面的 `head` 标签中，如下

<img src="D:/download/downloadFromMicsoft/day13-Vue&Element/01-Vue&ElementUI/ppt/assets/image-20210831190419248.png" alt="image-20210831190419248" style="zoom:80%;" />

将方法和模型数据拷贝到 Vue 对象指定的位置

<img src="D:/download/downloadFromMicsoft/day13-Vue&Element/01-Vue&ElementUI/ppt/assets/image-20210831190534720.png" alt="image-20210831190534720" style="zoom:80%;" />

拷贝完成后通过浏览器打开可以看到表格的效果

![image-20210831191234876](D:/download/downloadFromMicsoft/day13-Vue&Element/01-Vue&ElementUI/ppt/assets/image-20210831191234876.png)

表格效果出来了，但是显示的表头和数据并不是想要的，所以接下来就需要对页面代码进行修改了。

##### 2.3.2.2  修改

1. **修改表头和数据**

   下面是对表格代码进行分析的图解。根据下图说明修改自己的列数和列名

   <img src="D:/download/downloadFromMicsoft/day13-Vue&Element/01-Vue&ElementUI/ppt/assets/image-20210831192032118.png" alt="image-20210831192032118" style="zoom:70%;" />

   修改完页面后，还需要对绑定的模型数据进行修改，下图是对模型数据进行分析的图解

   <img src="D:/download/downloadFromMicsoft/day13-Vue&Element/01-Vue&ElementUI/ppt/assets/image-20210831192429806.png" alt="image-20210831192429806" style="zoom:70%;" />

2. **给表格添加操作列**

   从之前的表格拷贝一列出来并对其进行修改。按钮是从官网的 `Button 按钮` 组件中拷贝并修改的

   <img src="D:/download/downloadFromMicsoft/day13-Vue&Element/01-Vue&ElementUI/ppt/assets/image-20210831192809304.png" alt="image-20210831192809304" style="zoom:70%;" />

3. **给表格添加复选框列和标号列**

   给表格添加复选框和标号列，效果如下

   ![image-20210831193216143](D:/download/downloadFromMicsoft/day13-Vue&Element/01-Vue&ElementUI/ppt/assets/image-20210831193216143.png)

   此效果也是从 Element 官网进行拷贝，先找到对应的表格效果，然后将其对应代码拷贝到的代码中，如下是复选框列官网效果图和代码

   ![image-20210831193601788](D:/download/downloadFromMicsoft/day13-Vue&Element/01-Vue&ElementUI/ppt/assets/image-20210831193601788.png)

   这里需要注意在 `<el-table>` 标签上有一个事件 `@selection-change="handleSelectionChange"` ，这里绑定的函数也需要从官网拷贝到自己的页面代码中，函数代码如下：

   ![image-20210831194013986](D:/download/downloadFromMicsoft/day13-Vue&Element/01-Vue&ElementUI/ppt/assets/image-20210831194013986.png)

   从该函数中又发现还需要一个模型数据 `multipleSelection ` ，所以还需要定义出该模型数据

标号列也用同样的方式进行拷贝并修改。

#### 2.3.3  完成搜索表单展示

在 Element 官网找到横排的表单效果，然后拷贝代码并进行修改

![image-20210831194300357](D:/download/downloadFromMicsoft/day13-Vue&Element/01-Vue&ElementUI/ppt/assets/image-20210831194300357.png)

点击上面的 `显示代码` 后，就会展示出对应的代码，下面是对这部分代码进行分析的图解

![image-20210831194835721](D:/download/downloadFromMicsoft/day13-Vue&Element/01-Vue&ElementUI/ppt/assets/image-20210831194835721.png)

然后根据要的效果修改代码。

#### 2.3.4  完成批量删除和新增按钮展示

从 Element 官网找具有着色效果的按钮，并将代码拷贝到自己的页面上

<img src="D:/download/downloadFromMicsoft/day13-Vue&Element/01-Vue&ElementUI/ppt/assets/image-20210831214602954.png" alt="image-20210831214602954" style="zoom:70%;" />



#### 2.3.5  完成对话框展示

在 Element 官网找对话框，如下：

<img src="D:/download/downloadFromMicsoft/day13-Vue&Element/01-Vue&ElementUI/ppt/assets/image-20210831214818516.png" alt="image-20210831214818516" style="zoom:70%;" />

下面对官网提供的代码进行分析

<img src="D:/download/downloadFromMicsoft/day13-Vue&Element/01-Vue&ElementUI/ppt/assets/image-20210831215609729.png" alt="image-20210831215609729" style="zoom:80%;" />

上图分析出来的模型数据需要在 Vue 对象中进行定义。

#### 2.3.6  完成分页条展示

在 Element 官网找到 `Pagination 分页` ，在页面主体部分找到需要的效果，如下

<img src="D:/download/downloadFromMicsoft/day13-Vue&Element/01-Vue&ElementUI/ppt/assets/image-20210831220034775.png" alt="image-20210831220034775" style="zoom:70%;" />

点击 `显示代码` ，找到 `完整功能` 对应的代码，接下来对该代码进行分析

<img src="D:/download/downloadFromMicsoft/day13-Vue&Element/01-Vue&ElementUI/ppt/assets/image-20210831220446390.png" alt="image-20210831220446390" style="zoom:80%;" />

上面代码属性说明：

* `page-size` ：每页显示的条目数

* `page-sizes` ： 每页显示个数选择器的选项设置。

  `:page-sizes="[100,200,300,400]"`  对应的页面效果如下：

  <img src="D:/download/downloadFromMicsoft/day13-Vue&Element/01-Vue&ElementUI/ppt/assets/image-20210831220820557.png" alt="image-20210831220820557" style="zoom:70%;" />

* `currentPage` ：当前页码。点击那个页码，此属性值就是几。

* `total` ：总记录数。用来设置总的数据条目数，该属性设置后， Element 会自动计算出需分多少页并给展示对应的页码。

事件说明：

* `size-change` ：pageSize 改变时会触发。也就是当改变了每页显示的条目数后，该事件会触发。
* `current-change` ：currentPage 改变时会触发。也就是当点击了其他的页码后，该事件会触发。

#### 2.3.7  完整页面代码

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        .el-table .warning-row {
            background: oldlace;
        }
        .el-table .success-row {
            background: #f0f9eb;
        }
    </style>
</head>
<body>
<div id="app">
    <!--搜索表单-->
    <el-form :inline="true" :model="brand" class="demo-form-inline">
        <el-form-item label="当前状态">
            <el-select v-model="brand.status" placeholder="当前状态">
                <el-option label="启用" value="1"></el-option>
                <el-option label="禁用" value="0"></el-option>
            </el-select>
        </el-form-item>

        <el-form-item label="企业名称">
            <el-input v-model="brand.companyName" placeholder="企业名称"></el-input>
        </el-form-item>

        <el-form-item label="品牌名称">
            <el-input v-model="brand.brandName" placeholder="品牌名称"></el-input>
        </el-form-item>

        <el-form-item>
            <el-button type="primary" @click="onSubmit">查询</el-button>
        </el-form-item>
    </el-form>

    <!--按钮-->
    <el-row>
        <el-button type="danger" plain>批量删除</el-button>
        <el-button type="primary" plain @click="dialogVisible = true">新增</el-button>
    </el-row>
    
    <!--添加数据对话框表单-->
    <el-dialog
            title="编辑品牌"
            :visible.sync="dialogVisible"
            width="30%">
        <el-form ref="form" :model="brand" label-width="80px">
            <el-form-item label="品牌名称">
                <el-input v-model="brand.brandName"></el-input>
            </el-form-item>

            <el-form-item label="企业名称">
                <el-input v-model="brand.companyName"></el-input>
            </el-form-item>

            <el-form-item label="排序">
                <el-input v-model="brand.ordered"></el-input>
            </el-form-item>

            <el-form-item label="备注">
                <el-input type="textarea" v-model="brand.description"></el-input>
            </el-form-item>

            <el-form-item label="状态">
                <el-switch v-model="brand.status"
                           active-value="1"
                           inactive-value="0"
                ></el-switch>
            </el-form-item>
            <el-form-item>
                <el-button type="primary" @click="addBrand">提交</el-button>
                <el-button @click="dialogVisible = false">取消</el-button>
            </el-form-item>
        </el-form>
    </el-dialog>

    <!--表格-->
    <template>
        <el-table
                :data="tableData"
                style="width: 100%"
                :row-class-name="tableRowClassName"
                @selection-change="handleSelectionChange">
            <el-table-column
                    type="selection"
                    width="55">
            </el-table-column>
            <el-table-column
                    type="index"
                    width="50">
            </el-table-column>
            <el-table-column
                    prop="brandName"
                    label="品牌名称"
                    align="center">
            </el-table-column>
            <el-table-column
                    prop="companyName"
                    label="企业名称"
                    align="center">
            </el-table-column>
            <el-table-column
                    prop="ordered"
                    align="center"
                    label="排序">
            </el-table-column>
            <el-table-column
                    prop="status"
                    align="center"
                    label="当前状态">
            </el-table-column>
            <el-table-column
                    align="center"
                    label="操作">
                <el-row>
                    <el-button type="primary">修改</el-button>
                    <el-button type="danger">删除</el-button>
                </el-row>
            </el-table-column>

        </el-table>
    </template>

    <!--分页工具条-->
    <el-pagination
            @size-change="handleSizeChange"
            @current-change="handleCurrentChange"
            :current-page="currentPage"
            :page-sizes="[5, 10, 15, 20]"
            :page-size="5"
            layout="total, sizes, prev, pager, next, jumper"
            :total="400">
    </el-pagination>

</div>
<script src="js/vue.js"></script>
<script src="element-ui/lib/index.js"></script>
<link rel="stylesheet" href="element-ui/lib/theme-chalk/index.css">
<script>
    new Vue({
        el: "#app",
        methods: {
            tableRowClassName({row, rowIndex}) {
                if (rowIndex === 1) {
                    return 'warning-row';
                } else if (rowIndex === 3) {
                    return 'success-row';
                }
                return '';
            },
            // 复选框选中后执行的方法
            handleSelectionChange(val) {
                this.multipleSelection = val;

                console.log(this.multipleSelection)
            },
            // 查询方法
            onSubmit() {
                console.log(this.brand);
            },
            // 添加数据
            addBrand(){
                console.log(this.brand);
            },
            //分页
            handleSizeChange(val) {
                console.log(`每页 ${val} 条`);
            },
            handleCurrentChange(val) {
                console.log(`当前页: ${val}`);
            }
        },
        data() {
            return {
                // 当前页码
                currentPage: 4,
                // 添加数据对话框是否展示的标记
                dialogVisible: false,

                // 品牌模型数据
                brand: {
                    status: '',
                    brandName: '',
                    companyName: '',
                    id:"",
                    ordered:"",
                    description:""
                },
                // 复选框选中数据集合
                multipleSelection: [],
                // 表格数据
                tableData: [{
                    brandName: '华为',
                    companyName: '华为科技有限公司',
                    ordered: '100',
                    status: "1"
                }, {
                    brandName: '华为',
                    companyName: '华为科技有限公司',
                    ordered: '100',
                    status: "1"
                }, {
                    brandName: '华为',
                    companyName: '华为科技有限公司',
                    ordered: '100',
                    status: "1"
                }, {
                    brandName: '华为',
                    companyName: '华为科技有限公司',
                    ordered: '100',
                    status: "1"
                }]
            }
        }
    })
</script>
</body>
</html>
```

## 3，综合案例

### 3.1  功能介绍

![image-20210825171411003](D:/传智播客/2021年/web阶段文档编写/JavaWeb课程文档/day14-综合案例/assets/image-20210825171411003.png)

以上是在综合案例要实现的功能。对数据的除了对数据的增删改查功能外，还有一些复杂的功能，如 `批量删除`、`分页查询`、`条件查询` 等功能

* `批量删除` 功能：每条数据前都有复选框，当我选中多条数据并点击 `批量删除` 按钮后，会发送请求到后端并删除数据库中指定的多条数据。
* `分页查询` 功能：当数据库中有很多数据时，不可能将所有的数据展示在一页里，这个时候就需要分页展示数据。
* `条件查询` 功能：数据库量大的时候，就需要精确的查询一些想看到的数据，这个时候就需要通过条件查询。

这里的 `修改品牌` 和 `删除品牌` 功能在课程上不做讲解，留作同学来下的练习。

### 3.2  环境准备

环境准备主要完成以下两件事即可

* 将资料的 brand-case 模块导入到 idea中
* 执行资料中提供的 tb_brand.sql脚本

#### 3.2.1  工程准备

将 `04-资料\01-初始工程` 中的 `brand-case` 工程导入到自己的 idea 中。工程结构如下：

<img src="D:/传智播客/2021年/web阶段文档编写/JavaWeb课程文档/day14-综合案例/assets/image-20210825195522904.png" alt="image-20210825195522904" style="zoom:80%;" />

#### 3.2.2  创建表

下面是创建表的语句

```sql
-- 删除tb_brand表
drop table if exists tb_brand;
-- 创建tb_brand表
create table tb_brand (
    -- id 主键
    id           int primary key auto_increment,
    -- 品牌名称
    brand_name   varchar(20),
    -- 企业名称
    company_name varchar(20),
    -- 排序字段
    ordered      int,
    -- 描述信息
    description  varchar(100),
    -- 状态：0：禁用  1：启用
    status       int
);
-- 添加数据
insert into tb_brand (brand_name, company_name, ordered, description, status)
values 
       ('华为', '华为技术有限公司', 100, '万物互联', 1),
       ('小米', '小米科技有限公司', 50, 'are you ok', 1),
       ('格力', '格力电器股份有限公司', 30, '让世界爱上中国造', 1),
       ('阿里巴巴', '阿里巴巴集团控股有限公司', 10, '买买买', 1),
       ('腾讯', '腾讯计算机系统有限公司', 50, '玩玩玩', 0),
       ('百度', '百度在线网络技术公司', 5, '搜搜搜', 0),
       ('京东', '北京京东世纪贸易有限公司', 40, '就是快', 1),
       ('小米', '小米科技有限公司', 50, 'are you ok', 1),
       ('三只松鼠', '三只松鼠股份有限公司', 5, '好吃不上火', 0),
       ('华为', '华为技术有限公司', 100, '万物互联', 1),
       ('小米', '小米科技有限公司', 50, 'are you ok', 1),
       ('格力', '格力电器股份有限公司', 30, '让世界爱上中国造', 1),
       ('阿里巴巴', '阿里巴巴集团控股有限公司', 10, '买买买', 1),
       ('腾讯', '腾讯计算机系统有限公司', 50, '玩玩玩', 0),
       ('百度', '百度在线网络技术公司', 5, '搜搜搜', 0),
       ('京东', '北京京东世纪贸易有限公司', 40, '就是快', 1),
       ('华为', '华为技术有限公司', 100, '万物互联', 1),
       ('小米', '小米科技有限公司', 50, 'are you ok', 1),
       ('格力', '格力电器股份有限公司', 30, '让世界爱上中国造', 1),
       ('阿里巴巴', '阿里巴巴集团控股有限公司', 10, '买买买', 1),
       ('腾讯', '腾讯计算机系统有限公司', 50, '玩玩玩', 0),
       ('百度', '百度在线网络技术公司', 5, '搜搜搜', 0),
       ('京东', '北京京东世纪贸易有限公司', 40, '就是快', 1),
       ('小米', '小米科技有限公司', 50, 'are you ok', 1),
       ('三只松鼠', '三只松鼠股份有限公司', 5, '好吃不上火', 0),
       ('华为', '华为技术有限公司', 100, '万物互联', 1),
       ('小米', '小米科技有限公司', 50, 'are you ok', 1),
       ('格力', '格力电器股份有限公司', 30, '让世界爱上中国造', 1),
       ('阿里巴巴', '阿里巴巴集团控股有限公司', 10, '买买买', 1),
       ('腾讯', '腾讯计算机系统有限公司', 50, '玩玩玩', 0),
       ('百度', '百度在线网络技术公司', 5, '搜搜搜', 0),
       ('京东', '北京京东世纪贸易有限公司', 40, '就是快', 1),
       ('华为', '华为技术有限公司', 100, '万物互联', 1),
       ('小米', '小米科技有限公司', 50, 'are you ok', 1),
       ('格力', '格力电器股份有限公司', 30, '让世界爱上中国造', 1),
       ('阿里巴巴', '阿里巴巴集团控股有限公司', 10, '买买买', 1),
       ('腾讯', '腾讯计算机系统有限公司', 50, '玩玩玩', 0),
       ('百度', '百度在线网络技术公司', 5, '搜搜搜', 0),
       ('京东', '北京京东世纪贸易有限公司', 40, '就是快', 1),
       ('小米', '小米科技有限公司', 50, 'are you ok', 1),
       ('三只松鼠', '三只松鼠股份有限公司', 5, '好吃不上火', 0),
       ('华为', '华为技术有限公司', 100, '万物互联', 1),
       ('小米', '小米科技有限公司', 50, 'are you ok', 1),
       ('格力', '格力电器股份有限公司', 30, '让世界爱上中国造', 1),
       ('阿里巴巴', '阿里巴巴集团控股有限公司', 10, '买买买', 1),
       ('腾讯', '腾讯计算机系统有限公司', 50, '玩玩玩', 0),
       ('百度', '百度在线网络技术公司', 5, '搜搜搜', 0),
       ('京东', '北京京东世纪贸易有限公司', 40, '就是快', 1);
```

### 3.3  查询所有功能

![image-20210825200138600](D:/传智播客/2021年/web阶段文档编写/JavaWeb课程文档/day14-综合案例/assets/image-20210825200138600.png)

如上图所示是查询所有品牌数据在页面展示的效果。要实现这个功能，要先搞明白如下问题：

* 什么时候发送异步请求？

  页面加载完毕后就需要在页面上看到所有的品牌数据。所以在 `mounted()` 这个构造函数中写发送异步请求的代码。

* 请求需要携带参数吗？

  查询所有功能不需要携带什么参数。

* 响应的数据格式是什么样？

  后端是需要将 `List<Brand>` 对象转换为 JSON 格式的数据并响应回给浏览器。响应数据格式如下：

  ![image-20210825201634849](D:/传智播客/2021年/web阶段文档编写/JavaWeb课程文档/day14-综合案例/assets/image-20210825201634849.png)

整体流程如下

![image-20210825200332542](D:/传智播客/2021年/web阶段文档编写/JavaWeb课程文档/day14-综合案例/assets/image-20210825200332542.png)

先实现后端程序，然后再实现前端程序。

#### 3.3.1 后端实现

##### 3.3.1.1  dao方法实现

在 `com.itheima.mapper.BrandMapper` 接口中定义抽象方法，并使用 `@Select` 注解编写 sql 语句

```java
/**
     * 查询所有
     * @return
     */
@Select("select * from tb_brand")
List<Brand> selectAll();
```

由于表中有些字段名和实体类中的属性名没有对应，所以需要在 `com/itheima/mapper/BrandMapper.xml` 映射配置文件中定义结果映射 ，使用`resultMap` 标签。映射配置文件内容如下：

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.itheima.mapper.BrandMapper">

    <resultMap id="brandResultMap" type="brand">
        <result property="brandName" column="brand_name" />
        <result property="companyName" column="company_name" />
    </resultMap>
</mapper>
```

定义完结果映射关系后，在接口 `selectAll()` 方法上引用该结构映射。使用 `@ResultMap("brandResultMap")` 注解

完整接口的 `selectAll()` 方法如下：

```java
/**
     * 查询所有
     * @return
     */
@Select("select * from tb_brand")
@ResultMap("brandResultMap")
List<Brand> selectAll();
```

##### 3.3.1.2  service方法实现

在 `com.itheima.service` 包下创建 `BrandService` 接口，在该接口中定义查询所有的抽象方法

```java
public interface BrandService {

    /**
     * 查询所有
     * @return
     */
    List<Brand> selectAll();
}
```

并在 `com.itheima.service` 下再创建 `impl` 包；`impl` 表示是放 service 层接口的实现类的包。 在该包下创建名为 `BrandServiceImpl` 类

```java
public class BrandServiceImpl implements BrandService {

    @Override
    public List<Brand> selectAll() {
    }
}
```

此处为什么要给 service 定义接口呢？因为service定义了接口后，在 servlet 中就可以使用多态的形式创建Service实现类的对象，如下：

<img src="D:/传智播客/2021年/web阶段文档编写/JavaWeb课程文档/day14-综合案例/assets/image-20210825203843142.png" alt="image-20210825203843142" style="zoom:80%;" />

这里使用多态是因为方便后期解除 `Servlet` 和 `service` 的耦合。从上面的代码可以看到 `SelectAllServlet` 类和 `BrandServiceImpl` 类之间是耦合在一起的，如果后期 `BrandService` 有其它更好的实现类（例如叫 `BrandServiceImpl`），那就需要修改 `SelectAllServlet` 类中的代码。后面学习了 `Spring` 框架后就可以解除 `SelectAllServlet` 类和红色框括起来的代码耦合。而现在咱们还做不到解除耦合，在这里只需要理解为什么定义接口即可。

`BrandServiceImpl` 类代码如下：

```java
public class BrandServiceImpl implements BrandService {
    //1. 创建SqlSessionFactory 工厂对象
    SqlSessionFactory factory = SqlSessionFactoryUtils.getSqlSessionFactory();

    @Override
    public List<Brand> selectAll() {
        //2. 获取SqlSession对象
        SqlSession sqlSession = factory.openSession();
        //3. 获取BrandMapper
        BrandMapper mapper = sqlSession.getMapper(BrandMapper.class);

        //4. 调用方法
        List<Brand> brands = mapper.selectAll();

        //5. 释放资源
        sqlSession.close();

        return brands;
    }
}
```

##### 3.3.1.3  servlet实现

在 `com.itheima.web.servlet` 包下定义名为 `SelectAllServlet` 的查询所有的 `servlet`。该 `servlet` 逻辑如下：

* 调用service的 `selectAll()` 方法查询所有的品牌数据，并接口返回结果
* 将返回的结果转换为 json 数据
* 响应 json 数据

代码如下：

```java
@WebServlet("/selectAllServlet")
public class SelectAllServlet extends HttpServlet {

    private BrandService brandService = new BrandServiceImpl();

    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //1. 调用service查询
        List<Brand> brands = brandService.selectAll();
        //2. 转为JSON
        String jsonString = JSON.toJSONString(brands);
        //3. 写数据
        response.setContentType("text/json;charset=utf-8"); //告知浏览器响应的数据是什么， 告知浏览器使用什么字符集进行解码
        response.getWriter().write(jsonString);
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doGet(request, response);
    }
}
```

##### 3.3.1.4  测试后端程序

在浏览器输入访问 servlet 的资源路径 `http://localhost:8080/brand-case/selectAllServlet` ，如果没有报错，并能看到如下信息表明后端程序没有问题

![image-20210825205133752](D:/传智播客/2021年/web阶段文档编写/JavaWeb课程文档/day14-综合案例/assets/image-20210825205133752.png)

#### 3.3.2  前端实现

前端需要在页面加载完毕后发送 ajax 请求，所以发送请求的逻辑应该放在 `mounted()` 钩子函数中。而响应回来的数据需要赋值给表格绑定的数据模型，从下图可以看出表格绑定的数据模型是 `tableData`

<img src="D:/传智播客/2021年/web阶段文档编写/JavaWeb课程文档/day14-综合案例/assets/image-20210825220436889.png" alt="image-20210825220436889" style="zoom:70%;" />

前端代码如下：

```js
 mounted(){
     //当页面加载完成后，发送异步请求，获取数据
     var _this = this;

     axios({
         method:"get",
         url:"http://localhost:8080/brand-case/selectAllServlet"
     }).then(function (resp) {
         _this.tableData = resp.data;
     })
 }
```

### 3.4  添加功能

<img src="D:/传智播客/2021年/web阶段文档编写/JavaWeb课程文档/day14-综合案例/assets/image-20210825221138245.png" alt="image-20210825221138245" style="zoom:70%;" />

上图是添加数据的对话框，当点击 `提交` 按钮后就需要将数据提交到后端，并将数据保存到数据库中。下图是整体的流程：

![image-20210825221329231](D:/传智播客/2021年/web阶段文档编写/JavaWeb课程文档/day14-综合案例/assets/image-20210825221329231.png)

页面发送请求时，需要将输入框输入的内容提交给后端程序，而这里是以 json 格式进行传递的。而具体的数据格式如下：

![image-20210826185917510](D:/传智播客/2021年/web阶段文档编写/JavaWeb课程文档/day14-综合案例/assets/image-20210826185917510.png)

> ==注意：由于是添加数据，所以上述json数据中id是没有值的。==

#### 3.4.1  后端实现

##### 3.4.1.1  dao方法实现

在 `BrandMapper` 接口中定义 `add()` 添加方法，并使用 `@Insert` 注解编写sql语句

```java
/**
     * 添加数据
     * @param brand
     */
@Insert("insert into tb_brand values(null,#{brandName},#{companyName},#{ordered},#{description},#{status})")
void add(Brand brand);
```

##### 3.4.1.2  service方法实现

在 `BrandService` 接口中定义 `add()` 添加数据的业务逻辑方法

```java
/**
     * 添加数据
     * @param brand
     */
void add(Brand brand);
```

在 `BrandServiceImpl` 类中重写 `add()` 方法，并进行业务逻辑实现

```java
@Override
public void add(Brand brand) {
    //2. 获取SqlSession对象
    SqlSession sqlSession = factory.openSession();
    //3. 获取BrandMapper
    BrandMapper mapper = sqlSession.getMapper(BrandMapper.class);

    //4. 调用方法
    mapper.add(brand);
    sqlSession.commit();//提交事务

    //5. 释放资源
    sqlSession.close();
}
```

> ==注意：增删改操作一定要提交事务。==

##### 3.4.1.3  servlet实现

在 `com.itheima.web.servlet` 包写定义名为 `AddServlet` 的 Servlet。该 Servlet 的逻辑如下：

* 接收页面提交的数据。页面到时候提交的数据是 json 格式的数据，所以此处需要使用输入流读取数据
* 将接收到的数据转换为 `Brand` 对象
* 调用 service 的 `add()` 方法进行添加的业务逻辑处理
* 给浏览器响应添加成功的标识，这里直接给浏览器响应 `success` 字符串表示成功

servlet 代码实现如下：

```java
@WebServlet("/addServlet")
public class AddServlet extends HttpServlet {

    private BrandService brandService = new BrandServiceImpl();

    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

        //1. 接收品牌数据
        BufferedReader br = request.getReader();
        String params = br.readLine();//json字符串
        //转为Brand对象
        Brand brand = JSON.parseObject(params, Brand.class);
        //2. 调用service添加
        brandService.add(brand);
        //3. 响应成功的标识
        response.getWriter().write("success");
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doGet(request, response);
    }
}
```

#### 3.4.2  前端实现

<img src="D:/传智播客/2021年/web阶段文档编写/JavaWeb课程文档/day14-综合案例/assets/image-20210825223121993.png" alt="image-20210825223121993" style="zoom:60%;" />

上图左边是页面效果，里面的 `提交` 按钮可以通过上图右边看出绑定了一个 单击事件，而该事件绑定的是 `addBrand` 函数，所以添加数据功能的逻辑代码应该写在 `addBrand()`  函数中。在此方法中需要发送异步请求并将表单中输入的数据作为参数进行传递。如下

```js
// 添加数据
addBrand() {
    var _this = this;

    // 发送ajax请求，添加数据
    axios({
        method:"post",
        url:"http://localhost:8080/brand-case/addServlet",
        data:_this.brand
    }).then(function (resp) {
       	//响应数据的处理逻辑
    })
}
```

在 `then` 函数中的匿名函数是成功后的回调函数，而 `resp.data` 就可以获取到响应回来的数据，如果值是 `success` 表示数据添加成功。成功后需要做一下逻辑处理：

1. **关闭新增对话框窗口**

   如下图所示是添加数据的对话框代码，从代码中可以看到此对话框绑定了 `dialogVisible` 数据模型，只需要将该数据模型的值设置为 false，就可以关闭新增对话框窗口了。

   <img src="D:/传智播客/2021年/web阶段文档编写/JavaWeb课程文档/day14-综合案例/assets/image-20210825223933953.png" alt="image-20210825223933953" style="zoom:70%;" />

2. **重新查询数据**

   数据添加成功与否，用户只要能在页面上查看到数据说明添加成功。而此处需要重新发送异步请求获取所有的品牌数据，而这段代码在 `查询所有` 功能中已经实现，所以可以将此功能代码进行抽取，抽取到一个 `selectAll()` 函数中

   ```js
   // 查询所有数据
   selectAll(){
       var _this = this;
   
       axios({
           method:"get",
           url:"http://localhost:8080/brand-case/selectAllServlet"
       }).then(function (resp) {
           _this.tableData = resp.data;
       })
   }
   ```

   那么就需要将 `mounted()` 钩子函数中代码改进为

   ```js
   mounted(){
       //当页面加载完成后，发送异步请求，获取数据
       this.selectAll();
   }
   ```

   同时在新增响应的回调中调用 `selectAll()` 进行数据的重新查询。

3. **弹出消息给用户提示添加成功**

   ![image-20210825224958220](D:/传智播客/2021年/web阶段文档编写/JavaWeb课程文档/day14-综合案例/assets/image-20210825224958220.png)

   上图左边就是 elementUI 官网提供的成功提示代码，而上图右边是具体的效果。

   > ==注意：上面的this需要的是表示 VUE 对象的this。==

综上所述，前端代码如下：

```js
// 添加数据
addBrand() {
    var _this = this;

    // 发送ajax请求，添加数据
    axios({
        method:"post",
        url:"http://localhost:8080/brand-case/addServlet",
        data:_this.brand
    }).then(function (resp) {
        if(resp.data == "success"){
            //添加成功
            //关闭窗口
            _this.dialogVisible = false;
            // 重新查询数据
            _this.selectAll();
            // 弹出消息提示
            _this.$message({
                message: '恭喜你，添加成功',
                type: 'success'
            });
        }
    })
}
```



# 综合案例

**今日目标：**

> * 能够完成查询所有功能
> * 能够完成添加功能
> * 能够理解 BaseServlet 思想
> * 能够完成批量删除功能
> * 能够完成分页查询功能
> * 能够完成条件查询功能

## 1，功能介绍

![image-20210825171411003](D:/download/downloadFromMicsoft/day14-综合案例/ppt/assets/image-20210825171411003.png)

以上是在综合案例要实现的功能。对数据的除了对数据的增删改查功能外，还有一些复杂的功能，如 `批量删除`、`分页查询`、`条件查询` 等功能

* `批量删除` 功能：每条数据前都有复选框，当我选中多条数据并点击 `批量删除` 按钮后，会发送请求到后端并删除数据库中指定的多条数据。
* `分页查询` 功能：当数据库中有很多数据时，不可能将所有的数据展示在一页里，这个时候就需要分页展示数据。
* `条件查询` 功能：数据库量大的时候，就需要精确的查询一些想看到的数据，这个时候就需要通过条件查询。

这里的 `修改品牌` 和 `删除品牌` 功能在课程上不做讲解，留作同学来下的练习。

## 2，环境准备

环境准备主要完成以下两件事即可

* 将资料的 brand-case 模块导入到 idea中
* 执行资料中提供的 tb_brand.sql脚本

### 2.1  工程准备

将 `04-资料\01-初始工程` 中的 `brand-case` 工程导入到自己的 idea 中。工程结构如下：

<img src="D:/download/downloadFromMicsoft/day14-综合案例/ppt/assets/image-20210825195522904.png" alt="image-20210825195522904" style="zoom:80%;" />

### 2.2  创建表

下面是创建表的语句

```sql
-- 删除tb_brand表
drop table if exists tb_brand;
-- 创建tb_brand表
create table tb_brand (
    -- id 主键
    id           int primary key auto_increment,
    -- 品牌名称
    brand_name   varchar(20),
    -- 企业名称
    company_name varchar(20),
    -- 排序字段
    ordered      int,
    -- 描述信息
    description  varchar(100),
    -- 状态：0：禁用  1：启用
    status       int
);
-- 添加数据
insert into tb_brand (brand_name, company_name, ordered, description, status)
values 
       ('华为', '华为技术有限公司', 100, '万物互联', 1),
       ('小米', '小米科技有限公司', 50, 'are you ok', 1),
       ('格力', '格力电器股份有限公司', 30, '让世界爱上中国造', 1),
       ('阿里巴巴', '阿里巴巴集团控股有限公司', 10, '买买买', 1),
       ('腾讯', '腾讯计算机系统有限公司', 50, '玩玩玩', 0),
       ('百度', '百度在线网络技术公司', 5, '搜搜搜', 0),
       ('京东', '北京京东世纪贸易有限公司', 40, '就是快', 1),
       ('小米', '小米科技有限公司', 50, 'are you ok', 1),
       ('三只松鼠', '三只松鼠股份有限公司', 5, '好吃不上火', 0),
       ('华为', '华为技术有限公司', 100, '万物互联', 1),
       ('小米', '小米科技有限公司', 50, 'are you ok', 1),
       ('格力', '格力电器股份有限公司', 30, '让世界爱上中国造', 1),
       ('阿里巴巴', '阿里巴巴集团控股有限公司', 10, '买买买', 1),
       ('腾讯', '腾讯计算机系统有限公司', 50, '玩玩玩', 0),
       ('百度', '百度在线网络技术公司', 5, '搜搜搜', 0),
       ('京东', '北京京东世纪贸易有限公司', 40, '就是快', 1),
       ('华为', '华为技术有限公司', 100, '万物互联', 1),
       ('小米', '小米科技有限公司', 50, 'are you ok', 1),
       ('格力', '格力电器股份有限公司', 30, '让世界爱上中国造', 1),
       ('阿里巴巴', '阿里巴巴集团控股有限公司', 10, '买买买', 1),
       ('腾讯', '腾讯计算机系统有限公司', 50, '玩玩玩', 0),
       ('百度', '百度在线网络技术公司', 5, '搜搜搜', 0),
       ('京东', '北京京东世纪贸易有限公司', 40, '就是快', 1),
       ('小米', '小米科技有限公司', 50, 'are you ok', 1),
       ('三只松鼠', '三只松鼠股份有限公司', 5, '好吃不上火', 0),
       ('华为', '华为技术有限公司', 100, '万物互联', 1),
       ('小米', '小米科技有限公司', 50, 'are you ok', 1),
       ('格力', '格力电器股份有限公司', 30, '让世界爱上中国造', 1),
       ('阿里巴巴', '阿里巴巴集团控股有限公司', 10, '买买买', 1),
       ('腾讯', '腾讯计算机系统有限公司', 50, '玩玩玩', 0),
       ('百度', '百度在线网络技术公司', 5, '搜搜搜', 0),
       ('京东', '北京京东世纪贸易有限公司', 40, '就是快', 1),
       ('华为', '华为技术有限公司', 100, '万物互联', 1),
       ('小米', '小米科技有限公司', 50, 'are you ok', 1),
       ('格力', '格力电器股份有限公司', 30, '让世界爱上中国造', 1),
       ('阿里巴巴', '阿里巴巴集团控股有限公司', 10, '买买买', 1),
       ('腾讯', '腾讯计算机系统有限公司', 50, '玩玩玩', 0),
       ('百度', '百度在线网络技术公司', 5, '搜搜搜', 0),
       ('京东', '北京京东世纪贸易有限公司', 40, '就是快', 1),
       ('小米', '小米科技有限公司', 50, 'are you ok', 1),
       ('三只松鼠', '三只松鼠股份有限公司', 5, '好吃不上火', 0),
       ('华为', '华为技术有限公司', 100, '万物互联', 1),
       ('小米', '小米科技有限公司', 50, 'are you ok', 1),
       ('格力', '格力电器股份有限公司', 30, '让世界爱上中国造', 1),
       ('阿里巴巴', '阿里巴巴集团控股有限公司', 10, '买买买', 1),
       ('腾讯', '腾讯计算机系统有限公司', 50, '玩玩玩', 0),
       ('百度', '百度在线网络技术公司', 5, '搜搜搜', 0),
       ('京东', '北京京东世纪贸易有限公司', 40, '就是快', 1);
```

## 3，查询所有功能

![image-20210825200138600](D:/download/downloadFromMicsoft/day14-综合案例/ppt/assets/image-20210825200138600.png)

如上图所示是查询所有品牌数据在页面展示的效果。要实现这个功能，要先搞明白如下问题：

* 什么时候发送异步请求？

  页面加载完毕后就需要在页面上看到所有的品牌数据。所以在 `mounted()` 这个构造函数中写发送异步请求的代码。

* 请求需要携带参数吗？

  查询所有功能不需要携带什么参数。

* 响应的数据格式是什么样？

  后端是需要将 `List<Brand>` 对象转换为 JSON 格式的数据并响应回给浏览器。响应数据格式如下：

  ![image-20210825201634849](D:/download/downloadFromMicsoft/day14-综合案例/ppt/assets/image-20210825201634849.png)

整体流程如下

![image-20210825200332542](D:/download/downloadFromMicsoft/day14-综合案例/ppt/assets/image-20210825200332542.png)

先实现后端程序，然后再实现前端程序。

### 3.1 后端实现

#### 3.1.1  dao方法实现

在 `com.itheima.mapper.BrandMapper` 接口中定义抽象方法，并使用 `@Select` 注解编写 sql 语句

```java
/**
     * 查询所有
     * @return
     */
@Select("select * from tb_brand")
List<Brand> selectAll();
```

由于表中有些字段名和实体类中的属性名没有对应，所以需要在 `com/itheima/mapper/BrandMapper.xml` 映射配置文件中定义结果映射 ，使用`resultMap` 标签。映射配置文件内容如下：

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.itheima.mapper.BrandMapper">

    <resultMap id="brandResultMap" type="brand">
        <result property="brandName" column="brand_name" />
        <result property="companyName" column="company_name" />
    </resultMap>
</mapper>
```

定义完结果映射关系后，在接口 `selectAll()` 方法上引用该结构映射。使用 `@ResultMap("brandResultMap")` 注解

完整接口的 `selectAll()` 方法如下：

```java
/**
     * 查询所有
     * @return
     */
@Select("select * from tb_brand")
@ResultMap("brandResultMap")
List<Brand> selectAll();
```

#### 3.1.2  service方法实现

在 `com.itheima.service` 包下创建 `BrandService` 接口，在该接口中定义查询所有的抽象方法

```java
public interface BrandService {

    /**
     * 查询所有
     * @return
     */
    List<Brand> selectAll();
}
```

并在 `com.itheima.service` 下再创建 `impl` 包；`impl` 表示是放 service 层接口的实现类的包。 在该包下创建名为 `BrandServiceImpl` 类

```java
public class BrandServiceImpl implements BrandService {

    @Override
    public List<Brand> selectAll() {
    }
}
```

此处为什么要给 service 定义接口呢？因为service定义了接口后，在 servlet 中就可以使用多态的形式创建Service实现类的对象，如下：

<img src="D:/download/downloadFromMicsoft/day14-综合案例/ppt/assets/image-20210825203843142.png" alt="image-20210825203843142" style="zoom:80%;" />

这里使用多态是因为方便后期解除 `Servlet` 和 `service` 的耦合。从上面的代码可以看到 `SelectAllServlet` 类和 `BrandServiceImpl` 类之间是耦合在一起的，如果后期 `BrandService` 有其它更好的实现类（例如叫 `BrandServiceImpl`），那就需要修改 `SelectAllServlet` 类中的代码。后面学习了 `Spring` 框架后就可以解除 `SelectAllServlet` 类和红色框括起来的代码耦合。而现在咱们还做不到解除耦合，在这里只需要理解为什么定义接口即可。

`BrandServiceImpl` 类代码如下：

```java
public class BrandServiceImpl implements BrandService {
    //1. 创建SqlSessionFactory 工厂对象
    SqlSessionFactory factory = SqlSessionFactoryUtils.getSqlSessionFactory();

    @Override
    public List<Brand> selectAll() {
        //2. 获取SqlSession对象
        SqlSession sqlSession = factory.openSession();
        //3. 获取BrandMapper
        BrandMapper mapper = sqlSession.getMapper(BrandMapper.class);

        //4. 调用方法
        List<Brand> brands = mapper.selectAll();

        //5. 释放资源
        sqlSession.close();

        return brands;
    }
}
```

#### 3.1.3  servlet实现

在 `com.itheima.web.servlet` 包下定义名为 `SelectAllServlet` 的查询所有的 `servlet`。该 `servlet` 逻辑如下：

* 调用service的 `selectAll()` 方法查询所有的品牌数据，并接口返回结果
* 将返回的结果转换为 json 数据
* 响应 json 数据

代码如下：

```java
@WebServlet("/selectAllServlet")
public class SelectAllServlet extends HttpServlet {

    private BrandService brandService = new BrandServiceImpl();

    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //1. 调用service查询
        List<Brand> brands = brandService.selectAll();
        //2. 转为JSON
        String jsonString = JSON.toJSONString(brands);
        //3. 写数据
        response.setContentType("text/json;charset=utf-8"); //告知浏览器响应的数据是什么， 告知浏览器使用什么字符集进行解码
        response.getWriter().write(jsonString);
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doGet(request, response);
    }
}
```

#### 3.1.4  测试后端程序

在浏览器输入访问 servlet 的资源路径 `http://localhost:8080/brand-case/selectAllServlet` ，如果没有报错，并能看到如下信息表明后端程序没有问题

![image-20210825205133752](D:/download/downloadFromMicsoft/day14-综合案例/ppt/assets/image-20210825205133752.png)

### 3.2  前端实现

前端需要在页面加载完毕后发送 ajax 请求，所以发送请求的逻辑应该放在 `mounted()` 钩子函数中。而响应回来的数据需要赋值给表格绑定的数据模型，从下图可以看出表格绑定的数据模型是 `tableData`

<img src="D:/download/downloadFromMicsoft/day14-综合案例/ppt/assets/image-20210825220436889.png" alt="image-20210825220436889" style="zoom:70%;" />

前端代码如下：

```js
 mounted(){
     //当页面加载完成后，发送异步请求，获取数据
     var _this = this;

     axios({
         method:"get",
         url:"http://localhost:8080/brand-case/selectAllServlet"
     }).then(function (resp) {
         _this.tableData = resp.data;
     })
 }
```

## 4，添加功能

<img src="D:/download/downloadFromMicsoft/day14-综合案例/ppt/assets/image-20210825221138245.png" alt="image-20210825221138245" style="zoom:70%;" />

上图是添加数据的对话框，当点击 `提交` 按钮后就需要将数据提交到后端，并将数据保存到数据库中。下图是整体的流程：

![image-20210825221329231](D:/download/downloadFromMicsoft/day14-综合案例/ppt/assets/image-20210825221329231.png)

页面发送请求时，需要将输入框输入的内容提交给后端程序，而这里是以 json 格式进行传递的。而具体的数据格式如下：

![image-20210826185917510](D:/download/downloadFromMicsoft/day14-综合案例/ppt/assets/image-20210826185917510.png)

> ==注意：由于是添加数据，所以上述json数据中id是没有值的。==

### 4.1  后端实现

#### 4.1.1  dao方法实现

在 `BrandMapper` 接口中定义 `add()` 添加方法，并使用 `@Insert` 注解编写sql语句

```java
/**
     * 添加数据
     * @param brand
     */
@Insert("insert into tb_brand values(null,#{brandName},#{companyName},#{ordered},#{description},#{status})")
void add(Brand brand);
```

#### 4.1.2  service方法实现

在 `BrandService` 接口中定义 `add()` 添加数据的业务逻辑方法

```java
/**
     * 添加数据
     * @param brand
     */
void add(Brand brand);
```

在 `BrandServiceImpl` 类中重写 `add()` 方法，并进行业务逻辑实现

```java
@Override
public void add(Brand brand) {
    //2. 获取SqlSession对象
    SqlSession sqlSession = factory.openSession();
    //3. 获取BrandMapper
    BrandMapper mapper = sqlSession.getMapper(BrandMapper.class);

    //4. 调用方法
    mapper.add(brand);
    sqlSession.commit();//提交事务

    //5. 释放资源
    sqlSession.close();
}
```

> ==注意：增删改操作一定要提交事务。==

#### 4.1.3  servlet实现

在 `com.itheima.web.servlet` 包写定义名为 `AddServlet` 的 Servlet。该 Servlet 的逻辑如下：

* 接收页面提交的数据。页面到时候提交的数据是 json 格式的数据，所以此处需要使用输入流读取数据
* 将接收到的数据转换为 `Brand` 对象
* 调用 service 的 `add()` 方法进行添加的业务逻辑处理
* 给浏览器响应添加成功的标识，这里直接给浏览器响应 `success` 字符串表示成功

servlet 代码实现如下：

```java
@WebServlet("/addServlet")
public class AddServlet extends HttpServlet {

    private BrandService brandService = new BrandServiceImpl();

    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

        //1. 接收品牌数据
        BufferedReader br = request.getReader();
        String params = br.readLine();//json字符串
        //转为Brand对象
        Brand brand = JSON.parseObject(params, Brand.class);
        //2. 调用service添加
        brandService.add(brand);
        //3. 响应成功的标识
        response.getWriter().write("success");
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doGet(request, response);
    }
}
```

### 4.2  前端实现

<img src="D:/download/downloadFromMicsoft/day14-综合案例/ppt/assets/image-20210825223121993.png" alt="image-20210825223121993" style="zoom:60%;" />

上图左边是页面效果，里面的 `提交` 按钮可以通过上图右边看出绑定了一个 单击事件，而该事件绑定的是 `addBrand` 函数，所以添加数据功能的逻辑代码应该写在 `addBrand()`  函数中。在此方法中需要发送异步请求并将表单中输入的数据作为参数进行传递。如下

```js
// 添加数据
addBrand() {
    var _this = this;

    // 发送ajax请求，添加数据
    axios({
        method:"post",
        url:"http://localhost:8080/brand-case/addServlet",
        data:_this.brand
    }).then(function (resp) {
       	//响应数据的处理逻辑
    })
}
```

在 `then` 函数中的匿名函数是成功后的回调函数，而 `resp.data` 就可以获取到响应回来的数据，如果值是 `success` 表示数据添加成功。成功后需要做一下逻辑处理：

1. **关闭新增对话框窗口**

   如下图所示是添加数据的对话框代码，从代码中可以看到此对话框绑定了 `dialogVisible` 数据模型，只需要将该数据模型的值设置为 false，就可以关闭新增对话框窗口了。

   <img src="D:/download/downloadFromMicsoft/day14-综合案例/ppt/assets/image-20210825223933953.png" alt="image-20210825223933953" style="zoom:70%;" />

2. **重新查询数据**

   数据添加成功与否，用户只要能在页面上查看到数据说明添加成功。而此处需要重新发送异步请求获取所有的品牌数据，而这段代码在 `查询所有` 功能中已经实现，所以可以将此功能代码进行抽取，抽取到一个 `selectAll()` 函数中

   ```js
   // 查询所有数据
   selectAll(){
       var _this = this;
   
       axios({
           method:"get",
           url:"http://localhost:8080/brand-case/selectAllServlet"
       }).then(function (resp) {
           _this.tableData = resp.data;
       })
   }
   ```

   那么就需要将 `mounted()` 钩子函数中代码改进为

   ```js
   mounted(){
       //当页面加载完成后，发送异步请求，获取数据
       this.selectAll();
   }
   ```

   同时在新增响应的回调中调用 `selectAll()` 进行数据的重新查询。

3. **弹出消息给用户提示添加成功**

   ![image-20210825224958220](D:/download/downloadFromMicsoft/day14-综合案例/ppt/assets/image-20210825224958220.png)

   上图左边就是 elementUI 官网提供的成功提示代码，而上图右边是具体的效果。

   > ==注意：上面的this需要的是表示 VUE 对象的this。==

综上所述，前端代码如下：

```js
// 添加数据
addBrand() {
    var _this = this;

    // 发送ajax请求，添加数据
    axios({
        method:"post",
        url:"http://localhost:8080/brand-case/addServlet",
        data:_this.brand
    }).then(function (resp) {
        if(resp.data == "success"){
            //添加成功
            //关闭窗口
            _this.dialogVisible = false;
            // 重新查询数据
            _this.selectAll();
            // 弹出消息提示
            _this.$message({
                message: '恭喜你，添加成功',
                type: 'success'
            });
        }
    })
}
```

## 5，servlet优化

### 5.1  问题导入

==Web 层的 Servlet 个数太多了，不利于管理和编写==

通过之前的两个功能，发现每一个功能都需要定义一个 `servlet`，一个模块需要实现增删改查功能，就需要4个 `servlet`，模块一多就会造成`servlet` 泛滥。此时就想 `servlet` 能不能像 `service` 一样，一个模块只定义一个 `servlet`，而每一个功能只需要在该 `servlet` 中定义对应的方法。例如下面代码：

```java
@WebServlet("/brand/*")
public class BrandServlet {
    //查询所有
	public void selectAll(...) {}
    
    //添加数据
    public void add(...) {}
    
     //修改数据
    public void update(...) {}
    
    //删除删除
    public void delete(...) {}
}
```

在已有的代码中，继承extends HttpServlet，该类中自动存在的service源码如下:

而知道发送请求 `servlet`，`tomcat` 会自动的调用 `service()` 方法，之前在自定义的 `servlet` 中重写 `doGet()` 方法和 `doPost()` 方法，当访问该 `servlet` 时会根据请求方式将请求分发给 `doGet()` 或者 `doPost()`  方法，如下图

<img src="D:/download/downloadFromMicsoft/day14-综合案例/ppt/assets/image-20210826184103210.png" alt="image-20210826184103210" style="zoom:80%;" />



仿照这样请求分发的思想，在 `service()` 方法中根据具体的操作调用对应的方法，如：查询所有就调用 `selectAll()` 方法，添加企业信息就调用 `add()` 方法。

为了做到通用，定义一个通用的 `servlet` 类，在定义其他的 `servlet` 是不可以绕过继承 `HttpServlet`，而继承自定义的 `BaseServlet`，（已经继承了HttpServlet ）在` BaseServlet` 中调用具体 `servlet`（如`BrandServlet`）中的对应方法。

即多做一层封装，封装中重写 HttpServlet根据请求方式分发的形式，

```java
public class BaseServlet extends HttpServlet {
    @Override
    protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //进行请求的分发
    }
}
```

`BrandServlet` 定义就需要修改为如下：

```java
@WebServlet("/brand/*")
public class BrandServlet extends BaseServlet {
    //用户实现分页查询
	public void selectAll(...) {} 
    
    //添加企业信息
    public void add(...) {}
    
    //修改企业信息
    public void update(...) {}
    
    //删除企业信息
    public void delete(...) {}
}
```

那么如何在 `BaseServlet` 中调用对应的方法呢？比如查询所有就调用 `selectAll()` 方法。

可以==规定在发送请求时，请求资源的二级路径（/brandServlet/selectAll）和需要调用的方法名相同==，如：

查询所有数据的路径以后就需要写成： `http://localhost:8080/brand-case/brandServlet/selectAll`

添加数据的路径以后就需要写成： `http://localhost:8080/brand-case/brandServlet/add`

修改数据的路径以后就需要写成： `http://localhost:8080/brand-case/brandServlet/update`

删除数据的路径以后就需要写成： `http://localhost:8080/brand-case/brandServlet/delete`

这样的话，在 `BaseServlet` 中就需要获取到资源的二级路径作为方法名，然后调用该方法

```java
public class BaseServlet extends HttpServlet {
    @Override
    protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //1. 获取请求路径
        String uri = req.getRequestURI(); // 例如路径为：/brand-case/brand/selectAll
        //2. 获取最后一段路径，方法名
        int index = uri.lastIndexOf('/');
        String methodName = uri.substring(index + 1); //  获取到资源的二级路径  selectAll

        //2. 执行方法
        //2.1 获取BrandServlet /UserServlet 字节码对象 Class
        //System.out.println(this);

        Class<? extends BaseServlet> cls = this.getClass();
        //2.2 获取方法 Method对象
        try {
            Method method = cls.getMethod(methodName,？？？);
            //4,调用该方法
            method.invoke(this,？？？);
        } catch (NoSuchMethodException e) {
            e.printStackTrace();
        } catch (IllegalAccessException e) {
            e.printStackTrace();
        } catch (InvocationTargetException e) {
            e.printStackTrace();
        }
    }
}
```

通过上面代码发现根据方法名获取对应方法的 `Method` 对象时需要指定方法参数的字节码对象。解决这个问题，可以将方法的参数类型规定死，而方法中可能需要用到 `request` 对象和 `response` 对象，所以指定方法的参数为 `HttpServletRequest` 和 `HttpServletResponse`，那么 `BrandServlet` 代码就可以改进为：

```java
@WebServlet("/brand/*")
public class BrandServlet extends BaseServlet {
    //用户实现分页查询
	public void selectAll(HttpServletRequest req, HttpServletResponse resp) {}
    
    //添加企业信息
    public void add(HttpServletRequest req, HttpServletResponse resp) {}
    
    //修改企业信息
    public void update(HttpServletRequest req, HttpServletResponse resp) {}
    
    //删除企业信息
    public void delete(HttpServletRequest req, HttpServletResponse resp) {}
}
```

BaseServlet代码可以改进为：

```java
public class BaseServlet extends HttpServlet {

    //根据请求的最后一段路径来进行方法分发
    @Override
    protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //1. 获取请求路径
        String uri = req.getRequestURI(); // 例如路径为：/brand-case/brand/selectAll
        //2. 获取最后一段路径，方法名
        int index = uri.lastIndexOf('/');
        String methodName = uri.substring(index + 1); //  获取到资源的二级路径  selectAll   

        //2. 执行方法
        //2.1 获取BrandServlet /UserServlet 字节码对象 Class
        //System.out.println(this);

        Class<? extends BaseServlet> cls = this.getClass();
        //2.2 获取方法 Method对象
        try {   
            Method method = cls.getMethod(methodName, HttpServletRequest.class, HttpServletResponse.class);
            //2.3 执行方法
            method.invoke(this,req,resp);
        } catch (NoSuchMethodException e) {
            e.printStackTrace();
        } catch (IllegalAccessException e) {
            e.printStackTrace();
        } catch (InvocationTargetException e) {
            e.printStackTrace();
        }
    }
}
```

### 5.2  代码优化

#### 5.2.1  后端优化

定义了 `BaseServlet` 后，针对品牌模块定义一个 `BrandServlet` 的 Servlet，并使其继承 `BaseServlet` 。在`BrandServlet`中定义 以下功能的方法：

* `查询所有`  功能：方法名声明为 `selectAll` ，并将之前的 `SelectAllServlet` 中的逻辑代码拷贝到该方法中
* `添加数据` 功能：方法名声明为 `add` ，并将之前的 `AddServlet` 中的逻辑代码拷贝到该方法中

具体代码如下：

```java
@WebServlet("/brand/*")
public class BrandServlet extends BaseServlet{
    private BrandService brandService = new BrandServiceImpl();

    public void selectAll(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //1. 调用service查询
        List<Brand> brands = brandService.selectAll();

        //2. 转为JSON
        String jsonString = JSON.toJSONString(brands);
        //3. 写数据
        response.setContentType("text/json;charset=utf-8");
        response.getWriter().write(jsonString);
    }

    public void add(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

        //1. 接收品牌数据
        BufferedReader br = request.getReader();
        String params = br.readLine();//json字符串

        //转为Brand对象
        Brand brand = JSON.parseObject(params, Brand.class);

        //2. 调用service添加
        brandService.add(brand);

        //3. 响应成功的标识
        response.getWriter().write("success");
    }
}
```

#### 5.2.2  前端优化

页面中之前发送的请求的路径都需要进行修改，`selectAll()` 函数中发送异步请求的 `url` 应该改为 `http://localhost:8080/brand-case/brand/selectAll` 。具体代码如下：

```js
// 查询分页数据
selectAll(){
    var _this = this;

    axios({
        method:"get",
        url:"http://localhost:8080/brand-case/brand/selectAll"
    }).then(function (resp) {
        _this.tableData = resp.data;
    })
}
```

`addBrand()` 函数中发送异步请求的 `url` 应该改为 `http://localhost:8080/brand-case/brand/add` 。具体代码如下：

```js
// 添加数据
addBrand() {
    //console.log(this.brand);
    var _this = this;

    // 发送ajax请求，添加数据
    axios({
        method:"post",
        url:"http://localhost:8080/brand-case/brand/add",
        data:_this.brand
    }).then(function (resp) {
        if(resp.data == "success"){
            //添加成功
            //关闭窗口
            _this.dialogVisible = false;
            // 重新查询数据
            _this.selectAll();
            // 弹出消息提示
            _this.$message({
                message: '恭喜你，添加成功',
                type: 'success'
            });
        }
    })
}
```

## 6，批量删除

<img src="D:/download/downloadFromMicsoft/day14-综合案例/ppt/assets/image-20210826185420668.png" alt="image-20210826185420668" style="zoom:70%;" />

如上图所示点击多条数据前的复选框就意味着要删除这些数据，而点击了 `批量删除` 按钮后，需要让用户确认一下，因为有可能是用户误操作的，当用户确定后需要给后端发送请求并携带者需要删除数据的多个id值，后端程序删除数据库中的数据。具体的流程如下：

![image-20210826201651241](D:/download/downloadFromMicsoft/day14-综合案例/ppt/assets/image-20210826201651241.png)

==注意：==

前端发送请求时需要将要删除的多个id值以json格式提交给后端，而该json格式数据如下：

```json
[1,2,3,4]
```



### 6.1  后端实现

#### 6.1.1  dao方法实现

在 `BrandMapper` 接口中定义 `deleteByIds()` 添加方法，由于这里面要用到动态 sql ，属于复杂的sql操作，建议使用映射配置文件。

接口方法声明如下：

```java
 /**
     * 批量删除
     * @param ids
     */
void deleteByIds(@Param("ids") int[] ids);
```

在 `BrandMapper.xml` 映射配置文件中添加 statement

```xml
<delete id="deleteByIds">
    delete from tb_brand where id in
    <foreach collection="ids" item="id" separator="," open="(" close=")">
        #{id}
    </foreach>
</delete>
```

#### 6.1.2  service方法实现

在 `BrandService` 接口中定义 `deleteByIds()` 批量删除的业务逻辑方法

```java
/**
     * 批量删除
     * @param ids
     */
void deleteByIds( int[] ids);
```

在 `BrandServiceImpl` 类中重写 `deleteByIds()` 方法，并进行业务逻辑实现

```java
@Override
public void deleteByIds(int[] ids) {
    //2. 获取SqlSession对象
    SqlSession sqlSession = factory.openSession();
    //3. 获取BrandMapper
    BrandMapper mapper = sqlSession.getMapper(BrandMapper.class);

    //4. 调用方法
    mapper.deleteByIds(ids);

    sqlSession.commit();//提交事务

    //5. 释放资源
    sqlSession.close();
}
```

#### 6.1.3  servlet实现

在 `BrandServlet` 类中定义 `deleteByIds()`  方法。而该方法的逻辑如下：

* 接收页面提交的数据。页面到时候提交的数据是 json 格式的数据，所以此处需要使用输入流读取数据
* 接收页面提交的数据。页面到时候提交的数据是 json 格式的数据，所以此处需要使用输入流读取数据
* 将接收到的数据转换为 `int[]` 数组
* 调用 service 的 `deleteByIds()` 方法进行批量删除的业务逻辑处理
* 给浏览器响应添加成功的标识，这里直接给浏览器响应 `success` 字符串表示成功

servlet 中 `deleteByIds()` 方法代码实现如下：

```java
public void deleteByIds(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
    //1. 接收数据 json  [1,2,3]
    BufferedReader br = request.getReader();
    String params = br.readLine();//json字符串
    //转为 int[]
    int[] ids = JSON.parseObject(params, int[].class);
    //2. 调用service添加
    brandService.deleteByIds(ids);
    //3. 响应成功的标识
    response.getWriter().write("success");
}
```

### 6.2  前端实现

此功能的前端代码实现稍微有点麻烦，分为以下几步实现

#### 6.2.1  获取选中的id值

<img src="D:/download/downloadFromMicsoft/day14-综合案例/ppt/assets/image-20210826223103884.png" alt="image-20210826223103884" style="zoom:70%;" />

从上图可以看出表格复选框绑定了一个 `selection-change` 事件，该事件是当选择项发生变化时会触发。该事件绑定了 `handleSelectionChange` 函数，而该函数有一个参数 `val` ，该参数是获取选中行的数据，如下

<img src="D:/download/downloadFromMicsoft/day14-综合案例/ppt/assets/image-20210826223750518.png" alt="image-20210826223750518" style="zoom:70%;" />

而只需要将所有选中数据的id值提交给服务端即可，获取id的逻辑书写在 `批量删除` 按钮绑定的函数中。

在 `批量删除` 按钮绑定单击事件，并给绑定触发时调用的函数，如下

<img src="D:/download/downloadFromMicsoft/day14-综合案例/ppt/assets/image-20210826224121445.png" alt="image-20210826224121445" style="zoom:70%;" />

并在Vue对象中的 methods 中定义 `deleteByIds()` 函数，在该函数中从 `multipleSelection` 数据模型中获取所选数据的id值。要完成这个功能需要在 Vue 对象中定义一个数据模型 `selectedIds:[]`，在 `deleteByIds()` 函数中遍历 `multipleSelection` 数组，并获取到每一个所选数据的id值存储到 `selectedIds` 数组中，代码实现如下：

```js
//1. 创建id数组 [1,2,3], 从 this.multipleSelection 获取即可
for (let i = 0; i < this.multipleSelection.length; i++) {
    let selectionElement = this.multipleSelection[i];
    this.selectedIds[i] = selectionElement.id;
}
```

#### 6.2.2  发送异步请求

使用 axios 发送异步请求并经上一步获取到的存储所有的 id 数组作为请求参数

```js
//2. 发送AJAX请求
var _this = this;

// 发送ajax请求，添加数据
axios({
    method:"post",
    url:"http://localhost:8080/brand-case/brand/deleteByIds",
    data:_this.selectedIds
}).then(function (resp) {
    if(resp.data == "success"){
        //删除成功
        // 重新查询数据
        _this.selectAll();
        // 弹出消息提示
        _this.$message({
            message: '恭喜你，删除成功',
            type: 'success'
        });
    }
})
```

#### 6.2.3  确定框实现

由于删除操作是比较危险的；有时候可能是由于用户的误操作点击了 `批量删除` 按钮，所以在点击了按钮后需要先给用户确认提示。而确认框在 `elementUI` 中也提供了，如下图

![image-20210826225742852](D:/download/downloadFromMicsoft/day14-综合案例/ppt/assets/image-20210826225742852.png)

而在点击 `确定` 按钮后需要执行之前删除的逻辑。因此前端代码实现如下：

```js
 // 批量删除
deleteByIds(){
    // 弹出确认提示框
    this.$confirm('此操作将删除该数据, 是否继续?', '提示', {
        confirmButtonText: '确定',
        cancelButtonText: '取消',
        type: 'warning'
    }).then(() => {
        //用户点击确认按钮
        //1. 创建id数组 [1,2,3], 从 this.multipleSelection 获取即可
        for (let i = 0; i < this.multipleSelection.length; i++) {
            let selectionElement = this.multipleSelection[i];
            this.selectedIds[i] = selectionElement.id;
        }
        //2. 发送AJAX请求
        var _this = this;
        // 发送ajax请求，添加数据
        axios({
            method:"post",
            url:"http://localhost:8080/brand-case/brand/deleteByIds",
            data:_this.selectedIds
        }).then(function (resp) {
            if(resp.data == "success"){
                //删除成功
                // 重新查询数据
                _this.selectAll();
                // 弹出消息提示
                _this.$message({
                    message: '恭喜你，删除成功',
                    type: 'success'
                });
            }
        })
    }).catch(() => {
        //用户点击取消按钮
        this.$message({
            type: 'info',
            message: '已取消删除'
        });
    });
}
```

## 7，分页查询

之前做的 `查询所有` 功能中将数据库中所有的数据查询出来并展示到页面上，试想如果数据库中的数据有很多（假设有十几万条）的时候，将数据全部展示出来肯定不现实，那如何解决这个问题呢？几乎所有的网站都会使用分页解决这个问题。每次只展示一页的数据，比如一页展示10条数据，如果还想看其他的数据，可以通过点击页码进行查询

![image-20210826230648031](D:/download/downloadFromMicsoft/day14-综合案例/ppt/assets/image-20210826230648031.png)

### 7.1  分析

#### 7.1.1  分页查询sql

分页查询也是从数据库进行查询的，所以要分页对应的SQL语句应该怎么写。分页查询使用 `LIMIT` 关键字，格式为：==`LIMIT 开始索引 每页显示的条数`==。以后前端页面在发送请求携带参数时，它并不明确开始索引是什么，但是它知道查询第几页。所以 `开始索引` 需要在后端进行计算，计算的公式是 ：==开始索引 = （当前页码 -  1）*  每页显示条数==

比如查询第一页的数据的 SQL 语句是：

```
select * from tb_brand  limit 0,5;
```

查询第二页的数据的 SQL 语句是：

```
select * from tb_brand  limit 5,5;
```

查询第三页的数据的 SQL 语句是：

```
select * from tb_brand  limit 10,5;
```

#### 7.1.2  前后端数据分析

分页查询功能时候比较复杂的，所以要先分析清楚以下两个问题：

* **前端需要传递什么参数给后端**

  根据上一步对分页查询 SQL 语句分析得出，前端需要给后端两个参数

  * 当前页码 ： currentPage
  * 每页显示条数：pageSize

* **后端需要响应什么数据给前端**

  <img src="D:/download/downloadFromMicsoft/day14-综合案例/ppt/assets/image-20210826231842293.png" alt="image-20210826231842293" style="zoom:80%;" />

  上图是分页查询页面展示的效果，从上面可以看出需要响应以下联股份数据

  * 当前页需要展示的数据。在后端一般会存储到 List 集合中
  * 总共记录数。在上图页面中需要展示总的记录数，所以这部分数据也需要。总的页面 elementUI 的分页组件会自动计算，不需要关心

  而这两部分需要封装到 PageBean 对象中，并将该对象转换为 json 格式的数据响应回给浏览器

  ！！！！！！！！

  思路就是这么来的，前端交给后端什么数据，后端交给前端什么数据

  才能总体设计

  <img src="D:/download/downloadFromMicsoft/day14-综合案例/ppt/assets/image-20210826232158234.png" alt="image-20210826232158234" style="zoom:65%;" />



通过上面的分析需要先在 `pojo` 包下创建 `PageBean` 类，为了做到通过会将其定义成泛型类，代码如下：

```java
//分页查询的JavaBean
public class PageBean<T> {
    // 总记录数
    private int totalCount;
    // 当前页数据
    private List<T> rows;


    public int getTotalCount() {
        return totalCount;
    }

    public void setTotalCount(int totalCount) {
        this.totalCount = totalCount;
    }

    public List<T> getRows() {
        return rows;
    }

    public void setRows(List<T> rows) {
        this.rows = rows;
    }
}
```

#### 7.1.3  流程分析

后端需要响应`总记录数` 和 `当前页的数据` 两部分数据给前端，所以在 `BrandMapper`  接口中需要定义两个方法：

* selectByPage() ：查询当前页的数据的方法
* selectTotalCount() ：查询总记录的方法

整体流程如下：

![image-20210826232620404](D:/download/downloadFromMicsoft/day14-综合案例/ppt/assets/image-20210826232620404.png)

### 7.2  后端实现

#### 7.2.1  dao方法实现

在 `BrandMapper` 接口中定义 `selectByPage()` 方法进行分页查询，代码如下：

```java
/**
     * 分页查询
     * @param begin
     * @param size
     * @return
     */
@Select("select * from tb_brand limit #{begin} , #{size}")
@ResultMap("brandResultMap")
List<Brand> selectByPage(@Param("begin") int begin,@Param("size") int size);
```

在 `BrandMapper` 接口中定义 `selectTotalCount()` 方法进行统计记录数，代码如下：

```java
/**
     * 查询总记录数
     * @return
     */
@Select("select count(*) from tb_brand ")
int selectTotalCount();
```

#### 7.2.2  service方法实现

在 `BrandService` 接口中定义 `selectByPage()` 分页查询数据的业务逻辑方法

```java
/**
     * 分页查询
     * @param currentPage  当前页码
     * @param pageSize   每页展示条数
     * @return
     */
    PageBean<Brand>  selectByPage(int currentPage,int pageSize);
```

在 `BrandServiceImpl` 类中重写 `selectByPage()` 方法，并进行业务逻辑实现

```java
@Override
public PageBean<Brand> selectByPage(int currentPage, int pageSize) {
    //2. 获取SqlSession对象
    SqlSession sqlSession = factory.openSession();
    //3. 获取BrandMapper
    BrandMapper mapper = sqlSession.getMapper(BrandMapper.class);
    //4. 计算开始索引
    int begin = (currentPage - 1) * pageSize;
    // 计算查询条目数
    int size = pageSize;
    //5. 查询当前页数据
    List<Brand> rows = mapper.selectByPage(begin, size);
    //6. 查询总记录数
    int totalCount = mapper.selectTotalCount();
    //7. 封装PageBean对象
    PageBean<Brand> pageBean = new PageBean<>();
    pageBean.setRows(rows);
    pageBean.setTotalCount(totalCount);

    //8. 释放资源
    sqlSession.close();
    return pageBean;
}
```

#### 7.2.3  servlet实现

在 `BrandServlet` 类中定义 `selectByPage()`  方法。而该方法的逻辑如下：

* 获取页面提交的 `当前页码` 和 `每页显示条目数` 两个数据。这两个参数是在url后进行拼接的，格式是  `url?currentPage=1&pageSize=5`。获取这样的参数需要使用 `requet.getparameter()` 方法获取。
* 调用 service 的 `selectByPage()` 方法进行分页查询的业务逻辑处理
* 将查询到的数据转换为 json 格式的数据
* 响应 json 数据

servlet 中 `selectByPage()` 方法代码实现如下：

```java
public void selectByPage(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
    //1. 接收 当前页码 和 每页展示条数    url?currentPage=1&pageSize=5
    String _currentPage = request.getParameter("currentPage");
    String _pageSize = request.getParameter("pageSize");

    int currentPage = Integer.parseInt(_currentPage);
    int pageSize = Integer.parseInt(_pageSize);

    //2. 调用service查询
    PageBean<Brand> pageBean = brandService.selectByPage(currentPage, pageSize);

    //2. 转为JSON
    String jsonString = JSON.toJSONString(pageBean);
    //3. 写数据
    response.setContentType("text/json;charset=utf-8");
    response.getWriter().write(jsonString);
}
```

#### 7.2.4  测试

在浏览器上地址栏输入 `http://localhost:8080/brand-case/brand/selectByPage?currentPage=1&pageSize=5` ，查询到以下数据

![image-20210828184610060](D:/download/downloadFromMicsoft/day14-综合案例/ppt/assets/image-20210828184610060.png)

### 7.3  前端实现

#### 7.3.1  selectAll 代码改进

`selectAll()` 函数之前是查询所有数据，现需要改成分页查询。 请求路径应改为 `http://localhost:8080/brand-case/brand/selectByPage?currentPage=1&pageSize=5` ，而 `currentPage`  和 `pageSize`  是需要携带的参数，分别是 当前页码 和 每页显示的条目数。

 刚才对后端代码进行测试可以看出响应回来的数据，所以在异步请求的成功回调函数（`then` 中的匿名函数）中给页面表格的数据模型赋值 `_this.tableData = resp.data.rows;`。整体代码如下

```js
var _this = this;
axios({
    method:"post",
    url:"http://localhost:8080/brand-case/brand/selectByPage？currentPage=1&pageSize=5"
}).then(resp =>{
    //设置表格数据
    _this.tableData = resp.data.rows; // {rows:[],totalCount:100}
})
```

响应的数据中还有总记录数，要进行总记录数展示需要在页面绑定数据模型

<img src="D:/download/downloadFromMicsoft/day14-综合案例/ppt/assets/image-20210828185553407.png" alt="image-20210828185553407" style="zoom:70%;" />

> ==注意：该数据模型需要在Vue对象中声明出来。==

那异步请求的代码就可以优化为

```js
var _this = this;
axios({
    method:"post",
    url:"http://localhost:8080/brand-case/brand/selectByPage?currentPage=1&pageSize=5"
}).then(resp =>{
    //设置表格数据
    _this.tableData = resp.data.rows; // {rows:[],totalCount:100}
    //设置总记录数
    _this.totalCount = resp.data.totalCount;
})
```

而页面中分页组件给 `当前页码` 和 `每页显示的条目数` 都绑定了数据模型

<img src="D:/download/downloadFromMicsoft/day14-综合案例/ppt/assets/image-20210828191752872.png" alt="image-20210828191752872" style="zoom:80%;" />

所以 `selectAll()` 函数中发送异步请求的资源路径中不能将当前页码和 每页显示条目数写死，代码就可以优化为

```js
var _this = this;
axios({
    method:"post",
    url:"http://localhost:8080/brand-case/brand/selectByPage?currentPage="+this.currentPage+"&pageSize=" + this.pageSize
}).then(resp =>{
    //设置表格数据
    _this.tableData = resp.data.rows; // {rows:[],totalCount:100}
    //设置总记录数
    _this.totalCount = resp.data.totalCount;
})
```

#### 7.3.2  改变每页条目数

<img src="D:/download/downloadFromMicsoft/day14-综合案例/ppt/assets/image-20210828192937340.png" alt="image-20210828192937340" style="zoom:80%;" />

当改变每页显示的条目数后，需要重新发送异步请求。而下图是分页组件代码，`@size-change` 就是每页显示的条目数发生变化时会触发的事件

<img src="D:/download/downloadFromMicsoft/day14-综合案例/ppt/assets/image-20210828193143116.png" alt="image-20210828193143116" style="zoom:80%;" />

而该事件绑定了一个 `handleSizeChange` 函数，整个逻辑如下：

```js
handleSizeChange(val) { //选择的是 ‘5条/页’ 此值就是 5.而选择了 `10条/页` 此值就是 10
    // 重新设置每页显示的条数
    this.pageSize  = val; 
    //调用 selectAll 函数重新分页查询数据
    this.selectAll();
}
```

#### 7.3.3  改变当前页码

当改变页码时，需要重新发送异步请求。而下图是分页组件代码，`@current-change` 就是页码发生变化时会触发的事件

<img src="D:/download/downloadFromMicsoft/day14-综合案例/ppt/assets/image-20210828193713913.png" alt="image-20210828193713913" style="zoom:80%;" />

而该事件绑定了一个 `handleSizeChange` 函数，整个逻辑如下：

```js
handleCurrentChange(val) { //val 就是改变后的页码
    // 重新设置当前页码
    this.currentPage  = val;
    //调用 selectAll 函数重新分页查询数据
    this.selectAll();
}
```

## 8，条件查询

<img src="D:/download/downloadFromMicsoft/day14-综合案例/ppt/assets/image-20210828212019663.png" alt="image-20210828212019663" style="zoom:60%;" />

上图就是用来输入条件查询的条件数据的。要做条件查询功能，先明确以下三个问题

* 3个条件之间什么关系？

  同时满足，所用 SQL 中多个条件需要使用 and 关键字连接

* 3个条件必须全部填写吗？

  不需要。想根据哪儿个条件查询就写那个，所以这里需要使用动态 sql 语句

* 条件查询需要分页吗？

  需要

根据上面三个问题的明确，就可以确定sql语句了：

<img src="D:/download/downloadFromMicsoft/day14-综合案例/ppt/assets/image-20210828213116559.png" alt="image-20210828213116559" style="zoom:70%;" /> 

整个条件分页查询流程如下

![image-20210828224859135](D:/download/downloadFromMicsoft/day14-综合案例/ppt/assets/image-20210828224859135.png)

### 8.1  后端实现

#### 8.1.1  dao实现

在 `BrandMapper` 接口中定义 `selectByPageAndCondition()` 方法 和 `selectTotalCountByCondition` 方法，用来进行条件分页查询功能，方法如下：

```java
/**
     * 分页条件查询
     * @param begin
     * @param size
     * @return
     */
List<Brand> selectByPageAndCondition(@Param("begin") int begin,@Param("size") int size,@Param("brand") Brand brand);

/**
     * 根据条件查询总记录数
     * @return
     */
int selectTotalCountByCondition(Brand brand);
```

参数：

* `begin` 分页查询的起始索引
* `size` 分页查询的每页条目数
* `brand` 用来封装条件的对象

由于这是一个复杂的查询语句，需要使用动态sql；所以在映射配置文件中书写 sql 语句。`brand_name` 字段和 `company_name` 字段需要进行模糊查询，所以需要使用 `%` 占位符。映射配置文件中 statement 书写如下：

```xml
<!--查询满足条件的数据并进行分页-->
<select id="selectByPageAndCondition" resultMap="brandResultMap">
    select *
    from tb_brand
    <where>
        <if test="brand.brandName != null and brand.brandName != '' ">
            and  brand_name like #{brand.brandName}
        </if>

        <if test="brand.companyName != null and brand.companyName != '' ">
            and  company_name like #{brand.companyName}
        </if>

        <if test="brand.status != null">
            and  status = #{brand.status}
        </if>
    </where>
    limit #{begin} , #{size}
</select>

<!--查询满足条件的数据条目数-->
<select id="selectTotalCountByCondition" resultType="java.lang.Integer">
    select count(*)
    from tb_brand
    <where>
        <if test="brandName != null and brandName != '' ">
            and  brand_name like #{brandName}
        </if>

        <if test="companyName != null and companyName != '' ">
            and  company_name like #{companyName}
        </if>

        <if test="status != null">
            and  status = #{status}
        </if>
    </where>
</select>
```

#### 8.1.2  service实现

在 `BrandService` 接口中定义 `selectByPageAndCondition()` 分页查询数据的业务逻辑方法

```java
 /**
     * 分页条件查询
     * @param currentPage
     * @param pageSize
     * @param brand
     * @return
     */
PageBean<Brand>  selectByPageAndCondition(int currentPage,int pageSize,Brand brand);
```

在 `BrandServiceImpl` 类中重写 `selectByPageAndCondition()` 方法，并进行业务逻辑实现

```java
 @Override
    public PageBean<Brand> selectByPageAndCondition(int currentPage, int pageSize, Brand brand) {
        //2. 获取SqlSession对象
        SqlSession sqlSession = factory.openSession();
        //3. 获取BrandMapper
        BrandMapper mapper = sqlSession.getMapper(BrandMapper.class);


        //4. 计算开始索引
        int begin = (currentPage - 1) * pageSize;
        // 计算查询条目数
        int size = pageSize;

        // 处理brand条件，模糊表达式
        String brandName = brand.getBrandName();
        if (brandName != null && brandName.length() > 0) {
            brand.setBrandName("%" + brandName + "%");
        }

        String companyName = brand.getCompanyName();
        if (companyName != null && companyName.length() > 0) {
            brand.setCompanyName("%" + companyName + "%");
        }

        //5. 查询当前页数据
        List<Brand> rows = mapper.selectByPageAndCondition(begin, size, brand);

        //6. 查询总记录数
        int totalCount = mapper.selectTotalCountByCondition(brand);

        //7. 封装PageBean对象
        PageBean<Brand> pageBean = new PageBean<>();
        pageBean.setRows(rows);
        pageBean.setTotalCount(totalCount);

        //8. 释放资源
        sqlSession.close();

        return pageBean;
    
```

> ==注意：brandName 和 companyName 属性值到时候需要进行模糊查询，所以前后需要拼接上 `%`==。

#### 8.1.3  servlet实现

在 `BrandServlet` 类中定义 `selectByPageAndCondition()`  方法。而该方法的逻辑如下：

* 获取页面提交的 `当前页码` 和 `每页显示条目数` 两个数据。这两个参数是在url后进行拼接的，格式是  `url?currentPage=1&pageSize=5`。获取这样的参数需要使用 `requet.getparameter()` 方法获取。

* 获取页面提交的 `条件数据` ，并将数据封装到一个Brand对象中。由于这部分数据到时候是需要以 json 格式进行提交的，所以需要通过流获取数据，具体代码如下：

  ```java
  // 获取查询条件对象
  BufferedReader br = request.getReader();
  String params = br.readLine();//json字符串
  
  //转为 Brand
  Brand brand = JSON.parseObject(params, Brand.class);
  ```

* 调用 service 的 `selectByPageAndCondition()` 方法进行分页查询的业务逻辑处理

* 将查询到的数据转换为 json 格式的数据

* 响应 json 数据

servlet 中 `selectByPageAndCondition()` 方法代码实现如下：

```java
/**
     * 分页条件查询
     * @param request
     * @param response
     * @throws ServletException
     * @throws IOException
     */

public void selectByPageAndCondition(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
    //1. 接收 当前页码 和 每页展示条数    url?currentPage=1&pageSize=5
    String _currentPage = request.getParameter("currentPage");
    String _pageSize = request.getParameter("pageSize");

    int currentPage = Integer.parseInt(_currentPage);
    int pageSize = Integer.parseInt(_pageSize);

    // 获取查询条件对象
    BufferedReader br = request.getReader();
    String params = br.readLine();//json字符串

    //转为 Brand
    Brand brand = JSON.parseObject(params, Brand.class);


    //2. 调用service查询
    PageBean<Brand> pageBean = brandService.selectByPageAndCondition(currentPage,pageSize,brand);

    //2. 转为JSON
    String jsonString = JSON.toJSONString(pageBean);
    //3. 写数据
    response.setContentType("text/json;charset=utf-8");
    response.getWriter().write(jsonString);
}
```

### 8.2  前端实现

前端代码从以下几方面实现：

1. **查询表单绑定查询条件对象模型**

   这一步在页面上已经实现了，页面代码如下：

   <img src="D:/download/downloadFromMicsoft/day14-综合案例/ppt/assets/image-20210828223817324.png" alt="image-20210828223817324" style="zoom:70%;" />

2. **点击查询按钮查询数据**

   <img src="D:/download/downloadFromMicsoft/day14-综合案例/ppt/assets/image-20210828223952142.png" alt="image-20210828223952142" style="zoom:67%;" />

   从上面页面可以看到给 `查询` 按钮绑定了 `onSubmit()` 函数，而在 `onSubmit()` 函数中只需要调用 `selectAll()` 函数进行条件分页查询。

3. **改进 selectAll() 函数**

   子页面加载完成后发送异步请求，需要携带当前页码、每页显示条数、查询条件对象。接下来先对携带的数据进行说明：

   * `当前页码` 和 `每页显示条数` 这两个参数会拼接到 URL 的后面
   * `查询条件对象` 这个参数需要以 json 格式提交给后端程序

   修改 `selectAll()` 函数逻辑为

   ```js
   var _this = this;
   
   axios({
       method:"post",
       url:"http://localhost:8080/brand-case/brand/selectByPageAndCondition?currentPage="+this.currentPage+"&pageSize="+this.pageSize,
       data:this.brand
   }).then(function (resp) {
   
       //设置表格数据
       _this.tableData = resp.data.rows; // {rows:[],totalCount:100}
       //设置总记录数
       _this.totalCount = resp.data.totalCount;
   })
   ```

## 9，前端代码优化

咱们已经将所有的功能实现完毕。而针对前端代码中的发送异步请求的代码，如下

```js
var _this = this;

axios({
    method:"post",
    url:"http://localhost:8080/brand-case/brand/selectByPageAndCondition?currentPage="+this.currentPage+"&pageSize="+this.pageSize,
    data:this.brand
}).then(function (resp) {

    //设置表格数据
    _this.tableData = resp.data.rows; // {rows:[],totalCount:100}
    //设置总记录数
    _this.totalCount = resp.data.totalCount;
})
```

需要在成功的回调函数（也就是`then` 函数中的匿名函数）中使用this，都需要在外边使用 `_this` 记录一下 `this` 所指向的对象；因为在外边的 `this` 表示的是 Vue 对象，而回调函数中的 `this` 表示的不是 vue 对象。这里可以使用 `ECMAScript6` 中的新语法（箭头函数）来简化这部分代码，如上面的代码可以简化为:

```js
axios({
    method:"post",
    url:"http://localhost:8080/brand-case/brand/selectByPageAndCondition?currentPage="+this.currentPage+"&pageSize="+this.pageSize,
    data:this.brand
}).then((resp) => {

    //设置表格数据
    this.tableData = resp.data.rows; // {rows:[],totalCount:100}
    //设置总记录数
    this.totalCount = resp.data.totalCount;
})
```

**箭头函数语法：**

```
(参数) => {
	逻辑代码
}
```

**箭头函数的作用：**

替换（简化）匿名函数。



## 案例感受

黑马老师的优点：写了一个层次的代码就测试有没有出问题，防止最后出BUG！！！

写完全部层再来测试，到时出问题都不知道是哪个层次的问题

