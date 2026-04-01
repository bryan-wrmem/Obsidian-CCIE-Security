[Open: Pasted image 20260331200217.png](../../../Media/af2c55a593f1806db25b52df8552390e_MD5.jpeg)
![](../../../Media/af2c55a593f1806db25b52df8552390e_MD5.jpeg)

[Open: Pasted image 20260331202304.png](../../../Media/da66aefa6f371759c0af99259860462f_MD5.jpeg)
![](../../../Media/da66aefa6f371759c0af99259860462f_MD5.jpeg)

[Open: Pasted image 20260331202331.png](../../../Media/9e9cd06978471e064b3d641fd417caeb_MD5.jpeg)
![](../../../Media/9e9cd06978471e064b3d641fd417caeb_MD5.jpeg)

[Open: Pasted image 20260331204532.png](../../../Media/318839974270cc941c26be9c0e61e63e_MD5.jpeg)
![](../../../Media/318839974270cc941c26be9c0e61e63e_MD5.jpeg)

[Open: Pasted image 20260331204547.png](../../../Media/459ef1a1020d4af63ed8a24ac3032b50_MD5.jpeg)
![](../../../Media/459ef1a1020d4af63ed8a24ac3032b50_MD5.jpeg)

[Open: Pasted image 20260331205109.png](../../../Media/81f0531eede34c886567fb1f569d3644_MD5.jpeg)
![](../../../Media/81f0531eede34c886567fb1f569d3644_MD5.jpeg)

[Open: Pasted image 20260331205119.png](../../../Media/442058ce371cf6eff59c79de317228e5_MD5.jpeg)
![](../../../Media/442058ce371cf6eff59c79de317228e5_MD5.jpeg)

show failover

```
Failover On 
Failover unit Primary
Failover LAN Interface: HA GigabitEthernet0/2 (up)
Reconnect timeout 0:00:00
Unit Poll frequency 1 seconds, holdtime 15 seconds
Interface Poll frequency 5 seconds, holdtime 25 seconds
Interface Policy 1
Monitored Interfaces 3 of 311 maximum
MAC Address Move Notification Interval not set
failover replication http
Version: Ours 9.18(2)200, Mate 9.18(2)200
Serial Number: Ours 9A6ALUTW82P, Mate 9AF7V9Q4R3J
Last Failover at: 00:46:49 UTC Apr 1 2026
	This host: Primary - Active 
		Active time: 635 (sec)
		slot 0: ASAv hw/sw rev (/9.18(2)200) status (Up Sys)
		  Interface diagnostic (0.0.0.0): Normal (Waiting)
		  Interface outside (172.16.10.1): Normal (Monitored)
		  Interface inside (10.10.10.1): Normal (Monitored)
		slot 1: snort rev (1.0)  status (up)
		slot 2: diskstatus rev (1.0)  status (up)
	Other host: Secondary - Standby Ready 
		Active time: 0 (sec)
		  Interface diagnostic (0.0.0.0): Normal (Waiting)
		  Interface outside (172.16.10.2): Normal (Monitored)
		  Interface inside (10.10.10.2): Normal (Monitored)
		slot 1: snort rev (1.0)  status (up)
		slot 2: diskstatus rev (1.0)  status (up)

Stateful Failover Logical Update Statistics
	Link : HA GigabitEthernet0/2 (up)
	Stateful Obj 	xmit       xerr       rcv        rerr      
	General		79         0          74         0         
	sys cmd  	74         0          74         0         
	up time  	0          0          0          0         
	RPC services  	0          0          0          0         
	TCP conn 	0          0          0          0         
	UDP conn 	0          0          0          0         
	ARP tbl  	4          0          0          0         
	Xlate_Timeout  	0          0          0          0         
	IPv6 ND tbl  	0          0          0          0         
	VPN IKEv1 SA 	0          0          0          0         
	VPN IKEv1 P2 	0          0          0          0         
	VPN IKEv2 SA 	0          0          0          0         
	VPN IKEv2 P2 	0          0          0          0         
	VPN CTCP upd 	0          0          0          0         
	VPN SDI upd 	0          0          0          0         
	VPN DHCP upd 	0          0          0          0         
	SIP Session 	0          0          0          0         
	SIP Tx 	0          0          0          0         
	SIP Pinhole 	0          0          0          0         
	Route Session 	0          0          0          0         
	Router ID 	0          0          0          0         
	User-Identity 	1          0          0          0         
	CTS SGTNAME 	0          0          0          0         
	CTS PAC 	0          0          0          0         
	TrustSec-SXP 	0          0          0          0         
	IPv6 Route 	0          0          0          0         
	STS Table 	0          0          0          0         
	Umbrella Device-ID 	0          0          0          0         
	Rule DB B-Sync 	0          0          0          0         
	Rule DB P-Sync 	0          0          0          0         
	Rule DB Delete 	0          0          0          0         

	Logical Update Queue Information
	 	 	Cur 	Max 	Total
	Recv Q: 	0 	11 	74
	Xmit Q: 	0 	11 	394

```