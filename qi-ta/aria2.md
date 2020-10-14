[Windows 配置 Aria2 及 Web 管理面板教程](https://www.cnblogs.com/jpfss/p/8622938.html)

今天闲来没事，想找点东西折腾下，然后看到个在 Debian 7 x64 系统环境下配置 Aria2 和 Web 管理面板的教程，针对 Linux 服务器用的。但很多人没服务器，也不知道什么是 Aria2，更不知道如何配置，网上教程基本都如出一辙，没啥好看的，所以今天就教大家如何在 Windows 上配置Aria2，步骤基于那篇文章改良的。

很多人没听说过 Aria2，Aria2 是什么？

Aria2 简介
Aria2 是一个多平台轻量级，支持 HTTP、FTP、BitTorrent 等多协议、多来源的命令行下载工具。Aria2 可以从多个来源、多个协议下载资源，最大的程度上利用了你的带宽。Aria2 有着非常小的资源占用，在关闭磁盘缓存的情况下，物理内存占用通常为 4M（正常 HTTP/FTP 下载的情况下），BitTorrent 下载每秒2.8M/S的情况下，CPU 占有率约为 6%。Aria2 支持 JSON-RPC 和 XML-RPC 接口远程调用。
（翻译自：Aria2）

很多人在 Windows 可能用过 Internet Download Manager，是很好用的多线程下载工具。Aria2 跟 IDM 类似，不仅可以多线程下载，还可以通过多来源进行下载，简单的说就是从多个镜像服务器同时下载一个文件，Aria2 还支持 BT 协议，弥补了 IDM 只支持 HTTP 和 FTP 的痛点。

好了，废话不多说，教程开始。

下载 Aria2 及 Web 管理面板
废话
Aria2 是一个命令行下载工具，所以使用的时候要敲命令，可是每下载一个文件敲一条命令，太麻烦了，那咋办？Aria2 支持远程接口调用，只需要配置一个 Web 管理面板就可以在浏览器管理 Aira2 了

1.下载并解压 Aria2 主程序

进入 https://github.com/aria2/aria2/releases 下载 Aria2 主程序

2.下载并解压 Web 管理面板

进入 https://github.com/mayswind/AriaNg/releases 下载 Web 管理面板，下载第一个 ZIP 压缩包，下载后解压。

3.下载 Web 服务器

点击 https://cdn.mivm.cn/www.mivm.cn/archives/windows-aria2/EasyWebSvr.zip 下载 Web 服务器，下载后解压。

安装/配置 Aria2 及 Web 管理面板
1.点击 https://cdn.mivm.cn/www.mivm.cn/archives/windows-aria2/aria2_conf.zip 下载 Aria2 配置文件，解压至 Aria2 目录里。

默认已经配置好了，如果需要更改配置，用记事本等文本编辑器，打开 aria2.conf ，里面有对应的注释，这里说几个比较重要的参数。

dir=Download
文件保存目录 ，默认下载到 Aria2 目录的 Download 文件夹。

disk-cache=32M
硬盘缓存，默认 32M，作用是将数据缓存到内存中。

file-allocation=none
文件预分配方式，配置文件有速度比较，具体看你的硬盘，机械硬盘用默认的none不进行预分配就好，固态硬盘可以选择falloc。

enable-rpc=true
是否启用 RPC，RPC 是远程调用接口，开启：true，关闭：false。

#rpc-secret=mivm.cn
RPC 授权令牌，如果启用授权令牌，远程管理会要求输入令牌，去掉 # 即可启用，默认授权令牌：mivm.cn.

剩下的参数配置文件有注释，更多参数可以查阅官方文档（英文）。

修改完记得重启 Aria2

2.点击 https://cdn.mivm.cn/www.mivm.cn/archives/windows-aria2/aria2_bat.zip 下载Aria2 控制脚本，解压至 Aria2 目录里。

Start.bat
带命令行窗口输出启动 Aria2

Start.vbs
不带命令行窗口启动 Aria2

Stop.bat
停止 Aria2

Status.bat
查看 Aria2 进程状态

Restart.bat
重启 Aria2

Boot.bat
开启或关闭 Aria2 开机启动

运行 Start.vbs 或 Start.bat 启动 Aria2

首次运行会出现防火墙警告，允许即可。

3.打开 Web 服务器目录，打开 EasyWebSvr.exe → 点击底部的锤子图标 → [设置] → [主目录] 设置为 Web 管理面板目录 → [确定] → 点击底部的锤子图标 → [启动服务器]

如果不想搭建Web服务器的话，直接访问 http://yaaw.ghostry.cn/ 或 http://webui-aria2.ghostry.cn/ 也可以 。

如果出现404等无法访问的情况，请检查[主目录]是否正确或重启 Web 服务器。

[开机自动运行] 需要使用管理员权限运行

关闭服务器：右键托盘图标选择[关闭服务器]

配置完服务器第二次运行不会显示界面，后台运行。

4.Web服务器开启后，浏览器访问 http://localhost/ 就可以访问 Web 管理面板。

设置中文方法：点击 [AriaNg Settings] → [Language] 选择 [简体中文]

5. [Aria2 状态] 如果显示 已连接，恭喜你，Aria2 搭建成功，如果显示 未连接，请检查 Aria2 是否正常开启，或者重启 Aria2。

Aria2 使用方法
Web 管理面板点击 [新建]，可以添加 HTTP、FTP、BT 任务等，同时添加多个任务每行一个 URL，添加镜像 URL 用空格分割，点击文件夹图标可以打开种子文件等。

如果你使用的是 Chrome 浏览器，可以使用 https://chrome.google.com/webstore/detail/llhdoolhgigbnppanegcohafahjgbpek 这个扩展程序来让 Aria2 下载文件，其他浏览器请自行查找扩展。

小贴士
Web 管理面板删除下载任务后，Aria2 并不会删除下载文件或缓存，需要去下载文件夹删除掉。
同一个局域网内，其他设备输入当前设备内网 IP 地址，就可以访问 Web 管理界面 。
浏览器关闭 Web 管理面板也不影响 Aria2 下载。
教程里有不懂或者不对的地方，给我留言。