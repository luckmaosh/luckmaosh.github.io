---
layout: post
title: ipa文件逆向以及修改签名
date: 2020-02-06
categories: ipa
tags: ipa apple ios
---

- 下载一个ipa文件，解压出来

```

$ codesign -vv -d  /Users/zhixuezhen/Downloads/i4ToolsDownloads/App/QQ_8.2.6的副本/Payload/QQ.app
Executable=/Users/zhixuezhen/Downloads/i4ToolsDownloads/App/QQ_8.2.6的副本/Payload/QQ.app/QQ
Identifier=com.tencent.mqq
Format=app bundle with Mach-O universal (armv7 arm64)
CodeDirectory v=20500 size=1179 flags=0x0(none) hashes=13+7 location=embedded
Signature size=4390
Authority=Apple iPhone OS Application Signing
Authority=Apple iPhone Certification Authority
Authority=Apple Root CA
Info.plist entries=67
TeamIdentifier=88L2Q4487U
Sealed Resources version=2 rules=20 files=6912
Internal requirements count=1 size=96

```
