[Open: Pasted image 20260108143803.png](../../../Media/83db7e07983b058c477c812c5a535cf9_MD5.jpeg)
![](../../../Media/83db7e07983b058c477c812c5a535cf9_MD5.jpeg)

Static NAT Lab

Bi-directional NAT

NAT Accounting server 172.17.30.1 to 192.1.1.70
NAT Salesforce Server 172.17.31.1 to 192.1.1.71

Create objects and NAT Config

```
network object Accountingserver
	host 172.17.30.1
	nat (dmz,outside) static 192.1.1.70
	
network object Salesforceserver
	host 172.17.31.1
	nat (dmz,outside) static 192.1.1.71
```