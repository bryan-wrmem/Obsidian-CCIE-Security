VLAN access control lists (VACLs) or VLAN maps are used to control network traffic within a VLAN. VACLs are configured globally, and the rules are applied on VLANs. VACLs are supported in both ingress and egress directions. In ingress direction VACLs are applied after Port ACL and before Routed ACL. In egress direction VACLs are applied after Routed ACL and before Port ACL. VLAN map is applied to both routed and switched traffic. VLAN map can contain both IP and MAC ACLs to be applied to IP and non-IP traffic respectively.

```

# Create acl to match icmp and udp 53

access-list 102 permit icmp any any
access-list 102 permit udp any any eq 53

# Creat access map to match traffic and define an action (similiar to a route-map)

vlan access-map XYZ 10
	match ip address 102
	action drop
vlan access-map XYZ 20
	action forward
	
# Apply vlan filter to list of vlans

vlan filter XYZ vlan-list 10
```