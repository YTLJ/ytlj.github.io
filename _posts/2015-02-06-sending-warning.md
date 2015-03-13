---
layout: post
title: “sending 'const NSString *' to parameter of type 'NSString *' discards qualifiers” warning
tags: [iOS]
---

###“sending 'const NSString *' to parameter of type 'NSString *' discards qualifiers” warning
在项目中碰到“sending 'const NSString *' to parameter of type 'NSString *' discards qualifiers” warning，代码如下：

{% highlight Objective-C %}
NSString const * ShopListDidClickShopNotification = @"ShopListDidClickShopNotification";

[[NSNotificationCenter defaultCenter] addObserverForName:ShopListDidClickShopNotification object:nil queue:nil usingBlock:^(NSNotification *note) {
//..
}];
{% endhighlight %}

期初以为是常量ShopListDidClickShopNotification声明有误，左改右改都没用，后来发现是NSNotificationCenter的调用有问题，正确的方式应该为：

{% highlight Objective-C %}
NSString const * ShopListDidClickShopNotification = @"ShopListDidClickShopNotification";

[[NSNotificationCenter defaultCenter] addObserverForName:(NSString *)ShopListDidClickShopNotification object:nil queue:nil usingBlock:^(NSNotification *note) {
     //...
}];
    
{% endhighlight %}