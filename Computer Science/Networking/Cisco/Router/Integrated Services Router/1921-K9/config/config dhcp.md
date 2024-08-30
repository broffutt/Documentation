# Commands extracted from Cisco 1921/K9

[Cisco 1921/K9 Data Sheet](https://www.cisco.com/c/en/us/products/collateral/routers/1900-series-integrated-services-routers-isr/data_sheet_c78-598389.html)

```
ROUTER(config)#ip dhcp pool <LINE>
ROUTER(dhcp-config)# ?
```

See: [`config ip dhcp pool`](/Computer%20Science/Networking/Cisco/Router/Integrated%20Services%20Router/1921-K9/config/config%20ip.md#ip-dhcp-pool)

|  Sub Command  | Description |
| ------------- | ----------- |
| [`accounting`](#accounting) | Send Accounting Start/Stop messages |
| bootfile | Boot file name |
| class | Specify a DHCP class |
| client-identifier | Client identifier |
| client-name | Client name |
| [`default-router`](#default-router) | Default routers |
| [`dns-server`](#dns-server) | DNS servers |
| [`domain-name`](#domain-name) | Domain name |
| exit | Exit from DHCP Pool Configuration Mode |
| `hardware-address` | Client hardware address |
| host | Client IP address and mask |
| import | Programatically importing DHCP option parameters |
| lease | Address lease time |
| netbios-name-server | NetBIOS (WINS) Name Servers |
| netbios-node-type | NetBIOS node type |
| network | Network number and mask |
| next-server | Next server in boot process |
| no | Negate a command or set its defaults |
| odap | Configure ODAP |
| option | Raw DHCP options |
| origin | Configure the origin of the pool |
| relay | Function as a DHCP relay |
| remember | Remeber released bindings |
| renew | Configure renewal policy |
| server | Configure the Server ID option value |
| subnet | Subnet allocation commands |
| update | Dynamic updates |
| utilization | Configure various utilization parameters |
| vrf | Associate this pool with a VRF |

## `accounting`

Configure the default router provided to DHCP clients.

```
ROUTER(dhcp-config)# accounting <accounting-list-name: WORD>
```

|  Sub Command  | Description |
| ------------- | ----------- |
| accounting-list-name (WORD) | Named Accounting list |


## `default-router`

Configure the default router provided to DHCP clients.

```
ROUTER(dhcp-config)# default-router <Hostname | A.B.C.D>
```

|  Sub Command  | Description |
| ------------- | ----------- |
| Hostname or [A.B.C.D](/Computer%20Science/Networking/Cisco/cisco-glossary.md#abcd) | Router's name or IP address |

## `dns-server`

Specify DNS servers for dhcp clients to use.

Multiple dns-servers can be provided as alternates.

```
ROUTER(dhcp-config)# dns-server <Hostname or A.B.C.D>
```

|  Sub Command  | Description |
| ------------- | ----------- |
| Hostname or [A.B.C.D](/Computer%20Science/Networking/Cisco/cisco-glossary.md#abcd) | Server's name or IP address |

## `domain-name`

Specify the domain name associated with the DHCP server

```
ROUTER(dhcp-config)# domain-name <domain-identifier: WORD>
```

|  Sub Command  | Description |
| ------------- | ----------- |
| domain-identifier (WORD) | Domain name |


## `hardware-address`

```
ROUTER(dhcp-config)# hardware-address <mac-address: dotted-hex (WORD)> [arp-hw-type: int (0-255)]
```

|  Sub Command  | Description |
| ------------- | ----------- |
| mac-address (WORD) | Dotted-hexadecimal string (aabb.ccdd.eeff ...) |

|  Options  | Description |
| ------------- | ----------- |
| arp-hw-type (0-255) | ARP hardware type from ["Assigned Numbers" RFC](https://www.rfc-editor.org/rfc/rfc3232) |
