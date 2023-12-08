## Java SE

### 大二下学习预览dor4

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220313102014060.png" alt="image-20220313102014060" style="zoom:67%;" />

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220313103421443.png" alt="image-20220313103421443" style="zoom:67%;" />

JDK编译java代码，编译成.class文件，运行由JRE代理

C:\Users\86178\.jdks\openjdk-17.0.2

### 开发基础配置

#### 1）DOS命令

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220125234322408.png" alt="image-20220125234322408" style="zoom:50%;" />

#### 2）idea结构

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220126163745145.png" alt="image-20220126163745145" style="zoom:50%;" />

### IDEA常用快捷键

![image-20220126123207353](C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220126123207353.png)

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220129150356169.png" alt="image-20220129150356169" style="zoom:67%;" />

- ctrl+x删除，剪切
- Alt同时选中多行
- ctrl+点击 查看代码
- ctrl+r快速同时修改相同代码
- 构建模块、文件，file->project struture
- 重写java接口实现类：alt+enter快速操作
- 方法说明注释：/** + enter
- Ctrl+N按名字搜索类： 全局搜索类（包括自己写的和依赖的）；
- Ctrl+F12 访问当前类中所有的方法
- Ctrl+insert 访问Generate
- 利用鼠标选择一段需要被括号括起来的字符，再在末尾处打上左引号即可
- Ctrl+Shift+N按文件名搜索文件： 与Ctrl + N 一样，只不过是匹配全局所有类型的文件；
- Ctrl+H： 鼠标放在类上，查看类的继承关系；
- Ctrl+Alt+B查看子类方法实现： 鼠标放在类上，ctrl+alt+b；
- Alt+F7： 查找类或方法在哪被使用；
- Ctrl+F/Ctrl+Shift+F： 按照文本的内容查找，不加 shift 代表搜索本类或文件中，加上 shift 代表全局搜索；
- Shift+Shift： 搜索idea中的任何东西；
- 写代码时：跳括号外头： ctrl shift enter
  叫做 Complete Current Statement
  如果后面没关闭，会自动帮你关闭并跳下一行
  如果有关闭了，会跳下一行

### IDEA常用操作

![image-20220317132931012](C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220317132931012.png)  

   导入模块（放在同一个工程下）：

- 先点击当前模块，然后再file-new-创建新模块

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220317133834865.png" alt="image-20220317133834865" style="zoom:50%;" />

- 复制模块的.com，粘贴到新建模块的.com中即可

删除模块：

直接在磁盘中删除即可

### IDEA debug

开启debug后，不可以再添加代码，会忽略添加入的代码，往后执行

原因：已经编译完成，生成了字节码文件，不会再改变java程序

### 导包

不使用maven的导包方式

1. 新建文件夹lib（同src同级即可）
2. 将jar包复制到文件夹
3. jar文件右键，选择 Add as Library ->OK
4. 即可使用

### 结构

#### 1）API文档结构

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220223202409469.png" alt="image-20220223202409469" style="zoom: 67%;" />

#### 2）类结构

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220227232405814.png" alt="image-20220227232405814" style="zoom:150%;" />

### Helloworld案例

编写->编译->运行

编译：

![image-20220125234948484](C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220125234948484.png)

![image-20220125235024572](C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220125235024572.png)

红色框框分别对应编译与运行

javac: 编译的工具产生HelloWorld类

java: 运行java文件

### 注释

![image-20220125235859689](C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220125235859689.png)

### 关键字

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220126000240377.png" alt="image-20220126000240377" style="zoom:50%;" />

### 数据类型

![image-20220126001952689](C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220126001952689.png)

![image-20220126002034877](C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220126002034877.png)

整数默认：int

浮点数默认：double

### 开发的命名规则

模块-》包-》类-》方法

方法名：同变量名一致

![image-20220126002628384](C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220126002628384.png)

包名与module：全部小写

包名：www.xxx.com     将其翻转，即com.xxx.具体意义

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220226104255728.png" alt="image-20220226104255728" style="zoom:67%;" />

文件名同public修饰的类名一致：

- Alt+Shift+Enter,让文件名同类名一致
- Alt+Enter一样有效

### 类型转换

![image-20220126003155185](C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220126003155185.png)

1、自动

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220126003348434.png" alt="image-20220126003348434" style="zoom:50%;" />

2、表达式

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220126003430259.png" alt="image-20220126003430259" style="zoom:50%;" />

应用：

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220126160546104.png" alt="image-20220126160546104" style="zoom:67%;" />

3、强制

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220126003543928.png" alt="image-20220126003543928" style="zoom:50%;" />

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220126003712341.png" alt="image-20220126003712341" style="zoom:50%;" />

### 数值运算

#### 1）获取数各个位的具体数值

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220126003133693.png" alt="image-20220126003133693" style="zoom:50%;" />

#### 2）数据的存储形式——二进制、八进制、十六进制

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220129151919338.png" alt="image-20220129151919338" style="zoom:67%;" />

```
int ib = 0B01100001;
int io = 0141;
int ih = 0x61;
//全部值为97
```

### 运算符

#### 1）逻辑运算符

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220126005728949.png" alt="image-20220126005728949" style="zoom:50%;" />

重点关注：&&和||两种运算符，和c++是一样的

#### 2）运算符优先级

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220126010448727.png" alt="image-20220126010448727" style="zoom:67%;" />

#### 3）位运算符

细节，移动的位数写在右边

| 运算符 | 含义     | 举例      | 规则                                 |
| --- | ------ | ------- | ---------------------------------- |
| <<  | 左移位    | a << 2  | 空位补0，被移除的高位丢弃                      |
| >>  | 右移位    | a >> 2  | 被移位的二进制最高位为0，右移后，空缺位补0；最高位为1，空缺位补1 |
| >>> | 无符号右移位 | a >>> 2 | 被移位二进制最高位无论是0还是1，空缺位都用0补           |

### Scanner键盘录入

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220126011424638.png" alt="image-20220126011424638" style="zoom:50%;" />

### 流程控制语句

#### 1）分支语句

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220126105201366.png" alt="image-20220126105201366" style="zoom: 50%;" />

#### 2）循环语句

for循环：

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220126105654557.png" alt="image-20220126105654557" style="zoom: 50%;" />

while循环：

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220126110113734.png" alt="image-20220126110113734" style="zoom:50%;" />

区别：

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220126110153874.png" alt="image-20220126110153874" style="zoom: 67%;" />

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220126110621742.png" alt="image-20220126110621742" style="zoom: 80%;" />

当不知道循环几次时，用while思维更顺畅

### 跳转控制语句

![image-20220126111516583](C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220126111516583.png)

注意：

break:立即结束当前的循环体，而如果存在循环嵌套，最外层的循环体不被结束

### Random

![image-20220126111035758](C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220126111035758.png)

​                            注意数据【0，10）

### 数组

#### 1）静态数组的写法

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220126162540747.png" alt="image-20220126162540747" style="zoom:67%;" />

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220126162844781.png" alt="image-20220126162844781" style="zoom:67%;" />

在定义中，长度，类型就固定了

二维数组

```java
int[][] direc=new int[][]{{0,1},{0,-1},{-1,0},{1,0}};
```

#### 2）动态数组的写法

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220126162955318.png" alt="image-20220126162955318" style="zoom: 50%;" />

##### a)默认初始化值：

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220126163249180.png" alt="image-20220126163249180" style="zoom: 50%;" />

##### b)非基础数据类型

默认初始化为null

| 法   |      |      |      |      |      |
| ---- | ---- | ---- | ---- | ---- | ---- |
| 法   |      |      |      |      |      |
|      |      |      |      |      |      |
|      |      |      |      |      |      |



#### 3）两者的注意区别

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220126163127522.png" alt="image-20220126163127522" style="zoom:50%;" />

#### 4）案例猜数字

```Java
public static void main(String[] args) {
    int[] data=new int[5];
    Random r=new Random();

    for(int i=0;i<data.length;i++){
        data[i]=r.nextInt(20)+1;
    }
    Scanner sc=new Scanner(System.in);
    out://out代之最外层得循环！！！！！！！！！！！！！！！！！！！
    while (true){
        System.out.println("请输入1-20的数据");
        int guessNumber=sc.nextInt();
        for(int i=0;i<data.length;++i) {
            if (guessNumber == data[i]) {
                System.out.println("您猜中了，且数据索引是"+i);
                break out;
            }

        }
        System.out.println("您没猜中，请重新输入");
    }
    System.out.println("当前数组的数据为");
    for (int i = 0; i < data.length; i++) {
        System.out.print(data[i]+" " );
         //   System.out.print(data[i]+"\t" );！！！！！
    }
}
```

#### 5)案例简单的复制数组

```java
public static void main(String[] args) {
        /**
         *复制数值
         */
        int[] arr1 = new int[10];
        Random r = new Random();
        for (int i = 0; i < 10; i++) {
            arr1[i] = r.nextInt(100);
        }
        int[] arr2 = new int[arr1.length];//length为什么不要括号
        copy(arr1, arr2);
        printArray(arr2);
    }

    public static void printArray(int[] arr) {
        System.out.print("[");
        for (int i = 0; i < arr.length; i++) {
            System.out.print(i == arr.length - 1 ? arr[i] : arr[i] + ",");
        }
        System.out.println("]");//使用println自动换行
    }


    public static void copy(int[] arr1, int[] arr2) {
        for (int i = 0; i < arr1.length; i++) {
            arr2[i] = arr1[i];
        }
    }
```

### 内存分配

![image-20220129113314324](C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220129113314324.png)

![image-20220129113347349](C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220129113347349.png)

**new出来的数据全部都在堆**

对于不同的数据类型分为基本类型内存分配与引用类型内存分配（自己构造类都是）

#### 引用类型

多个对象内存：

<img title="" src="file:///C:/Users/86178/AppData/Roaming/Typora/typora-user-images/image-20220226110302453.png" alt="image-20220226110302453" data-align="inline">

方法先存入方法区，调用时再压入栈；c1变量名存放的是地址，指向堆内存中存储的对象；堆内存中成员方法只有地址

两个变量指向同一个对象：![image-20220226152454349](C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220226152454349.png) 

```java
   LinkedList<Integer> w=new LinkedList<>();
        w.add(1);
        w.add(2);
        w.add(3);
        w.add(4);
        w.add(5);
        LinkedList<Integer> z=new LinkedList<>(w);
//依旧是浅复制，但是开辟出新空间浅复制，也就是说，对于w的操作影响不到z
        LinkedList<Integer> t=w;
