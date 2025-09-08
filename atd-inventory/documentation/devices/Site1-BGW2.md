# Site1-BGW2

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
| Management1 | OOB_MANAGEMENT | oob | mgmt | 192.168.0.18/24 | 192.168.0.5 |

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
   ip address 192.168.0.18/24
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
| 20 | L2-V20 | - |
| 30 | L2-V30 | - |
| 2300 | bluenet1 | - |
| 2301 | bluenet2 | - |

### VLANs Device Configuration

```eos
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
```

## Interfaces

### Ethernet Interfaces

#### Ethernet Interfaces Summary

##### L2

| Interface | Description | Mode | VLANs | Native VLAN | Trunk Group | Channel-Group |
| --------- | ----------- | ---- | ----- | ----------- | ----------- | ------------- |

*Inherited from Port-Channel Interface

##### IPv4

| Interface | Description | Channel Group | IP Address | VRF |  MTU | Shutdown | ACL In | ACL Out |
| --------- | ----------- | ------------- | ---------- | ----| ---- | -------- | ------ | ------- |
| Ethernet5/1 | P2P_DCI-1_Ethernet2/1 | - | 172.16.30.6/31 | default | 9000 | False | - | - |
| Ethernet6/1 | P2P_DCI-2_Ethernet2/1 | - | 172.16.30.8/31 | default | 9000 | False | - | - |
| Ethernet7/1 | P2P_DCI-3_Ethernet2/1 | - | 172.16.30.10/31 | default | 9000 | False | - | - |
| Ethernet51/1 | P2P_Site1-S1_Ethernet6/1 | - | 172.30.255.91/31 | default | 9000 | False | - | - |
| Ethernet52/1 | P2P_Site1-S2_Ethernet6/1 | - | 172.30.255.93/31 | default | 9000 | False | - | - |
| Ethernet53/1 | P2P_Site1-S3_Ethernet6/1 | - | 172.30.255.95/31 | default | 9000 | False | - | - |

#### Ethernet Interfaces Device Configuration

```eos
!
interface Ethernet5/1
   description P2P_DCI-1_Ethernet2/1
   no shutdown
   mtu 9000
   no switchport
   ip address 172.16.30.6/31
!
interface Ethernet6/1
   description P2P_DCI-2_Ethernet2/1
   no shutdown
   mtu 9000
   no switchport
   ip address 172.16.30.8/31
!
interface Ethernet7/1
   description P2P_DCI-3_Ethernet2/1
   no shutdown
   mtu 9000
   no switchport
   ip address 172.16.30.10/31
!
interface Ethernet51/1
   description P2P_Site1-S1_Ethernet6/1
   no shutdown
   mtu 9000
   no switchport
   ip address 172.30.255.91/31
!
interface Ethernet52/1
   description P2P_Site1-S2_Ethernet6/1
   no shutdown
   mtu 9000
   no switchport
   ip address 172.30.255.93/31
!
interface Ethernet53/1
   description P2P_Site1-S3_Ethernet6/1
   no shutdown
   mtu 9000
   no switchport
   ip address 172.30.255.95/31
```

### Loopback Interfaces

#### Loopback Interfaces Summary

##### IPv4

| Interface | Description | VRF | IP Address |
| --------- | ----------- | --- | ---------- |
| Loopback0 | ROUTER_ID | default | 192.0.255.18/32 |
| Loopback1 | VXLAN_TUNNEL_SOURCE | default | 192.0.254.18/32 |
| Loopback100 | DIAG_VRF_bluevrf | bluevrf | 10.255.1.18/32 |

##### IPv6

| Interface | Description | VRF | IPv6 Address |
| --------- | ----------- | --- | ------------ |
| Loopback0 | ROUTER_ID | default | - |
| Loopback1 | VXLAN_TUNNEL_SOURCE | default | - |
| Loopback100 | DIAG_VRF_bluevrf | bluevrf | - |

#### Loopback Interfaces Device Configuration

