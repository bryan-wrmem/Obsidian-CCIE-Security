[Open: Pasted image 20260120182322.png](../../../Media/09aad7209d4e8b46b43ff970a9d0bd35_MD5.jpeg)
![](../../../Media/09aad7209d4e8b46b43ff970a9d0bd35_MD5.jpeg)

Need dedicated link for clustering. Exam - will usually present spanned mode asas
Connect to switch with port-channel
# Lab

[Open: Pasted image 20260120182456.png](../../../Media/428057f0e818cec2ebe17f00713f9429_MD5.jpeg)
![](../../../Media/428057f0e818cec2ebe17f00713f9429_MD5.jpeg)

Cluster config

```
# check cluster status

show cluster info

# check if interfaces are in span or individual interface mode

show cluster interface-mode

# configure asa to be in cluster interface span mode

cluster interface-mode spanned

# configure cluster group, name the local unit, and assign cluster interface

cluster group LAB
local-unit ASA2
cluster-interface e0 ip 192.168.1.1 255.255.255.0
key cisco123
# lower priority is preffered
priority 5
enable

# repeat commands for other ASA

cluster interface-mode spanned
cluster group LAB
local-unit ASA2
cluster-interface e0 ip 192.168.1.2 255.255.255.0
key cisco123
priority 10
enable

# configure interfaces

int eth1
	channel-group 1
	
int po1
	

```