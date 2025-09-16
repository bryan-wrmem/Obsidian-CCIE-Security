### NAT Types

NAT Types
	Dynamic NAT (aka object nat, auto nat)
	Static NAT
	Dynamic PAT
	Static PAT
	Destination NAT
	Manual NAT / Twice NAT

In dynamic NAT / PAT it does not allow traffic to come from outside to inside (static can)

If internal IP is getting translated it's "source nat"

Check state / connection entry then NAT then ACLs. 

## Dynamic NAT
many to many
can use pool of ip's
ex inside to outside 
internal devices typically not aware
can be translated both directions
packet return - asa checks the nat table 
