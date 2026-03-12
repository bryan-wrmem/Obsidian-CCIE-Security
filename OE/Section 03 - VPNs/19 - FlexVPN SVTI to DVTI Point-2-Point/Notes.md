[Open: Pasted image 20260312104938.png](../../../Media/afe8084f48d21bc9e5b75d08f1172769_MD5.jpeg)
![](../../../Media/afe8084f48d21bc9e5b75d08f1172769_MD5.jpeg)

SVTI-SVTI - Static IPs
DVTI - SVTI - Hub 2 Spoke
DVTI - SVTI - Spoke 2 Spoke

Tokyo will have Dynamic IP
Doha Static IP

```
# ============================
# Tokyo

# Phase 1

crypto ikev2 proposal PROPOSAL
	integrity sha1
	encryption 3des
	group 2
	
crypto ikev2 policy POLICY
	proposal PROPOSAL
	
crypto ikev2 keyring TOKYO
	peer Doha
	address 5.5.5.2
	pre-shared-key moshin123
	
crypto ikev2 profile PROFILE
	match identity remote address 5.5.5.2
	authentication local pre-share
	authentication remote pre-share
	keyring local TOKYO

# Phase 2

crypto ipsec transform-set TS esp-3des esp-sha-hmac

crypto ipsec profile DVTIPROF
	set transform-set TS
	set ikev2 PROFILE
	
int tunnel 1
	ip address 192.168.1.3 255.255.255.0
	tunnel source e0/0
	tunnel destination 5.5.5.2
	tunnel protection ipsec profile DVTIPROF
	tunnel mode ipsec ipv4

router eigrp 1
	network 192.168.1.0
	network 172.16.1.0 255.255.255.0
	network 172.16.2.0 255.255.255.0

# ============================
# Doha

# Phase 1

crypto ikev2 proposal PROPOSAL
	integrity sha1
	encryption 3des
	group 2
	
crypto ikev2 policy POLICY
	proposal PROPOSAL
	
crypto ikev2 keyring DOHA
	peer SPOKES
	address 0.0.0.0
	pre-shared-key moshin123
	
crypto ikev2 profile PROFILE
	match identity remote address 0.0.0.0
	authentication local pre-share
	authentication remote pre-share
	keyring local DOHA

# Phase 2

crypto ipsec transform-set TS esp-3des esp-sha-hmac

crypto ipsec profile DVTIPROF
	set transform-set TS
	set ikev2 PROFILE

int lo1
	ip address 192.168.1.1 255.255.255.0

int virtual-template 1 type tunnel
	ip unnumbered lo1
	tunnel source e0/0
	tunnel mode ipsec ipv4
	tunnel protection ipsec profile DVTIPROF

crypto ikev2 profile IKEV2-DOH
 match identity remote address 0.0.0.0 
 authentication remote pre-share
 authentication local pre-share
 keyring local DOHA
 virtual-template 1
!

router eigrp 1
	network 192.168.1.0
	network 172.16.9.0 255.255.255.0
	network 172.16.10.0 255.255.255.0
	
# ============================
```