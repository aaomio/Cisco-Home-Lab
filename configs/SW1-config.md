Current configuration : 3655 bytes
!
version 12.2
no service pad
service timestamps debug uptime
service timestamps log uptime
no service password-encryption
!
hostname SW1
!
enable secret 5 $
!
username admin privilege 15 secret 5 $
no aaa new-model
system mtu routing 1500
ip subnet-zero
ip domain-name lab.local
!
!
!
!
no file verify auto
!
spanning-tree mode pvst
spanning-tree extend system-id
spanning-tree vlan 10,20,30 priority 24576
!
vlan internal allocation policy ascending
!
!
interface Port-channel1
 switchport trunk encapsulation dot1q
 switchport trunk native vlan 99
 switchport trunk allowed vlan 10,20,30,40,50,99
 switchport mode trunk
!
interface FastEthernet0/1
 switchport access vlan 10
 switchport mode access
 spanning-tree portfast
 spanning-tree bpduguard enable
!
interface FastEthernet0/2
 switchport access vlan 10
 switchport mode access
 spanning-tree portfast
 spanning-tree bpduguard enable
!
interface FastEthernet0/3
 switchport access vlan 10
 switchport mode access
 spanning-tree portfast
 spanning-tree bpduguard enable
!
interface FastEthernet0/4
 switchport access vlan 10
 switchport mode access
 spanning-tree portfast
 spanning-tree bpduguard enable
!
interface FastEthernet0/5
 switchport access vlan 10
 switchport mode access
 spanning-tree portfast
 spanning-tree bpduguard enable
!
interface FastEthernet0/6
 switchport access vlan 10
 switchport mode access
 spanning-tree portfast
 spanning-tree bpduguard enable
!
interface FastEthernet0/7
 switchport access vlan 10
 switchport mode access
 spanning-tree portfast
 spanning-tree bpduguard enable
!
interface FastEthernet0/8
 switchport access vlan 10
 switchport mode access
 spanning-tree portfast
 spanning-tree bpduguard enable
!
interface FastEthernet0/9
 switchport access vlan 10
 switchport mode access
 spanning-tree portfast
 spanning-tree bpduguard enable
!
interface FastEthernet0/10
 switchport trunk encapsulation dot1q
 switchport trunk native vlan 99
 switchport trunk allowed vlan 10,20,30,40,50,99
 switchport mode trunk
 channel-group 1 mode active
!
interface FastEthernet0/11
 description TO-R1
 switchport trunk encapsulation dot1q
 switchport trunk native vlan 99
 switchport trunk allowed vlan 10,20,30,40,50,99
 switchport mode trunk
!
interface FastEthernet0/12
 switchport trunk encapsulation dot1q
 switchport trunk native vlan 99
 switchport trunk allowed vlan 10,20,30,40,50,99
 switchport mode trunk
 channel-group 1 mode active
!
interface FastEthernet0/13
 description UNUSED
 shutdown
!
interface FastEthernet0/14
 description UNUSED
 shutdown
!
interface FastEthernet0/15
 description UNUSED
 shutdown
!
interface FastEthernet0/16
 description UNUSED
 shutdown
!
interface FastEthernet0/17
 description UNUSED
 shutdown
!
interface FastEthernet0/18
 description UNUSED
 shutdown
!
interface FastEthernet0/19
 description UNUSED
 shutdown
!
interface FastEthernet0/20
 description UNUSED
 shutdown
!
interface FastEthernet0/21
 description UNUSED
 shutdown
!
interface FastEthernet0/22
 description UNUSED
 shutdown
!
interface FastEthernet0/23
 description UNUSED
 shutdown
!
interface FastEthernet0/24
 description UNUSED
 shutdown
!
interface GigabitEthernet0/1
!
interface GigabitEthernet0/2
!
interface Vlan1
 no ip address
 shutdown
!
interface Vlan10
 no ip address
!
interface Vlan20
 no ip address
!
interface Vlan30
 ip address 192.168.30.11 255.255.255.0
!
ip default-gateway 192.168.30.1
ip classless
ip http server
!
!
!
control-plane
!
!
line con 0
 logging synchronous
line vty 0 4
 login local
 transport input telnet
line vty 5 15
 login local
 transport input telnet
!
end

