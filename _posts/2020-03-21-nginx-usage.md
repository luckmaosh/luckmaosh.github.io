# nginx使用

## 匹配规则

```
~  为区分大小写匹配
~* 为不区分大小写匹配
^开头
$结尾
.任意字符
(?!) 忽略大小写
```
 
## 代理
proxy_pass


## 重写
**rewrite**

语法：```rewrite regex replacement [flag];```

flag

- 1.last 相当于apache里面的[L]标记，表示rewrite。
- 2.break本条规则匹配完成后，终止匹配，不再匹配后面的规则。
- 3.redirect 返回302临时重定向，浏览器地址会显示跳转后的URL地址。
- 4.permanent 返回301永久重定向，浏览器地址会显示跳转后的URL地址。

正则表达式

```
6）常用的变量

$args ： #这个变量等于请求行中的参数，同$query_string

$content_length ： 请求头中的Content-length字段。

$content_type ： 请求头中的Content-Type字段。

$document_root ： 当前请求在root指令中指定的值。

$host ： 请求主机头字段，否则为服务器名称。

$http_user_agent ： 客户端agent信息

$http_cookie ： 客户端cookie信息

$limit_rate ： 这个变量可以限制连接速率。

$request_method ： 客户端请求的动作，通常为GET或POST。

$remote_addr ： 客户端的IP地址。

$remote_port ： 客户端的端口。

$remote_user ： 已经经过Auth Basic Module验证的用户名。

$request_filename ： 当前请求的文件路径，由root或alias指令与URI请求生成。

$scheme ： HTTP方法（如http，https）。

$server_protocol ： 请求使用的协议，通常是HTTP/1.0或HTTP/1.1。

$server_addr ： 服务器地址，在完成一次系统调用后可以确定这个值。

$server_name ： 服务器名称。

$server_port ： 请求到达服务器的端口号。

$request_uri ： 包含请求参数的原始URI，不包含主机名，如：”/foo/bar.php?arg=baz”。

$uri ： 不带请求参数的当前URI，$uri不包含主机名，如”/foo/bar.html”。

$document_uri ： 与$uri相同。


使用括号（）标记要截取的内容

7）常用正则：

. ： 匹配除换行符以外的任意字符

? ： 重复0次或1次

+ ： 重复1次或更多次

* ： 重复0次或更多次

\d ：匹配数字

^ ： 匹配字符串的开始

$ ： 匹配字符串的介绍

{n} ： 重复n次

{n,} ： 重复n次或更多次

[c] ： 匹配单个字符c

[a-z] ： 匹配a-z小写字母的任意一个
```

## 根据url转发


