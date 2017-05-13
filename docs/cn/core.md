---
layout: default_cn
title: 核心概念
isDoc: true
docPage: core
displayName: core
icon: home
---


# IOC

## 什么是IOC？(大神可直接跳最下面)

IoC(Inversion of Control)，意为控制反转，不是什么技术，而是一种设计思想。Ioc意味着**将你设计好的对象交给容器控制，而不是传统的在你的对象内部直接控制**。

如何理解好Ioc呢？理解好Ioc的关键是要明确“谁控制谁，控制什么，为何是反转（有反转就应该有正转了），哪些方面反转了”，那我们来深入分析一下：

- **谁控制谁，控制什么**：传统Java SE程序设计，我们直接在对象内部通过new进行创建对象，是程序主动去创建依赖对象；而IoC是有专门一个容器来创建这些对象，即由Ioc容器来控制对 象的创建；谁控制谁？当然是IoC 容器控制了对象；控制什么？那就是主要控制了外部资源获取（不只是对象包括比如文件等）。

- **为何是反转，哪些方面反转了**：有反转就有正转，传统应用程序是由我们自己在对象中主动控制去直接获取依赖对象，也就是正转；而反转则是由容器来帮忙创建及注入依赖对象；为何是反转？因为由容器帮我们查找及注入依赖对象，对象只是被动的接受依赖对象，所以是反转；哪些方面反转了？依赖对象的获取被反转了。

下面举个例子说明说明是IOC：

假设我们要设计一个Girl和一个Boy类，其中Girl有kiss方法，即Girl想要Kiss一个Boy。那么，我们的问题是，Girl如何能够认识这个Boy？

在我们中国，常见的ＭＭ与GG的认识方式有以下几种:


1. 青梅竹马
2. 亲友介绍
3. 父母包办

那么哪一种才是最好呢？ 
　　
1. **青梅竹马：Girl从小就知道自己的Boy。**

```java
public class Girl {　
    void kiss(){ 
　　　 Boy boy = new Boy(); 
　　} 
} 
```

然而从开始就创建的Boy缺点就是无法在更换。并且要负责Boy的整个生命周期。如果我们的Girl想要换一个怎么办？（笔者严重不支持Girl经常更换Boy）

2. **亲友介绍：由中间人负责提供Boy来见面**

```java
public class Girl { 
　 void kiss(){ 
　　　 Boy boy = BoyFactory.createBoy();　　　
　 } 
}
```

亲友介绍，固然是好。如果不满意，尽管另外换一个好了。但是，亲友BoyFactory经常是以Singleton的形式出现，不然就是，存在于Globals，无处不在，无处不能。实在是太繁琐了一点，不够灵活。我为什么一定要这个亲友掺和进来呢？为什么一定要付给她介绍费呢？万一最好的朋友爱上了我的男朋友呢？ 

3. **父母包办：一切交给父母，自己不用费吹灰之力，只需要等着Kiss就好了。**

```java
public class Girl { 
　  void kiss(Boy boy){ 
　　　 // kiss boy　
　　　boy.kiss(); 
　　} 
}
```

Well，这是对Girl最好的方法，只要想办法贿赂了Girl的父母，并把Boy交给他。那么我们就可以轻松的和Girl来Kiss了。看来几千年传统的父母之命还真是有用哦。至少Boy和Girl不用自己瞎忙乎了。 

这就是IOC，将对象的创建和获取提取到外部。由外部容器提供需要的组件。 

## IoC能做什么

IoC 不是一种技术，只是一种思想，一个重要的面向对象编程的法则，它能指导我们如何设计出松耦合、更优良的程序。传统应用程序都是由我们在类内部主动创建依赖对象，从而导致类与类之间高耦合，难于测试；有了IoC容器后，把创建和查找依赖对象的控制权交给了容器，由容器进行注入组合对象，所以对象与对象之间是 松散耦合，这样也方便测试，利于功能复用，更重要的是使得程序的整个体系结构变得非常灵活。

