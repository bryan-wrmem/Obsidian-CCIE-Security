[Open: Pasted image 20260319142910.png](../../../Media/56bd3d89b310c4cb9993d2f41b7bd4da_MD5.jpeg)
![](../../../Media/56bd3d89b310c4cb9993d2f41b7bd4da_MD5.jpeg)

S2S tunnel between R6/R4 passing through ASA

Phase 1

```
crypto ipsakmp policy 10
	auth pre-share
	hash md5
	enc 3des
	group 2
	
crypto 
```