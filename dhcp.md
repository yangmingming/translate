# 动态主机配置协议（DHCP）

DHCP 是一种向一个 DHCP 客户端 动态分配 [IP 地址](https://wiki.wireshark.org/IP-address)参数（或者其他内容）的客服端/服务端协议。它被实施为 [BOOTP](https://wiki.wireshark.org/BOOTP) 的一种选项。

许多操作系统（包括 Windows 98 和后续版本以及 Mac OS 8.5 及后续版本）在没有有效的 DHCP 服务器的时候使用 [APIPA](https://wiki.wireshark.org/APIPA)来本地分配一个 ip 地址。

# 历史
* [RFC1531][1] “动态主机配置协议”，1993 年 10 月，被 RFC1541 所废弃
* [RFC1541][2] “动态主机配置协议”，1993 年 10 月，被 RFC2131 所废弃
* [RFC2131][3] “动态主机配置协议”，1997 年 3 月，被 RFC3396 所更新
* [RFC3396][4] “在动态主机配置协议（DHCPv4）中编码长选项”，2002 年 11 月

# 协议的依赖
* [BOOTP][5]：DHCP 使用 [BOOTP][5] 作为传输协议

# 流量举例
![](https://wiki.wireshark.org/DHCP?action=AttachFile&do=get&target=dhcp-ws.png)

# Wireshark
DHCP 的解析器功能完全

# Windows 大小端 bug 检测
微软的 Windows 大部分版本在编码秒字段的时候使用小端。Wireshark 将会尝试检测这个并且在包详细信息面板显示“小端 bug？”的信息。举例如下，Windows XP 客户端发送的包，秒对应的值是 0x0e00（3584， 将近一个小时），即使客户端没有尝试那么长时间。解析成为 0x000e（14）则匹配上第一次请求（3号对应的包）持续的时间。
![](https://wiki.wireshark.org/DHCP?action=AttachFile&do=get&target=dhcp-le-bug.png)

# 首选项设置
* Decode Option 85 as String: Novell Servers option 85 can be configured as a string instead of address.
* PacketCable CCC protocol version: The PacketCable CCC protocol version.
* PacketCable CCC option: Option Number for PacketCable CableLabs Client Configuration.
* Custom BootP/DHCP Options (Excl. suboptions): Define custom interpretation of options

＃　捕获的例子文件  
* [SampleCaptures/dhcp.pcap][a]  
* [SampleCaptures/dhcp-auth.pcap.gz][b]  
* [SampleCaptures/PRIV_bootp-both_overload.pcap][c]  
* [SampleCaptures/PRIV_bootp-both_overload_empty-no_end.pcap][c]  

# 显示过滤器
由于 DHCP 是 BOOTP 一种实现，所以你只可以通过 BOOTP 进行过滤。当通过随意的端口进行通信的时候，你不能直接通过 BOOTP 协议进行过滤。BOOTP 流量通常情况下使用 67 和 68 端口进行通信，并且通过 67 和 68 端口的流量通常情况下就是 BOOTP 流量，所以你可以通过这些端口过滤。

只通过 67 和 68 端口进行流量抓包  

	port 67 or port 68

在许多系统，你可以使用“port bootps”代替“port 67”，用“port bootpc”代替“port 68”。

在[RFC 搜索][6]你可以搜索 DHCP 相关内容，有好多 DHCP 选项通过一些 RFC 传播开来。

# 讨论
什么是小端bug？也有一些关于“持续秒”的错误哦，但是没有关于这个的问题。（我已经在 DHCP 请求数据中发现这个错误，请求被加载2次，持续3秒，并且其中一次请求包含这次错误）—— [CortoGueguen][e].

如果你认为在 Wireshark 的 DHCP 解析器有bug，或者在 Wireshark Bugzilla 上写下这个bug，或者向 Wireshark 用户邮箱列表发一封邮件。这儿不是报告 Wireshark bug 的地方。 —— Guy Harris

我认为 [CortoGueguen][e] 可能引用了 Wireshark 显示的一个错误信息。我已经随着截图添加了一个说明。 —— [GeraldCombs][f]

是的，的确如此，[GeraldCombs][f]，多谢 —— [CortoGueguen][e]

--------------------------------------------------------------------------------

via: https://wiki.wireshark.org/DHCP

译者：[yangmingming](https://github.com/yangmingming)
校对：

[1]: http://www.ietf.org/rfc/rfc1531.txt
[2]: http://www.ietf.org/rfc/rfc1541.txt
[3]: http://www.ietf.org/rfc/rfc2131.txt
[4]: http://www.ietf.org/rfc/rfc3396.txt
[5]: https://wiki.wireshark.org/BOOTP
[6]: http://www.rfc-editor.org/rfcsearch.html
[a]: https://wiki.wireshark.org/SampleCaptures?action=AttachFile&do=view&target=dhcp.pcap
[b]: https://wiki.wireshark.org/SampleCaptures?action=AttachFile&do=view&target=dhcp-auth.pcap.gz
[c]: https://wiki.wireshark.org/SampleCaptures?action=AttachFile&do=view&target=PRIV_bootp-both_overload.pcap
[d]: https://wiki.wireshark.org/SampleCaptures?action=AttachFile&do=view&target=PRIV_bootp-both_overload_empty-no_end.pcap
[e]: https://wiki.wireshark.org/CortoGueguen
[f]: https://wiki.wireshark.org/GeraldCombs

