<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [第2章 简单的HTTP协议](#%E7%AC%AC2%E7%AB%A0-%E7%AE%80%E5%8D%95%E7%9A%84http%E5%8D%8F%E8%AE%AE)
    - [目录](#%E7%9B%AE%E5%BD%95)
      - [2.1 HTTP协议用于客户端和服务端之间的通信](#21-http%E5%8D%8F%E8%AE%AE%E7%94%A8%E4%BA%8E%E5%AE%A2%E6%88%B7%E7%AB%AF%E5%92%8C%E6%9C%8D%E5%8A%A1%E7%AB%AF%E4%B9%8B%E9%97%B4%E7%9A%84%E9%80%9A%E4%BF%A1)
      - [2.2 通过请求和响应的交换达成通信](#22-%E9%80%9A%E8%BF%87%E8%AF%B7%E6%B1%82%E5%92%8C%E5%93%8D%E5%BA%94%E7%9A%84%E4%BA%A4%E6%8D%A2%E8%BE%BE%E6%88%90%E9%80%9A%E4%BF%A1)
      - [2.3 HTTP是不保存状态的协议](#23-http%E6%98%AF%E4%B8%8D%E4%BF%9D%E5%AD%98%E7%8A%B6%E6%80%81%E7%9A%84%E5%8D%8F%E8%AE%AE)
      - [2.4 请求URI定位资源](#24-%E8%AF%B7%E6%B1%82uri%E5%AE%9A%E4%BD%8D%E8%B5%84%E6%BA%90)
      - [2.5 告知服务器意图的HTTP方法](#25-%E5%91%8A%E7%9F%A5%E6%9C%8D%E5%8A%A1%E5%99%A8%E6%84%8F%E5%9B%BE%E7%9A%84http%E6%96%B9%E6%B3%95)
      - [2.6 使用方法下达命令](#26-%E4%BD%BF%E7%94%A8%E6%96%B9%E6%B3%95%E4%B8%8B%E8%BE%BE%E5%91%BD%E4%BB%A4)
      - [2.7 持久连接节省通信量](#27-%E6%8C%81%E4%B9%85%E8%BF%9E%E6%8E%A5%E8%8A%82%E7%9C%81%E9%80%9A%E4%BF%A1%E9%87%8F)
        - [&ensp;&ensp;2.7.1 持久连接](#enspensp271-%E6%8C%81%E4%B9%85%E8%BF%9E%E6%8E%A5)
        - [&ensp;&ensp;2.7.2 管线化](#enspensp272-%E7%AE%A1%E7%BA%BF%E5%8C%96)
      - [2.8 使用Cookie的状态管理](#28-%E4%BD%BF%E7%94%A8cookie%E7%9A%84%E7%8A%B6%E6%80%81%E7%AE%A1%E7%90%86)
  - [<span id = "anchor21">2.1 HTTP协议用于客户端和服务端之间的通信</span>](#span-id--anchor2121-http%E5%8D%8F%E8%AE%AE%E7%94%A8%E4%BA%8E%E5%AE%A2%E6%88%B7%E7%AB%AF%E5%92%8C%E6%9C%8D%E5%8A%A1%E7%AB%AF%E4%B9%8B%E9%97%B4%E7%9A%84%E9%80%9A%E4%BF%A1span)
  - [<span id = "anchor22">2.2 通过请求和响应的交换达成通信</span>](#span-id--anchor2222-%E9%80%9A%E8%BF%87%E8%AF%B7%E6%B1%82%E5%92%8C%E5%93%8D%E5%BA%94%E7%9A%84%E4%BA%A4%E6%8D%A2%E8%BE%BE%E6%88%90%E9%80%9A%E4%BF%A1span)
  - [<span id = "anchor23">2.3 HTTP是不保存状态的协议</span>](#span-id--anchor2323-http%E6%98%AF%E4%B8%8D%E4%BF%9D%E5%AD%98%E7%8A%B6%E6%80%81%E7%9A%84%E5%8D%8F%E8%AE%AEspan)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## 第2章 简单的HTTP协议

本章将针对 HTTP 协议结构进行讲解，主要使用HTTP/1.1版本。



### <span id = "anchor21">2.1 HTTP协议用于客户端和服务端之间的通信</span>

* HTTP协议用于**客户端和服务端之间的通信**
  * 客户端：请求访问文本或图像资源的一端
  * 服务端：提供资源响应的一端

### <span id = "anchor22">2.2 通过请求和响应的交换达成通信</span>

![](/001-图解HTTP/Pictures/2201.png)

具体示例如下所示：

![](/001-图解HTTP/Pictures/2202.png)

**1、下面是从客户端发送给某个HTTP服务器端的请求报文中的内容**
```text
GET /index.htm HTTP/1.1
Host: hackr.jp
```
* **GET**
  * 表示请求访问服务器的类型，称为**方法（method）**
* **/index.htm**
  * 指明了请求访问的资源对象，也叫做**请求URI（request-URI）**
* **HTTP/1.1**
  * HTTP的版本号，用来提示客户端使用的HTTP协议功能

综合来看，这段请求内容的意思是：请求访问某台HTTP服务器上的/index.htm页面资源

**请求报文的构成**
请求报文是由请求方法、请求URI、协议版本、可选的请求首部字段和内容实体构成的
请求报文的构成如下图所示
![](/001-图解HTTP/Pictures/2203.png)

**2、接收到请求的服务器，会将请求内容的处理结果以响应的形式返回**

**响应报文**
响应报文是由协议报文、状态码、原因短语、可选的响应首部字段以及内容实体构成
响应报文的构成如下图所示

![](/001-图解HTTP/Pictures/2304.png)

* **HTTP/1.1**
  * 服务器对应的HTTP版本
* **200 OK**
  * 请求处理结果的**状态码**（status code）和**原因短语**（reason-phrase）
* **下一行**
  * 创建响应的日期时间，是首部字段内的一个属性
* **下一行**
  * 以一空行分隔，之后的内容称为**资源实体的主体**（entity body）


### <span id = "anchor23">2.3 HTTP是不保存状态的协议</span>
