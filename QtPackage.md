# Qt程序打包发布方法（使用官方windeployqt工具）

## 添加windeployqt到环境变量

控制面板-系统和安全-系统-系统属性-高级-环境变量-系统变量-Path-编辑环境变量-新建-`E:\Qt\Qt5.7.0\5.7\msvc2015_64\bin`-确定

> 修改为你的windeployqt路径

## 添加qmldir到环境变量

控制面板-系统和安全-系统-系统属性-高级-环境变量-系统变量-Path-编辑环境变量-新建-`E:\Qt\Qt5.7.0\5.7\msvc2015_64\qml\QtQml`-确定

> 修改为你的qmldir路径

## Qt Widgets Application

用 QtCreator 新建一个 Qt Widgets Application 项目，以 Release 方式运行生成 exe 程序。

找到生成的exe程序，如`build-helloworld-unknown-Release\release\helloworld.exe`

复制exe文件到一个新建文件夹，如`C:\Users\huihu\Desktop\release`

打开cmd，`cd C:\Users\huihu\Desktop\release`

打包，`windeployqt helloworld.exe`

完成

## Qt Quick Application

用 QtCreator 新建一个 Qt Quick Application 项目，以 Release 方式运行生成 exe 程序。

找到生成的exe程序，如`build-helloworld-unknown-Release\release\helloworld.exe`

复制exe文件到一个新建文件夹，如`C:\Users\huihu\Desktop\release`

打开cmd，`cd C:\Users\huihu\Desktop\release`

打包，`windeployqt helloworld.exe --qmldir`

~~（打包，`windeployqt helloworld.exe --qmldir E:\Qt\Qt5.7.0\5.7\msvc2015_64\qml\QtQml`）~~

完成

## 链接

[Qt官方开发环境生成的exe发布方式--使用windeployqt](http://tieba.baidu.com/p/3730103947?qq-pf-to=pcqq.group)

[Qt 程序打包发布总结](http://blog.csdn.net/liuyez123/article/details/50462637)

### 知乎

[Qt 如何打包一个软件？](https://www.zhihu.com/question/21359230)

### 官方

[Deploying Qt Applications](http://doc.qt.io/qt-5/deployment.html)
[Qt for Windows - Deployment](http://doc.qt.io/qt-5/windows-deployment.html)
