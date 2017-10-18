# curl
模拟网络请求和传输

```
curl [options] [URL...]
```


## URL说明
`url` 支持 `glob` 通配符的形式
```
http://site.{one,two,three}.com
ftp://ftp.numericals.com/file[1-100].txt
ftp://ftp.numericals.com/file[001-100].txt
ftp://ftp.letters.com/file[a-z].txt
http://www.numericals.com/file[1-100:10].txt
http://www.letters.com/file[a-z:2].txt
```


## 选项说明
### 普通选项
|选项 | 说明 |
|--- |--- |
|-#, --progress-bar | 显示一个简单的进度条来代替标准的输出 |
|-0, --http1.0 | 使用 HTTP 1.0 |
|-4, --ipv4 | 只解析 ipv4 |
|-6, --ipv6 | 只解析 ipv6 |
|-b, --cookie &lt; name=data &gt; | 指定Cookie键值或文件（只有name部分时）|
|-c, --cookie-jar &lt; file &gt; | 保存返回结果的Cookie到指定的文件 | 
|--compressed | 指定返回结果是解压后的 |
|--connect-timeout &lt; seconds &gt; | 指定连接超时，重复指定时最后一个生效 |
|-D, --dump-header &lt; file &gt; | 保存返回结果的请求头 |
|-i, --include | 在输出结果中显示头信息 |
|-I, --head | 只请求HTTP头信息 |
|--interface &lt; name &gt; | 指定网络接口 |
|-j, --junk-session-cookies | 从文件读取Cookie时忽略会话Cookie |
|--keepalive-time <seconds> | 指定发送keepalive的时间间隔 |
|--limit-rate | 限制传输速率 |
|--local-port | 指定请求时本地使用的端口 |
|-m, --max-time &lt; seconds &gt; | 指定整个操作的超时时间 |
|--no-keepalive | 不使用keepalive |
|--raw | 显示返回结果未解码的内容 |
|--tcp-nodelay	| 使用TCP_NODELAY选项 |
|-w, --write-out &lt; format &gt; | 指定输出格式 |

#### keepalive
详情参考[这里][3]

#### tcp-nodelay
详情参考[这里][4]


### 参数选项
|选项 | 说明 |
|--- |--- |
|-A, --user-agen | 设置用户代理标识 |
|-B, --use-ascii | 使用ASCII编码传输 |
|-d, --data &lt; data &gt; | HTTP POST 方式指定请求参数，和 `--data-ascii` 一样 |
|--data-ascii &lt; data &gt; | 使用ascii的方式传递请求参数 |
|--data-binary &lt; data &gt;　| 使用二进制的方式传递请求参数 | 
|--data-urlencode | 对请求参数进行url编码 |
|-e, --referer URL | 指定请求来源url |
|-F, --form <name=content> | HTTP FORM 方式指定请求参数 |
|--form-string | 和 `--form`，只是' @ '、' &lt; '、' ;type= ' 会失去特殊的含义 |
|-g, --globoff | 关闭url部分的glob解析 |
|-G, --get | 使得`-d`类参数变为Get请求的参数，重复指定时第一个生效 |
|-H, --header <header> | 指定HTTP头信息 |
|--ignore-content-length | 忽略 `Content-Length` 头信息 |
|-K, --config <config file> | 指定读取请求参数的配置文件 |
|-X, --request &lt; command &gt; | 指定请求方法类型 |

#### 用户代理标识
详情参考[这里][5]

#### 浏览器的编码
详情参考[这里][6]

#### http post
1. `-d` 的 `Content-Type` 为 `application/x-www-form-urlencoded`
2. `-F` 的 `Content-Type` 为 `multipart/form-data`
3. `-F` 支持使用分号分割多个参数，值的`@`前缀代表上传文件

> POST提交数据方式请参考[这里][7]

#### http header
详情参考[这里][8]

#### http method

