# DCI-2 Commands Output

## Table of Contents

- [show lldp neighbors](#show-lldp-neighbors)
- [show ip interface brief](#show-ip-interface-brief)
- [show interfaces description](#show-interfaces-description)
- [show version](#show-version)
- [show running-config](#show-running-config)
## show interfaces description

```
Interface                      Status         Protocol           Description
Et1/1                          up             up                 P2P_Site1-BGW1_Ethernet6/1
Et2/1                          up             up                 P2P_Site1-BGW2_Ethernet6/1
Et3/1                          up             up                 P2P_Site1-BGW3_Ethernet6/1
Et4/1                          up             up                 P2P_Site2-BGW1_Ethernet6/1
Et5/1                          up             up                 P2P_Site2-BGW2_Ethernet6/1
Et6/1                          up             up                 P2P_Site2-BGW3_Ethernet6/1
Et7/1                          down           down               
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
Ma1                            up             up                 OOB_MANAGEMENT
```
## show ip interface brief

```
Address
Interface       IP Address           Status     Protocol         MTU    Owner  
--------------- -------------------- ---------- ------------ ---------- -------
Ethernet1/1     172.16.30.3/31       up         up              9214           
Ethernet2/1     172.16.30.9/31       up         up              9214           
Ethernet3/1     172.16.30.15/31      up         up              9214           
Ethernet4/1     172.16.30.21/31      up         up              9214           
Ethernet5/1     172.16.30.27/31      up         up              9214           
Ethernet6/1     172.16.30.33/31      up         up              9214           
Loopback0       192.168.250.2/32     up         up             65535           
Management1     192.168.0.101/24     up         up              1500
```
## show lldp neighbors

```
Last table change time   : 2:43:42 ago
Number of table inserts  : 6
Number of table deletes  : 0
Number of table drops    : 0
Number of table age-outs : 0

Port           Neighbor Device ID       Neighbor Port ID    TTL
----------- ------------------------ ---------------------- ---
Et1/1          Site1-BGW1.act.lab       Ethernet6/1         120
Et2/1          Site1-BGW2.act.lab       Ethernet6/1         120
Et3/1          Site1-BGW3.act.lab       Ethernet6/1         120
Et4/1          Site2-BGW1.act.lab       Ethernet6/1         120
Et5/1          Site2-BGW2.act.lab       Ethernet6/1         120
Et6/1          Site2-BGW3.act.lab       Ethernet6/1         120
```
## show running-config

```
! Command: show running-config
! device: DCI-2 (vEOS-lab, EOS-4.32.2F)
!
! boot system flash:/CloudEOS.swi
!
no aaa root
!
username arista privilege 15 role network-admin secret sha512 $6$arista$hvhzPKMNzxDEPi2.4ml69k2ZGn88hWas4/loWEFDCkC2QEh/onTkN954QCDvZPAHLZDn41AoDozW5SKPFe0.6.
username cvpadmin privilege 15 role network-admin secret sha512 $6$wQ47S3n8va1pD4v5$G92i6gzm5C4SIaA4o.TqSm.xMLmcnwfUaOjPWkABuqQDfoaj0Pjy4ohKy4aqZULCE9mDA4E0G1Mf8yxLLl/vh/
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
hostname DCI-2
ip name-server vrf mgmt 192.168.0.5
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
   description P2P_Site1-BGW1_Ethernet6/1
   mtu 9214
   no switchport
   ip address 172.16.30.3/31
!
interface Ethernet2/1
   description P2P_Site1-BGW2_Ethernet6/1
   mtu 9214
   no switchport
   ip address 172.16.30.9/31
!
interface Ethernet3/1
   description P2P_Site1-BGW3_Ethernet6/1
   mtu 9214
   no switchport
   ip address 172.16.30.15/31
!
interface Ethernet4/1
   description P2P_Site2-BGW1_Ethernet6/1
   mtu 9214
   no switchport
   ip address 172.16.30.21/31
!
interface Ethernet5/1
   description P2P_Site2-BGW2_Ethernet6/1
   mtu 9214
   no switchport
   ip address 172.16.30.27/31
!
interface Ethernet6/1
   description P2P_Site2-BGW3_Ethernet6/1
   mtu 9214
   no switchport
   ip address 172.16.30.33/31
!
interface Ethernet7/1
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
   ip address 192.168.250.2/32
!
interface Management1
   description OOB_MANAGEMENT
   vrf mgmt
   ip address 192.168.0.101/24
!
ip routing
no ip routing vrf mgmt
!
ip prefix-list PL-LOOPBACKS-EVPN-OVERLAY
   seq 10 permit 192.168.250.0/24 eq 32
!
ip route vrf mgmt 0.0.0.0/0 192.168.0.5
!
ntp server vrf mgmt 192.168.0.5
ntp server vrf mgmt 192.168.0.6
!
route-map RM-CONN-2-BGP permit 10
   match ip address prefix-list PL-LOOPBACKS-EVPN-OVERLAY
!
router bgp 64999
   router-id 192.168.250.2
   no bgp default ipv4-unicast
   distance bgp 20 200 200
   maximum-paths 4 ecmp 4
   neighbor IPv4-UNDERLAY-PEERS peer group
   neighbor IPv4-UNDERLAY-PEERS send-community
   neighbor IPv4-UNDERLAY-PEERS maximum-routes 12000
   neighbor 172.16.30.2 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.16.30.2 remote-as 65131
   neighbor 172.16.30.2 description Site1-BGW1
   neighbor 172.16.30.8 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.16.30.8 remote-as 65131
   neighbor 172.16.30.8 description Site1-BGW2
   neighbor 172.16.30.14 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.16.30.14 remote-as 65131
   neighbor 172.16.30.14 description Site1-BGW3
   neighbor 172.16.30.20 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.16.30.20 remote-as 65231
   neighbor 172.16.30.20 description Site2-BGW1
   neighbor 172.16.30.26 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.16.30.26 remote-as 65231
   neighbor 172.16.30.26 description Site2-BGW2
   neighbor 172.16.30.32 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.16.30.32 remote-as 65231
   neighbor 172.16.30.32 description Site2-BGW3
   redistribute connected route-map RM-CONN-2-BGP
   !
   address-family ipv4
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
Serial number: f7e0b660f861416d8853f73968c0325a
Hardware MAC address: 8427.6d53.ac9e
System MAC address: 8427.6d53.ac9e

Software image version: 4.32.2F
Architecture: x86_64
Internal build version: 4.32.2F-38195967.4322F
Internal build ID: 47416e3e-5279-42fe-a5bd-cf7624a68bb9
Image format version: 1.0
Image optimization: None

Uptime: 2 hours and 47 minutes
Total memory: 3970560 kB
Free memory: 2502888 kB
```
