
1. apt install aria2
2. 普通下载

    ```shell
    aria2c https://github.com/fatedier/frp/releases/download/v0.31.2/frp_0.31.2_darwin_amd64.tar.gz -d / -o 1.txt -s 10
    ```
    
3. 文件下载
    1. down.conf  *配置以空格开头*
    2. ```aria2c -i down.conf```


```
https://github.com/fatedier/frp/releases/download/v0.31.2/frp_0.31.2_darwin_amd64.tar.gz
 dir=/
 out=1.txt
 split=10
https://github.com/fatedier/frp/releases/download/v0.31.2/frp_0.31.2_darwin_amd64.tar.gz
 dir=/
 out=2.txt
 split=10
```

4. 配置aria2 rpc
    1. aria2.conf
    2. aria2c --conf-path=aria2.conf -D
    
```properties
#用户名
#rpc-user=user
#密码
#rpc-passwd=passwd
#上面的认证方式不建议使用,建议使用下面的token方式
#设置加密的密钥
rpc-secret=token
#允许rpc
enable-rpc=true
#允许所有来源, web界面跨域权限需要
rpc-allow-origin-all=true
#允许外部访问，false的话只监听本地端口
rpc-listen-all=true
#RPC端口, 仅当默认端口被占用时修改
#rpc-listen-port=6800
#最大同时下载数(任务数), 路由建议值: 3
max-concurrent-downloads=5
#断点续传
continue=true
#同服务器连接数
max-connection-per-server=10
#最小文件分片大小, 下载线程数上限取决于能分出多少片, 对于小文件重要
min-split-size=10M
#单文件最大线程数, 路由建议值: 5
split=10
#下载速度限制
max-overall-download-limit=0
#单文件速度限制
max-download-limit=0
#上传速度限制
max-overall-upload-limit=0
#单文件速度限制
max-upload-limit=0
#断开速度过慢的连接
#lowest-speed-limit=0
#验证用，需要1.16.1之后的release版本
#referer=*
#文件保存路径, 默认为当前启动位置
#dir=/Users/xxx/Downloads
#文件缓存, 使用内置的文件缓存, 如果你不相信Linux内核文件缓存和磁盘内置缓存时使用, 需要1.16及以上版本
#disk-cache=0
#另一种Linux文件缓存方式, 使用前确保您使用的内核支持此选项, 需要1.15及以上版本(?)
#enable-mmap=true
#文件预分配, 能有效降低文件碎片, 提高磁盘性能. 缺点是预分配时间较长
#所需时间 none < falloc ? trunc « prealloc, falloc和trunc需要文件系统和内核支持
file-allocation=prealloc
#日志文件
log=/root/aria2.log
#log-level=info
#记录下载历史文件目录
input-file=/root/aria2.session
#存放下载历史文件目录
save-session=/root/aria2.session
save-session-interval=60
force-save=true

```
