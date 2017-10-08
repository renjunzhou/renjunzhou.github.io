---
layout: post
title: Web Service
---
## SOAP
> SOAP 是完全透明的，底层的SOAP库在发送端生成SOAP并在接收端解析SOAP，以使两侧的Java代码可以对被发送和被接收的是什么类型的有效载荷保持不可知。

### WSDL 合同详解
- **definitions** *文档(根元素)*
- **types** *类型* 可选元素, 包含一个XML模式或等效的指定服务中包含消息的数据类型的语法
- **messages** *消息*  
- **portType** 只有一个, 本质是服务接口, 服务的操作和操作体现/示范的消息模式的规范
- **binding** *绑定* 1...\*个, 提供了实现的细节(如传输协议), 服务的风格, 以及SOAP的版本
  - transport (http, SMTP...)
  - style (document)
- **service** *服务* 汇集前面所有细节来定义关键属性, 如服务端点(service endpoint), 即可用于访问服务的URL, 嵌套在service元素中的是一个或多个port(portType + binding)子元素

### 实例
handler 访问传入和传出的SOAP消息的Java代码
