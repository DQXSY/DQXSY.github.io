####1.UDP简介
UDP（User Data Protocol，用户数据报协议）是与TCP相对应的协议。它是面向非连接的协议，UDP传送数据不需要和服务器连接，只需要知道ip和监听端口，不需要链接没有目的的socket，只是将数据报投递出去，不管接收方是否成功接收到，因此是一种不可靠的传输。但是UDP的开销更小数据传输速率更高，因为不必进行收发数据的确认，所以UDP的实时性更好。
####2.UDP特点
1.无连接，发送数据之前不需要建立连接。开销和发送之前的时间延迟较短。 2.尽最大努力交付。（可以采取一定策略实现可靠传输） 3.面向报文，UDP对应用程序交付的报文，添加UDP首部后直接交给IP层。不合并，不拆分。 4.没有拥塞控制，网络拥塞不会使源主机发送率降低。 5.UDP支持一对一，一对多，多对一的交互通信 6.UDP首部开销较小，8字节（TCP为20字节、IP为20字节）
####3.UDP开发可使用的类库
1.AsyncUdpSocket
2.GCDAsyncUdpSocket
####4.AsyncUdpSocket开发使用说明

在项目中，所用到的类库是AsyncUdpSocket，所以这里基于AsyncUdpSocket对UDP开发做一个简单的文档说明：
1.将AsyncUdpSocket.h, AsyncUdpSocket.m文件拷贝到项目中。在项目target -> build phases -> compile sources -> AsyncUdpSocket文件后面加入 -fobjc-arc ，这是为了使编译器编译的时候将此文件在arc的条件下编译。
2.添加CFNetwork.framework
####5.代码示例
````
@property (nonatomic, strong) AsyncUdpSocket *reciveSocket;//负责接受收数据
@property (nonatomic, strong) AsyncUdpSocket *sendSocket;//负责发送数据
@property (nonatomic, strong) NSString *socketHost;//指定Ip地址发送，这里取的是第一个发送心跳包过来的Ip
@property (nonatomic, strong) NSTimer *heartBeatTimer;//心跳定时器
````
初始化socket,设置代理，绑定端口号
````
//收
self.reciveSocket = [[AsyncUdpSocket alloc] initIPv4];
[self.reciveSocket setDelegate:self];
[self.reciveSocket bindToPort:1917 error:nil];
[self.reciveSocket receiveWithTimeout:-1 tag:0];
//发
self.sendSocket = [[AsyncUdpSocket alloc] initIPv4];
[self.sendSocket setDelegate:self];
[self.sendSocket connectToHost:self.socketHost onPort:1918 error:nil];
[self.sendSocket enableBroadcast:YES error:nil];
//开启定时器
self.heartBeatTimer = [NSTimer scheduledTimerWithTimeInterval:5 target:self selector:@selector(heartBeatToSocket) userInfo:nil repeats:YES];
[self.heartBeatTimer fire];
````
心跳包就是广播255.255.255.255，确保在同一局域网的都能收到心跳
````
NSString *heartBeat = @"heartBeat";
NSData *sendData = [heartBeat dataUsingEncoding:NSUTF8StringEncoding];
if ([self.sendSocket sendData:sendData toHost:@"255.255.255.255" port:1917 withTimeout:-1 tag:1]) {
    NSLog(@"发送指令成功");
}else {
    NSLog(@"发送指令失败"); 
}
[self.sendSocket receiveWithTimeout:-1 tag:1]; 
[self.reciveSocket receiveWithTimeout:-1 tag:0];
````
AsyncUDPSocketDelegate的代理方法
````
- (void)onUdpSocket:(AsyncUdpSocket *)sock didSendDataWithTag:(long)tag
{
    //!<信息发送成功
}
- (BOOL)onUdpSocket:(AsyncUdpSocket *)sock didReceiveData:(NSData *)data withTag:(long)tag fromHost:(NSString *)host port:(UInt16)port
{
    //过滤来自本机的消息 继续监听接收消息
    NSString *IPAdress = host;
    if ([IPAdress isEqualToString:[IPHelper deviceIPAdress]]) {
        [self.reciveSocket receiveWithTimeout:-1 tag:0];
        return YES;
    }
    self.socketHost = host;
    //!<接收到了信息  在这里解包
    NSString *reciveStr  =[[NSString alloc] initWithData:data encoding:NSUTF8StringEncoding];
    if ([reciveStr isEqualToString:@"heartBeat"]) {
        [self heartBeatToSocket];//收到心跳包后回应一个心跳
    }else {
        if (self.block) {
            self.block(reciveStr);
        }
    }
    return YES;
}
- (void)onUdpSocket:(AsyncUdpSocket *)sock didNotSendDataWithTag:(long)tag dueToError:(NSError *)error
{
    NSLog(@"发送失败：%@",error);
}
-(void)onUdpSocket:(AsyncUdpSocket *)sock didNotReceiveDataWithTag:(long)tag dueToError:(NSError *)error
{
    NSLog(@"接受失败：%@",error);
}
````
####6.Demo
[传送门](https://github.com/DQXSY/UdpSocketDemo.git)
