#### 1.代码片段备份路径：
-Xcode中的代码片段默认放在下面的目录中：
-~/Library/Developer/Xcode/UserData/CodeSnippets
#### 2.UIWebView的属性设置（字体，颜色）以及WebView的canGoBack属性
```
UIWebView无法通过自身的属性设置字体的一些属性，只能通过html代码进行设置，在webView加载完毕后，在-(void)webViewDidFinishLoad:(UIWebView *)webView  方法中加入js代码
NSString *str = @"document.getElementsByTagName('body')[0].style.webkitTextSizeAdjust= '60%'";
[_webView stringByEvaluatingJavaScriptFromString:str];
或加入
NSString *jsString = [[NSString alloc] initWithFormat:@"document.body.style.fontSize=%f;document.body.style.color=%@",fontSize,fontColor];
[webView stringByEvaluatingJavaScriptFromString:jsString];
在使用UIWebview CanGoBack属性的时候要使用loadRequest才可以，使用loadHTMLString读本地html文件的时候是不能后退的。
```
#### 3.NSBundle pathForResource取不到值如何解决
```
NSString *myFilePath = [[NSBundle mainBundle] pathForResource:@"qidong"ofType:@"mp4"];
这个MP4的字符串无法获取，要在项目工程中▸Target▸Copy Bundle Resource中添加MP4文件
```
#### 4.项目中添加Pch文件的步骤
Build Setting▸搜索Prefix Header▸把路径修改为相对路径
#### 5.解决Cell左侧留有空白的问题
```
#pragma mark - 解决cell左侧留白
-(void)viewDidLayoutSubviews
{
    if ([self.tableView respondsToSelector:@selector(setSeparatorInset:)]) {
        [self.tableView setSeparatorInset:UIEdgeInsetsZero];
    }
    if ([self.tableView respondsToSelector:@selector(setLayoutMargins:)]) {
        [self.tableView setLayoutMargins:UIEdgeInsetsZero];
    }
}
- (void)tableView:(UITableView *)tableView willDisplayCell:(UITableViewCell *)cell forRowAtIndexPath:(NSIndexPath *)indexPath
{
    if ([cell respondsToSelector:@selector(setSeparatorInset:)]) {
        [cell setSeparatorInset:UIEdgeInsetsZero];
    }
    if ([cell respondsToSelector:@selector(setLayoutMargins:)]) {
        [cell setLayoutMargins:UIEdgeInsetsZero];
    }
}
```
#### 5.修改Xcode.m文件内容的路径
文件夹位置,应用程序-找到xcode-右击显示包内容 Xcode ▸ Contents ▸ Developer ▸ Platforms ▸ iPhoneOS.platform ▸ Developer ▸ Library ▸ Xcode ▸ Templates ▸ File Templates ▸ Source  可自定义.m文件的模板
#### 6.在viewWillDisappear中要将UISearchController移除
```
在viewWillDisappear中要将UISearchController移除, 否则切换到下一个View中, 搜索框仍然会有短暂的存在.
    if (self.searchVC.active) {
        self.searchVC.active = NO;
        [self.searchVC.searchBar removeFromSuperview];
    }
```
#### 7.真机调试包安装路径
Xcode ▸ Contents ▸ Developer ▸ platforms ▸ IPhoneOS.platform ▸ DeviceSupport
####8.adb常用命令
```
adb devices
adb install 文件名
adb shell
adb pull 手机路径  电脑路径
add push 要传输的路径  手机路径
add logical －v time ＊> 电脑路径
adb logcat －s jianqi
```
9.iOS10跳转系统设置 WIFI 蓝牙 以及应用设置
```
Wi-Fi:App-Prefs:root=WIFI
蓝牙:App-Prefs:root=Bluetooth
蜂窝移动网络:App-Prefs:root=MOBILE_DATA_SETTINGS_ID
个人热点:App-Prefs:root=INTERNET_TETHERING
运营商:App-Prefs:root=Carrier
通知:App-Prefs:root=NOTIFICATIONS_ID
通用:App-Prefs:root=General
通用-关于本机:App-Prefs:root=General&path=About
通用-键盘:App-Prefs:root=General&path=Keyboard
通用-辅助功能:App-Prefs:root=General&path=ACCESSIBILITY
通用-语言与地区:App-Prefs:root=General&path=INTERNATIONAL
通用-还原:App-Prefs:root=Reset
墙纸:App-Prefs:root=Wallpaper
Siri:App-Prefs:root=SIRI
隐私:App-Prefs:root=Privacy
定位:App-Prefs:root=LOCATION_SERVICES
Safari:App-Prefs:root=SAFARI
音乐:App-Prefs:root=MUSIC
音乐-均衡器:App-Prefs:root=MUSIC&path=com.apple.Music:EQ
照片与相机:App-Prefs:root=Photos
FaceTime:App-Prefs:root=FACETIME
NSURL *url = [NSURL URLWithString:UIApplicationOpenSettingsURLString]; if ([[UIApplication sharedApplication]canOpenURL:url]) { [[UIApplication sharedApplication]openURL:url]; }
```
#### 10.关于Build Active Architecture Only属性
这个属性设置为yes，是为了debug的时候编译速度更快，它只编译当前的architecture版本。而设置为no时，会编译所有的版本。
#### 11.使用Xcode查找项目中的中文字符串
```
1.打开”Find Navigator”
2.切换搜索模式到 “Find > Regular Expression”
3.输入@"[^"]*[\u4E00-\u9FA5]+[^"\n]*?" (swift请去掉”@” 输入@"[^"]*[\u4E00-\u9FA5]+[^"\n]*?" 就好了
```
#### 12.自定义textField的ClearButton(KVC模式)
```
UIButton *button = [textField valueForKey:@"_clearButton"];
[button setImage:[UIImage imageNamed:@"icon_clear"] forState:UIControlStateNormal];
textField.clearButtonMode = UITextFieldViewModeWhileEditing;
```
#### 13.CocoaPods的使用
```
1.从终端一直cd到项目总目录（注意：包含.xcodeproj的文件）
2.建立Podfile（配置文件），终端输入 vim Podfile
3.进入编辑模式，输入以下内容（模板）：
platform :ios, '8.0'
use_frameworks!
target "项目名称" do
pod 'ReactiveObjC'
end
4.esc->:wq ，输入pod install
```
#### 14.当UItextView/UITextField中没有文字时，禁用回车键
````
textField.enablesReturnKeyAutomatically = YES;
````
#### 15.icon和启动页尺寸
````
App icon: 40x40  60X60 58x58 87X87 80x80 120x120 180x180 1024 x1024(无圆角)
App 启动页：640 × 960，640 × 1136，750 × 1334，1242 × 2208，1125 x 2436, 828 x 1792, 1242 x 2688
````
