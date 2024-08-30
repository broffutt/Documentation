# `interface`

|    Command    | Description |
| ------------- | ----------- |
| [`GigabitEthernet`](#gigabitethernet) | GigabitEthernet IEEE 802.3z |
| Management | Management interface |
| Port-channel | Ethernet Channel of interfaces |
| Redundant | Reduntant Interface |
| vni | VNI Interface |
| `<cr>` | |

## `GigabitEthernet`

```
ciscoasa(config)# interface GigabitEthernet 1/1
```

|    Command    | Description |
| ------------- | ----------- |
| authentication | authentication subcommands |
| channel-group | Etherchannel/port bundling configuration |
| cts | Configure interface specific CTS settings |
| ddns | Configure Dynamic DNS |
| default | Set a command to its defaults |
| delay | Specify interface throughput delay |
| description | Interface specific description |
| dhcp | Configure parameters for DHCP client |
| dhcprelay | Configure DHCP Relay Agent |
| duplex | Configure duplex operation |
| exit | Exit from interface configuration mode |
| flowcontrol | Configure flowcontrl operation |
| hello-interval | Configures EIGRP-IPv4 hello interval |
| help | Interactive help for interface commands |
| hold-time | Configures EIGRP-IPv4 hold time |
| igmp | IGMP interface commands |
| ip | Configure the ip address |
| ipv6 | IPv6 interface commands |
| lacp | LACP interface commands |
| mac-address | Assign MAC address to interface |
| management-only | Dedicate an interface to management. Block thru traffic |
| mfib | Interface Specific MFIB Control |
| multicast | Configure multicast routing |
| nameif | Assign name to interface |
| no | Negate a command or set its defaults |
| nve-only | Dedicate an interface to source-interface of an NVE. Block thru traffic |
| ospf | OSPF interface commands |
| pim | PIM interface commands |
| policy-route | Enable policy based routing |
| pppoe | Configure parameters for PPPoE client |
| rip | Router Information Protocol |
| security-level | Specify the security level of this interface after this keyword (e.g., 0, 100, etc.). The relative security level between two interfaces determines the way the Adaptive Security Algorithm is applied. A lower security_level interface is outside relative to a higher level interface and equivalent interfaces are outside to each other |
| shutdown | Shutdown the selected interface |
| speed | Configure speed operation |
| split-horizon | Configures EIGRP-IPv4 split-horizon |
| summary-address | Configures EIGRP-IPv4 summary-address |
| zone-member | Associate interface to a zone |
