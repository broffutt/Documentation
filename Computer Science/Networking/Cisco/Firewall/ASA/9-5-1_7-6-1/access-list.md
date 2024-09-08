# ASA 9.9.2(1) `access-list` Subcommands

```
ciscoasa> enable
ciscoasa# configure terminal
ciscoasa(config)# access-list ?
```

```
Usage:
    access-list <ID: WORD (<241 Char)>
        access-list <ID> deny
        access-list <ID> ethertype
        access-list <ID> extended
        access-list <ID> line
        access-list <ID> permit
        access-list <ID> remark
        access-list <ID> rename
        access-list <ID> standard
        access-list <ID> webtype
    access-list alert-interval <1-3600>
    access-list deny-flow-max <1-4096>
```

## `access-list <ID: WORD (<241 Char)>`

> Access list identifier. This can be alphanumeric, and can include dashes.

### `access-list <ID> extended`



### `access-list <ID> permit`

```
Usage:
    <0-255>
    <Hostname | A.B.C.D>
    ah
    any4
    eigrp
    esp
    gre
    host
    icmp
        <A.B.C.D>
        <X:X:X:X::X/<0-128>>
        any
        any4
        any6
        host
        interface
        object
        object-group
        object-group-security
        object-group-user
        security-group
        user
        user-group
    icmp6
    igmp
    igrp
    ip
    ipinip
    ipsec
    nos
    object
    object-group
    ospf
    pcp
    pim
    pptp
    sctp
    snp
    tcp
    udp
```

#### `access-list <ID> permit icmp`

```
Usage:
    access-list <ID> permit icmp <A.B.C.D> <A.B.C.D>
    access-list <ID> permit icmp <X:X:X:X::X/<0-128>>
    access-list <ID> permit icmp any
    access-list <ID> permit icmp any4
    access-list <ID> permit icmp any6
    access-list <ID> permit icmp host
    access-list <ID> permit icmp interface
    access-list <ID> permit icmp object
    access-list <ID> permit icmp object-group
    access-list <ID> permit icmp object-group-security
    access-list <ID> permit icmp object-group-user
    access-list <ID> permit icmp security-group
    access-list <ID> permit icmp user
    access-list <ID> permit icmp user-group
```

##### `access-list <ID> permit icmp <A.B.C.D> <A.B.C.D>`

* `ID` - Access list identifier
* `<A.B.C.D>` - IPv4 address
* `<A.B.C.D>` - IPv4 address mask

##### `access-list <ID> permit icmp <X:X:X:X::X/<0-128>>`

##### `access-list <ID> permit icmp any`

##### `access-list <ID> permit icmp any4`

##### `access-list <ID> permit icmp any6`

##### `access-list <ID> permit icmp host`

##### `access-list <ID> permit icmp interface`

##### `access-list <ID> permit icmp object`

##### `access-list <ID> permit icmp object-group`

##### `access-list <ID> permit icmp object-group-security`

##### `access-list <ID> permit icmp object-group-user`

##### `access-list <ID> permit icmp security-group`

##### `access-list <ID> permit icmp user`

##### `access-list <ID> permit icmp user-group`

### `access-list <ID> standard`

1. `access-list <ID> standard (deny | permit) <hostname | A.B.C.D> <A.B.C.D>`
    1. Match based on destination network address and mask.
1. `access-list <ID> standard (deny | permit) any4`
    1. Abbreviation for an address and mask of `0.0.0.0 0.0.0.0`.
1. `access-list <ID> standard (deny | permit) host <hostname | A.B.C.D> <A.B.C.D>`
    1. Match based on destination host address and mask.

### `access-list <ID> webtype`

## `access-list alert-interval`

> Specify the alert interval for generating syslog message 106001 which alerts
> that the system has reached a deny flow maximum.  If not specified, the
> default value is 300 seconds.
>
> Valid values are 1-3600 seconds.

## `access-list deny-flow-max`

> Specify the maximum number of concurrent deny flows that can be created.  If
> not specified, the default value is 4096.
>
> Valid values are 1-4096.
