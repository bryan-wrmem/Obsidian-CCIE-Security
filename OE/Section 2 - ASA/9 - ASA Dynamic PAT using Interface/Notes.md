[Open: Pasted image 20260107142103.png](../../../Media/3c49bb9ed78d4969b5f63bc7b36a7582_MD5.jpeg)
![](../../../Media/3c49bb9ed78d4969b5f63bc7b36a7582_MD5.jpeg)

Dynamic PAT 10.20.40.0 subnet to ASA outside interface

Create network object for 10.20.40.0

```
object network INTNET_10.20.40.0
	subnet 10.20.40.0 255.255.255.0
	nat (inside,outside) dynamic 
```
