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

- 下载刷机的固件6.1.3或者6.1.4和刷机软件
-  启动Mac上的软件n1ghtshade，点击restore ，第二步，select ipsw，选中刚才下载的固件，再点击restore就开始
-  这时候将手机进入dfu（Device Firmware Upgrade）模式 ，进入的方式可以百度一下
-  等待刷机，等几分钟，这时候可能会卡住不动，退出进程，重新来一次，直到出现这个界面，就开始刷机了
![](https://tva1.sinaimg.cn/large/0082zybpgy1gc9im8nc7aj31mo0q07wh.jpg)

完成界面
![](https://tva1.sinaimg.cn/large/0082zybpgy1gc9ijq6q90j30rt112aep.jpg)

-  第一阶段刷完之后页面显示完成，其实还没有真正完成。还需要点击页面第二个按钮，进入boot，再次进入dfu模式

![](https://tva1.sinaimg.cn/large/0082zybpgy1gc9ik7lrf7j30rt112afd.jpg)

-   这次刷完之后就好了 
