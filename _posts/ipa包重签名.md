####1.作用
目前，重签名主要用于企业证书重新签名个人证书发布的ipa包，包括各种助手以及企业内测包的发布等。
####2.使用工具（ios-app-signer）
[下载链接](http://dantheman827.github.io/ios-app-signer/)：http://dantheman827.github.io/ios-app-signer/
####3.操作步骤
1）右键需要重新签名的ipa包 -> 选择打开方式 归档实用工具[QQ20180623-160122@2x.png](https://upload-images.jianshu.io/upload_images/6941348-d6e1d904b17e0081.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

2）打开生成的文件夹 –> 打开里面的Payload文件 –>右键.app显示包内容![QQ20180623-160326@2x.png](https://upload-images.jianshu.io/upload_images/6941348-bc14612365a03725.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

3）按照上述步骤，操作公司用299打包的ipa文件，将其中的embedded.mobileprovision文件拷贝出来,放到步骤2中.app文件中（选择替换）,一定要记得需要这个 embedded.mobileprovision 文件,如果没有这个文件,重签名后是安装不了的。（注意，有些ipa包中有两个embedded.mobileprovision 文件，这里都需要替换掉），如图所示：![QQ20180623-160531@2x.png](https://upload-images.jianshu.io/upload_images/6941348-8efa9bb9d093c2b2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

4）打开iOS-App-Signer![QQ20180623-160731@2x.png](https://upload-images.jianshu.io/upload_images/6941348-9b26690ea6e214d0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)注意，这里的Input File应选择需要重签名的.app文件，证书选择企业级发布证书。最后选择start，生成新的ipa包，就可以使用iTools或者其他应用管理器下载应用了。