```eos
!
interface Loopback0
   description ROUTER_ID
   no shutdown
   ip address 192.0.255.18/32
!
interface Loopback1
   description VXLAN_TUNNEL_SOURCE
   no shutdown
   ip address 192.0.254.18/32
!
interface Loopback100
   description DIAG_VRF_bluevrf
   no shutdown
   vrf bluevrf
   ip address 10.255.1.18/32
```

### VLAN Interfaces

#### VLAN Interfaces Summary

| Interface | Description | VRF |  MTU | Shutdown |
| --------- | ----------- | --- | ---- | -------- |
| Vlan2300 | bluenet1 | bluevrf | - | False |
| Vlan2301 | bluenet2 | bluevrf | - | False |

##### IPv4

| Interface | VRF | IP Address | IP Address Virtual | IP Router Virtual Address | ACL In | ACL Out |
| --------- | --- | ---------- | ------------------ | ------------------------- | ------ | ------- |
| Vlan2300 |  bluevrf  |  -  |  192.168.11.1/24  |  -  |  -  |  -  |
| Vlan2301 |  bluevrf  |  -  |  192.168.12.1/24  |  -  |  -  |  -  |

#### VLAN Interfaces Device Configuration

```eos
!
interface Vlan2300
   description bluenet1
   no shutdown
   vrf bluevrf
   ip address virtual 192.168.11.1/24
!
interface Vlan2301
   description bluenet2
   no shutdown
   vrf bluevrf
   ip address virtual 192.168.12.1/24
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
| 20 | 30020 | - | - |
| 30 | 30030 | - | - |
| 2300 | 32300 | - | - |
| 2301 | 32301 | - | - |

##### VRF to VNI and Multicast Group Mappings

| VRF | VNI | Multicast Group |
| ---- | --- | --------------- |
| bluevrf | 10 | - |

#### VXLAN Interface Device Configuration

```eos
!
interface Vxlan1
   description Site1-BGW2_VTEP
   vxlan source-interface Loopback1
   vxlan udp-port 4789
   vxlan vlan 20 vni 30020
   vxlan vlan 30 vni 30030
   vxlan vlan 2300 vni 32300
   vxlan vlan 2301 vni 32301
   vxlan vrf bluevrf vni 10
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

#### IP Routing Device Configuration

```eos
!
ip routing
ip routing vrf bluevrf
no ip routing vrf mgmt
```

### IPv6 Routing

#### IPv6 Routing Summary

| VRF | Routing Enabled |
| --- | --------------- |
| default | False |
| bluevrf | false |
| mgmt | false |

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
| 65131 | 192.0.255.18 |

| BGP Tuning |
| ---------- |
| graceful-restart restart-time 300 |
| graceful-restart |
| update wait-install |
| no bgp default ipv4-unicast |
| distance bgp 20 200 200 |
| maximum-paths 4 ecmp 4 |

#### Router BGP Peer Groups

##### EVPN-OVERLAY-CORE

| Settings | Value |
| -------- | ----- |
| Address Family | evpn |
| Source | Loopback0 |
| BFD | True |
| Ebgp multihop | 15 |
| Send community | all |
| Maximum routes | 0 (no limit) |

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
| 172.16.30.7 | 64999 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - | - | - | - | - |
| 172.16.30.9 | 64999 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - | - | - | - | - |
| 172.16.30.11 | 64999 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - | - | - | - | - |
| 172.30.255.90 | 65001 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - | - | - | - | - |
| 172.30.255.92 | 65001 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - | - | - | - | - |
| 172.30.255.94 | 65001 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - | - | - | - | - |
| 192.0.255.1 | 65001 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 192.0.255.2 | 65001 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 192.0.255.3 | 65001 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 192.168.250.1 | 64999 | default | - | Inherited from peer group EVPN-OVERLAY-CORE | Inherited from peer group EVPN-OVERLAY-CORE | - | Inherited from peer group EVPN-OVERLAY-CORE | - | - | - | - |
| 192.168.250.2 | 64999 | default | - | Inherited from peer group EVPN-OVERLAY-CORE | Inherited from peer group EVPN-OVERLAY-CORE | - | Inherited from peer group EVPN-OVERLAY-CORE | - | - | - | - |
| 192.168.250.3 | 64999 | default | - | Inherited from peer group EVPN-OVERLAY-CORE | Inherited from peer group EVPN-OVERLAY-CORE | - | Inherited from peer group EVPN-OVERLAY-CORE | - | - | - | - |

