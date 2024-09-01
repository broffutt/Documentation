# ASA 5508-X config ssh

##

##

###

```
Usage:
    1. ssh <Hostname | (A.B.C.D A.B.C.D)>
    2. ssh <X:X:X:X::X/0-128>
    3. ssh key-exchange <DH-group>
    4. ssh pubkey-chain
        # pubkey-chain enters a new menu. See Usage 4
    5. ssh scopy enable
        5.1. no ssh scopy enable
    6. ssh stricthostkeycheck
    7. ssh timeout <1-60>
    8. ssh version (1 | 2)
```

#### Usage 1 | FQDN OR IPv4

The IP Address of the host and/or network authorized to login to the system.

If giving an IP address, a Base-10 subnet mask MUST also be provided

#### Usage 2 | IPv6

IPv6 address/prefix authorized to login to the system.

#### Usage 3 | Diffie-Hellman Key Exchange Group

Configure the Diffie-Hellman key exchange group to use for SSH.

#### Usage 4 | Public Key Chain

SSH host public keys

#### Usage 5 | Secure Copy

Secure Copy mode

- To enable, use `ciscoasa(config)# ssh scopy enable`
- To disable, use `ciscoasa(config)# no ssh scopy enable`

#### Usage 6 | SSH Strict Host Key Check

SSH strict host key check

#### Usage 7 | SSH Idle Timeout

Configure ssh idle timeout in minutes (1-60).

#### Usage 8 | SSH Version

Specify protocol version to be supported; either version 1 or version 2.
