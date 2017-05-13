---
layout: default_cn
title: 框架配置
isDoc: true
docPage: configuration
displayName: configuration
---


# 框架配置

Blade 中的配置也比较简单，它的模式是一个主配置文件 `app.properties`，也可以硬编码进行配置。

## 配置文件

```bash
server.port = 9002
app.name = nice
app.dev = true

app.upload_dir = /Users/biezhi/workspace/annal_www
app.site_url = http://127.0.0.1:9000
app.aes_salt = 0123456789abcdef

# email config
mail.smtp.host=smtp.qq.com
mail.user=xxx
mail.pass=xxx
mail.from=Nice
```

这是一个已经上线的应用的简单配置，我们来解释一下常用的几个：

- server.port: web服务器的启动端口，默认为9000
- app.name: 当前应用的别名，在启动时会打印出来
- app.dev: 是否是开发者模式，开发者模式错误信息会直接显示
- mvc.statics: 设置一个目录为静态资源文件目录，存放在`resources`目录之下
- mvc.view.404: 设置当出现404的统一页面
- mvc.view.500: 设置当出现500错误的统一页面
- server.timeout: 设置web服务的session超时时间，默认为15分钟，单位为分钟

## 获取配置

 我们习惯在主配置文件中设置好，比如邮箱配置，在系统启动的时候将它获取到并保存为常量。Blade的约定是将所有读取配置的操作放在基础包下的 `config` 包中，定义一个Java类继承自 `BaseConfig` 接口，在这里可以获取到配置信息。

```java
public class WebContext implements WebContextListener {
	
    @Override
    public void init(BConfig bConfig, ServletContext sec) {
        Config config = bConfig.confog();
	// 这里就可以读取你的自定义配置了
	Constant.MAIL_HOST = config.get("mail.smtp.host");
        Constant.MAIL_USER = config.get("mail.user");
        Constant.MAIL_USERNAME = config.get("mail.from");
        Constant.MAIL_PASS = config.get("mail.pass");
    }
}
```

在这里加载了邮件配置并将它保存在常量中供其他地方使用。

