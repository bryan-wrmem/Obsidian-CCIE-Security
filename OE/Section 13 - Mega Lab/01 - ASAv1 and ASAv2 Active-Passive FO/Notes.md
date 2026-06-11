[Open: Pasted image 20260610195741.png](../../../Media/4aa6ba61b87e8ff7f6a47e09802c9399_MD5.png)
![](../../../Media/4aa6ba61b87e8ff7f6a47e09802c9399_MD5.png)

Config Scratch

```
ASAv1

int gi0/2
  nameif inside
  ip address 10.10.30.1 255.255.255.0
  no shut
  
int gi0/3
  name if outside
  ip address 100.100.40.1 255.255.255.0
  no shut
  

```