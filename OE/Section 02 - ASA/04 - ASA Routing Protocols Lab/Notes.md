# OSPF
## ASA Inside
gi0/1

router ospf 1
router-id 0.0.0.200
network 10.10.10.0 255.255.255.0 area 0

## R1
e0/0

router ospf 1
router-id 0.0.0.100
network 10.10.10.0 0.0.0.255 area 0
network 10.20.10.0 0.0.0.255 area 0
network 10.20.20.0 0.0.0.255 area 0

interface configs:
ip ospf network point-to-point

authentication:
int e0/0
ip ospf authentication message-digest
ip ospf message-digest-key 200 md5 test123

# BGP
## ASA Outside
gi0/0

router bgp 65530
address-family ipv4 unicast
neighbor 192.168.10.2 remote-as 65534
neighbor 192.168.10.2 activate

redistribute:
redistribute ospf
redistribute eigrp

## Service Provider
router bgp 65534
neighbor 192.168.10.1 remote-as 65530
network 1.1.1.0 255.255.255.252

authentication:
router bgp 65534
neighbor 192.168.10.1 password test123
# EIGRP
## ASA DMZ
gi0/2

router eigrp 1
network 172.16.1.0 255.255.255.0

int gi0/2
authentication mode eigrp 1
authentication key eigrp 1 test123 key-id 189

## r3
e0/0

router eigrp 1
network 172.16.1.0 255.255.255.0
network 172.17.30.0 255.255.255.0
network 172.17.31.0 255.255.255.0

authentication w/ key chain:
key chain EIGRP
key 189
key-string test123

int e0/0
ip authentication mode eigrp 1 md5 
ip authentication key-chain eigrp 1 EIGRP

