[Open: Pasted image 20260226094620.png](../../../Media/7f6291e97e90be587772dec2bd1e658a_MD5.jpeg)
![](../../../Media/7f6291e97e90be587772dec2bd1e658a_MD5.jpeg)

LTPv3 - layer tunnel protocol version 3
allows to tunnel protocols over l3

useful for remote/branch sites to allow resources to be on the "same layer 2 network"

R2

```
# IKEv2 Config

crypto ikev2 keyring key1
	peer 10.10.10.3
	address 10.10.10.3
	pre-shared-key cisco123

crypto ikev2 profile IkeMike
	match identity remote address 10.10.10.3 255.255.255.255
	identity local address 10.10.10.2
	authentication remote pre-share
	authentication local pre-share
	keyring local key1

# Tunnel Interface Config

int tunnel 1
	ip address 172.16.1.2 255.255.255.0
	tunnel source 10.10.10.2
	tunnel destination 10.10.10.3
	tunnel protection ipsec profile IkeMike

# L2TPv3 / pseudowire Config

pseudowire-class l2tp1
	encapsulation l2tpv3
	ip local interface tunnel 1

# Config for interface facing L2 networks

int e0/0
	no ip address
	xconnect 172.16.1.3 1001 encapsulation l2tpv3 pw-class l2tp1
```

R3

```

# IKEv2 Config

crypto ikev2 keyring key1
	peer 10.10.10.2
	address 10.10.10.2
	pre-shared-key cisco123

crypto ikev2 profile IkeMike
	match identity remote address 10.10.10.2 255.255.255.255
	identity local address 10.10.10.3
	authentication remote pre-share
	authentication local pre-share
	keyring local key1

# Tunnel Interface Config

int tunnel 1
	ip address 172.16.1.2 255.255.255.0
	tunnel source 10.10.10.2
	tunnel destination 10.10.10.3
	tunnel protection ipsec profile IkeMike

# L2TPv3 / pseudowire Config

pseudowire-class l2tp1
	encapsulation l2tpv3
	ip local interface tunnel 1

# Config for interface facing L2 networks

int e0/0
	no ip address
	xconnect 172.16.1.4 1001 encapsulation l2tpv3 pw-class l2tp1
```