```







#### 基本类型

非程序员自己写的数据类型，存放在栈中

#### 局部变量

基本类型传入类中，在栈内存，为深复制，开辟为新的数据

引用类型(new 出来的数据)：传入的数据放入栈内存中

### 方法|函数

#### 1）内存分配

![image-20220129115657932](C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220129115657932.png)

![image-20220129115614123](C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220129115614123.png)

#### 2）参数传递机制

##### a、值传递—基本类型的参数传递

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220129120447237.png" alt="image-20220129120447237" style="zoom: 67%;" />

##### b、引用传递—引用类型的参数传递

![image-20220129120537925](C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220129120537925.png)

```java
change(arrs);//传入地址
//......
void change(int[] arrs)//接受地址
```

本质也是值传递，不过传递的值是指针

#### 3）方法重载

![image-20220129121422209](C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220129121422209.png)

#### 4)方法案例，验证码的编写

```java
 public static String createCode(int n) {
        StringBuilder code = new StringBuilder();
        Random r = new Random();
        for (int i = 0; i < n; i++) {
            int type = r.nextInt(3);//0=2
            switch (type) {
                case 0 -> {//大写字符,A,65
                    char big = (char) (r.nextInt(25) + 65);
                    code.append(big);
                }
                case 1 -> {//小写字符
                    char small = (char) (r.nextInt(25) + 97);
                    code.append(small);
                }
                case 2 -> code.append(r.nextInt(10));
            }
        }

        return code.toString();
    }
```

### print与println

```java
System.out.println();//1、输出；2、换行
System.out.print();//输出
```

### 面向对象—构造器

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220226133859529.png" alt="image-20220226133859529" style="zoom: 80%;" />

注意：

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220226134717414.png" alt="image-20220226134717414" style="zoom:80%;" />

本质上：

- jvm会自动帮组没有构造器的类补一个无参构造器，并且成员变量的数据都是默认值，也就是在堆里创建了一个默认对象
- 手动只要创建构造器，jvm就不会帮忙，因为一旦程序员写的是无参构造，并且jvm也写一个，即存在二义性，不知调用哪个，(猜测，无法jvm无法识别出创建的是有参构造器还是无参构造器)

### 面向对象—this

```java
public class Goods {
    int id;
    public Goods(int id) {
//        id=id；语句出现二义性，不知道谁给谁赋值
    }
}
```

利用this指向类成员变量，访问当前对象的成员变量

### 面向对象—JavaBean

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220226144040655.png" alt="image-20220226144040655" style="zoom: 67%;" />

写法：

- private:Alt统一加private
- set/get:  Genater->Getter and Setter->shift全选
- 无参构造：Genater->construct->select none

idea:

实际开发中无参构造更重要，有参构造是不断迭代出来的

```Java
public class user {//alt+shift+enter
    //1、 成员变量私有
    private String name;
    private double height;
    private double salary;

    //3、提供无参构造函数
    public user() {
    }

    //4、有参构造（可有可无）
    public user(String name, double height, double salary) {
        this.name = name;
        this.height = height;
        this.salary = salary;
    }

    //2、提供get与set函数
    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public double getHeight() {
        return height;
    }

    public void setHeight(double height) {
        this.height = height;
    }

    public double getSalary() {
        return salary;
    }

    public void setSalary(double salary) {
        this.salary = salary;
    }
}
```

### 常用API

#### String

##### 1）构造方式

- 字面量    “”

- new
  
  <img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220226163251428.png" alt="image-20220226163251428" style="zoom:67%;" />

```java
 byte[] by=new byte[]{55,90,97,65}
 String str4=new String(by);
 char[] ch=new char[]{'w','z','t'}
 String str5=new String(ch);
 System.out.println(str4);
 System.out.println(str5);
 /*
 7ZaA
 wzt
 */
```

##### 2）浅析底层

```java
 public static void main(String[] args) {
        String str1 = "abc";
        String str2 = "abc";
        String str3 = new String("abc");
        System.out.println(str1 == str2);
        System.out.println(str2 == str3);
/*
打印结果
 true
false
*/


    }
```

string被称为不可变字符串类型，对象在创建后不能被更改,即存放在字符串常量池中，可以提供多个变量引用，所以不允许更改

- 字面量构造，实际对象存放在堆的字符串常量池中

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220226154419094.png" alt="image-20220226154419094" style="zoom:67%;" />

- 计算操作：“传智”+“教育”=“传智教育”，本质上string对象“传智”没有被更改
  
  new操作，与+操作，在常量池与推中都创建了数据，赋予的是堆数据。==比较的是地址，重写equal方法，比较内容，才会出现true
  
  只要不是“”直接给出，都是堆内存中的
  
  **最后栈中变量名获得的都是堆内存中字符串的引用，而非字符串常量池中的引用**

特殊的java存在编译优化

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220226165557053.png" alt="image-20220226165557053" style="zoom:67%;" />

.java文件

```java
String s1="abc";
String s2="ab";
String s3=s2+"c";
System.out.println(s1==s3);
String s4="abc";
String s5="a"+"b"+"c";
System.out.println(s4==s5);
```

.class文件(编译优化)

```java
  String s1 = "abc";
  String s2 = "ab";
  String s3 = s2 + "c";
  System.out.println(s1 == s3);
  String s4 = "abc";
  String s5 = "abc";
  System.out.println(s4 == s5);
```

s5直接被编译优化，但是变量要到运行时分配空间

##### 3）常用

字符串一定要用equal来进行比较

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220226171200470.png" alt="image-20220226171200470" style="zoom:67%;" />

- equal:只关心变量的内容是否一致，忽略变量名引用的地址差异问题
- 基本数据类型也还是用==

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220226171837907.png" alt="image-20220226171837907" style="zoom:67%;" />

```java
//       1、获取长度
        String name = "时间是important";
        System.out.println(name.length());
//       2、获取每个字符
        System.out.println(name.charAt(2));
        for (int i = 0; i < name.length(); i++) {
            System.out.print(name.charAt(i));
        }
//       3、转换字符串数组
        char[] chas = name.toCharArray();
        for (int i = 0; i < chas.length; i++) {
            System.out.println(chas[i]);
        }
//       4、截取子串（包前不包后）
        System.out.println(name.substring(0, 2));//0,1
//       5、截取到末尾
        System.out.println(name.substring(2));
//       6、精准替代（不改变原字符串）
        System.out.println(name.replace("时间", "金钱"));
        System.out.println(name);
//       7、查询包含
        System.out.println(name.contains("im"));
//       8、判断开始的字符
        System.out.println(name.startsWith("时间"));
//       9、切割（按字符串）
        String team="wzt,wlq,yyc";
        String[] teams=team.split(",");
        for (int i = 0; i < teams.length; i++) {
            System.out.println(teams[i]);
        }
```

- 2中获取每个字符，不可以用下标访问

#### ArrayList

##### 1）构造

常用的泛型：

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220226202316169.png" alt="image-20220226202316169" style="zoom:67%;" />

非泛型：

```java
ArrayList al=new ArrayList();
```

什么数据都要存储：

```java
ArrayList<object> al=new ArrayList<>();
```

##### 2）常用

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220226202433807.png" alt="image-20220226202433807" style="zoom:50%;" />

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220226202240421.png" alt="image-20220226202240421" style="zoom:50%;" />

```java
   public static void main(String[] args) {
        ArrayList<String> al = new ArrayList<>();
        al.add("Java");
        al.add("wzt");
        al.add("xiaoyang");
        al.add("Java");
        al.add("isworkinghard");
//      1、获取索引元素
        String mn=al.get(2);
        System.out.println(mn);
//      2、获取大小
        System.out.println(al.size());
//      3、遍历集合
        System.out.println(al);
//      4、remove(int index),返回索引上的元素
        System.out.println(al.remove(1));
//      5、remove(object),返回删除是否成功,同类元素删除前面的
        System.out.println(al.remove("wzt"));
        al.remove("Java");
        System.out.println(al);
//      6、修改索引位置元素
        al.set(0,"wzt");
        System.out.println(al);
    }
```

#### Object

| 方法名                             | 说明                                        |
| ------------------------------- | ----------------------------------------- |
| public String toString()        | 默认是返回当前对象在堆内存中的地址信息:类的全限名@内存地址            |
| public boolean equals(Object o) | 默认是比较当前对象与另一个对象的地址是否相同，相同返回true，不同返回false |

toString():

- 开发中直接输出对象，默认输出对象的地址其实是毫无意义的。
- 开发中输出对象变量，更多的时候是希望看到对象的内容数据而不是对象的地址信息。
- Object的toString方法的作用是:让子类重写，以便返回子类对象的内容。

equals

- 默认是与另一个对象比较地址是否一样
- 让子类重写，以便比较2个子类对象的内容是否相同

```java
public class api_object {
    public static void main(String[] args) {
        String s1=null;
        String s2=new String("加油，今天要看到线程");
//        System.out.println(s1.equals(s2));//程序崩溃
        System.out.println(Objects.equals(s1,s2));//没有问题输出false
//        Objects.equals原因，判断输入对象是否为空，再调用子类本身的equals方法，即String中的equal方法
      /*  public static boolean equals(Object a, Object b) {
            return (a == b) || (a != null && a.equals(b));
        }*/
        Student w=new Student("wzt",'男',20);
        Student c=new Student("wzt",'男',20);
        Student l=null;
        System.out.println(l);
        System.out.println(w.toString());
        System.out.println(w.equals(c));
    }
}
```

- 类中自带equals，如String,使用 Objects.equals,（利用了类中自带的比较内容的equals,即默认比较的不是地址）加了判断空
- 自写类要重写equals，因为Objects.equals默认比较的是地址（源码很明白，在上面），实际中要比较内容
- 开发中用idea写的即可

```java
/*  @Override
  public boolean equals(Object o) {
      if (this == o) return true;
      if (o == null || getClass() != o.getClass()) return false;
      Student student = (Student) o;
      return sex == student.sex && age == student.age && Objects.equals(name, student.name);
  }*/
  @Override
  public boolean equals(Object o) {
      if(o instanceof Student){//判断了O是否属于Student,包含对O空值的判断
          //必须强转才能访问Student独有的属性
          Student s2=(Student) o;
          return this.age==s2.age&&
                  this.sex==s2.sex&&
                  this.name.equals(s2.name);
      }else{
          return false;
      }
  }
