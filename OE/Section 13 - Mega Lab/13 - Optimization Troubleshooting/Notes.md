Will get a few optimization/troubleshooting questions. Typically easier in nature.

R40
```
class-map type inspect match-any outside-to-inside
 match protocol icmp
!
policy-map type inspect policy-outside-to-inside
 class type inspect outside-to-inside
  inspect
 class class-default
  drop
!
zone security OUTSIDE
zone security INSIDE
zone-pair security outside-inside source OUTSIDE destination INSIDE
 service-policy type inspect policy-outside-to-inside

interface Ethernet0/0
 no shutdown
 ip address 192.168.0.44 255.255.255.0
 zone-member security OUTSIDE
!
interface Ethernet0/1
 no shutdown
 ip address 172.16.60.254 255.255.255.0
 zone-member security INSIDE
```

