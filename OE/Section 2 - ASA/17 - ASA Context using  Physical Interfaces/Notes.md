[Open: Pasted image 20260116191543.png](../../../Media/5d03e0bcfbe3f8c908d4aa818aa59572_MD5.jpeg)
![](../../../Media/5d03e0bcfbe3f8c908d4aa818aa59572_MD5.jpeg)



# Lab

[Open: Pasted image 20260116192207.png](../../../Media/43ff136ca66bf5d73901bc9f1f889359_MD5.jpeg)
![](../../../Media/43ff136ca66bf5d73901bc9f1f889359_MD5.jpeg)

```
# verify mode asa is in

show mode

# change to multiple context mode, note: this will wipe all configs and reboot the asa

mode multiple

# define contexts, allocate interfaces, and initialize the contects with the config-url command

context company1
allocate interface company1 e0
allocate interface company1 e1
config-url disk0:/company1.cfg

context copmany2
allocate interface company2 e2
allocate interface copmany2 e3
config-url disk0:/company2.cfg

# switch contexts with the changeto command

changeto context company1


```