```

#### StringBuilder

| 方法名称                              | 说明                                       |
| --------------------------------- | ---------------------------------------- |
| public StringBuilder append(任意类型) | 添加数据并返回StringBuilder对象本身                 |
| public StringBuilder reverse()    | 将对象的内容反转                                 |
| public int length()               | 返回对象内容长度                                 |
| public String toString()          | 通过toString()就可以实现把StringBuilder转换为String |

- 定义字符串使用String
- 拼接、修改等操作字符串使用StringBuilder

##### 底层内存比较

+的原理就是使用一次StringBuilder再跳回String

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220305163104144.png" alt="image-20220305163104144" style="zoom:67%;" />

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220305163147969.png" alt="image-20220305163147969" style="zoom:67%;" />

- String ：内容是不可变的、拼接字符串性能差。大量内存弃用
- StringBuilder：内容是可变的、拼接字符串性能好、代码优雅
- StringBuilder的API接口返回this指针，支持链式访问

##### 拼接数组案例

```java
public class test02 {
    public static void main(String[] args) {
        int[] arr=new int[]{10,20,30};
        int[] str=new int[]{};
        System.out.println(toString(arr));
        System.out.println(toString(str));
    }
    public static String toString(int[] str){
        if(str !=null){
            StringBuilder sb=new StringBuilder("[");
            for (int i = 0; i < str.length; i++) {
                sb.append(str[i]).append(i== str.length-1?"":",");
                //不能写成"]",","
            }
            sb.append("]");
            return sb.toString();
        }else{
            return null;
        }
    }
}
```

#### Math

| 方法名                                         | 说明                         |
| ------------------------------------------- | -------------------------- |
| public static int abs(int a)                | 获取参数绝对值                    |
| public static double  ceil(double a)        | 向上取整                       |
| public static double  floor(double a)       | 向下取整                       |
| public static int round(float a)            | 四舍五入                       |
| public static int max(int a,int b)          | 获取两个int值中的较大值              |
| public static double pow(double a,double b) | 返回a的b次幂的值                  |
| public static double random()               | 返回值为double的随机值，范围[0.0,1.0) |

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220305165445827.png" alt="image-20220305165445827" style="zoom:67%;" />

#### System

| 方法名                                                           | 说明                        |
| ------------------------------------------------------------- | ------------------------- |
| public  static void exit(int status)                          | 终止当前运行的 Java 虚拟机，非零表示异常终止 |
| public  static long currentTimeMillis()                       | 返回当前系统的时间毫秒值形式            |
| public  static void arraycopy(数据源数组, 起始索引, 目的地数组, 起始索引, 拷贝个数) | 数组拷贝  //不必记忆，直接点进去看看      |

#### BigDecimal

用于解决浮点型运算精度失真的问题，只能做jing'du

| 方法名                                                  | 说明  |
| ---------------------------------------------------- | --- |
| public BigDecimal add(BigDecimal b)                  | 加法  |
| public BigDecimal subtract(BigDecimal b)             | 减法  |
| public BigDecimal multiply(BigDecimal b)             | 乘法  |
| public BigDecimal divide(BigDecimal b)               | 除法  |
| public BigDecimal divide (另一个BigDecimal对象，精确几位，舍入模式) | 除法  |

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220305171913900.png" alt="image-20220305171913900" style="zoom: 67%;" />

#### 日期与时间

##### Date

获取的是系统时间，可用直接手动更改时间

常用构造器

```java
Date d=new Date();//1、无参构造
Date(long date)/*   2、分配一个 Date对象，并将其初始化为表示从标准基准时间（称为“时代”）即1970年1月1日00:00:00 GMT起的指定毫秒数。
//        参数
//        date - 1970年1月1日00:00:00 GMT以来的毫秒数*/
```

常见方法

```java
public long getTime();
public void setTime(long time);
```

以下的太啰嗦

1、日期对象如何创建，如何获取时间毫秒值？

public Date();

public long getTime();

2、时间毫秒值怎么恢复成日期对象

public Date(long time);

public void setTime(long time);

```java
    Date d=new Date();
//      输出易于阅读的时间
        System.out.println(d);
//      获取毫秒值，两种
        long time=d.getTime();
        System.out.println(time);

        long time2=System.currentTimeMillis();
        System.out.println(time2);
//      将毫秒值转换为可读时间,两种
        System.out.println(new Date(time2));
        d.setTime(time2);
        System.out.println(d);
```

输出:CST代表中国时区

```java
Mon Mar 21 12:57:38 CST 2022
1647838658359
1647838658385
Mon Mar 21 12:57:38 CST 2022
Mon Mar 21 12:57:38 CST 2022
```

##### SimpleDateFormat

目的：将时间变为用户亲切的时间格式，即时间格式化的工具

构造方法

| 构造器                                     | 说明                           |
| --------------------------------------- | ---------------------------- |
| public SimpleDateFormat(String pattern) | 构造一个SimpleDateFormat，使用指定的格式 |

常见的时间格式

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220321131800978.png" alt="image-20220321131800978" style="zoom:67%;" />

- EEE：星期几

- a:上下午

方法：

| 格式化方法                                       | 说明                |
| ------------------------------------------- | ----------------- |
| public final String **format(Date date)**   | 将日期格式化成日期/时间字符串   |
| public final String **format(Object time)** | 将时间毫秒值式化成日期/时间字符串 |

| 解析方法                                 | 说明                 |
| ------------------------------------ | ------------------ |
| public Date **parse(String source)** | 从给定字符串的开始解析文本以生成日期 |

```java
       Date d=new Date();
        System.out.println(d);
//        构造方法
        SimpleDateFormat s=new SimpleDateFormat("YYYY年MM月dd HH:mm:ss EEE a");
//      方法一
        System.out.println(s.format(d));
//      方法二：解析时间，任务，将拿到的string  2020年7月8号 17：30：00时间转化 毫秒值
        SimpleDateFormat time=new SimpleDateFormat("YYYY年MM月dd号 HH:mm:ss");
       Date d2=time.parse("2020年07月08号 17:30:00");
        System.out.println(d2);
        System.out.println(d2.getTime());
```

##### Calendar

- Calendar代表了系统此刻日期对应的日历对象。
- Calendar是一个抽象类，不能直接创建对象，通过调用静态方法，静态方法中new子类对象，创造出对象

构造方法

```java
public static Calendar getInstance();
```

方法

| 方法名                                   | 说明             |
| ------------------------------------- | -------------- |
| public int get(int field)             | 取日期中的某个字段信息。   |
| public void set(int field,int value)  | 修改日历的某个字段信息。   |
| public void add(int field,int amount) | 为某个字段增加/减少指定的值 |
| public final Date getTime()           | 拿到此刻日期对象。      |
| public long getTimeInMillis()         | 拿到此刻时间毫秒值      |

```java
  Calendar cal=Calendar.getInstance();
        System.out.println(cal);
//       get(int)细节的month要+1
        int year=cal.get(Calendar.YEAR);
        int month=cal.get(Calendar.MONTH)+1;
        System.out.println(month);
//       输出系统的当前时间
        System.out.println(cal.getTime());
```

输出

```java
java.util.GregorianCalendar[time=1647843875640,areFieldsSet=true,areAllFieldsSet=true,lenient=true,zone=sun.util.calendar.ZoneInfo[id="Asia/Shanghai",offset=28800000,dstSavings=0,useDaylight=false,transitions=31,lastRule=null],firstDayOfWeek=1,minimalDaysInFirstWeek=1,ERA=1,YEAR=2022,MONTH=2,WEEK_OF_YEAR=13,WEEK_OF_MONTH=4,DAY_OF_MONTH=21,DAY_OF_YEAR=80,DAY_OF_WEEK=2,DAY_OF_WEEK_IN_MONTH=3,AM_PM=1,HOUR=2,HOUR_OF_DAY=14,MINUTE=24,SECOND=35,MILLISECOND=640,ZONE_OFFSET=28800000,DST_OFFSET=0]
3
Mon Mar 21 14:24:35 CST 2022
```

##### JDK8新增日期类

- LocalDate：不包含具体时间的日期。
- LocalTime：不含日期的时间。
- LocalDateTime：包含了日期及时间。
- Instant：代表的是时间戳。(不重要)
- DateTimeFormatter 用于做时间的格式化和解析的
- Duration:用于计算两个“时间”间隔
- Period:用于计算两个“日期”间隔

在代码中查看实际运用

[D:\download\downloadFromMicsoft\day14-常用API（常用API、正则表达式、Lambda、算法）\代码\api-lambda-app\src\com\itheima\d4_jdk8_time](D:\download\downloadFromMicsoft\day14-常用API（常用API、正则表达式、Lambda、算法）\代码\api-lambda-app\src\com\itheima\d4_jdk8_time)

#### Arrays

工具类，针对数组提供排序与二分查找方法

```java
// 目标：学会使用Arrays类的常用API ,并理解其原理
int[] arr = {10, 2, 55, 23, 24, 100};
System.out.println(arr);

// 1、返回数组内容的 toString(数组)


System.out.println(Arrays.toString(arr));

// 2、排序的API(默认自动对数组元素进行升序排序)
Arrays.sort(arr);
System.out.println(Arrays.toString(arr));

// 3、二分搜索技术（前提数组必须排好序才支持，否则出bug）
int index = Arrays.binarySearch(arr, 55);
System.out.println(index);

// 返回不存在元素的规律： - （应该插入的位置索引 + 1）
int index2 = Arrays.binarySearch(arr, 22);
System.out.println(index2);


// 注意：数组如果没有排好序，可能会找不到存在的元素，从而出现bug!!
int[] arr2 = {12, 36, 34, 25 , 13,  24,  234, 100};
System.out.println(Arrays.binarySearch(arr2 , 36));
```

自定义构造器

- 左边数据大于右边数据返回正**整数** ，记忆：男左女右，左边更大是正的
- 左边数据小于右边数据返回负**整数**
- 等于返回0
- 只能操作储存引用类型元素的数组
- 对于浮点数，用特定的方法

```java
Arrays.sort(ages1, new Comparator<Integer>() {
            @Override
            public int compare(Integer o1, Integer o2) {
                // 指定比较规则。
//                if(o1 > o2){
//                    return 1;
//                }else if(o1 < o2){
//                    return -1;
//                }
//                return 0;
                // return o1 - o2; // 默认升序
                return o2 - o1; //  降序
            }
        });
        System.out.println(Arrays.toString(ages1));

        System.out.println("-------------------------");
        Student[] students = new Student[3];
        students[0] = new Student("吴磊",23 , 175.5);
        students[1] = new Student("谢鑫",18 , 185.5);
        students[2] = new Student("王亮",20 , 195.5);
        System.out.println(Arrays.toString(students));

        // Arrays.sort(students);  // 直接运行奔溃
        Arrays.sort(students, new Comparator<Student>() {
            @Override
            public int compare(Student o1, Student o2) {
                // 自己指定比较规则
                // return o1.getAge() - o2.getAge(); // 按照年龄升序排序！
                // return o2.getAge() - o1.getAge(); // 按照年龄降序排序！！
                // return Double.compare(o1.getHeight(), o2.getHeight()); // 比较浮点型可以这样写 升序
                return Double.compare(o2.getHeight(), o1.getHeight()); // 比较浮点型可以这样写  降序
            }
        });
        System.out.println(Arrays.toString(students));
