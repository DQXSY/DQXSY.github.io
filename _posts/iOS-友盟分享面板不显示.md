分享面板无法弹出(这个是由于由于创建Xcode项目会默认添加Main.storyboard作为Main Interface(General - Deployment Info)，也就是项目的主Window。如果没使用Main.storyboard而又另外在AppDelegate中创建了UIWindow对象，如
self.window = [[UIWindow alloc] initWithFrame:[UIScreen mainScreen].bounds]
如果项目中同时出现Main Interface以及代码创建UIWindow会导致分享面板无法正常弹出，解决方法是移除其一即可。如果移除了Main.storyboard，需要clean工程后再重新运行。
######1.移除Main.storyboard
######2.将Targets->General->Main Interface项中“Main(storyboard名字)”去掉
