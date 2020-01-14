## iPhone5从ios10.3.3降级到8.4.1

准备：一台mac电脑、爱思助手安装好、安装homebrew、python3

确保手机和电脑在同一个wifi环境

- 下载一键刷机工具 https://github.com/MatthewPierson/Vieux
- 解锁出文件来，安装python依赖包：```pip3  install -r   requirements.txt```
- 下载iPhone5，8.4.1的固件，注意区分版本
- 把手机先越狱，安装好OpenSSL 、openssh，确认可以通过ssh连接手机```ssh root@192.168.30.58  默认密码是alpine ```
- 然后可以执行脚本``` sudo ./vieux -i iPhone5,2_8.4.1_12H321_Restore.ipsw ```
- 手机屏幕会亮一下，然后出现进度条，开始慢慢刷机，十分钟即可刷好
- 激活手机开始使用



## 降级ios6

- 文档：https://github.com/synackuk/n1ghtshade
- 步骤
-  下载6.1.2的固件
-  启动n1ghtshade，点击restore ，第二步，select ipsw，再点击restore就开始
-  将手机进入dfu（Device Firmware Upgrade）模式
-  等待刷机
-   第一阶段刷完之后页面显示完成，其实还没有真正完成。还需要点击页面第二个按钮，进入boot，再次进入dfu模式
-   这次刷完之后就好了 