```

### 数据结构

#### 集合

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220322180043243.png" alt="image-20220322180043243" style="zoom:67%;" />

- 初步认知：ArrayList底层使用数组实现，LinkedList使用双链表实现
- List,set也是接口
- 注意：集合和泛型都只能支持引用数据类型，不支持基本数据类型，所以集合中存储的元素都认为是对象
- collection没有支持索引的API

1.collection的通用文档(collection)

  [collection的API](D:\Project\Java\JavaSe_Code\base_study\src\com\example\collection)

常用API与迭代器的查询操作

2.ArrayList的API（ListDemo1、2）

常用API

遍历

### Static

#### 1）静态成员变量

- 内存：内存加载在堆区
- 使用目的：同类对象要共用数据
- 初始化：静态成员变量同实例成员变量一样，没有初始化就采用数据类型对应的默认值
- 访问：类名.静态成员变量；同类可以直接通过名访问

![image-20220227221640922](C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220227221640922.png)

```java
public class User {

        public static int onLineNumber=0;//初始化,如果没有手动初始化，static变量默认为该数据类型下的默认值
        private String name;
        private int age=30;

        public static void main(String[] args) {
                User.onLineNumber++;
                System.out.println(onLineNumber++);//访问权限
                User u1=new User();
                u1.name="wzt";
                u1.age=20;
                System.out.println(u1.name);
                System.out.println(u1.age);
                u1.onLineNumber++;//并不欢迎这样使用
                System.out.println(onLineNumber);
        }
}
class Good{
        public static void main(String[] args) {
//               没有 onLineNumber的访问权限
        }
}
```

#### 2）静态成员方法

- 内存：暴露在方法区,同main一同加载入方法区

- 目的：类的通用功能

- 访问：类.方法，类和对象共享的
  
  <img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220227224951200.png" alt="image-20220227224951200" style="zoom:67%;" />
  
  ```java
  public class test02 {
      private String name;
      public void study() {
          System.out.println(name + "在卷");
      }
      public static int getMax(int a, int b) {
          return Math.max(a, b);
  //        name="wzt";不可以访问类内的需要实例化的成员变量，原因参照内存
      }
  
      public static void main(String[] args) {
  //      1、访问
  //      同时属于类与对象
          System.out.println(test02.getMax(10,2));
          System.out.println(getMax(30,2));//同类访问可以省略
  //      2、对象.实例成员方法
          test02 s=new test02();
          s.name="wzt";
          s.study();
      }
  }
  ```

#### 3）工具类

![image-20220227230815917](C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220227230815917.png)

- 不直接写全局方法，用类包含方法类似于用文件夹包含文件，同质工具方法放在同一个工具类中即可
- 私有化构造器，不创建对象，节省内存
- 工具类中全是static方法

```java
/**
 * 工具类
 */
public class ArrayUtils {
    private ArrayUtils() {
    }
    public static String toString(int[] arr) {
        String result = "[";
        for (int i = 0; i < arr.length; i++) {
            result +=(i == arr.length - 1 ? arr[i]+"]": arr[i] + "，");
        }
        return result;
    }
}
```

```java
public class test03 {
    public static void main(String[] args) {
        int[] arr=new int[]{1,2,3};
        System.out.println(ArrayUtils.toString(arr));
    }
}
```

#### 4）代码块

**代码块分为**

a）**静态代码块**:

- **格式**：static{}
- **特点**：需要通过static关键字修饰，随着类的加载而加载，并且自动触发、只执行一次
- **使用场景**：在类加载的时候做一些静态成员变量初始化的操作，以便后续使用。（不初始化实例成员变量，需要先创造实例对象）

b)**构造代码块**（**了解，用的少**）：

- **格式**：{}
- **特点**：每次创建对象，调用构造器执行时，都会执行该代码块中的代码，并且在构造器执行前执行
- **使用场景**：初始化实例资源。

```java
 public static ArrayList<String> cards = new ArrayList<>();
//   随着类的加载而自动执行一次
    static {
        String[] colors = {"♠ ", "♥", "♣", "♦"};
        String[] sizes = {"3", "4", "5", "6", "7", "8", "9", "10", "J", "Q", "K", "A", "2"};
        for (int i = 0; i < sizes.length; i++) {
            for (int j = 0; j < colors.length; j++) {
                cards.add(sizes[i] + colors[j]);
            }
        }
        cards.add("小🃏");
        cards.add("大🃏");
    }
    public static void main(String[] args) {
        System.out.println("欢迎来到斗地主" + cards);
        System.out.println(cards.size());
    }
```

#### 5）单例

简单的理解成一个类只有一个实例化对象

要求：

私有化构造函数，并且提供一个静态对象

饿汉单例：需要实例化静态对象

```java
public class SingleInstance1 {
    public static SingleInstance1 Instance=new SingleInstance1();
//私有化构造器
    private SingleInstance1() {
    }
}
```

```java
public class test05 {
    public static void main(String[] args) {
        SingleInstance1 s1 = SingleInstance1.Instance;
        SingleInstance1 s2 = SingleInstance1.Instance;
        System.out.println(s1 == s2);
//      构造器私有化不能再次实例化对象
//      SingleInstance1 s3=new SingleInstance1();
    }
}
```

懒汉单例：不需要实例化对象，私有化静态对象

```java
public class SingleInstance2 {
//    私有化，必须通过getInstance得到
   private static SingleInstance2 Instance;
//    构造器私有
    private SingleInstance2(){
    }
//    暴露对象
    public static SingleInstance2 getInstance(){
        if(Instance==null){
         Instance=new SingleInstance2();
        }
        return Instance;
    }
}
```

区别：懒汉只有需要的时候才实例化单例，节省内存空间

### 继承

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220228203728706.png" alt="image-20220228203728706" style="zoom:80%;" />

getter与setter在idea中自动构造

#### 1）特点

**继承的特点**

①子类可以继承父类的属性和行为（有争议），（private 成员无法被访问，有的人认为没有继承）但是**子类不能继承父类的构造器**。静态成员由于唯一性，所以没有继承只是共享

②Java是单继承模式：一个类只能继承一个直接父类。

③Java不支持多继承、但是支持多层继承。

④Java中所有的类都是Object类的子类。

变量访问：最近原则
方法访问：访问父类需要中转

#### 2）重写父类方法

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220302205524534.png" alt="image-20220302205524534" style="zoom:67%;" />

- super类似this,指向父类空间
- 利用override重写，**只能重写函数体**
- 父类private函数不能重写（无法访问的）
- 静态不能重写（共享的）
- 重写的本质是当子类可以访问父类方法时才可以重写
- 父类方法的权限要大于等于子类才可以重写（理解父类固定的范围子类只能缩小或者不变，因为子类有super指针可以直接调用到父类方法，如果权限相反，父类就会被暴露）

#### 3）构造器

子类中所有的构造器默认都会先访问父类中无参的构造器，再执行自己

- 子类在初始化的时候，有可能会使用到父类中的数据，如果父类没有完成初始化，子类将无法使用父类的数据。

- 存在形式：子类构造器的第一行语句默认都是：**super()**，默认调用无参构造器

父类中没有无参构造器，只有有参构造器

- 子类每一个构造器中必须手动super(参数1，参数2)
- 子类每一个构造器都要完成父类的数据初始化的任务

父类

```java
package com.example.extends_method;
public class Phone {
    public Phone(String name, int age) {
        this.name = name;
        this.age = age;
    }
    public void call(){
        System.out.println("打电话，发送你好");
    }
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
    private String name;
    private int age;
}
```

子类

```java
package com.example.extends_method;
public class NewPhone extends Phone {

    public NewPhone() {
        super("三星", 2);

    }

    public NewPhone(String name, int age,int cost) {
        super(name, age);
        this.cost=cost;
    }

    @Override
    public void call() {
        System.out.println("用" + getName() + "手机" + getAge() + "年");
    }
    private int cost;
}
```

#### 4）super与this的详细情况(难点)

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220302215014599.png" alt="image-20220302215014599" style="zoom:67%;" />

![image-20220302222824546](C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220302222824546.png)

```java
public class Phone {
    public Phone() {
    }
    public Phone(String name) {
        super();
//        this(name,10);super与this调用不能共存
//        Phone(String name, int age)默认调用了super，不能重复调用
    }
    public Phone(String name, int age) {
        this.name = name;
        this.age = age;
    }
    private String name;
    private int age;
}
```

#### 5）@Override的作用

1. 可以给你当作注释用，感觉这个也不能说明什么，注释也没什么用。
2. 编译器可以给你验证@Override下面的方法名称是否是你父类中所有的，如果没有就会报错。

心得：所以有些时候为了方便，有些代码没有写@override，我都不理解哪里调用了写的代码，用来是用其他提供、封装好的类调用了

### 包

- idea会自动相同包下的类可以直接访问，不同包下的类必须导包,才可以使用！导包格式：**import** **包名.类名**
- 假如一个类中需要用到不同类，而这个两个类的名称是一样的，那么默认只能导入一个类，另一个类要带包名访问。

![image-20220302224813323](C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220302224813323.png)

### 权限修饰符（封装）

个人理解：实际开发中就private和public用的多，protected隔离性没接触到

记忆：  分隔点：同类，同包，不同包的子类

![image-20220302225104369](C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220302225104369.png)

| **修饰符**   | **同一 个类中** | **同一个包中**  **其他类** | **不同包下的**  **子类** | **不同包下的**  **无关类** |
| --------- | ---------- | ------------------ | ----------------- | ------------------ |
| private   | √          |                    |                   |                    |
| 缺省        | √          | √                  |                   |                    |
| protected | √          | √                  | √                 |                    |
| public    | √          | √                  | √                 | √                  |

```java
public class Fu {
//    同类
    private void show1() {
        System.out.println("private");
    }
//同类，本类同包的类
    void show2() {
        System.out.println("缺省");
    }
//同类，本类同包的类，继承的子类
    protected void show3() {
        System.out.println("protected");
    }
//任意
    public void show4() {
        System.out.println("public");
    }

