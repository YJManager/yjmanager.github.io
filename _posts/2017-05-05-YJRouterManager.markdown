---
layout: post
title: YJRouterManager 的使用方法
date: 2017-05-05 14:21:24.000000000 +09:00
---

### 效果
![](https://ws3.sinaimg.cn/large/006tNc79ly1fi6oaqx4ucg30a80izgul.gif)

## 安装

### [CocoaPods](http://cocoapods.org)

```ruby
    pod 'YJRouterManagerOC'
```

### 使用方法
#### 在 AppDelegate 初始化注册
```objc
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {

    self.window = [[UIWindow alloc] initWithFrame:CGRectMake(0, 0, [UIScreen mainScreen].bounds.size.width, [UIScreen mainScreen].bounds.size.height)];

    // 初始化路由器
    [[YJRouterManager sharedInstance] registerMainScheme:nil keyWindow:self.window];

    // 其他设置...

    [self.window makeKeyAndVisible];
return YES;
}
```

#### 在 YJRouterManagerConfig.plist 配置映射关系 或者 在控制器中手动注册
##### Plist 方式
![](https://ws2.sinaimg.cn/large/006tNc79ly1fi6ocx1oqqj30k908ndh8.jpg)

##### 控制器注册方式

```objc

+ (void)load{
    [YJRouterManager registerRouterCode:@"R1101" customInitBlock:nil];
}

```

#### Push 方式
```objc
/**
push 方式打开

@param url 路由url 比如: "yj://1101?id=2001"
@param parameter 参数字典
@param navigationController 导航控制器 如果是nil, 默认当前导航 并不是present的导航
@param complete 初始化完成的回调
*/
+ (void)pushViewControllerUrl:(NSString *)url parameter:(NSDictionary *)parameter navigationController:(UINavigationController *)navigationController complete:(YJViewControllerCreatedBlock)complete;
```

#### Present 方式
```objc
/**
present 方式打开

@param url 路由url 比如: "yj://1101?id=2001"
@param parameter 参数字典
@param showType 显示类型 带导航还是不带
@param sourceViewController 起始控制器 如果是nil 默认是window根控制器
@param packingNavigationBlock 包装导航方法
@param complete 初始化完成的回调
*/
+ (void)presentViewControllerUrl:(NSString *)url parameter:(NSDictionary *)parameter showType:(YJRouterShowType)showType sourceViewController:(UIViewController *)sourceViewController packingNavigationBlock:(YJPackingNavigationBlock)packingNavigationBlock complete:(YJViewControllerCreatedBlock)complete
```


