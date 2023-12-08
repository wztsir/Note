

# 瑞吉外卖

## day4

### 文件的上传

页面端：

![image-20220603111800747](C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220603111800747.png)





<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220603111915915.png" alt="image-20220603111915915" style="zoom:67%;" />



文件端：  

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220603112028001.png" alt="image-20220603112028001" style="zoom: 80%;" />

### 文件下载



<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220603112122099.png" alt="image-20220603112122099" style="zoom: 80%;" />

## git的使用

![image-20220607220311898](C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220607220311898.png)

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220607220715500.png" alt="image-20220607220715500" style="zoom:50%;" />

git不允许版本嵌套，所以初始化的目录结构不能嵌套



版本库中的信息，存放在index中

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220607225323634.png" alt="image-20220607225323634" style="zoom:80%;" />







git add <filename> 之后文件变为已跟踪（纳入版本控制）

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220607225453261.png" alt="image-20220607225453261" style="zoom:67%;" />





在纳入版本控制之后

git commit -m"init wzt.txt" wzt.txt

git log

细节：退出git log 状态**英文状态下按q ,即可退出**

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220607225751682.png" alt="image-20220607225751682" style="zoom:67%;" />

放入暂存区，变为绿色的字体，工作则为红色字体



git reset的作用

![image-20220607231540464](C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220607231540464.png)





细节的 要在仓库里面执行一系列的git命令，即有.git“虚文件”下的目录执行git操作

git remote 查看与远程仓库是否关联上，一开始需要确认一下

git remote -v 查看URL地址

git remote add origin(默认这个名字) <URL>

![image-20220608103237125](C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220608103237125.png)





git clone <URL>

细节，会在本地创建一个文件夹，文件夹内有.git  即存在git管理 ，所以要在还没被git管理的目录下使用git clone



提交到远程仓库

git push origin master

细节，需要身份认证 账号必须是仓库成员，才可以推送代码到仓库中，并且账号（不是真名）

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220608105512766.png" alt="image-20220608105512766" style="zoom:67%;" />





从远程仓库拉取

git pull origin master

细节的需要，提前查看是否关联了远程仓库，推送代码需要权限，但是拉取代码不需要权限，只要对方开源即可

![image-20220608110412076](C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220608110412076.png)

fatal: refusing to merge unrelated histories

本地仓库的历史，与远程仓库的历史没有合并

解决办法：git pull origin master --allow-unrelated-histories 

会进入vim的编辑，需要输入一次提交信息 i进入插入模式， esc退出编辑，:wq保存并退出







分支操作

![image-20220608112045992](C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220608112045992.png)





查看分支

![image-20220608112423367](C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220608112423367.png)

HEAD是分支的指针，指向了master分支

git branch b1 创建新分支

git checkout b1切换分支

git push origin b1   推送分支   提示信息，将本地的b1分支推送至远程的b1分支     * [new branch]      b1 -> b1

git merge -m "merge b1" b1 合并分支，细节的，首先切换回master分支，再合并





git 的冲突合并

1、手动修改文件

2、git add b1.txt

3、git commit -m "" b1.txt

细节的报错：fatal: cannot do a partial commit during a merge.

即冲突合并成功

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220608120333708.png" alt="image-20220608120333708" style="zoom:67%;" />







#### 标签

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220608161050743.png" alt="image-20220608161050743" style="zoom:67%;" />

git tag v0.1

git push origin v0.1    [shortName]远程仓库的名字，name为本地的版本名

检出标签，创建新的分支指向标签

标签的作用与分支的区别：标签是静态的，相当于照了一张相，开发出的版本v0.1,可以不断迭代



idea中使用以后再学吗

#### idea中使用git

<img src="C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220608163331588.png" alt="image-20220608163331588" style="zoom: 67%;" />

 本地初始化仓库

远程仓库克隆





gitignore的作用

![image-20220608164424321](C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20220608164424321.png)





## 部署服务器

自己解决的问题（课程之外的）

1、finalshell 乱码，重启finalshell

2、mysql连接的问题，直接尝试DG连接，由于mysql的版本过老，version不匹配，在DG的提示下完成配置





细节:防火墙需要firewall-cmd --reload，立即重启防火墙，立即生效



https://nodejs.org/dist/v16.18.0/node-v16.18.0.tar.gz





删除当前目录下的所有文件;  rm -f *

删除所有文件夹：        rm -rf + 路径/目录名





进入文件目录：usr/local/sh

执行代码：./bootStart.sh

