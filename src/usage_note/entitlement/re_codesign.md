# 重签名

如前所述，把debugserver的原始entitlement权限做了改动后，需要去：`重签名`=`重新签名`

* 推荐方式：`codesign`
  * 优点：适用于`iOS 15.0+`和`iOS < 15.0`
  * 具体方式
    * **推荐方式**：（最省事的）**直接一步**
      ```bash
      codesign -f -s - --entitlements debugserver.entitlements debugserver
      ```
      * 等价于=简写为
        ```bash
        codesign -fs- --entitlements debugserver.entitlements debugserver
        ```
    * 次优方式：分两步
      * 第一步：先找到自己当前的有效的`sign identity`
        ```bash
        security find-identity -p codesigning
        ```
        * 得到：`sign identity：CDDC8C0D2F3A79EB17C183E14F799F75815E294E`
      * 第二步：再加上完整的参数，去用codesign重签名
        ```bash
        codesign --force --sign CDDC8C0D2F3A79EB17C183E14F799F75815E294E --entitlements debugable_entitlement.xml --timestamp=none --generate-entitlement-der debugserver
        ```
* 当`iOS < 15.0`，也可以用：`ldid`
  ```bash
  ldid -Sdebugserver.entitlements debugserver
  ```
  * 说明
    * `-S`和`参数`（即权限文件：`debugserver.entitlements`）之间**没有**空格
  * 注意：当`iOS >15.0`时，此方式会导致：运行崩溃killed
    * 详见：[运行崩溃killed](../../common_issues/run_crash_killed.md)
