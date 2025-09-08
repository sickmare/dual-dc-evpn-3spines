# Site1-L2 Commands Output

## Table of Contents

- [show lldp neighbors](#show-lldp-neighbors)
- [show ip interface brief](#show-ip-interface-brief)
- [show interfaces description](#show-interfaces-description)
- [show version](#show-version)
- [show running-config](#show-running-config)
## show interfaces description

```
Interface                      Status         Protocol           Description
Et1                            down           down               test eth1 trunk port
Et2                            up             up                 test eth2 routed port
Et3                            down           down               
Et4                            down           down               
Et5                            down           down               
Et6                            down           down               
Et7                            down           down               
Et8                            down           down               
Et9                            down           down               
Et10                           down           down               
Et11                           down           down               
Et12                           down           down               
Et13                           down           down               
Et14                           down           down               
Et15                           down           down               
Et16                           down           down               
Et17                           down           down               
Et18                           down           down               
Et19                           down           down               
Et20                           down           down               
Et21                           down           down               
Et22                           down           down               
Et23                           down           down               
Et24                           down           down               
Et25                           down           down               
Et26                           down           down               
Et27                           down           down               
Et28                           down           down               
Et29                           down           down               
Et30                           down           down               
Et31                           down           down               
Et32                           down           down               
Et33                           down           down               
Et34                           down           down               
Et35                           down           down               
Et36                           down           down               
Et37                           down           down               
Et38                           down           down               
Et39                           down           down               
Et40                           down           down               
Et41                           down           down               
Et42                           down           down               
Et43                           down           down               
Et44                           down           down               
Et45                           down           down               
Et46                           down           down               
Et47                           down           down               
Et48                           down           down               
Et49/1                         down           down               
Et50/1                         down           down               
Et51/1                         up             up                 P2P_Site1-S1_Ethernet2/1
Et52/1                         up             up                 P2P_Site1-S2_Ethernet2/1
Et53/1                         up             up                 P2P_Site1-S3_Ethernet2/1
Et54/1                         down           down               
Et55/1                         down           down               
Et56/1                         down           down               
Lo0                            up             up                 ROUTER_ID
Lo1                            up             up                 VXLAN_TUNNEL_SOURCE
Lo100                          up             up                 DIAG_VRF_bluevrf
Ma1                            up             up                 OOB_MANAGEMENT
Vl2300                         up             up                 bluenet1
Vl2301                         up             up                 bluenet2
Vl4097                         up             up                 
Vx1                            up             up                 Site1-L2_VTEP
```
## show ip interface brief

```
Address
Interface        IP Address           Status     Protocol         MTU   Owner  
---------------- -------------------- ---------- ------------ --------- -------
Ethernet51/1     172.30.255.67/31     up         up              9000          
Ethernet52/1     172.30.255.69/31     up         up              9000          
Ethernet53/1     172.30.255.71/31     up         up              9000          
Loopback0        192.0.255.14/32      up         up             65535          
Loopback1        192.0.254.14/32      up         up             65535          
Loopback100      10.255.1.14/32       up         up             65535          
Management1      192.168.0.14/24      up         up              1500          
Vlan2300         192.168.11.1/24      up         up              1500          
Vlan2301         192.168.12.1/24      up         up              1500          
Vlan4097         unassigned           up         up              9164
```
## show lldp neighbors

```
Last table change time   : 2:44:41 ago
Number of table inserts  : 4
Number of table deletes  : 0
Number of table drops    : 0
Number of table age-outs : 0

Port            Neighbor Device ID       Neighbor Port ID    TTL
------------ ------------------------ ---------------------- ---
Et2             Site1-Host2              Ethernet2           120
Et51/1          Site1-S1.act.lab         Ethernet2/1         120
Et52/1          Site1-S2.act.lab         Ethernet2/1         120
Et53/1          Site1-S3.act.lab         Ethernet2/1         120
```
## show running-config

```
! Command: show running-config
! device: Site1-L2 (vEOS-lab, EOS-4.32.2F)
!
! boot system flash:/CloudEOS.swi
!
no aaa root
!
username arista privilege 15 role network-admin secret sha512 $6$arista$hvhzPKMNzxDEPi2.4ml69k2ZGn88hWas4/loWEFDCkC2QEh/onTkN954QCDvZPAHLZDn41AoDozW5SKPFe0.6.
username cvpadmin privilege 15 role network-admin secret sha512 $6$ZZBPke/mJp.3PLCS$gmfrxDMATlhfkX345SHOyGABUPyOSsqMlp5T5nzDQfu.z5CfTpobmwEygI0DK6TKkiCzlGBjGF3SBqYiR66Hh1
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
hostname Site1-L2
ip name-server vrf mgmt 192.168.0.5
ip name-server vrf mgmt 192.168.0.6
dns domain act.lab
!
spanning-tree mode mstp
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
vrf instance bluevrf
!
vrf instance mgmt
!
aaa authorization exec default local
!
interface Ethernet1
   description test eth1 trunk port
   switchport trunk allowed vlan 20,30,2300-2301
   switchport mode trunk
   spanning-tree portfast
   spanning-tree bpduguard enable
!
interface Ethernet2
   description test eth2 routed port
   vrf bluevrf
   ip address 10.192.22.254/24
!
interface Ethernet3
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
!
interface Ethernet50/1
!
interface Ethernet51/1
   description P2P_Site1-S1_Ethernet2/1
   mtu 9000
   no switchport
   ip address 172.30.255.67/31
!
interface Ethernet52/1
   description P2P_Site1-S2_Ethernet2/1
   mtu 9000
   no switchport
   ip address 172.30.255.69/31
!
interface Ethernet53/1
   description P2P_Site1-S3_Ethernet2/1
   mtu 9000
   no switchport
   ip address 172.30.255.71/31
!
interface Ethernet54/1
!
interface Ethernet55/1
!
interface Ethernet56/1
!
interface Loopback0
   description ROUTER_ID
   ip address 192.0.255.14/32
!
interface Loopback1
   description VXLAN_TUNNEL_SOURCE
   ip address 192.0.254.14/32
!
interface Loopback100
   description DIAG_VRF_bluevrf
   vrf bluevrf
   ip address 10.255.1.14/32
!
interface Management1
   description OOB_MANAGEMENT
   vrf mgmt
   ip address 192.168.0.14/24
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
interface Vxlan1
   description Site1-L2_VTEP
   vxlan source-interface Loopback1
   vxlan udp-port 4789
   vxlan vlan 20 vni 30020
   vxlan vlan 30 vni 30030
   vxlan vlan 2300 vni 32300
   vxlan vlan 2301 vni 32301
   vxlan vrf bluevrf vni 10
!
ip virtual-router mac-address 00:1c:73:00:dc:01
ip address virtual source-nat vrf bluevrf address 10.255.1.14
!
ip routing
ip routing vrf bluevrf
no ip routing vrf mgmt
!
ip prefix-list PL-LOOPBACKS-EVPN-OVERLAY
   seq 10 permit 192.0.255.0/24 eq 32
   seq 20 permit 192.0.254.0/24 eq 32
!
ip route vrf mgmt 0.0.0.0/0 192.168.0.5
!
ntp server vrf mgmt 192.168.0.5 prefer iburst
ntp server vrf mgmt 192.168.0.6 prefer iburst
!
route-map RM-CONN-2-BGP permit 10
   match ip address prefix-list PL-LOOPBACKS-EVPN-OVERLAY
!
router bfd
   multihop interval 1200 min-rx 1200 multiplier 3
!
router bgp 65102
   router-id 192.0.255.14
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
   neighbor 172.30.255.66 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.30.255.66 remote-as 65001
   neighbor 172.30.255.66 description Site1-S1_Ethernet2/1
   neighbor 172.30.255.68 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.30.255.68 remote-as 65001
   neighbor 172.30.255.68 description Site1-S2_Ethernet2/1
   neighbor 172.30.255.70 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.30.255.70 remote-as 65001
   neighbor 172.30.255.70 description Site1-S3_Ethernet2/1
   neighbor 192.0.255.1 peer group EVPN-OVERLAY-PEERS
   neighbor 192.0.255.1 remote-as 65001
   neighbor 192.0.255.1 description Site1-S1_Loopback0
   neighbor 192.0.255.2 peer group EVPN-OVERLAY-PEERS
   neighbor 192.0.255.2 remote-as 65001
   neighbor 192.0.255.2 description Site1-S2_Loopback0
   neighbor 192.0.255.3 peer group EVPN-OVERLAY-PEERS
   neighbor 192.0.255.3 remote-as 65001
   neighbor 192.0.255.3 description Site1-S3_Loopback0
   redistribute connected route-map RM-CONN-2-BGP
   !
   vlan 20
      rd 192.0.255.14:30020
      route-target both 30020:30020
      redistribute learned
   !
   vlan 30
      rd 192.0.255.14:30030
      route-target both 30030:30030
      redistribute learned
   !
   vlan 2300
      rd 192.0.255.14:32300
      route-target both 32300:32300
      redistribute learned
   !
   vlan 2301
      rd 192.0.255.14:32301
      route-target both 32301:32301
      redistribute learned
   !
   address-family evpn
      neighbor EVPN-OVERLAY-PEERS activate
   !
   address-family ipv4
      no neighbor EVPN-OVERLAY-PEERS activate
      neighbor IPv4-UNDERLAY-PEERS activate
   !
   vrf bluevrf
      rd 192.0.255.14:10
      route-target import evpn 10:10
      route-target export evpn 10:10
      router-id 192.0.255.14
      redistribute connected
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
Serial number: a778b9afa3864e14ba32274f06b408df
Hardware MAC address: 8418.3875.896b
System MAC address: 8418.3875.896b

Software image version: 4.32.2F
Architecture: x86_64
Internal build version: 4.32.2F-38195967.4322F
Internal build ID: 47416e3e-5279-42fe-a5bd-cf7624a68bb9
Image format version: 1.0
Image optimization: None

Uptime: 2 hours and 48 minutes
Total memory: 3970560 kB
Free memory: 2468292 kB
```