### 加密选项
|选项 | 说明 |
|--- |--- |
|-1, --tlsv1 | 使用 TLS 1 |
|--tlsv1.0 | 使用 TLS 1.0 |
|--tlsv1.1 | 使用 TLS 1.1 |
|--tlsv1.2 | 使用 TLS 1.2 |
|-2, --sslv2 | 使用 SSL 2 |
|-3, --sslv3 | 使用 SSL 3 |
|--ciphers &lt; list of ciphers &gt; | 指定SSL通信使用的密钥 |
|-E, --cert &lt; certificate[:password] &gt; | 指定SSL证书文件和密码 |
|--cert-type &lt; type> &gt; | 指定SSL证书文件类型 (DER/PEM/ENG) |
|--cacert &lt; CA certificate &gt; | 指定CA证书 |
|--capath &lt; CA certificate directory &gt; | 指定CA证书目录 |
|-k, --insecure | 允许不使用证书访问SSL站点 |
|--key &lt; key &gt;| 指定SSL私钥文件 |
|--key-type &lt; key &gt; | 指定SSL私钥文件类型(DER/PEM/ENG) |
|--pass | 指定SSL私钥文件的密码 | 

#### TLS和SSL

### 认证选项 
|选项 | 说明 |
|--- |--- |
|-anyauth | 由curl来决定最好的身份验证方式 |
|--basic | 使用 HTTP basic 验证身份 |
|--digest | 使用 HTTP digest 验证身份 |
|-u, --user &lt; user:password &gt; | 指定认证使用的用户名和密码 |
|--krb &lt; level &gt; | FTP指定Kerberos认证级别 |

#### http认证

#### Kerberos认证

### 代理选项
|选项 | 说明 |
|--- |--- |
|--noproxy | 指定访问不需要使用代理的主机列表 |
|--proxy-anyauth | 在代理中由curl来决定最好的身份验证方式 |
|--proxy-basic | 在代理中使用 HTTP basic 验证身份 |
|--proxy-digest | 在代理中使用 HTTP digest 验证身份 |
|-U, --proxy-user &lt; user:password &gt; | 指定代理使用的用户名和密码 |
|--socks4 &lt; host[:port] &gt; | 使用socks4代理 |
|--socks5 &lt; host[:port] &gt; | 使用socks5代理 |

#### http代理

#### socks代理

### 文件选项
|选项 | 说明 |
|--- |--- |
|-a, --append | (FTP/SFTP)上传文件时使用追加模式 |
|-C, --continue-at &lt; offset &gt; | 指定断点续传位置 |
|--create-dirs | 保存下载时创建不存在的目录 |
|--crlf | 上传时将 LF（换行） 转换为CRLF（回车换行）|
|-J, --remote-header-name | 保存下载时使用`Content-Disposition`头来决定文件名 |
|-o, --output <file> | 将结果保存到指定的文件中 |
|-O, --remote-name | 将结果保存到指定的文件中 |
|-l, --list-only | FTP只列出文件和目录 |

### 调试选项
|选项 | 说明 |
|--- |--- |
|--trace &lt; file &gt; | 记录所有的输入输出数据 |
|--trace-ascii &lt; file &gt; | 记录所有的输入输出数据的ASCII部分 |
|--trace-time | 在记录中显示时间 |


# nc
读取或发送网络数据

```
nc [options] [hostname] [port]
```


# route
查看网络的路由信息
```
route [-CFvnNee] [-A family |-4|-6]

route  [-v] [-A family |-4|-6] add [-net|-host] target [netmask Nm] [gw Gw] [metric N] [mss M] [window W] [irtt I] [reject] [mod] [dyn] [reinstate] [[dev] If]

route  [-v] [-A family |-4|-6] del [-net|-host] target [gw Gw] [netmask Nm] [metric N [[dev] If]

route  [-V] [--version] [-h] [--help]
```



<br/>

---

# 参考

[Linux curl命令详解][1]  
[curl网站开发指南][2]  
[HTTP Keep-Alive是什么？][3]  
[TCP_NODELAY 和 TCP_NOPUSH的解释][4]  
[总结整理时下流行的浏览器User-Agent大全][]  
[说说http协议中的编码和解码][6]  
[四种常见的 POST 提交数据方式][7]  
[HTTP头部详解][8]  
[HTTP的请求方法][]    

[1]: http://www.cnblogs.com/duhuo/p/5695256.html
[2]: http://blog.csdn.net/wishfly/article/details/7004198
[3]: http://www.nowamagic.net/academy/detail/23350305
[4]: http://www.cnblogs.com/wajika/p/6573014.html
[5]: http://luo476979657.iteye.com/blog/2097937
[6]: http://www.cnblogs.com/zhao1949/p/5545064.html
[7]: https://imququ.com/post/four-ways-to-post-data-in-http.html
[8]: http://ynhu33.blog.51cto.com/412835/408801
[]: http://www.cnblogs.com/findumars/p/7086193.html