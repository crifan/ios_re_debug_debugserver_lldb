# iPhone中用debugserver启动app

此处通过例子来介绍，iPhone中用debugserver启动iOS的app：抖音

## 概述

iPhone中用debugserver启动（抖音）app：

* Attach模式
  * 用PID：`debugserver 0.0.0.0:20221 -a 10194`
  * 用app名称：`debugserver 0.0.0.0:20221 -a "Aweme"`
* Spawn模式
  * `debugserver -x auto 0.0.0.0:20221 /private/var/xxx/Aweme.app/Aweme`

## 详解

* Attach模式：先手动启动app，再去用`debugserver`挂载`attach`
  * `-a`加上`PID`或`app名`
    * `PID`=进程ID
      ```bash
      debugserver 0.0.0.0:20221 -a 10194
      ```
    * app名
      ```bash
      debugserver 0.0.0.0:20221 -a "Aweme"
      debugserver 0.0.0.0:1234 -a "YouTube"
      ```
  * 其他额外参数
    * 加日志`log`
      ```bash
      debugserver -l debug.log 0.0.0.0:20221 -a 10194
      ```
    * 加详情`verbose`
      ```bash
      debugserver -v 0.0.0.0:20221 -a 10194
      ```
    * 开启调试`debugging`
      ```bash
      debugserver -g 0.0.0.0:20221 -a 10194
      ```
* Spaw模式：直接用debugserver启动app
  ```bash
  debugserver -x auto 0.0.0.0:20221 /private/var/containers/Bundle/Application/9AB25481-0AD3-435C-A02E-68F9623535BB/Aweme.app/Aweme
  ```
  * 说明
    * 关于如何获取到iOS的app二进制的完整路径，详见：
      * [二进制文件路径 · iOS逆向：心得集锦 (crifan.org)](https://book.crifan.org/books/ios_re_experience_collection/website/ios_app/bin_path.html)

### 相关说明

* `0.0.0.0`：比较好理解，表示：允许（来自外部的）任意IP访问
  * 此处指的是：允许电脑端（Mac）中的lldb来访问
* `20221`：端口号
  * 可以设置任意值，只要不和其他端口号冲突即可
    * 注：后续Mac中lldb连接时，要用到此端口号
* 如果遇到反调试而启动失败，则需要去处理`反反调试`
  * 详见：[常见问题](../common_issues/README.md)
