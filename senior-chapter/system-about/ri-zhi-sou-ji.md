# 系统日志
系统日志对于问题追踪和安全防护非常重要，通常在 `/var/log` 目录下面，详情参考参考中的链接



# 日志切割
日志每时每刻都在产生，需要在某个时刻或达到指定大小后进行切割和备份，详情参考参考中的链接



# 日志采集
## 日志采集
日志采集是指利用日志搜集工具将机器数据和网络数据采集到统一的地方进行分析和处理

### 机器数据
机器数据是指软件所能够产生的各种数据

- 日志文件
- 指标数据
- 业务数据

### 网络数据
网络数据是指对网络流量进行抓包和解析


## 日志分析
日志分析是对日志数据进行解析，并结合实际业务进行分析和处理

- 故障排查
- 异常告警
- 趋势预测
- 性能监控
- 业务分析
- 安全审计


## 技术特点
- 日志集中分析，处理和存储
- 全文检索，字段检索，关联分析
- 可视化展示，及时预警



# 采集工具
## linux日志采集工具
### rsyslog
`rsyslog` 是大多数linux系统的默认采集工具，具有以下特点

- 基于c语言开发的，支持多线程的高性能采集工具
- 支持可靠的tcp传输，并且可以使用ssl加密
- 模块化设计，支持按需加载模块使用
- 支持基于内存和文件缓冲队列
- 支持kafka等多种输出
- 支持日志压缩

> rsyslog的基础知识可以参照[这里][1]，官网参考[这里][2]，Github参考[这里][3]

### syslog-ng
`syslog-ng` 也是linux上比较好的采集工具，和 `rsyslog` 类似
> `SUSE Linux`和 `OpenSUSE`默认使用`syslog-ng`，详情参照[这里][9]

### logstash
logstash是新兴的开源日志采集工具，是ELK中重要的一员

|缩写 | 说明 |
|--- |--- |
|E | Elasticsearch（日志存储和检索引擎） |
|L | Logstash（日志采集工具） |
|K | Kibana（可视化展示工具） |


但是由于logstash非常消耗性能，所以衍生了更加轻量的采集工具

|工具 | 说明 |
|--- |--- |
|Filebeat   | 采集文件数据 |
|Metricbeat | 采集指标数据 |
|Packetbeat | 采集网络数据 |
|Winlogbeat | 采集Windows系统日志 |
|Heartbeat  | 监测应用存活状态 |

> `rsyslog`，`syslog-ng`，`logstash`的对比可以参照[这里][10]


## windows日志采集工具
### nxlog
nxlog是windows平台上比较常用的日志采集工具，详情参照[这里][11]

### rsyslog
rsyslog也有windows平台的客户端



<br/> 

---

# 参考

