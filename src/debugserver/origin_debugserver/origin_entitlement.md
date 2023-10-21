# 原始debugserver的entitlement权限

从原始版本的debugserver中查看=导出的entitlement权限（基本）都是一样的。

此处列出

* `iOS 13.4.1`的`iPhone7 Plus`中的
  * 原始的`debugserver`（`/Developer/usr/bin/debugserver`）

的`entitlement`权限：

```xml
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

供参考。
