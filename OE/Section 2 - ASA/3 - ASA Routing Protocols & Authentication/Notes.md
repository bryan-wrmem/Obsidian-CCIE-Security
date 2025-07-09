OSPF Configuration and Auth

4 OSPF Auth types supported

0 - Null
1 -  Plain Text
2 - md5
3 - SHA

ASA Features

OSPF auth defined under router ospf process, or directly on interface
OSPF key only defined under interface
If auth defined in both the process and interface, interface takes priority
Can't define passive interface
support of intra-area, inter-area, and external (I, II types) routes
Supports virtual link
ospf lsa flooding
auth ospf packets
asa can be DR, DBR, ABR
Support stub and not-so-stubby areas
Area boundary router type 3 lsa filtering