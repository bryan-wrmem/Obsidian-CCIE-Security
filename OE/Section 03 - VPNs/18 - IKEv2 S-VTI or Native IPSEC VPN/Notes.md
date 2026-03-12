[Open: Pasted image 20260312095515.png](../../../Media/8ee8a36bfa0b7847b95c729f3c6d21d6_MD5.jpeg)
![](../../../Media/8ee8a36bfa0b7847b95c729f3c6d21d6_MD5.jpeg)

SVTI - static virtual tunnel interface

```
# UK Config

crypto ikev2 proposal PROPOSAL
	encryption aes-cbc-128
	integrity sha1
	group 2

crypto ikev2 policy POLICY
	proposal PROPOSAL
	
crypto ikev2 keyring UK
	peer NZ
	address 2.1.1.2
	pre-share moshin123
	
crypto ikev2 profile PROFILE
	match identity remote address 2.1.1.2 255.255.255.255
	authentication local pre-share
	authentication remote pre-share
	keyring local UK
	
crypto ipsec transform-set TS esp-3des esp-sha-hmac

crypto ipsec profile SVTIPROFILE
	set transform-set TS
	set ikev2 PROFILE
	
int tunnel 1
	ip address 192.168.1.1 255.255.255.0
	tunnel source 1.1.1.2
	tunnel destination 2.1.1.2
	tunnel protection ipsec profile SVTIPROFILE
	tunnel mode ipsec ipv4
	
router eigrp 1
	network 192.168.1.0
	network 192.168.10.0
	
	
	
# ==================

# NZ Config

crypto ikev2 proposal PROPOSAL
	encryption aes-cbc-128
	integrity sha1
	group 2

crypto ikev2 policy POLICY
	proposal PROPOSAL
	
crypto ikev2 keyring NZ
	peer NZ
	address 1.1.1.2
	pre-share moshin123
	
crypto ikev2 profile PROFILE
	match identity remote address 1.1.1.2 255.255.255.255
	authentication local pre-share
	authentication remote pre-share
	keyring local NZ
	
crypto ipsec transform-set TS esp-3des esp-sha-hmac

crypto ipsec profile SVTIPROFILE
	set transform-set TS
	set ikev2 PROFILE
	
int tunnel 1
	ip address 192.168.1.2 255.255.255.0
	tunnel source 2.1.1.2
	tunnel destination 1.1.1.2
	tunnel mode ipsec ipv4
	tunnel protection ipsec profile SVTIPROFILE
	
router eigrp 1
	network 192.168.1.0
	network 192.168.20.0

```