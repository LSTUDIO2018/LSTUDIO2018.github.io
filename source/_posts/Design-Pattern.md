---
title: Design Pattern
date: 2020-10-04 00:52:09
tags:
---





在策略模式（Strategy Pattern）中，一个类的行为或其算法可以在运行时更改。这种类型的设计模式属于行为型模式。

在策略模式中，我们创建表示各种策略的对象和一个行为随着策略对象改变而改变的 context 对象。策略对象改变 context 对象的执行算法

{%asset_img Strategy.svg%}

![](Design-Pattern/Strategy.svg)





当对象间存在一对多关系时，则使用观察者模式（Observer Pattern）。比如，当一个对象被修改时，则会自动通知依赖它的对象。观察者模式属于行为型模式。

{%asset_img Observer.svg%}

![](Design-Pattern/Observer.svg)

装饰器模式（Decorator Pattern）允许向一个现有的对象添加新的功能，同时又不改变其结构。这种类型的设计模式属于结构型模式，它是作为现有的类的一个包装。

{%asset_img Decorator.svg%}

![](Design-Pattern/Decorator.svg)