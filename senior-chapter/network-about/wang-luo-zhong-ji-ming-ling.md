# curl
模拟网络请求和传输

```
curl [options] [URL...]
```

|选项 | 说明 |
|--- |--- |
|-#, --progress-bar | 显示一个简单的进度条来代替标准的输出 |
|-0, --http1.0 | 使用 HTTP 1.0 |
|-1, --tlsv1 | 使用 TLS 1.x |
|-2, --sslv2 | 使用 SSL 2 |
|-3, --sslv3 | 使用 SSL 3 |
|-4, --ipv4 | 只解析 ipv4 |
|-6, --ipv6 | 只解析 ipv6 |
|-a, --append | FTP上传文件时使用追加模式 |
|-A, --user-agen | 设置用户代理标识 | 
|-anyauth | 由curl来决定最好的身份验证方式 |
|-b, --cookie &lt; name=data &gt; | 指定Cookie键值或文件（只有name部分）|
|-B, --use-ascii | 使用ASCII编码传输 |
|--basic | 使用 HTTP basic 验证身份 |
|-c, --cookie-jar &lt; file &gt; | 保存返回结果的Cookie | 
|-C, --continue-at &lt; offset &gt; | 指定断点续传位置 |
|--ciphers &lt; list of ciphers &gt; | 指定SSL通信使用的密钥 |
|--compressed | 请求压缩的返回结果并解压 |
|--connect-timeout &lt; seconds &gt; | 指定连接超时，重复指定时最后一个生效 |
|--create-dirs | 保存下载时创建不存在的目录 |
|--crlf | 上传时将 LF（换行） 转换为CRLF（回车换行）|
|-d, --data &lt; data &gt; | HTTP POST 方式指定请求参数，和 `--data-ascii` 一样 |
|-D, --dump-header &lt; file &gt; | 保存返回结果的请求头 |
|--data-ascii &lt; data &gt; | 使用ascii的方式传递请求参数 |
|--data-binary &lt; data &gt;　| 使用二进制的方式传递请求参数 | 
|--data-urlencode | 对请求参数进行url编码 |
|--digest | 使用 HTTP digest 验证身份 |
|-e, --referer URL | 指定请求来源url |
|-E, --cert &lt; certificate[:password] &gt; | 指定SSL证书文件和密钥 |
|--cert-type &lt; type> &gt; | 指定SSL证书文件类型 (DER/PEM/ENG) |
|--cacert &lt; CA certificate &gt; | 指定CA证书 |
|--capath &lt; CA certificate directory &gt; | 指定CA证书目录 |
|-F, --form <name=content> | HTTP FORM 方式指定请求参数，Content-Type multipart/form-data |
|--form-string | 和 `--form`，只是' @ '、' &lt; '、' ;type= ' 会失去特殊的含义 |
|-g, --globoff | 关闭url部分的glob解析 |
|-G, --get | 使得`-d`类参数变为Get请求的参数，重复指定时第一个生效 |
|-H, --header <header> | 指定HTTP头信息 |
|--ignore-content-length | 忽略 `Content-Length` 头信息 |
|-i, --include | 在输出结果中显示头信息 |
|-I, --head | 只请求HTTP头信息 |
|--interface &lt; name &gt; | 指定网络接口 |
|-j, --junk-session-cookies | 从文件读取Cookie时忽略会话Cookie |
|-J, --remote-header-name | 保存下载时使用`Content-Disposition`头来决定文件名 |
|-k, --insecure | 允许不使用证书访问SSL站点 |
|-K, --config <config file> | 指定读取请求参数的配置文件 |
|--keepalive-time <seconds> | 指定发送keepalive的时间间隔 |
|--key &lt; key &gt;| 指定SSL私钥文件 |
|--key-type &lt; key &gt; | 指定SSL私钥文件类型(DER/PEM/ENG) |
|--krb &lt; level &gt; | FTP指定Kerberos认证级别 |
|-l, --list-only | FTP只列出文件和目录 |
|--limit-rate | 限制传输速率 |
|--local-port | 指定请求时本地使用的端口 |
|-m, --max-time &lt; seconds &gt; | 指定整个操作的超时时间 |
|--no-keepalive | 不使用keepalive |
|--noproxy | 指定访问不需要使用代理的主机列表 |
|-o, --output <file> | 将结果保存到指定的文件中 |
|-O, --remote-name | 将结果保存到指定的文件中 |
|--pass | 指定SSL私钥文件的密码 | 
|-anyauth | 在代理中由curl来决定最好的身份验证方式 |
|--basic | 在代理中使用 HTTP basic 验证身份 |
|--digest | 在代理中使用 HTTP digest 验证身份 |
|--raw | 显示返回结果未解码的内容 |
|--socks4 &lt; host[:port] &gt; | 使用socks4代理 |
|--socks5 &lt; host[:port] &gt; | 使用socks5代理 |
|--tcp-nodelay	| 使用TCP_NODELAY选项 |
|--trace &lt; file &gt; | 记录所有的输入输出数据 |
|--trace-ascii &lt; file &gt; | 记录所有的输入输出数据的ASCII部分 |
|--trace-time | 在记录中显示时间 |
|-u, --user &lt; user:password &gt; | 指定认证使用的用户名和密码 |
|-U, --proxy-user &lt; user:password &gt; | 指定代理使用的用户名和密码 |
|-w, --write-out &lt; format &gt; | 指定输出格式 |
|-X, --request &lt; command &gt; | 指定请求方法类型 |



# nc
读取或发送网络数据

```
nc [options] [hostname] [port]
```


# route
查看网络的路由信息
```
route [-CFvnNee] [-A family |-4|-6]

       route  [-v] [-A family |-4|-6] add [-net|-host] target [netmask Nm] [gw Gw] [metric N] [mss M] [window W]
              [irtt I] [reject] [mod] [dyn] [reinstate] [[dev] If]

       route  [-v] [-A family |-4|-6] del [-net|-host] target [gw Gw] [netmask Nm] [metric N] [[dev] If]

       route  [-V] [--version] [-h] [--help]
```