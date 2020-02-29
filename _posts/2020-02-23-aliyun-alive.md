
# 阿里云直播

## 目前的协议

- HLS(HTTP Live Streaming) HTML5的video标签并不能直接播放hls直播流，需要借助插件来实现。关于插件的话网上也搜了一大堆用来测试，发现免费还好用的应该算是video.js了，video.js也是专门针对hls直播流做了一个依赖video.js的插件videojs-contrib-hls.js。前端页面
- Real Time Messaging Protocol（简称 RTMP）是 Macromedia 开发的一套视频直播协议，现在属于 Adobe。和 HLS 一样都可以应用于视频直播，区别是 RTMP 基于 flash 无法在 iOS 的浏览器里播放，但是实时性比 HLS 要好。所以一般使用这种协议来上传视频流，也就是视频流推送到服务器。 浏览器端，HTML5 video标签无法播放 RTMP 协议的视频，可以通过 video.js 来实现。
- 🔽RTSP:(Real Time Streaming Protocol)
- 🔽HTTP-FLV 基于http



## 阿里云添加域名

[https://help.aliyun.com/document_detail/98296.html?spm=a2c4g.11186623.6.579.2dd84d25R499CD](https://help.aliyun.com/document_detail/98296.html?spm=a2c4g.11186623.6.579.2dd84d25R499CD)

- 播流域名 
- 推流域名




### PC端推流与播流整体架构


![](https://tva1.sinaimg.cn/large/0082zybply1gc8gw8abs1j30nc0d241d.jpg)


![](https://tva1.sinaimg.cn/large/0082zybply1gc8gxdlqljj30nc0ftdmf.jpg)


## 服务搭建

服务器的作用是视频转存和分发，有付费也有免费的开源方案。付费的比如阿里云的直播服务，也可以自己搭建，这里说说自己搭建。搭建的方法有两种，
- nginx搭建
- srs搭建 https://github.com/ossrs/srs/tree/3.0release/trunk

整个直播的业务架构是：


```
+---------+      +-----------------+       +---------+
| Encoder +-->---+ SRS/CDN Network +--->---+ Player  |
+---------+      +-----------------+       +---------+

```

客户端推流(Encoder)和播放器(Player)的架构一般是：

```
+-------------------------------------------+
|           Device(Out/In YUV/PCM)          |
+-------------------------------------------+
|   Codec(YUV/PCM to/from H.264/AAC stream) |
+-------------------------------------------+
|   Muxer(H.264/AAC to/from FLV/MP4/HLS)    |
+-------------------------------------------+
|          Transport(RTMP/HTTP/UDP)         |
+-------------------------------------------+
```

srs配置

```
# main config for srs.
# @see full.conf for detail config.

listen              1935;
max_connections     1000;
srs_log_tank        file;
srs_log_file        ./objs/srs.log;

# 内置Nginx 代理
http_server {
    enabled         on;
    listen          8080;
    dir             ./objs/nginx/html;
}
vhost __defaultVhost__ {
    # hls直播（手机端）
    hls {
        enabled         on;
        hls_fragment    10;
        hls_window      60;
        hls_path        ./objs/nginx/html;
        hls_m3u8_file   [app]/[stream].m3u8;
        hls_ts_file     [app]/[stream]-[seq].ts;
    }
    # flv直播
    http_remux {
        enabled     on;
        mount       [vhost]/[app]/[stream].flv;
        hstrs       on;
    }
}

# vhost多租用
vhost dvr.com {
    hls {
        enabled off;
    }

    dvr {
        enabled      on;
        dvr_path     ./objs/nginx/html/[app]/[stream].[timestamp].flv;
        dvr_plan     session;
    }
}
dvr录制存储配置规则

```

启动srs

```
./objs/srs -c ./conf/srs.conf

```

## 推流工具

###  ffmpeg

 开源的，https://git.ffmpeg.org/ffmpeg.git，
### OBS推流工具
Open Broadcaster Software（简称OBS）是一款好用的直播流媒体内容制作软件。

- 使用obs录取屏幕
https://blog.csdn.net/liuchen1206/article/details/77771703


[https://help.aliyun.com/document_detail/45212.html?spm=a2c4g.11186623.2.15.15f625cfRm5DzU](https://help.aliyun.com/document_detail/45212.html?spm=a2c4g.11186623.2.15.15f625cfRm5DzU)


推流地址：
``` rtmp://localhost/[app]/[stream]```

例如 ``` rtmp://localhost/live/stream1```

![](https://tva1.sinaimg.cn/large/0082zybply1gcazu6otrsj30wu082772.jpg)

>注意：OBS推流时，流名称的翻译有问题，流名称是要写在流密钥这里的，如下图所示。


##  播放流
 两种方式： vlc播放器，或者h5播放
 
 vlc就可以直接下载播放器播放，这里看看h5的播放
![](https://tva1.sinaimg.cn/large/0082zybply1gc8selxklbj30iu079mxr.jpg)
简简单单的代码，重点在于拉流地址必须与推流地址一致


- https://pay.weixin.qq.com/static/applyment_guide/applyment_detail_website.shtml

- https://docs.open.alipay.com/270/105899/