# LunarCore
小历（iOS & OS X）的农历核心部分。

# 何为小历

<a href="https://itunes.apple.com/app/id1031088612">![](https://cdn.rawgit.com/cyanzhong/LunarCore/master/App_Store.svg)</a>
<a href="https://itunes.apple.com/app/id1114272557">![](https://cdn.rawgit.com/cyanzhong/LunarCore/master/Mac_App_Store.svg)</a>

小历是一个简洁的农历 app，目前支持 iOS & OS X 两端，iOS 端多次被 App Store 官方推荐。
![image](https://github.com/cyanzhong/LunarCore/raw/master/iOS.png)
![image](https://github.com/cyanzhong/LunarCore/raw/master/Mac.png)

# 前世今生
LunarCore 最早来自于一个 JavaScript 编写的农历库：[LunarCalendar](https://github.com/zzyss86/LunarCalendar)。

出于性能原因，我将其用 Objective-C 重写，同时改进了原版里面一些数据不准确的问题。LunarCore 现已工作在小历上面，在未来可能会使用 Swift 重写。

为了更灵活的抽离，LunarCore 不包含任何 UI 实现，所有的数据均以 Dictionary 的形式透出。

# 食用方法
```Objective-C
#import "AppDelegate.h"
#import "LunarCore.h"

@implementation AppDelegate

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    
    NSDictionary *lunarCalendar = calendar(2016, 5);
    NSLog(@"%@", lunarCalendar);
    
    return YES;
}

@end
```

即获得一个 2016年5月 的日历数据，你可以方便的用其实现 UI 部分，利用 LunarCore，我使用一周的时间将 iOS 版本的小历移植到了 OS X。

更多内部接口请参考：[LunarCore/LunarCore.m](https://github.com/cyanzhong/LunarCore/blob/master/LunarCore/LunarCore.m)

# 温馨提示
计算农历的耗时较长（主要是节气计算，如果你不需要也可以直接去掉），如果你在 UI 上面每次日历变化都计算一次，显然是不划算的做法。我个人的建议是做内存和文件缓存，小历的缓存策略如下（以 2016年5月 日历为例）：

- 从内存中读取 2016.5 的日历
- 没有读到的话从文件中读取
- 还是没有读到的话构建 2016.5 的日历
- 构建日历后缓存到文件和内存
- 在子线程生成上个月和下个月的日历

# 联系方式
Weibo: [@StackOverflowError](http://weibo.com/0x00eeee/)

Twitter: [@cyanapps](https://twitter.com/cyanapps)

Email: [log.e@qq.com](mailto:log.e@qq.com)
