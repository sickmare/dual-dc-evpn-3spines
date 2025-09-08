# Site1-S1 Commands Output

## Table of Contents

- [show lldp neighbors](#show-lldp-neighbors)
- [show ip interface brief](#show-ip-interface-brief)
- [show interfaces description](#show-interfaces-description)
- [show version](#show-version)
- [show running-config](#show-running-config)
## show interfaces description

```
Interface                      Status         Protocol           Description
Et1/1                          up             up                 P2P_Site1-L1_Ethernet51/1
Et2/1                          up             up                 P2P_Site1-L2_Ethernet51/1
Et3/1                          up             up                 P2P_Site1-L3_Ethernet51/1
Et4/1                          up             up                 P2P_Site1-L4_Ethernet51/1
Et5/1                          up             up                 P2P_Site1-BGW1_Ethernet51/1
Et6/1                          up             up                 P2P_Site1-BGW2_Ethernet51/1
Et7/1                          up             up                 P2P_Site1-BGW3_Ethernet51/1
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
Et33                           down           down               
Et34                           down           down               
Lo0                            up             up                 ROUTER_ID
Ma1                            up             up                 OOB_MANAGEMENT
```
## show ip interface brief

```
Address
Interface       IP Address           Status     Protocol         MTU    Owner  
--------------- -------------------- ---------- ------------ ---------- -------
Ethernet1/1     172.30.255.60/31     up         up              9000           
Ethernet2/1     172.30.255.66/31     up         up              9000           
Ethernet3/1     172.30.255.72/31     up         up              9000           
Ethernet4/1     172.30.255.78/31     up         up              9000           
Ethernet5/1     172.30.255.84/31     up         up              9000           
Ethernet6/1     172.30.255.90/31     up         up              9000           
Ethernet7/1     172.30.255.96/31     up         up              9000           
Loopback0       192.0.255.1/32       up         up             65535           
Management1     192.168.0.10/24      up         up              1500
```
## show lldp neighbors

```
Last table change time   : 2:39:10 ago
Number of table inserts  : 7
Number of table deletes  : 0
Number of table drops    : 0
Number of table age-outs : 0

Port           Neighbor Device ID       Neighbor Port ID    TTL
----------- ------------------------ ---------------------- ---
Et1/1          Site1-L1.act.lab         Ethernet51/1        120
Et2/1          Site1-L2.act.lab         Ethernet51/1        120
Et3/1          Site1-L3.act.lab         Ethernet51/1        120
Et4/1          Site1-L4.act.lab         Ethernet51/1        120
Et5/1          Site1-BGW1.act.lab       Ethernet1/1         120
Et6/1          Site1-BGW2.act.lab       Ethernet1/1         120
Et7/1          Site1-BGW3.act.lab       Ethernet1/1         120
```
## show running-config

```
! Command: show running-config
! device: Site1-S1 (vEOS-lab, EOS-4.32.2F)
!
! boot system flash:/CloudEOS.swi
!
no aaa root
!
username arista privilege 15 role network-admin secret sha512 $6$arista$hvhzPKMNzxDEPi2.4ml69k2ZGn88hWas4/loWEFDCkC2QEh/onTkN954QCDvZPAHLZDn41AoDozW5SKPFe0.6.
username cvpadmin privilege 15 role network-admin secret sha512 $6$yY53xYKBjCdNmQbR$/Qtk4jnyTFaK2j2P.7Nt.hQI97DwRJMtFVPbLBOzvdpZ/cCTH0UeTi58gnNyRFV9tMZnaIVX5yoRs7KhJzNNU.
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
hostname Site1-S1
ip name-server vrf mgmt 192.168.0.5
ip name-server vrf mgmt 192.168.0.6
dns domain act.lab
!
spanning-tree mode none
!
system l1
   unsupported speed action error
   unsupported error-correction action error
!
vrf instance mgmt
!
aaa authorization exec default local
!
interface Ethernet1/1
   description P2P_Site1-L1_Ethernet51/1
   mtu 9000
   no switchport
   ip address 172.30.255.60/31
!
interface Ethernet2/1
   description P2P_Site1-L2_Ethernet51/1
   mtu 9000
   no switchport
   ip address 172.30.255.66/31
!
interface Ethernet3/1
   description P2P_Site1-L3_Ethernet51/1
   mtu 9000
   no switchport
   ip address 172.30.255.72/31
!
interface Ethernet4/1
   description P2P_Site1-L4_Ethernet51/1
   mtu 9000
   no switchport
   ip address 172.30.255.78/31
!
interface Ethernet5/1
   description P2P_Site1-BGW1_Ethernet51/1
   mtu 9000
   no switchport
   ip address 172.30.255.84/31
!
interface Ethernet6/1
   description P2P_Site1-BGW2_Ethernet51/1
   mtu 9000
   no switchport
   ip address 172.30.255.90/31
!
interface Ethernet7/1
   description P2P_Site1-BGW3_Ethernet51/1
   mtu 9000
   no switchport
   ip address 172.30.255.96/31
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
interface Ethernet33
!
interface Ethernet34
!
interface Loopback0
   description ROUTER_ID
   ip address 192.0.255.1/32
!
interface Management1
   description OOB_MANAGEMENT
   vrf mgmt
   ip address 192.168.0.10/24
!
ip routing
no ip routing vrf mgmt
!
ip prefix-list PL-LOOPBACKS-EVPN-OVERLAY
   seq 10 permit 192.0.255.0/24 eq 32
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
router bgp 65001
   router-id 192.0.255.1
   update wait-install
   no bgp default ipv4-unicast
   distance bgp 20 200 200
   graceful-restart restart-time 300
   graceful-restart
   maximum-paths 4 ecmp 4
   neighbor EVPN-OVERLAY-PEERS peer group
   neighbor EVPN-OVERLAY-PEERS next-hop-unchanged
   neighbor EVPN-OVERLAY-PEERS update-source Loopback0
   neighbor EVPN-OVERLAY-PEERS bfd
   neighbor EVPN-OVERLAY-PEERS ebgp-multihop 3
   neighbor EVPN-OVERLAY-PEERS send-community
   neighbor EVPN-OVERLAY-PEERS maximum-routes 0
   neighbor IPv4-UNDERLAY-PEERS peer group
   neighbor IPv4-UNDERLAY-PEERS send-community
   neighbor IPv4-UNDERLAY-PEERS maximum-routes 12000
   neighbor 172.30.255.61 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.30.255.61 remote-as 65101
   neighbor 172.30.255.61 description Site1-L1_Ethernet51/1
   neighbor 172.30.255.67 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.30.255.67 remote-as 65102
   neighbor 172.30.255.67 description Site1-L2_Ethernet51/1
   neighbor 172.30.255.73 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.30.255.73 remote-as 65103
   neighbor 172.30.255.73 description Site1-L3_Ethernet51/1
   neighbor 172.30.255.79 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.30.255.79 remote-as 65103
   neighbor 172.30.255.79 description Site1-L4_Ethernet51/1
   neighbor 172.30.255.85 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.30.255.85 remote-as 65131
   neighbor 172.30.255.85 description Site1-BGW1_Ethernet51/1
   neighbor 172.30.255.91 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.30.255.91 remote-as 65131
   neighbor 172.30.255.91 description Site1-BGW2_Ethernet51/1
   neighbor 172.30.255.97 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.30.255.97 remote-as 65131
   neighbor 172.30.255.97 description Site1-BGW3_Ethernet51/1
   neighbor 192.0.255.13 peer group EVPN-OVERLAY-PEERS
   neighbor 192.0.255.13 remote-as 65101
   neighbor 192.0.255.13 description Site1-L1_Loopback0
   neighbor 192.0.255.14 peer group EVPN-OVERLAY-PEERS
   neighbor 192.0.255.14 remote-as 65102
   neighbor 192.0.255.14 description Site1-L2_Loopback0
   neighbor 192.0.255.15 peer group EVPN-OVERLAY-PEERS
   neighbor 192.0.255.15 remote-as 65103
   neighbor 192.0.255.15 description Site1-L3_Loopback0
   neighbor 192.0.255.16 peer group EVPN-OVERLAY-PEERS
   neighbor 192.0.255.16 remote-as 65103
   neighbor 192.0.255.16 description Site1-L4_Loopback0
   neighbor 192.0.255.17 peer group EVPN-OVERLAY-PEERS
   neighbor 192.0.255.17 remote-as 65131
   neighbor 192.0.255.17 description Site1-BGW1_Loopback0
   neighbor 192.0.255.18 peer group EVPN-OVERLAY-PEERS
   neighbor 192.0.255.18 remote-as 65131
   neighbor 192.0.255.18 description Site1-BGW2_Loopback0
   neighbor 192.0.255.19 peer group EVPN-OVERLAY-PEERS
   neighbor 192.0.255.19 remote-as 65131
   neighbor 192.0.255.19 description Site1-BGW3_Loopback0
   redistribute connected route-map RM-CONN-2-BGP
   !
   address-family evpn
      neighbor EVPN-OVERLAY-PEERS activate
   !
   address-family ipv4
      no neighbor EVPN-OVERLAY-PEERS activate
      neighbor IPv4-UNDERLAY-PEERS activate
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
Serial number: 6e8813fbb5344fcb8d7d4c276544f9d4
Hardware MAC address: 84e2.7936.2cd4
System MAC address: 84e2.7936.2cd4

Software image version: 4.32.2F
Architecture: x86_64
Internal build version: 4.32.2F-38195967.4322F
Internal build ID: 47416e3e-5279-42fe-a5bd-cf7624a68bb9
Image format version: 1.0
Image optimization: None

Uptime: 2 hours and 47 minutes
Total memory: 3970560 kB
Free memory: 2522240 kB
```
