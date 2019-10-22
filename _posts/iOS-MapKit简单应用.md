####1.地图显示
1）引用头文件
````
#import <MapKit/MapKit.h>
`````
2)初始化地图控件MKMapView
````
- (MKMapView *)mapView
{
    if (!_mapView) {

        _mapView = [[MKMapView alloc] initWithFrame:CGRectMake(0, 0, SCREEN_WIDTH, SCREEN_HEIGHT)];
        _mapView.delegate = self;
        _mapView.showsCompass = YES; // 是否显示指南针      
        _mapView.showsScale = YES;// 是否显示比例尺
        _mapView.showsTraffic = YES;// 是否显示交通
        _mapView.showsBuildings = YES// 是否显示建筑物
    }
    return _mapView;
}
````
3）把mapView加载到当前的view上

