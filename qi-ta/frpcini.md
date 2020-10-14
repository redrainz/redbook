```
[common]
server_addr = x.x.x.x
server_port = 7000
pool_count = 20

[ssh]
type = tcp
local_ip = 127.0.0.1
local_port = 22
remote_port = 6000
tcp_mux = true

[web]
type = tcp
local_ip =127.0.0.1
local_port = 18080
remote_port = 18083
tcp_mux = true
use_compression = true


[front]
type = tcp
local_ip =127.0.0.1
local_port = 13000
remote_port = 18085
tcp_mux = true
use_compression = true

[boot]
type = tcp
local_ip =127.0.0.1
local_port = 8080
remote_port = 18084
tcp_mux = true
use_compression = true

```