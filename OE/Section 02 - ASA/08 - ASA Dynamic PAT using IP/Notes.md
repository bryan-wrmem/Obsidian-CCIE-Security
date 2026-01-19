[Open: Pasted image 20260107140308.png](3c49bb9ed78d4969b5f63bc7b36a7582_MD5.jpeg)
![](3c49bb9ed78d4969b5f63bc7b36a7582_MD5.jpeg)

Dynamic PAT traffic from 10.20.30.0/24 using the following IP: 192.1.1.21

Create PAT pool and object for 10.20.30.0 network

```
object network ISPPOOL_DynamicPAT
	host 192.1.1.21

object network INTNET_10.20.30.0
	subnet 10.20.30.0 255.255.255.0
	nat (inside,outside) dynamic ISPPOOL_DynamicPAT
```

