![image](https://github.com/user-attachments/assets/ef7eedac-8aff-476f-9a52-a5f723de2ec3)
# CAU HINH DIA CHI IP
### R1
```
ena
conf ter
int s0/0
ip address 10.1.1.1 255.255.255.252
no shut
int s0/1
ip address 10.2.2.2 255.255.255.252
no shut
exit
```
### R2
```
ena
conf ter
int s0/0
ip address 10.1.1.2 255.255.255.252
no shut
int f0/1
ip address 209.165.200.225 255.255.255.248
no shut
exit
```
### R3
```
ena
conf ter
int s0/0
ip address 10.2.2.1 255.255.255.252
no shut
int f0/0
ip address 172.168.3.1 255.255.255.0
no shut
exit
```
# CAU HINH DINH TUYEN DONG OSPF
### R1
```
conf t
router ospf 1
network 10.1.1.0 0.0.0.3 area 0
network 10.2.2.0 0.0.0.3 area 0
network 209.165.200.224 0.0.0.7 area 0
end
```
### R2
```
conf t
router ospf 1
network 10.1.1.0 0.0.0.3 area 0
network 209.165.200.224 0.0.0.7 area 0
network 192.168.2.0 0.0.0.255 area 0
end
```
### R3
```
conf t
router ospf 1
network 10.2.2.0 0.0.0.3 area 0
network 172.16.3.0 0.0.0.255 area 0
end
```
## KIEM TRA LAI OSPF
```
show ip ospf neighbor
show ip route ospf
```