#### Router BGP EVPN Address Family

##### EVPN Peer Groups

| Peer Group | Activate | Route-map In | Route-map Out | Encapsulation | Next-hop-self Source Interface |
| ---------- | -------- | ------------ | ------------- | ------------- | ------------------------------ |
| EVPN-OVERLAY-CORE | True |  - | - | default | - |
| EVPN-OVERLAY-PEERS | True |  - | - | default | - |

##### EVPN DCI Gateway Summary

| Settings | Value |
| -------- | ----- |
| Remote Domain Peer Groups | EVPN-OVERLAY-CORE |
| L3 Gateway Configured | True |
| L3 Gateway Inter-domain | True |

#### Router BGP VLANs

| VLAN | Route-Distinguisher | Both Route-Target | Import Route Target | Export Route-Target | Redistribute |
| ---- | ------------------- | ----------------- | ------------------- | ------------------- | ------------ |
| 20 | 192.0.255.18:30020 | 30020:30020<br>remote 30020:30020 | - | - | learned |
| 30 | 192.0.255.18:30030 | 30030:30030<br>remote 30030:30030 | - | - | learned |
| 2300 | 192.0.255.18:32300 | 32300:32300<br>remote 32300:32300 | - | - | learned |
| 2301 | 192.0.255.18:32301 | 32301:32301<br>remote 32301:32301 | - | - | learned |

#### Router BGP VRFs

| VRF | Route-Distinguisher | Redistribute |
| --- | ------------------- | ------------ |
| bluevrf | 192.0.255.18:10 | connected |

#### Router BGP Device Configuration

```eos
!
router bgp 65131
   router-id 192.0.255.18
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
   neighbor 172.16.30.7 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.16.30.7 remote-as 64999
   neighbor 172.16.30.7 description DCI-1
   neighbor 172.16.30.9 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.16.30.9 remote-as 64999
   neighbor 172.16.30.9 description DCI-2
   neighbor 172.16.30.11 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.16.30.11 remote-as 64999
   neighbor 172.16.30.11 description DCI-3
   neighbor 172.30.255.90 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.30.255.90 remote-as 65001
   neighbor 172.30.255.90 description Site1-S1_Ethernet6/1
   neighbor 172.30.255.92 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.30.255.92 remote-as 65001
   neighbor 172.30.255.92 description Site1-S2_Ethernet6/1
   neighbor 172.30.255.94 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.30.255.94 remote-as 65001
   neighbor 172.30.255.94 description Site1-S3_Ethernet6/1
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
   vlan 20
      rd 192.0.255.18:30020
      rd evpn domain remote 192.0.255.18:30020
      route-target both 30020:30020
      route-target import export evpn domain remote 30020:30020
      redistribute learned
   !
   vlan 30
      rd 192.0.255.18:30030
      rd evpn domain remote 192.0.255.18:30030
      route-target both 30030:30030
      route-target import export evpn domain remote 30030:30030
      redistribute learned
   !
   vlan 2300
      rd 192.0.255.18:32300
      rd evpn domain remote 192.0.255.18:32300
      route-target both 32300:32300
      route-target import export evpn domain remote 32300:32300
      redistribute learned
   !
   vlan 2301
      rd 192.0.255.18:32301
      rd evpn domain remote 192.0.255.18:32301
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
      rd 192.0.255.18:10
      route-target import evpn 10:10
      route-target export evpn 10:10
      router-id 192.0.255.18
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

### VRF Instances Device Configuration

```eos
!
vrf instance bluevrf
!
vrf instance mgmt
```

## Virtual Source NAT

### Virtual Source NAT Summary

| Source NAT VRF | Source NAT IPv4 Address | Source NAT IPv6 Address |
| -------------- | ----------------------- | ----------------------- |
| bluevrf | 10.255.1.18 | - |

### Virtual Source NAT Configuration

```eos
!
ip address virtual source-nat vrf bluevrf address 10.255.1.18
```
