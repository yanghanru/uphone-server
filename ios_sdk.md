## SDK下载
iOS SDK 用于 iOS 终端接入，支持端游和手游。SDK 提供了丰富的接口，满足大部分接入需求。接入方法请参见 [工程配置](https://docs.ucloud.cn/uphone/ios_sdk?id=工程配置)，并可通过接口说明页面，获取更多功能指引。

| SDK     | ZIP 包 | GitHub  |
| ----------- | ----------- | ----------- |
| iOS SDK | [下载](http://uphone-sdk.cn-bj.ufileos.com/uphone-ios-sdk.zip)| [GitHub 下载](https://github.com/ucloud/uphone-ios-sdk) | 

## 工程配置
### 导入SDK
将我们提供的SDK 压缩包中 UPhoneSDK.framework 导入项目中（记得选上Copy items if needed）.

### 配置权限
#### Target配置
Target中所需配置如下：

1、  TARGET -> General -> Frameworks,Libraries,and Embedded Contend -> UPhoneSDK.framework 选择 Embed & Sign.

2、  TARGET->Build Settings -> Build Options-> Enable Bitcode 选择 NO.

#### Info.plist文件配置
在工程文件下的 Info.plist文件中加入以下代码：
```
<key>NSMicrophoneUsageDescription</key>
 <string>此App将要访问您的麦克风</string>
<key>NSAppTransportSecurity</key>  
<dict>  
<key>NSAllowsArbitraryLoads</key>
<true/>  
</dict>
```
注：麦克风权限文字可根据自己App修改。

## 接入步骤
为方便 iOS 开发者调试和接入云游戏产品 API，这里向您介绍适用于 iOS 开发的快速接入文档。快速入门文档只提供最主要的接入接口，更多详细接口请参考 本文“[接口说明](https://docs.ucloud.cn/uphone/ios_sdk?id=接口说明)”部分。

| 重要接口            | 接口含义             | 建议调用时机            |
|:-------- |:-------- |:------- |
|initWithUphone|初始化SDK|连接云手机需要展示云手机界面时|

说明：
SDK 使用前请对工程进行配置，否则 SDK 不生效。

### 初始化SDK
函数原型
```
- (instancetype)initWithUphone:(NSString *)uphoneId;
```
| 参数            | 类型             | 意义            |
|:-------- |:-------- |:------- |
|uphoneId|NSString|接入商的唯一 ID，用来区分不同的接入商。|
|token|NSString|连接访问校验值(注:如果调用api接口SetUPhoneToken进行了设置，此处为必填,否则填空)|

示例代码
```
UTestVideoViewController *videoCallViewController = [[UTestVideoViewController alloc] initWithUphone:phoneId];
videoCallViewController.token = @"123456";
```
## 接口说明
### 连接云手机
函数原型
```
- (void)connectUPhone;
```
示例代码
```
[self connectUPhone];
```
注：self是UPhoneVideoViewController的子类
### 断开云手机
函数原型
```
- (void)disConnectUPhone;
```
示例代码
```
[self disConnectUPhone];
```
注：self是UPhoneVideoViewController的子类
### 重连云手机
函数原型
```
+ (void)reconnetUPhone;
```
示例代码
```
[UPhoneService reconnetUPhone];
```
### 设置分辨率
设置UPhone分辨率

函数原型
```
- (void)setUPhoneResolution:(int)resolution;
```
| 参数            | 类型             | 意义            |
|:-------- |:-------- |:------- |
|resolution|int|0    // 标清<br>3   // 高清<br>6  // 超清 |

示例代码
```
[self setUPhoneResolution: resolution];
```
注：self是UPhoneVideoViewController的子类
### 获取网络延时
函数原型
```
- (NSInteger)getUPhoneLinkDelay;
```
示例代码
```
- (NSInteger)getUPhoneLinkDelay;
```
注：self是UPhoneVideoViewController的子类
### 获取SDK版本号
函数原型
```
+ (NSString *) getVersionCode;
```
示例代码
```
NSString *delay = [UPhoneService getVersionCode];
```
### 云手机加速
函数原型
```
- (void)speedUpUPhone;
```
示例代码
```
[self speedUpUPhone];
```
注：self是UPhoneVideoViewController的子类
### 云手机返回到桌面
函数原型
```
- (void)backUPhoneHome;
```
示例代码
```
[self backUPhoneHome];
```
注：self是UPhoneVideoViewController的子类
### 云手机返回到上一级界面
函数原型
```
- (void)backUPhoneLastPage;
```
示例代码
```
[self backUPhoneLastPage];
```
注：self是UPhoneVideoViewController的子类
### 获取网络速度
云手机获取当前网络速度

函数原型
```
- (NSString *)getNetworkSpeed;
```
返回参数说明： 返回值类型为NSString，单位为 MB/s，保留两位小数，例如：0.15MB/s。

示例代码
```
NSString *networkSpeed = [self getNetworkSpeed];
```
注：self是UPhoneVideoViewController的子类
### 开始直播
开始直播推流

函数原型
```
- (void)startLiving:(NSString *)url;
```
| 参数            | 类型             | 意义            |
|:-------- |:-------- |:------- |
|url|NSString|直播推流地址|

示例代码
```
[strongSelf startLiving:url];
```
注：self是UPhoneVideoViewController的子类
### 停止直播
函数原型
```
- (void)stopLiving;
```
示例代码
```
[self stopLiving];
```
注：self是UPhoneVideoViewController的子类
### 获取当前播放器截屏
云手机启动后，如果想要获取当前播放器截屏，可以调用此函数

函数原型
```
- (UIImage *)getShortcut;
```
返回参数说明： 返回当前播放器截屏的 UIImage 对象 

示例代码
```
UIImage *image = [self getShortcut];
```
注：self是UPhoneVideoViewController的子类
### 检测当前截屏是否黑屏
如果检测当前截屏的UIImage对象是否黑屏功能，调用此函数

函数原型
```
- (NSInteger)checkBlackScreen:(UIImage *)image;
```
| 参数            | 类型             | 意义            |
|:-------- |:-------- |:------- |
|image|Image|当前需要检测的UIImage对象|

返回参数说明： 

1//检测结果为纯色 排除黑色和全透明色，因为播放器没开始工作，不通设备获取截屏有的是纯黑色有的是纯透明色 

2//检测结果为纯透明色 

3//检测结果为正常 

4//检测结果为纯黑色

示例代码
```
NSInteger color = [self checkBlackScreen:image];
```
注：self是UPhoneVideoViewController的子类
### 获取丢包率
获取网络传输过程中的丢包率

函数原型
```
- (NSString *)getLossRate;
```
返回参数说明： 返回值类型为NSString，已转化成百分比并且保留两位小数，例如：0.15%。

示例代码
```
NSString *lossRate = [self getLossRate];
```
注：self是UPhoneVideoViewController的子类
### 获取视频流基本参数接口
获取视频分辨率、横竖屏参数

函数原型
```
- (NSDictionary *)getQRCodeData;
```
返回参数说明:NSDictionary 类型参数

// key值为style，value返回值为0时表示横屏，value为1时表示竖屏；

// key值为height，value返回值即为当前分辨率的height；

// key值为width，value返回值即为当前分辨率的width。

示例代码
```
NSDictionary *dic =  [strongSelf getQRCodeData];
NSString *style = [dic valueForKey:@"style"];
NSString *height = [dic valueForKey:@"height"];
NSString *width = [dic valueForKey:@"width"];
```
注：self是UPhoneVideoViewController的子类
### 获取用户最后一次操作时间戳
云手机启动后，通过该接口获取用户最后一次操作实例的时间戳
函数原型
```
+ (NSString *)getLastUserOperationTimestamp;
```
返回参数说明:NSString 类型参数，单位为：ms。

0//默认返回 0，代表用户没有操作过实例，否则返回相应时间戳 

示例代码
```
NSString *lastUserOperationTimestamp = [UPhoneService getLastUserOperationTimestamp];
```
### 是否支持直播
云手机启动后，通过该接口获取是否支持直播

函数原型
```
- (NSString *)isSupportLiving;
```
返回参数说明:NSString 类型参数

0//未设置

1//正在启动推流

2//正在推流

3//已停止推流

示例代码
```
NSString *isLiveStr = [self isSupportLiving];
```
注：self是UPhoneVideoViewController的子类
### 静音开关功能
设置当前的播放是否为静音状态

函数原型
```
- (void)setAudioMute:(BOOL)isMute;
```
传入参数说明:BOOL类型参数

YES：全局静音

NO：取消全局静音

示例代码
```
BOOL mute1 = [self setAudioMute:YES];
BOOL mute2 = [self setAudioMute:NO];
```
注：self是UPhoneVideoViewController的子类
## 注意事项
1.该SDK仅支持iOS10以上系统。

2.该SDK仅支持真机运行。

3.需要用到SDK的地方增加头文件#import <UPhoneSDK/UPhoneSDK.h>

4.跳转到新建子类的界面时，前者需要遵守< UPhoneVideoViewControllerDelegate>协议，在退出云手机时需要的一些方法可以写在协议方法里面。

5.每次进入云手机会从远端获取分辨率，可以根据自己的需求修改相应的分辨率可以参照[设置分辨率](https://docs.ucloud.cn/uphone/ios_sdk?id=设置分辨率)。
