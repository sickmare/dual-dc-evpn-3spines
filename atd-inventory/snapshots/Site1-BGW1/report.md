# Site1-BGW1 Commands Output

## Table of Contents

- [show lldp neighbors](#show-lldp-neighbors)
- [show ip interface brief](#show-ip-interface-brief)
- [show interfaces description](#show-interfaces-description)
- [show version](#show-version)
- [show running-config](#show-running-config)
## show interfaces description

```
Interface                      Status         Protocol           Description
Et1/1                          up             up                 P2P_Site1-S1_Ethernet5/1
Et2/1                          up             up                 P2P_Site1-S2_Ethernet5/1
Et3/1                          up             up                 P2P_Site1-S3_Ethernet5/1
Et4/1                          down           down               
Et5/1                          up             up                 P2P_DCI-1_Ethernet1/1
Et6/1                          up             up                 P2P_DCI-2_Ethernet1/1
Et7/1                          up             up                 P2P_DCI-3_Ethernet1/1
Et8/1                          down           down               
Et9/1                          down           down               
Et10/1                         down           down               
Et11/1                         down           down               
Et12/1                         down           down               
Et13/1                         down           down               
Et14/1                         down           down               
Et15/1                         down           down               
Et16/1                         down           down               
Et17/1                         down           down               
Et18/1                         down           down               
Et19/1                         down           down               
Et20/1                         down           down               
Et21/1                         down           down               
Et22/1                         down           down               
Et23/1                         down           down               
Et24/1                         down           down               
Et25/1                         down           down               
Et26/1                         down           down               
Et27/1                         down           down               
Et28/1                         down           down               
Et29/1                         down           down               
Et30/1                         down           down               
Et31/1                         down           down               
Et32/1                         down           down               
Et33/1                         down           down               
Et34/1                         down           down               
Et35/1                         down           down               
Et36/1                         down           down               
Lo0                            up             up                 ROUTER_ID
Lo1                            up             up                 VXLAN_TUNNEL_SOURCE
Lo100                          up             up                 DIAG_VRF_bluevrf
Lo200                          up             up                 DIAG_VRF_redvrf
Ma1                            up             up                 OOB_MANAGEMENT
Vl101                          up             up                 bluenet1
Vl102                          up             up                 bluenet2
Vl201                          up             up                 rednet1
Vl202                          up             up                 rednet2
Vl4097                         up             up                 
Vl4098                         up             up                 
Vx1                            up             up                 Site1-BGW1_VTEP
```
## show ip interface brief

```
Address
Interface       IP Address           Status     Protocol         MTU    Owner  
--------------- -------------------- ---------- ------------ ---------- -------
Ethernet1/1     172.30.255.85/31     up         up              9000           
Ethernet2/1     172.30.255.87/31     up         up              9000           
Ethernet3/1     172.30.255.89/31     up         up              9000           
Ethernet5/1     172.16.30.0/31       up         up              9000           
Ethernet6/1     172.16.30.2/31       up         up              9000           
Ethernet7/1     172.16.30.4/31       up         up              9000           
Loopback0       192.0.255.17/32      up         up             65535           
Loopback1       192.0.254.17/32      up         up             65535           
Loopback100     10.255.1.17/32       up         up             65535           
Loopback200     10.255.2.17/32       up         up             65535           
Management1     192.168.0.17/24      up         up              1500           
Vlan101         10.10.101.254/24     up         up              1500           
Vlan102         10.10.102.254/24     up         up              1500           
Vlan201         10.20.201.254/24     up         up              1500           
Vlan202         10.20.202.254/24     up         up              1500           
Vlan4097        unassigned           up         up              9164           
Vlan4098        unassigned           up         up              9164
```
## show lldp neighbors

```
Last table change time   : 0:55:42 ago
Number of table inserts  : 6
Number of table deletes  : 0
Number of table drops    : 0
Number of table age-outs : 0

Port           Neighbor Device ID       Neighbor Port ID    TTL
----------- ------------------------ ---------------------- ---
Et1/1          Site1-S1.act.lab         Ethernet5/1         120
Et2/1          Site1-S2.act.lab         Ethernet5/1         120
Et3/1          Site1-S3.act.lab         Ethernet5/1         120
Et5/1          DCI-1.act.lab            Ethernet1/1         120
Et6/1          DCI-2.act.lab            Ethernet1/1         120
Et7/1          DCI-3.act.lab            Ethernet1/1         120
```
## show running-config

```
! Command: show running-config
! device: Site1-BGW1 (vEOS-lab, EOS-4.32.2F)
!
! boot system flash:/CloudEOS.swi
!
no aaa root
!
username arista privilege 15 role network-admin secret sha512 $6$arista$hvhzPKMNzxDEPi2.4ml69k2ZGn88hWas4/loWEFDCkC2QEh/onTkN954QCDvZPAHLZDn41AoDozW5SKPFe0.6.
username cvpadmin privilege 15 role network-admin secret sha512 $6$itnQOfNHs7eEuiAc$jshSu89mFFORc9nhOY64v6RtGnpn4/.zA.6zNAd5naRbvYx.hDWFNjVI.kXeNlT/QJq91D01OSn6drYd2sNSK0
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
hostname Site1-BGW1
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
vlan 101
   name bluenet1
!
vlan 102
   name bluenet2
!
vlan 201
   name rednet1
!
vlan 202
   name rednet2
!
vlan 301
   name L2-V301
!
vlan 302
   name L2-V302
!
vrf instance bluevrf
!
vrf instance mgmt
!
vrf instance redvrf
!
aaa authorization exec default local
!
interface Ethernet1/1
   description P2P_Site1-S1_Ethernet5/1
   mtu 9000
   no switchport
   ip address 172.30.255.85/31
!
interface Ethernet2/1
   description P2P_Site1-S2_Ethernet5/1
   mtu 9000
   no switchport
   ip address 172.30.255.87/31
!
interface Ethernet3/1
   description P2P_Site1-S3_Ethernet5/1
   mtu 9000
   no switchport
   ip address 172.30.255.89/31
!
interface Ethernet4/1
!
interface Ethernet5/1
   description P2P_DCI-1_Ethernet1/1
   mtu 9000
   no switchport
   ip address 172.16.30.0/31
!
interface Ethernet6/1
   description P2P_DCI-2_Ethernet1/1
   mtu 9000
   no switchport
   ip address 172.16.30.2/31
!
interface Ethernet7/1
   description P2P_DCI-3_Ethernet1/1
   mtu 9000
   no switchport
   ip address 172.16.30.4/31
!
interface Ethernet8/1
!
interface Ethernet9/1
!
interface Ethernet10/1
!
interface Ethernet11/1
!
interface Ethernet12/1
!
interface Ethernet13/1
!
interface Ethernet14/1
!
interface Ethernet15/1
!
interface Ethernet16/1
!
interface Ethernet17/1
!
interface Ethernet18/1
!
interface Ethernet19/1
!
interface Ethernet20/1
!
interface Ethernet21/1
!
interface Ethernet22/1
!
interface Ethernet23/1
!
interface Ethernet24/1
!
interface Ethernet25/1
!
interface Ethernet26/1
!
interface Ethernet27/1
!
interface Ethernet28/1
!
interface Ethernet29/1
!
interface Ethernet30/1
!
interface Ethernet31/1
!
interface Ethernet32/1
!
interface Ethernet33/1
!
interface Ethernet34/1
!
interface Ethernet35/1
!
interface Ethernet36/1
!
interface Loopback0
   description ROUTER_ID
   ip address 192.0.255.17/32
!
interface Loopback1
   description VXLAN_TUNNEL_SOURCE
   ip address 192.0.254.17/32
!
interface Loopback100
   description DIAG_VRF_bluevrf
   vrf bluevrf
   ip address 10.255.1.17/32
!
interface Loopback200
   description DIAG_VRF_redvrf
   vrf redvrf
   ip address 10.255.2.17/32
!
interface Management1
   description OOB_MANAGEMENT
   vrf mgmt
   ip address 192.168.0.17/24
!
interface Vlan101
   description bluenet1
   vrf bluevrf
   ip address virtual 10.10.101.254/24
!
interface Vlan102
   description bluenet2
   vrf bluevrf
   ip address virtual 10.10.102.254/24
!
interface Vlan201
   description rednet1
   vrf redvrf
   ip address virtual 10.20.201.254/24
!
interface Vlan202
   description rednet2
   vrf redvrf
   ip address virtual 10.20.202.254/24
!
interface Vxlan1
   description Site1-BGW1_VTEP
   vxlan source-interface Loopback1
   vxlan udp-port 4789
   vxlan vlan 101 vni 30101
   vxlan vlan 102 vni 30102
   vxlan vlan 201 vni 30201
   vxlan vlan 202 vni 30202
   vxlan vlan 301 vni 30301
   vxlan vlan 302 vni 30302
   vxlan vrf bluevrf vni 10
   vxlan vrf redvrf vni 20
!
ip virtual-router mac-address 00:1c:73:00:dc:01
ip address virtual source-nat vrf bluevrf address 10.255.1.17
ip address virtual source-nat vrf redvrf address 10.255.2.17
!
ip routing
ip routing vrf bluevrf
no ip routing vrf mgmt
ip routing vrf redvrf
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
router bgp 65131
   router-id 192.0.255.17
   no bgp default ipv4-unicast
   distance bgp 20 200 200
   graceful-restart restart-time 300
   graceful-restart
   maximum-paths 4 ecmp 4
   neighbor EVPN-OVERLAY-CORE peer group
   neighbor EVPN-OVERLAY-CORE update-source Loopback0
   neighbor EVPN-OVERLAY-CORE bfd
   neighbor EVPN-OVERLAY-CORE ebgp-multihop 15
   neighbor EVPN-OVERLAY-CORE send-community
   neighbor EVPN-OVERLAY-CORE maximum-routes 0
   neighbor EVPN-OVERLAY-PEERS peer group
   neighbor EVPN-OVERLAY-PEERS update-source Loopback0
   neighbor EVPN-OVERLAY-PEERS bfd
   neighbor EVPN-OVERLAY-PEERS ebgp-multihop 3
   neighbor EVPN-OVERLAY-PEERS send-community
   neighbor EVPN-OVERLAY-PEERS maximum-routes 0
   neighbor IPv4-UNDERLAY-PEERS peer group
   neighbor IPv4-UNDERLAY-PEERS send-community
   neighbor IPv4-UNDERLAY-PEERS maximum-routes 12000
   neighbor 172.16.30.1 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.16.30.1 remote-as 64999
   neighbor 172.16.30.1 description DCI-1
   neighbor 172.16.30.3 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.16.30.3 remote-as 64999
   neighbor 172.16.30.3 description DCI-2
   neighbor 172.16.30.5 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.16.30.5 remote-as 64999
   neighbor 172.16.30.5 description DCI-3
   neighbor 172.30.255.84 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.30.255.84 remote-as 65001
   neighbor 172.30.255.84 description Site1-S1_Ethernet5/1
   neighbor 172.30.255.86 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.30.255.86 remote-as 65001
   neighbor 172.30.255.86 description Site1-S2_Ethernet5/1
   neighbor 172.30.255.88 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.30.255.88 remote-as 65001
   neighbor 172.30.255.88 description Site1-S3_Ethernet5/1
   neighbor 192.0.255.1 peer group EVPN-OVERLAY-PEERS
   neighbor 192.0.255.1 remote-as 65001
   neighbor 192.0.255.1 description Site1-S1_Loopback0
   neighbor 192.0.255.2 peer group EVPN-OVERLAY-PEERS
   neighbor 192.0.255.2 remote-as 65001
   neighbor 192.0.255.2 description Site1-S2_Loopback0
   neighbor 192.0.255.3 peer group EVPN-OVERLAY-PEERS
   neighbor 192.0.255.3 remote-as 65001
   neighbor 192.0.255.3 description Site1-S3_Loopback0
   neighbor 192.168.250.1 peer group EVPN-OVERLAY-CORE
   neighbor 192.168.250.1 remote-as 64999
   neighbor 192.168.250.1 description DCI-1_Loopback0
   neighbor 192.168.250.2 peer group EVPN-OVERLAY-CORE
   neighbor 192.168.250.2 remote-as 64999
   neighbor 192.168.250.2 description DCI-2_Loopback0
   neighbor 192.168.250.3 peer group EVPN-OVERLAY-CORE
   neighbor 192.168.250.3 remote-as 64999
   neighbor 192.168.250.3 description DCI-3_Loopback0
   redistribute connected route-map RM-CONN-2-BGP
   !
   vlan 101
      rd 192.0.255.17:30101
      rd evpn domain remote 192.0.255.17:30101
      route-target both 30101:30101
      route-target import export evpn domain remote 30101:30101
      redistribute learned
   !
   vlan 102
      rd 192.0.255.17:30102
      rd evpn domain remote 192.0.255.17:30102
      route-target both 30102:30102
      route-target import export evpn domain remote 30102:30102
      redistribute learned
   !
   vlan 201
      rd 192.0.255.17:30201
      rd evpn domain remote 192.0.255.17:30201
      route-target both 30201:30201
      route-target import export evpn domain remote 30201:30201
      redistribute learned
   !
   vlan 202
      rd 192.0.255.17:30202
      rd evpn domain remote 192.0.255.17:30202
      route-target both 30202:30202
      route-target import export evpn domain remote 30202:30202
      redistribute learned
   !
   vlan 301
      rd 192.0.255.17:30301
      rd evpn domain remote 192.0.255.17:30301
      route-target both 30301:30301
      route-target import export evpn domain remote 30301:30301
      redistribute learned
   !
   vlan 302
      rd 192.0.255.17:30302
      rd evpn domain remote 192.0.255.17:30302
      route-target both 30302:30302
      route-target import export evpn domain remote 30302:30302
      redistribute learned
   !
   address-family evpn
      neighbor EVPN-OVERLAY-CORE activate
      neighbor EVPN-OVERLAY-CORE domain remote
      neighbor EVPN-OVERLAY-PEERS activate
      neighbor default next-hop-self received-evpn-routes route-type ip-prefix inter-domain
   !
   address-family ipv4
      no neighbor EVPN-OVERLAY-CORE activate
      no neighbor EVPN-OVERLAY-PEERS activate
      neighbor IPv4-UNDERLAY-PEERS activate
   !
   address-family rt-membership
      neighbor EVPN-OVERLAY-CORE activate
      neighbor EVPN-OVERLAY-PEERS activate
   !
   vrf bluevrf
      rd 192.0.255.17:10
      route-target import evpn 10:10
      route-target export evpn 10:10
      router-id 192.0.255.17
      redistribute connected
   !
   vrf redvrf
      rd 192.0.255.17:20
      route-target import evpn 20:20
      route-target export evpn 20:20
      router-id 192.0.255.17
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
Serial number: aa756ab215794a1fb2f508675b0536ff
Hardware MAC address: 84d9.b0af.a796
System MAC address: 84d9.b0af.a796

Software image version: 4.32.2F
Architecture: x86_64
Internal build version: 4.32.2F-38195967.4322F
Internal build ID: 47416e3e-5279-42fe-a5bd-cf7624a68bb9
Image format version: 1.0
Image optimization: None

Uptime: 59 minutes
Total memory: 3970560 kB
Free memory: 2479348 kB
```
