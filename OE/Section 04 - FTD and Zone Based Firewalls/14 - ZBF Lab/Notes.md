[Open: Pasted image 20260401102518.png](../../../Media/18a699aba00cbb0651e53e9a2468e570_MD5.jpeg)
![](../../../Media/18a699aba00cbb0651e53e9a2468e570_MD5.jpeg)

```

!
class-map type inspect match-any outside-to-dmz
 match access-group 100
class-map type inspect match-any inside-to-outside
 match protocol http
 match protocol telnet
 match protocol icmp
class-map type inspect match-any inside-to-dmz
 match protocol http
 match protocol telnet
 match protocol icmp
!
policy-map type inspect policy-outside-to-dmz
 class type inspect outside-to-dmz
  inspect 
 class class-default
  drop
policy-map type inspect policy-inside-to-dmz
 class type inspect inside-to-dmz
  inspect 
 class class-default
  drop
policy-map type inspect policy-inside-to-outside
 class type inspect inside-to-outside
  inspect 
 class class-default
  drop
!
zone security outside
zone security inside
zone security dmz
zone-pair security inside-outside source inside destination outside
 service-policy type inspect policy-inside-to-outside
zone-pair security inside-dmz source inside destination dmz
 service-policy type inspect policy-inside-to-dmz
zone-pair security outside-dmz source outside destination dmz
 service-policy type inspect policy-outside-to-dmz
! 
!
!
interface Ethernet0/0
 ip address 172.16.1.1 255.255.255.0
 zone-member security inside
 duplex auto
!
interface Ethernet0/1
 ip address 1.1.1.1 255.255.255.0
 zone-member security outside
 duplex auto
!
interface Ethernet0/2
 ip address 172.16.2.1 255.255.255.0
 zone-member security dmz
 duplex auto
!
interface Ethernet0/3
 ip address 172.16.3.1 255.255.255.0
 zone-member security dmz
 duplex auto
!
!
access-list 100 permit tcp any host 172.16.2.2 eq telnet
access-list 100 permit icmp any host 172.16.2.2 echo
access-list 100 permit icmp any host 172.16.2.2 echo-reply
access-list 100 permit tcp any host 172.16.3.2 eq www
access-list 100 permit icmp any host 172.16.3.2 echo
access-list 100 permit icmp any host 172.16.3.2 echo-reply
!
```