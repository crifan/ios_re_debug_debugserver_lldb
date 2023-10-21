# 查看entitlement权限

如果想要`查看`=`导出`，比如原始版本的`debugserver`的，entitlement权限，可以用：`codesign`或`ldid`

* 查看/导出entitlement权限
  * ldid
    ```bash
    ldid -e debugserver
    ```
  * codesign
    ```bash
    codesign -d --entitlements - debugserver
    ```
    * 参数说明
      * `-d`：display显示
      * `--entitlements`：权限信息
      * `-`：（把信息输出到）当前默认（stdout的）终端=terminal

## ldid对于FAT格式会输出多份entitlement权限信息

如果是`FAT`格式，`ldid -e debugserver`则会输出（多个架构所对应的）**多份**entitlement权限信息

举例：

此处从iPhone8中导出的包含`arm64`和`arm64e`的`FAT`格式的`debugserver`：

```bash
crifan@licrifandeMacBook-Pro  ~/dev/dev_root/iosReverse/AppleStore/fromiPhone8/Developer/usr/bin  ll
total 5240
-rw-r--r--  1 crifan  staff   832B  3  3 11:48 debugable_entitlement.xml
-rwxrwxr-x  1 crifan  staff   1.3M  8  8  2021 debugserver

 crifan@licrifandeMacBook-Pro  ~/dev/dev_root/iosReverse/AppleStore/fromiPhone8/Developer/usr/bin  file debugserver
debugserver: Mach-O universal binary with 2 architectures: [arm64:Mach-O 64-bit executable arm64] [arm64e:Mach-O 64-bit executable arm64e]
debugserver (for architecture arm64):    Mach-O 64-bit executable arm64
debugserver (for architecture arm64e):    Mach-O 64-bit executable arm64e
```

用ldid查看时，会输出2份entitlement权限信息：

```bash
crifan@licrifandeMacBook-Pro  ~/dev/dev_root/iosReverse/AppleStore/fromiPhone8/Developer/usr/bin  ldid -e debugserver
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>com.apple.springboard.debugapplications</key>
    <true/>
    <key>com.apple.backboardd.launchapplications</key>
    <true/>
    <key>com.apple.backboardd.debugapplications</key>
    <true/>
    <key>com.apple.frontboard.launchapplications</key>
    <true/>
    <key>com.apple.frontboard.debugapplications</key>
    <true/>
    <key>seatbelt-profiles</key>
    <array>
        <string>debugserver</string>
    </array>
    <key>com.apple.private.logging.diagnostic</key>
    <true/>
    <key>com.apple.security.network.server</key>
    <true/>
    <key>com.apple.security.network.client</key>
    <true/>
    <key>com.apple.private.memorystatus</key>
    <true/>
    <key>com.apple.private.cs.debugger</key>
    <true/>
</dict>
</plist>
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>com.apple.springboard.debugapplications</key>
    <true/>
    <key>com.apple.backboardd.launchapplications</key>
    <true/>
    <key>com.apple.backboardd.debugapplications</key>
    <true/>
    <key>com.apple.frontboard.launchapplications</key>
    <true/>
    <key>com.apple.frontboard.debugapplications</key>
    <true/>
    <key>seatbelt-profiles</key>
    <array>
        <string>debugserver</string>
    </array>
    <key>com.apple.private.logging.diagnostic</key>
    <true/>
    <key>com.apple.security.network.server</key>
    <true/>
    <key>com.apple.security.network.client</key>
    <true/>
    <key>com.apple.private.memorystatus</key>
    <true/>
    <key>com.apple.private.cs.debugger</key>
    <true/>
</dict>
</plist>
```

对比：

后来去用lipo瘦身后：

```bash
✘ crifan@licrifandeMacBook-Pro  ~/dev/dev_root/iosReverse/AppleStore/fromiPhone8/Developer/usr/bin  lipo -thin arm64 debugserver -output debugserver_orig_arm64
 crifan@licrifandeMacBook-Pro  ~/dev/dev_root/iosReverse/AppleStore/fromiPhone8/Developer/usr/bin  ll
total 6504
-rw-r--r--  1 crifan  staff   832B  3  3 11:48 debugable_entitlement.xml
-rwxrwxr-x  1 crifan  staff   1.3M  8  8  2021 debugserver
-rwxr-xr-x  1 crifan  staff   1.3M  3  3 11:49 debugserver_debugable
-rwxr-xr-x  1 crifan  staff   632K  8  8  2021 debugserver_orig_arm64
crifan@licrifandeMacBook-Pro  ~/dev/dev_root/iosReverse/AppleStore/fromiPhone8/Developer/usr/bin  cp debugserver_orig_arm64 debugserver_arm64_debugable
```

就只有一个架构arm64了

再去查看entitlement，就只有一份entitlement信息了：

```bash
crifan@licrifandeMacBook-Pro  ~/dev/dev_root/iosReverse/AppleStore/fromiPhone8/Developer/usr/bin  ldid -e debugserver_arm64_debugable
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>com.apple.springboard.debugapplications</key>
    <true/>
    <key>com.apple.backboardd.launchapplications</key>
    <true/>
    <key>com.apple.backboardd.debugapplications</key>
    <true/>
    <key>com.apple.frontboard.launchapplications</key>
    <true/>
    <key>com.apple.frontboard.debugapplications</key>
    <true/>
    <key>com.apple.private.logging.diagnostic</key>
    <true/>
    <key>com.apple.private.memorystatus</key>
    <true/>
    <key>com.apple.private.cs.debugger</key>
    <true/>
    <key>get-task-allow</key>
    <true/>
    <key>task_for_pid-allow</key>
    <true/>
    <key>run-unsigned-code</key>
    <true/>
</dict>
</plist>%
```

