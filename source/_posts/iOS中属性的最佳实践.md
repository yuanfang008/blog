title: iOS中属性的最佳实践
catAlias: iOS
categories: iOS
date: 2015-12-10 13:29:23
timestamp: 1449725518
tags: iOS，property
keywords: iOS，property
description: 在iOS开发中，属性和成员变量有何区别，最佳实践是神马，本文将试着为您揭开这些疑惑。
---
#### 在iOS开发中，属性和成员变量有何区别，最佳实践是神马，本文将试着为您揭开这些疑惑。

> 关于属性和成员变量

```
@interface MyViewController :UIViewControlle
{
    UIButton *myButton;
}
@property (nonatomic, retain) UIButton *myButton;
@end
```

##### 类与类别中添加的属性要区分开来，因为类别中只能添加方法，不能添加实例变量。经常会在ios的代码中看到在类别中添加属性，这种情况下，是不会自动生成实例变量的。比如在：UINavigationController.h文件中会对UIViewController类进行扩展

```
@interface UIViewController (UINavigationControllerItem)
@property(nonatomic,readonly,retain) UINavigationItem *navigationItem;
@property(nonatomic) BOOL hidesBottomBarWhenPushed;
@property(nonatomic,readonly,retain) UINavigationController *navigationController;
@end
```

  这里添加的属性，不会自动生成实例变量，这里添加的属性其实是添加的getter与setter方法。
  注意一点，匿名类别(匿名扩展)是可以添加实例变量的，非匿名类别是不能添加实例变量的，只能添加方法，或者属性（其实也是方法）。

#### 成员变量用于类内部，无需与外界接触的变量。根据成员变量的私有性，为了方便访问，所以就有了属性变量。属性变量的好处就是允许让其他对象访问到该变量。当然，你可以设置只读或者可写等，设置方法也可自定义。所以，属性变量是用于与其他对象交互的变量。

#### 一些建议:
1. 如果只是单纯的private变量，最好声明在implementation里.
2. 如果是类的public属性，就用property写在.h文件里
3. 如果自己内部需要setter和getter来实现一些东西，就在.m文件的类目里用property来声明

> 关于属性修饰符的最佳实践

#### 关于objective-C的属性，常见的有：strong、weak、copy、assign
1. 对于基本数据类型，当然使用assigin；
2. 对于mutable的，一定要使用strong。父控件UI元素也使用strong；
3. 子控件元素使用weak；
4. 不可变的类型，使用copy。（NSString,NSArray,NSDictonary这些一定要用copy），对于mutable的对象，如果是mutable的却定义属性为copy，则往里面加值时可能引起程序崩溃。而对于不可变的使用了strong，则可能引起值改变，这就违背了内存管理语义

#### 关于是否使用`self`或直接获取属性的讨论，`《effective objectivec 2.0》`一书中指出，内部获取值直接用下划线方式，显然不经过方法派送速度会更快。而设置值时使用`self.xx`则能保证正确的内存管理。
