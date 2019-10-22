####1.终端查看framework和.a的支持架构
项目中经常会使用到一些第三方，真机运行的时候是OK的，但是模拟器运行却飘红了，当出现
````
Undefined symbols for architecture x86_64
````
说明第三方可能不支持模拟器运行的cpu架构：Undefined symbols for architecture x86_64，这时候打开终端查看一下这个framework支持的到底有哪些架构
````
lipo -info /Users/路径/Desktop/xxxx.framework/xxxx
lipo -info  xxxx.a
例：lipo -info /Users/qing/Desktop/HelloSDK.framework/HelloSDK
````
####2.iPhone真机和模拟器的CPU架构
````
iPhone真机CPU架构：
arm64: iPhone 5s, iPhone 6(Plus), iPhone 6s(Plus), iPhone SE, iPhone 7(Plus), iPad Air(2), Retina iPad Mini(2,3)…… 
armv7s: iPhone 5, iPhone 5c, iPad 4 
armv7: iPhone 3GS, iPhone 4, iPhone 4S, iPod 3G/4G/5G, iPad, iPad 2, iPad 3, iPad Mini 
armv6: iPhone, iPhone 3G, iPod 1G/2G
iPhone模拟器CPU架构：
模拟器32位处理器测试需要i386架构，iPhone5及之前设置:i386 
模拟器64位处理器测试需要x86_64架构，iPhone5s及之后设备 
````

