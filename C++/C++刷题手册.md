C++刷题手册



## 环境

​    ***.sln**：(Visual Studio.Solution) 通过为环境提供对项目、项目项和解决方案项在磁盘上位置的引用,可将它们组织到解决方案中。比如是生成Debug模式,还是Release模式,是通用CPU还是专用的等.

​    ps:就是打开文件的索引,正确引导你进入环境,进入工程





Visual Studio 刷新很慢

如果vs本身报错，无法正常启动，可以手动启动生成解决方案

ctrl+shift+B

格式化代码

```C++
ctrl+k  ctrl+d
```

### vscode

**问题**：vscode里，.cpp文件无法链接到不在同一子目录下的.h文件，链接方式是#include".h"

在 Visual Studio Code (VSCode) 中，如果你的 `.cpp` 文件无法链接到不在同一子目录下的 `.h` 文件，通常是因为编译器无法找到这些头文件的位置。你可以采取以下步骤来解决这个问题：

1. **确保头文件的路径正确：** 在 `.cpp` 文件中使用 `#include` 包含头文件时，确保提供了正确的路径。你可以使用相对路径或绝对路径，具体取决于你的项目结构。如果头文件在 `.cpp` 文件的相同目录中，只需使用 `#include "header.h"` 即可。如果在不同目录中，需要提供相对或绝对路径，如 `#include "../folder/header.h"`。

2. **配置编译器的包含路径：** 在 VSCode 中，你可以配置编译器的包含路径，以告诉编译器在哪里查找头文件。这通常在项目的配置文件（如 `c_cpp_properties.json`）中完成。以下是一个示例：

   ```
   jsonCopy code{
       "configurations": [
           {
               "name": "Win32",
               "includePath": [
                   "${workspaceFolder}/**", // 包括工作区中的所有文件夹
                   "D:/path/to/your/headers" // 添加头文件所在的目录
               ],
               // 其他配置项...
           }
       ],
       // 其他配置项...
   }
   ```

   在这个示例中，我们将 `"D:/path/to/your/headers"` 添加到包含路径中，以便编译器能够找到头文件。请根据你的项目和操作系统进行相应的配置



## 英语

divisor  除法，公约数

the greatest common divisor最大公约数

tentive 实验性的

combinatorial 组合的

adjacent 相邻的

clique 小集团

precedence 优先级

parenthese 括号

Infix Expression 后缀表达式

 siblings 兄弟

## 低级错误

### bool值判断

错误代码

```c++
                if(diff){//
                    money += (long long)diff * cost[i];
                    if(money > budget)return false;
                } 
```

正确代码，一定要注意是正值还是负值，注意判断

```c++
                if(diff > 0){//
                    money += (long long)diff * cost[i];
                    if(money > budget)return false;
                } 
```

### 指针申请

```c++
List * node;
node->value = 0;
```

正确代码，一定要给指针分配空间

```c++
 List * node = new List();
 node->value = 0;
```



### 指针指向

```c++
	while(list1 != nullptr && list2 != nullptr){
        if(list1->val < list2->val){
            head = list1;//犯错误
            list1 = list1->next;
        }else{
            head = list2;	
            list2 = list2->next;
        }
        head = head->next;  
    }
```

将指针指向另一个指针，并不能构建一条新的链表，要构建链表是将节点通过next连起来

### 二分搜索

#### 右边界

由于r是没取到的，需要多加上+1

#### 递增递减

没有考虑到



### >>



```c++
 int mid = (l+r)>>2;//犯错，除4，呆呆地
```

实际上应该是

```
 int mid = (l+r)>>1;
```



### 形参&

要在整个递归中运用同一个数据结构，形参要加上&，但是我却犯错

## 考试注意事项

180分钟，一共3小时

四道题：20，25，25，30分

## 弱提示

1. 浮点错误：有可能是引入错误的0作为除数


2. 段错误：

temp输入超过数组范围

```c++
	if (temp > 0&&temp<100001)out[temp]=1;//细节，数组有范围
```



对于输出，要重点检查一遍，可能是输出的格式理解出问题，导致输出的行数不对

3. 答案错误

   ```c++
   printf("Take Line#%d from %04d to %04d.\n", preLine, start, p[i - 1]);
   ```

   注意答案输出的格式

答案输出错误

## 数据范围

int 4字节 ，-2^31-1~ 2^31    9位数据

```
[-2147483648,2147483647]
```

unsigned int 4字节，0 ~ 2^32-1

long long 8字节

float 4字节 6位有效数字

double 8字节 15位有效数字





表示无穷大    1061109567

```c++
const int INF = 0x3f3f3f3f;
```



## 自动类型转换

赋值左右两边不会相互影响，

简单的说，等号右边全是整型参与的运算，最后产生的结果是整型，然后根据左边类型进行自动变换而已

但是有浮点类型数据参加，等号右边产生结果就是浮点数

```C++
return (res[(m + n) / 2] + res[(m + n) / 2 - 1]) / 2.0;
```

需要返回浮点数，直接将要表达式中的一个值改成浮点数

但是要注意的是，如果用int变量去接，将会变浮点数为整数



long long也是一样的：在 C++ 中，对于加法、减法、乘法和除法运算，如果其中一个操作数是 `long long` 类型，那么会发生隐式类型提升，将其他操作数自动转换为 `long long`，以便进行操作。这是 C++ 的类型提升规则的一部分，也称为"整数提升"。



所以

## 输入与输出

### 内存大小

比较容易遗忘的就是1B为1个byte

1B(Byte 字节)=8bit，
1KB (Kilobyte 千字节)=1024B，
1MB (Megabyte 兆字节 简称“兆”)=1024KB，
1GB (Gigabyte 吉字节 又称“千兆”)=1024MB，
1TB (Trillionbyte 万亿字节 太字节)=1024GB，其中1024=2^10 ( 2 的10次方)，
1PB（Petabyte 千万亿字节 拍字节）=1024TB，
1EB（Exabyte 百亿亿字节 艾字节）=1024PB，
1ZB (Zettabyte 十万亿亿字节 泽字节)= 1024 EB,
1YB (Yottabyte 一亿亿亿字节 尧字节)= 1024 ZB,
1BB (Brontobyte 一千亿亿亿字节)= 1024 YB.



