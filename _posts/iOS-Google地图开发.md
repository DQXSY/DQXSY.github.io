#### 一.问题描述
客户对项目使用的系统原生地图不满意，需要更改成Google地图。
#### 二.集成步骤
###### 1.翻啥的软件
mac端：[蓝灯](https://github.com/getlantern/download/wiki)
iphone端：[ExpressVPN](https://express.01b122.cn/ios_tutorial.html)
不论是查看官方文档申请key，还是下载google map demo都需要翻啥的。
###### 2.申请key
点击[Google开发者中心](https://cloud.google.com/maps-platform/),由此申请App key。
###### 3.下载Google map demo
这里直接下载定位的demo即可，里面包含了地图和定位的framework,终端执行命令的时候记得开启蓝灯。
````
pod try GooglePlaces
````
###### 4.info.plist文件配置
````
添加下面的key到plist中，添加定位相关私有信息配置。
<key>LSApplicationQueriesSchemes</key>
<array>
    <string>googlechromes</string>
    <string>comgooglemaps</string>
</array>
	<key>NSLocationAlwaysAndWhenInUseUsageDescription</key>
	<string>我们需要通过您的地理位置信息获取您周边的位置信息</string>
	<key>NSLocationAlwaysUsageDescription</key>
	<string>我们需要通过您的地理位置信息获取您周边的位置信息</string>
	<key>NSLocationWhenInUseUsageDescription</key>
	<string>我们需要通过您的地理位置信息获取您周边的位置信息</string>
````
######  5.导入SDK
导入的这块，本来只打算移入googlemap这一个framework的，但是不幸的是运行的时候报错了。所以干脆直接按照demo里面的来添加了。如图：![2.png](https://upload-images.jianshu.io/upload_images/6941348-f3a8d031e00d4008.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
需要注意的是要将Resources文件夹下的GoogleMaps.bundle添加到工程中。其次就是添加依赖库：
````
AVFoundation.framework
CoreData.framework
CoreLocation.framework
CoreText.framework
GLKit.framework
ImageIO.framework
libc++.dylib
libicucore.dylib
libz.dylib
OpenGLES.framework
QuartzCore.framework
SystemConfiguration.framework

OtherLinker Flags中添加-ObjC
````
###### 6.显示Google地图
（1）AppDelegate调用Google地图的头文件
````
 ＃import <GoogleMaps/GoogleMaps.h>
````
（2）注册Google地图key
````
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
      [GMSServices provideAPIKey:kGoogleKey];
}
````
（3）Google地图初始化
````
- (GMSMapView *)mapView
{
    if (!_mapView) {

        _mapView = [[GMSMapView alloc] initWithFrame:CGRectMake(0, 0, SCREEN_WIDTH, self.view.height - KTabBarHeight)];
        _mapView.delegate = self;
        _mapView.mapType = kGMSTypeNormal;
        _mapView.camera = [[GMSCameraPosition alloc] initWithLatitude:[HYLocationManager sharedInstance].userLatitude longitude:[HYLocationManager sharedInstance].userLongitude zoom:_zoomLevel];
    }
    return _mapView;
}

````
到这里，开启手机VPN，运行项目，先查看是否能显示地图，再做接下来的工作。
###### 7.常用类以及常用方法介绍
Google地图常用类以及常用的方法介绍：
 *   [- (void)mapView:(GMSMapView *)mapView willMove:(BOOL)gesture](https://developers.google.com/maps/documentation/ios-sdk/reference/protocol_g_m_s_map_view_delegate-p.html#ae1f53e0d056bf4d246356134ec594612) 镜头即将移动时调用 *  
 *  [- (void)mapView:(GMSMapView *)mapView didChangeCameraPosition:(GMSCameraPosition *)position](https://developers.google.com/maps/documentation/ios-sdk/reference/protocol_g_m_s_map_view_delegate-p.html#aabd01d59d7680799a0c24d3c8b5e4622) 镜头移动完成后调用*   
 *   [- (void)mapView:(GMSMapView *)mapView didTapAtCoordinate:(CLLocationCoordinate2D)coordinate](https://developers.google.com/maps/documentation/ios-sdk/reference/protocol_g_m_s_map_view_delegate-p.html#a9f226252840c79a996df402da9eec235) 点击地图时调用 *  

 *  [- (void)mapView:(GMSMapView *)mapView didLongPressAtCoordinate:(CLLocationCoordinate2D)coordinate](https://developers.google.com/maps/documentation/ios-sdk/reference/protocol_g_m_s_map_view_delegate-p.html#a0499f484d9ea51041babd3ac8dcc7b27) 长按地图时调用*    
*   [- (BOOL)mapView:(GMSMapView *)mapView didTapMarker:(GMSMarker *)marker](https://developers.google.com/maps/documentation/ios-sdk/reference/protocol_g_m_s_map_view_delegate-p.html#ae291e1bff99f9d06428ced09daf5802d) 点击大头针时调用*   
 *   [- (void)mapView:(GMSMapView *)mapView didTapInfoWindowOfMarker:(GMSMarker *)marker](https://developers.google.com/maps/documentation/ios-sdk/reference/protocol_g_m_s_map_view_delegate-p.html#ae1614978aef680d671a6a95da8e13bf7) 点击大头针的弹出视窗时调用*   
 *   [- (void)mapView:(GMSMapView *)mapView didLongPressInfoWindowOfMarker:(GMSMarker *)marker](https://developers.google.com/maps/documentation/ios-sdk/reference/protocol_g_m_s_map_view_delegate-p.html#a4ff47da211c1cc6ca0aa53d52717f0db) 长按大头针视窗时调用* 
 *   [- (nullable UIView *)mapView:(GMSMapView *)mapView markerInfoWindow:(GMSMarker *)marker](https://developers.google.com/maps/documentation/ios-sdk/reference/protocol_g_m_s_map_view_delegate-p.html#ab83c3dab588f06e6227794740782bf55) 自定义大头针弹出视窗，返回UIView*   
 *   [- (void)mapView:(GMSMapView *)mapView didDragMarker:(GMSMarker *)marker](https://developers.google.com/maps/documentation/ios-sdk/reference/protocol_g_m_s_map_view_delegate-p.html#ae13d024d818081757bb058ecc532459a) 拖拽大头针时调用*  
 *   [- (void)mapView:(GMSMapView *)mapView didEndDraggingMarker:(GMSMarker *)marker](https://developers.google.com/maps/documentation/ios-sdk/reference/protocol_g_m_s_map_view_delegate-p.html#adab19737cc05cfda53a03c0247ab9e1e) 大头针拖拽完成时调用*   
````
GMSMapView 最主要的地图类
GMSCameraPosition 地图摄像头，可以理解为当前地图的可视范围，可以获取到摄像头中心点坐标、镜头缩放比例、方向、视角等参数
GMSMarker 地图大头针
GMSGeocoder 反向地理编码类
GMSAddress 反向地理编码返回的类,包含坐标及地理位置描述等信息
CLLocationManager 就是CoreLocation框架下的地理位置管理类
GMSAutocompleteFetcher 搜索自动补全抓取器，通过该类的代理方法实现搜索自动补全
```` 
###### 8.自定义气泡
使用[SMCalloutView](https://github.com/nfarina/calloutview)
###### (1).添加标注
````
- (void)setMarkOnMapViewWithCoor:(CLLocationCoordinate2D)coor
                            Zoom:(float)zoom
{
    [self.mapView clear];//清除地图上所有的标注
    GMSCameraPosition *position = [[GMSCameraPosition alloc] initWithLatitude:coor.latitude longitude:coor.longitude zoom:zoom];
    [self.mapView setCamera:position];
    GMSMarker *marker = [GMSMarker markerWithPosition:coor];
    marker.icon = ImageNamed(@"bg_userLocal");
    marker.map = self.mapView;
    self.mapView.selectedMarker = marker;
}
````
######（2）气泡显示
````
- (UIView *)emptyCalloutView
{
    if (!_emptyCalloutView) {

        _emptyCalloutView = [[UIView alloc] init];
        _calloutView.backgroundColor = [UIColor clearColor];
    }
    return _emptyCalloutView;
}

- (GoogleCalloutView *)calloutView//这个自定义view继承SMCalloutView

{
    if (!_calloutView) {
        _calloutView = [[GoogleCalloutView alloc] initWithFrame:CGRectMake(0, 0, 260, 200)];
    }
    return _calloutView;
}

- (UIView *)mapView:(GMSMapView *)mapView markerInfoWindow:(GMSMarker *)marker
{
        CLLocationCoordinate2D anchor = marker.position;
        CGPoint point = [mapView.projection pointForCoordinate:anchor];
        self.calloutView.calloutOffset = CGPointMake(0, -20);
        self.calloutView.hidden = NO;
        CGRect calloutRect = CGRectZero;
        calloutRect.origin = point;
        calloutRect.size = CGSizeZero;
        //确定一个对象是否是当前类的成员
        if([marker isMemberOfClass:[GMSMarker class]]){
            GMSMarker *marker = (GMSMarker*) marker;
            [self.calloutView setTitle:self.model.name];
            [self.calloutView setPower:self.model.elec];
            [self.calloutView setDistance:self.model.distance];
            [self.calloutView setDistance:self.model.speed];
            [self.calloutView setLocationType:self.model.locationType];
            [self.calloutView setGpstime:self.model.gpstime];
            [self reversiGeocode:anchor];
        }
        [self.calloutView presentCalloutFromRect:calloutRect inView:mapView constrainedToView:mapView animated:YES];
        return self.emptyCalloutView;
}

- (void)mapView:(GMSMapView *)mapView didChangeCameraPosition:(GMSCameraPosition *)position
{
        //这里镜头移动时，气泡需要跟随移动
        if (mapView.selectedMarker != nil && !self.calloutView.hidden) {
            CLLocationCoordinate2D anchor = [mapView.selectedMarker position];

            CGPoint arrowPt = self.calloutView.backgroundView.arrowPoint;

            CGPoint pt = [mapView.projection pointForCoordinate:anchor];
            pt.x -= arrowPt.x;
            pt.y -= arrowPt.y + 20;

            self.calloutView.frame = (CGRect) {.origin = pt, .size = self.calloutView.frame.size };
        } 
}
````
###### 9.其他
######（1）.GMSCircle 
````
- (void)addOverlay:(CLLocationCoordinate2D)coor Radius:(CGFloat)radius
{
    GMSCircle *circle = [GMSCircle circleWithPosition:coor radius:radius];
    circle.fillColor =  RGBColor(41, 127, 249, 0.25);
    circle.strokeColor = RGBColor(41, 127, 249, 0.8);
    circle.map = self.mapView;
}
````
###### （2）.GMSPolyline
````
@property (nonatomic, strong) GMSMutablePath *paths;
@property (nonatomic, strong) GMSPolyline *polyline;
               [self.paths addCoordinate:coordinate0];
                [self.paths addCoordinate:coordinate];
                self.polyline.path = self.paths;
                UIColor *strokeColor= [UIColor colorWithRed:31/255.0 green:147/255.0 blue:255/255.0 alpha:1];
                self.polyline.strokeColor = strokeColor;
                self.polyline.strokeWidth = 2;
                self.polyline.map = self.mapView;
```` 
