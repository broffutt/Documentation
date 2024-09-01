# `crypto` sub-commands

```
ciscoasa(config)# crypto ?
```

|    Command    | Description |
| ------------- | ----------- |
| [`ca`](#ca) | Certification Authority |
| dynamic-map | Configure a dynamic crypto map |
| ikev1 | Configure IKEv1 policy |
| ikev2 | Configure IKEv2 policy |
| ipsec | Configure transform-set, IPSec SA lifetime, and fragmentation |
| isakmp | Configure ISAKMP |
| key | Long-term key operations |
| map | Configure a crypto map |

## `ca`

```
ciscoasa(config)# crypto ca ?
```

|    Command    | Description |
| ------------- | ----------- |
| alerts | Configure alerts |
| authenticate | Get the CA certificate |
| certificates | Actions on certificates |
| crl | Actions on certificate revocation lists |
| enroll | Request a certificate from a CA |
| export | Export a trustpoint configuration with all associated keys and certificates in PKCS12 format, or export the identity certificate in PEM format |
| import | Import certificate or pkcs-12 data |
| server | Define Local Certificate Server |
| trustpoint | Define a CA trustpoint |
| trustpool | Define a CA trustpool |

```
Usage:
    crypto ca enroll <trustpoint-name: WORD (<65 char)> [noconfirm]
```

### ca trustpoint

```
crypto ca trustpoint accept-subordinates
crypto ca trustpoint ca-check
crypto ca trustpoint crl
crypto ca trustpoint default
crypto ca trustpoint email
crypto ca trustpoint enrollment
crypto ca trustpoint exit
crypto ca trustpoint fqdn
crypto ca trustpoint help
crypto ca trustpoint id-cert-issuer
crypto ca trustpoint id-usage
crypto ca trustpoint ignore-ipsec-keyusage
crypto ca trustpoint ignore-ssl-keyusage
crypto ca trustpoint ip-address
crypto ca trustpoint keypair
crypto ca trustpoint match
crypto ca trustpoint no
crypto ca trustpoint ocsp
crypto ca trustpoint password
crypto ca trustpoint proxy-ldc-issuer
crypto ca trustpoint revocation-check
crypto ca trustpoint serial-number
crypto ca trustpoint subject-name
crypto ca trustpoint validation-usage
```

- accept-subordinates
    - Accept subordinate CA certificates
- ca-check
    - CA Certificate installed in this trust point must have the CA flag set
      in the Basic Constraints extension CRL options
- crl
    - Certificate Revocation List (CRL) options
- default
    - Return all enrollment parameters to their default values
- email
    - Email Address
- enrollment
    - Enrollment Parameters
- exit
    - Exit from Certificate Authority Trustpoint mode
- fqdn
    - Include fully-qualified domain name
- help
    - Help for crypto CA Trustpoint Configuration commands
- id-cert-issuer
    - Accept ID Certificates
- id-usage
    - Specifies how the device identity represented by this trustpoint can be
      used
- ignore-ipsec-keyusage
    - Suppress Key Usage checking on IPSec client certificates
- ignore-ssl-keyusage
    - Suppress Key Usage checking on SSL client certificates
- ip-address
    - Include IP Address
- keypair
    - Specify the key pair whose public key is to be certified
- match
    - Match a certificate map
- no
    - Negate a command or set its defaults
- ocsp
    - OCSP Parameters
- password
    - revocation password
- proxy-ldc-issuer
    - An issuer for TLS proxy local dynamic certificates
- revocation-check
    - Revocation checking options
- serial-number
    - include serial number
- subject-name
    - Subject Name
- validation-usage
    - Specifies the usage types for which validation with this trustpoint
      is permitted

## 

```
ciscoasa(config)# crypto dynamic-map <template-tag: WORD> <sequence: INT (1-65535)> <<annotation <annotation-string: WORD>> | <match address <access-list-name: WORD>> | set>
```

|    Command    | Description |
| ------------- | ----------- |
