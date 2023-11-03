## 安装

* Windows

    ① 安装 Git for Windows

    https://git-for-windows.github.io/
    
    ② 使用git客户端
    
    https://git-scm.com/download/win
    
* Mac

    ① 用图形界面git安装工具安装
    
    http://sourceforge.net/projects/git-osx-installer/
    
    ② 用homebrew安装
    
        brew install git
        
* Fedora

        sudo yum install git-all

* Debian & Ubuntu

        sudo apt-get install git-all
       
        
* 源码编译安装

    ① 安装依赖工具
    
    * Fedora
    
            sudo yum install dh-autoreconf curl-devel expat-devel gettext-devel \
            openssl-devel perl-devel zlib-devel

    * Debian & Ubuntu
    
            apt-get install libcurl4-gnutls-dev libexpat1-dev gettext \
            libz-dev libssl-dev
    
    ② 下载git源码
        
    http://git-scm.com/download
    
    ③ 编译安装
    
        tar -zxf git-1.7.2.2.tar.gz
        cd git-1.7.2.2
        make prefix=/usr/local all
        sudo make prefix=/usr/local install

## 配置

* 设置本地git用户名和邮箱

        #用户名
        git config --global user.name "huihut" 
        
        #邮箱
        git config --global user.email "huihut@outlook.com" 
    
        #检查配置是否正确
        git config --list
        

* 生成SSH key

        ssh-keygen -t rsa -C "huihut@outlook.com"

    需要确认一些信息，一般默认就行。

* 获取ssh key

        #首先转换到git的默认的路径下，再cat
        
        cat ~/.ssh/id_rsa.pub
        
        #输出如下
        ssh-rsa AAAA....huihut@outlook.com

* 复制ssh-rsa...com到Github SSH keys上,如下图：


