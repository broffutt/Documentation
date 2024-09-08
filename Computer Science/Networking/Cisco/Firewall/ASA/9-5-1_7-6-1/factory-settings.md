# Cisco ASA-5508-X Factory Default Settings

## Table of Contents

- [Displayed on First Boot](#displayed-on-first-boot)
    - [Licensed features for this platform](#licensed-features-for-this-platform)
    - [Encryption Hardware Device](#encryption-hardware-device)
- [Configuration After First Boot](#configuration-after-first-boot)

## Displayed on First Boot

The following are the features I have present on my machine after a factory
reset. This displays during first boot, before the Power-On Self Test (POST).

Your command availability may vary:

### Licensed features for this platform

```
   Maximum Physical Interfaces       : Unlimited      perpetual
   Maximum VLANs                     : 50             perpetual
   Inside Hosts                      : Unlimited      perpetual
   Failover                          : Active/Active  perpetual
   Encryption-DES                    : Enabled        perpetual
   Encryption-3DES-AES               : Enabled        perpetual
   Security Contexts                 : 2              perpetual
   GTP/GPRS                          : Disabled       perpetual
   AnyConnect Premium Peers          : 4              perpetual
   AnyConnect Essentials             : Disabled       perpetual
   Other VPN Peers                   : 100            perpetual
   Total VPN Peers                   : 100            perpetual
   Shared License                    : Disabled       perpetual
   AnyConnect for Mobile             : Disabled       perpetual
   AnyConnect for Cisco VPN Phone    : Disabled       perpetual
   Advanced Endpoint Assessment      : Disabled       perpetual
   Total UC Proxy Sessions           : 320            perpetual
   Botnet Traffic Filter             : Disabled       perpetual
   Cluster                           : Disabled       perpetual
   VPN Load Balancing                : Enabled        perpetual
```

### Encryption hardware device

Cisco ASA Crypto on-board accelerator

## Configuration After First Boot

To obtain the initial configuration, perform the following:

```
ciscoasa> enable
ciscoasa# configure terminal
  ** You are prompted to enable/disable call-home here. I opted out. **
ciscoasa(config)# write terminal
```

See [call-home](call-home.md) for the initial `configure terminal` prompt.

My factory default settings are as follows:

> [!NOTE]
> Anything that states `<REDACTED>` is potentially compromising information
> and is not provided here but there should be content on your end.

```
: Serial Number: <REDACTED>
: Hardware:   ASA5508, 8192 MB RAM, CPU Atom C2000 series 2000 MHz, 1 CPU (8 cores)
:
ASA Version 9.5(1)
!
hostname ciscoasa
enable password <REDACTED> encrypted
names
!
interface GigabitEthernet1/1
 nameif outside
 security-level 0
 ip address dhcp setroute
!
interface GigabitEthernet1/2
 nameif inside
 security-level 100
 ip address 192.168.1.1 255.255.255.0
!
interface GigabitEthernet1/3
 shutdown
 no nameif
 no security-level
 no ip address
!
interface GigabitEthernet1/4
 shutdown
 no nameif
 no security-level
 no ip address
!
interface GigabitEthernet1/5
 shutdown
 no nameif
 no security-level
 no ip address
!
interface GigabitEthernet1/6
 shutdown
 no nameif
 no security-level
 no ip address
!
interface GigabitEthernet1/7
 shutdown
 no nameif
 no security-level
 no ip address
!
interface GigabitEthernet1/8
 shutdown
 no nameif
 no security-level
 no ip address
!
interface Management1/1
 management-only
 no nameif
 no security-level
 no ip address
!
ftp mode passive
object network obj_any
 subnet 0.0.0.0 0.0.0.0
pager lines 24
logging asdm informational
mtu outside 1500
mtu inside 1500
no failover
no monitor-interface service-module
icmp unreachable rate-limit 1 burst-size 1
no asdm history enable
arp timeout 14400
no arp permit-nonconnected
!
object network obj_any
 nat (any,outside) dynamic interface
timeout xlate 3:00:00
timeout pat-xlate 0:00:30
timeout conn 1:00:00 half-closed 0:10:00 udp 0:02:00 icmp 0:00:02
timeout sunrpc 0:10:00 h323 0:05:00 h225 1:00:00 mgcp 0:05:00 mgcp-pat 0:05:00
timeout sip 0:30:00 sip_media 0:02:00 sip-invite 0:03:00 sip-disconnect 0:02:00
timeout sip-provisional-media 0:02:00 uauth 0:05:00 absolute
timeout tcp-proxy-reassembly 0:01:00
timeout floating-conn 0:00:00
user-identity default-domain LOCAL
http server enable
http 192.168.1.0 255.255.255.0 inside
no snmp-server location
no snmp-server contact
service sw-reset-button
crypto ipsec security-association pmtu-aging infinite
crypto ca trustpool policy
telnet timeout 5
no ssh stricthostkeycheck
ssh timeout 5
ssh key-exchange group dh-group1-sha1
console timeout 0

dhcpd auto_config outside
!
dhcpd address 192.168.1.5-192.168.1.254 inside
dhcpd enable inside
!
threat-detection basic-threat
threat-detection statistics access-list
no threat-detection statistics tcp-intercept
dynamic-access-policy-record DfltAccessPolicy
!
class-map inspection_default
 match default-inspection-traffic
!
!
policy-map type inspect dns preset_dns_map
 parameters
  message-length maximum client auto
  message-length maximum 512
policy-map global_policy
 class inspection_default
  inspect dns preset_dns_map
  inspect ftp
  inspect h323 h225
  inspect h323 ras
  inspect rsh
  inspect rtsp
  inspect esmtp
  inspect sqlnet
  inspect skinny
  inspect sunrpc
  inspect xdmcp
  inspect sip
  inspect netbios
  inspect tftp
  inspect ip-options
!
service-policy global_policy global
prompt hostname context
no call-home reporting anonymous
Cryptochecksum:<REDACTED>
: end
[OK]
```

### Default SSH

After a factory reset, there is a Key-Pair that is automatically generated
called `<Default-RSA-Key>`.

```
ciscoasa(config)# show crypto key mypubkey rsa
Key pair was generated at: 21:24:03 UTC Jun 27 2018
Key name: <Default-RSA-Key>
 Usage: General Purpose Key
 Modulus Size (bits): 2048
 Key Data:

  <REDACTED>
```