即如果限制内存为1MB时，可以申请数组空间为250000

scanf

printf

同时需要掌握

```c++
//加入头文件
#include<cstdio>
```



答案要完全一致，没有一点差距



### getchar

getchar——读取字符的函数

```
int getchar(void)
```

返回类型为int,参数为void.
有人可能会有疑惑，getchar既然是读取字符的，为什么返回类型是int呢？
1、getchar其实返回的是字符的ASCII码值（整数）。
2、getchar在读取结束或者失败的时候，会返回EOF。

EOF意思是end of file,本质上是-1.



注意：可以输入空格，遇到ctrl+z结束

```c++
#include<stdio.h>
int main()
{
	int ch = 0;
	while ((ch = getchar()) != EOF)
	{
		putchar(ch);
	}

	return 0;

}
```

### 清空输入缓冲区

![img](https://github.com/wztsir/Note/blob/main/Image/getchar.png?raw=true)

![img](https://github.com/wztsir/Note/blob/main/Image/getchar2.png?raw=true)

getchar取走换行符

```c++
//把缓冲区中的内容全读走
	while ( getchar() != '\n')
	{
		;
	}
```



### getline

遇见空格可以正常输入

遇见换行符号依旧会终止

```C++

string s;
getline(cin，s);

```



### cin

从输入流（输入缓冲区）读取数据后，不会舍弃‘\n’

所以再接getline后，输入终止

需要加上

```c++
cin.ignore();
//或者
getchar();
```



### cin.getline

```C++
char s[101];
cin.getline(s, sizeof(s));
cout << s;
```
## for循环

这显然是正确的

```C++
	for (int i = row-1,j=col-1; i >= 0&&j>=0; i--,j--)
		if(temp[i][j] == 'Q')return false;	
```

然而有一种想当然的写法

```C++
	for (int i = row-1,j=col-1; i >= 0,j>=0; i--,j--)
		if(temp[i][j] == 'Q')return false;	
```

条件判断必须用关系连接符连接，如&&，||

## 引用

在C++中，引用有两种类型：常量引用（const reference）和非常量引用（non-const reference）。

- 常量引用可以绑定到左值和右值，因为它们不允许修改所引用的对象。例如：`const int& x = 42;` 这里 `x` 是一个常量引用，可以绑定到右值 `42`。
- 非常量引用通常绑定到左值，因为它们允许修改所引用的对象。例如：`int y = 10; int& z = y;` 这里 `z` 是一个非常量引用，绑定到左值 `y`。

```c++
int& w = 42; // 这会导致编译错误
```

## size_t


当我们考虑一个集装箱装满货物时，`size_t` 就好比这个集装箱的容量，而 `int` 就好比可以用来计数的数字。

1. `size_t` 就像一个非负容量：集装箱的容量总是非负的，它代表了容器可以容纳的最大物品数量。同样，`size_t` 表示了容器（比如字符串、数组、向量等）可以容纳的最大元素数量。
2. `int` 好比集装箱里的物品数量：`int` 是一个整数，可以代表物品的数量，包括正数、负数和零。但在表示集装箱容量时，负数没有实际意义，因为容器不可能具有负容量。

使用 `size_t` 类型来表示容器大小或索引就像在考虑集装箱容量时不考虑负数一样。这有助于避免错误和混淆，因为在容器大小和索引方面，负数通常没有实际用途。

所以，`size_t` 通常用于表示容器的大小、计数以及与容器相关的信息，因为它更符合实际情况，可以减少潜在的错误。

## list

### 指针

永远记住，指针是个标签，他标注了一个真正的商品，要修改链表，本质上要通过标签修改对于的商品

### dummy

涉及链表的增删改时都记得搞个虚拟节点

## arr

### 初始化



```
arr[10]={1};//第一项为1，其余为0
arr[10]={0};//全部初始化为0
arr[10]={5,2,1};//前面三个数据初始化为5，2，1,后面还是0
```

【1428】小鱼比可爱   有没有更快的形式

非n^2的时长





### 最大与内存

最大可以开到1mb， 25*10^4个数组

对于二维数组而言，如果内存大小限制1mb,开到的大小为500,500



### 深复制

```C++
	vector<int>a, b;
	a.push_back(0);
	cout << &a << " " << &b<<"\n";
	b = a;
	b[0] = 10;
	cout << a[0] << b[0]<<"\n";
	cout << &a <<" "<< &b;
```
vector不是常量，不在常量池中，是深复制

将数值复制过来，但数值的地址不同，vector初始化时的地址就不同

输出

```c++
000000F4426FF9C8 000000F4426FFA08
010
000000F4426FF9C8 000000F4426FFA08
```



## vector

### 初始化

1.长度n个string,且每个string初始化为n个‘.’

```C++
vector<string> board(n, string(n, '.'));
```



2.长度n个string,且每个string都未被初始化，未知的数据

```C++
vector<string> board(n);
```



3.初始化，n个0

```
vector<int> board(n);
```



4.初始化，n个0.0

```
vector<float> board(n);
```



5.初始化，n个false

```
vector<bool> board(n);
```



6.【】与()的区别

```C++
vector<double> points[pointsCount];
```

```C++
vector<double> points(pointsCount);
```

一个数组里有两个vector<double>，一个是存放元素，double

### 二维数组

可以初始化大小，如下：

```C++
vector<vector<long long>> dp(s.size() + 1, vector<long long>(t.size() + 1));
```





### 一维数组

初始化大小

```C++
vector<int> out(5);
```

初始化的数据大小为0

使用fill函数初始化二维数组大小，类似于sort（），只适用于一维

```C++
fill(f.begin(), f.end(), -1);
```



## queue

队列（Queue）是一种常见的数据结构，用于存储和管理数据项，通常采用先进先出（FIFO）的方式处理元素。在C++中，队列可以使用STL（Standard Template Library）中的`std::queue`来实现。`std::queue`是一个适配器容器，它基于底层容器（通常是`std::deque`）提供队列的功能。

在`std::queue`中，有两种主要方法可以用来将元素添加到队列中：`push`和`emplace`。它们的区别在于如何将元素添加到队列中以及需要传递的参数。

简单来说，就是push不会帮你调用构造，直接把存在的对象添加进去，但是`emplace`方法会帮你调用构造



1. **`push`方法**：

   - `push`方法用于将已经创建的元素副本添加到队列的末尾。
   - 当你想要将一个已经存在的对象添加到队列中时，使用`push`方法是合适的。

   示例：

   ```
   cppCopy codestd::queue<int> q;
   int value = 42;
   q.push(value); // 添加一个整数副本到队列中
   ```

2. **`emplace`方法**：

   - `emplace`方法允许你在队列中构造新元素，而不是将现有元素的副本添加到队列。
   - 你需要传递构造元素所需的参数给`emplace`方法，它会在队列内部构造新元素。
   - `emplace`通常比`push`更高效，因为它避免了元素的拷贝操作。

   示例：

   ```
   cppCopy codestd::queue<std::pair<int, std::string>> q;
   q.emplace(1, "one"); // 使用参数构造一个新的pair对象并将其添加到队列中
   ```

## lambda

表达式一般为：

```
[捕获列表](参数列表) -> 返回类型 {
    函数体
}
```

- `捕获列表`：指定外部变量，以供 lambda 表达式内部使用。可以为空，表示不捕获任何外部变量，或者使用 `[变量名]` 或 `[=]` 等方式捕获变量。
- `参数列表`：类似于函数的参数列表，指定 lambda 表达式的输入参数。
- `返回类型`：指定 lambda 表达式的返回类型。可以省略，让编译器自动推导返回类型。
- `函数体`：lambda 表达式的实际代码块。



省略返回类型的 lambda 表达式（让编译器自动推导，常见！）：

```
[外部变量](参数列表) {
    // 函数体
}
```

### []捕获

提供的 lambda 表达式如果没有使用捕获列表，这意味着它没有捕获任何外部变量。在这种情况下，lambda 表达式中的代码只能访问其参数，而不能访问任何外部变量。



捕获所有外部变量，自动推导参数和返回类型的 lambda 表达式：

```
[=]() {
    // 函数体
}
```

捕获外部变量并使用引用，指定参数和返回类型的 lambda 表达式：

```
[&外部变量](参数列表) -> 返回类型 {
    // 函数体
}
```



示例代码：

```c++
    std::vector<int> numbers = {5, 2, 8, 1, 9};

    // 使用 lambda 表达式作为比较函数来排序向量
    std::sort(numbers.begin(), numbers.end(), [](int a, int b) {
        return a < b; // 按升序排列
    });
```



```c++
[&](const int i, const int j) {
    return nums[i] > nums[j];
}

```

- `[&]`: 捕获列表，表示捕获外部的所有变量。在这个 lambda 表达式中，它捕获了你之前定义过的 `nums` 向量。
- `(const int i, const int j)`: 参数列表，指定了两个整数参数 `i` 和 `j`，用于进行比较。
- `return nums[i] > nums[j];`: 函数体，表示比较 `nums[i]` 和 `nums[j]` 的值，如果前者大于后者则返回 `true`，否则返回 `false`。

### 立即执行

```c++
int init = []() {
    for (int i = 2; i < MX; i++)
        if (omega[i] == 0) // i 是质数
            for (int j = i; j < MX; j += i)
                omega[j]++; // i 是 j 的一个质因子
    return 0;
}();
```

`()`：这是立即调用 lambda 表达式的语法。将 `()` 放在 lambda 表达式的后面，就会立即执行这个 lambda 函数，并返回结果。

### 值/引用方式

值方式

```c++
int y = 30;
auto lambda = [y]() {
    // 使用 y 作为值捕获的外部变量
    // 修改 lambda 内部的 y 不会影响外部变量
};

```

`y` 被以值的方式捕获，lambda 内部的 `y` 是外部变量 `y` 的一个副本，修改 lambda 内部的 `y` 不会影响外部变量。

```
auto lambda = [&](int p) {
    // 捕获所有外部变量以引用方式
    // 除了参数 p，它是以值方式传递的
};

```

`[&]` 指示以引用方式捕获所有外部变量。但需要注意，如果在 lambda 表达式内部使用了一个在 lambda 内未命名的变量（如上例中的 `p`），它将默认以值方式捕获。



### dfs写法

不能偷懒用auto 描述该变量，会编译错误

如下;

```
   auto dfs = [&](int node){
        vised.insert(nums[node]);
        for(auto& son : g[node]){
            if(vised.find(nums[son]) == vised.end())dfs(son);
        }
    };
```

改成

```
    function<void(int)> dfs = [&](int node){
        vised.insert(nums[node]);
        for(auto& son : g[node]){
            if(vised.find(nums[son]) == vised.end())dfs(son);
        }
    };
```



## 函数对象

Func关键字，将函数传入不同函数

```c++
#include <iostream>
#include <vector>

template <typename Func>
void processData(const std::vector<int>& data, Func func) {
    for (int value : data) {
        func(value);
    }
}

struct PrintSquare {
    void operator()(int x) const {
        std::cout << x * x << " ";
    }
};

struct PrintDouble {
    void operator()(int x) const {
        std::cout << x * 2 << " ";
    }
};

int main() {
    std::vector<int> nums = {1, 2, 3, 4, 5};
    
    // 使用不同的函数对象来处理数据
    processData(nums, PrintSquare());
    std::cout << std::endl;
    
    processData(nums, PrintDouble());
    std::cout << std::endl;
    
    return 0;
}

```

## set

C++中set既可以实现快速查找，又可以实现排序，具体数据结构信息如下：

1. **普通set**：这是最基本的set类型，它提供了基本的插入、删除、查找等操作，并且会自动排序。
2. **multiset**：与set类似，但允许重复元素。
3. **set_map**：一种关联容器，提供类似map的功能，但是键值对的键是有序的。实际上，set_map就是有序版本的map。
4. **multiset_map**：一种关联容器，提供类似multimap的功能，键值对的键是有序的，且允许重复键。
5. **unordered_set**：无序集合，元素插入和删除的复杂度为O(1)，查找的复杂度为O(n)，它实际上是一个哈希表实现的集合。
6. **unordered_multiset**：无序集合，允许重复元素，元素插入和删除的复杂度为O(1)，查找的复杂度为O(n)。
7. **map**：关联容器，它包含键值对，并且可以根据键值进行查找、插入、删除等操作。
8. **multimap**：关联容器，与map类似但允许重复键值对。
9. **unordered_map**：关联容器，无序存储键值对，键唯一，插入、删除、查找等操作的复杂度通常比map快。
10. **unordered_multimap**：关联容器，与unordered_map类似但允许重复键值对。

其中细节犯错：



```c++
multiset<int> prices;
int pre = timePriceMap[timestamp];
prices.erase(pre);//会删除所有的等于pre的值
```

要想只删除一个，使用迭代器

```c++
multiset<int> prices;
int pre = timePriceMap[timestamp];
auto it = prices.find(pre);
prices.erase(it);
```



## map



通过数组，自己构建哈希表

好处明显：可以方便控制哈希表里的元素

### 重复key

multimap

插入元素，必须用insert  {  }, 并且同map一样，是有序的

```c++
multimap<int, int> left_id;
left_id.insert({left, res});
```



### 哈希冲突

Quadratic probing（平方探测/二次探测）：如果发生冲突，就+1，+4, +9



### find()

查找是否存在

```C++
 if (proxy.find(s) != proxy.end()) {}
```



### count()

```C++
if (agent.count(temp) == 1){}
```

`std::unordered_map`或`std::map`类的成员函数，用于返回容器中键为`m`的元素数量

而不是值的数据

### 遍历数据

```C++
for (auto& it : agent) {// 要修改其中的元素，必须使用&，别名，类似指针
    it.second = true;
}
```





### unordered_map细节

```C++
unordered_map<string, int> mat;
for(auto& it : words){
    mat[it]++;
}
```

可以使用方括号访问键对应的值 `map[key]`。需要注意的是，如果该 `key` 不存在，C++ 会自动创建这个 key，并把 `map[key]` 赋值为 0。



## String

### string

```c++
//头文件
#include<string>
string line;
string s(p, ' ');//获得p长度的字符串
```



### 值语义

```C++
int main(){ 
    string s = "wzt";
    vector<string> res;
    res.push_back(s);
    s += "sk";
    // generateParenthesis(3);

}

```

res中不会被更改



### 部分字符

i:index ,n  截取字符的长度

!!! n是字符串截取的长度

```C++
s.substr(i,n)
```



### string->int

```c++
string  temp1(num,i, K);
int temp2 = atoi(temp1.c_str());
```

简单的

使用stoll()函数，转化为为long long型数字

```c++
#include<string>
a = stoll(s.substr(0, l / 2));
b = stoll(s.substr(l / 2, l / 2));
```

stol()转化为int型数字

### int->string

```C++
to_string(1223);
```



### 字符串拼接

<img src=".\image\string.png" alt="string" style="zoom: 80%;" />

1、k+=b比k=k+b效率更高，因为右边的等式是先生成一个新的string再进行赋值

2、char型是基础数据类型，没有进行重载，两个char进行相加不是字符串拼接，所以要想字符串拼接，+左右必须有一个string类型

![string拼接](.\image\string拼接.png)



append与+=的效率比较

```c++
s += words[j] + " ";
```

将 `words[j]` 和一个空格字符串拼接起来，然后将结果附加到字符串 `s` 的末尾。这个操作会创建一个新的字符串，其中包含 `words[j]`、一个空格字符，以及 `s` 的内容。然后，它将 `s` 的内容替换为这个新字符串。

这种方式每次循环都会创建一个新的字符串，这可能会导致额外的内存分配和复制操作。从效率的角度来看，如果需要频繁地执行这种操作，可能会引入一些性能开销。



所以应该换成

```C++
s.append(words[j]);
s.push_back(' '); // 或者使用 s.append(" ");
```

使用push_back更好，统一所有数据结构

### char <-> int

```c++
//char->int
char c = '0';
int i3 = c - '0';              // 0
```

显然，int->char则是反过来即可

```c++
//char->int
int i3 = 0;
char c = i3+ '0';              // 0
```



### 比大小

char类型就直接比较ASCLL值。
字符串类型比较大小：
1：首先比较字符串中的第一个字符的ASCLL值。
2：如果第一个字符相同，则比较第二个字符仍相同，则比较第三……比较第N个字符，直至有不相同。
3：如果字符串长度不等，如(James和Jan)作比较，也取决于ASCLL值，两个字符串的前面两个字母都相同，则比较第三个，因为n的ASCLL值比m的大，所以Jan>James;
4：如果两个字符串比较到末尾还没出现不匹配，则比较短字符串被认为较小。





比较方式

1.比较符号> ,<,=

2.compare(）

```c++
#include <iostream>
using namespace std;
int main(){
	string str1="hello";
	cout<<str1.compare("helloo")<<endl;//返回-1； 
    cout<<str1.compare("hello")<<endl;//返回0 ； 
	cout<<str1.compare("hell")<<endl;//返回1； 
} 
```

3.strcmp（）

```c++
//原型extern int strcmp(const char *s1,const char *s2);
cout<<strcmp(str1,str2)<<endl;//返回1； 
cout<<strcmp(str1,str3)<<endl;//返回-1； 
cout<<strcmp(str1,str4)<<endl;//返回0. 
```



### 分割-stringstreamn

c++中没有split函数



`std::stringstream` 对象 `ss` 中。然后，我们使用 `std::getline` 函数从 `ss` 中提取每个单词，以空格 `' '` 作为分隔符。每次提取都将一个单词存储在 `word` 变量中，然后输出到标准输出。

可以根据需要修改分隔符，例如使用逗号、分号等，只需将 `std::getline` 的第三个参数更改为所需的分隔符。这样，你就可以轻松地拆分字符串并处理其中的各个部分。

```c++
#include <iostream>
#include <string>
#include <sstream>

int main() {
    std::string inputString = "Hello World How are you";
    std::stringstream ss(inputString); // 将字符串放入 stringstream 中

    std::string word;
    while (std::getline(ss, word, ' ')) {
        std::cout << word << std::endl;
    }

    return 0;
}

```

默认是空格，可以这么写：

``` c++
int main() {
    std::string inputString = "Hello World How are you";
    std::stringstream ss(inputString); // 将字符串放入 stringstream 中

    std::string word;
    while (ss >> word) {
        std::cout << word << std::endl;
    }

    return 0;
}

```



**stringstream**

主要是读入字符串，格式转化

```c++
#include <sstream>  
#include <iostream>  
  
int main() {  
    std::stringstream ss;  
  
    int num = 123;  
    ss << num;    // 向stringstream中写入一个数字  
    std::string str = ss.str();    // 从stringstream中读取，现在str是"123"  
  
    std::cout << "str: " << str << std::endl;  
    return 0;  
}
```

```c++
#include <sstream>  
#include <fstream>  
#include <string>  
#include <iostream>  
  
int main() {  
    std::ifstream file("test.txt");  
    std::stringstream ss;  
    ss << file.rdbuf();    // 读取整个文件并写入到stringstream中  
  
    std::string str = ss.str();    // 从stringstream中读取，现在str是文件的内容  
    std::cout << "str: " << str << std::endl;  
  
    return 0;  
}
```



## algorithm

### min_element

查找数组内最小的元素

```c++
#include <iostream>
#include <algorithm>
#include <vector>

int main() {
    std::vector<int> numbers = {3, 1, 4, 1, 5, 9, 2, 6, 5, 3, 5};
    
    // 使用 min_element 查找最小元素的迭代器
    std::vector<int>::iterator minIt = std::min_element(numbers.begin(), numbers.end());
    
    // 输出最小元素的值
    std::cout << "The minimum element is: " << *minIt << std::endl;
    
    return 0;
}

```



### find函数

`std::vector` 并没有提供 `find` 方法，具体使用如下

```c++
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    int n = 10; // 假设 n 是你的向量的大小
    int a = 2; // 假设 a 是你要查找的向量的索引
    int b = 42; // 假设 b 是你要查找的值

    std::vector<std::vector<int>> map(n + 1);

    // 使用 std::find 查找 b 是否存在于 map[a]
    auto it = std::find(map[a].begin(), map[a].end(), b);

    if (it != map[a].end()) {
        // 找到了 b，可以在这里处理它的存在
        std::cout << "Found b in map[a]" << std::endl;
    } else {
        // 没找到 b，可以在这里处理它的不存在
        std::cout << "Did not find b in map[a]" << std::endl;
    }

    return 0;
}

```



### reverse函数

头文件

```C++
#include <algorithm>
```

详情，用于反转在[first,last)范围内的顺序（包括first指向的元素，不包括last指向的元素），reverse函数没有**返回值**

显然，[ left,right),right-left  才会刚刚好等于区间大小

reverse函数反转string

```c++
string N;
cin>>N;
reverse(N.begin(), N.end());
```



reverse函数反转字符数组

```C++
char s[101];
cin.getline(s,sizeof(s));
int m=strlen(s);
reverse(s,s+m);
puts(s);

```

reverse函数反转整型数组

```c++
int a[100];
reverse(a,a+10);         //第二个参数是数组最后一个元素的下一个地址
```



### 排序sort

头文件

```c++
#include<algorithm>
```

二维基础数组不好使用sort排序

#### 一维度数组

从大到小排序，n是待排序数组元素个数

```c++
bool cmp(int a,int b){
	return a>b;
}
sort(a,a+n,cmp);
```

一维其他类型数组同理

![排序_char](.\image\排序_char.png)

#### 二维数组排序

使用结构体（直接使用数组会报错）

```c++
struct Number
{
	int n;
	int A;
};	
Number out[200];

bool cmp(Number a, Number b)
{
	if (a.n != b.n) return a.n < b.n;
	if (a.A != b.A) return a.A < b.A;
	/*if (a[2] != b[2]) return a[2] > b[2];*/
}

```



使用vector

```c++
#include <vector>
struct node {
    int n, a;
};

bool cmp(node& a, node& b) {
    if (a.n != b.n)return a.n < b.n;
    return a.a < b.a;
}
vector<node> v;
v.push_back({ d,c });
sort(v.begin(), v.end(), cmp);
 
```

细节：不可以直接同普通数组一样使用地址



```
sort(intervals.begin(), intervals.end(), [](const vector&lt;int&gt;&amp; u, const vector&lt;int&gt;&amp; v) {
            return u[0] &lt; v[0] || (u[0] == v[0] &amp;&amp; u[1] &gt; v[1]);
            });
```



## 必知必会函数

### 求最大公约数

辗转相除法

记忆 ，可以让大数小数交换位置，gcd左边是被除数，右边是除数

```c++
int gcd(int a,int b){
	return b==0?a:gcd(b,a%b);
}
```

### 求质数

```c++
#include<algorithm>
bool isprime(int n){
	if(n<3)return false;
    int x = sqrt(n);
	for(int i=2;i<=x;i++){
		if(n%i==0)return false;
	}
	return true;
}
```

反转链表

```java
// 单链表节点的结构
public class ListNode {
    int val;
    ListNode next;
    ListNode(int x) { val = x; }
}
// 定义：输入一个单链表头结点，将该链表反转，返回新的头结点
ListNode reverse(ListNode head) {
    if (head == null || head.next == null) {
        return head;
    }
    ListNode last = reverse(head.next);
    head.next.next = head;
    head.next = null;
    return last;
}
```



### 将字符串全部大小写化

```C++
int j=0;
while(j<sn.size()){
    sn[j]=tolower(sn[j]);
     j++;
}
```

```C++
int j=0;
while(j<sn.size()){
    sn[j]=toupper(sn[j]);
     j++;
}
```

### max

```c++
            if((hash[i] & hash[j]) == 0){
                ans = max(ans, int(words[i].size() * words[j].size()));
            }
```



## 迭代器必知必会

### find

set、map的find函数

找到了返回确切的迭代器位置

否，返回   .end()



## 细节避坑

1. 对于浮点数比较大小，注意要先浮点数相加，再比较，不能直接整数相加
2. 题目更考察的是验证类问题，直接求解答案的问题更少
3. break只能结束当前循环体
4. 注意，如果题目通过率很高，自己也通过了测试点，却依旧不知道是哪里错误，记得多编几个测试点
5. 重载操作符能相当于排序。注意set用迭代器遍历的时候，访问到的数据成员是常量，不能赋值的。所以如果要改的话就得删除、再插入一个新的。
6. 为了代码的可读性，减少使用break,continue控制代码的输出，用复杂度，换可读性，换少bug
7. 当数组的下标从1开始，一定要万分注意，尤其有可能出错
8. 对于题目的理解不够精准，of的理解更准确，of要准确定位到描述的对象
9. 对于除法的比较大小，可以转化为乘法比较
10. 树的NLR prefix前序遍历，或者LRN postfix后序遍历，注意要先观察测试集，有右结合的符号，比如“-”，1162



## 整体思维过程与刷题模式

1、用什么数据结构存储数据，要考虑到之后要用这些数据做哪些处理

2、处理数据，注意边界

3、输出结果

### 刷题模式

解释几个名词



oj平台 ：online judge，即线上评测

核心代码模式 ： 如leetcode

acm模式：如pat，如洛谷，如牛客网





## 数组技巧

### 双指针

无非就是快慢指针，和双向而行两种情况

其实更加套路的讲，对于**需要双层遍历数据**，i -> [0, n],  j ->[i+1, n] 的情况，完全可以考虑双指针双向而行，或者从中心往两边穷举，能够将for两次变成for一次

题目参考：接雨水，找两数之和为0，寻找最长回文子串，都是n^2穷举

### 滑动窗口

模板

```c++
/* 滑动窗口算法框架 */
void slidingWindow(string s) {
    // 用合适的数据结构记录窗口中的数据
    unordered_map<char, int> window;
    
    int left = 0, right = 0;
    while (right < s.size()) {
        // c 是将移入窗口的字符
        char c = s[right];
        window.add(c)
        // 增大窗口
        right++;
        // 进行窗口内数据的一系列更新
        ...

        /*** debug 输出的位置 ***/
        // 注意在最终的解法代码中不要 print
        // 因为 IO 操作很耗时，可能导致超时
        printf("window: [%d, %d)\n", left, right);
        /********************/
        
        // 判断左侧窗口是否要收缩
        while (left < right && window needs shrink) {
            // d 是将移出窗口的字符
            char d = s[left];
            window.remove(d)
            // 缩小窗口
            left++;
            // 进行窗口内数据的一系列更新
            ...
        }
    }
}

```

指针 `left, right` 不会回退（它们的值只增不减），所以字符串/数组中的每个元素都只会进入窗口一次，然后被移出窗口一次，不会说有某些元素多次进入和离开窗口，所以算法的时间复杂度就和字符串/数组的长度成正比。这才是为O(n)算法的魅力，不需要再苦哈哈的遍历窗口里面的数据

细节：

**现在开始套模板，只需要思考以下几个问题**：

1、什么时候应该移动 `right` 扩大窗口？窗口加入字符时，应该更新哪些数据？

2、什么时候窗口应该暂停扩大，开始移动 `left` 缩小窗口？从窗口移出字符时，应该更新哪些数据？

3、我们要的结果应该在扩大窗口时还是缩小窗口时进行更新？

### 顺序放数据入包

将数组按顺序放入包中，且包的大小固定为x，放入数据和小于等于x；

没有数据时直接放回，有数据初始化包为1，要往里面放数据

```c++
if(nums.size() == 0)return 0;        
int need = 1, sum =0, s = nums.size();//一定存在数据，先开了一个包
        for(int i = 0; i < s; ++i){
            if(sum + nums[i] > x){
                need++;
                sum = nums[i];
            }else sum += nums[i];
        }
        return need;
```



### 区间和各类问题

数组不变，求区间和：「前缀和」、「树状数组」、「线段树」
多次修改某个数（单点），求区间和：「树状数组」、「线段树」
多次修改某个区间，输出最终结果：「差分」
多次修改某个区间，求区间和：「线段树」、「树状数组」（看修改区间范围大小）
多次将某个区间变成同一个数，求区间和：「线段树」、「树状数组」（看修改区间范围大小）



## bfs/dfs

### 选择

- 如果问题可以建模成图，例如寻找从一个节点到另一个节点的最短路径或寻找图中的连通组件，通常使用BFS更合适。
- 如果问题涉及到搜索整个状态空间，如在搜索问题中，通常使用DFS。

### 细节

考虑当前子节点，但是考虑的都是最小的子问题，一定要将当前节点的所有子问题穷尽



### dfs/回溯/动态规划



dfs优先以树为例子，进入节点，然后出节点，当前代码关注点在于这个节点

回溯不同，以排列组合/8皇后为例子，当前代码重点在于选择，选择哪一个点入，然后出这个点，撤销入这个点的状态，然后再入下一个点，所以写在for循环里面

```C++


// DFS 算法，关注点在节点
void traverse(TreeNode* root) {
    if (root == nullptr) return;
    printf("进入节点 %s", root);
    for (TreeNode* child : root->children) {
        traverse(child);
    }
    printf("离开节点 %s", root);
}

// 回溯算法，关注点在树枝
void backtrack(TreeNode *root) {
    if (root == nullptr) return;
    for (TreeNode* child : root->children) {
        // 做选择
        printf("从 %s 到 %s", root, child);
        backtrack(child);
        // 撤销选择
        printf("从 %s 到 %s", child, root);
    }
}

```

动态规划，如斐波那契，如打家劫舍（区间子问题），关注的是子问题，其实同二叉树的后序遍历代码架构很相似

​	简单，比如计算二叉树的节点个数，直接关注子问题count(n) = count(n->left) +count(n->right)+1;

​	f(n)=max{f(n-1)， f(n-2) + nums[n]}等待子问题的一步一步推导

```c++
int count(TreeNode* root){
	if(root == nullptr)return 0;
	return count(root->left) + count(root->right) + 1;//
}
```

总结

- **动态规划算法属于分解问题的思路，它的关注点在整棵「子树」**。
- **回溯算法属于遍历的思路，它的关注点在节点间的「树枝」**。
- **DFS 算法属于遍历的思路，它的关注点在单个「节点」**。

## tree

树就是两种代码框架（dfs前中后序/层次遍历），两种思维框架（分解/遍历）

**二叉树的所有问题，就是让你在前中后序位置注入巧妙的代码逻辑，去达到自己的目的，你只需要单独思考每一个节点应该做什么，其他的不用你管，抛给二叉树遍历框架，递归会在所有节点上做相同的操作**

**dfs核心思想，只思考当前节点应该干的事**

### 代码框架

```c++
void traverse(TreeNode* root) {
    if (root == nullptr) {
        return;
    }
    // 前序位置
    traverse(root->left);
    // 中序位置
    traverse(root->right);
    // 后序位置
}

```

### 核心思想

遇到一道二叉树的题目时的通用思考过程是：

**1、是否可以通过遍历一遍二叉树得到答案**？如果可以，用一个 `traverse` 函数配合外部变量来实现。

**2、是否可以定义一个递归函数，通过子问题（子树）的答案推导出原问题的答案**？如果可以，写出这个递归函数的定义，并充分利用这个函数的返回值。

**3、无论使用哪一种思维模式，你都要明白二叉树的每一个节点需要做什么，需要在什么时候（前中后序）做**。

### 遍历/分解比较

<img src=".\image\leet-1123.png" alt="leet-1123" style="zoom:80%;" />

使用遍历思想，比较复杂，（先入为主的思想）

后序位置考虑两种情况，容易出错

```c++
TreeNode * res; int m = -1;
int dps(TreeNode* root, int h){//传入的是当前的深度，返回当前以当前节点的深度
    if(root == nullptr)return h-1;
    int l = dps(root->left, h+1);
    int r = dps(root->right, h+1);
    if(l >= m && l == r){//考虑两种情况，容易出错，不便于理解
        res = root;
        m = l;
    }
    return max(l , r);
}
TreeNode* lcaDeepestLeaves(TreeNode* root) {
    dps(root, 0);
    return res;
}
```

官方答案（使用分解方式），对于返回值没想到，最大深度，从后往前迭增想到了

```c++
pair<TreeNode*, int> dfs(TreeNode* node){
    if(node == nullptr)return {node, -1};
    pair<TreeNode*, int> l = dfs(node->left);
    pair<TreeNode*, int> r = dfs(node->right);
    //谁深返回谁的子节点
    if(l.second > r.second)return {l.first, l.second+1};
    else if(l.second < r.second)return {r.first, r.second+1};
    //一样深，返回当前子节点
    return {node, l.second+1};
}
TreeNode* lcaDeepestLeaves(TreeNode* root) {
    return dfs(root).first;
}
```

结论：分解比较难想，但是代码简洁，可读性强

品味一下后序位置的特点，只有后序位置才能通过返回值获取子树的信息。**一旦你发现题目和子树有关，那大概率要给函数设置合理的定义和返回值，在后序位置写代码了**

a、**先判断要不要子树信息**，要的话，就是后序

b、要后序写代码，

​	1.直接思考当前节点需要什么子树信息，就可以推导出当前节点的返回值（子树应该返回的信息），

​	2.并且针对拿到的子树信息处理的，写出当前后序的逻辑代码

### 套路

分解一般都是后序，后序的返回值，深度非常常见，4/5用深度

分解思考方法**之一**，子树已经解决了题目的问题，并且返回问题要求的答案（问题解）



### 序列化

<img src=".\image\leet-652.png" alt="leet-652" style="zoom:67%;" />

要比对字符串，最重要的要思考到树的序列化

要知道当前节点为根的树的模样，所以只能**后序遍历**



并且再进行字符串拼接的时候，**不能使用中序**，**非数字的特殊符`#`表示空指针，并且用字符`,`分隔每个二叉树节点值**，这属于序列化二叉树的套路了

0                                                  0

​    \                                             /

​      0                                       0

中序拼接：#0#0#   #0#0# 

前序拼接：0#0##   00###   

后序拼接：###00   ##0#0  

给出空指针可以容易反序列化



### 前缀树

是一种多叉树，但是这种树很特殊，一般的树节点存储的都是值，但是前缀树，在树杈上存储节点值

```c++
struct TrieNode {
    bool isEnd; //该结点是否是一个串的结束
    TrieNode* next[26]; //字母映射表
};


```



```c++
class Trie {
private:
    bool isEnd;//判断是否以该点作为结尾
    Trie* next[26];
public:
    Trie() {
        isEnd = false;
        memset(next, 0, sizeof(next));//指针初始化0
       	//memset 是用于设置内存块的值，而 nullptr 是一个空指针常量，不是一个表示内存中的具体数值。因此，memset 无法直接用 nullptr 来初始化指针数组。

		//在C/C++中，nullptr 通常是一个空指针，它的二进制表示通常是全0，但这并不是由 memset 来设置的。
    }
}
```



## 贪心

最重要的不是证明，是解决这道题目

局部最优推导全句最优，有时候策略没有那么常识，可以举反例，如果没有，就证明策略没问题

## 并查集

模板

```C++
int father[1000];
int findfather(int v){
	return v==father[v]?v:(father[v]=findfather(father[v]));
}
void u(int a, int b) {
	int faA = findfather(a);
	int faB = findfather(b);
	if (faA < faB) {
		father[faA] = faB;
	}
	else if (faA > faB) {
		father[faB] = faA;
	}
}
```





## 回溯

### N皇后

不是简单的数据结构题目

还有如何摆脱重复数据的去重



## 动态规划

### 通用技巧

首先要判断具备**选择**的状态是什么，视角要站在状态上，往后看，往可以到达这个状态的回头看，就能清晰知道状态转移方程

也就是说，明白dp是啥，这道题就解决一半，dp的定义是最重要的

零钱兑换

**1、确定 base case**，这个很简单，显然目标金额 `amount` 为 0 时算法返回 0，因为不需要任何硬币就已经凑出目标金额了。

**2、确定「状态」，也就是原问题和子问题中会变化的变量**。由于硬币数量无限，硬币的面额也是题目给定的，只有目标金额会不断地向 base case 靠近，所以唯一的「状态」就是目标金额 `amount`。

**3、确定「选择」，也就是导致「状态」产生变化的行为**。目标金额为什么变化呢，因为你在选择硬币，你每选择一枚硬币，就相当于减少了目标金额。所以说所有硬币的面值，就是你的「选择」。

**4、明确 `dp` 函数/数组的定义**。我们这里讲的是自顶向下的解法，所以会有一个递归的 `dp` 函数，一般来说函数的参数就是状态转移中会变化的量，也就是上面说到的「状态」；函数的返回值就是题目要求我们计算的量。就本题来说，状态只有一个，即「目标金额」，题目要求我们计算凑出目标金额所需的最少硬币数量。

### 子序列问题

通用base， 状态就是一段序列的数组





然后注意转递归操作时，背包问题，子序列问题都是，i ，j都是 1~m， 实际数据 0~m-1







## 二分法搜索

### 搜索左边界

搜索等于目标值的最左边界

搜索大于等于目标值最左边界

### 搜索右边界

搜索等于目标值的最右边界

搜索小于等于目标值的最右边界



```C++
int findLeft(vector<int>& nums, int target){
    int left = 0, right = nums.size();
    while(left < right){
        int mid = left + (right - left)/2;
        if(nums[mid] == target){
            right = mid;
        }else if(nums[mid] > target){
            right = mid;
        }else{
            left = mid + 1;
        }
    }
    if(left < 0 || left >= nums.size())return -1;
    return nums[left] == target ? left : -1;
}
int findRight(vector<int>& nums, int target){
    int left = 0, right = nums.size();
    while(left < right){
        int mid = left + (right - left)/2;
        if(nums[mid] == target){
            left = mid + 1;
        }else if(nums[mid] > target){
            right = mid;
        }else{
            left = mid + 1;
        }
    }
    if(left - 1 < 0 || left - 1 >= nums.size())return -1;
    return nums[left-1] == target ? left-1 : -1;
}
vector<int> searchRange(vector<int>& nums, int target) {
    if(nums.size() == 0)return {-1, -1};
    int l = findLeft(nums, target);
    int r = findRight(nums, target);
    return {l, r};
}
```

细节：寻找右边界时，要left-1,因为终止条件时left == right, 由[r-1, r)发展而来，l = l+1后，l==r，并且由于r全程到尾都没有等同于mid，只存在空与大于t的可能性

### 实际技巧

一旦出现最大值最小，就往二分法上面套



第一步读题，转化题意为      满足`f(x) == target`的`x`的最小值（左边界）/最大值（右边界）是多少 ，（确定搜索左边还是右边）

第二步 **确定`x, f(x), target`分别是什么，并写出函数`f`的代码**。 显然x就是题目要求出的值，再移动x，变化x的大小，看一看什么变量在随之变大或者变小

第三步 **找到`x`的取值范围作为二分搜索的搜索区间，初始化`left`和`right`变量**。

代码框架

```c++
// 函数 f 是关于自变量 x 的单调函数
int f(int x) {//一般改写成lambda
    // ...
}

// 主函数，在 f(x) == target 的约束下求 x 的最值
int solution(int[] nums, int target) {
    if (nums.length == 0) return -1;
    // 问自己：自变量 x 的最小值是多少？
    int left = ...;
    // 问自己：自变量 x 的最大值是多少？
    int right = ... + 1;

    while (left < right) {
        int mid = left + (right - left) / 2;
        if (f(mid) == target) {
            // 问自己：题目是求左边界还是右边界？
            // ...
        } else if (f(mid) < target) {
            // 问自己：怎么让 f(x) 大一点？
            // ...
        } else if (f(mid) > target) {
            // 问自己：怎么让 f(x) 小一点？
            // ...
        }
    }
    return left;
}
```



## python语法规则

### 计算

```python
　6 // 4 = 1
 
　　6 / 4 =1.5
```



数据类型转化

字符串转为数字

```python
num_list=['1','2','3']

str_list = ''.join(num_str)  #把列表中的元素连起来

print(int(str_list))

输出

123

```



int(str)函数将符合整数的规定的字符串转换成int型的
float(str)函数将符合浮点型的规定的字符串转换成float型的
str(num)将整数、浮点型转换成字符串型的



### 文件

```python
directory_path = r'C:\Users\LZP\Desktop\青马班读书报告整理'
```

在打开文件的时候open(r'c:\....')

加r和不加''r是有区别的

'r'是防止字符转义的 如果路径中出现'\t'的话 不加r的话\t就会被转义 而加了'r'之后'\t'就能保留原有的样子

另外；字符串赋值的时候 前面加'r'可以防止字符串在时候的时候不被转义 原理是在转义字符前加'\'

r的含义是raw的意思

#### 编码出错

```
Traceback (most recent call last):
  File "D:\Project\Python\basestudy\file.py", line 2, in <module>
    print(f.read())
UnicodeDecodeError: 'gbk' codec can't decode byte 0xb5 in position 147: illegal multibyte sequence
```

原因：文件中含有中文

```python
f = open('../aiTest/trymmd.py', 'r',encoding="utf-8")
print(f.read())
```

utf-8的方式编码，文字->byte



## 数学基础

### 线性代数

对角矩阵，Anxn，并且数据集中于对角上

### mmd

MMD的基本思想就是，如果两个随机变量的任意阶都相同的话，那么两个分布就是一致的。而当两个分布不相同的话，那么使得两个分布之间差距最大的那个矩应该被用来作为度量两个分布的标准。





