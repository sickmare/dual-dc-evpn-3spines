# Site2-S3

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
- [Interfaces](#interfaces)
  - [Ethernet Interfaces](#ethernet-interfaces)
  - [Loopback Interfaces](#loopback-interfaces)
- [Routing](#routing)
  - [Service Routing Protocols Model](#service-routing-protocols-model)
  - [IP Routing](#ip-routing)
  - [IPv6 Routing](#ipv6-routing)
  - [Static Routes](#static-routes)
  - [Router BGP](#router-bgp)
- [BFD](#bfd)
  - [Router BFD](#router-bfd)
- [Filters](#filters)
  - [Prefix-lists](#prefix-lists)
  - [Route-maps](#route-maps)
- [VRF Instances](#vrf-instances)
  - [VRF Instances Summary](#vrf-instances-summary)
  - [VRF Instances Device Configuration](#vrf-instances-device-configuration)

## Management

### Management Interfaces

#### Management Interfaces Summary

##### IPv4

| Management Interface | Description | Type | VRF | IP Address | Gateway |
| -------------------- | ----------- | ---- | --- | ---------- | ------- |
| Management1 | OOB_MANAGEMENT | oob | mgmt | 192.168.0.22/24 | 192.168.0.5 |

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
   ip address 192.168.0.22/24
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

STP mode: **none**

### Spanning Tree Device Configuration

```eos
!
spanning-tree mode none
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
| Ethernet1/1 | P2P_Site2-L1_Ethernet53/1 | - | 172.32.255.124/31 | default | 9000 | False | - | - |
| Ethernet2/1 | P2P_Site2-L2_Ethernet53/1 | - | 172.32.255.130/31 | default | 9000 | False | - | - |
| Ethernet3/1 | P2P_Site2-L3_Ethernet53/1 | - | 172.32.255.136/31 | default | 9000 | False | - | - |
| Ethernet4/1 | P2P_Site2-L4_Ethernet53/1 | - | 172.32.255.142/31 | default | 9000 | False | - | - |
| Ethernet5/1 | P2P_Site2-BGW1_Ethernet3/1 | - | 172.32.255.148/31 | default | 9000 | False | - | - |
| Ethernet6/1 | P2P_Site2-BGW2_Ethernet3/1 | - | 172.32.255.154/31 | default | 9000 | False | - | - |
| Ethernet7/1 | P2P_Site2-BGW3_Ethernet3/1 | - | 172.32.255.160/31 | default | 9000 | False | - | - |

#### Ethernet Interfaces Device Configuration

```eos
!
interface Ethernet1/1
   description P2P_Site2-L1_Ethernet53/1
   no shutdown
   mtu 9000
   no switchport
   ip address 172.32.255.124/31
!
interface Ethernet2/1
   description P2P_Site2-L2_Ethernet53/1
   no shutdown
   mtu 9000
   no switchport
   ip address 172.32.255.130/31
!
interface Ethernet3/1
   description P2P_Site2-L3_Ethernet53/1
   no shutdown
   mtu 9000
   no switchport
   ip address 172.32.255.136/31
!
interface Ethernet4/1
   description P2P_Site2-L4_Ethernet53/1
   no shutdown
   mtu 9000
   no switchport
   ip address 172.32.255.142/31
!
interface Ethernet5/1
   description P2P_Site2-BGW1_Ethernet3/1
   no shutdown
   mtu 9000
   no switchport
   ip address 172.32.255.148/31
!
interface Ethernet6/1
   description P2P_Site2-BGW2_Ethernet3/1
   no shutdown
   mtu 9000
   no switchport
   ip address 172.32.255.154/31
!
interface Ethernet7/1
   description P2P_Site2-BGW3_Ethernet3/1
   no shutdown
   mtu 9000
   no switchport
   ip address 172.32.255.160/31
```

### Loopback Interfaces

#### Loopback Interfaces Summary

##### IPv4

| Interface | Description | VRF | IP Address |
| --------- | ----------- | --- | ---------- |
| Loopback0 | ROUTER_ID | default | 192.2.255.3/32 |

##### IPv6

| Interface | Description | VRF | IPv6 Address |
| --------- | ----------- | --- | ------------ |
| Loopback0 | ROUTER_ID | default | - |

#### Loopback Interfaces Device Configuration

```eos
!
interface Loopback0
   description ROUTER_ID
   no shutdown
   ip address 192.2.255.3/32
```

## Routing

### Service Routing Protocols Model

Multi agent routing protocol model enabled

```eos
!
service routing protocols model multi-agent
```

### IP Routing

#### IP Routing Summary

| VRF | Routing Enabled |
| --- | --------------- |
| default | True |
| mgmt | False |

#### IP Routing Device Configuration

```eos
!
ip routing
no ip routing vrf mgmt
```

### IPv6 Routing

#### IPv6 Routing Summary

| VRF | Routing Enabled |
| --- | --------------- |
| default | False |
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
| 65002 | 192.2.255.3 |

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
| Next-hop unchanged | True |
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
| 172.32.255.125 | 65201 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - | - | - | - | - |
| 172.32.255.131 | 65202 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - | - | - | - | - |
| 172.32.255.137 | 65203 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - | - | - | - | - |
| 172.32.255.143 | 65203 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - | - | - | - | - |
| 172.32.255.149 | 65231 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - | - | - | - | - |
| 172.32.255.155 | 65231 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - | - | - | - | - |
| 172.32.255.161 | 65231 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - | - | - | - | - |
| 192.2.255.23 | 65201 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 192.2.255.24 | 65202 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 192.2.255.25 | 65203 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 192.2.255.26 | 65203 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 192.2.255.27 | 65231 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 192.2.255.28 | 65231 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 192.2.255.29 | 65231 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |

#### Router BGP EVPN Address Family

##### EVPN Peer Groups

| Peer Group | Activate | Route-map In | Route-map Out | Encapsulation | Next-hop-self Source Interface |
| ---------- | -------- | ------------ | ------------- | ------------- | ------------------------------ |
| EVPN-OVERLAY-PEERS | True |  - | - | default | - |

#### Router BGP Device Configuration

```eos
!
router bgp 65002
   router-id 192.2.255.3
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
   neighbor 172.32.255.125 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.32.255.125 remote-as 65201
   neighbor 172.32.255.125 description Site2-L1_Ethernet53/1
   neighbor 172.32.255.131 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.32.255.131 remote-as 65202
   neighbor 172.32.255.131 description Site2-L2_Ethernet53/1
   neighbor 172.32.255.137 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.32.255.137 remote-as 65203
   neighbor 172.32.255.137 description Site2-L3_Ethernet53/1
   neighbor 172.32.255.143 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.32.255.143 remote-as 65203
   neighbor 172.32.255.143 description Site2-L4_Ethernet53/1
   neighbor 172.32.255.149 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.32.255.149 remote-as 65231
   neighbor 172.32.255.149 description Site2-BGW1_Ethernet3/1
   neighbor 172.32.255.155 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.32.255.155 remote-as 65231
   neighbor 172.32.255.155 description Site2-BGW2_Ethernet3/1
   neighbor 172.32.255.161 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.32.255.161 remote-as 65231
   neighbor 172.32.255.161 description Site2-BGW3_Ethernet3/1
   neighbor 192.2.255.23 peer group EVPN-OVERLAY-PEERS
   neighbor 192.2.255.23 remote-as 65201
   neighbor 192.2.255.23 description Site2-L1_Loopback0
   neighbor 192.2.255.24 peer group EVPN-OVERLAY-PEERS
   neighbor 192.2.255.24 remote-as 65202
   neighbor 192.2.255.24 description Site2-L2_Loopback0
   neighbor 192.2.255.25 peer group EVPN-OVERLAY-PEERS
   neighbor 192.2.255.25 remote-as 65203
   neighbor 192.2.255.25 description Site2-L3_Loopback0
   neighbor 192.2.255.26 peer group EVPN-OVERLAY-PEERS
   neighbor 192.2.255.26 remote-as 65203
   neighbor 192.2.255.26 description Site2-L4_Loopback0
   neighbor 192.2.255.27 peer group EVPN-OVERLAY-PEERS
   neighbor 192.2.255.27 remote-as 65231
   neighbor 192.2.255.27 description Site2-BGW1_Loopback0
   neighbor 192.2.255.28 peer group EVPN-OVERLAY-PEERS
   neighbor 192.2.255.28 remote-as 65231
   neighbor 192.2.255.28 description Site2-BGW2_Loopback0
   neighbor 192.2.255.29 peer group EVPN-OVERLAY-PEERS
   neighbor 192.2.255.29 remote-as 65231
   neighbor 192.2.255.29 description Site2-BGW3_Loopback0
   redistribute connected route-map RM-CONN-2-BGP
   !
   address-family evpn
      neighbor EVPN-OVERLAY-PEERS activate
   !
   address-family ipv4
      no neighbor EVPN-OVERLAY-PEERS activate
      neighbor IPv4-UNDERLAY-PEERS activate
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

## Filters

### Prefix-lists

#### Prefix-lists Summary

##### PL-LOOPBACKS-EVPN-OVERLAY

| Sequence | Action |
| -------- | ------ |
| 10 | permit 192.2.255.0/24 eq 32 |

#### Prefix-lists Device Configuration

```eos
!
ip prefix-list PL-LOOPBACKS-EVPN-OVERLAY
   seq 10 permit 192.2.255.0/24 eq 32
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
| mgmt | disabled |

### VRF Instances Device Configuration

```eos
!
vrf instance mgmt
```