    public static void main(String[] args) {
        Fu f=new Fu();
        f.show1();
        f.show2();
        f.show3();
        f.show4();
    }
}
```

```java
//对于protected方法的验证
public class Zi extends Fu {
    public static void main(String[] args) {
        Fu f=new Fu();
//        f.show1();
//        f.show2();
//        f.show3();
        f.show4();
        Zi z=new Zi();
        z.show3();
        z.show4();
    }
}
```

通过父类对象对于protected方法仍然无法访问，只有子类对象可以访问

- 成员变量一般私有。
- 方法一般公开。
- 如果该成员只希望本类访问，使用private修饰。
- 如果该成员只希望本类，同一个包下的其他类和子类访问，使用protected修饰

### final

实际开发中少用

- final 关键字是最终的意思，可以修饰（方法，变量，类）
- 修饰方法：表明该方法是最终方法，不能被重写。与abstract冲突
- 修饰变量：表示该变量第一次赋值后，不能再次被赋值(有且仅能被赋值一次)。
- 修饰类：表明该类是最终类，不能被继承。string类就是final

特殊的

**final**修饰变量的注意

- final修饰的变量是基本类型：那么变量存储的**数据值**不能发生改变。
- final修饰的变量是引用类型：那么变量存储的**地址值**不能发生改变，但是地址指向的对象内容是可以发生变化的。

```java
  public static void main(String[] args) {
        final int age = 10;
//        age=20;局部基本变量只能赋值一次
        final Cat c=new Cat();
        c.name="汤姆";
        System.out.println(c.name);
        c.name="鸡巴";
        System.out.println(c.name);
        final Cat b=new Cat();
//      c=b;地址不能改变
    }
```

### 变量的种类

根据内存的区别：

main函数中局部变量

- 基本类型，数据直接放在栈中
- 引用类型，栈中放指针，实际数据放在堆中

类中成员变量

- 静态成员变量
- 实例成员变量

### 引用变量的类型转换

自动类型转换

- 多态中，Dog子类指向 Animal变量，小变大，本质上d是Animal变量（猜测，底层不明白）
  
  ```java
   Animal d=new Dog();
  ```

强制类型转换

- Animal变量变为了Dog对象，大变小，有丢失数据的风险，需要强制类型转换

```java
  Dog dog=(Dog) d;
```

### 引用类型的赋值

```
 public static void main(String[] args) {
        A a1=new A();
        a1.a1=1;
        a1.a2 = 1;
        A a2=new A();
        a2.a1=2;
        a2.a2 = 2;


        A temp=new A();
//      引用类型的赋值是浅赋值，只是将地址赋值过去
        temp=a1;
        temp.a1=100;
        a1=a2;
        a2=temp;
        System.out.println("nima");
    }
```

### 语言特性null

null为空

细节的为空将不会开辟空间存储数据

无效代码如下;

```
TreeNode p=root.right;
while (p.!=null){
    p=p.right;
}
p=temp;
```

p如果为空，则赋值无效

有效代码如下：

```
TreeNode p=root;
while (p.right!=null){
    p=p.right;
}
p.right=temp;
```

### 常量

常量名大写

- 常量是使用了public static final修饰的成员变量，必须有初始化值，而且执行的过程中其值不能被改变。
- 常量的作用和好处：可以用于做系统的配置信息，方便程序的维护，同时也能提高可读性

常量的执行原理

- 在编译阶段会进行“宏替换”，把使用常量的地方全部替换成真实的字面量。
- 这样做的好处是让使用常量的程序的执行性能与直接使用字面量是一样的。

源代码

```java
public class Cahngliang {
    public static final String name = "wzt";
    public static void main(String[] args) {
        System.out.println(name);
    }
}
```

编译替换，并且自动加入无参构造器

```java
public class Cahngliang {
    public static final String name = "wzt";
    public Cahngliang() {
    }
    public static void main(String[] args) {
        System.out.println("wzt");
    }
}
```

### 枚举

相对于常量的优势

入参值受约束，代码更严谨

```java
public enum Orientation {
    UP,DOWN,LEFT,RIGHT;
}
```

```java
public class Senson {
    public static void move(Orientation o){
        switch (o){
            case UP :
                System.out.println("up");
                break;
            case DOWN:
                System.out.println("down");
                break;
            case LEFT:
                System.out.println("left");
                break;
            case RIGHT:
                System.out.println("right");
                break;
        }
    }
}
```

### 抽象类

#### 1）写法

在Java中abstract是抽象的意思，如果一个类中的某个方法的具体实现不能确定，就可以申明成abstract修饰的抽象方法（不能写方法体了），这个类必须用abstract修饰，被称为抽象类。

#### 2）特点

1、抽象类的作用是什么样的？

**可以被子类继承、充当模板的、同时也可以提高代码复用。**

2、抽象方法是什么样的？

**只有方法签名，没有方法体，使用了**abstract修饰。

3、继承抽象类有哪些要注意？

- **一个类如果继承了抽象类，那么这个类必须重写完抽象类的全部抽象方法。**（全部）
- **否则这个类也必须定义成抽象类。**（开发中没有意义）

4、抽象类不能创建对象

5、有抽象方法的一定要定义为抽象类，定义为抽象类的不一定有抽象方法（即普通类，但是不能创建对象）

6、abstract不修饰变量、代码块、构造器

7、final与abstract互斥，一个需要继承，一个不允许继承

#### 3）案例：

**系统需求**

- 某加油站推出了2种支付卡，一种是预存10000的**金卡**，后续加油享受8折优惠，另一种是预存5000的**银卡 **,后续加油享受8.5折优惠。
- 请分别实现2种卡片进入收银系统后的逻辑，卡片需要包含主人名称，余额，支付功能。

**分析实现**

- 创建一张卡片父类：定义属性包括主人名称、余额、支付功能（具体实现交给子类）
- 创建一张白金卡类：重写支付功能，按照原价的8折计算输出。
- 创建一张银卡类：重写支付功能，按照原价的8.5折计算输出。

父类

```java
public abstract class Card {
    private String name;
    private double money;
//   抽象方法，不写方法体
    public abstract void pay(double money);
    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public double getMoney() {
        return money;
    }

    public void setMoney(double money) {
        this.money = money;
    }
}
```

子类

```java
public class GoldCard extends Card{
    @Override
    public void pay(double money) {
        double rs=money*0.8;
        double lastMoney=getMoney()-rs;
        setMoney(lastMoney);

    }
}
```

### 模板方法

模板方法handle,升级之使用**final**修饰，子类不能重写模板方法，只能继承使用

![image-20220303220359712](C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220303220359712.png)

不同对象，需要特殊实现的部分，可以用抽象类

### 接口

#### 1）接口的定义与特点

- 接口的格式如下：

​      接口用关键字interface来定义

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220304152146609.png" alt="image-20220304152146609" style="zoom: 80%;" />

- JDK8之前接口中只能是抽象方法和常量，没有其他成分了。
- 接口类不能实例化对象
- 接口中的成员都是public修饰的，写不写都是，因为规范的目的是为了公开化。

#### 2）接口的实现类

- 使用implements继承接口，可以继承多个接口，接口相当于“干爹”，可以有多个
- 必须实现全部接口

```java
public class relise implements ManInterface,SecondInterface{
    @Override
    public void run() {
        System.out.println(SCHOOL_NAME+"举办跑步比赛");
    }

    @Override
    public void study() {
        System.out.println(SCHOOL_NAME+"的同学要好好学习");
    }
}
```

#### 3）接口与接口的关系

类和类的关系：单继承。

类和接口的关系：多实现。

接口和接口的关系：多继承，一个接口可以同时继承多个接口。

- 接口与接口之间可以多继承
- 接口之间存在冲突，当参数一致时，但是返回对象不同，ManInterface中的study接口与SecondInterface中study接口冲突，原因是在调用时无法识别，并且最终实现的功能不同（应该识别出来），就会引发ThirdInterface无法继承。（本质上，接口之间的继承还是基于两个接口之间没有冲突的功能，与类只能单继承的设计理念重叠）

```java
public interface ManInterface {
    //    1、常量灰色，说明代码无效，接口默认加上限制
    public static final String SCHOOL_NAME = "华南理工大学";
    //  2、抽象方法
    public abstract void run();
    String study();
}
```

```java
public interface SecondInterface {
    //void study();冲突
    void study(int a);
}
```

```java
public interface ThirdInterface extends ManInterface,SecondInterface{
    void play();
}
```

#### 4）接口中新增方法(理解程度不高)

JDK8开始后新增了那些方法?

- **默认方法：**default修饰，实现类对象调用。
- **静态方法：static修饰，必须用当前接口名调用，实现类不能调用
- **私有方法：**private修饰，jdk9开始才有的，只能在接口内部被调用。
- 他们都会默认被public修饰。

**JDK8**新增的3种方法我们自己在开发中很少使用，通常是Java源码涉及到的，我们需要理解、识别语法、明白调用关系即可。

#### 5）注意事项

- 接口不能创建对象
- 一个类实现多个接口，多个接口中有同样的静态方法不冲突。
- 一个类继承了父类，同时又实现了接口，父类中和接口中有同名方法，默认用父类的。
- 一个类实现了多个接口，多个接口中存在同名的默认方法，不冲突，这个类重写该方法即可。
- 一个接口继承多个接口，是没有问题的，如果多个接口中存在规范冲突则不能多继承。

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220304161021148.png" alt="image-20220304161021148" style="zoom: 80%;" />

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220304160922585.png" alt="image-20220304160922585" style="zoom: 80%;" />

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220304160746798.png" alt="image-20220304160746798" style="zoom:67%;" />

### 多态

#### 1）访问

**多态中成员访问特点**

- 方法调用：编译看左边，运行看右边。
- 变量调用：编译看左边，运行也看左边。（**多态侧重行为多态**）
- 缺点，子类独有的方法无法访问

```java
public class Animal {
    String name="人";
    void run(){
        System.out.println("动物在跑");
    }
}
```

```java
public class Dog extends Animal {
    String name="金毛";
    @Override
    void run() {
        System.out.println("狗在跑");
    }
}
```

```java
public class test01 {
    public static void main(String[] args) {
        Animal d=new Dog();
//      多态，方法行为实现的是子类的，缺点，不能访问子类独有的方法行为
        d.run();
//      变量调用运行也是左边
        System.out.println(d.name);
    }
}
```

#### 2）强制类型转换

弥补无法访问方法的缺陷

- 如果转型后的类型和对象真实类型不是同一种类型，编译阶段不会报错，运行阶段会出现ClassCastException

- 避免这种情况，加一层判断保护，用下面代码（变量名 **instanceof** 真实类型 判断关键字左边的变量指向的对象的真实类型，是否是右边的类型或者是其子类类型，是则返回true）

```java
 public static void main(String[] args) {
        Animal d=new Dog();
//      多态，方法行为实现的是子类的，缺点，不能访问子类独有的方法行为
        d.run();
//      变量调用运行也是左边
        System.out.println(d.name);
//       强制类型转换前先判断对象是否属于目标对象
// 测试左边的对象是否是右边类或者该类的子类创建的实例对象，是，则返回true，否则返回false。
        if(d instanceof Dog){
            Dog dog=(Dog) d;
            System.out.println(dog.name);
        }
    }
