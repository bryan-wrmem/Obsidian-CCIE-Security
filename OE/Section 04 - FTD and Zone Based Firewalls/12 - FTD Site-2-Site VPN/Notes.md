[Open: Pasted image 20260401092106.png](../../../Media/c92bff8044b289a34d23c22393da710f_MD5.jpeg)
![](../../../Media/c92bff8044b289a34d23c22393da710f_MD5.jpeg)

IKEv2 S2S

Firepower Config

[Open: Pasted image 20260401094228.png](../../../Media/62494ebe7e9cca4108538dd8eddc704c_MD5.jpeg)
![](../../../Media/62494ebe7e9cca4108538dd8eddc704c_MD5.jpeg)

[Open: Pasted image 20260401094344.png](../../../Media/031e0f4b79160e97b665143197a970f5_MD5.jpeg)
![](../../../Media/031e0f4b79160e97b665143197a970f5_MD5.jpeg)

[Open: Pasted image 20260401094355.png](../../../Media/f1a387b77731d6762110b79acb6ce900_MD5.jpeg)
![](../../../Media/f1a387b77731d6762110b79acb6ce900_MD5.jpeg)

[Open: Pasted image 20260401094429.png](../../../Media/847c28e32859e4c14de7cb2f123359bd_MD5.jpeg)
![](../../../Media/847c28e32859e4c14de7cb2f123359bd_MD5.jpeg)


[Open: Pasted image 20260401094452.png](../../../Media/9eb1f3a235703b5a3f3c911668dc4323_MD5.jpeg)
![](../../../Media/9eb1f3a235703b5a3f3c911668dc4323_MD5.jpeg)

R4 Config

```
# Create IKEV2 Proposal

crypto ikev2 proposal FTD-Proposal
	encryption aes-cbc-128
	integrity sha1
	group 14
	prf sha1
	
# Create key ring

crypto ikev2 keyring FTD-Key
	Peer FTD
		address 1.1.1.1
		pre-shared-key local cisco123
		pre-shared-key remote cisco123

# Create IKEv2 Policy

crypto ikev2 policy FTD
	crypto ikev2 proposal FTD-Proposal

# Create IKEv2 Profile

crypto ikev2 profile FTD-Profile
	match identity remote address 1.1.1.1 255.255.255.255
	authentication local pre-share
	authentication remote pre-share
	keyring local FTD-Key

crypto ipsec transform-set TS esp-aes esp-sha-hmac
	
access-list 102 permit ip 172.16.2.0 0.0.0.255 172.16.1.0 0.0.255.255

crypto map CMAP 10 ipsec-isakmp
	set peer 1.1.1.1
	set transform-set TS
	match address 102
	set ikev2-profile FTD-Profile

int e0/0
	crypto map CMAP


```