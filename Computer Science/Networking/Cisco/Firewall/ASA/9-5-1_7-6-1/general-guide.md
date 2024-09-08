# General Guide to the ASA 5508-X

## Table of Contents

## Factory Reset

```
ciscoasa> enable
ciscoasa# configure terminal
ciscoasa(config)# configure factory-default
ciscoasa(config)# write memory
ciscoasa(config)# reload save-config noconfirm
```

## Update ASDM

```
ciscoasa> enable
ciscoasa# show disk0:

path
----
asa951-lfbff-k8.SPA
asa991-2-lfbff-k8.SPA
asdm-751.bin
asdm-761.bin
asdm-791.bin

ciscoasa# configure terminal
ciscoasa(config)# asdm image disk0:/asdm-791.bin
ciscoasa(config)# write memory
ciscoasa(config)# reload
```

## Update ASA

```
ciscoasa> enable
ciscoasa# show disk0:

path
----
asa951-lfbff-k8.SPA
asa991-2-lfbff-k8.SPA
asdm-751.bin
asdm-761.bin
asdm-791.bin

ciscoasa# configure terminal
ciscoasa(config)# boot system disk0:/asa991-2-lfbff-k8.SPA
ciscoasa(config)# write memory
ciscoasa(config)# reload
```
