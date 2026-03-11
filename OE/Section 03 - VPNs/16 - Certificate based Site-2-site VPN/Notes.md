[Open: Pasted image 20260311134842.png](../../../Media/270913457de65eafcc70e8f12a420f06_MD5.jpeg)
![](../../../Media/270913457de65eafcc70e8f12a420f06_MD5.jpeg)

Certificate as an alternative to pre-shared keys. Have certificates issued from CA-Server Router

Baseline Config

```
SP

en
conf t

hostname SP
no ip domain-lookup

int e0/3
ip address 5.5.5.1 255.255.255.0
no shut

int e1/0
ip address 1.1.1.1 255.255.255.0
no shut

int e0/2
ip address 2.2.2.1 255.255.255.0
no shut

int e0/0
ip address 3.3.3.1 255.255.255.0
no shut

int e0/1
ip address 4.4.4.1 255.255.255.0
no shut

router eigrp 1
	network 5.5.5.0 255.255.255.0
	network 1.1.1.0 255.255.255.0
	network 2.2.2.0 255.255.255.0
	network 3.3.3.0 255.255.255.0
	network 4.4.4.0 255.255.255.0

end
wr

==============

Tokyo

en
conf t

hostname Tokyo
no ip domain-lookup

int e0/0
ip address 1.1.1.2 255.255.255.0
no shut

int lo1
ip address 172.16.1.1 255.255.255.0
no shut

int lo2
ip address 172.16.2.1 255.255.255.0
no shut

ip route 0.0.0.0 0.0.0.0 1.1.1.1


router eigrp 1
	network 172.16.1.0 255.255.255.0
	network 172.16.2.0 255.255.255.0
	network 1.1.1.0 255.255.255.0

end
wr

================

Riyadh


en
conf t

hostname Riyadh
no ip domain-lookup

int e0/0
ip address 2.2.2.2 255.255.255.0
no shut

int lo1
ip address 172.16.3.1 255.255.255.0
no shut

int lo2
ip address 172.16.4.1 255.255.255.0
no shut

ip route 0.0.0.0 0.0.0.0 2.2.2.1

router eigrp 1
	network 172.16.3.0 255.255.255.0
	network 172.16.4.0 255.255.255.0
	network 2.2.2.0 255.255.255.0

end
wr

==============

Melbourne


en
conf t

hostname Melbourne
no ip domain-lookup

int e0/0
ip address 3.3.3.2 255.255.255.0
no shut

int lo1
ip address 172.16.5.1 255.255.255.0
no shut

int lo2
ip address 172.16.6.1 255.255.255.0
no shut

ip route 0.0.0.0 0.0.0.0 3.3.3.1

router eigrp 1
	network 172.16.5.0 255.255.255.0
	network 172.16.6.0 255.255.255.0
	network 3.3.3.0 255.255.255.0

end
wr

==============

Perth


en
conf t

hostname Perth
no ip domain-lookup

int e0/0
ip address 4.4.4.2 255.255.255.0
no shut

int lo1
ip address 172.16.7.1 255.255.255.0
no shut

int lo2
ip address 172.16.8.1 255.255.255.0
no shut

ip route 0.0.0.0 0.0.0.0 4.4.4.1

router eigrp 1
	network 172.16.7.0 255.255.255.0
	network 172.16.8.0 255.255.255.0
	network 4.4.4.0 255.255.255.0

end
wr

==============

CA Server


en
conf t

hostname CA-Server
no ip domain-lookup

int e0/0
ip address 5.5.5.2 255.255.255.0
no shut


ip route 0.0.0.0 0.0.0.0 1.1.1.1

router eigrp 1
	network 5.5.5.0 255.255.255.0


end
wr

```

CA Server Config

```
crypto key generate rsa modulu 2048 label Trust-CA

crypto pki server Trust-CA
	issuer-name CN=cisco L=NewZealand C=NZ
	no shut
	# Enter Password moshin123
	
CA-Server#show crypto
*Mar 11 18:05:36.936: %SYS-5-CONFIG_I: Configured from console by console
CA-Server#show crypto pki server
Certificate Server Trust-CA:
    Status: disabled, HTTP Server is disabled
    State: check failed
    Server's configuration is locked  (enter "shut" to unlock it)
    Issuer name: CN=cisco L=NewZealand C=NZ
    CA cert fingerprint: 8C2EA580 AD3B0A93 7649299A 14D6E7CF 
    Granting mode is: manual
    Last certificate issued serial number (hex): 1
    CA certificate expiration timer: 18:05:13 UTC Mar 10 2029
    CRL NextUpdate timer: 00:05:13 UTC Mar 12 2026
    Current primary storage dir: nvram:
    Database Level: Minimum - no cert data written to storage
CA-Server#
```

Tokyo Config

```
ip domain-name tokyo.xyz.com

crypto key generate rsa modulus 2024

crypto pki trustpoint SITES
	enrollment url http://5.5.52
	revocation-check none
	
crypto pki authenticate SITES
	# Yes
	
crypto pki enroll SITES
	# Password
```