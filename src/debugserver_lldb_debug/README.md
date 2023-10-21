# debugserver+lldb调试

此处介绍用`debugserver`+`lldb`去调试iOS程序。

此处举例说明：

* iPhone机型：`iPhone 7 Plus`, `iOS 13.4.1`
* 被调试app：`抖音`
* 调试方式：`debugserver+lldb`的命令行

核心思路是：

* `iPhone`中：确保`debugserver`有正确的权限entitlement
  * 先从`iPhone`中导出`debugserver`
  * 再去`Mac`中，（用`codesign`或`ldid`）给`debugserver`加上合适的权限
  * 再把加了`entitlement`的`debugserver`拷贝回`iPhone`中
* `iPhone`中：用`debugserver`启动(抖音)app
* `Mac中`：用`lldb`去调试(抖音)app

下面介绍详细过程。

