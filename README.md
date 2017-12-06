# 组件功能LSMessage的主要功能是
第一阶段
1、多条提示信息可以按调用先后顺序先后展示
2、可以手动让当前正在展示的消息消失，比如点击整个view
3、支持只在指定的viewcontroller展示，和全局展示（非指定）
全局：切换controller后，新消息可以在新viewcontroller中展示，也就是全局消息会一直展示在当前window
----
下面是支持的信息类型：
2、展示内容：Success、Failed、Error、Message
3、展示位置：调用controller的Top、Bottom、OverNavBar
4、展示时长：自动消失、不能自动消失（需要点击本view的按钮进行消失）



第二阶段
可以支持button点击


# 类设计

## LSMessage--管理类，调度类
它是对外接口类，也是展示提示信息调用的管理类，他来实现以上”主要功能”的内容
方案一:
他如果不把view创建出来，他就要存储用户调用展示的model，每次创建一个view，这里不需要model，将提示信息，直接放入成员数组进行存储
方案二：
放入NSOperationQueue中，执行的时候，再创建view，需要model，放入NSOperation中



### 类方法
单例

```objective-c
[LSMessage showMessageWithTitle:@"Your Title"
subtitle:@"A description"
type:TSMessageNotificationTypeError];


// Add a button inside the message
[LSMessage showMessageInViewController:self
title:@"Update available"
subtitle:@"Please update the app"
image:nil
type:0
duration:0
atPosition:0
];

+ (void)dissmissActiveMessage;
```


## LSMessageView -- View类blurview
```o
UI展示提示信息样式：
icon左侧
title
subtitle
背景
button
```
### 动画 （done）
根据传入pos来做动画
自上而下出现，动画
自下而上出现，动画

消失动画，相反

### 支持横竖屏（done）
### 适配iPhone X
### 指定位置进行展示 --- todo

#   pod安装方法
pod 'LSMessage'

## Screenshots

**iOS 7 Design**

![iOS 7 Error](http://www.toursprung.com/wp-content/uploads/2013/09/error_ios7.png)

![iOS 7 Message](http://www.toursprung.com/wp-content/uploads/2013/09/warning_ios7.png)

