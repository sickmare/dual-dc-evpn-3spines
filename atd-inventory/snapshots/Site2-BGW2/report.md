# Site2-BGW2 Commands Output

## Table of Contents

- [show lldp neighbors](#show-lldp-neighbors)
- [show ip interface brief](#show-ip-interface-brief)
- [show interfaces description](#show-interfaces-description)
- [show version](#show-version)
- [show running-config](#show-running-config)
## show interfaces description

```
Interface                      Status         Protocol           Description
Et1/1                          up             up                 
Et2/1                          up             up                 
Et3/1                          up             up                 
Et4/1                          up             up                 
Et5/1                          up             up                 P2P_DCI-1_Ethernet5/1
Et6/1                          up             up                 P2P_DCI-2_Ethernet5/1
Et7/1                          up             up                 P2P_DCI-3_Ethernet5/1
Et8/1                          up             up                 
Et9/1                          up             up                 
Et10/1                         up             up                 
Et11/1                         up             up                 
Et12/1                         up             up                 
Et13/1                         up             up                 
Et14/1                         up             up                 
Et15/1                         up             up                 
Et16/1                         up             up                 
Et17/1                         up             up                 
Et18/1                         up             up                 
Et19/1                         up             up                 
Et20/1                         up             up                 
Et21/1                         up             up                 
Et22/1                         up             up                 
Et23/1                         up             up                 
Et24/1                         up             up                 
Et25/1                         up             up                 
Et26/1                         up             up                 
Et27/1                         up             up                 
Et28/1                         up             up                 
Et29/1                         up             up                 
Et30/1                         up             up                 
Et31/1                         up             up                 
Et32/1                         up             up                 
Et33/1                         up             up                 
Et34/1                         up             up                 
Et35/1                         up             up                 
Et36/1                         up             up                 
Lo0                            up             up                 ROUTER_ID
Lo1                            up             up                 VXLAN_TUNNEL_SOURCE
Lo100                          up             up                 DIAG_VRF_bluevrf
Ma1                            up             up                 OOB_MANAGEMENT
Vl2300                         up             up                 bluenet1
Vl2301                         up             up                 bluenet2
Vl4097                         up             up                 
Vx1                            up             up                 Site2-BGW2_VTEP
```
## show ip interface brief

```
Address
Interface       IP Address          Status     Protocol          MTU    Owner  
--------------- ------------------- ---------- ------------- ---------- -------
Ethernet5/1     172.16.30.24/31     up         up               9000           
Ethernet6/1     172.16.30.26/31     up         up               9000           
Ethernet7/1     172.16.30.28/31     up         up               9000           
Loopback0       192.2.255.28/32     up         up              65535           
Loopback1       192.2.254.28/32     up         up              65535           
Loopback100     10.255.1.28/32      up         up              65535           
Management1     192.168.0.28/24     up         up               1500           
Vlan2300        192.168.11.1/24     up         up               1500           
Vlan2301        192.168.12.1/24     up         up               1500           
Vlan4097        unassigned          up         up               9164
```
## show lldp neighbors

```
Last table change time   : 2:44:05 ago
Number of table inserts  : 6
Number of table deletes  : 0
Number of table drops    : 0
Number of table age-outs : 0

Port           Neighbor Device ID       Neighbor Port ID    TTL
----------- ------------------------ ---------------------- ---
Et1/1          Site2-S1.act.lab         Ethernet6/1         120
Et2/1          Site2-S2.act.lab         Ethernet6/1         120
Et3/1          Site2-S3.act.lab         Ethernet6/1         120
Et5/1          DCI-1.act.lab            Ethernet5/1         120
Et6/1          DCI-2.act.lab            Ethernet5/1         120
Et7/1          DCI-3.act.lab            Ethernet5/1         120
```
## show running-config

```
! Command: show running-config
! device: Site2-BGW2 (vEOS-lab, EOS-4.32.2F)
!
! boot system flash:/CloudEOS.swi
!
no aaa root
!
username arista privilege 15 role network-admin secret sha512 $6$arista$hvhzPKMNzxDEPi2.4ml69k2ZGn88hWas4/loWEFDCkC2QEh/onTkN954QCDvZPAHLZDn41AoDozW5SKPFe0.6.
username cvpadmin privilege 15 role network-admin secret sha512 $6$Z02i6YuIADcgyHaF$wG1rIf1OZHOZZnUc0ufrxbIA9sifsZUKtWw4eteM9GL8HgTvrjvyLBiMpdGQH.C5./40KxsAzBCyMVBB6XtdT.
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
hostname Site2-BGW2
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
interface Ethernet1/1
!
interface Ethernet2/1
!
interface Ethernet3/1
!
interface Ethernet4/1
!
interface Ethernet5/1
   description P2P_DCI-1_Ethernet5/1
   mtu 9000
   no switchport
   ip address 172.16.30.24/31
!
interface Ethernet6/1
   description P2P_DCI-2_Ethernet5/1
   mtu 9000
   no switchport
   ip address 172.16.30.26/31
!
interface Ethernet7/1
   description P2P_DCI-3_Ethernet5/1
   mtu 9000
   no switchport
   ip address 172.16.30.28/31
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
interface Ethernet51/1
   description P2P_Site2-S1_Ethernet6/1
   mtu 9000
   no switchport
   ip address 172.32.255.151/31
!
interface Ethernet52/1
   description P2P_Site2-S2_Ethernet6/1
   mtu 9000
   no switchport
   ip address 172.32.255.153/31
!
interface Ethernet53/1
   description P2P_Site2-S3_Ethernet6/1
   mtu 9000
   no switchport
   ip address 172.32.255.155/31
!
interface Loopback0
   description ROUTER_ID
   ip address 192.2.255.28/32
!
interface Loopback1
   description VXLAN_TUNNEL_SOURCE
   ip address 192.2.254.28/32
!
interface Loopback100
   description DIAG_VRF_bluevrf
   vrf bluevrf
   ip address 10.255.1.28/32
!
interface Management1
   description OOB_MANAGEMENT
   vrf mgmt
   ip address 192.168.0.28/24
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
   description Site2-BGW2_VTEP
   vxlan source-interface Loopback1
   vxlan udp-port 4789
   vxlan vlan 20 vni 30020
   vxlan vlan 30 vni 30030
   vxlan vlan 2300 vni 32300
   vxlan vlan 2301 vni 32301
   vxlan vrf bluevrf vni 10
!
ip virtual-router mac-address 00:1c:73:00:dc:01
ip address virtual source-nat vrf bluevrf address 10.255.1.28
!
ip routing
ip routing vrf bluevrf
no ip routing vrf mgmt
!
ip prefix-list PL-LOOPBACKS-EVPN-OVERLAY
   seq 10 permit 192.2.255.0/24 eq 32
   seq 20 permit 192.2.254.0/24 eq 32
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
router bgp 65231
   router-id 192.2.255.28
   update wait-install
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
   neighbor 172.16.30.25 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.16.30.25 remote-as 64999
   neighbor 172.16.30.25 description DCI-1
   neighbor 172.16.30.27 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.16.30.27 remote-as 64999
   neighbor 172.16.30.27 description DCI-2
   neighbor 172.16.30.29 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.16.30.29 remote-as 64999
   neighbor 172.16.30.29 description DCI-3
   neighbor 172.32.255.150 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.32.255.150 remote-as 65002
   neighbor 172.32.255.150 description Site2-S1_Ethernet6/1
   neighbor 172.32.255.152 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.32.255.152 remote-as 65002
   neighbor 172.32.255.152 description Site2-S2_Ethernet6/1
   neighbor 172.32.255.154 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.32.255.154 remote-as 65002
   neighbor 172.32.255.154 description Site2-S3_Ethernet6/1
   neighbor 192.2.255.1 peer group EVPN-OVERLAY-PEERS
   neighbor 192.2.255.1 remote-as 65002
   neighbor 192.2.255.1 description Site2-S1_Loopback0
   neighbor 192.2.255.2 peer group EVPN-OVERLAY-PEERS
   neighbor 192.2.255.2 remote-as 65002
   neighbor 192.2.255.2 description Site2-S2_Loopback0
   neighbor 192.2.255.3 peer group EVPN-OVERLAY-PEERS
   neighbor 192.2.255.3 remote-as 65002
   neighbor 192.2.255.3 description Site2-S3_Loopback0
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
   vlan 20
      rd 192.2.255.28:30020
      rd evpn domain remote 192.2.255.28:30020
      route-target both 30020:30020
      route-target import export evpn domain remote 30020:30020
      redistribute learned
   !
   vlan 30
      rd 192.2.255.28:30030
      rd evpn domain remote 192.2.255.28:30030
      route-target both 30030:30030
      route-target import export evpn domain remote 30030:30030
      redistribute learned
   !
   vlan 2300
      rd 192.2.255.28:32300
      rd evpn domain remote 192.2.255.28:32300
      route-target both 32300:32300
      route-target import export evpn domain remote 32300:32300
      redistribute learned
   !
   vlan 2301
      rd 192.2.255.28:32301
      rd evpn domain remote 192.2.255.28:32301
      route-target both 32301:32301
      route-target import export evpn domain remote 32301:32301
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
      rd 192.2.255.28:10
      route-target import evpn 10:10
      route-target export evpn 10:10
      router-id 192.2.255.28
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
Serial number: 13eead74f5994ebdbc69e4783bedec1f
Hardware MAC address: 84b9.5fa1.5c6d
System MAC address: 84b9.5fa1.5c6d

Software image version: 4.32.2F
Architecture: x86_64
Internal build version: 4.32.2F-38195967.4322F
Internal build ID: 47416e3e-5279-42fe-a5bd-cf7624a68bb9
Image format version: 1.0
Image optimization: None

Uptime: 2 hours and 47 minutes
Total memory: 3970560 kB
Free memory: 2454932 kB
```
