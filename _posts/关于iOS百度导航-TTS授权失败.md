#### 1.问题描述
项目中用的是旧版的百度导航SDK，进入到导航界面会提示TTS授权失败且语言播报功能无法正常使用。
#### 2.问题原因
百度导航SDK内置百度TTS语音播报功能，需要对应用进行授权验证才能够使用，因此需要主动注册应用相关信息。而最新的导航SDK修改了之前的TTS鉴权方案，新方案不再使用白名单方案。
####3.解决方法
1. 在这里[百度语言](http://yuyin.baidu.com/app)创建自己的应用，注册语音合成功能，如下所示：![QQ20180603-162648@2x.png](https://upload-images.jianshu.io/upload_images/6941348-5891a42cc732488c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
2.点击上图右侧的“管理包名”，绑定bundle id
3.点击右侧的“查看key”，获取App ID、API Key、Secret Key
4.注意：新增导航appid设置接口，需要在**初始化导航**前，需要调用如下设置App ID、API Key、Secret Key，否则会没有声音
```
    [BNCoreServices_Instance authorizeTTSAppId:KAppID apiKey:KAPIKey secretKey:KSecretKey completion:^(BOOL suc) {
    }];
    [BNCoreServices_Instance authorizeNaviAppKey:kBaiduKey completion:^(BOOL suc) {
    }];
````
#### 4.遗留问题
1.项目中替换了新的百度导航SDK之后，发现百度地图和百度导航SDK冲突duplicate symbols for architecture arm6。解决方法是使用百度地图SDK4.0和百度导航SDK4.1，至于其中的MBProgress冲突只有替换成SVProgress。
2.百度导航需要添加ADSupport.framework，这个在上架的时候需要在广告标识符选项前勾选是，然后会有4个选项：
（1）、在 App 内投放广告 服务应用中的广告。如果你的应用中集成了广告的时候，你需要勾选这一项。
（2）、将此 App 安装归因于先前投放的特定广告 跟踪广告带来的安装。如果你使用了第三方的工具来跟踪广告带来的激活以及一些其他事件，但是应用里并没有展示广告你需要勾选这一项。
（3）、将此 App 中发生的操作归因于先前投放的特定广告 跟踪广告带来的用户的后续行为。如果你使用了第三方的工具来跟踪广告带来的激活以及一些其他事件。
（4）、iOS 中的“限制广告跟踪”设置 这一项下的内容其实就是对你的应用使用 IDFA 的目的做下确认，只要你选择了采集 IDFA，那么这一项都是需要勾选的。
这里勾选2，4即可。
3.设置 “Required background modes”，Target->Capabilities->Background Modes->勾选Localtion Updates。再看下Infoplist有没有添加键值对Required background modes，没有的话需要手动添加一下![1212.png](https://upload-images.jianshu.io/upload_images/6941348-4a4c72192dae0bb3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
