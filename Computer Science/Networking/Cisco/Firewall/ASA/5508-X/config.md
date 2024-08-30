# `config` Commands from Cisco ASA 5508-X

Also: `configure`

```
ciscoasa(config)# ?
```

|    Command    | Description |
| ------------- | ----------- |
| aaa | Enable, disable, or view user authentication, authorization, and accounting |
| aaa-server | Configure an AAA server group or an AAA server |
| access-group | Bind an access-list to an interface to filter raffic |
| access-list | Configure an access control element |
| arp | Change or view ARP table, set ARP timeout value, view statistics |
| as-path | BGP autonomous system path filter |
| asdm | Configure Device Manager |
| asp | Configure ASP parameters |
| auth-prompt | Customize authentication challenge, rejecttion, or acceptance prompt |
| auto-prompt | Configure Auto Update |
| banner | Configure login/session banners |
| bgp-community | format for BGP community |
| boot | Set system boot parameters |
| ca | Certification Authority |
| call-home | Smart Call-Home Configuration |
| checkheaps | Configure checkheap verification interfals |
| class-map | Configure MPF Class Map |
| clear | Clear |
| client-update | Configure and change client update parameters |
| clock | Configure time-of-day clock |
| cluster | Cluster configuration |
| command-alias | Create command alias |
| community-list | Add a community list entry |
| compression | Configure global Compression parameters |
| config-register | Define the configuration register |
| configure | Configure using various methods |
| console | Serial console functions |
| coredump | Configure Coredump options |
| crashinfo | Enable/Disable writing crashinfo to flash |
| crypto | Configure IPSec, ISAKMP, Certification Authority, Key... |
| ctl-provider | Configure a CTL Provider instance |
| ddns | Configure Dynamic DNS update method |
| dhcp-client | Configure parameters for DHCP client operation |
| dhcpd | Configure DHCP Server |
| dhcprelay | Configure DHCP Relay Agent |
| dns | Add DNS functionality to an interface |
| dns-group | Set the global DNS server group |
| dns-guard | Enforce one DNS response per query |
| domain-name | Change domain name |
| dynamic-access-policy-record | Dynamic Access Policy configuration commands |
| dynamic-filter | Configure Dynamic Filter |
| dynamic-map | Configure crypto dynamic map |
| enable | Configure password for the enable command |
| end | Exit from configure mode |
| established | Allow inbound connections based on established connections |
| event | Configure Event Manager |
| exit | Exit from config mode |
| failover | Enable/disable failover feature |
| filter | Enable/disable URL, FTP, HTTPS, Java, and ActiveX filtering |
| fips | FIPS 140-2 compliance information |
| firewall | Switch to router/transparent mode |
| fixup | Add or delete inspection services |
| flow-export | Configure flow information export through NetFlow |
| forward-reference | Enable forward reference of ACL, Object, and Object-Group names |
| fragment | Configure the IP fragment database |
| ftp | Set FTP mode |
| ftp-map | Configure advanced options for FTP inspection |
| group-delimiter | The delimiter for tunnel-group lookup. |
| group-policy | Configure or remove a group policy |
| gtp-map | Configure advanced options for GTP inspection |
| h225-map | Configure advanced options for H225 inspection |
| help | Interactive help for commands |
| [`hostname`](/Computer%20Science/Networking/Cisco/Firewall/ASA/5508-X/config/hostname.md) | Change the hostname of the system |
| hpm | Configure TopN host statistics collection |
| http | Configure HTTP server and HTTPS related commands |
| http-map | DEPRECATED |
| icmp | Configure access rules for ICMP traffic |
| imap4s | DEPRECATED |
| [`interface`](/Computer%20Science/Networking/Cisco/Firewall/ASA/5508-X/config/interface.md) | Select an interface to configure |
| ip | Configure IP address pools |
| ip | Configure IP addresses, address pools, IDS, etc. |
| ipsec | Configure transform-set, IPSec SA lifetime and PMTU Aging reset timer |
| ipv6 | Configure IPv6 address pools |
| ipv6 | Global IPv6 configuration commands |
| ipv6-vpn-addr-assign | Global settings for VPN IP address assignment policy |
| isakmp | Configure ISAKMP options |
| jumbo-frame | Configure jumbo-frame support |
| key | Create various configuration keys |
| l2tp | Configure Global L2TP Parameters |
| lacp | LACP configuration |
| ldap | Configure LDAP Mapping |
| logging | Configure logging levels, recipients, and other options |
| logout | Logoff from config mode |
| mac-address | MAC address options |
| mac-list | Create a mac-list to filter based on MAC address |
| management-access | Configure management interface |
| map | Configure crypto map |
| mdm-proxy | Configure advanced options for MGCP inspection |
| migrate | Migrate IKEv1 configuration to IKEv2/SSL |
| mode | Toggle between single and multiple security context modes |
| monitor-interface | Enable or disable failover monitoring on a specific interface |
| mount | Configure a system mount |
| mroute | Configure static multicast routes |
| mtu | Specify MTU (Maximum Transmission Unit) for an interface |
| multicast-routing | Enable IP multicast |
| name | Associate a name with an IP address |
| names | Enable/Disable IP address to name mapping |
| nat | Associate a network with a pool of global IP addresses |
| no | Negate a command or set its defaults |
| ntp | Configure NTP |
| nve | Configure a Network Virtualization Endpoint (NVE) |
| object | Configure an object |
| object-group | Create an object group for use in `access-list`, etc. |
| object-group-search | Enables object group search algorithm |
| pager | Control page length for pagination |
| passwd | Change Telnet console access password |
| password | Configure password encryption |
| password-policy | Configure password policy options |
| pim | Configure Protocol Independent Multicast |
| policy-list | Define IP Policy List |
| policy-map | Configure MPF Parameter Map |
| pop3s | DEPRECATED |
| prefix-list | Build a prefix list |
| priority-queue | Enter sub-command mode to set priority-queue attributes |
| privilege | Configure privilege levels for commands |
| prompt | configure session prompt display |
| quit | Exit from config mode |
| quota | Configure quotas |
| regex | Define a regular expression |
| remote-access | Configure SNMP trap threshold for VPN remote-access sessions |
| rest-api | Configure REST API |
| route | Configure a static route for an interface |
| route-map | Create route-map or enter route-map |
| router | Enable a routing process |
| same-security-traffic | Enable same security level interfaces to communicate |
| scansafe | Scansafe configuration |
| service | Configure system services |
| service-policy | Configure MPF service policy |
| setup | Pre-configure the system |
| sla | IP Service Level Agreement |
| smtp-server | Configure default SMTP server address to be used for Email |
| smtps | DEPRECATED |
| snmp | Configure the SNMP options |
| snmp-server | Modify SNMP engine parameters |
| ssh | Configure SSH options |
| ssl | Configure SSL options |
| sunrpc-server | Create SUNRPC services table |
| sysopt | Set system functional options |
| tcp-map | Configure advanced options for TCP inspection |
| telnet | Add telnet access to system console or set idle timeout |
| terminal | Set terminal line parameters |
| tftp-server | Configure default TFTP server address and directory |
| threat-detection | Show threat detection information |
| time-range | Define time range entries |
| timeout | Configure maximum idle times |
| tls-proxy | Confiugre a TLS proxy instance or the maximum sessions |
| track | Object tracking configuration commands |
| tunnel-group | Create and manage the database of connection specific records for IPSec connections |
| tunnel-group-map | Specify policy by which the tunnel-group name is derived from the content of a certificate. |
| url-block | Enable URL pending block buffer and long URL support |
| url-cache | Enable/Disable URL caching |
| url-server | Configure a URL filtering server |
| user-identity | Configure user-identity firewall |
| username | Configure user authentication local database |
| virtual | Configure address for authentication virtual servers |
| vpdn | Configure VPDN feature |
| vpn | Configure VPN parameters |
| vpn-addr-assign | Global settings for VPN IP address assignment policy |
| vpn-sessiondb | Configure the VPN Session Manger |
| vpnclient | Configure and Easy VPN connection |
| vpnsetup | Configure VPN Setup Commands |
| vxlan | Configure VXLAN system parameters |
| wccp | Web-Cache Coordination Protocol Commands |
| webvpn | Configure the WebVPN service |
| xlate | Configure an xlate option |
| zone | Create or show a zone |
| zonelabs-integrity | ZoneLabs integrity Firewall Server Configuration |

