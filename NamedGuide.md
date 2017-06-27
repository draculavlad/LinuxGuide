## Named Guide

# for example, your have 4 hosts:
```conf
node0.kzk.lc.   172.20.78.191
node1.kzk.lc.   172.20.78.192
node2.kzk.lc.   172.20.78.193
node3.kzk.lc.   172.20.78.194
```

# add zone configuration to /etc/named.conf:
```conf
zone "kzk.lc" IN {
        type master;
        file "/var/named/data/kafka.cluster";
};
```

# add data configuration to 
```conf
$TTL 15m
@                    IN SOA  kzk.lc.  root.kzk.lc. (
                       2016111101 ; serial (yyyymmddnn)
                       1h         ; refresh
                       10m        ; retry
                       14d        ; expire
                       10m        ; nxdomain ttl
                     )

; name servers - NS records
    IN      NS      node0.kzk.lc.
    IN      NS      node1.kzk.lc.
    IN      NS      node2.kzk.lc.
    IN      NS      node3.kzk.lc.

; name servers - A records
node0.kzk.lc.   IN      A       172.20.78.191
node1.kzk.lc.   IN      A       172.20.78.192
node2.kzk.lc.    IN      A       172.20.78.193
node3.kzk.lc.    IN      A       172.20.78.194
```