```

实际开发中的保护判断作用：

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220305110718776.png" alt="image-20220305110718776" style="zoom:150%;" />

特殊的，当a就是Tortoise对象时，由于Animal大于Tortoise，参数没有问题，并且instanceof animal也没有问题

#### 3）案例

接口：

```java
public interface USB {
     void connect();
     void unconnect();
}
```

实现类（子类）

```java
public class KeyBoard implements USB {
   private String name;

    public KeyBoard(String name) {
        this.name = name;
    }
    @Override
    public void connect() {
        System.out.println(name+"键盘已连接，赶紧使用敲击代码吧");
    }
    @Override
    public void unconnect() {
        System.out.println(name+"键盘已拔出，休息一下吧");
    }
    public void keyDown(){
        System.out.println("已经开始敲击代码了呢");
    }
    public String getName() {
        return name;
    }
    public void setName(String name) {
        this.name = name;
    }
}
```

```java
public class Mouse implements USB {
    private String name;

    public Mouse(String name) {
        this.name = name;
    }

    @Override
    public void connect() {
        System.out.println(name+"鼠标已连接，赶紧打开黑马吧");
    }

    @Override
    public void unconnect() {
        System.out.println(name+"鼠标已拔出，休息一下吧");
    }
    public void Kick(){
        System.out.println("点击已经有反应了哦");
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }
}
```

电脑类：

```java
public class Computer {
    public Computer(String name) {
        this.name = name;
    }
    void installUSB(USB usb) {
        usb.connect();
        if (usb instanceof KeyBoard) {
            KeyBoard k = (KeyBoard) usb;
            k.keyDown();
        } else {
            Mouse m=(Mouse) usb;
            m.Kick();
        }
        usb.unconnect();
    }
    void start(){
        System.out.println(name+"开机顺畅");
    }
    public String getName() {
        return name;
    }
    public void setName(String name) {
        this.name = name;
    }
    private String name;
}
```

测试类：

```java
public class test01 {
    public static void main(String[] args) {
        Computer c=new Computer("联想");
        c.start();
        KeyBoard u=new KeyBoard("雷电");
        c.installUSB(u);
        USB s=new Mouse("罗技");
        c.installUSB(s);
    }
}
```

### 内部类

#### 静态内部类[了解]

- 有static修饰，属于外部类本身。
- 它的特点和使用与普通类是完全一样的，类有的成分它都有，只是位置在别人里面而已。
- 可以直接访问外部类的静态成员，不能直接访问外部类的实例成员。
- 实际开发中可以单独拿出来用，不如直接定义新的类

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220305120511549.png" alt="image-20220305120511549" style="zoom: 50%;" />

#### 成员内部类[了解]

比如人是外部类，心脏既可以作为成员内部类

- 实际开发中，现有外部类，才有内部类，存在一个嵌套关系
- 成员内部类的实例方法中可以直接访问外部类的实例成员（因为调用内部类实例方法时，就需要走外部类构造器与内部类构造器，即外部类的实例成员已经被创建出来了）
- 成员内部类中可以直接访问外部类的静态成员

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220305132235432.png" alt="image-20220305132235432" style="zoom: 50%;" />

- 成员内部类如何创建对象，先是外部类的构造器，之后是内部类的构造器，外部类名.内部类名 对象名 = new 外部类构造器.new 内部类构造器();
- 访问外部类成员变量

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220305132819866.png" alt="image-20220305132819866" style="zoom:50%;" />

#### 局部内部类[了解]

放在static中自动触发一次，并且只有一次

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220305141253370.png" alt="image-20220305141253370" style="zoom:67%;" />

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220305135328989.png" alt="image-20220305135328989" style="zoom:67%;" />

类似C++中放在main函数中的局部类

#### 匿名内部类概述[重点]

##### a)特点

- 本质上是一个没有名字的局部内部类，定义在方法中、代码块中。（不能说成实例化抽象类，接口）

- 作用：方便创建子类对象，最终目的为了简化代码编写。

- 匿名内部类是一个没有名字的内部类。

- 匿名内部类写出来就会产生一个匿名内部类的对象。

- 匿名内部类的对象类型相当于是当前new的那个的类型的子类类型，即继承了new类型
  
  写法：
  
  <img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220305135955300.png" alt="image-20220305135955300" style="zoom: 67%;" />

##### b)案例

整体作为一个类传参

```java
public class test02 {
    public static void main(String[] args) {
        Swimming s=new Swimming() {
            @Override
            public void swim() {
                System.out.println("学生游的不错");
            }
        };
        go(s);
//      实际开发中，利用匿名内部类，直接简化入参
        go(new Swimming() {
            @Override
            public void swim() {
                System.out.println("老师游的很快");
            }
        });
    }
    public static void go(Swimming s){
        System.out.println("开始游泳");
        s.swim();
        System.out.println("结束");
    }
    interface Swimming{
        void swim();
    }
}
//接口在类内的实现方式
class run implements test02.Swimming {
    @Override
    public void swim() {
    }
}
```

### 包装类

JAVA是面向对象的语言，很多类和方法中的参数都需使用对象(例如集合)，但基本数据类型却不是面向对象的，这就造成了很多不便。

如：List<int> = new ArrayList<>();，就无法编译通过

为了解决该问题，我们引入了包装类，顾名思义，就是将基本类型“包装起来“，使其具备对象的性质，包括可以添加属性和方法，位于java.lang包下。

```
//  语言特性，Interger存在自动缓存，数据足够大时，不能使用==判断
//  -1 ：可以使用==判断，由于进行拆箱，转为int进行判断
//  ==:可以使用 invalue   也可以使用equal进行判断
```

Java 的 Integer，String 等类型判定相等应该用 `equals` 方法而不能直接用等号 `==`，这是 Java 包装类的一个隐晦细节。

| 基本数据类型  | 引用数据类型    |
| ------- | --------- |
| byte    | Byte      |
| short   | Short     |
| int     | Integer   |
| long    | Long      |
| char    | Character |
| float   | Float     |
| double  | Double    |
| boolean | Boolean   |

目的：

- Java为了实现一切皆对象，为8种基本类型提供了对应的引用类型。
- 后面的集合和泛型其实也只能支持包装类型，不支持基本数据类型。

方法作用将整数转为string（鸡肋，利用加号自动转换）,将string转为整数（方法）

```java
           int a = 10;
        Integer a1 = 11;
        Integer a2 = a; // 自动装箱
        System.out.println(a);
        System.out.println(a1);

        Integer it = 100;
        int it1 = it; // 自动拆箱
        System.out.println(it1);

        double db = 99.5;
        Double db2 = db; // 自动装箱了
        double db3 = db2; // 自动拆箱
        System.out.println(db3);

        // int age = null; // 报错了！
        Integer age1 = null;
        Integer age2 = 0;

        System.out.println("-----------------");
        // 1、包装类可以把基本类型的数据转换成字符串形式。（没啥用）
        Integer i3 = 23;
        String rs = i3.toString();
        System.out.println(rs + 1);

        String rs1 = Integer.toString(i3);
        System.out.println(rs1 + 1);

        // 可以直接+字符串得到字符串类型(基本类型和包装类都可行)
        String rs2 = i3 + "";
        System.out.println(rs2 + 1);

        // 可以直接+字符串得到字符串类型
        int b2=23;
        String str2 = b2 + "";
        System.out.println(str2 + 1);

        System.out.println("-----------------");

        String number = "23";
        //转换成整数
        // int age = Integer.parseInt(number);
        int age = Integer.valueOf(number);
        System.out.println(age + 1);

        String number1 = "99.9";
        //转换成小数
//        double score = Double.parseDouble(number1);
        double score = Double.valueOf(number1);
        System.out.println(score + 0.1);
```

### 正则表达式

### Lambda表达式

- Lambda表达式是JDK 8开始后的一种新语法形式。
- 作用：简化匿名内部类的代码写法
- Lambda表达式只能简化函数式接口的匿名内部类的写法形式

函数式接口

- 接口
- 并且只有一个抽象方法（理解：唯一的方法，才可以简化，匿名内部类才不需要识别）

```java
@FunctionalInterface
public interface Comparator<T> {}
```

```java
public class testmyself {
    public static void main(String[] args) {

        Climbing wzt = () -> System.out.println("只有每天都敲打很多代码，之后才有老婆孩子去爬山");
        go(wzt);
        Climbing lhx=new Climbing() {
            @Override
            public void climb() {
                System.out.println("很强");
            }
        };
        go(lhx);


        Integer[] arr=new Integer[]{123,113,1342,456,132,324,24};
        Arrays.sort(arr, ( o1,  o2) -> o1-o2);
        System.out.println(Arrays.toString(arr));


    }

    public static void go(Climbing cli) {
        System.out.println("开始爬山");
        cli.climb();
        System.out.println("休息一下吧");

    }
}
@FunctionalInterface
interface Climbing {
    void climb();
}
```

极简：只重写一行代码是，将多余的括号，return，参数之类的全部拿走（重点，当别人写出极简代码时自己要看的懂）

### 泛型

查看代码，足够详细

泛型设计，要自己会写一个泛型，可以适配不同类型的数据处理

```
  泛型方法的定义格式:
!!!!!!理解：<泛型变量说明了T是泛型>
       修饰符 <泛型变量> 返回值类型 方法名称(形参列表){
       }
```

泛型类、泛型方法、泛型接口

### Collection

[文档详解](D:\download\downloadFromMicsoft\day16、集合（Set、Collections、Map、集合嵌套）\PPT)

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220407151227427.png" alt="image-20220407151227427" style="zoom:50%;" />

 目标：Collection集合的常用API.  [collection的API](D:\Project\Java\JavaSe_Code\base_study\src\com\example\collection)
 Collection是集合的祖宗类，它的功能是全部集合都可以继承使用的，所以要学习它。
 Collection API如下:

      - public boolean add(E e)：  把给定的对象添加到当前集合中 。
            - public void clear() :清空集合中所有的元素。
      - public boolean remove(E e): 把给定的对象在当前集合中删除。
            - public boolean contains(Object obj): 判断当前集合中是否包含给定的对象。
      - public boolean isEmpty(): 判断当前集合是否为空。
            - public int size(): 返回集合中元素的个数。
      - public Object[] toArray(): 把集合中的元素，存储到数组中。
            - 小结：

- addAll把c2集合的元素全部倒入到c1中去。

Collection集合的遍历方式有三种:
    （1）迭代器。
    （2）foreach(增强for循环)。
    （3）JDK 1.8开始之后的新技术Lambda表达式(了解)

疑问：迭代器的底层究竟是什么（看源码）

```java
Iterator<String> it = lists.iterator();
System.out.println(it);
String ele = it.next();
```

it.next是先获得数据还是先移动再获得数据

```java
it.hasnext()
```

查看的是当前位置是否存在元素，还是下一个位置是否存在元素

易错：

```java
Iterator<String> it = list.iterator();
list.remove("Java");
```

当使用迭代器后，不能再使用remove,remove会使迭代器跳到下一个元素

下列更安全，具体实现看底层

```java
   it.remove();
