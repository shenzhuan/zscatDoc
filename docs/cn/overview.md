---
layout: default_cn
title: Blade 简介
isDoc: true
docPage: overview
displayName: Overview
icon: home
---

## Blade 简介


 `blade` 意为利刃，刀剑；在中国冷兵器中刀剑的杀伤力可谓锐不可当，对它的名字没有很刻意的去琢磨，碰巧看到这个单词觉得比较喜欢，当然我希望它日后能够成为一把锐利的杀手锏。我个人的追求简洁和优雅的，所以在设计上不追求过度抽象。


 `blade` 借鉴了很多优秀mvc框架的设计，它是为java开发人员提供的便捷易用快速上手的一款框架，你可以用它快速开发API、Web 及后端服务等各种应用，本站也是基于Blade开发，源码在 [这里](https://github.com/biezhi/grice)！

 它提供了非常多的功能，内置ioc、rest路由，视图渲染，json返回，统一配置，aop，非orm的jdbc操作等等。框架对外提供很多扩展接口，支持开发者使用自己喜欢的，比如模版引擎，如果你的服务和框架设计理念符合我们愿意将它加入blade组件列表。

## “微” 是什么意思？

“微”(micro) 并不表示你需要把整个 Web 应用塞进单个 Java 文件，也不意味着 Blade 在功能上有所欠缺。微框架中的“微”意味着 Blade 旨在保持核心简单而易于扩展。Blade 不会替你做出太多决策——比如使用结合 `权限管理`。而那些 Blade 所选择的——比如使用何种模板引擎——则很容易替换。除此之外的一切都由可由你掌握。如此，Blade 可以与您珠联璧合。

[API 指南](http://bladejava.com/apidocs)

JDK 的最低版本要求为 **1.8**。

## 主要特性

- 轻量级。不依赖更多的库，摆脱SSH的臃肿，模块化设计，使用起来更轻便！
- 模块化(你可以选择使用哪些组件)
- Restful风格的路由接口
- No Orm (Active Record方式玩转数据库操作)
- 模板引擎支持
- 非web方式开发和发布

