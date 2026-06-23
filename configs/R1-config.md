Current configuration : 1762 bytes
!
! No configuration change since last restart
version 15.1
service timestamps debug datetime msec
service timestamps log datetime msec
no service password-encryption
!
hostname R1
!
boot-start-marker
boot-end-marker
!
!
enable secret 5 $
!
no aaa new-model
ip source-route
!
!
!
ip dhcp excluded-address 192.168.10.1
ip dhcp excluded-address 192.168.20.1
ip dhcp excluded-address 192.168.30.1 192.168.30.20
!
ip dhcp pool VLAN10
 network 192.168.10.0 255.255.255.0
 default-router 192.168.10.1
!
ip dhcp pool VLAN20
 network 192.168.20.0 255.255.255.0
 default-router 192.168.20.1
!
ip dhcp pool VLAN30
 network 192.168.30.0 255.255.255.0
 default-router 192.168.30.1
!
!
ip cef
ip domain name lab.local
multilink bundle-name authenticated
!
!
license udi pid CISCO1841 sn FHK10511441
username admin privilege 15 secret 5 $1$TMr/$tXc8UqQbGwxpZNN1zpfcp/
!
!
!
!
!
!
interface FastEthernet0/0
 no ip address
 duplex auto
 speed auto
!
interface FastEthernet0/0.10
 encapsulation dot1Q 10
 ip address 192.168.10.1 255.255.255.0
!
interface FastEthernet0/0.20
 encapsulation dot1Q 20
 ip address 192.168.20.1 255.255.255.0
!
interface FastEthernet0/0.30
 encapsulation dot1Q 30
 ip address 192.168.30.1 255.255.255.0
!
interface FastEthernet0/0.99
 encapsulation dot1Q 99 native
!
interface FastEthernet0/1
 no ip address
 shutdown
 duplex auto
 speed auto
!
interface Serial0/1/0
 no ip address
 shutdown
 no fair-queue
 clock rate 2000000
!
ip forward-protocol nd
!
!
no ip http server
!
!
!
control-plane
!
!
!
line con 0
 logging synchronous
line aux 0
line vty 0 4
 exec-timeout 15 0
 login local
 transport input telnet
line vty 5 15
 exec-timeout 15 0
 login local
 transport input telnet
!
scheduler allocate 20000 1000
end
