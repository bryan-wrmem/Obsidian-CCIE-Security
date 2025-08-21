# OSPF
ASA Inside
gi0/1

router ospf 1
router-id 0.0.0.200
network 10.10.10.0 255.255.255.0 area 0

R1
e0/0

router ospf 1
router-id 0.0.0.100
network 10.10.10.0 0.0.0.255 area 0
network 10.20.10.0 0.0.0.255 area 0
network 10.20.20.0 0.0.0.255 area 0

interface configs:
ip ospf network point-to-point

# BGP
ASA Outside
gi0/0


# EIGRP
ASA DMZ
gi0/2

