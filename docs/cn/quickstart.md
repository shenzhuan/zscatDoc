---
layout: default_cn
title: 快速入门
isDoc: true
docPage: quickstart
displayName: quickstart
icon: home
---

# 第一个Bldae程序

迫不及待要开始了吗？本页提供了一个很好的 Blade `Hello World` 介绍。

## 开发启程

创建一个 maven 工程，加入 Blade 依赖：

![](https://ooo.0o0.ooo/2016/09/07/57cf914bc1eb3.png)

![](https://ooo.0o0.ooo/2016/09/07/57cf91670569f.png)

![](https://ooo.0o0.ooo/2016/09/07/57cf91702328c.png)

```xml
<dependencies>
	<dependency>
		<groupId>com.bladejava</groupId>
		<artifactId>blade-core</artifactId>
		<version>1.7.2-beta</version>
	</dependency>
	<dependency>
		<groupId>com.bladejava</groupId>
		<artifactId>blade-embed-jetty</artifactId>
		<version>0.1.3</version>
	</dependency>
</dependencies>
```

创建启动类：

```java
package com.xxx.first;

import static com.blade.Blade.$;

import com.blade.mvc.http.Request;
import com.blade.mvc.http.Response;
import com.blade.mvc.handler.RouteHandler;

public class Application {

	public static void main(String[] args) {
		$().get("/", (request, response) -> {
			response.html("<h1>Hello Blade</h1>");
		}).start(Application.class);
	}
	
}
```

我们还需要加一个 `log4j` 的配置文件，因为 blade 目前默认使用log4j作为日志服务，如果你倾向于其他的也可以配置。

_log4j.properties_

```bash
log4j.rootLogger = info, stdout
log4j.appender.stdout = org.apache.log4j.ConsoleAppender
log4j.appender.stdout.layout = org.apache.log4j.PatternLayout
log4j.appender.stdout.layout.ConversionPattern = [hello] %d %-5p [%t] %c | %m%n
```

将这个文件放在 `classpath` 下即可，如果你不这么做也不会报错，只是控制台看不到日志输出 :)

配置一下 `jdk8`，因为我们使用了 `maven` 有些同学默认的编译版本是8以下，所以可以在`pom.xml`加入以下配置指定编译版本：

```xml
<properties>
  <maven.compiler.source>1.8</maven.compiler.source>
  <maven.compiler.target>1.8</maven.compiler.target>
  <maven.compiler.compilerVersion>1.8</maven.compiler.compilerVersion>
</properties>
```

也有其他方法可以设置，点[这里](http://www.blogjava.net/fancydeepin/archive/2015/06/23/maven-jdk.html)看看

ok，现在启动 `Application` 的main函数你将看:

```bash
[hello] 2016-09-07 16:06:14,596 DEBUG [main] com.blade.config.ApplicationConfig | Add Resource: /public
[hello] 2016-09-07 16:06:14,597 DEBUG [main] com.blade.config.ApplicationConfig | Add Resource: /assets
[hello] 2016-09-07 16:06:14,597 DEBUG [main] com.blade.config.ApplicationConfig | Add Resource: /static
[hello] 2016-09-07 16:06:14,601 INFO  [main] com.blade.mvc.route.Routers | Add Route => GET	/
[hello] 2016-09-07 16:06:14,601 INFO  [main] com.blade.kit.base.Config | Load config [classpath:app.properties]
[hello] 2016-09-07 16:06:14,609 INFO  [main] com.blade.kit.base.Config | Load config [classpath:jetty.properties]
[hello] 2016-09-07 16:06:14,625 INFO  [main] org.eclipse.jetty.util.log | Logging initialized @188ms
[hello] 2016-09-07 16:06:14,715 INFO  [main] org.eclipse.jetty.server.Server | jetty-9.2.12.v20150709
[hello] 2016-09-07 16:06:14,886 INFO  [main] com.blade.mvc.DispatcherServlet | jdk.version	=> 1.8.0_101
[hello] 2016-09-07 16:06:14,886 INFO  [main] com.blade.mvc.DispatcherServlet | user.dir		=> D:\workspace\first-blade-app
[hello] 2016-09-07 16:06:14,886 INFO  [main] com.blade.mvc.DispatcherServlet | java.io.tmpdir	=> C:\Users\ADMINI~1\AppData\Local\Temp\
[hello] 2016-09-07 16:06:14,886 INFO  [main] com.blade.mvc.DispatcherServlet | user.timezone	=> GMT+08:00
[hello] 2016-09-07 16:06:14,886 INFO  [main] com.blade.mvc.DispatcherServlet | file.encodin	=> UTF-8
[hello] 2016-09-07 16:06:14,888 INFO  [main] com.blade.mvc.DispatcherServlet | blade.webroot	=> D:\workspace\first-blade-app\target\classes
[hello] 2016-09-07 16:06:14,893 INFO  [main] com.blade.mvc.DispatcherServlet | blade.isDev = true

		 __, _,   _, __, __,
		 |_) |   /_\ | \ |_
		 |_) | , | | |_/ |
		 ~   ~~~ ~ ~ ~   ~~~
		 :: Blade :: (v1.7.2-beta)

[hello] 2016-09-07 16:06:14,896 INFO  [main] com.blade.mvc.DispatcherServlet | Blade initialize successfully, Time elapsed: 10 ms.
[hello] 2016-09-07 16:06:14,896 INFO  [main] org.eclipse.jetty.server.handler.ContextHandler | Started o.e.j.w.WebAppContext@5a61f5df{/,file:/D:/workspace/first-blade-app/target/classes/,AVAILABLE}
[hello] 2016-09-07 16:06:14,944 INFO  [main] org.eclipse.jetty.server.ServerConnector | Started ServerConnector@3e6fa38a{HTTP/1.1}{0.0.0.0:9000}
[hello] 2016-09-07 16:06:14,944 INFO  [main] org.eclipse.jetty.server.Server | Started @514ms
[hello] 2016-09-07 16:06:14,944 INFO  [main] com.blade.embedd.EmbedJettyServer | Blade Server Listen on 0.0.0.0:9000
```

打开浏览器，输入 [http://127.0.0.1:9000](http://127.0.0.1:9000)

wow~ 看起来还不错，这就算走进 Blade 的大门了。


## 都做了什么？

1. 首先，我们创建了 `Application` 类。这个类的是整个程序启动类，它是程序的入口。
2. 接下来，创建了一个路由，创建的方式是 `new RouteHandler`。
3. 通过 `Response` 对象渲染html。
4. 添加 `log4j.properties` 日志配置文件
5. 启动 `start` 方法 

## 了解更多

以上的描述介绍了这个应用的启动，虽然它看起来很简单，但也是一个基本的 Blade 应用，我们要开始一个完整的web项目会有如下的一些疑问：

- start方法为什么要传入 `Application.class` ？
- 创建路由还有什么方式？
- 我想更换日志组件怎么办？
- 我想使用模板引擎？
- 配置文件要写在哪里？
- 如何部署到服务器？

等等一系列的问题，作为框架设计者，已经为大家准备好了，如果你是一个web开发的老手可以看看[这个](https://github.com/otale/tale)项目，当然新手直接晋级也是没关系的，因为它非常简单。

> 在开发的过程中有疑问可以参考文档中的其他解释和查看API基本就可以搞定一切！
