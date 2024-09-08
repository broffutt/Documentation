# Cisco ASA 5508-X `config-ikev2-policy` mode

```
ciscoasa> enable
ciscoasa# configure terminal
ciscoasa(config)# crypto ikev2 policy <1-65535>
```

```
Usage:
    encryption ([3des] | [aes] | [aes-192] | [aes-256] | [aes-gcm] |
                [aes-gcm-192] | [aes-gcm-256] | [des] | [null])...
    exit
    group ([1] | [2] | [5] | [14] | [19] | [20] | [21] | [24])...
    help
    integrity ([md5] | [sha] | [sha256] | [sha384] | [sha512])...
    lifetime seconds (none | <120-2147483647>)
    no
    prf ([md5] | [sha] | [sha256] | [sha384] | [sha512])...
```

## `encryption`

> Configure one or more encryption algorithm
>
> At least one MUST be specified, but you can specify multiple.

- QCR: Quantum Computer Resistant
- NGE: Next Generation Encryption

| Algorithm | Operation | Status | Alternative | QCR | Mitigation |
| --------- | --------- | -------- | ----------- | --- | ---------- |
| DES | Encryption | Avoid | AES | -- | -- |
| 3DES | Encryption | Legacy | AES | -- | Short key lifetime |
| RC4 | Encryption | Avoid | AES | -- | -- |
| AES-CBC mode | Encryption | Acceptable | AES-GCM | [ X ] 256-bit | -- |
| AES-GCM mode | Authenticated encryption | NGE | -- | [ X ] 256-bit | -- |
| DH-768, -1024 | Key exchange | Avoid | DH-3072 (Group 15) | -- | -- |
| RSA-769, -1024 | Encryption | Avoid | RSA-3072 | -- | -- |
| DSA-768, -1024 | Authentication | Avoid | DSA-3072 | -- | -- |
| DH-2048 | Key exchange | acceptable | ECDH-256 | -- | -- |
| RSA-2048 | Encryption | acceptable | -- | -- | -- |
| DSA-2048 | Authentication | acceptable | ECDSA-256 | -- | -- |
| DH-3072 | Key exchange | acceptable | ECDH-256 | -- | -- |
| ECDH-256 | Key exchange | acceptable | -- | -- | -- |
| ECDSA-256 | Authentication | acceptable | ECDSA-256 | -- | -- |
| MD5 | Integrity | Avoid | SHA-256 | -- | -- |
| SHA-1 | Integrity | Legacy | SHA-256 | -- | -- |
| SHA-256 | Integrity | NGE | SHA-384 | -- | -- |
| SHA-384 | Integrity | NGE | -- | [ X ] | -- |
| SHA-512 | Integrity | NGE | -- | [ X ] | -- |
| HMAC-MD5 | Integrity | Legacy | HMAC-SHA-256 | -- | Short key lifetime |
| HMAC-SHA-1 | Integrity | Acceptable | HMAC-SHA-256 | -- | Short key lifetime |
| HMAC-SHA-256 | Integrity | NGE | -- | [ X ] | -- |
| ECDH-256 | Key exchange | Acceptable | ECDH-384 | -- | -- |
| ECDSSA-256 | Authentication | Acceptable | ECDH-384 | -- | -- |
| ECDH-384 | Key Exchange | NGE | -- | -- | -- |
| ECDSA-384 | Authentication | NGE | -- | -- | -- |

Table Reference: [Cisco](https://sec.cloudapps.cisco.com/security/center/resources/next_generation_cryptography)

## `exit`

> Exit from ikev2 policy configuration mode

## `group`

> Configure one or more DH groups
>
> At least one MUST be specified, but you can specify multiple.

- `1`
    - 768 bit modulus
    - AVOID
- `2`
    - 1024 bit modulus
    - AVOID
- `5`
    - 1536 bit modulus
    - AVOID
- `14`
    - 2048 bit modulus
    - MINIMUM ACCEPTABLE
- `19`
    - 256 bit elliptic curve
    - ACCEPTABLE
- `20`
    - 384 bit elliptic curve
    - Next Generation Encryption
- `21`
    - 521 bit elliptic curve
    - Next Generation Encryption
- `24`
    - Modular exponentiation group with a 2048 bit modulus, and
      256 bit prime order subgroup
    - Next Generation Encryption

Reference: [Cisco](https://community.cisco.com/t5/security-knowledge-base/diffie-hellman-groups/ta-p/3147010)

## `help`

> Help for ikev2 policy configuration commands

## `integrity`

> Configure one or more integrity algorithm
>
> At least one MUST be specified, but you can specify multiple.

## `lifetime seconds (none | <120-2147483647>)`

> Configure the ikev2 lifetime

- `none`
    - Disable rekey and allow an unlimited key period
- `<120-2147483647>`
    - Set the rekey lifetime in seconds

2147483647 seconds is:
- 35791394.116666... minutes, or
- 596523.2352777... hours, or
- 24855.1348032407 days, or
- 828.504493441358 (30-day) months, or
- 63.7311148801045 years

In PowerShell, you can use `New-TimeSpan -Days <days>` to get a timespan
in seconds.

## `no`

> Remove an ikev2 policy configuration item

## `prf`

> Configure one or more hash algorithm
>
> At least one MUST be specified, but you can specify multiple.
