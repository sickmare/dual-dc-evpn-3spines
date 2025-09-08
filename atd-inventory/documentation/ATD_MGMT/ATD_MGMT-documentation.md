# ATD_MGMT

## Table of Contents

- [Fabric Switches and Management IP](#fabric-switches-and-management-ip)
  - [Fabric Switches with inband Management IP](#fabric-switches-with-inband-management-ip)
- [Fabric Topology](#fabric-topology)
- [Fabric IP Allocation](#fabric-ip-allocation)
  - [Fabric Point-To-Point Links](#fabric-point-to-point-links)
  - [Point-To-Point Links Node Allocation](#point-to-point-links-node-allocation)
  - [Loopback Interfaces (BGP EVPN Peering)](#loopback-interfaces-bgp-evpn-peering)
  - [Loopback0 Interfaces Node Allocation](#loopback0-interfaces-node-allocation)
  - [VTEP Loopback VXLAN Tunnel Source Interfaces (VTEPs Only)](#vtep-loopback-vxlan-tunnel-source-interfaces-vteps-only)
  - [VTEP Loopback Node allocation](#vtep-loopback-node-allocation)
- [Connected Endpoints](#connected-endpoints)
  - [Connected Endpoint Keys](#connected-endpoint-keys)
  - [Servers](#servers)
  - [Port Profiles](#port-profiles)

## Fabric Switches and Management IP

| POD | Type | Node | Management IP | Platform | Provisioned in CloudVision | Serial Number |
| --- | ---- | ---- | ------------- | -------- | -------------------------- | ------------- |
| ATD_MGMT | super-spine | DCI-1 | 192.168.0.100/24 | 7280CR3-36S | Provisioned | - |
| ATD_MGMT | super-spine | DCI-2 | 192.168.0.101/24 | 7280CR3-36S | Provisioned | - |
| ATD_MGMT | super-spine | DCI-3 | 192.168.0.102/24 | 7280CR3-36S | Provisioned | - |
| ATD_MGMT | l3leaf | Site1-BGW1 | 192.168.0.17/24 | 7280CR3-36S | Provisioned | - |
| ATD_MGMT | l3leaf | Site1-BGW2 | 192.168.0.18/24 | 7280CR3-36S | Provisioned | - |
| ATD_MGMT | l3leaf | Site1-BGW3 | 192.168.0.19/24 | 7280CR3-36S | Provisioned | - |
| ATD_MGMT | l3leaf | Site1-L1 | 192.168.0.13/24 | 7050SX3-48YC8C | Provisioned | - |
| ATD_MGMT | l3leaf | Site1-L2 | 192.168.0.14/24 | 7050SX3-48YC8C | Provisioned | - |
| ATD_MGMT | l3leaf | Site1-L3 | 192.168.0.15/24 | 7050SX3-48YC8C | Provisioned | - |
| ATD_MGMT | l3leaf | Site1-L4 | 192.168.0.16/24 | 7050SX3-48YC8C | Provisioned | - |
| ATD_MGMT | spine | Site1-S1 | 192.168.0.10/24 | 7050CX3-32C | Provisioned | - |
| ATD_MGMT | spine | Site1-S2 | 192.168.0.11/24 | 7050CX3-32C | Provisioned | - |
| ATD_MGMT | spine | Site1-S3 | 192.168.0.12/24 | 7050CX3-32C | Provisioned | - |
| ATD_MGMT | l3leaf | Site2-BGW1 | 192.168.0.27/24 | 7280CR3-36S | Provisioned | - |
| ATD_MGMT | l3leaf | Site2-BGW2 | 192.168.0.28/24 | 7280CR3-36S | Provisioned | - |
| ATD_MGMT | l3leaf | Site2-BGW3 | 192.168.0.29/24 | 7280CR3-36S | Provisioned | - |
| ATD_MGMT | l3leaf | Site2-L1 | 192.168.0.23/24 | 7050SX3-48YC8C | Provisioned | - |
| ATD_MGMT | l3leaf | Site2-L2 | - | 7050SX3-48YC8C | Provisioned | - |
| ATD_MGMT | l3leaf | Site2-L3 | 192.168.0.25/24 | 7050SX3-48YC8C | Provisioned | - |
| ATD_MGMT | l3leaf | Site2-L4 | 192.168.0.26/24 | 7050SX3-48YC8C | Provisioned | - |
| ATD_MGMT | spine | Site2-S1 | 192.168.0.20/24 | 7050CX3-32C | Provisioned | - |
| ATD_MGMT | spine | Site2-S2 | 192.168.0.21/24 | 7050CX3-32C | Provisioned | - |
| ATD_MGMT | spine | Site2-S3 | 192.168.0.22/24 | 7050CX3-32C | Provisioned | - |

> Provision status is based on Ansible inventory declaration and do not represent real status from CloudVision.

### Fabric Switches with inband Management IP

| POD | Type | Node | Management IP | Inband Interface |
| --- | ---- | ---- | ------------- | ---------------- |

## Fabric Topology

| Type | Node | Node Interface | Peer Type | Peer Node | Peer Interface |
| ---- | ---- | -------------- | --------- | ----------| -------------- |
| super-spine | DCI-1 | Ethernet1/1 | l3leaf | Site1-BGW1 | Ethernet5/1 |
| super-spine | DCI-1 | Ethernet2/1 | l3leaf | Site1-BGW2 | Ethernet5/1 |
| super-spine | DCI-1 | Ethernet3/1 | l3leaf | Site1-BGW3 | Ethernet5/1 |
| super-spine | DCI-1 | Ethernet4/1 | l3leaf | Site2-BGW1 | Ethernet5/1 |
| super-spine | DCI-1 | Ethernet5/1 | l3leaf | Site2-BGW2 | Ethernet5/1 |
| super-spine | DCI-1 | Ethernet6/1 | l3leaf | Site2-BGW3 | Ethernet5/1 |
| super-spine | DCI-2 | Ethernet1/1 | l3leaf | Site1-BGW1 | Ethernet6/1 |
| super-spine | DCI-2 | Ethernet2/1 | l3leaf | Site1-BGW2 | Ethernet6/1 |
| super-spine | DCI-2 | Ethernet3/1 | l3leaf | Site1-BGW3 | Ethernet6/1 |
| super-spine | DCI-2 | Ethernet4/1 | l3leaf | Site2-BGW1 | Ethernet6/1 |
| super-spine | DCI-2 | Ethernet5/1 | l3leaf | Site2-BGW2 | Ethernet6/1 |
| super-spine | DCI-2 | Ethernet6/1 | l3leaf | Site2-BGW3 | Ethernet6/1 |
| super-spine | DCI-3 | Ethernet1/1 | l3leaf | Site1-BGW1 | Ethernet7/1 |
| super-spine | DCI-3 | Ethernet2/1 | l3leaf | Site1-BGW2 | Ethernet7/1 |
| super-spine | DCI-3 | Ethernet3/1 | l3leaf | Site1-BGW3 | Ethernet7/1 |
| super-spine | DCI-3 | Ethernet4/1 | l3leaf | Site2-BGW1 | Ethernet7/1 |
| super-spine | DCI-3 | Ethernet5/1 | l3leaf | Site2-BGW2 | Ethernet7/1 |
| super-spine | DCI-3 | Ethernet6/1 | l3leaf | Site2-BGW3 | Ethernet7/1 |
| l3leaf | Site1-BGW1 | Ethernet51/1 | spine | Site1-S1 | Ethernet5/1 |
| l3leaf | Site1-BGW1 | Ethernet52/1 | spine | Site1-S2 | Ethernet5/1 |
| l3leaf | Site1-BGW1 | Ethernet53/1 | spine | Site1-S3 | Ethernet5/1 |
| l3leaf | Site1-BGW2 | Ethernet51/1 | spine | Site1-S1 | Ethernet6/1 |
| l3leaf | Site1-BGW2 | Ethernet52/1 | spine | Site1-S2 | Ethernet6/1 |
| l3leaf | Site1-BGW2 | Ethernet53/1 | spine | Site1-S3 | Ethernet6/1 |
| l3leaf | Site1-BGW3 | Ethernet51/1 | spine | Site1-S1 | Ethernet7/1 |
| l3leaf | Site1-BGW3 | Ethernet52/1 | spine | Site1-S2 | Ethernet7/1 |
| l3leaf | Site1-BGW3 | Ethernet53/1 | spine | Site1-S3 | Ethernet7/1 |
| l3leaf | Site1-L1 | Ethernet51/1 | spine | Site1-S1 | Ethernet1/1 |
| l3leaf | Site1-L1 | Ethernet52/1 | spine | Site1-S2 | Ethernet1/1 |
| l3leaf | Site1-L1 | Ethernet53/1 | spine | Site1-S3 | Ethernet1/1 |
| l3leaf | Site1-L2 | Ethernet51/1 | spine | Site1-S1 | Ethernet2/1 |
| l3leaf | Site1-L2 | Ethernet52/1 | spine | Site1-S2 | Ethernet2/1 |
| l3leaf | Site1-L2 | Ethernet53/1 | spine | Site1-S3 | Ethernet2/1 |
| l3leaf | Site1-L3 | Ethernet49/1 | mlag_peer | Site1-L4 | Ethernet49/1 |
| l3leaf | Site1-L3 | Ethernet50/1 | mlag_peer | Site1-L4 | Ethernet50/1 |
| l3leaf | Site1-L3 | Ethernet51/1 | spine | Site1-S1 | Ethernet3/1 |
| l3leaf | Site1-L3 | Ethernet52/1 | spine | Site1-S2 | Ethernet3/1 |
| l3leaf | Site1-L3 | Ethernet53/1 | spine | Site1-S3 | Ethernet3/1 |
| l3leaf | Site1-L4 | Ethernet51/1 | spine | Site1-S1 | Ethernet4/1 |
| l3leaf | Site1-L4 | Ethernet52/1 | spine | Site1-S2 | Ethernet4/1 |
| l3leaf | Site1-L4 | Ethernet53/1 | spine | Site1-S3 | Ethernet4/1 |
| l3leaf | Site2-BGW1 | Ethernet51/1 | spine | Site2-S1 | Ethernet5/1 |
| l3leaf | Site2-BGW1 | Ethernet52/1 | spine | Site2-S2 | Ethernet5/1 |
| l3leaf | Site2-BGW1 | Ethernet53/1 | spine | Site2-S3 | Ethernet5/1 |
| l3leaf | Site2-BGW2 | Ethernet51/1 | spine | Site2-S1 | Ethernet6/1 |
| l3leaf | Site2-BGW2 | Ethernet52/1 | spine | Site2-S2 | Ethernet6/1 |
| l3leaf | Site2-BGW2 | Ethernet53/1 | spine | Site2-S3 | Ethernet6/1 |
| l3leaf | Site2-BGW3 | Ethernet51/1 | spine | Site2-S1 | Ethernet7/1 |
| l3leaf | Site2-BGW3 | Ethernet52/1 | spine | Site2-S2 | Ethernet7/1 |
| l3leaf | Site2-BGW3 | Ethernet53/1 | spine | Site2-S3 | Ethernet7/1 |
| l3leaf | Site2-L1 | Ethernet51/1 | spine | Site2-S1 | Ethernet1/1 |
| l3leaf | Site2-L1 | Ethernet52/1 | spine | Site2-S2 | Ethernet1/1 |
| l3leaf | Site2-L1 | Ethernet53/1 | spine | Site2-S3 | Ethernet1/1 |
| l3leaf | Site2-L2 | Ethernet51/1 | spine | Site2-S1 | Ethernet2/1 |
| l3leaf | Site2-L2 | Ethernet52/1 | spine | Site2-S2 | Ethernet2/1 |
| l3leaf | Site2-L2 | Ethernet53/1 | spine | Site2-S3 | Ethernet2/1 |
| l3leaf | Site2-L3 | Ethernet49/1 | mlag_peer | Site2-L4 | Ethernet49/1 |
| l3leaf | Site2-L3 | Ethernet50/1 | mlag_peer | Site2-L4 | Ethernet50/1 |
| l3leaf | Site2-L3 | Ethernet51/1 | spine | Site2-S1 | Ethernet3/1 |
| l3leaf | Site2-L3 | Ethernet52/1 | spine | Site2-S2 | Ethernet3/1 |
| l3leaf | Site2-L3 | Ethernet53/1 | spine | Site2-S3 | Ethernet3/1 |
| l3leaf | Site2-L4 | Ethernet51/1 | spine | Site2-S1 | Ethernet4/1 |
| l3leaf | Site2-L4 | Ethernet52/1 | spine | Site2-S2 | Ethernet4/1 |
| l3leaf | Site2-L4 | Ethernet53/1 | spine | Site2-S3 | Ethernet4/1 |

## Fabric IP Allocation

### Fabric Point-To-Point Links

| Uplink IPv4 Pool | Available Addresses | Assigned addresses | Assigned Address % |
| ---------------- | ------------------- | ------------------ | ------------------ |
| 172.30.255.0/24 | 256 | 42 | 16.41 % |
| 172.32.255.0/24 | 256 | 42 | 16.41 % |

### Point-To-Point Links Node Allocation

| Node | Node Interface | Node IP Address | Peer Node | Peer Interface | Peer IP Address |
| ---- | -------------- | --------------- | --------- | -------------- | --------------- |
| DCI-1 | Ethernet1/1 | 172.16.30.1/31 | Site1-BGW1 | Ethernet5/1 | 172.16.30.0/31 |
| DCI-1 | Ethernet2/1 | 172.16.30.7/31 | Site1-BGW2 | Ethernet5/1 | 172.16.30.6/31 |
| DCI-1 | Ethernet3/1 | 172.16.30.13/31 | Site1-BGW3 | Ethernet5/1 | 172.16.30.12/31 |
| DCI-1 | Ethernet4/1 | 172.16.30.19/31 | Site2-BGW1 | Ethernet5/1 | 172.16.30.18/31 |
| DCI-1 | Ethernet5/1 | 172.16.30.25/31 | Site2-BGW2 | Ethernet5/1 | 172.16.30.24/31 |
| DCI-1 | Ethernet6/1 | 172.16.30.31/31 | Site2-BGW3 | Ethernet5/1 | 172.16.30.30/31 |
| DCI-2 | Ethernet1/1 | 172.16.30.3/31 | Site1-BGW1 | Ethernet6/1 | 172.16.30.2/31 |
| DCI-2 | Ethernet2/1 | 172.16.30.9/31 | Site1-BGW2 | Ethernet6/1 | 172.16.30.8/31 |
| DCI-2 | Ethernet3/1 | 172.16.30.15/31 | Site1-BGW3 | Ethernet6/1 | 172.16.30.14/31 |
| DCI-2 | Ethernet4/1 | 172.16.30.21/31 | Site2-BGW1 | Ethernet6/1 | 172.16.30.20/31 |
| DCI-2 | Ethernet5/1 | 172.16.30.27/31 | Site2-BGW2 | Ethernet6/1 | 172.16.30.26/31 |
| DCI-2 | Ethernet6/1 | 172.16.30.33/31 | Site2-BGW3 | Ethernet6/1 | 172.16.30.32/31 |
| DCI-3 | Ethernet1/1 | 172.16.30.5/31 | Site1-BGW1 | Ethernet7/1 | 172.16.30.4/31 |
| DCI-3 | Ethernet2/1 | 172.16.30.11/31 | Site1-BGW2 | Ethernet7/1 | 172.16.30.10/31 |
| DCI-3 | Ethernet3/1 | 172.16.30.17/31 | Site1-BGW3 | Ethernet7/1 | 172.16.30.16/31 |
| DCI-3 | Ethernet4/1 | 172.16.30.23/31 | Site2-BGW1 | Ethernet7/1 | 172.16.30.22/31 |
| DCI-3 | Ethernet5/1 | 172.16.30.29/31 | Site2-BGW2 | Ethernet7/1 | 172.16.30.28/31 |
| DCI-3 | Ethernet6/1 | 172.16.30.35/31 | Site2-BGW3 | Ethernet7/1 | 172.16.30.34/31 |
| Site1-BGW1 | Ethernet51/1 | 172.30.255.85/31 | Site1-S1 | Ethernet5/1 | 172.30.255.84/31 |
| Site1-BGW1 | Ethernet52/1 | 172.30.255.87/31 | Site1-S2 | Ethernet5/1 | 172.30.255.86/31 |
| Site1-BGW1 | Ethernet53/1 | 172.30.255.89/31 | Site1-S3 | Ethernet5/1 | 172.30.255.88/31 |
| Site1-BGW2 | Ethernet51/1 | 172.30.255.91/31 | Site1-S1 | Ethernet6/1 | 172.30.255.90/31 |
| Site1-BGW2 | Ethernet52/1 | 172.30.255.93/31 | Site1-S2 | Ethernet6/1 | 172.30.255.92/31 |
| Site1-BGW2 | Ethernet53/1 | 172.30.255.95/31 | Site1-S3 | Ethernet6/1 | 172.30.255.94/31 |
| Site1-BGW3 | Ethernet51/1 | 172.30.255.97/31 | Site1-S1 | Ethernet7/1 | 172.30.255.96/31 |
| Site1-BGW3 | Ethernet52/1 | 172.30.255.99/31 | Site1-S2 | Ethernet7/1 | 172.30.255.98/31 |
| Site1-BGW3 | Ethernet53/1 | 172.30.255.101/31 | Site1-S3 | Ethernet7/1 | 172.30.255.100/31 |
| Site1-L1 | Ethernet51/1 | 172.30.255.61/31 | Site1-S1 | Ethernet1/1 | 172.30.255.60/31 |
| Site1-L1 | Ethernet52/1 | 172.30.255.63/31 | Site1-S2 | Ethernet1/1 | 172.30.255.62/31 |
| Site1-L1 | Ethernet53/1 | 172.30.255.65/31 | Site1-S3 | Ethernet1/1 | 172.30.255.64/31 |
| Site1-L2 | Ethernet51/1 | 172.30.255.67/31 | Site1-S1 | Ethernet2/1 | 172.30.255.66/31 |
| Site1-L2 | Ethernet52/1 | 172.30.255.69/31 | Site1-S2 | Ethernet2/1 | 172.30.255.68/31 |
| Site1-L2 | Ethernet53/1 | 172.30.255.71/31 | Site1-S3 | Ethernet2/1 | 172.30.255.70/31 |
| Site1-L3 | Ethernet51/1 | 172.30.255.73/31 | Site1-S1 | Ethernet3/1 | 172.30.255.72/31 |
| Site1-L3 | Ethernet52/1 | 172.30.255.75/31 | Site1-S2 | Ethernet3/1 | 172.30.255.74/31 |
| Site1-L3 | Ethernet53/1 | 172.30.255.77/31 | Site1-S3 | Ethernet3/1 | 172.30.255.76/31 |
| Site1-L4 | Ethernet51/1 | 172.30.255.79/31 | Site1-S1 | Ethernet4/1 | 172.30.255.78/31 |
| Site1-L4 | Ethernet52/1 | 172.30.255.81/31 | Site1-S2 | Ethernet4/1 | 172.30.255.80/31 |
| Site1-L4 | Ethernet53/1 | 172.30.255.83/31 | Site1-S3 | Ethernet4/1 | 172.30.255.82/31 |
| Site2-BGW1 | Ethernet51/1 | 172.32.255.145/31 | Site2-S1 | Ethernet5/1 | 172.32.255.144/31 |
| Site2-BGW1 | Ethernet52/1 | 172.32.255.147/31 | Site2-S2 | Ethernet5/1 | 172.32.255.146/31 |
| Site2-BGW1 | Ethernet53/1 | 172.32.255.149/31 | Site2-S3 | Ethernet5/1 | 172.32.255.148/31 |
| Site2-BGW2 | Ethernet51/1 | 172.32.255.151/31 | Site2-S1 | Ethernet6/1 | 172.32.255.150/31 |
| Site2-BGW2 | Ethernet52/1 | 172.32.255.153/31 | Site2-S2 | Ethernet6/1 | 172.32.255.152/31 |
| Site2-BGW2 | Ethernet53/1 | 172.32.255.155/31 | Site2-S3 | Ethernet6/1 | 172.32.255.154/31 |
| Site2-BGW3 | Ethernet51/1 | 172.32.255.157/31 | Site2-S1 | Ethernet7/1 | 172.32.255.156/31 |
| Site2-BGW3 | Ethernet52/1 | 172.32.255.159/31 | Site2-S2 | Ethernet7/1 | 172.32.255.158/31 |
| Site2-BGW3 | Ethernet53/1 | 172.32.255.161/31 | Site2-S3 | Ethernet7/1 | 172.32.255.160/31 |
| Site2-L1 | Ethernet51/1 | 172.32.255.121/31 | Site2-S1 | Ethernet1/1 | 172.32.255.120/31 |
| Site2-L1 | Ethernet52/1 | 172.32.255.123/31 | Site2-S2 | Ethernet1/1 | 172.32.255.122/31 |
| Site2-L1 | Ethernet53/1 | 172.32.255.125/31 | Site2-S3 | Ethernet1/1 | 172.32.255.124/31 |
| Site2-L2 | Ethernet51/1 | 172.32.255.127/31 | Site2-S1 | Ethernet2/1 | 172.32.255.126/31 |
| Site2-L2 | Ethernet52/1 | 172.32.255.129/31 | Site2-S2 | Ethernet2/1 | 172.32.255.128/31 |
| Site2-L2 | Ethernet53/1 | 172.32.255.131/31 | Site2-S3 | Ethernet2/1 | 172.32.255.130/31 |
| Site2-L3 | Ethernet51/1 | 172.32.255.133/31 | Site2-S1 | Ethernet3/1 | 172.32.255.132/31 |
| Site2-L3 | Ethernet52/1 | 172.32.255.135/31 | Site2-S2 | Ethernet3/1 | 172.32.255.134/31 |
| Site2-L3 | Ethernet53/1 | 172.32.255.137/31 | Site2-S3 | Ethernet3/1 | 172.32.255.136/31 |
| Site2-L4 | Ethernet51/1 | 172.32.255.139/31 | Site2-S1 | Ethernet4/1 | 172.32.255.138/31 |
| Site2-L4 | Ethernet52/1 | 172.32.255.141/31 | Site2-S2 | Ethernet4/1 | 172.32.255.140/31 |
| Site2-L4 | Ethernet53/1 | 172.32.255.143/31 | Site2-S3 | Ethernet4/1 | 172.32.255.142/31 |

### Loopback Interfaces (BGP EVPN Peering)

| Loopback Pool | Available Addresses | Assigned addresses | Assigned Address % |
| ------------- | ------------------- | ------------------ | ------------------ |
| 192.0.255.0/24 | 256 | 10 | 3.91 % |
| 192.2.255.0/24 | 256 | 10 | 3.91 % |
| 192.168.250.0/24 | 256 | 3 | 1.18 % |

### Loopback0 Interfaces Node Allocation

| POD | Node | Loopback0 |
| --- | ---- | --------- |
| ATD_MGMT | DCI-1 | 192.168.250.1/32 |
| ATD_MGMT | DCI-2 | 192.168.250.2/32 |
| ATD_MGMT | DCI-3 | 192.168.250.3/32 |
| ATD_MGMT | Site1-BGW1 | 192.0.255.17/32 |
| ATD_MGMT | Site1-BGW2 | 192.0.255.18/32 |
| ATD_MGMT | Site1-BGW3 | 192.0.255.19/32 |
| ATD_MGMT | Site1-L1 | 192.0.255.13/32 |
| ATD_MGMT | Site1-L2 | 192.0.255.14/32 |
| ATD_MGMT | Site1-L3 | 192.0.255.15/32 |
| ATD_MGMT | Site1-L4 | 192.0.255.16/32 |
| ATD_MGMT | Site1-S1 | 192.0.255.1/32 |
| ATD_MGMT | Site1-S2 | 192.0.255.2/32 |
| ATD_MGMT | Site1-S3 | 192.0.255.3/32 |
| ATD_MGMT | Site2-BGW1 | 192.2.255.27/32 |
| ATD_MGMT | Site2-BGW2 | 192.2.255.28/32 |
| ATD_MGMT | Site2-BGW3 | 192.2.255.29/32 |
| ATD_MGMT | Site2-L1 | 192.2.255.23/32 |
| ATD_MGMT | Site2-L2 | 192.2.255.24/32 |
| ATD_MGMT | Site2-L3 | 192.2.255.25/32 |
| ATD_MGMT | Site2-L4 | 192.2.255.26/32 |
| ATD_MGMT | Site2-S1 | 192.2.255.1/32 |
| ATD_MGMT | Site2-S2 | 192.2.255.2/32 |
| ATD_MGMT | Site2-S3 | 192.2.255.3/32 |

### VTEP Loopback VXLAN Tunnel Source Interfaces (VTEPs Only)

| VTEP Loopback Pool | Available Addresses | Assigned addresses | Assigned Address % |
| ------------------ | ------------------- | ------------------ | ------------------ |
| 192.0.254.0/24 | 256 | 7 | 2.74 % |
| 192.2.254.0/24 | 256 | 7 | 2.74 % |

### VTEP Loopback Node allocation

| POD | Node | Loopback1 |
| --- | ---- | --------- |
| ATD_MGMT | Site1-BGW1 | 192.0.254.17/32 |
| ATD_MGMT | Site1-BGW2 | 192.0.254.18/32 |
| ATD_MGMT | Site1-BGW3 | 192.0.254.19/32 |
| ATD_MGMT | Site1-L1 | 192.0.254.13/32 |
| ATD_MGMT | Site1-L2 | 192.0.254.14/32 |
| ATD_MGMT | Site1-L3 | 192.0.254.15/32 |
| ATD_MGMT | Site1-L4 | 192.0.254.15/32 |
| ATD_MGMT | Site2-BGW1 | 192.2.254.27/32 |
| ATD_MGMT | Site2-BGW2 | 192.2.254.28/32 |
| ATD_MGMT | Site2-BGW3 | 192.2.254.29/32 |
| ATD_MGMT | Site2-L1 | 192.2.254.23/32 |
| ATD_MGMT | Site2-L2 | 192.2.254.24/32 |
| ATD_MGMT | Site2-L3 | 192.2.254.25/32 |
| ATD_MGMT | Site2-L4 | 192.2.254.25/32 |

## Connected Endpoints

### Connected Endpoint Keys

| Key | Type | Description |
| --- | ---- | ----------- |
| servers | server | Server |

### Servers

| Name | Port | Fabric Device | Fabric Port | Description | Shutdown | Mode | Access VLAN | Trunk Allowed VLANs | Profile |
| ---- | ---- | ------------- | ------------| ----------- | -------- | ---- | ----------- | ------------------- | ------- |
| Site1-L3=Site1-L4=vPC1 | NIC1 | Site1-L3 | Ethernet1 | SERVER_Site1-L3=Site1-L4=vPC1_NIC1 | False | trunk | - | 20 | int_vpc_trunk_host |
| Site1-L3=Site1-L4=vPC1 | NIC2 | Site1-L4 | Ethernet1 | SERVER_Site1-L3=Site1-L4=vPC1_NIC2 | False | trunk | - | 20 | int_vpc_trunk_host |
| Site1-L3=Site1-L4=vPC2 | NIC1 | Site1-L3 | Ethernet2 | SERVER_Site1-L3=Site1-L4=vPC2_NIC1 | False | trunk | - | 20 | int_vpc_trunk_host |
| Site1-L3=Site1-L4=vPC2 | NIC2 | Site1-L4 | Ethernet2 | SERVER_Site1-L3=Site1-L4=vPC2_NIC2 | False | trunk | - | 20 | int_vpc_trunk_host |
| Site2-L3=Site2-L4=vPC1 | NIC1 | Site2-L3 | Ethernet1 | SERVER_Site2-L3=Site2-L4=vPC1_NIC1 | False | trunk | - | 20 | int_vpc_trunk_host |
| Site2-L3=Site2-L4=vPC1 | NIC2 | Site2-L4 | Ethernet1 | SERVER_Site2-L3=Site2-L4=vPC1_NIC2 | False | trunk | - | 20 | int_vpc_trunk_host |
| Site2-L3=Site2-L4=vPC2 | NIC1 | Site2-L3 | Ethernet2 | SERVER_Site2-L3=Site2-L4=vPC2_NIC1 | False | trunk | - | 20 | int_vpc_trunk_host |
| Site2-L3=Site2-L4=vPC2 | NIC2 | Site2-L4 | Ethernet2 | SERVER_Site2-L3=Site2-L4=vPC2_NIC2 | False | trunk | - | 20 | int_vpc_trunk_host |

### Port Profiles

| Profile Name | Parent Profile |
| ------------ | -------------- |
| int_access_host | - |
| int_routed_host | - |
| int_trunk_host | - |
| int_vpc_trunk_host | - |