```

#### List

拓展常用Api： subList

[D:\Project\Java\JavaSe_Code\base_study\src\com\example\collection\List\ListDemo01.java]()

#### set

##### HashSet

特点：无序，不重复，无索引

具体底层看源码

底层中先比较哈希值再比较内容是否相同。（设计的初衷是如果内容一致，默认的哈希值是一致，要去重，所以为了效率，先检查地址）？

！！！！！插入自己定义的引用类型时，必须重写equal和hashcode，底层不一致的原因须看源码

总结，底层使用了hash,即名字里带了hash，存入自定义类型数据时，必须重写equal和hashcode函数

##### LinkedHashSet

特点：有序，不重复，无索引

插入的顺序用双链表维护

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220407231023353.png" alt="image-20220407231023353" style="zoom:50%;" />

##### TreeSet

特点：可排序，不重复，无索引

底层基于红黑树

对于自定义的数据类型，要自定义排序方式

[代码详解](D:\Project\Java\JavaSe_Code\base_study\src\com\example\collection\set\d1_collection_set\SetDemo5.java)

[文档详解](D:\download\downloadFromMicsoft\day16、集合（Set、Collections、Map、集合嵌套）\PPT)

##### Collections工具类

[代码详解](D:\Project\Java\JavaSe_Code\base_study\src\com\example\collection\set\d3_collections\CollectionsDemo01.java)

#### 应用详解

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220407232629870.png" alt="image-20220407232629870" style="zoom:50%;" />

### Map

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220408164226846.png" alt="image-20220408164226846" style="zoom:50%;" />

#### map

常见API

遍历

使用foreach遍历map集合.发现Map集合的键值对元素直接是没有类型的。所以不可以直接foreach遍历集合

可以通过调用Map的方法 entrySet把Map集合转换成Set集合形式  maps.entrySet();

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220408181209614.png" alt="image-20220408181209614" style="zoom: 67%;" />

1**、HashMap的特点和底层原理**

由键决定：无序、不重复、无索引。HashMap底层是哈希表结构的。

依赖hashCode方法和equals方法保证键的唯一。

如果键要存储的是自定义对象，需要重写hashCode和equals方法。

基于哈希表。增删改查的性能都较好。

子类概述

HashMap:元素按照键是无序，不重复，无索引，值不做要求，基于哈希表（与Map体系一致）

LinkedHashMap:元素按照键是有序，不重复，无索引，值不做要求，基于哈希表

TreeMap：元素只能按照**键排序**，不重复，无索引的，值不做要求，可以做排序

理解，map同set类似，set里存入的即使map中的键，

### 可变参数

1.一个形参列表中只能有一个可变参数,

2.可变参数必须放在形参列表的最后面

3.可变参数在方法内部其实就是一个数组。 nums

```java
/**
    目标：可变参数。

    可变参数用在形参中可以接收多个数据。
    可变参数的格式：数据类型...参数名称

    可变参数的作用：
         传输参数非常灵活，方便。
         可以不传输参数。
         可以传输一个参数。
         可以传输多个参数。
         可以传输一个数组。

     可变参数在方法内部本质上就是一个数组。
     可变参数的注意事项：
         1.一个形参列表中可变参数只能有一个！！
         2.可变参数必须放在形参列表的最后面！！
     小结：
        记住。
 */
public class MethodDemo {
    public static void main(String[] args) {

        sum(); // 1、不传参数
        sum(10); // 2、可以传输一个参数
        sum(10, 20, 30); // 3、可以传输多个参数
        sum(new int[]{10, 20, 30, 40, 50}); // 4、可以传输一个数组
    }

    /**
       注意：
     1.一个形参列表中只能有一个可变参数,
     2.可变参数必须放在形参列表的最后面
     * @param nums
     */
    public static void sum(  int...nums){
        // 注意：可变参数在方法内部其实就是一个数组。 nums
        System.out.println("元素个数：" + nums.length);
        System.out.println("元素内容：" + Arrays.toString(nums));
    }
}
```

### 不可变集合

```java
public class CollectionDemo {
    public static void main(String[] args) {
        // 1、不可变的List集合
        List<Double> lists = List.of(569.5, 700.5, 523.0,  570.5);
        // lists.add(689.0);
        // lists.set(2, 698.5);
        // System.out.println(lists);
        double score = lists.get(1);
        System.out.println(score);

        // 2、不可变的Set集合
        Set<String> names = Set.of("迪丽热巴", "迪丽热九", "马尔扎哈", "卡尔眨巴" );
//         names.add("三少爷");
        System.out.println(names);

        // 3、不可变的Map集合
        Map<String, Integer> maps = Map.of("huawei",2, "Java开发", 1 , "手表", 1);
        // maps.put("衣服", 3);
        System.out.println(maps);
    }
}
```

### Stream

无存储。stream不是一种数据结构，它只是某种数据源的一个视图，数据源可以是一个数组，Java容器或I/O channel等。
为函数式编程而生。对stream的任何修改都不会修改背后的数据源，比如对stream执行过滤操作并不会删除被过滤的元素，而是会产生一个不包含被过滤元素的新stream。

1. 先得到集合或者数组的Stream流（就是一根传送带）。

2. 把元素放上去。

3. 然后就用这个Stream流简化的API来方便的操作元素。

.map做了一个对象映射，可以从流中原始的对象产生新的对象

中间API

| 名称                                                   | 说明                              |
| ---------------------------------------------------- | ------------------------------- |
| Stream<T>  filter(Predicate<?  super  T>  predicate) | 用于对流中的数据进行**过滤。**               |
| Stream<T>  limit(long maxSize)                       | 获取前几个元素                         |
| Stream<T>  skip(long n)                              | 跳过前几个元素                         |
| Stream<T>  distinct()                                | 去除流中重复的元素。依赖(hashCode和equals方法) |
| static  <T> Stream<T> concat(Stream  a, Stream b)    | **合并**a和b两个流为一个流                |

终结API

| 名称                             | 说明             |
| ------------------------------ | -------------- |
| void  forEach(Consumer action) | 对此流的每个元素执行遍历操作 |
| long count()                   | 返回此流中的元素数      |

注意：

1. 中间方法也称为非终结方法，调用完成后返回新的Stream流可以继续使用，支持链式编程。

2. 在Stream流中无法直接修改集合、数组中的数据。

收集流

| 名称                             | 说明                |
| ------------------------------ | ----------------- |
| R collect(Collector collector) | 开始收集Stream流，指定收集器 |

| 名称                                                                        | 说明            |
| ------------------------------------------------------------------------- | ------------- |
| public static <T> Collector toList()                                      | 把元素收集到List集合中 |
| public static <T> Collector toSet()                                       | 把元素收集到Set集合中  |
| public static Collector toMap(Function keyMapper  , Function valueMapper) | 把元素收集到Map集合中  |

### 异常

适用场景，对数据进行合法处理时，异常十分有用

编译异常javac、运行异常jvm(java虚拟机)

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220413131736918.png" alt="image-20220413131736918" style="zoom:50%;" />

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220413131557940.png" alt="image-20220413131557940" style="zoom:50%;" />

异常处理的三种方式

- 出现异常直接抛出去给调用者，调用者也继续抛出去，抛给jvm。
- 出现异常自己捕获处理，不麻烦别人。
- 前两者结合，出现异常直接抛出去给调用者，调用者捕获处理。

自定义异常理解一般

[代码](D:\Project\Java\JavaSe_Code\base_study\src\com\example\unchangeCollection_stream_exception\d9_exception_custom)

### file

file的构造函数：根据路径获取文件，只能得到相应的文件属性，并不可以修改文件的内容

相对路径：当无法确定默认定位到哪里时，直接使用绝对定位，并且尝试删除前面的路径

用处：可以适配不同的电脑，不同的环境

易错：相对路径不需要写 /  根目录

易错：file的相对路径定位从模块名开始，即加上模块名

```java
File f2 = new File("base_study/src/com/example/file_recursion_io/data.txt");//相对路径base_study模块名
```

- File对象可以定位文件和文件夹
- File封装的对象仅仅是一个路径名，**这个路径可以是存在的，也可以是不存在的。**

file的api

```
- public String getAbsolutePath()  ：返回此File的绝对路径名字符串。
- public String getPath()  ： 获取创建文件对象的时候用的路径
- public String getName()  ： 返回由此File表示的文件或目录的名称。
- public long length()  ：    返回由此File表示的文件的长度。
```

getPath()返回的是file变量存放的内容

getAbsolutePath()返回的是文件的绝对路径

- delete方法默认只能删除文件和空文件夹。
- delete方法直接删除不走回收站

文件遍历

| 方法名称                          | 说明                                  |
| ----------------------------- | ----------------------------------- |
| public String[] list()        | 获取当前目录下所有的"一级文件名称"到一个字符串数组中去返回。     |
| public File[] listFiles()(常用) | 获取当前目录下所有的"一级文件对象"到一个文件对象数组中去返回（重点） |

### 递归

三要素

递归的公式： f(n) = f(n-1) * n;

递归的终结点：f(1) 

递归的方向必须走向终结点：即return 必须-1

案例：猴子吃桃

题目：猴子第一天摘下若干桃子，当即吃了一半，觉得好不过瘾，于是又多吃了一个第二天又吃了前天剩余桃子数量的一半，觉得好不过瘾，于是又多吃了一个以后每天都是吃前天剩余桃子数量的一半，觉得好不过瘾，又多吃了一个等到第10天的时候发现桃子只有1个了。

需求：请问猴子第一天摘了多少个桃子？

公式： f(x) - f(x)/2 - 1 = f(x+1)

```java
public class RecursionDemo04_taozi {
    public static void main(String[] args) {
        System.out.println(f(1));
//        System.out.println(f(2));
//        System.out.println(f(3));
    }

