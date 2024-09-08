# Cisco ASA-5508-X `username` Subcommands


## `config` mode

> Configure user authentication local database

```
ciscoasa> enable
ciscoasa# configure terminal
ciscoasa(config)# username ?
```

```
Usage:
    username <username> attributes
    username <username> nopassword
    username <username> nopassword privilege <0-15>
    username <username> password <password>
    username <username> password <password> encrypted privilege [<0-15>]
    username <username> password <password> mschap privilege [<0-15>]
    username <username> password <password> nt-encrypted privilege [<0-15>]
    username <username> password <password> privilege [<0-15>]

Arguments:
    username - Name of the user. MUST be between 3 and 64 characters.
    password - Password for the user. MUST be between 3 and 32 characters.
               MUST comply with the configured password policy.
```

### `username <username> attributes`

> Enters the `config-username` mode

See [config-username](config-username.md)

### `username <username> password <password>`

- Username:
    - The name of the user.
    - MUST be between 3 and 64 characters.
- Password:
    - The password for the user.
    - MUST be between 3 and 32 characters.
    - MUST comply with the configured password policy.


