网址：https://www.w3cschool.cn/pegosu/

#### 目录
##### [1、cookie的起源](#anchor1)
##### [2、cookie是什么](#anchor2)
##### [3、创建cookie](#anchor3)
##### [4、cookie 编码](#anchor4)
##### [5、过期时间选项](#anchor5)


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
