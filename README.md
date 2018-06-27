# ZXCNoDataPlaceholder

[![License](https://img.shields.io/badge/License-%20Apache%20LICENSE%202.0-yellow.svg)]()
[![CocoaPods](https://img.shields.io/badge/pod-1.0.0-green.svg)]()
[![Support](https://img.shields.io/badge/support-iOS7.0+-blue.svg?style=flat)](https://www.apple.com/nl/ios/)

一个超级简单易用的UITableView和UICollectionView的空数据占位图，可区分实现网络错误状态和空数据状态

![数据图片](./img.png)

## 使用说明


0. CocoaPods

```
pod 'XCNoDataPlaceholder'
```

1.引用头文件ZXCNoDataPlaceholder.h

2.遵循协议，实现对应的代理方法


## Protocol

```
/**
 无数据占位图
 */
- (UIImage *)PlaceholderNoDataImage;
/**
 网络错误的占位图
 */
- (UIImage *)PlaceholderNetErrorImage;
/**
 占位图尺寸。默认200*200
 */
- (CGSize)PlaceholderImageSize;
/**
 图片位置调整
 */
- (UIOffset)PlaceholderOffset;
/**
 刷新按钮
 */
- (UIButton *)PlaceholderRefreshButton;

```
注意：若要实现网络错误状态下显示相应占位图需给zxcBackgroundImageNetStateBlock赋值 return YES表示网络正常


## TableViewDemo（CollectionView使用方式相同）

```
<ZXCNoDataPlaceholderDelegate>

//-----

_tableView.placeholderImageDelegate = self;

//------

- (UIImage *) PlaceholderNoDataImage{
    return [UIImage imageNamed:@"noData"];
}

- (UIImage *)PlaceholderNetErrorImage{
	return [UIImage imageNamed:@"netErr"];
}

- (UIButton *)PlaceholderRefreshButton{
    UIButton * refreshButton = [[UIButton alloc] initWithFrame:CGRectMake(0, 0, 200, 40)];
    return refreshButton;
}


```

## 网络错误占位图

需要在网络状态监听器中做状态修改

```
e.p.
[[AFNetworkReachabilityManager sharedManager]setReachabilityStatusChangeBlock:^(AFNetworkReachabilityStatus status) {
    if (status == AFNetworkReachabilityStatusNotReachable) {
        zxcPlaceholderNetState = NO;
    }else{
        zxcPlaceholderNetState = YES;
    }
}];

```



## Apache License 2.0


