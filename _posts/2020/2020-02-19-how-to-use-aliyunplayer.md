---
layout: post
title: 阿里云播放器使用
date: 2020-02-19
categories: aliyun 
tags: business
---


# web播放器

[https://help.aliyun.com/document_detail/125553.html?spm=a2c4g.11186623.6.1083.7d2d1bc7a1jwFb](https://help.aliyun.com/document_detail/125553.html?spm=a2c4g.11186623.6.1083.7d2d1bc7a1jwFb)

- STS(Security Token Service) 的播放流程 (临时授权)
STS是一个安全凭证（Token）的管理系统，用来授予临时的访问权限，这样就可以通过STS来完成对于临时用户的访问授权。详情参见 STS介绍。


![](https://tva1.sinaimg.cn/large/0082zybpgy1gbzc5xmxk5j30rf0hu77n.jpg)


- PlayAuth的播放流程 (播放凭证)
流程：用户App获取上传凭证 > 服务端下发上传凭证 > 用户上传视频并获取vid > 服务端获取播放凭证 > 将播放凭证下发给客户端 > 完成视频播放。


![](https://tva1.sinaimg.cn/large/0082zybpgy1gbzc7i9n6nj30nt0h0q4j.jpg)

[参考](https://help.aliyun.com/document_detail/125553.html?spm=a2c4g.11186623.6.1083.7d2d1bc7a1jwFb)

### 上传凭证

[获取上传凭证](https://help.aliyun.com/document_detail/55407.html?spm=a2c4g.11186623.6.709.2df3480fmNnx8C)

```
http://vod.cn-shanghai.aliyuncs.com/?Action=CreateUploadVideo&Title=exampleTitle&FileName=example.avi&FileSize=10485760&Format=JSON&<公共参数>

```

返回

```
{
 "RequestId": "25818875-5F78-4A13-BEF6-D7393642CA58",
 "VideoId": "93ab850b4f6f44eab54b6e91d24d81d4",
 "UploadAddress": "eyJTZWN1cml0eVRva2VuIjoiQ0FJU3p3TjF",
 "UploadAuth": "eyJFbmRwb2ludCI6Im"
}

```
[code](https://help.aliyun.com/document_detail/101396.html?spm=a2c4g.11186623.2.34.3101257e79vfgZ#CreateUploadVideo)

通过uploadAuth和uploadAddress上传  [文档](https://help.aliyun.com/document_detail/99889.html?spm=a2c4g.11186623.6.1050.3c5b6bd14ZdJlr)

[sdk下载](https://help.aliyun.com/document_detail/51992.html?spm=a2c4g.11186623.2.41.15896bd1oai8iH)

```

  <!--  IE需要es6-promise -->
    <script src="../lib/es6-promise.min.js"></script>
    <script src="../lib/aliyun-oss-sdk5.2.0.min.js"></script>
    <script src="../aliyun-vod-upload-sdk1.4.0.min.js"></script>
    
    javascript代码
    
var uploader = new AliyunUpload.Vod({
    partSize: 1048576,//分片大小默认1M，不能小于100K
       parallel: 5,//并行上传分片个数，默认5
    retryCount: 3,//网络原因失败时，重新上传次数，默认为3
    retryDuration: 2,//网络原因失败时，重新上传间隔时间，默认为2秒
    'onUploadstarted': function (uploadInfo) {
          uploader.setUploadAuthAndAddress(
              uploadInfo, 
            uploadAuth, 
            uploadAddress,
            videoId);
    }
    …… //其他回调
});

```
整体流程 
![](https://tva1.sinaimg.cn/large/0082zybply1gc1hdi5iwqj30cb097gnt.jpg)


### 播放凭证
拿视频去获取播放凭证，然后再播放

[获取播放凭证](https://help.aliyun.com/document_detail/52833.html?spm=a2c4g.11186623.2.15.3321142aWmx65J)

## 阿里播放器


[https://yq.aliyun.com/articles/241608?spm=5176.10695662.1996646101.searchclickresult.29006743SOiMob&aly_as=s1g1kUmZ
](https://yq.aliyun.com/articles/241608?spm=5176.10695662.1996646101.searchclickresult.29006743SOiMob&aly_as=s1g1kUmZ)

### 直接播放url实例

```
<body>
    <div id="J_prismPlayer" class="prism-player"></div>   <!-- prism-player为h5播放器皮肤的钩子类名，请务必加上 -->
    <script>
        var videoUrl=""; //获取的视频地址
        // 初始化播放器
        var player = new Aliplayer({
            id: "J_prismPlayer", // 容器id
            source: videoUrl,        // 视频url
            width: "100%",       // 播放器宽度
            height: "400px"      // 播放器高度
        });
    </script>
</body>
```


### vid播放实例
通过设置视频vid和播放凭证playauth参数播放阿里云视频点播服务中托管的视频

如何接入点播服务

```
<body>
    //播放器容器
    <div id='J_prismPlayer' class='prism-player'>   <!-- prism-player为h5播放器皮肤的钩子类名，请务必加上 -->
    //播放器初始化代码
    <script>
          var player = new Aliplayer({
              id: "J_prismPlayer", // 容器id
              vid : '1e067a2831b641db90d570b6480fbc40',//媒体转码服务的媒体Id
              playauth : '',//播放鉴权 [playauth参照](https://help.aliyun.com/document_detail/52833.html?spm=5176.doc51236.6.627.5gm5gf)
              width: "640px",
              height: "480px"
          });
     </script>
</body>

### ```![](![https://scratch.mit.edu/projects/217893304/](https://scratch.mit.edu/projects/217893304/))