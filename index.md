
#### 免费frp节点1（增加中...）
你只需要修改frpc.ini 中的服务器地址以及端口等，例如服务器地址 s1.frp.asia 端口7004 

```
[common] 
server_addr = s1.frp.asia
server_port = 7004
token = loz7wS
```
修改好配置文件，运行客户端就可以使用了！推荐使用stcp方式连接！

#### 示例


这个示例将会创建一个只有自己能访问到的 SSH 服务代理。
对于某些服务来说如果直接暴露于公网上将会存在安全隐患。

使用 stcp(secret tcp) 类型的代理可以避免让任何人都能访问到要穿透的服务，但是访问者也需要运行另外一个 frpc 客户端。

frps.ini 内容如下：

[common]
bind_port = 7000
在需要暴露到外网的机器上部署 frpc，且配置如下：
```
[common]
server_addr = x.x.x.x
server_port = 7000

[secret_ssh]
type = stcp
# 只有 sk 一致的用户才能访问到此服务
sk = abcdefg
local_ip = 127.0.0.1
local_port = 22
```
在想要访问内网服务的机器上也部署 frpc，且配置如下：
```
[common]
server_addr = x.x.x.x
server_port = 7000

[secret_ssh_visitor]
type = stcp
# stcp 的访问者
role = visitor
# 要访问的 stcp 代理的名字
server_name = secret_ssh
sk = abcdefg
# 绑定本地端口用于访问 SSH 服务
bind_addr = 127.0.0.1
bind_port = 6000
```

现在可以通过访问本地127.0.0.1的6000端口访问到内网机器SSH 了。

[ 更多frp文档](https://gofrp.org/docs/)



---



* 免费frp仅供学习和研究，不得用于非法用途！保留所有权利。



![thisisapicture](https://tse2-mm.cn.bing.net/th/id/OIP-C.-_Hy7CugwLBZ-wXn4AMFIAHaCk?w=330&h=121&c=7&r=0&o=5&dpr=1.3&pid=1.7)

[ 扫一扫](https://github.com/lcrs-git/frpAsia/blob/main/upload.md)
 帮助我们维护和开通更多frp服务节点。

©2023 frpAsia &ensp; [来吐槽](https://github.com/lcrs-git/frpAsia/issues/1)&emsp;

