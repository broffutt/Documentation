# Cisco ASA-5508-X `ssh` Subcommands

Disconnect a specific SSH session

## `config` mode

```
Usage:
    ssh hostname
    ssh <A.B.C.D> <A.B.C.D> (inside | outside)
    ssh <X:X:X:X::X>/<0-128>
    ssh key-exchange group
    ssh pubkey-chain
    ssh scopy
    ssh stricthostkeycheck
    ssh version <1 | 2>
```

### `ssh (<hostname> | <A.B.C.D A.B.C.D>)`

> The IP address of the host and/or network authorized to login to the system.
>
> Hostname will be some WORD, and the IP address will be some A.B.C.D.
>
> If IP is specified, a network mask MUST also be specified.

### `ssh <X:X:X:X::X>/<0-128>`

Connect to a specific host by IPv6 address.

### `ssh key-exchange`

### `ssh pubkey-chain`

### `ssh scopy`

### `ssh stricthostkeycheck`

### `ssh version <1 | 2>`

Set the SSH version to use.

> [!WARNING]
> If you set the SSH version to 2, you will not be able to connect from
> devices that only support SSH version 1.