![](http://ojlsgreog.bkt.clouddn.com/githubsshkeys.png)


## 下载到本地仓库

* 用克隆命令（SSH or HTTPS）

        git clone git@github.com:huihut/huihut.github.io.git

一般推荐使用SSH，因为HTTPS一般来说`fetch`和`push`代码都需要输入账号和密码，比较麻烦，而且速度较慢；但是在某些只开放HTTP端口的公司内部就无法使用SSH协议而只能用HTTPS。

## 上传到远程仓库

* 新建远程仓库，如：`huihut.github.io`
* 终端进入本地仓库文件夹，如：

        cd /Users/xx/code/Github/huihut.github.io

* 初始化仓库

        git init
        
* 将本地的仓库和远程的仓库进行关联（SSH key ）

        git remote add origin git@github.com:huihut/huihut.github.io.git
    
* 新建文件或者修改文件

        touch test.txt

* 添加新建或修改的文件到仓库

        #添加特定文件  
        git add test.txt
        
        #添加此目录下全部文件
        git add .

* 将文件提交到仓库

        git commit -m "add test.txt"

* 将本地仓库的内容推送到远程仓库

        git push -u origin master

注意：第一次`push`的时候最好加上`-u`参数，这样git就会把本地master分支与远程的master分支关联起来，我们以后的`push`操作就不再需要加上`-u`参数了。


## 分支

### 新建分支

	git branch huihut
	
### 转换分支

	git checkout huihut
	
### 新建并转换分支

	git checkout -b huihut

### 分支合并

	# 把master分支合并到huihut分支
	git merge master huihut
	
### 查看分支

	git branch

### 删除分支

	git branch -d huihut

### 克隆指定分支

        git clone -b huihut git@github.com:huihut/huihut.github.io.git


## 查询

* 查看工作区和版本库里面最新版本的区别

        git diff HEAD -- readme.txt
        
* 查询状态

        git status

## 修改

* 丢弃工作区的修改

        git checkout -- readme.txt
        
* 清理仓库

		find . -name ".git" | xargs rm -Rf
		        

* 删除文件

        rm test.txt
    
* 删除文件夹（`-r`：向下递归；`-f`：强制删除）

        rm -rf /Users/xx/test

* 清空缓存

		git rm -r --cached . 

## 重置（删除提交记录）

* 从`master`创建并切换到新的分支`new_branch`

		git checkout --orphan new_branch

* 添加此目录下全部文件

		git add .

* 提交

		git commit -m 'init'

* 删除原来的`master`分支

		git branch -D master

* 把新分支`new_branch`重命名成`master`

		git branch -m  master

* 提交到远程分支

		git push -f origin master


## 大文件存储

Github 上传单个文件应该低于100M。上传文件超过50M会给予警告，超过100M则会不允许上传，这时可以使用`git lfs`上传。

[git-lfs 官网](https://git-lfs.github.com/)

### 安装 Git-LFS

	git lfs install
	
### 跟踪大文件

* 跟踪某类型文件
		
		git lfs track "*.psd"
	
* 跟踪多个文件
	
		git lfs track "aa.psd" "bb.pdf" "cc.zip"
	
### 确保gitattributes被跟踪

	git add .gitattributes
	
	# 可以在.gitattributes查看跟踪的文件
	cat .gitattributes

### 接下来步骤和平常一样

	git add .
	git commit -m "Add Large File"
	git push origin master


## 常见错误：

###  1. error: failed to push some refs to ....

#### 原因

问题的出现原因在于：git仓库中已经有一部分代码，所以它不允许你直接把你的代码覆盖上去。  

#### 解决

① 方法一：强推（`-f`），视情况加`-u`  
    
    git push -f -u origin master
    
②方法二：先把git的东西fetch到你本地然后merge后再push

    git fetch
    git merge
    
这两句等价于  

    git pull 

可是，这时候又出现了如下的问题：  

上面出现的 [branch "master"]是需要明确(.git/config)如下的内容  

    [branch "master"]

    remote = origin

    merge = refs/heads/master
    
这等于告诉git2件事:

1，当你处于master branch, 默认的remote就是origin。  

2，当你在master branch上使用git pull时，没有指定remote和branch，那么git就会采用默认的remote（也就是origin）来merge在master branch上所有的改变

如果不想或者不会编辑config文件的话，可以在bush上输入如下命令行：

    git config branch.master.remote origin 
    
    git config branch.master.merge refs/heads/master 

之后再重新git pull下

    git pull 

最后git push你的代码（视情况加`-u` ）

    git push -u origin master

### 2. fatal: The remote end hung up unexpectedly error: RPC failed; curl 56 SSL read: error:00000000:lib(0):func(0):reason(0), errno 10053

#### 表现：

```
Username for 'https://github.com': Newbie
Password for 'https://Newbie@github.com':
Counting objects: 11507, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (8210/8210), done.
Writing objects: 100% (11506/11506), 21.75 MiB | 0 bytes/s, done.
Total 11506 (delta 2213), reused 11504 (delta 2211)
efrror: RPC failed; result=56, HTTP code = 200
atal: The remote end hung up unexpectedly
fatal: The remote end hung up unexpectedly
Everything up-to-date
```

#### 原因

可能是git缓冲区太小

#### 解决

用`git config var`，将`http.postBuffer`设置为`524288000`来增加Git的HTTP缓冲区。
```
git config http.postBuffer 524288000
```
#### 参考

[Git push error: RPC failed; result=56, HTTP code = 200 fatal: The remote end hung up unexpectedly fatal](https://stackoverflow.com/questions/24952683/git-push-error-rpc-failed-result-56-http-code-200-fatal-the-remote-end-hun)

## Thanks

> [廖雪峰的官方网站 . Git教程](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)
>
>[YotrolZ的博客 . 本地Git仓库和远程仓库的创建及关联](http://www.jianshu.com/p/dcbb8baa6e36)
>
> [ConquerMobileApp博客 . git push用法和常见问题分析](http://www.cnblogs.com/renkangke/archive/2013/05/31/conquerAndroid.html)
> 
> [pringbarley博客 . git常用命令](http://www.cnblogs.com/springbarley/archive/2012/11/03/2752984.html)
>
> [git-lfs](https://git-lfs.github.com/)
