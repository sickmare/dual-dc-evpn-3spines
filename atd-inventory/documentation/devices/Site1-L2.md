# Site1-L2

## Table of Contents

- [Management](#management)
  - [Management Interfaces](#management-interfaces)
  - [DNS Domain](#dns-domain)
  - [IP Name Servers](#ip-name-servers)
  - [NTP](#ntp)
  - [Management API HTTP](#management-api-http)
- [Authentication](#authentication)
  - [Local Users](#local-users)
  - [Enable Password](#enable-password)
  - [AAA Authorization](#aaa-authorization)
- [Spanning Tree](#spanning-tree)
  - [Spanning Tree Summary](#spanning-tree-summary)
  - [Spanning Tree Device Configuration](#spanning-tree-device-configuration)
- [Internal VLAN Allocation Policy](#internal-vlan-allocation-policy)
  - [Internal VLAN Allocation Policy Summary](#internal-vlan-allocation-policy-summary)
  - [Internal VLAN Allocation Policy Device Configuration](#internal-vlan-allocation-policy-device-configuration)
- [VLANs](#vlans)
  - [VLANs Summary](#vlans-summary)
  - [VLANs Device Configuration](#vlans-device-configuration)
- [Interfaces](#interfaces)
  - [Ethernet Interfaces](#ethernet-interfaces)
  - [Loopback Interfaces](#loopback-interfaces)
  - [VLAN Interfaces](#vlan-interfaces)
  - [VXLAN Interface](#vxlan-interface)
- [Routing](#routing)
  - [Service Routing Protocols Model](#service-routing-protocols-model)
  - [Virtual Router MAC Address](#virtual-router-mac-address)
  - [IP Routing](#ip-routing)
  - [IPv6 Routing](#ipv6-routing)
  - [Static Routes](#static-routes)
  - [Router BGP](#router-bgp)
- [BFD](#bfd)
  - [Router BFD](#router-bfd)
- [Multicast](#multicast)
  - [IP IGMP Snooping](#ip-igmp-snooping)
- [Filters](#filters)
  - [Prefix-lists](#prefix-lists)
  - [Route-maps](#route-maps)
- [VRF Instances](#vrf-instances)
  - [VRF Instances Summary](#vrf-instances-summary)
  - [VRF Instances Device Configuration](#vrf-instances-device-configuration)
- [Virtual Source NAT](#virtual-source-nat)
  - [Virtual Source NAT Summary](#virtual-source-nat-summary)
  - [Virtual Source NAT Configuration](#virtual-source-nat-configuration)

## Management

### Management Interfaces

#### Management Interfaces Summary

##### IPv4

| Management Interface | Description | Type | VRF | IP Address | Gateway |
| -------------------- | ----------- | ---- | --- | ---------- | ------- |
| Management1 | OOB_MANAGEMENT | oob | mgmt | 192.168.0.14/24 | 192.168.0.5 |

##### IPv6

| Management Interface | Description | Type | VRF | IPv6 Address | IPv6 Gateway |
| -------------------- | ----------- | ---- | --- | ------------ | ------------ |
| Management1 | OOB_MANAGEMENT | oob | mgmt | - | - |

#### Management Interfaces Device Configuration

```eos
!
interface Management1
   description OOB_MANAGEMENT
   no shutdown
   vrf mgmt
   ip address 192.168.0.14/24
```

### DNS Domain

DNS domain: act.lab

#### DNS Domain Device Configuration

```eos
dns domain act.lab
!
```

### IP Name Servers

#### IP Name Servers Summary

| Name Server | VRF | Priority |
| ----------- | --- | -------- |
| 192.168.0.5 | mgmt | - |
| 192.168.0.6 | mgmt | - |

#### IP Name Servers Device Configuration

```eos
ip name-server vrf mgmt 192.168.0.5
ip name-server vrf mgmt 192.168.0.6
```

### NTP

#### NTP Summary

##### NTP Servers

| Server | VRF | Preferred | Burst | iBurst | Version | Min Poll | Max Poll | Local-interface | Key |
| ------ | --- | --------- | ----- | ------ | ------- | -------- | -------- | --------------- | --- |
| 192.168.0.5 | mgmt | True | - | True | - | - | - | - | - |
| 192.168.0.6 | mgmt | True | - | True | - | - | - | - | - |

#### NTP Device Configuration

```eos
!
ntp server vrf mgmt 192.168.0.5 prefer iburst
ntp server vrf mgmt 192.168.0.6 prefer iburst
```

### Management API HTTP

#### Management API HTTP Summary

| HTTP | HTTPS | UNIX-Socket | Default Services |
| ---- | ----- | ----------- | ---------------- |
| False | True | - | - |

#### Management API VRF Access

| VRF Name | IPv4 ACL | IPv6 ACL |
| -------- | -------- | -------- |
| mgmt | - | - |

#### Management API HTTP Device Configuration

```eos
!
management api http-commands
   protocol https
   no shutdown
   !
   vrf mgmt
      no shutdown
```

## Authentication

### Local Users

#### Local Users Summary

| User | Privilege | Role | Disabled | Shell |
| ---- | --------- | ---- | -------- | ----- |
| arista | 15 | network-admin | False | - |

#### Local Users Device Configuration

```eos
!
username arista privilege 15 role network-admin secret sha512 <removed>
```

### Enable Password

Enable password has been disabled

### AAA Authorization

#### AAA Authorization Summary

| Type | User Stores |
| ---- | ----------- |
| Exec | local |

Authorization for configuration commands is disabled.

#### AAA Authorization Device Configuration

```eos
aaa authorization exec default local
!
```

## Spanning Tree

### Spanning Tree Summary

STP mode: **mstp**

#### MSTP Instance and Priority

| Instance(s) | Priority |
| -------- | -------- |
| 0 | 16384 |

### Spanning Tree Device Configuration

```eos
!
spanning-tree mode mstp
spanning-tree mst 0 priority 16384
```

## Internal VLAN Allocation Policy

### Internal VLAN Allocation Policy Summary

| Policy Allocation | Range Beginning | Range Ending |
| ------------------| --------------- | ------------ |
| ascending | 1006 | 1199 |

### Internal VLAN Allocation Policy Device Configuration

```eos
!
vlan internal order ascending range 1006 1199
```

## VLANs

### VLANs Summary

| VLAN ID | Name | Trunk Groups |
| ------- | ---- | ------------ |
| 101 | bluenet1 | - |
| 102 | bluenet2 | - |
| 201 | rednet1 | - |
| 202 | rednet2 | - |
| 301 | L2-V301 | - |
| 302 | L2-V302 | - |

### VLANs Device Configuration

```eos
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
```

## Interfaces

### Ethernet Interfaces

#### Ethernet Interfaces Summary

##### L2

| Interface | Description | Mode | VLANs | Native VLAN | Trunk Group | Channel-Group |
| --------- | ----------- | ---- | ----- | ----------- | ----------- | ------------- |
| Ethernet1 | test eth1 access port | access | 201 | - | - | - |

*Inherited from Port-Channel Interface

##### IPv4

| Interface | Description | Channel Group | IP Address | VRF |  MTU | Shutdown | ACL In | ACL Out |
| --------- | ----------- | ------------- | ---------- | ----| ---- | -------- | ------ | ------- |
| Ethernet2 | test eth2 routed port | - | 10.192.122.254/24 | redvrf | - | False | - | - |
| Ethernet51/1 | P2P_Site1-S1_Ethernet2/1 | - | 172.30.255.67/31 | default | 9000 | False | - | - |
| Ethernet52/1 | P2P_Site1-S2_Ethernet2/1 | - | 172.30.255.69/31 | default | 9000 | False | - | - |
| Ethernet53/1 | P2P_Site1-S3_Ethernet2/1 | - | 172.30.255.71/31 | default | 9000 | False | - | - |

#### Ethernet Interfaces Device Configuration

```eos
!
interface Ethernet1
   description test eth1 access port
   no shutdown
   switchport access vlan 201
   switchport mode access
   switchport
   spanning-tree portfast
   spanning-tree bpduguard enable
!
interface Ethernet2
   description test eth2 routed port
   no shutdown
   no switchport
   no switchport
   vrf redvrf
   ip address 10.192.122.254/24
!
interface Ethernet51/1
   description P2P_Site1-S1_Ethernet2/1
   no shutdown
   mtu 9000
   no switchport
   ip address 172.30.255.67/31
!
interface Ethernet52/1
   description P2P_Site1-S2_Ethernet2/1
   no shutdown
   mtu 9000
   no switchport
   ip address 172.30.255.69/31
!
interface Ethernet53/1
   description P2P_Site1-S3_Ethernet2/1
   no shutdown
   mtu 9000
   no switchport
   ip address 172.30.255.71/31
```

### Loopback Interfaces

#### Loopback Interfaces Summary

##### IPv4

| Interface | Description | VRF | IP Address |
| --------- | ----------- | --- | ---------- |
| Loopback0 | ROUTER_ID | default | 192.0.255.14/32 |
| Loopback1 | VXLAN_TUNNEL_SOURCE | default | 192.0.254.14/32 |
| Loopback100 | DIAG_VRF_bluevrf | bluevrf | 10.255.1.14/32 |
| Loopback200 | DIAG_VRF_redvrf | redvrf | 10.255.2.14/32 |

##### IPv6

| Interface | Description | VRF | IPv6 Address |
| --------- | ----------- | --- | ------------ |
| Loopback0 | ROUTER_ID | default | - |
| Loopback1 | VXLAN_TUNNEL_SOURCE | default | - |
| Loopback100 | DIAG_VRF_bluevrf | bluevrf | - |
| Loopback200 | DIAG_VRF_redvrf | redvrf | - |

#### Loopback Interfaces Device Configuration

```eos
!
interface Loopback0
   description ROUTER_ID
   no shutdown
   ip address 192.0.255.14/32
!
interface Loopback1
   description VXLAN_TUNNEL_SOURCE
   no shutdown
   ip address 192.0.254.14/32
!
interface Loopback100
   description DIAG_VRF_bluevrf
   no shutdown
   vrf bluevrf
   ip address 10.255.1.14/32
!
interface Loopback200
   description DIAG_VRF_redvrf
   no shutdown
   vrf redvrf
   ip address 10.255.2.14/32
```

### VLAN Interfaces

#### VLAN Interfaces Summary

| Interface | Description | VRF |  MTU | Shutdown |
| --------- | ----------- | --- | ---- | -------- |
| Vlan101 | bluenet1 | bluevrf | - | False |
| Vlan102 | bluenet2 | bluevrf | - | False |
| Vlan201 | rednet1 | redvrf | - | False |
| Vlan202 | rednet2 | redvrf | - | False |

##### IPv4

| Interface | VRF | IP Address | IP Address Virtual | IP Router Virtual Address | ACL In | ACL Out |
| --------- | --- | ---------- | ------------------ | ------------------------- | ------ | ------- |
| Vlan101 |  bluevrf  |  -  |  10.10.101.254/24  |  -  |  -  |  -  |
| Vlan102 |  bluevrf  |  -  |  10.10.102.254/24  |  -  |  -  |  -  |
| Vlan201 |  redvrf  |  -  |  10.20.201.254/24  |  -  |  -  |  -  |
| Vlan202 |  redvrf  |  -  |  10.20.202.254/24  |  -  |  -  |  -  |

#### VLAN Interfaces Device Configuration

```eos
!
interface Vlan101
   description bluenet1
   no shutdown
   vrf bluevrf
   ip address virtual 10.10.101.254/24
!
interface Vlan102
   description bluenet2
   no shutdown
   vrf bluevrf
   ip address virtual 10.10.102.254/24
!
interface Vlan201
   description rednet1
   no shutdown
   vrf redvrf
   ip address virtual 10.20.201.254/24
!
interface Vlan202
   description rednet2
   no shutdown
   vrf redvrf
   ip address virtual 10.20.202.254/24
```

### VXLAN Interface

#### VXLAN Interface Summary

| Setting | Value |
| ------- | ----- |
| Source Interface | Loopback1 |
| UDP port | 4789 |

##### VLAN to VNI, Flood List and Multicast Group Mappings

| VLAN | VNI | Flood List | Multicast Group |
| ---- | --- | ---------- | --------------- |
| 101 | 30101 | - | - |
| 102 | 30102 | - | - |
| 201 | 30201 | - | - |
| 202 | 30202 | - | - |
| 301 | 30301 | - | - |
| 302 | 30302 | - | - |

##### VRF to VNI and Multicast Group Mappings

| VRF | VNI | Multicast Group |
| ---- | --- | --------------- |
| bluevrf | 10 | - |
| redvrf | 20 | - |

#### VXLAN Interface Device Configuration

```eos
!
interface Vxlan1
   description Site1-L2_VTEP
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
```

## Routing

### Service Routing Protocols Model

Multi agent routing protocol model enabled

```eos
!
service routing protocols model multi-agent
```

### Virtual Router MAC Address

#### Virtual Router MAC Address Summary

Virtual Router MAC Address: 00:1c:73:00:dc:01

#### Virtual Router MAC Address Device Configuration

```eos
!
ip virtual-router mac-address 00:1c:73:00:dc:01
```

### IP Routing

#### IP Routing Summary

| VRF | Routing Enabled |
| --- | --------------- |
| default | True |
| bluevrf | True |
| mgmt | False |
| redvrf | True |

#### IP Routing Device Configuration

```eos
!
ip routing
ip routing vrf bluevrf
no ip routing vrf mgmt
ip routing vrf redvrf
```

### IPv6 Routing

#### IPv6 Routing Summary

| VRF | Routing Enabled |
| --- | --------------- |
| default | False |
| bluevrf | false |
| mgmt | false |
| redvrf | false |

### Static Routes

#### Static Routes Summary

| VRF | Destination Prefix | Next Hop IP | Exit interface | Administrative Distance | Tag | Route Name | Metric |
| --- | ------------------ | ----------- | -------------- | ----------------------- | --- | ---------- | ------ |
| mgmt | 0.0.0.0/0 | 192.168.0.5 | - | 1 | - | - | - |

#### Static Routes Device Configuration

```eos
!
ip route vrf mgmt 0.0.0.0/0 192.168.0.5
```

### Router BGP

ASN Notation: asplain

#### Router BGP Summary

| BGP AS | Router ID |
| ------ | --------- |
| 65102 | 192.0.255.14 |

| BGP Tuning |
| ---------- |
| graceful-restart restart-time 300 |
| graceful-restart |
| no bgp default ipv4-unicast |
| distance bgp 20 200 200 |
| maximum-paths 4 ecmp 4 |

#### Router BGP Peer Groups

##### EVPN-OVERLAY-PEERS

| Settings | Value |
| -------- | ----- |
| Address Family | evpn |
| Source | Loopback0 |
| BFD | True |
| Ebgp multihop | 3 |
| Send community | all |
| Maximum routes | 0 (no limit) |

##### IPv4-UNDERLAY-PEERS

| Settings | Value |
| -------- | ----- |
| Address Family | ipv4 |
| Send community | all |
| Maximum routes | 12000 |

#### BGP Neighbors

| Neighbor | Remote AS | VRF | Shutdown | Send-community | Maximum-routes | Allowas-in | BFD | RIB Pre-Policy Retain | Route-Reflector Client | Passive | TTL Max Hops |
| -------- | --------- | --- | -------- | -------------- | -------------- | ---------- | --- | --------------------- | ---------------------- | ------- | ------------ |
| 172.30.255.66 | 65001 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - | - | - | - | - |
| 172.30.255.68 | 65001 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - | - | - | - | - |
| 172.30.255.70 | 65001 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - | - | - | - | - |
| 192.0.255.1 | 65001 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 192.0.255.2 | 65001 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 192.0.255.3 | 65001 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |

#### Router BGP EVPN Address Family

##### EVPN Peer Groups

| Peer Group | Activate | Route-map In | Route-map Out | Encapsulation | Next-hop-self Source Interface |
| ---------- | -------- | ------------ | ------------- | ------------- | ------------------------------ |
| EVPN-OVERLAY-PEERS | True |  - | - | default | - |

#### Router BGP VLANs

| VLAN | Route-Distinguisher | Both Route-Target | Import Route Target | Export Route-Target | Redistribute |
| ---- | ------------------- | ----------------- | ------------------- | ------------------- | ------------ |
| 101 | 192.0.255.14:30101 | 30101:30101 | - | - | learned |
| 102 | 192.0.255.14:30102 | 30102:30102 | - | - | learned |
| 201 | 192.0.255.14:30201 | 30201:30201 | - | - | learned |
| 202 | 192.0.255.14:30202 | 30202:30202 | - | - | learned |
| 301 | 192.0.255.14:30301 | 30301:30301 | - | - | learned |
| 302 | 192.0.255.14:30302 | 30302:30302 | - | - | learned |

#### Router BGP VRFs

| VRF | Route-Distinguisher | Redistribute |
| --- | ------------------- | ------------ |
| bluevrf | 192.0.255.14:10 | connected |
| redvrf | 192.0.255.14:20 | connected |

#### Router BGP Device Configuration

```eos
!
router bgp 65102
   router-id 192.0.255.14
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
   vlan 101
      rd 192.0.255.14:30101
      route-target both 30101:30101
      redistribute learned
   !
   vlan 102
      rd 192.0.255.14:30102
      route-target both 30102:30102
      redistribute learned
   !
   vlan 201
      rd 192.0.255.14:30201
      route-target both 30201:30201
      redistribute learned
   !
   vlan 202
      rd 192.0.255.14:30202
      route-target both 30202:30202
      redistribute learned
   !
   vlan 301
      rd 192.0.255.14:30301
      route-target both 30301:30301
      redistribute learned
   !
   vlan 302
      rd 192.0.255.14:30302
      route-target both 30302:30302
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
   vrf redvrf
      rd 192.0.255.14:20
      route-target import evpn 20:20
      route-target export evpn 20:20
      router-id 192.0.255.14
      redistribute connected
```

## BFD

### Router BFD

#### Router BFD Multihop Summary

| Interval | Minimum RX | Multiplier |
| -------- | ---------- | ---------- |
| 1200 | 1200 | 3 |

#### Router BFD Device Configuration

```eos
!
router bfd
   multihop interval 1200 min-rx 1200 multiplier 3
```

## Multicast

### IP IGMP Snooping

#### IP IGMP Snooping Summary

| IGMP Snooping | Fast Leave | Interface Restart Query | Proxy | Restart Query Interval | Robustness Variable |
| ------------- | ---------- | ----------------------- | ----- | ---------------------- | ------------------- |
| Enabled | - | - | - | - | - |

#### IP IGMP Snooping Device Configuration

```eos
```

## Filters

### Prefix-lists

#### Prefix-lists Summary

##### PL-LOOPBACKS-EVPN-OVERLAY

| Sequence | Action |
| -------- | ------ |
| 10 | permit 192.0.255.0/24 eq 32 |
| 20 | permit 192.0.254.0/24 eq 32 |

#### Prefix-lists Device Configuration

```eos
!
ip prefix-list PL-LOOPBACKS-EVPN-OVERLAY
   seq 10 permit 192.0.255.0/24 eq 32
   seq 20 permit 192.0.254.0/24 eq 32
```

### Route-maps

#### Route-maps Summary

##### RM-CONN-2-BGP

| Sequence | Type | Match | Set | Sub-Route-Map | Continue |
| -------- | ---- | ----- | --- | ------------- | -------- |
| 10 | permit | ip address prefix-list PL-LOOPBACKS-EVPN-OVERLAY | - | - | - |

#### Route-maps Device Configuration

```eos
!
route-map RM-CONN-2-BGP permit 10
   match ip address prefix-list PL-LOOPBACKS-EVPN-OVERLAY
```

## VRF Instances

### VRF Instances Summary

| VRF Name | IP Routing |
| -------- | ---------- |
| bluevrf | enabled |
| mgmt | disabled |
| redvrf | enabled |

### VRF Instances Device Configuration

```eos
!
vrf instance bluevrf
!
vrf instance mgmt
!
vrf instance redvrf
```

## Virtual Source NAT

### Virtual Source NAT Summary

| Source NAT VRF | Source NAT IPv4 Address | Source NAT IPv6 Address |
| -------------- | ----------------------- | ----------------------- |
| bluevrf | 10.255.1.14 | - |
| redvrf | 10.255.2.14 | - |

### Virtual Source NAT Configuration

```eos
!
ip address virtual source-nat vrf bluevrf address 10.255.1.14
ip address virtual source-nat vrf redvrf address 10.255.2.14
```