[rsyslog官方文档][1]  
[slog介绍(一) ：BSD syslog协议的格式][2]  
[Linux环境下使用rsyslog管理日志][3]  
[rsyslog使用详解][4]  
[在CentOS和RHEL 5上使用rsyslog构建中央日志主机-Howtoing运维教程][5]  
[使用rsyslog集中管理日志][6]  
[HowTo Configure Mac OS X Syslog To Forward Data][7]  
[Configuring System Message Logging][8]  
[IBM PASE for System i and Syslog / Syslogd][9]  
[Remote SYSLOGD from AS400 to UNIX or Linux Servers][10]  
[使用Evtsys和Nxlog搭建syslog日志服务器-烂泥行天下][11]  
[ELK 5.x 搭建大规模日志实时处理系统][12]  
[rsyslog 的 TCP 转发性能测试][13]  
[Flume日志采集系统——初体验（Logstash对比版）][14]  
[Flume(NG)架构设计要点及配置实践][15]  
[关于Logstash中grok插件的正则表达式例子][16]  
[OpenSUSE - rsyslog wiki][17]  
[Understand logging in Linux][18]  
[What is the difference between syslogd and klogd daemon in Linux? - Quora][19]  
[Unix/Linux system logging, log files, kernel messages][20]  
[RHEL7: 系统日志(rsyslog, journal)][21]  
[Rsyslog configuration for changing source interface][22]  
[reopenOnTruncate is not obeyed unless a state file was loaded · Issue #1090][23]  
[ELK+Filebeat 集中式日志解决方案详解][24]  
[syslog及syslog-ng详解][25]  
[Troubleshooting and debugging syslog-ng][26]  
[[syslog-ng] Cannot find init.d.AIX in contrib folder][27]  
[AIX mkssys Command][28]  
[AIX rmssys Command][29]  
[AIX lssrc  Command][30]  
[[syslog-ng] How to install syslog-ng on AIX 5.3 [English]][31]  
[ELKstack 中文指南 · GitBook][32]  
[Elasticsearch官网][33]  
[Elasticsearch社区][34]  
[aix系统下怎么收集日志 - Elastic中文社区][35]  
[ELK-install-in-AIX-and-Windows][36]  
[基于Flume的美团日志收集系统(一)架构和设计][37]  
[Logstash 最佳实践][38]  
[logstash-forwarder][39] 
[logstash-forwarder-java][40]  
[How to create a java keystore][41]  
[ELK 性能(1) — Logstash 性能及其替代方案 - Richaaaard - 博客园][42]  
[Logstash Forwarder 配置详解][43]  
[Logstash Forwarder 长期运行][44]  
[Add setting to enable string escaping in Logstash pipeline config][45]  
[What is the best date/time parsing library in any language? - Quora][46]  
[logstash-forwarder-java javax.net.ssl.SSLHandshakeException][47]  
[rsyslog, Using Wildcards with rsyslog's File Monitor imfile][48]  
[每秒百万级流式日志处理架构的开发运维调优笔记][49]  
[Linux中rsyslog日志系统详解][50]  
[rsyslog 队列介绍][51]  
[Linux中syslog-ng日志系统 – 运维那点事][52]  
[‘Afsql’ error on syslog-ng resolved][53]  
[syslog-ng on vServer with Debian Lenny][54]  
[Troubleshooting syslog-ng][55]  
[日志易：IT 运维分析及海量日志搜索的实践之路（上）][56]  
[日志易：IT 运维分析及海量日志搜索的实践之路（下）][57]
[日志易官网][58]  
[Loggly官网][59]  
[Splunk官网][60]  
[如何查看linux系统下的各种日志文件 linux 系统日志的分析大全][61]  
[/var/log目录下的20个Linux日志文件功能详解][62]  
[Linux系统中‘dmesg’命令处理故障和收集系统信息的7种用法][63]  
[Linux中logrotate日志管理工具详解][64]  
[被遗忘的Logrotate][65]  
[logrotate机制和原理][66]  
[Linux日志文件总管——logrotate][67]  
[/dev/random和/dev/urandom的一点备忘][68]  
[怎么使用 /dev/urandom 生成固定长度的随机数？][69]  

[1]: http://www.rsyslog.com/
[2]: http://areyouok.iteye.com/blog/251590
[3]: https://segmentfault.com/a/1190000003509909
[4]: http://bigsec.net/one/tool/rsyslog.html
[5]: https://www.howtoing.com/building-a-central-loghost-on-centos-and-rhel-5-with-rsyslog/
[6]: http://dmdgeeker.com/post/rsyslog-collect-logs/
[7]: https://wiki.splunk.com/Community:HowTo_Configure_Mac_OS_X_Syslog_To_Forward_Data
[8]: https://www.cisco.com/c/en/us/td/docs/switches/lan/catalyst3750x_3560x/software/release/12-2_55_se/configuration/guide/3750xscg/swlog.pdf
[9]: https://www.ibm.com/support/home/
[10]: http://as400topics.blogspot.com/2011/12/remote-syslogd-from-as400-to-unix-or.html
[11]: http://www.ilanni.com/?p=595
[12]: http://www.jianshu.com/p/f3658d267b5d
[13]: http://chenlinux.com/2015/02/12/rsyslog-forwarder-testing/
[14]: http://www.cnblogs.com/xing901022/p/5631445.html
[15]: http://shiyanjun.cn/archives/915.html
[16]: http://blog.csdn.net/liukuan73/article/details/52318243
[17]: http://wiki.rsyslog.com/index.php/OpenSUSE
[18]: https://unix.stackexchange.com/questions/205883/understand-logging-in-linux
[19]: https://www.quora.com/What-is-the-difference-between-syslogd-and-klogd-daemon-in-Linux
[20]: http://teaching.idallen.com/cst8207/12f/notes/805_system_log_files.html
[21]: https://feichashao.com/rhel7-logging/
[22]: https://serverfault.com/questions/532278/rsyslog-configuration-for-changing-source-interface
[23]: https://github.com/rsyslog/rsyslog/issues/1090
[24]: https://www.ibm.com/developerworks/cn/opensource/os-cn-elk-filebeat/index.html
[25]: http://ant595.blog.51cto.com/5074217/1080922
[26]: https://pzolee.blogs.balabit.com/2009/12/troubleshooting-and-debugging-syslog-ng/
[27]: https://lists.balabit.hu/pipermail/syslog-ng/2009-January/012454.html
[28]: https://www.ibm.com/support/knowledgecenter/en/ssw_aix_61/com.ibm.aix.cmds3/mkssys.htm
[29]: https://www.ibm.com/support/knowledgecenter/zh/ssw_aix_72/com.ibm.aix.cmds4/rmssys.htm
[30]: https://www.ibm.com/support/knowledgecenter/zh/ssw_aix_72/com.ibm.aix.cmds3/lssrc.htm
[31]: http://networker.tistory.com/421
[32]: https://www.gitbook.com/book/chenryn/elk-stack-guide-cn/details
[33]: https://www.elastic.co/cn/products/elasticsearch
[34]: https://elasticsearch.cn/explore/
[35]: https://elasticsearch.cn/question/1815
[36]: http://l1z2g9.github.io/2015/11/17/ELK-install-in-AIX-and-Windows/
[37]: https://tech.meituan.com/mt-log-system-arch.html
[38]: https://doc.yonyoucloud.com/doc/logstash-best-practice-cn/get_start/index.html
[39]: https://github.com/elastic/logstash-forwarder/blob/master/README.md
[40]: https://github.com/didfet/logstash-forwarder-java
[41]: https://github.com/didfet/logstash-forwarder-java/blob/master/HOWTO-KEYSTORE.md
[42]: http://www.cnblogs.com/richaaaard/p/6109595.html
[43]: https://github.com/chenryn/logstash-best-practice-cn/blob/master/ecosystem/logstash_forwarder.md
[44]: https://github.com/chenryn/logstash-best-practice-cn/blob/master/get_start/daemon.md
[45]: https://github.com/elastic/logstash/pull/7442
[46]: https://www.quora.com/What-is-the-best-date-time-parsing-library-in-any-language
[47]: https://github.com/didfet/logstash-forwarder-java/issues/29
[48]: https://www.slideshare.net/rainergerhards1/using-wildcards-with-rsyslogs-file-monitor-imfile
[49]: https://cloudblog.github.io/2016/11/19/%E6%AF%8F%E7%A7%92%E7%99%BE%E4%B8%87%E7%BA%A7%E6%B5%81%E5%BC%8F%E6%97%A5%E5%BF%97%E5%A4%84%E7%90%86%E6%9E%B6%E6%9E%84%E7%9A%84%E5%BC%80%E5%8F%91%E8%BF%90%E7%BB%B4%E8%B0%83%E4%BC%98%E7%AC%94%E8%AE%B0/
[50]: http://www.ywnds.com/?p=1304
[51]: http://www.jianshu.com/p/74c1f8ac00c7
[52]: http://www.ywnds.com/?p=2778
[53]: http://www.crackjet.com/afsql-error-on-syslog-ng-resolved/
[54]: https://www.carrier-lost.org/syslog-ng-on-vserver-with-debian-lenny/
[55]: https://www.balabit.com/documents/syslog-ng-ose-latest-guides/en/syslog-ng-ose-guide-admin/html/chapter-troubleshooting-syslog-ng.html
[56]: https://www.qcloud.com/community/article/328693
[57]: https://www.qcloud.com/community/article/693305
[58]: https://www.rizhiyi.com/
[59]: https://www.loggly.com/
[60]: https://www.splunk.com/zh-hans_cn/
[61]: http://blog.csdn.net/u013038461/article/details/44154221
[62]: http://h2appy.blog.51cto.com/609721/781281/
[63]: https://linux.cn/article-3587-1.html
[64]: http://www.ywnds.com/?p=5471
[65]: http://www.udpwork.com/item/9695.html
[66]: http://www.lightxue.com/how-logrotate-works
[67]: https://linux.cn/article-4126-1.html
[68]: http://blog.csdn.net/ohmygirl/article/details/40385083
[69]: https://segmentfault.com/q/1010000007761269/a-1020000007761350