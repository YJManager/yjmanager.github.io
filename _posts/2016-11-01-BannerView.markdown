---
layout: post
title: YJBannerView 的使用方法
date: 2017-01-01 14:21:24.000000000 +09:00
---

🔥 非常火，使用简单、功能丰富的 `Objective-C版` 轮播控件, 基于 `UICollectionView` 实现, 多种场景均支持使用，并且支持100%自定义。

##  预览效果
<image src="https://ws3.sinaimg.cn/large/006tNc79ly1fi6k9kmghsg30dr0oju10.gif" width=250>

## 特性

- [x] 支持循环无限轮播(自动/手动)、非循环轮播
- [x] 支持自定义轮播内容
- [x] 支持自定义PageControl样式
- [x] 支持多个方向滚动
- [x] 支持自动滚动时间设置                               
- [x] 支持滚动相关手势的控制                            
- [x] 支持ContentMode的设置                            
- [x] 支持Banner标题的设置自定义
- [x] 支持自定义UICollectionViewCell                    
- [x] 支持自定义 UIView 填充BannerView
- [x] 支持在Storyboard\xib中创建并配置其属性   
- [x] 支持非首尾循环的Footer样式和进入详情回调
- [x] 不依赖其他三方SDWebImage或者AFNetworking设置图片
- [x] 支持CocoaPods
- [x] 支持Carthage
- [x] ......

## 安装

### [CocoaPods](http://cocoapods.org)

```ruby
    pod 'YJBannerView'
```

### [Carthage](https://github.com/Carthage/Carthage)
```ruby
    github "YJManager/YJBannerViewOC"
```

## 使用方法

### 1.创建BannerView
```objc
#pragma mark - 懒加载
- (YJBannerView *)bannerView{
    if (!_bannerView) {

        // 其中 selectorString 是给UIImageView设置图片和和placeholder的方法
        _bannerView = [YJBannerView bannerViewWithFrame:CGRectZero dataSource:self delegate:self placeholderImageName:@"placeholder" selectorString:@"setImageWithURL:placeholderImage:"];
    }
    return _bannerView;
}
```
### 2.实现数据源方法和代理:
```objc
// 将网络图片或者本地图片 或者混合数组
- (NSArray *)bannerViewImages:(YJBannerView *)bannerView{
    return self.imageDataSources;
}

// 将标题对应数组传递给bannerView 如果不需要, 可以不实现该方法
- (NSArray *)bannerViewTitles:(YJBannerView *)bannerView{
    return self.titlesDataSources;
}

// 代理方法 点击了哪个bannerView 的 第几个元素
-(void)bannerView:(YJBannerView *)bannerView didSelectItemAtIndex:(NSInteger)index{
    NSString *title = [self.titlesDataSources objectAtIndex:index];
    NSLog(@"当前%@-->%@", bannerView, title);
}
```

### 扩展自定义方法
```objc
// 自定义Cell方法
- (Class)bannerViewCustomCellClass:(YJBannerView *)bannerView{
    return [HeadLinesCell class];
}

// 自定义Cell的数据刷新方法
- (void)bannerView:(YJBannerView *)bannerView customCell:(UICollectionViewCell *)customCell index:(NSInteger)index{

    HeadLinesCell *cell = (HeadLinesCell *)customCell;
    [cell cellWithHeadHotLineCellData:@"打折活动开始了~~快来抢购啊"];
}
```

最后附上<a href="https://github.com/YJManager/YJBannerViewOC">Demo地址</a>