其实IoC对编程带来的最大改变不是从代码上，而是从思想上，发生了“主从换位”的变化。应用程序原本是老大，要获取什么资源都是主动出击，但是在IoC/DI思想中，应用程序就变成被动的了，被动的等待IoC容器来创建并注入它所需要的资源了。

IoC很好的体现了面向对象设计法则之一—— 好莱坞法则：“别找我们，我们找你”；即由IoC容器帮对象找相应的依赖对象并注入，而不是由对象主动去找。

## IoC和DI

DI—Dependency Injection，即“依赖注入”：组件之间依赖关系由容器在运行期决定，形象的说，即由容器动态的将某个依赖关系注入到组件之中。依赖注入的目的并非为软件系统带来更多功能，而是为了提升组件重用的频率，并为系统搭建一个灵活、可扩展的平台。通过依赖注入机制，我们只需要通过简单的配置，而无需任何代码就可指定目标需要的资源，完成自身的业务逻辑，而不需要关心具体的资源来自何处，由谁实现。

理解DI的关键是：“谁依赖谁，为什么需要依赖，谁注入谁，注入了什么”，那我们来深入分析一下：

- 谁依赖于谁：当然是应用程序依赖于IoC容器；

- 为什么需要依赖：应用程序需要IoC容器来提供对象需要的外部资源；

- 谁注入谁：很明显是IoC容器注入应用程序某个对象，应用程序依赖的对象；

- 注入了什么：就是注入某个对象所需要的外部资源（包括对象、资源、常量数据）。

IoC和DI由什么关系呢？其实它们是同一个概念的不同角度描述，由于控制反转概念比较含糊（可能只是理解为容器控制对象这一个层面，很难让人想到谁来维护对象关系），所以2004年大师级人物Martin Fowler又给出了一个新的名字：“依赖注入”，相对IoC 而言，“依赖注入”明确描述了“被注入对象依赖IoC容器配置依赖对象”。

对于Spring Ioc这个核心概念，我相信每一个学习Spring的人都会有自己的理解。这种概念上的理解没有绝对的标准答案，仁者见仁智者见智。
理解了IoC和DI的概念后，一切都将变得简单明了，剩下的工作只是在框架中堆积木而已，下一节来看看Spring是怎么用的

## Blade的IOC

上面BB了那么多就是给大家回顾一下ioc的概念和优势，Blade设计者认为不该让开发者还去管理诸多的对象，这样显得凌乱而且不好控制，我们将ioc的功能加入到框架内部，使用起来非常简单，这个IOC也没那么多功能。

Blade 将对象分为 `控制器` `配置` `服务` `组件`,使用形式是用注解的方式。

### 操作IOC容器

我们将整个web应用的ioc容器绑定在blade对象上

```java
Ioc ioc = Blade.$().ioc();

// 添加一个对象到容器中
User jobs = new User("jobs", 23);
ioc.addBean(jobs);

// 获取一个对象
User jb = ioc.getBean(jb);
```

有时候我们会用到对象依赖以及注册，比如下面

```java
@Service
public class UserService{
	
	@Inject
	private MailService mailService;

}
```

正因为我们的对象被容器所托管，才使得在使用的时候不必关心对象的创建，这个例子使用
`@Service`注解告诉容器这是一个服务(服务即组件的一种,所有组件被容器管理)，
使用 `Inject` 注解将 `MailService` 注入到 `UserService`，想必你也猜到了这里的
`MailService` 一定是被托管在容器中的。

