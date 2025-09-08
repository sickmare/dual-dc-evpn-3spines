# Site2-L3 Commands Output

## Table of Contents

- [show lldp neighbors](#show-lldp-neighbors)
- [show ip interface brief](#show-ip-interface-brief)
- [show interfaces description](#show-interfaces-description)
- [show version](#show-version)
- [show running-config](#show-running-config)
## show interfaces description

```
Interface                      Status         Protocol           Description
Et1                            up             up                 SERVER_Site2-L3=Site2-L4=vPC1_NIC1
Et2                            up             up                 SERVER_Site2-L3=Site2-L4=vPC2_NIC1
Et3                            up             up                 test eth3 routed port
Et4                            up             up                 
Et5                            up             up                 
Et6                            up             up                 
Et7                            up             up                 
Et8                            up             up                 
Et9                            up             up                 
Et10                           up             up                 
Et11                           up             up                 
Et12                           up             up                 
Et13                           up             up                 
Et14                           up             up                 
Et15                           up             up                 
Et16                           up             up                 
Et17                           up             up                 
Et18                           up             up                 
Et19                           up             up                 
Et20                           up             up                 
Et21                           up             up                 
Et22                           up             up                 
Et23                           up             up                 
Et24                           up             up                 
Et25                           up             up                 
Et26                           up             up                 
Et27                           up             up                 
Et28                           up             up                 
Et29                           up             up                 
Et30                           up             up                 
Et31                           up             up                 
Et32                           up             up                 
Et33                           up             up                 
Et34                           up             up                 
Et35                           up             up                 
Et36                           up             up                 
Et37                           up             up                 
Et38                           up             up                 
Et39                           up             up                 
Et40                           up             up                 
Et41                           up             up                 
Et42                           up             up                 
Et43                           up             up                 
Et44                           up             up                 
Et45                           up             up                 
Et46                           up             up                 
Et47                           up             up                 
Et48                           up             up                 
Et49/1                         up             up                 MLAG_Site2-L4_Ethernet49/1
Et50/1                         up             up                 MLAG_Site2-L4_Ethernet50/1
Et51/1                         up             up                 P2P_Site2-S1_Ethernet3/1
Et52/1                         up             up                 P2P_Site2-S2_Ethernet3/1
Et53/1                         up             up                 P2P_Site2-S3_Ethernet3/1
Et54/1                         up             up                 
Et55/1                         up             up                 
Et56/1                         up             up                 
Lo0                            up             up                 ROUTER_ID
Lo1                            up             up                 VXLAN_TUNNEL_SOURCE
Lo100                          up             up                 DIAG_VRF_bluevrf
Ma1                            up             up                 OOB_MANAGEMENT
Po1                            down           lowerlayerdown     PortChannel
Po2                            down           lowerlayerdown     PortChannel
Po491                          up             up                 MLAG_Site2-L4_Port-Channel491
Vl2300                         up             up                 bluenet1
Vl2301                         up             up                 bluenet2
Vl3009                         up             up                 MLAG_L3_VRF_bluevrf
Vl4093                         up             up                 MLAG_L3
Vl4094                         up             up                 MLAG
Vl4097                         up             up                 
Vx1                            up             up                 Site2-L3_VTEP
```
## show ip interface brief

```
Address
Interface       IP Address            Status     Protocol         MTU   Owner  
--------------- --------------------- ---------- ------------ --------- -------
Ethernet51/1    172.32.255.133/31     up         up              9000          
Ethernet52/1    172.32.255.135/31     up         up              9000          
Ethernet53/1    172.32.255.137/31     up         up              9000          
Loopback0       192.2.255.25/32       up         up             65535          
Loopback1       192.2.254.25/32       up         up             65535          
Loopback100     10.255.1.25/32        up         up             65535          
Management1     192.168.0.25/24       up         up              1500          
Vlan2300        192.168.11.1/24       up         up              1500          
Vlan2301        192.168.12.1/24       up         up              1500          
Vlan3009        10.222.251.44/31      up         up              9000          
Vlan4093        10.222.251.44/31      up         up              9000          
Vlan4094        10.222.252.44/31      up         up              9000          
Vlan4097        unassigned            up         up              9164
```
## show lldp neighbors

```
Last table change time   : 2:39:17 ago
Number of table inserts  : 7
Number of table deletes  : 0
Number of table drops    : 0
Number of table age-outs : 0

Port            Neighbor Device ID       Neighbor Port ID    TTL
------------ ------------------------ ---------------------- ---
Et1             Site2-Host3              Ethernet1           120
Et2             Site2-Host4              Ethernet1           120
Et49/1          Site2-L4.act.lab         Ethernet49/1        120
Et50/1          Site2-L4.act.lab         Ethernet50/1        120
Et51/1          Site2-S1.act.lab         Ethernet3/1         120
Et52/1          Site2-S2.act.lab         Ethernet3/1         120
Et53/1          Site2-S3.act.lab         Ethernet3/1         120
```
## show running-config

```
! Command: show running-config
! device: Site2-L3 (vEOS-lab, EOS-4.32.2F)
!
! boot system flash:/CloudEOS.swi
!
no aaa root
!
username arista privilege 15 role network-admin secret sha512 $6$arista$hvhzPKMNzxDEPi2.4ml69k2ZGn88hWas4/loWEFDCkC2QEh/onTkN954QCDvZPAHLZDn41AoDozW5SKPFe0.6.
username cvpadmin privilege 15 role network-admin secret sha512 $6$ZdEghAjKPPMbkYVD$VjJwTiI82T2u7lgbdGaF9tVNVmgDZOdwvN/iyKUVelOUCpZ7ORF0LCklwwg55qwCmgvT.IBtohbfu5efQk9bE/
!
management api http-commands
   no shutdown
   !
   vrf default
      no shutdown
   !
   vrf mgmt
      no shutdown
!
daemon TerminAttr
   exec /usr/bin/TerminAttr -smashexcludes=ale,flexCounter,hardware,kni,pulse,strata -cvaddr=192.168.0.5:9910 -cvauth=token,/tmp/token -cvvrf=mgmt -taillogs
   no shutdown
!
vlan internal order ascending range 1006 1199
!
no service interface inactive port-id allocation disabled
!
transceiver qsfp default-mode 4x10G
!
service routing protocols model multi-agent
!
hostname Site2-L3
ip name-server vrf mgmt 192.168.0.5
ip name-server vrf mgmt 192.168.0.6
dns domain act.lab
!
spanning-tree mode mstp
no spanning-tree vlan-id 4093-4094
spanning-tree mst 0 priority 16384
!
system l1
   unsupported speed action error
   unsupported error-correction action error
!
vlan 20
   name L2-V20
!
vlan 30
   name L2-V30
!
vlan 2300
   name bluenet1
!
vlan 2301
   name bluenet2
!
vlan 3009
   name MLAG_L3_VRF_bluevrf
   trunk group MLAG
!
vlan 4093
   name MLAG_L3
   trunk group MLAG
!
vlan 4094
   name MLAG
   trunk group MLAG
!
vrf instance bluevrf
!
vrf instance mgmt
!
aaa authorization exec default local
!
interface Port-Channel1
   description PortChannel
   switchport trunk allowed vlan 20
   switchport mode trunk
   mlag 1
   spanning-tree portfast
   spanning-tree bpduguard enable
!
interface Port-Channel2
   description PortChannel
   switchport trunk allowed vlan 20
   switchport mode trunk
   mlag 2
   spanning-tree portfast
   spanning-tree bpduguard enable
!
interface Port-Channel491
   description MLAG_Site2-L4_Port-Channel491
   switchport mode trunk
   switchport trunk group MLAG
!
interface Ethernet1
   description SERVER_Site2-L3=Site2-L4=vPC1_NIC1
   channel-group 1 mode active
!
interface Ethernet2
   description SERVER_Site2-L3=Site2-L4=vPC2_NIC1
   channel-group 2 mode active
!
interface Ethernet3
   description test eth3 routed port
   vrf bluevrf
   ip address 10.192.233.254/24
!
interface Ethernet4
!
interface Ethernet5
!
interface Ethernet6
!
interface Ethernet7
!
interface Ethernet8
!
interface Ethernet9
!
interface Ethernet10
!
interface Ethernet11
!
interface Ethernet12
!
interface Ethernet13
!
interface Ethernet14
!
interface Ethernet15
!
interface Ethernet16
!
interface Ethernet17
!
interface Ethernet18
!
interface Ethernet19
!
interface Ethernet20
!
interface Ethernet21
!
interface Ethernet22
!
interface Ethernet23
!
interface Ethernet24
!
interface Ethernet25
!
interface Ethernet26
!
interface Ethernet27
!
interface Ethernet28
!
interface Ethernet29
!
interface Ethernet30
!
interface Ethernet31
!
interface Ethernet32
!
interface Ethernet33
!
interface Ethernet34
!
interface Ethernet35
!
interface Ethernet36
!
interface Ethernet37
!
interface Ethernet38
!
interface Ethernet39
!
interface Ethernet40
!
interface Ethernet41
!
interface Ethernet42
!
interface Ethernet43
!
interface Ethernet44
!
interface Ethernet45
!
interface Ethernet46
!
interface Ethernet47
!
interface Ethernet48
!
interface Ethernet49/1
   description MLAG_Site2-L4_Ethernet49/1
   channel-group 491 mode active
!
interface Ethernet50/1
   description MLAG_Site2-L4_Ethernet50/1
   channel-group 491 mode active
!
interface Ethernet51/1
   description P2P_Site2-S1_Ethernet3/1
   mtu 9000
   no switchport
   ip address 172.32.255.133/31
!
interface Ethernet52/1
   description P2P_Site2-S2_Ethernet3/1
   mtu 9000
   no switchport
   ip address 172.32.255.135/31
!
interface Ethernet53/1
   description P2P_Site2-S3_Ethernet3/1
   mtu 9000
   no switchport
   ip address 172.32.255.137/31
!
interface Ethernet54/1
!
interface Ethernet55/1
!
interface Ethernet56/1
!
interface Loopback0
   description ROUTER_ID
   ip address 192.2.255.25/32
!
interface Loopback1
   description VXLAN_TUNNEL_SOURCE
   ip address 192.2.254.25/32
!
interface Loopback100
   description DIAG_VRF_bluevrf
   vrf bluevrf
   ip address 10.255.1.25/32
!
interface Management1
   description OOB_MANAGEMENT
   vrf mgmt
   ip address 192.168.0.25/24
!
interface Vlan2300
   description bluenet1
   vrf bluevrf
   ip address virtual 192.168.11.1/24
!
interface Vlan2301
   description bluenet2
   vrf bluevrf
   ip address virtual 192.168.12.1/24
!
interface Vlan3009
   description MLAG_L3_VRF_bluevrf
   mtu 9000
   vrf bluevrf
   ip address 10.222.251.44/31
!
interface Vlan4093
   description MLAG_L3
   mtu 9000
   ip address 10.222.251.44/31
!
interface Vlan4094
   description MLAG
   mtu 9000
   no autostate
   ip address 10.222.252.44/31
!
interface Vxlan1
   description Site2-L3_VTEP
   vxlan source-interface Loopback1
   vxlan virtual-router encapsulation mac-address mlag-system-id
   vxlan udp-port 4789
   vxlan vlan 20 vni 30020
   vxlan vlan 30 vni 30030
   vxlan vlan 2300 vni 32300
   vxlan vlan 2301 vni 32301
   vxlan vrf bluevrf vni 10
!
ip virtual-router mac-address 00:1c:73:00:dc:01
ip address virtual source-nat vrf bluevrf address 10.255.1.25
!
ip routing
ip routing vrf bluevrf
no ip routing vrf mgmt
!
ip prefix-list PL-LOOPBACKS-EVPN-OVERLAY
   seq 10 permit 192.2.255.0/24 eq 32
   seq 20 permit 192.2.254.0/24 eq 32
!
ip prefix-list PL-MLAG-PEER-VRFS
   seq 10 permit 10.222.251.44/31
!
mlag configuration
   domain-id s2podmlag
   local-interface Vlan4094
   peer-address 10.222.252.45
   peer-link Port-Channel491
   reload-delay mlag 300
   reload-delay non-mlag 330
!
ip route vrf mgmt 0.0.0.0/0 192.168.0.5
!
ntp server vrf mgmt 192.168.0.5 prefer iburst
ntp server vrf mgmt 192.168.0.6 prefer iburst
!
route-map RM-CONN-2-BGP permit 10
   match ip address prefix-list PL-LOOPBACKS-EVPN-OVERLAY
!
route-map RM-CONN-2-BGP-VRFS deny 10
   match ip address prefix-list PL-MLAG-PEER-VRFS
!
route-map RM-CONN-2-BGP-VRFS permit 20
!
route-map RM-MLAG-PEER-IN permit 10
   description Make routes learned over MLAG Peer-link less preferred on spines to ensure optimal routing
   set origin incomplete
!
router bfd
   multihop interval 1200 min-rx 1200 multiplier 3
!
router bgp 65203
   router-id 192.2.255.25
   update wait-install
   no bgp default ipv4-unicast
   distance bgp 20 200 200
   graceful-restart restart-time 300
   graceful-restart
   maximum-paths 4 ecmp 4
   neighbor EVPN-OVERLAY-PEERS peer group
   neighbor EVPN-OVERLAY-PEERS update-source Loopback0
   neighbor EVPN-OVERLAY-PEERS bfd
   neighbor EVPN-OVERLAY-PEERS ebgp-multihop 3
   neighbor EVPN-OVERLAY-PEERS send-community
   neighbor EVPN-OVERLAY-PEERS maximum-routes 0
   neighbor IPv4-UNDERLAY-PEERS peer group
   neighbor IPv4-UNDERLAY-PEERS send-community
   neighbor IPv4-UNDERLAY-PEERS maximum-routes 12000
   neighbor MLAG-IPv4-UNDERLAY-PEER peer group
   neighbor MLAG-IPv4-UNDERLAY-PEER remote-as 65203
   neighbor MLAG-IPv4-UNDERLAY-PEER next-hop-self
   neighbor MLAG-IPv4-UNDERLAY-PEER description Site2-L4
   neighbor MLAG-IPv4-UNDERLAY-PEER route-map RM-MLAG-PEER-IN in
   neighbor MLAG-IPv4-UNDERLAY-PEER send-community
   neighbor MLAG-IPv4-UNDERLAY-PEER maximum-routes 12000
   neighbor 10.222.251.45 peer group MLAG-IPv4-UNDERLAY-PEER
   neighbor 10.222.251.45 description Site2-L4_Vlan4093
   neighbor 172.32.255.132 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.32.255.132 remote-as 65002
   neighbor 172.32.255.132 description Site2-S1_Ethernet3/1
   neighbor 172.32.255.134 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.32.255.134 remote-as 65002
   neighbor 172.32.255.134 description Site2-S2_Ethernet3/1
   neighbor 172.32.255.136 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.32.255.136 remote-as 65002
   neighbor 172.32.255.136 description Site2-S3_Ethernet3/1
   neighbor 192.2.255.1 peer group EVPN-OVERLAY-PEERS
   neighbor 192.2.255.1 remote-as 65002
   neighbor 192.2.255.1 description Site2-S1_Loopback0
   neighbor 192.2.255.2 peer group EVPN-OVERLAY-PEERS
   neighbor 192.2.255.2 remote-as 65002
   neighbor 192.2.255.2 description Site2-S2_Loopback0
   neighbor 192.2.255.3 peer group EVPN-OVERLAY-PEERS
   neighbor 192.2.255.3 remote-as 65002
   neighbor 192.2.255.3 description Site2-S3_Loopback0
   redistribute connected route-map RM-CONN-2-BGP
   !
   vlan 20
      rd 192.2.255.25:30020
      route-target both 30020:30020
      redistribute learned
   !
   vlan 30
      rd 192.2.255.25:30030
      route-target both 30030:30030
      redistribute learned
   !
   vlan 2300
      rd 192.2.255.25:32300
      route-target both 32300:32300
      redistribute learned
   !
   vlan 2301
      rd 192.2.255.25:32301
      route-target both 32301:32301
      redistribute learned
   !
   address-family evpn
      neighbor EVPN-OVERLAY-PEERS activate
   !
   address-family ipv4
      no neighbor EVPN-OVERLAY-PEERS activate
      neighbor IPv4-UNDERLAY-PEERS activate
      neighbor MLAG-IPv4-UNDERLAY-PEER activate
   !
   vrf bluevrf
      rd 192.2.255.25:10
      route-target import evpn 10:10
      route-target export evpn 10:10
      router-id 192.2.255.25
      update wait-install
      neighbor 10.222.251.45 peer group MLAG-IPv4-UNDERLAY-PEER
      neighbor 10.222.251.45 description Site2-L4_Vlan3009
      redistribute connected route-map RM-CONN-2-BGP-VRFS
!
router multicast
   ipv4
      software-forwarding kernel
   !
   ipv6
      software-forwarding kernel
!
end
```
## show version

```
Arista vEOS-lab
Hardware version: 
Serial number: f24fdb9beff047c5907c45cc196a487e
Hardware MAC address: 847b.80c8.5502
System MAC address: 847b.80c8.5502

Software image version: 4.32.2F
Architecture: x86_64
Internal build version: 4.32.2F-38195967.4322F
Internal build ID: 47416e3e-5279-42fe-a5bd-cf7624a68bb9
Image format version: 1.0
Image optimization: None

Uptime: 2 hours and 48 minutes
Total memory: 3970560 kB
Free memory: 2417576 kB
```
