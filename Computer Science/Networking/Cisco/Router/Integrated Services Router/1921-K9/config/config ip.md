# Commands extracted from Cisco 1921/K9

[Cisco 1921/K9 Data Sheet](https://www.cisco.com/c/en/us/products/collateral/routers/1900-series-integrated-services-routers-isr/data_sheet_c78-598389.html)

```
ROUTER> enable
password: ...
ROUTER# configure terminal
ROUTER(config)#ip <subcommand>
```

|  Sub Command  | Description |
| ------------- | ----------- |
| access-list | Named access-list |
| accounting-list | Select hosts for which IP accounting information is kept |
| accounting-threshold | Sets the maximum number of accounting entries |
| accounting-transits | Sets the maximum number of transit entries |
| address-pool | Specify default IP address pooling mechanism |
| alias | Alias an IP address to a TCP port |
| arp | IP ARP global configuration |
| as-path | BGP autonomous system path filter |
| bgp-community | format for BGP community |
| bootp | Config BOOTP services |
| cef | Cisco Express Forwarding |
| classless | Follow classless routing forwarding rules |
| community-list | Add a community list entry |
| ddns | Configure dynamic DNS |
| default-gateway | Specify default gateway (if not routing IP) |
| default-network | Flags networks as candidates for default routes |
| device | Device tracking |
| dfp | DFP configuration |
| dhcp | Configure DHCP server and relay parameters |
| dhcp-client | Configure parameters for DHCP client operation |
| dhcp-server | Specify target DHCP server parameters |
| dns | Configure DNS server for a zone |
| domain | IP DNS Resolver |
| domain-list | Domain name to complete unqualified host names |
| domain-lookup | Enable IP Domain Name System hostname translation |
| domain-name | Define the default domain name |
| drp | Director response protocol configuration commands |
| explicit-path | Configure explicit path |
| extcommunity-list | Add an extended community list entry |
| finger | finger server |
| flow-aggregation | Configure flow aggregation |
| flow-cache | Configure netflow cache parameters |
| flow-capture | Capture additional netflow information |
| flow-egress | Configure netflow egress |
| flow-export | Specify host/port to send flow statistics |
| flow-top-talkers | Configure netflow top talkers |
| forward-protocol | Controls forwarding of physical and directed IP broadcasts |
| ftp | FTP configuration commands |
| gdp | Router discovery mechanism |
| gratuitous-arps | Generate gratuitous ARPs for PPP/SLIP peer addresses |
| host | Add an entry to the ip hostname table |
| host-list | Configure a host list |
| host-routing | Enable host-based routing (proxy ARP and redirect) |
| hostname | Configure hostname types |
| hp-host | Enable the HP proxy probe service |
| http | HTTP server configuration |
| icmp | ICMP options |
| identd | Ident server |
| igmp | IGMP global configuration |
| ldap | LDAP configuration commands |
| local | Specify local options |
| mfib | Multicast Forwarding |
| mobile | Enable Mobile IP services |
| mrm | Configure IP Multicast Routing Monitor test parameters |
| mroute | Configure static multicast routes |
| msdp | MSDP global commands |
| multicast | Global IP Multicast Commands |
| multicast-routing | Enable IP multicast forwarding |
| mux | IP Multiplex configuration commands |
| name-server | Specify address of name server to use |
| nat | NAT configuration commands |
| nbar | NBAR - Network Based Application Recognition |
| options | IP Options treatment |
| ospf | OSPF |
| pgm | PGM Reliable Transport Protocol |
| pim | PIM global commands |
| policy-list | Define IP Policy list |
| port-map | Port to application mapping (PAM) configuration commands |
| prefix-list | Build a prefix list |
| radius | RADIUS configuration commands |
| rcmd | Rcmd commands |
| reflexive-list | Reflexive access list |
| [`route`](#config-ip-route) | Establish static routes |
| routing | Enable IP routing |
| rsvp | Configure static RSVP information |
| rtcp | RTCP parameters |
| sap | Global IP Multicast SAP Commands |
| scp | Scp commands |
| sctp | Global SCTP parameters |
| security | Specify system wide security information |
| sla | IP Service Level Agreement |
| source-route | Process packets with source routing header options |
| ssh | Configure ssh options |
| subnet-zero | Allow "subnet zero" subnets |
| tacacs | TACACS configuration commands |
| tcp | Global TCP parameters |
| telnet | Specify telnet options |
| tftp | tftp configuration commands |
| traffic-export | IP traffic export configuration commands |
| trigger-authentication | Trigger-authentication configurations parameters |
| udptn | UDPTN configuration commands |
| verify | URPF SNMP trap and IP packet header validation command |
| vrf | Configure an IP VPN Routing/Forwarding instance |
| wccp | Web-Cache Coordination Protocol IPv4 Commands |

## `ip route`

```
ROUTER(config)#ip route <subcommand>
```

|  Sub Command  | Description |
| ------------- | ----------- |
| A.B.C.D | Destination prefix |
| profile | Enable IP routing profile |
| static | Allow static routes |
| vrf | Configure static route for a VPN Routing/Forwarding instance |

### GATEWAY OF LAST RESORT

```
ROUTER(config)#ip route 0.0.0.0 0.0.0.0 <next-hop-IP>
```

### `ip route profile`

```
ROUTER(config)#ip route profile <cr>
```

## `ip ssh`

```
ROUTER(config)# ip ssh <sub-command>
```

|  Sub Command  | Description |
| ------------- | ----------- |
| authentication-retries | Specify number of authentication retries |
| break-string | break-string |
| client | Configuration for client |
| dh | Diffie-Hellman |
| dscp | IP DSCP value for SSH traffic |
| logging | Configure logging for SSH |
| maxstartups | Maximum concurrent sesions allowed |
| port | Starting (or only) port number to listen on |
| precedence | IP Precedence value for SSH traffic |
| pubkey-chain | pubkey-chain |
| rsa | Configure RSA keypair name for SSH |
| server | Configuration for server |
| source-interface | Specify interface for source address in SSH connections |
| stricthostkeycheck | Enable SSH Server Authentication |
| time-out | Specify SSH time-out interval |
| version | Specify protocol version to be supported |

### `ip ssh client`

```
ROUTER(config)# ip ssh client algorithm <encryption | mac>
```
