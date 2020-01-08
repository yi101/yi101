## 简介

Android 普华播放器 SDK 是普华云平台开源的一款播放器组件，简单几行代码即可拥有类似各大视频强大的播放功能，包括横竖屏切换、视频播放比例、手势和截图等基础功能，还支持边下边播、镜像旋转、GIF 录制和倍速播放等特殊功能，相比系统播放器，支持格式更多，兼容性更好，功能更强大，同时还具备首屏秒开、低延迟的优点，以及视频缩略图等高级能力。

## SDK 下载

点播 Android 超级播放器的项目地址是 [PHVideoView_Android](https://www.baidu.com)。

## 阅读对象

本文档部分内容为普华云专属能力，使用前请开通 [云平台](https://www.baidu.com) 相关服务，未注册用户可注册账号 [免费试用](https://www.baidu.com)。

## 快速集成

### aar 集成

1. 下载 SDK + Demo 开发包，项目地址为 [Android](https://github.com/tencentyun/SuperPlayer_Android)。
   2. 导入`libphplayer.aar`到工程中去。
2. 在`app/build.gralde`中添加依赖：

```java
implementation(name: 'libphplayer', ext: 'aar')
```

4. 在项目`build.gralde`中添加：

```
...
allprojects {
    repositories {
        flatDir {
            dirs 'libs'
        }
        ...
    }
}
...
```

5. 权限声明

```java
<!--网络权限-->
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<!--存储-->
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
```

> ! libphplayer.aar`以 moudle 方式开源，您可在 Demo 中找到所有源代码。

### 使用播放器

播放器主类为`PhPlayerView`，创建后即可播放视频。

```java
//您注册的企业ID
String appId = "";
//视频文件ID
String fileId = "";
//视频播放帮助类
mPhVideoPlayHelp = new PHVideoPlayHelp(this, appId);
//播放视频
mPhVideoPlayHelp.startPlayVideo(mPHVideoView, fileId);
```

运行代码，可以看到视频在手机上播放，并且界面上大部分功能都处于可用状态。
<img src="https://i.loli.net/2019/12/20/fbzLgEirnFNGTey.jpg" width="550">

### 选择 FileId

视频 `FileId` 在一般是在视频上传后，由服务器返回：

1. 客户端视频发布后，服务器会返回`FileId`到客户端。
2. 服务端视频上传时，在 [确认上传](https://cloud.tencent.com/document/product/266/9757) 的通知中包含对应的 `FileId`。

如果文件已存在云平台，则可以进入 [文件信息列表](https://console.cloud.tencent.com/vod/media) ，找到对应的文件，查看 `FileId`。如下图所示，文件 ID 即表示 `FileId`：
![企业微信截图_15764768863718.png](https://i.loli.net/2019/12/20/aKFkObpiue4SLq8.png)

## 视频缩略图

在播放长视频时，缩略图有助于观众找到感兴趣的点。进度条自带缩略图预览功能。

<img src="https://i.loli.net/2019/12/20/3aYgWfU9iuysGt2.jpg" width="550">

## 截图

通过`doScreenShot()`可以获取到当前的播放画面。

```
Bitmap bitmap = mPHVideoView.doScreenShot();
```

拿到`bitmap`后可以做进一步操作，存储到内存卡或显示到指定位置

## 显示比例

支持默认、16：9、4:3、原始大小、填充、居中裁剪等多种显示样式

```
mPHVideoView.setScreenScaleType(VideoView.SCREEN_SCALE_DEFAULT);//默认
mPHVideoView.setScreenScaleType(VideoView.SCREEN_SCALE_16_9);//16：9
mPHVideoView.setScreenScaleType(VideoView.SCREEN_SCALE_4_3);//4:3
mPHVideoView.setScreenScaleType(VideoView.SCREEN_SCALE_ORIGINAL);//原始大小
mPHVideoView.setScreenScaleType(VideoView.SCREEN_SCALE_MATCH_PARENT);//填充
mPHVideoView.setScreenScaleType(VideoView.SCREEN_SCALE_CENTER_CROP);//居中裁剪
```

## 镜像旋转

通过`setMirrorRotation(true)` API 可以对画面镜像旋转，`false`可以取消镜像，默认为`false`

```java
mPHVideoView.setMirrorRotation(true);
```

## GIF 录制

设置`String gifPath`，GIF 路径，通过`startGif(gifPath)`和`stopGif()`;API 可以录制 GIF

```
//开始录制GIF
mPHVideoView.startGif(gifPath);
//停止录制GIF
mPHVideoView.stopGif();
```

## 倍速播放

通过`setSpeed(0.5f)`和`setSpeed(2.0f)` API 可以控制视频的倍数播放

```
//0.5倍速度播放视频
mPHVideoView.setSpeed(0.5f);
//正常速度播放视频
mPHVideoView.setSpeed(1.0f);
//2倍速度播放视频
mPHVideoView.setSpeed(2.0f);
```

## 退出播放

当不需要播放器时，调用`mPhVideoPlayHelp.onDestory()`清理播放器内部状态，释放内存。

```java
mPhVideoPlayHelp.onDestory();
```

## 更多功能

完整功能可下载视频 Demo 体验，或直接运行工程 Demo。
