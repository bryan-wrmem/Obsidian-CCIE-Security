[Open: Pasted image 20260324084159.png](../../../Media/1f534e31fd19f2644f4e5dbff6e29751_MD5.jpeg)
![](../../../Media/1f534e31fd19f2644f4e5dbff6e29751_MD5.jpeg)

Default creds - admin / Admin123

FMC Config

[Open: Pasted image 20260325135912.png](../../../Media/3af0159f1b8c21726982fc85f2639d49_MD5.jpeg)
![](../../../Media/3af0159f1b8c21726982fc85f2639d49_MD5.jpeg)

[Open: Pasted image 20260325140005.png](../../../Media/778ec3a233c74cccd968f2ffdc504ed8_MD5.jpeg)
![](../../../Media/778ec3a233c74cccd968f2ffdc504ed8_MD5.jpeg)

[Open: Pasted image 20260325140018.png](../../../Media/109eed23f5d4e5a34038bdc1f974a65b_MD5.jpeg)
![](../../../Media/109eed23f5d4e5a34038bdc1f974a65b_MD5.jpeg)

[Open: Pasted image 20260325140302.png](../../../Media/fe14f153dd0bd8745a59691e021c3bee_MD5.jpeg)
![](../../../Media/fe14f153dd0bd8745a59691e021c3bee_MD5.jpeg)

R4 IKEv2 Policy
Integrity - SHA
Encryption - AES
PRF - SHA
DH - 14





R4 IPSec Proposal
HASH - SHA-1
Encryption - AES

R4 Config

```
crypto ikev2 proprosal v2-proposal
	encryption aes-gcm-256
	prf sha1
	group 14

crypto ikev2 policy v2-policy
	proposal v2-proposal
	
crypto ikev2 keyring FTD
	peer FTD
	address 1.1.1.1
	pre-share local cisco123
	pre-share remote cisco123

crypto ikev2 profile PROFILE
	match identity remote address 1.1.1.1 255.255.255.255
	authentication local pre-share
	authentication remote pre-share
	keyring local FTD

crypto ipsec transform-set TS esp-aes esp-sha-hmac

access-list 102 permit ip 10.20.20.0 0.0.0.255 10.20.10.0 0.0.0.255

crypto map CMAP 10 ipsec-isakmp
	set peer 1.1.1.1
	set transform-set TS
	match address 102
	
int e0/0
	crypto map CMAP
	
```

