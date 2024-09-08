# Terminology Glossary for Networking

[A](#a) | [B](#b) | [C](#c) | [D](#d) | [E](#e) | [F](#f) | [G](#g) | [H](#h) |
[I](#i) | [J](#j) | [K](#k) | [L](#l) | [M](#m) | [N](#n) | [O](#o) | [P](#p) |
[Q](#q) | [R](#r) | [S](#s) | [T](#t) | [U](#u) | [V](#v) | [W](#w) | [X](#x) |
[Y](#y) | [Z](#z)

## Table of Contents

- [A](#a)
- [B](#b)
    - [BOOTP](#bootp)
- [D](#d)
    - [DHCP](#dhcp)
- [N](#n)
    - [Name Server](#name-server)
- [S](#s)
    - [Subnet Mask](#subnet-mask)

## A

### Access Port

An access port refers to a switch port providing access to a single VLAN, where
the frames are not tagged with an 802.1Q header.  Normal client-type devices are
connected to access ports, which will comprise the majority of switch ports.
Devices on access ports do not need knowledge of VLANs or tagging.  They see the
network on their port the same way they would a switch without VLANs.

## B

### BOOTP

Bootstrap Protocol

> [!NOTE]
> The Bootstrap Protocol (BOOTP) [RFC951](https://www.iana.org/go/rfc951)
> describes an IP/UDP bootstrap protocol (BOOTP) which allows a diskless
> client machine to discover its own IP address, the address of a server host,
> and the name of a file to be loaded into memory and executed.
>
> The document "DHCP Options and BOOTP Vendor Information Extensions"
> [RFC2132](https://www.iana.org/go/rfc2132) describes options for
> DHCP, some of which can also be used with BOOTP.

## C

## D

### DHCP

Dynamic Host Configuration Protocol

> [!NOTE]
> The Dynamic Host Configuration Protocol (DHCP)
> [RFC2131](https://www.iana.org/go/rfc2131) provides a framework for
> automatic configuration of IP hosts.
>
> The document "DHCP Options and BOOTP Vendor Information Extensions"
> [RFC2132](https://www.iana.org/go/rfc2132) describes options for
> DHCP, some of which can also be used with BOOTP.
>
> Additional DHCP options are described in other RFCs,
> as documented in [this](https://www.iana.org/assignments/bootp-dhcp-parameters/bootp-dhcp-parameters.xhtml#options) registry.

#### Time Server Option

See:

- [RFC 2132 (3.6)](https://www.rfc-editor.org/rfc/rfc2132.html#section-3.6)

The [time server](#time-server) option specifies a list of
RFC 868 time servers available to the client. Servers SHOULD
be listed in order of preference.

The code for the time server option is 4. The minimum length
for this option is 4 octets, and the length MUST always be a
multiple of 4.

```
    Code   Len         Address 1               Address 2
   +-----+-----+-----+-----+-----+-----+-----+-----+--
   |  4  |  n  |  a1 |  a2 |  a3 |  a4 |  a1 |  a2 |  ...
   +-----+-----+-----+-----+-----+-----+-----+-----+--
```

#### Name Server Option

See:

- [RFC 2132 (3.7)](https://www.rfc-editor.org/rfc/rfc2132.html#section-3.7)


The [name server](#name-server) option specifies a list of
IEN 116 name servers available to the client. Servers
SHOULD be listed in order of preference.

The code for the name server option is 5. The minimum length
for this option is 4 octets, and the length MUST always be
a multiple of 4.

```
    Code   Len         Address 1               Address 2
   +-----+-----+-----+-----+-----+-----+-----+-----+--
   |  5  |  n  |  a1 |  a2 |  a3 |  a4 |  a1 |  a2 |  ...
   +-----+-----+-----+-----+-----+-----+-----+-----+--
```

## E

## F

## G

## H

## I

## J

## K

## L

## M

## N

### Name Server

## O

## P

### Parent Interface

The physical interface where a VLAN resides is known as its Parent Interface.
For example, igb0 or igc0.  When VLANs are configured on pfSense, each is
assigned a virtual interface.  The virtual interface named is crafted by
combining the parent interface plus the VLAN ID.  For example, for VLAN 20 on
igb0, the interface name is "igb0_vlan20".

> [!NOTE]
> The sole function of the parent interface is, ideally, to be the parent for
> the defined VLANs and not used directly.  In some situations this will work,
> but can cause difficulties with switch configuration, and it requires use of
> the default VLAN on the trunk port, which is best to avoid.

### Private VLAN (PVLAN)

PVLAN, sometimes called Port Isolation, refers to capabilities of some switches
to segment hosts within a single VLAN.  Normally hosts within a single VLAN
function the same as hosts on a single switch without VLANs configured.  PVLAN
provides a means of preventing hosts on a VLAN from talking to any other host on
that VLAN, only permitting communication between that host and its default
gateway.  Switch functionality such as this is the only way to prevent
communication between hosts in the same subnet.  Without a function like PVLAN,
no network firewall can control traffic within a subnet because it never touches
the default gateway.

## Q

### QinQ (Double Tagging)

QinQ refers to the double tagging of traffic, using both an outer and inner
802.1Q tag.  This can be useful in large ISP environments, other very large
networks, or networks that must carry multiple VLANs across a link that only
supports a single VLAN tag.  Triple tagging is also possible.
w
## R

## S

### Subnet Mask

See:

- [RFC 2132 | DHCP Options and BOOTP Vendor Extensions (3.3)](https://www.rfc-editor.org/rfc/rfc2132.html#section-3.3)
- [RFC 950 | Internet Standard Subnetting Procedure](https://www.rfc-editor.org/rfc/rfc950)

The subnet mask option specifies the client's subnet mask as per RFC 950.

If both the subnet mask and the router option are specified in a DHCP reply,
the subnet mask option MUST be first.

The code for the subnet mask option is 1, and its length is 4 octets.

     Code   Len        Subnet Mask
    +-----+-----+-----+-----+-----+-----+
    |  1  |  4  |  m1 |  m2 |  m3 |  m4 |
    +-----+-----+-----+-----+-----+-----+

## T

### Time Server

See:

- [RFC 868](https://www.rfc-editor.org/rfc/rfc868)

The use of time-servers makes it possible to quickly confirm
or correct a system's idea of the time, by making a brief
poll of several independent sites on the network.

When used via TCP the time service works as follows:

- S: Listen on port 37 (45 octal).
- U: Connect to port 37.
- S: Send the time as a 32 bit binary number.
- U: Receive the time.
- U: Close the connection.
- S: Close the connection.

The server listens for a connection on port 37. When the connection
is established, the server returns a 32-bit time value and closes the
connection. If the server is unable to determine the time at its
site, it should either refuse the connection or close it without
sending anything.

When used via UDP the time service works as follows:

- S: Listen on port 37 (45 octal).
- U: Send an empty datagram to port 37.
- S: Receive the empty datagram.
- S: Send a datagram containing the time as a 32 bit binary number.
- U: Receive the time datagram.

The server listens for a datagram on port 37.  When a datagram
arrives, the server returns a datagram containing the 32-bit time
value.  If the server is unable to determine the time at its site,
it should discard the arriving datagram and make no reply.

The Time

The time is the number of seconds since 00:00 (midnight) 1 January 1900
GMT, such that the time 1 is 12:00:01 am on 1 January 1900 GMT; this
base will serve until the year 2036.

For example:

```
   the time  2,208,988,800 corresponds to 00:00  1 Jan 1970 GMT,

             2,398,291,200 corresponds to 00:00  1 Jan 1976 GMT,

             2,524,521,600 corresponds to 00:00  1 Jan 1980 GMT,

             2,629,584,000 corresponds to 00:00  1 May 1983 GMT,

        and -1,297,728,000 corresponds to 00:00 17 Nov 1858 GMT.
```

### Trunking

Trunking refers to a means of carrying multiple VLANs on the same physical port
switch.  The frames leaving a trunk port are marked with an 802.1Q tag in the
header, enabling the connected device to differentiate between multiple VLANs.
Trunk ports are used to connect multiple switches, and for connecting any
devices that are capable of 802.1Q tagging and require access to multiple VLANs.
This is commonly limited to the firewall or router providing connectivity
between VLANs, as well as any connections to other switches containing multiple
VLANs.

Reference: [pfSense Documentation](https://docs.netgate.com/manuals/pfsense/en/latest/the-pfsense-documentation.pdf)

## U

## V

### VLAN ID

Each VLAN has an identifier number (ID) for distinguishing tagged traffic. This is a number between 1 and 4094.

> [!WARNING] The default VLAN on switches is 1, and this VLAN should not be
> used when deploying VLAN trunking.

Aside from avoiding the use of VLAN 1, VLAN numbers may be chosen at will.  Some
designs start with VLAN 2 and increment by one until the number of VLANs is
reached.  Another common design is to use the third octet in the subnet of the
VLAN as the VLAN ID.

For example, if the environment contains the network `10.0.10.0/24`,
`10.0.20.0/24`, and `10.0.30.0/24`, it is logical to use VLANs 10, 20, and 30
respectively.  Choose a VLAN ID assignment scheme that makes sense for a given
network design.

## W

## X

## Y

## Z
