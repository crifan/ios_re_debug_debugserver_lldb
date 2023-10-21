# debugserver

对于`debugserver+lldb`的调试方案来说，应该先介绍背景知识：

## LLDB的远程调试

* LLDB的远程调试
  * 涉及到2个端
    * `lldb client`
      * 运行在 local system
        * 比如PC端（`Linux`、`Mac`）的`lldb`命令行工具
    * `lldb server`
      * 不同平台
        * `Linux`和`Android`：`lldb-server`
          * 不依赖于`lldb`
            * 因为：已静态链接包含了`LLDB`的核心功能
            * 对比：`lldb`是默认是动态链接`liblldb.so`
        * `Mac`和`iOS`：`debugserver`
      * 运行在 remote system
        * 典型例子
          * iPhone中的：`debugserver`
          * Android中的：`lldb-server`
      * 实现了remote-gdb的功能
    * 两者通讯
      * 用的是：`gdb-remote`协议
        * 一般是在TCP/IP之上运行
  * 细节详见：
    * `docs/lldb-gdb-remote.txt`
  * 资料
    * 主页
      * Remote Debugging — The LLDB Debugger
        * http://lldb.llvm.org/use/remote.html

## debugserver

然后再来详细介绍：`debugserver`本身：

* `debugserver`
  * 是什么：一个终端的应用
    * 也是：`XCode`去调试iOS设备中程序时候的进程名
  * 在哪里：iOS设备中
    * 位置：`/Developer/usr/bin/debugserver`
    * 注：iOS中默认没安装debugserver
      * iOS何时安装了`debugserver`
        * 在设备连接过一次`Xcode`，并在`Window`->`Devices`中添加此设备后
          * `debugserver`才会被`Xcode`安装到`iOS`的`/Developer/usr/bin/`下
  * 作用：作为服务端，接受来自远端的`gdb`或`lldb`的调试
    * 可以理解为：`lldb`的`server`
  * 为何需要
    * iOS中，由于App运行检测到越狱后会直接退出，所以需要通过`debugserver`来启动程序
  * 通过`debugserver`来启动程序
    * 举例
      ```bash
      debugserver -x backboard 0.0.0.0:1234 ./*
      ```
      ```bash
      debugserver *:1234 -a "MoneyPlatListedVersion"
      ```
