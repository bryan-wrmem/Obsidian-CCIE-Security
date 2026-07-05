Router Server

```
clock timezone GST 4

interface Ethernet0/0
 no shutdown
 ip address 192.168.0.254 255.255.255.0

ntp authentication-key 100 md5 cisco
ntp authenticate
ntp trusted-key 100
ntp master 2
```

R17

```
clock timezone IST 5 30

interface Ethernet0/0
 no shutdown
 ip address 192.168.0.245 255.255.255.0

ntp authentication-key 100 md5 cisco
ntp authenticate
ntp trusted-key 100
```