    public static int f(int n){
        if(n == 10){
            return 1;
        }else {
            return 2 * f(n + 1) + 2;
        }
    }
}
```

### 编码

[代码test](D:\Project\Java\JavaSe_Code\base_study\src\com\example\file_recursion_io\d3_charset)

ASCII**字符集：**

- ASCII(American Standard Code for Information Interchange，美国信息交换标准代码)：包括了数字、英文、符号。
- ASCII使用1个字节存储一个字符，一个字节是8位，总共可以表示128个字符信息，对于英文，数字来说是够用的。

GBK

- window系统默认的码表。兼容ASCII码表，也包含了几万个汉字，并支持繁体汉字以及部分日韩文字。
- GBK是中国的码表，一个中文以两个字节的形式存储。但不包含世界上所有国家的文字

Unicode码表：

- unicode（又称统一码、万国码、单一码）是计算机科学领域里的一项业界字符编码标准。
- 容纳世界上大多数国家的所有常见文字和符号。
- 由于Unicode会先通过UTF-8，UTF-16，以及 UTF-32的编码成二进制后再存储到计算机，其中最为常见的就是UTF-8。
- Unicode是万国码，以UTF-8编码后一个中文一般以**三个字节**的形式存储。
- UTF-8也要兼容ASCII编码表。
- 技术人员都应该使用UTF-8的字符集编码。
- 编码前和编码后的字符集需要一致，否则会出现中文乱码。

编码-->二进制-->解码-->字符

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220413194047673.png" alt="image-20220413194047673" style="zoom:50%;" />

编码前的字符集和编码好的字符集有什么要求？

必须一致，否则会出现中文字符乱码

英文和数字在任何国家的编码中都不会乱码

```java
public class Test {
    public static void main(String[] args) throws Exception {
        // 1、编码：把文字转换成字节（使用指定的编码）
        String name = "abc我爱你中国";
        // byte[] bytes = name.getBytes(); // 以当前代码默认字符集进行编码 （UTF-8）
        byte[] bytes = name.getBytes(); // 指定编码,变为二进制存储
        System.out.println(bytes.length);

        System.out.println(Arrays.toString(bytes));

        // 2、解码：把字节转换成对应的中文形式（编码前 和 编码后的字符集必须一致，否则乱码 ）
        // String rs = new String(bytes); // 默认的UTF-8
        String rs = new String(bytes); // 指定GBK解码
        System.out.println(rs);
    }
}
```

### I/O流

[文档详情，当md文件不够时可查阅](D:\download\downloadFromMicsoft\day19、File、递归、IO流(一)\PPT)

文件的内容的读取与修改与file不同

#### IO流的分类

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220529194818501.png" alt="image-20220529194818501" style="zoom:67%;" />

字节流：音频与图片

字符流：java文件，text文件

#### IO流的体系

以内存为基准，即以正在运行的程序为基准，将数据从内存写入磁盘或者网络中去，为输出流，其他同理

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220529195106089.png" alt="image-20220529195106089" style="zoom:50%;" />

outputstream中flush的作用

部分outputstream的子类实现了缓存机制，为了提高效率当write()的时候不一定直接发过去，有可能先缓存起来一起发。flush()的作用就是强制性地将缓存中的数据发出去

### 多线程

#### 创建

创建三个方法

法一

①定义一个子类MyThread继承线程类java.lang.Thread，重写run()方法

②创建MyThread类的对象

③调用线程对象的start()方法启动线程（启动后还是执行run方法的）并且start需要放在主线程前面

直接调用run方法会当成普通方法执行，此时相当于还是单线程执行。

只有调用start方法才是启动一个新的线程执行。

```java
public static void main(String[] args) {
    Thread th=new MyThread();
    th.start();
    for (int i = 0; i < 10; i++) {
        System.out.println("主线程"+i);
    }
}
```

```java
public class MyThread extends Thread{
    @Override
    public void run() {
        for (int i = 0; i < 10; i++) {
            System.out.println("子线程正在执行"+i);
        }
    }
}
```

缺点：线程类已经继承Thread，无法继承其他类，不利于扩展。

法二

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220306110705703.png" alt="image-20220306110705703" style="zoom:67%;" />

```java
public class MyRunnable implements Runnable{
    @Override
    public void run() {
        for (int i = 0; i < 10; i++) {
            System.out.println("子线程正在执行"+i);
        }
    }
}
```

```java
public static void main(String[] args) {
    Runnable  tar=new MyRunnable();
    Thread th=new Thread(tar);
    th.start();
    for (int i = 0; i < 10; i++) {
        System.out.println("主线程"+i);
    }
}
```

法三：

优缺点

- 优点：线程任务类只是实现接口，可以继续继承类和实现接口，扩展性强。
- 可以在线程执行完毕后去获取线程执行的结果。
- 缺点：编码复杂一点。

futuretask的API

| 方法名称                               | 说明                          |
| ---------------------------------- | --------------------------- |
| public FutureTask<>(Callable call) | 把Callable对象封装成FutureTask对象。 |
| public V get() throws Exception    | 获取线程执行call方法返回的结果。          |

个人理解：在不改变原有thread的基础上，添加的futuretask作为桥梁，实现了提取线程返回值的需求

#### 线程安全

同步代码块、同步方法

[代码详解](D:\Project\Java\JavaSe_Code\base_study\src\com\example\multithreading\d5_thread_synchronized_method)

**同步代码块**

- 作用：把出现线程安全问题的核心代码给上锁。
- 原理：每次只能一个线程进入，执行完毕后自动解锁，其他线程才可以进来执行。

**锁对象的规范要求**

- 规范上：建议使用共享资源作为锁对象。
- 对于实例方法建议使用this作为锁对象。
- 对于静态方法建议使用字节码（类名.class）对象作为锁对象。

**同步方法底层原理**

- 同步方法其实底层也是有隐式锁对象的，只是锁的范围是整个方法代码。
- 如果方法是实例方法：同步方法默认用this作为的锁对象。但是代码要高度面向对象！
- 如果方法是静态方法：同步方法默认用类名.class作为的锁对象。

**Lock锁**

- 为了更清晰的表达如何加锁和释放锁，JDK5以后提供了一个新的锁对象Lock，更加灵活、方便。
- Lock实现提供比使用synchronized方法和语句可以获得更广泛的锁定操作。
- Lock是接口不能直接实例化，这里采用它的实现类ReentrantLock来构建Lock锁对象。

#### 线程通信

API

| 方法名称              | 说明                                         |
| ----------------- | ------------------------------------------ |
| void  wait()      | 当前线程等待，直到另一个线程调用notify() 或 notifyAll()唤醒自己 |
| void  notify()    | 唤醒正在等待对象监视器(锁对象)的单个线程                      |
| void  notifyAll() | 唤醒正在等待对象监视器(锁对象)的所有线程                      |

实例

[接受电话，只能固定一个接听员](D:\Project\Java\JavaSe_Code\base_study\src\com\example\multithreading\d7_thread_comunication)

#### 线程池（重点）

**创建临时线程**

新任务提交时发现核心线程都在忙，任务队列也满了，并且还可以创建临时线程，此时才会创建临时线程。

**拒绝任务**

核心线程和临时线程都在忙，任务队列也满了，新的任务过来的时候才会开始任务拒绝。

[API](D:\Project\Java\JavaSe_Code\base_study\src\com\example\multithreading\d8_threadpool)

| 方法名称                                | 说明                                      |
| ----------------------------------- | --------------------------------------- |
| void execute(Runnable command)      | 执行任务/命令，没有返回值，一般用来执行  Runnable 任务       |
| Future<T>  submit(Callable<T> task) | 执行任务，返回未来任务对象获取线程结果，一般拿来执行  Callable 任务 |
| void  shutdown()                    | 等任务执行完毕后关闭线程池                           |
| List<Runnable> shutdownNow()        | 立刻关闭，停止正在执行的任务，并返回队列中未执行的任务             |

executors工具类

| 方法名称                                                                                                                                                                                          | 说明                                             |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------- |
| public  static [ExecutorService](mk:@MSITStore:D:\course\jdk-11中文api修订版.CHM::/java.base/java/util/concurrent/ExecutorService.html) newCachedThreadPool()                                      | 线程数量随着任务增加而增加，如果线程任务执行完毕且空闲了一段时间则会被回收掉。        |
| public static [ExecutorService](mk:@MSITStore:D:\course\jdk-11中文api修订版.CHM::/java.base/java/util/concurrent/ExecutorService.html) newFixedThreadPool(int nThreads)                            | 创建固定线程数量的线程池，如果某个线程因为执行异常而结束，那么线程池会补充一个新线程替代它。 |
| public  static [ExecutorService](mk:@MSITStore:D:\course\jdk-11中文api修订版.CHM::/java.base/java/util/concurrent/ExecutorService.html) newSingleThreadExecutor ()                                 | 创建只有一个线程的线程池对象，如果该线程出现异常而结束，那么线程池会补充一个新线程。     |
| public  static [ScheduledExecutorService](mk:@MSITStore:D:\course\jdk-11中文api修订版.CHM::/java.base/java/util/concurrent/ScheduledExecutorService.html) newScheduledThreadPool(int corePoolSize) | 创建一个线程池，可以实现在给定的延迟后运行任务，或者定期执行任务。              |

**Executors**的底层其实也是基于线程池的实现类ThreadPoolExecutor创建线程池对象的。

#### 定时器

**Timer**定时器的特点和存在的问题

1、Timer是单线程，处理多个任务按照顺序执行，存在延时与设置定时器的时间有出入。

2、可能因为其中的某个任务的异常使Timer线程死掉，从而影响后续任务执行。

**ScheduledExecutorService**的优点

1、基于线程池，某个任务的执行情况不会影响其他定时任务的执行。

### 网络通信

#### UDP

**DatagramPacket**：数据包对象（韭菜盘子）

| 构造器                                                                            | 说明                                                                                   |
| ------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------ |
| public DatagramPacket(byte[] buf, int  length, InetAddress address,  int port) | 创建**发送端**数据包对象  buf：要发送的内容，字节数组  length：要发送内容的字节长度  address：接收端的IP地址对象  port：接收端的端口号 |
| public DatagramPacket(byte[] buf, int  length)                                 | 创建**接收端**的数据包对象  buf：用来存储接收的内容  length：能够接收内容的长度                                     |

套接字

**DatagramSocket**：发送端和接收端对象（人）

| 构造器                             | 说明                               |
| ------------------------------- | -------------------------------- |
| public DatagramSocket()         | 创建**发送端**的Socket对象，系统会随机分配一个端口号。 |
| public DatagramSocket(int port) | 创建**接收端**的Socket对象并指定端口号         |

| 方法                                    | 说明    |
| ------------------------------------- | ----- |
| public void send(DatagramPacket dp)   | 发送数据包 |
| public void receive(DatagramPacket p) | 接收数据包 |

剩余的网络通信的知识之后遇到了再看

D:\Project\Java\JavaSe_Code\base_study\src\com\example\net_communication

### 单元测试

### 反射

### 注解

### XML

### 解析

### 设计模式
