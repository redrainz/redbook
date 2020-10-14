1. 
    sudo apt install shadowsocks

2.
    python 2.7

    pip install

	pip install --upgrade pip
	
    pip install  setuptools

    pip install shadowsocks

    vim /etc/shadowsocks.json


    {
        "server":"0.0.0.0",
        "server_port":8390,
        "local_address":"127.0.0.1",
        "local_port":1080,
        "password":"redrain",
        "timeout":3000,
        "method":"aes-256-cfb",
        "fast_open":false
    }

    {
        “server”:”0.0.0.0″,
        “port_password”: {
        “端口1”: “密码1”,
        “端口2”: “密码2”
        },
        “timeout”:300,
        “method”:”aes-256-cfb”,
        “fast_open”: false
    }

    ssserver -c /etc/shadowsocks.json -d start

    vim /etc/rc.local //开机启动

    nohup ssserver -c /etc/shadowsocks.json start >/dev/null &

    
3. linux
```
    Ubuntu 16.04, Python 2.7.12.

安装libsodium:
sudo apt install libsodium-dev

安装shadowsocks:
pip install https://github.com/shadowsocks/shadowsocks/archive/master.zip -U


```

```
启动Privoxy
systemctl enable privoxy
systemctl start privoxy
systemctl status privoxy

```


```
/etc/profile
设置http/https代理：
export http_proxy=118.210.42.251:44367
或：
export https_proxy=118.210.42.251:44367


要取消该设置：
unset http_proxy
或：
unset https_proxy
```
