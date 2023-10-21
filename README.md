# iOS逆向调试：debugserver+lldb

* 最新版本：`v1.0`
* 更新时间：`20231021`

## 简介

介绍iOS逆向中动态调试中的其中一种方式：debugserver+lldb。先是概览；然后再去详细介绍如何调试，首先是确保iPhone中debugserver有正确的权限，接着是iPhone中用debugserver启动app，最后是Mac中用lldb去调试app；接着单独介绍debugserver，包括原始的位置和来源，以及附录上原始entitlement权限供参考，以及help语法；然后介绍lldb；然后总结使用心得，包括获取iOS的app二进制路径，entitlement权限的如何查看权限、如何重签名；以及常见问题，包括运行崩溃killed等内容。

## 源码+浏览+下载

本书的各种源码、在线浏览地址、多种格式文件下载如下：

### HonKit源码

* [crifan/ios_re_debug_debugserver_lldb: iOS逆向调试：debugserver+lldb](https://github.com/crifan/ios_re_debug_debugserver_lldb)

#### 如何使用此HonKit源码去生成发布为电子书

详见：[crifan/honkit_template: demo how to use crifan honkit template and demo](https://github.com/crifan/honkit_template)

### 在线浏览

* [iOS逆向调试：debugserver+lldb book.crifan.org](https://book.crifan.org/books/ios_re_debug_debugserver_lldb/website/)
* [iOS逆向调试：debugserver+lldb crifan.github.io](https://crifan.github.io/ios_re_debug_debugserver_lldb/website/)

### 离线下载阅读

* [iOS逆向调试：debugserver+lldb PDF](https://book.crifan.org/books/ios_re_debug_debugserver_lldb/pdf/ios_re_debug_debugserver_lldb.pdf)
* [iOS逆向调试：debugserver+lldb ePub](https://book.crifan.org/books/ios_re_debug_debugserver_lldb/epub/ios_re_debug_debugserver_lldb.epub)
* [iOS逆向调试：debugserver+lldb Mobi](https://book.crifan.org/books/ios_re_debug_debugserver_lldb/mobi/ios_re_debug_debugserver_lldb.mobi)

## 版权和用途说明

此电子书教程的全部内容，如无特别说明，均为本人原创。其中部分内容参考自网络，均已备注了出处。如发现有侵权，请通过邮箱联系我 `admin 艾特 crifan.com`，我会尽快删除。谢谢合作。

各种技术类教程，仅作为学习和研究使用。请勿用于任何非法用途。如有非法用途，均与本人无关。

## 鸣谢

感谢我的老婆**陈雪**的包容理解和悉心照料，才使得我`crifan`有更多精力去专注技术专研和整理归纳出这些电子书和技术教程，特此鸣谢。

## 其他

### 作者的其他电子书

本人`crifan`还写了其他`150+`本电子书教程，感兴趣可移步至：

[crifan/crifan_ebook_readme: Crifan的电子书的使用说明](https://github.com/crifan/crifan_ebook_readme)

### 关于作者

关于作者更多介绍，详见：

[关于CrifanLi李茂 – 在路上](https://www.crifan.org/about/)
