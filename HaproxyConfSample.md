## Configuration File Sample

```properties
global
    log         127.0.0.1 local2
    chroot      /var/lib/haproxy
    pidfile     /var/run/haproxy.pid
    maxconn     4000
    user        haproxy
    group       haproxy
    daemon
    # turn on stats unix socket
    stats socket /var/lib/haproxy/stats
defaults
    mode                    tcp 
    log                     global
    option                  dontlognull
    option                  redispatch
    retries                 3
    timeout queue           1m
    timeout connect         10s
    timeout client          1m
    timeout server          1m
    timeout check           10s
    maxconn                 3000
    
    
frontend front-$app_name-$app_port
	bind *:$app_port
	default_backend    back-$app_name-$app_port
	
backend back-$app_name-$app_port
	balance leastconn
	server ${app_name}-$no $app_host_ip:$app_port check
```
