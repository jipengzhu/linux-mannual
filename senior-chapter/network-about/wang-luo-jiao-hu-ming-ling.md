# nc(ncat)
读取或发送网络数据

```
nc [options] [hostname] [port]
```


## 选项说明
### 协议选项
|选项 | 说明 |
|--- |--- |
|-4 | 指定使用IPv4 |
|-6 | 指定使用IPv6 |
|-U, --unixsock | 使用Unix domain sockets |
|-u, --udp | 使用udp |

### 连接选项
|选项 | 说明 |
|--- |--- |
|-p port, --source-port port | 指定连接时使用的本地端口 |
|-s host, --source host | 指定连接时使用的本地IP |

### 监听选项
|选项 | 说明 |
|--- |--- |
|-l, --listen | 在本地监听连接 |
|-k, --keep-open | 客户端关闭连接时也保持监听 |

### 加密选项
|选项 | 说明 |
|--- |--- |
|--ssl | 使用ssl（连接模式） |
|--ssl-verify | 同时校验服务端（客户端模式）|
|--ssl-cert certfile.pem | 指定ssl证书 |
|--ssl-key keyfile.pem | 指定ssl密钥 |
|--ssl-trustfile | 指定信任证书列表 |

### 代理选项
|选项 | 说明 |
|--- |--- |
|--proxy host[:port] | 指定代理主机和端口 |
|--proxy-type proto | 指定代理协议 |
|--proxy-auth user[:pass] | 指定代理用户名和密码 |

> 更多的选项请参考 `nc` 的 `man` 手册


<br/>

---

# 参考

[nc/netcat命令][1]  

[1]: http://man.linuxde.net/nc_netcat
