# SSH Tunnel Guide

希望写完这篇小文档就再也不需要看这篇小文档了 ╮(╯_╰)╭

## TLDR

一句话连接远程服务器打开 SSH 隧道，并在本地 9999 端口开启 socks5 转发服务：

```
ssh -CTND 9999 username@remote_host
```

## Options

`ssh` 的参数可以用 `man ssh` 查看。其中跟开隧道相关的有这几个：

- __`-C`__ Requests gzip compression of all data  
在数据请求里启用 gzip 压缩。能大大节约流量。

- __`-T`__ Disable pseudo-tty allocation  
禁止远端分配虚拟终端。反正你也不会向对方发送指令。

- __`-N`__ Do not execute a remote command  
不执行远程命令。做隧道转发的专用参数。

- __`-D <port>`__ Specifies a local ‘dynamic’ application-level port forwarding.  
指定本地端口。这就是你用来连接的隧道入口。

- __`-f`__ Requests ssh to go to background just before command execution.  
使 SSH 隧道在后台运行。用了这个之后想停止服务就要杀进程 ID 了：
    - `ps aux | grep ssh` 查找 ssh 的进程
    - `kill processId` 杀 ID
