# ASA

## **Types of Firewalls**  
Proxy Firewall  

Bastion Host (Reverse Proxy)  

NGFW (Next Generation Firewall)  
- intrusion protection  
- application awareness  
- threat intelligence  
- telemetry  

UTM (Unified Threat Management)  
- single security appliance  
- multi functionality, single point in network  

Zone Based Firewalls  

Security Level Firewalls  

Stateless Firewalls  
- Legacy  
- Not aware of traffic patterns  

Stateful Firewalls  
- Introduced by checkpoint 1994  
- monitors active connections  
- inspection tables or state table  

## **ASA Firewall Overview and Architecture**  
Stateful firewall with vpn capabilities  
Based on linux  
Linkable format program - LINA  

### Features  
  
![[Pasted image 20250402230046.png]]

---

**Exam Note**  
Command: Nameif  
- not case sensitive, but preserve the case on exam  

---

ASA ACLs - normal mask, not inverse  
1 ACL per interface, per direction  

**Through Traffic**  
High Security Level to Low Security Level  
- All TCP/UDP allowed from H 2 L  
- show connection - stateful inspection entries  
Low to High  
- Blocked by default  
- Need to explicitly allow  
- Packet flow - check conn table first -> ACL -> Default Behavior  
Same Security Level  
- S 2 S - blocked, even with explicit ACL  
- same-security-traffic permit inter-interface  
 
## **Remote Management**  
Telnet  
- Cannot be configured on security level 0 interface  
- enabled on interface, with allowed IPs  
- need password  
- config:
		
		telnet 10.1.1.1 255.255.255.255 inside
		password C1sco123
		
SSH
- any interface
- enabled on interface with allowed ip
- requires RSA key
- requires username/password - LOCAL or AAA
- config:
	
		ssh 10.1.1.1 255.255.255.255 inside
		
ASDM
- config:
	
		http server enable
		http 0.0.0.0 0.0.0.0 mgmt
		username cisco password C1sco privilege 15
		aaa authentication http console LOCAL
	