---
title: Zeplin
date: 2018-10-17 17:14:57
tags:
---

[https://zeplin.io/](https://zeplin.io/)

### 设计师与开发者协作的工具

{% asset_img designer.png %}

设计师，使用Zeplin插件可以从Sketch，PhotoShop等设计工具直接导出标注稿，无需手动标注，同一个页面的模块不需要在不同的地方标注。
<br>
开发者，在写布局的时候，不会再为找不到标注，找不到字体，找不到色值而感到烦恼，从而降低了开发过程中的沟通成本。同时还可以提高设计的还原度。

#### 单行文本

{% asset_img single_line_label.png %}

#### 多行文本 (Zeplin)
{% asset_img multi_line_label.png %}

``` objc
    NSString *multiLineString = @"blablablablablablablabla";
    NSAttributedString *attributedString = multiLineString.typeface.font([UIFont ajkH3Font]).color([UIColor ajkBlackColor]).lineHeight(24.0).lineBreakMode(NSLineBreakByTruncatingTail).compose;

```

#### 多行文本（设备）

{% asset_img multi_line_label_device.png %}

#### lineSpacing vs lineHeight

纯英文的文本，lineSpacing设置为6.0

{% asset_img english_with_linespacing.png %}

中文文本，lineSpacing设置为6.0
{% asset_img chinese_with_linespacing.png %}

纯英文文本，lineHeight设置为22.0


{% asset_img english_with_lineheight.png %}

中文文本，lineHeight设置为22.0

{% asset_img chinese_with_lineheight.png %}


#### 阴影

{% asset_img shadow.png %}

``` objc
    view.layer.shadowOffset =  CGSizeMake(0.0, 2.0);
    view.layer.shadowRadius = blur / 2.0;
    view.layer.shadowColor = [UIColor ajkLineNavColor].CGColor;
    view.layer.shadowOpacity = 0.3;
    
    CGRect shadowRect = UIEdgeInsetsInsetRect(view.bounds, UIEdgeInsetsMake(-spread, -spread, -spread, -spread));
    view.layer.shadowPath = [UIBezierPath bezierPathWithRect:shadowRect].CGPath;
    
    // view本身背景色是透明的情况下，阴影会添加到有背景色的某个subview上
    view.backgroundColor = [UIColor whiteColor];
```

#### 渐变图层

{% asset_img gradient_layer.png %}

``` objc
    渐变图层不会标注渐变的方向，有时，需要UED以note的形式说明一下。
    另外， CAGradientLayer 本身只支持Frame
    如果某些特殊的场景需要使用autolayout， 可以使用 RTGradientView
```

#### 字间距

{% asset_img letter_spacing.png %}

``` objc
// NSKernAttributeName
NSAttributedString *title = RFAttributedString(@"绿化".typeface.kern(7.3).compose, @"率");

```

#### 安利一波 (RFTypeface)

RFTypeface 使 NSAttributedString 使用起来更加简洁，支持链式语法;

#### Talk Is Cheap

``` objc

// before 
NSAttributedString *hello = [[NSAttributedString alloc] initWithString:@"hello " attributes:@{ NSFontAttributeName : [UIFont boldSystemFontOfSize:22.0], NSForegroundColorAttributeName : kRGB(232.0, 74.0, 1.0) }];
NSAttributedString *world = [[NSAttributedString alloc] initWithString:@"world" attributes:@{ NSFontAttributeName : [UIFont systemFontOfSize:22.0], NSForegroundColorAttributeName : [UIColor blackColor] }];
NSMutableAttributedString *attributedString = [[NSMutableAttributedString alloc] init];
[attributedString appendAttributedString:hello];
[attributedString appendAttributedString:world];
self.label.attributedText = attributedString;

// after:
NSAttributedString *hello = @"hello".typeface.bold(22.0).rgb(232, 74, 1).compose;
NSAttributedString *world = @"world".typeface.normal(22.0).rgb(0, 0, 0).compose;
self.label.attributedText = RFAttributedString(hello, @" ", world);

```