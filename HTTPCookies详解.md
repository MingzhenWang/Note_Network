<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [<span id="anchor1">1、cookie的起源</span>](#span-idanchor11cookie%E7%9A%84%E8%B5%B7%E6%BA%90span)
  - [cookie的诞生](#cookie%E7%9A%84%E8%AF%9E%E7%94%9F)
- [<span id="anchor2">2、cookie是什么</span>](#span-idanchor22cookie%E6%98%AF%E4%BB%80%E4%B9%88span)
- [<span id="anchor3">3、创建cookie</span>](#span-idanchor33%E5%88%9B%E5%BB%BAcookiespan)
  - [HTTP请求发送Cookies的条件：](#http%E8%AF%B7%E6%B1%82%E5%8F%91%E9%80%81cookies%E7%9A%84%E6%9D%A1%E4%BB%B6)
  - [示例](#%E7%A4%BA%E4%BE%8B)
    - [服务器端发送`Set-Cookie`到浏览器端（response）](#%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%AB%AF%E5%8F%91%E9%80%81set-cookie%E5%88%B0%E6%B5%8F%E8%A7%88%E5%99%A8%E7%AB%AFresponse)
    - [浏览器端发送`cookie`到服务器端（request）](#%E6%B5%8F%E8%A7%88%E5%99%A8%E7%AB%AF%E5%8F%91%E9%80%81cookie%E5%88%B0%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%AB%AFrequest)
- [<span id="anchor4">4、cookie 编码</span>](#span-idanchor44cookie-%E7%BC%96%E7%A0%81span)
- [<span id="anchor5">5、cookie可选项</span>](#span-idanchor55cookie%E5%8F%AF%E9%80%89%E9%A1%B9span)
  - [<span id="anchor51">5.1 过期时间选项（expires）</span>](#span-idanchor5151-%E8%BF%87%E6%9C%9F%E6%97%B6%E9%97%B4%E9%80%89%E9%A1%B9expiresspan)
  - [<span id="anchor52">5.2 domain 选项</span>](#span-idanchor5252-domain-%E9%80%89%E9%A1%B9span)
  - [<span id="anchor53">5.3 path选项</span>](#span-idanchor5353-path%E9%80%89%E9%A1%B9span)
  - [<span id="anchor54">5.4 secure选项</span>](#span-idanchor5454-secure%E9%80%89%E9%A1%B9span)
- [<span id="anchor6">6、Cookie 的维护和生命周期</span>](#span-idanchor66cookie-%E7%9A%84%E7%BB%B4%E6%8A%A4%E5%92%8C%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9Fspan)
- [<span id="anchor7">7、使用失效日期</span>](#span-idanchor77%E4%BD%BF%E7%94%A8%E5%A4%B1%E6%95%88%E6%97%A5%E6%9C%9Fspan)
- [<span id="anchor8">8、cookie自动删除</span>](#span-idanchor88cookie%E8%87%AA%E5%8A%A8%E5%88%A0%E9%99%A4span)
- [<span id="anchor9">9、cookie限制条件</span>](#span-idanchor99cookie%E9%99%90%E5%88%B6%E6%9D%A1%E4%BB%B6span)
- [<span id="anchor10">10、Subcookies</span>](#span-idanchor1010subcookiesspan)
- [<span id="anchor11">11、JavaScript 中的 cookie</span>](#span-idanchor1111javascript-%E4%B8%AD%E7%9A%84-cookiespan)
- [<span id="anchor12">12、HTTP-Only cookies</span>](#span-idanchor1212http-only-cookiesspan)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

网址：https://www.w3cschool.cn/pegosu/




### <span id="anchor1">1、cookie的起源</span>
早期Web应用的最大问题之一：**如何维持状态**，服务器无法判断两次请求是否来自同一浏览器
#### cookie的诞生
* 1994年，网景通信公司的一名员工将**magic cookies**的概念应用到Web通讯中，他试图解决Web的第一个购物车应用
* 他的原始文档提供了cookie的基本工作原理，被收纳到**RFC 2109**（大多数浏览器的实现参考文档），最终被收纳到**RFC 2965**中
* 网景浏览器在第一个版本中开始支持cookie，现在所有的web浏览器都支持cookie

### <span id="anchor2">2、cookie是什么</span>
* cookie是浏览器存储在用户电脑上的一小段纯文本文件，不包含任何可执行代码
* 一个Web页面或者服务器**告知浏览器按照一定规范**来存储这些信息，并在随后的请求中将这些信息发送至服务器，Web服务器可以使用这些信息来识别不同的用户
* 大多数需要登陆的网址在**用户验证成功后都会设置一个cookie**，只要这个cookie存在并可以，用户就可以浏览这个网站的任意界面

### <span id="anchor3">3、创建cookie</span>
Web服务器通过发送一个称为`Set-Cookie`的HTTP消息头来创建一个cookie，`Set-Cookie`消息头是一个字符串，格式如下（中括号的部分是可选的）
```shell
Set-Cookie: value[; expire=date][; domain=domain][; path=path][; secure]
```
* 消息头的第一部分，value，通常是一个`name=value`格式的字符串
* 这种格式是原始规范中指定的格式，浏览器不会对cookie值按照此格式来验证
* 这种格式最常用，大多数接口只支持该格式
* 通过 Set-Cookie 指定的可选项只会在浏览器端使用，不会被发送至服务器端。
* 发送至服务器的cookie值与通过`Set-Cookie`指定的值完全一样，不会有进一步的解析或转码操作。如果请求中包含多个 cookie，它们将会被分号和空格分开，例如：
```shell
Cookie: value1; value2; name1=value1
```
* 服务器端框架通常包含解析 cookie 的方法，通过编程的方式获取cookie的值。
#### HTTP请求发送Cookies的条件：
* 本地已经缓存有cookies
* 根据请求的URL来匹配cookies的domain、path属性，如果都符合才会发送。
  * 举个例子：访问www.baidu.com时，就不发送www.qq.com的cookies

#### 示例
##### 服务器端发送`Set-Cookie`到浏览器端（response）
```shell
Response sent 52 bytes of Cookie data:
	Set-Cookie: GSPStateCount=1; path=/cwbase/web/session/; HttpOnly
Response sent 1315 bytes of Cookie data:
	Set-Cookie: GSPState0=U3lzT3JnQ29kZTowMSZBdXRoVG9rZW46c3JhUXBUenNzL1owTndvRllyY2llYW9QQm8rVzlhTzVjbkdnbGRYMWF0dWF5NW5EczJ6a3dpYlZ5TGFIVE9XVnpIcWI3V25DMVc0ZGhkZEZjNGpRbjgxcXNXU0JISTJvUTBucU0vNUk2TzhtMTFBeWplWE9idXhaandUOXNzTjBTaVh3RG5TeGxIUmNRVlM2UHI2bjI4QXNSY2N1TVp5bCZDbGllbnRJUDoxMC03Mi0xMzUtOTMmVXNlcklEOjJiNGQ3ODJiLTNhMmUtNDA4Yy1hNGRkLWUwMjY2ZWIyMDMzMSZVc2VyU2VjTGV2ZWxDb2RlOkNPTkZJREVOVElBTCZVc2VyU2VjTGV2ZWxJRDpDT05GSURFTlRJQUwmU2Vzc2lvbklkOmNiZTkyMGQ3LWQ3N2EtNDY1MS05ZWY3LWQ3NWMwZTUyMjNhOSZBcHBJbnN0YW5jZU5hbWU6TTg3MSZNYWluREJDb2RlOk04NzEmU3lzT3JnTmFtZTrljY7kuLDpm4blm6ImQ3VycmVudEFwcElEOkdTUCZVc2VyQXNzT2JqZWN0OjAmVXNlckNvZGU6d2FuZ21pbmd6aGVuJkNvZGU6R1NQJlVzZXJFbWFpbDomVXNlck5hbWU6546L5piO5oyvJlByb2Nlc3NJRDphMTlkNzM5Mi0xZjIyLTRlZDctOGM0NC1jMWViMWQ0YzU2NDkmVXNlclNlY0xldmVsTmFtZTrmnLrlr4YmSUQ6NzRmM2E0MTQtZDUzNy00YjFiLWEzOTUtNWIyYzg4ZmUyZjA4JkJpekRhdGU6MjAyMC0wOS0yNFQwMDowMDowMCswODowMCZGcmFtZVR5cGU6NSZDbGllbnRUb2tlbjoxMC03Mi0xMzUtOTMmTG9naW5EYXRlOjIwMjAtMDktMjRUMDg6MzM6MjErMDg6MDAmRnVuY0lEOiZIb3N0TmFtZTomVXNlclNlY0xldmVsOjMmU3lzT3JnSUQ6M2IyNTcxNzEtZDVkZi00MWU2LTk3MGMtNDRjZjgwZDFlNTY2Jkxhbmd1YWdlOnpoLUNOJkN1cnJlbnREYXRlOjIwMjAtMDktMjRUMDg6MzM6MjErMDg6MDAmQ3VycmVudERiVHlwZTpTUUxTZXJ2ZXImVmVyc2lvbjoyMmY1ZTE0Yy04ZTIwLTQyODAtYWRmZS0zNzY2YWU4MjE3ZmQmQXBwSW5zdGFuY2VJRDpNODcxJg==; path=/cwbase/web/session/; HttpOnly
Response sent 36 bytes of Cookie data:
	Set-Cookie: GSPWebThemeKey=gsp2019; path=/cwbase
```
##### 浏览器端发送`cookie`到服务器端（request）
```shell
Cookie: GSPStateCount=1; GSPState0=U3lzT3JnQ29kZTowMSZBdXRoVG9rZW46c3JhUXBUenNzL1owTndvRllyY2llYW9QQm8rVzlhTzVjbkdnbGRYMWF0dWF5NW5EczJ6a3dpYlZ5TGFIVE9XVnpIcWI3V25DMVc0ZGhkZEZjNGpRbjgxcXNXU0JISTJvUTBucU0vNUk2TzhtMTFBeWplWE9idXhaandUOXNzTjBTaVh3RG5TeGxIUmNRVlM2UHI2bjI4QXNSY2N1TVp5bCZDbGllbnRJUDoxMC03Mi0xMzUtOTMmVXNlcklEOjJiNGQ3ODJiLTNhMmUtNDA4Yy1hNGRkLWUwMjY2ZWIyMDMzMSZVc2VyU2VjTGV2ZWxDb2RlOkNPTkZJREVOVElBTCZVc2VyU2VjTGV2ZWxJRDpDT05GSURFTlRJQUwmU2Vzc2lvbklkOmNiZTkyMGQ3LWQ3N2EtNDY1MS05ZWY3LWQ3NWMwZTUyMjNhOSZBcHBJbnN0YW5jZU5hbWU6TTg3MSZNYWluREJDb2RlOk04NzEmU3lzT3JnTmFtZTrljY7kuLDpm4blm6ImQ3VycmVudEFwcElEOkdTUCZVc2VyQXNzT2JqZWN0OjAmVXNlckNvZGU6d2FuZ21pbmd6aGVuJkNvZGU6R1NQJlVzZXJFbWFpbDomVXNlck5hbWU6546L5piO5oyvJlByb2Nlc3NJRDphMTlkNzM5Mi0xZjIyLTRlZDctOGM0NC1jMWViMWQ0YzU2NDkmVXNlclNlY0xldmVsTmFtZTrmnLrlr4YmSUQ6NzRmM2E0MTQtZDUzNy00YjFiLWEzOTUtNWIyYzg4ZmUyZjA4JkJpekRhdGU6MjAyMC0wOS0yNFQwMDowMDowMCswODowMCZGcmFtZVR5cGU6NSZDbGllbnRUb2tlbjoxMC03Mi0xMzUtOTMmTG9naW5EYXRlOjIwMjAtMDktMjRUMDg6MzM6MjErMDg6MDAmRnVuY0lEOiZIb3N0TmFtZTomVXNlclNlY0xldmVsOjMmU3lzT3JnSUQ6M2IyNTcxNzEtZDVkZi00MWU2LTk3MGMtNDRjZjgwZDFlNTY2Jkxhbmd1YWdlOnpoLUNOJkN1cnJlbnREYXRlOjIwMjAtMDktMjRUMDg6MzM6MjErMDg6MDAmQ3VycmVudERiVHlwZTpTUUxTZXJ2ZXImVmVyc2lvbjoyMmY1ZTE0Yy04ZTIwLTQyODAtYWRmZS0zNzY2YWU4MjE3ZmQmQXBwSW5zdGFuY2VJRDpNODcxJg==; GSPWebLanguageKey=zh-CN; GSPWebThemeKey=gsp2019
```

### <span id="anchor4">4、cookie 编码</span>
* 普遍认为cookie的值必须经过URL编码，但实际是一个谬论
* 原始规范中明确指出，只有3个字符必须进行编码：**分号、逗号和空格**
* 实际上，几乎所有实现都对cookie的值进行了一系列的URL编码。
  * 对应`name=value`格式，通常会对`name`和`value`的值进行编码，不处理等号=

### <span id="anchor5">5、cookie可选项</span>

紧跟 cookie 值后面的每个选项**都以分号和空格**分开，每个选择都指定了 cookie 在什么情况下应该被发送至服务器。

#### <span id="anchor51">5.1 过期时间选项（expires）</span>
* 指定了 cookie 何时不会再被发送至服务器，随后浏览器将删除该 cookie。
* 该选项的值是一个 Wdy, DD-Mon-YYYY HH:MM:SS GMT 日期格式的值，例如：
```shell
Set-Cookie: name=Nicholas; expires=Sat, 02 May 2009 23:38:25 GMT
```
* 没有设置 expires 选项时，cookie 的生命周期仅限于当前会话中，关闭浏览器会结束此次会话，所以会话 cookie 仅存在于浏览器打开状态之下。
* 当登录一个 Web 应用时经常会看到一个复选框，询问你是否记住登录信息：如果你勾选了复选框，那么一个 expires 选项会被附加到登录 cookie 中。
* 如果 expires 设置了一个过去的时间点，那么这个 cookie 会被立即删掉

#### <span id="anchor52">5.2 domain 选项</span>

**指定了cookie将要被发送到哪个或哪些域中**

**默认值**
* domain会被设置为创建该cookie的页面所在域名

**作用**
* domain 选项可用来**扩充cookie可发送域的数量**，例如：
```shell
Set-Cookie: name=Nicholas; domain=nczonline.net
```

**例如**，Yahoo! 会有许多 name.yahoo.com 形式的站点（例如：my.yahoo.com, finance.yahoo.com 等等）。将一个 cookie 的 domain 选项设置为 yahoo.com，就可以将该 cookie 的值发送至所有这些站点。浏览器会把 domain 的值与请求的域名做一个**尾部比较**（即从字符串的尾部开始比较），并将匹配的 cookie 发送至服务器。

* domain 选项的值必须是**发送 Set-Cookie 消息头的主机名的一部分**，例如我不能在 google.com 上设置一个 cookie，因为这会产生安全问题。
* 不合法的 domain 选择将直接被忽略。

#### <span id="anchor53">5.3 path选项</span>

path选项指定了**请求的资源URL中必须存在指定的路径时，才会发送cookie消息头**
**domain 选项核实完毕之后才会对 path 属性进行比较**

通常是将path选项的值与请求的URL**从头开始逐字符比较**完成，如果字符匹配，则发送cookie消息头

例如：
```shell
Set-Cookie: name=Nicholas; path=/blog
```
上述cookie中，path选项值会与 `/bolg`，`/blogrool`等等做匹配；任何以 `/bolg`开头的选项都是合法的

**默认值**
path 属性的默认值是发送 Set-Cookie 消息头所对应的 URL 中的 path 部分。

#### <span id="anchor54">5.4 secure选项</span>
最后一个选项是secure，该选项只是一个标记没有值

* 只有当一个请求通过**SSL**或**HTTPS**创建时，包含secure选项的cookie才能被发送至服务器。
* 这种cookie的内容价值很高，如果以纯文本的形式传递，很容易被篡改
```shell
Set-Cookie: name=Nicholas; secure
```
* 机密信息绝不应该在cookie中存储或传输，因为cookie的整个机制都是不安全的
* 默认情况下，在 **HTTPS** 链接上传输的 cookie 都会被**自动添加上secure**选项

### <span id="anchor6">6、Cookie 的维护和生命周期</span>

* 在一个 cookie 中可以**指定任意数量的选项**，并且这些选项可以是**任意顺序**
* **如何改变一个cookie 的值**
  * 需要发送另一个具有相同 cookie name，domain，path 的 Set-Cookie 消息头
  * 上述操作将覆盖原有cookie的值，但是修改cookie中任意一项都会创建一个新的cookie
* **cookie排序**
  * 按照 domain-path-secure 的顺序，设置越详细的 cookie 在字符串中越靠前

例如，如下3个cookie设置值
```shell
Set-Cookie: name=Greg; domain=nczonline.net; path=/blog
Set-Cookie: name=Nicholas; domain=nczonline.net; path=/
Set-Cookie: name=Mike(在 ww.nczonline.net/blog 下用默认选项创建了另一个 cookie：)
```
如果你访问 www.nczonline.net/blog 下的一个页面，以下的消息头将被包含进来：
```shell
Cookie: name=Mike; name=Greg; name=Nicholas
```

**解释**：以 “Mike” 作为值的 cookie 使用了域名（www.nczonline.net）作为其 domain 值并且以全路径（/blog）作为其 path 值，则它较其它两个 cookie 更加详细。

### <span id="anchor7">7、使用失效日期</span>

* 当创建cookie时指定了失效日期，这个失效日期则关联了以`name-domain-path-secure`为标识的cookie
* 要改变一个 cookie 的失效日期，你必须指定同样的组合（包含expire选项）
* 如果不改变cookie的失效日期，一个会话cookie可以变成一个持久化cookie
* 为了要将一个**持久化 cookie**变为一个**会话 cookie**，你必须删除这个持久化 cookie，这只要设置它的失效日期为过去某个时间之后再创建**一个同名的会话** cookie 就可以实现。

**会话cookie和持久化cookie**
1. 会话cookie
	是一种临时的cookie，它记录了用户访问站点时的设置和偏好，关闭浏览器，会话cookie就被删除了

2. 持久化cookie
   存储在硬盘上，不同的操作系统，不同的浏览器存储的位置不一样，不管浏览器退出，或电脑重启，持久cookie都存在。持久cookie有过期时间。

**注意：**
**失效日期**是以**浏览器运行的电脑上的系统时间**为基准进行核实的。无法验证系统时间是否和服务器的时间同步，所以当服务器时间和浏览器所处系统时间存在差异时这样的设置会出现错误。

### <span id="anchor8">8、cookie自动删除</span>

cookie 会被浏览器自动删除，通常存在以下几种原因：
1. **会话 cookie** (Session cookie) 在会话结束时（浏览器关闭）会被删除
2. 持久化 cookie（Persistent cookie）在到达失效日期时会被删除
3. 浏览器中的 cookie 数量达到限制，那么 cookie 会被删除以为新建的 cookie 创建空间


### <span id="anchor9">9、cookie限制条件</span>
cookie 存在许多限制条件，来阻止 cookie 滥用并保护浏览器和服务器免受一些负面影响
有两种 cookie 限制条件：**cookie 的属性**和 **cookie的总大小**
1. 原始规范中限定每个域名下不超过 20 个 cookie
   1. IE7 中增加 cookie 的限制数量到 50 个
   2. Opera 限定 cookie 数量为 30 个
   3. Safari 和 Chrome 对与每个域名下的 cookie 个数没有限制。
2. 发向服务器的所有 cookie 的最大数量(空间)
   1. 仍旧维持原始规范中所指出的：4KB。所有超出该限制的 cookie 都会被截掉并且不会发送至服务器。


### <span id="anchor10">10、Subcookies</span>

有cookie的数量存在限制，开发者提出subcookies的观点来增加cookie的存储量。

* subcookies是存储在一个cookie值中的一些name-value键值对
  * 格式类似`name=a=b&c=d&e=f&g=h`
* 这种方式允许在单个cookie中保存多个`name=value`对，而不会超出浏览器cookie数量的限制
* 劣势：需要自定义解析方式来提取subcookies的值
### <span id="anchor11">11、JavaScript 中的 cookie</span>

在JavaScript中，可以通过document.cookie属性创建、维护和删除cookie

**创建cookie**
* 创建cookie时，该属性等同于`Set-cookie`消息头，需要使用和`Set-cookie`期望格式相同的字符串
```shell
doument.cookie="name=Nicholas;domain=nczonline.net;path=/";
```

**读取cookie**
* 使用 document.cookie 中读取即可
* 返回的字符串与 Cookie 消息头中的字符串格式相同，所以多个 cookie 会被分号和字符串分割，需要手工解析来读取数据


* 通过访问 document.cookie 返回的 cookie 遵循发向服务器的 cookie 一样的访问规则。要通过 JavaScript 访问 cookie，该页面和 cookie 必须在相同的域中，有相同的 path，有相同的安全级别。

**注意**：一旦 cookie 通过 **JavaScript设置后便不能提取它的选项**，所以你将不能知道 domain，path，expires 日期或 secure 标记。

### <span id="anchor12">12、HTTP-Only cookies</span>

**来源：** 微软的 IE6 SP1 在 cookie 中引入了一个新的选项：HTTP-only
**含义：** 告知浏览器该cookie不能通过document.cookie属性访问
**目的：** 提供一个安全措施，阻止通过JavaScript发起的跨站脚本（XXS）窃取cookie的行为
**支持：**  Firefox2.0.0.5+、Opera9.5+、Chrome 都支持 HTTP-Only cookie，3.2 版本的 Safari 仍不支持
**如何设置HTTP-only属性：**
```shell
Set-Cookie: name=Nicholas; HttpOnly
```
**其他安全问题**
IE 同时更近一步并且不允许通过 XMLHttpRequest 的 getAllResponseHeaders() 或 getResponseHeader() 方法访问 cookie，然而其它浏览器则允许此行为。Firefox 在 3.0.6 中修复了该漏洞。

注意：不能通过JavaScript设置HTTP-only