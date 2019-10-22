#####1.问题描述
 要使地图的中心点位置像上偏移,让地图上的轨迹完全显示出来，不被下方的自定义View遮挡。
#####2.解决方法
这里直接使用百度地图SDK里面提供的方法，在BMKMapView初始化的时候设置地图的中心点
`[_BDmap setMapCenterToScreenPt:CGPointMake(SCREEN_WIDTH/2, SCREEN_HEIGHT/2 - 140)];`
````
/**
 * 设置地图中心点在地图中的屏幕坐标位置
 * @param ptInScreen 要设定的地图中心点位置，为屏幕坐标，设置的中心点不能超过屏幕范围，否则无效
 */
- (void)setMapCenterToScreenPt:(CGPoint)ptInScreen;
````
