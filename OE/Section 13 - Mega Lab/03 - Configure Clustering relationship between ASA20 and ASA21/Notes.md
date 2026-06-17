```
# check cluster status

show cluster info

# check if interfaces are in span or individual interface mode

show cluster interface-mode

# configure asa to be in cluster interface span mode

cluster interface-mode spanned

# configure cluster group, name the local unit, and assign cluster interface

cluster group Cisco
local-unit ASA20
cluster-interface e0 ip 11.11.11.1 255.255.255.0
key C1sC0123!
# lower priority is preffered
priority 5
enable

# repeat commands for other ASA

cluster interface-mode spanned
cluster group Cisco
local-unit ASA21
cluster-interface e0 ip 11.11.11.2 255.255.255.0
key C1sC0123!
priority 10
enable

# configure interfaces

int eth1
   channel-group 1 mode active
   no shut
   
int po1
   port-channel span-cluster
   nameif inside
   ip address 10.10.10.1 255.255.255.0
   
int eth2
   channel-group 2 mode active
   no shut
   
int po2
   port-channel span-cluster
   nameif outside
   ip address 100.100.100.1 255.255.255.0


```
