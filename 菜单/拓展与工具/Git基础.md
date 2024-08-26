## 第一章、Git是什么

### 1.1 了解Git

Git是一个免费的、开源的`分布式版本控制系统`，可以高速处理从小型到大型的各种项目
版本控制：是一种记录文件内容变化，以便将来查阅特定版本修订情况的系统
了解一下：集中式与分布式版本控制工具

         -- 集中式版本控制工具：如CVS、`SVN`等，都有一个单一的几种管理服务器，保存所有文件的修订版本，而协同工作的人通过客户端连接到这台服务器，从而取出最新的文件或者提交更新。缺点：中央服务器的单点故障；多(程序员)对一(中央服务器)
    
         -- 分布式版本控制工具：如git,客户端取的不是最新的文件快照，而是把代码仓库完整的镜像下来到本地库(克隆/备份)

<font color="red">工作机制</font>

![img](https://longhaotuchuang.oss-cn-beijing.aliyuncs.com/img/202408261508147.png)

### 1.2 Git安装

> 官方网址：[Git](https://git-scm.com/)

点击下载： 

![img](https://longhaotuchuang.oss-cn-beijing.aliyuncs.com/img/202408261510274.png)

 找到对应电脑系统的网址： 

![img](https://longhaotuchuang.oss-cn-beijing.aliyuncs.com/img/202408261510464.png)

 配置选择，基本上一直下一步即可： 

![img](https://longhaotuchuang.oss-cn-beijing.aliyuncs.com/img/202408261511385.png)

 选择第一个就够使用：

![img](https://longhaotuchuang.oss-cn-beijing.aliyuncs.com/img/202408261511296.png)





## 第二章、Git常用命令 

### 2.1 常用命令

```json
git config --global user.name 用户名

设置用户签名

git config --global user.email 邮箱

设置用户签名

git init 

初始化本地库

git status

查看本地库状态

git add 文件名

添加到暂存区

git commit-m "日志信息" 文件名

提交到本地库

git reflog/git log

查看历史记录

git reset --hard 版本号

版本穿梭
```



### 2.2 基本操作

#### 2.2.1 打开git后端

（1）鼠标右键 --> Git Bash Here

![img](https://longhaotuchuang.oss-cn-beijing.aliyuncs.com/img/202408261512049.png)

 （2）找到自己新建的文件夹，然后鼠标右键 --> Git Bash Here(需要初始化文件)

![img](https://longhaotuchuang.oss-cn-beijing.aliyuncs.com/img/202408261512557.png)

#### 2.2.2 设置用户签名 

```mysql
git config --global user.name 浅风    设置用户签名
git config --global user.email 480364455@qq.com     设置用户签名
```

只需要首次配置就好了,如何查看配置成功，根据下面路径查看对应文件夹显示即可：

![img](https://longhaotuchuang.oss-cn-beijing.aliyuncs.com/img/202408261513633.jpeg)

#### 2.2.3 初始化本地库

```mysql
git init
```

![img](https://longhaotuchuang.oss-cn-beijing.aliyuncs.com/img/202408261513602.png)

#### 2.2.4 查看本地状态

```mysql
git status
```

![img](https://longhaotuchuang.oss-cn-beijing.aliyuncs.com/img/202408261514765.png)

#### 2.2.5 添加到暂存区

```mysql
git add 需要添加到暂存库的文件名
```

![img](https://longhaotuchuang.oss-cn-beijing.aliyuncs.com/img/202408261514294.png)

#### 2.2.6 提交到本地库

```mysql
git commit -m "日志信息（名字可以任意取）" 暂存区需要添加到工作区的文件名
```

![img](https://longhaotuchuang.oss-cn-beijing.aliyuncs.com/img/202408261515165.png)

#### 2.2.7 查看历史记录

```mysql
git reflog
git log
```

![img](https://longhaotuchuang.oss-cn-beijing.aliyuncs.com/img/202408261515806.png)

![img](https://longhaotuchuang.oss-cn-beijing.aliyuncs.com/img/202408261515546.png)

#### 2.2.8 版本穿梭

```mysql
git reset --hard 版本号（查看历史记录时候给的版本号）
```

修改文件：

![img](https://longhaotuchuang.oss-cn-beijing.aliyuncs.com/img/202408261515159.png)

切换版本：

![img](https://longhaotuchuang.oss-cn-beijing.aliyuncs.com/img/202408261516877.png)

### 2.3 分支操作

#### 2.3.1 分支的好处

 同时并进行多个功能开发，提高了开发效率
各个分支再开发过程中，如果某个分支开发失败，不会对其他分支有任何影响，失败的分支删除重新开始即可

#### 2.3.2 分支操作常用命令

```mysql
git branch 分支名      	   创建分支

git branch -v                查看分支

git checkout 分支名    	   切换分支

git merge 需要合并的分支名      把指定的分支合并到当前分支上
```



#### 2.3.3 查看分支

```json
git branch -v
```

![img](https://longhaotuchuang.oss-cn-beijing.aliyuncs.com/img/202408261517392.png)

#### 2.3.4 创建分支

```java
git branch 分支名  （相当于对主线分支的复制)
```

![img](https://longhaotuchuang.oss-cn-beijing.aliyuncs.com/img/202408261517513.png)

#### 2.3.5 切换分支

```mysql
git checkout 分支名
```

当前所在分支：

![img](https://longhaotuchuang.oss-cn-beijing.aliyuncs.com/img/202408261518682.png)

 切换后所在分支：

![img](https://longhaotuchuang.oss-cn-beijing.aliyuncs.com/img/202408261518977.png)

 查看分支内容->修改分支内容->该分支状态依旧从工作区到暂存区到本地库



![img](https://longhaotuchuang.oss-cn-beijing.aliyuncs.com/img/202408261518701.png)

![img](https://longhaotuchuang.oss-cn-beijing.aliyuncs.com/img/202408261518944.png)

![img](https://longhaotuchuang.oss-cn-beijing.aliyuncs.com/img/202408261519065.png)

#### 2.3.6 合并分支（正常合并）

```python
git merge 需要合并的分支名  //把指定的分支合并到当前分支上
```

该合并就是对比当前支线与需要合并的支线内容，将不同的内容合并一起 ；这种合并最重要的就是原分支不要做任何修改，只对需要合并的分支修改就好。

查看分支和主线的内容：

![img](https://longhaotuchuang.oss-cn-beijing.aliyuncs.com/img/202408261520860.png)

 合并后当前分支的内容：

![](https://longhaotuchuang.oss-cn-beijing.aliyuncs.com/img/202408261520167.png)

#### 2.3.7 合并分支（合并冲突）

**注意事项就是当前分支和合并的分支都不要同时修改，多人合作时，商量好，最好是等到上一个人合并好之后，下一个人再合并进去/提取出来**

![img](https://longhaotuchuang.oss-cn-beijing.aliyuncs.com/img/202408261520901.png)

需要手动合并—— 

查看内容：

![img](https://longhaotuchuang.oss-cn-beijing.aliyuncs.com/img/202408261520406.png)

手动合并，将更新的地方修改，然后放到本地库：

![img](https://longhaotuchuang.oss-cn-beijing.aliyuncs.com/img/202408261520200.png)

## 第三章、远程仓库的操作

码云：Gitee - 基于 Git 的代码托管和研发协作平台

### 1、注册账号、登录账号

### 2、新建仓库




![img](https://longhaotuchuang.oss-cn-beijing.aliyuncs.com/img/202408261520883.png)

![img](https://longhaotuchuang.oss-cn-beijing.aliyuncs.com/img/202408261521878.png)

![img](https://longhaotuchuang.oss-cn-beijing.aliyuncs.com/img/202408261521265.png)

### 3、从远程库拉取文件

对需要上传的文件内容，右键 --> Git Bush Here 
输入初始化命令 git init 回车

```mysql
git init
```

输入要链接到码云的地址,也就是上面图片需要记住的命令：`git remote add origin https://gitee.com/shallow-winds/test.git`（与码云链接很重要）

```mysql
git remote add origin https://gitee.com/shallow-winds/test.git
```

![img](https://longhaotuchuang.oss-cn-beijing.aliyuncs.com/img/202408261522382.png)

拉取码云上的所有文件到项目中来，`git pull origin master`

```mysql
git pull origin master
```

 得到的效果：

![img](https://longhaotuchuang.oss-cn-beijing.aliyuncs.com/img/202408261523268.png)

 

### 4、将文件上传到远程库

- 在命令行中继续输入代码执行 git add . (add空格后有个点别忘了，表示需要将所有的文件提交到暂存区) ：

```mysql
git add . （这一步是先添加到暂存区）
```

- 从暂存区添加到远程库，说明自己为什么要上传，方便以后自己查阅 git commit -m “第一次上传”

```mysql
git commit -m "第一次上传"
```

-  提交到码云上面，git push origin master

```mysql
git push origin (master/创建分支的名字)
```

 

![img](https://longhaotuchuang.oss-cn-beijing.aliyuncs.com/img/202408261525249.png)

上传成功的效果：


![img](https://longhaotuchuang.oss-cn-beijing.aliyuncs.com/img/202408261525846.png)