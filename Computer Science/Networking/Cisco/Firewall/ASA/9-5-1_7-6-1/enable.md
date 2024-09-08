# `enable` Commands from Cisco ASA 5508-X

The `enable` command provides access to commands at a (optionally specified)
privilege level. Privilege levels range from 0-15.  **Level 1** is the user
level access, which provides access to User Exec mode.  **Level 15** is the
highest and provides full access to all Privileged commands.

Levels 0 and 2-14 are typically disabled by default but can be configured
to provide varying levels of access to commands, creating a range from read-only
to full-access.

```
ciscoasa# ?
```

cfg

Configure password for the enable command