在 Blade 中没有对IOC的复杂操作，所以只要理解如何使用就可以了，在后续的章节会讲到配置，
我们将清楚什么样的包/类会被托管到ioc中，如果你再深入点儿研究ioc，可以参考我写过的[文章](https://github.com/biezhi/java-bible/blob/master/ioc/index.md)。


# 路由

讲到路由就有同学问了，路由是个什么东西？哦我不是说脏话，这是疑问句。。

现代 Web 应用的 URL 十分优雅，易于人们辨识记忆。
在 Blade 中, 路由是一个 HTTP 方法配对一个 URL 匹配模型， 每一个路由可以对应一个处理方法。

如何管理呢？Blade 从以下三个方面对资源进行定义：

1. 直观简短的资源地址：URI，比如：http://example.com/resources。
2. 可传输的资源：Web 服务接受与返回的互联网媒体类型，比如：JSON，XML 等。
3. 对资源的操作：Web 服务在该资源上所支持的一系列请求方法（比如：POST，GET，PUT或DELETE）。


前面我们写过下面这个入门示例：

```java
$().get("/", new RouteHandler() {
	public void handle(Request request, Response response) {
		response.html("<h1>Hello Blade</h1>");
	}
}).start(Application.class);
```

下面用一张图来分析

![](https://ooo.0o0.ooo/2016/09/07/57cfe3025dce4.png)

执行main函数之后，因为Blade使用了内嵌Jetty作为web服务器，此时会根据jetty服务来初始化核心调度 `DispatcherServlet` 类，
这里会对配置文件，ioc，路由进行初始化，我们使用了匿名类的方式实现了路由，当执行这个请求的时候会像handle方法注入Request对象
和Response对象，你在方法体内可以进行一些操作，然后使用response对象将内容渲染到浏览器。

下面来讲解Blade中的N种路由的创建方式和我们推荐的使用方式：

## 使用Blade核心类创建

### 回调式路由

我们在第一个Hello Blade的程序中使用的就是回调式路由，他是实现一个 `RouteHandle` 接口的匿名类来注册一个路由。

他的写法是这样的：

```java
$().get("/get", new RouteHandler() {
	@Override
	public void handle(Request request, Response response) {
		System.out.println("come get!!!");
		System.out.println("name = " + request.query("name"));
		request.attribute("base", request.contextPath());
		response.render("get.jsp");
	}
});
```

这种方式如果你使用java8那么写起来就很优雅，但缺陷是只能在方法内部进行注册，匿名类中的外部调用必须是常量。

### 函数式路由

```java
$().route("/hello", NormalController.class, "hello");
$().route("/save_user", NormalController.class, "post:saveUser");
$().route("/delete_user", NormalController.class, "deleteUser", HttpMethod.DELETE);
```

`NormalController` 类如下：

```java
public class NormalController {
	
	private static final Logger LOGGER = LoggerFactory.getLogger(NormalController.class);
	
	public void hello(Response response, Request request){
		LOGGER.info("进入hello~");
		request.attribute("name", "rose baby");
		response.text("hi");
	}
	
	public void saveUser(Request request, Response response){
		System.out.println("进入saveUser~");
		
		// test request.model()
		Person person = request.model("person", Person.class);
		System.out.println(person);
		
		// save操作
		JSONObject res = new JSONObject();
		res.put("status", 200);
		response.json(res);
	}
	
	public void deleteUser(Request request, Response response){
		System.out.println("进入deleteUser~");
		// delete操作
		JSONObject res = new JSONObject();
		res.put("status", 200);
		response.json(res);
	}

}
```

这种方式使用起来非常灵活，提供了一个让普通类就可以实现注册路由的功能。

`$().route("/hello", NormalController.class, "hello");`

我们传入的是 **请求地址** / 映射的类Class / 对应的类中方法名。
如果是指定Http请求可以使用 `post:hello` 或者多传递一个 `HttpMethod.POST`的方式进行注册。

上面这种路由方式是我在go语言的mvc框架中发现的，我个人不是很习惯这种方式。

## 使用配置文件创建

当路由比较多的时候我们可以将请求地址写在一个配置文件中进行统一注册

_配置文件格式_

```bash
GET     /                   IndexRoute.home
GET     /signin             IndexRoute.show_signin
POST    /signin             IndexRoute.signin
GET     /signout            IndexRoute.signout
POST    /upload_img         UploadRoute.upload_img
```

那对应的 `IndexRoute` 的写法如同 **函数式路由**

## 使用注解创建

```java
/**
 * web开发推荐的方式
 */
@Controller
public class AController {
	
	private static final Logger LOGGER = LoggerFactory.getLogger(AController.class);
	
	@Inject
	UserService userService;
	
	@Route(value = "post", method = HttpMethod.POST)
	public void post() {
		LOGGER.info("request POST");
	}
	
	@Route("users/:name")
	public String users(Request request, @PathVariable String name) {
		LOGGER.info("request users");
		LOGGER.info("param name = {}", name);
		request.attribute("name", name);
		return "users";
	}
	
	@Route({"/", "index"})
	public ModelAndView index(ModelAndView mav, @RequestParam int age) {
		LOGGER.info("request query age = {}", age);
		userService.sayHello();
		mav.add("name", "jack");
		mav.setView("index");
		return mav;
	}

}
```

看到如上代码你可能觉得比较熟悉，因为我们习惯了springmvc，
所以上面的写法你操作起来就更亲切，作者最推荐的是这种方式注册路由，并不是因为这种方式在性能上有多么好，原因有这几点：

1. 我们习惯了springmvc
2. 控制器是被IOC容器托管的，控制器就可以注入其他的bean
3. 在方法上使用注册以及自动注入更加强大


**@Controller是什么？**

+ `Controller`用来标识这个类是一个控制器，里面存储的都是路由
+ 可以在控制器上配置访问前缀和后缀，便于统一请求
    
**@Route是什么？**

+ `Route`是一个路由的最小单元，用于方法上
+ `Route`的参数有`value`，`method`
+ `value`用于配置路由的URL，也就是http请求的路径
+ 一般不以`/`开头，因为`@Path`上会指定的，写法如下：
    * /hello
    * /user/hello
    * /user/:uid
    * /user/:uid/post

+ Rest风格的路由配置，一定适合你的口味！


**你不知道一个 HTTP 方法是什么？不必担心，这里会简要介绍 HTTP 方法和它们为什么重要：**

_GET_

浏览器告知服务器：只 获取 页面上的信息并发给我。这是最常用的方法。

_HEAD_

浏览器告诉服务器：欲获取信息，但是只关心 消息头 。应用应像处理 GET 请求一样来处理它，但是不分发实际内容。在 Flask 中你完全无需 人工 干预，底层的 Werkzeug 库已经替你打点好了。

_POST_

浏览器告诉服务器：想在 URL 上 发布 新信息。并且，服务器必须确保 数据已存储且仅存储一次。这是 HTML 表单通常发送数据到服务器的方法。

_PUT_

类似 POST 但是服务器可能触发了存储过程多次，多次覆盖掉旧值。你可 能会问这有什么用，当然这是有原因的。考虑到传输中连接可能会丢失，在 这种 情况下浏览器和服务器之间的系统可能安全地第二次接收请求，而 不破坏其它东西。因为 POST 它只触发一次，所以用 POST 是不可能的。

_DELETE_

删除给定位置的信息。


#### 几点说明：

- 路由匹配的顺序是按照他们被定义的顺序执行的，
- 但是，匹配范围较小的路由优先级比匹配范围大的优先级高（详见 **匹配优先级**）。
- 最先被定义的路由将会首先被用户请求匹配并调用。


# 拦截器

## 什么是拦截器

拦截器在概念上和servlet过滤器或JDKs代理类一样。拦截器允许横切功能在动作和框架中单独实现。你可以使用拦截器实现下面的内容：

- 在动作被调用之前提供预处理逻辑
- 在动作被调用之后提供预处理逻辑
- 捕获异常，以便可以执行交替处理

Blade 中的拦截器是在一个请求执行前，后可以做一些自定义的处理，比如存储数据，校验数据，过滤请求等。

## 实现原理

Blade 中实现拦截器的方式非常简单，应用启动的时候框架会加载用户定义好的拦截器组件到IOC容器中，当处理一个路由的请求前后去检查在此之前和之后注册的拦截器组件，找到匹配的拦截器执行。

## 如何使用？

拦截器的使用方式也分多种，我们推荐按照blade的约定来写一个web程序，在你项目的基础包下面建立一个名为 `interceptor` 的包，我们将拦截器组件存放在这里，这里给出一个拦截器组件的示例。

```java
@Intercept
public class BaseInterceptor implements Interceptor {
	
	private static final Logger LOGGE = LoggerFactory.getLogger(BaseInterceptor.class);
	
	@Override
	public boolean before(Request request, Response response) {
		LOGGE.info("request user-agent：" + request.userAgent());
		return true;
	}
	
	@Override
	public boolean after(Request request, Response response) {
		return true;
	}
	
}
```

这个拦截器非常的简单，在每次请求之前输出一下当前请求的 `user-agent` 请求头信息。

### 具体步骤

1. 编写一个java类，实现`Interceptor`接口的`before`,`after`方法
2. 在该类添加注解`@Intercept`，用于配置拦截表达式。默认拦截所有请求
3. 拦截器的方法返回true表示允许本次请求，反之禁止继续请求

# 请求对象

在 Blade 中的核心对象 `Request` 和 `Response`，本次讲解 `Request`，它是对 `HttpServletRequest` 的一次包装，尽管 `HttpServletRequest` 已经够我们用，但不够优雅，在我的开发过程中发现还有一些总是写在 `BaseAction` 里的方法都可以在这里直接作为 `API`。

## 常用功能

### 获取URL/表单的数据

```java
String q1 = request.query("q1");
String q2 = request.query("q2", "hello");
int q3 = request.queryInt("page", 1);
```

这里第二个参数是当 `q2` 没有值的时候默认值是 `hello`

### 获取PATH/路径上的数据

比如定义了一个路由URL为：`/users/:uid` 我们需要获取 `uid`

```java
int uid = request.pathInt("uid");
```

### 获取上传文件信息

```java
FileItem fileItem = request.fileItem("upload_img");
File file = fileItem.file();
String fileName = fileItem.fileName();
```

获取在 `form` 表单中定义了 `input` 类型为 file 且 name 为`upload_img`
的文件，我们将它封装为 `FileItem` 对象，在这里可以通过相关方法获取到文件和文件名以及文件大小等相关信息。

**获取所有文件**

```java
FileItem[] fileItems = request.fileItems();
```

### 获取头信息/Header

```java
String userAgent = request.header("user-agent");
```

### 获取Cookie数据

```java
String sid = request.cookie("sid");
```

### 存储数据到Request Attribute

```java
request.attribute("name", "jack");
```

### 读取Session数据

```java
Session session = request.session();
User user = session.attribute("login_user");
```

### 读取Request Body

```java
BodyParser body = request.body();
String strBody = body.asString();
```

## 其他

### 获取原生 `HttpServletRequest` 对象

```java
HttpServletRequest r = request.raw();
```

### 根据form表单name前缀将请求封装为Java类

```java
User user = request.model("u", User.class);
```

此时你的form表单形如下面：
 
```html
<form method="post" action="/users/save">
	<input type="text" name="u.username" />
	<input type="text" name="u.age" />
	<input type="email" name="u.email" />
	<button type="submit">提交</button>
</form>
```

### 获取当前请求的的路由对象

```java
Route route = request.route();
```


# 响应对象

响应对象也是一个Web框架的核心对象，这里我们来看下Blade中的响应对象该怎么用。

## 常用功能

### 设置Cookie

```java
response.cookie(path, cookieName, value);
```

更详细的 API 可以查看 `/apidocs/index.html`

### JSON格式输出到客户端

```java
String json = "{\"name":\"jack", \"age": 18}";
response.json(json);
```

```java
User user = new User();
user.setAge(21);
user.setUsername("jack w");
response.json(user);
```

### 重定向到其他页面

**重定向到本站其他位置**

```java
response.go("/login");
```

**重定向到其他网站**

```java
response.redirect("https://github.com");
```

### 输出HTML

```java
String html = "<h1>Hello Blade!</h1>";
response.html(html);
```

### 设置头信息

```java
response.header("server", "nginxxxx");
```

## 其他

### 获取原生 `HttpServletResponse` 对象

```java
HttpServletResponse r = response.raw();
```

