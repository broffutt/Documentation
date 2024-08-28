# U7 Pro

Unifi AP SSH CLI taken from a [U7-Pro](https://store.ui.com/us/en/products/u7-pro)

> [!NOTE]
> If you're using a fresh install, consider running:\
> `selfupgrade -u` to upgrade the firmware.
>
> I found this command relatively late in the process of
> copying the documentation.
>
> This probably requires internet connection
> and will take the AP down for ~3 min.
>
> See `help` output for the [`selfupgrade`](#selfupgrade) command.

## ToC

- ...

### default configs

```bash
U7-Pro-BZ.7.0.21# set
# OUTPUT
HOME='/etc/persistent'
HOSTNAME='U7-Pro'
IFS='
'
LOGNAME='ui'
OPTIND='1'
PATH='/usr/bin:/bin:/usr/sbin:/sbin'
PPID='16768'
PS1='U7-Pro-BZ.7.0.21# '
PS2='> '
PS4='+ '
PWD='/etc/persistent'
SHELL='/bin/ash'
SHLVL='1'
SSH_client='192.168.1.2 62970 22'
ssh_connection='192.168.1.2 62970 192.168.1.21 22'
SSH_TTY='/dev/pts/0'
TERM='xterm'
USER='ui'
_='config_generate'
```

### Setup


```bash
U7-Pro-BZ.7.0.21# vi /tmp/system.cfg

# ...
aaa.l.ssid=<ssid_name>
# ...

# use `:wq` to exit and save
```


### Commands

#### 80211stats

```
usage: 80211stats [-a] [-i device] [mac...]
```

#### Qcmbr

> Not sure why, but it tries to start a process that listens on port 2390

#### acfg_set_profile

```
Usage: acfg_set_profile <radio_iface_name> <config_file>
```

#### acfg_tool

```
acfg_tool <acfg api name> <api arguments>
acfg_tool -p
        Print help for all acfg apis

acfg_tool -p<acfg api name>
        Print help for one acfg api

acfg_tool -e <interface name> [-n]
        Wait for events on interface.  -n issues a nonblocking call to acfg library
```

#### acsdbgtool

```
Usage:
acsdbgtool athX --file|-f <filename>
acsdbgtool athX --help|-h
```

#### adjtimex


```
Usage: adjtimex [-q] [-o OFF] [-f FREQ] [-p TCONST] [-t TICK]

Read or set kernel time variables. See adjtimex(2)

        -q      Quiet
        -o OFF  Time offset, microseconds
        -f FREQ Frequency adjust, integer kernel units (65536 is 1ppm)
        -t TICK Microseconds per tick, usually 10000
                (positive -t or -f values make clock run faster)
        -p TCONST
```


#### apstats

```
apstats v0.1: Display Access Point Statistics.

Usage:

apstats [Level] [[-i interface_name] | [-m STA_MAC_Address]] [-R]

One of four levels can be selected. The levels are as follows (from
the top to the bottom of the hierarchy):
Entire Access Point, Radio, VAP and STA.
The default is Entire Access Point. Information for sub-levels below
the selected level can be displayed by choosing the -R (recursive)
option (not applicable for the STA level, where information for a
single STA is displayed).

LEVELS:

-a or --aplevel
    Entire Access Point Level (WLAN).
    No Interface or STA MAC needs to be provided.

-r or --radiolevel
    Radio Level.
    Radio Interface Name needs to be provided.

-v or --vaplevel
    VAP Level.
    VAP Interface Name needs to be provided.

-s or --stalevel
    STA Level.
    STA MAC Address needs to be provided.

INTERFACE:

If Radio Level is selected:
-i wifiX or --ifname=wifiX

If VAP Level is selected:
-i <VAP_name> or --ifname=<VAP_name>

STA MAC ADDRESS:

Required if STA Level is selected:
-m xx:xx:xx:xx:xx:xx or --stamacaddr xx:xx:xx:xx:xx:xx

OTHER OPTIONS:
-R or --recursive
    Recursive display
-M Mesh stats
```

#### arp

```
Usage: arp
[-vn]   [-H HWTYPE] [-i IF] -a [HOSTNAME]
[-v]                [-i IF] -d HOSTNAME [pub]
[-v]    [-H HWTYPE] [-i IF] -s HOSTNAME HWADDR [temp]
[-v]    [-H HWTYPE] [-i IF] -s HOSTNAME HWADDR [netmask MASK] pub
[-v]    [-H HWTYPE] [-i IF] -Ds HOSTNAME IFACE [netmask MASK] pub

Manipulate ARP cache

        -a              Display (all) hosts
        -d              Delete ARP entry
        -s              Set new entry
        -v              Verbose
        -n              Don't resolve names
        -i IF           Network interface
        -D              Read HWADDR from IFACE
        -A,-p AF        Protocol family
        -H HWTYPE       Hardware address type
```

#### arping

```
Usage: arping [-fqbDUA] [-c CNT] [-w TIMEOUT] [-I IFACE] [-s SRC_IP] DST_IP

Send ARP requests/replies

        -f              Quit on first ARP reply
        -q              Quiet
        -b              Keep broadcasting, don't go unicast
        -D              Exit with 1 if DST_IP replies
        -U              Unsolicited ARP mode, update your neighbors
        -A              ARP answer mode, update your neighbors
        -c N            Stop after sending N ARP requests
        -w TIMEOUT      Seconds to wait for ARP reply
        -I IFACE        Interface to use (default eth0)
        -s SRC_IP       Sender IP address
        DST_IP          Target IP address
```

#### arptables

```
arptables v0.0.4

Usage: arptables -[AD] chain rule-specification [options]
       arptables -[RI] chain rulenum rule-specification [options]
       arptables -D chain rulenum [options]
       arptables -[LFZ] [chain] [options]
       arptables -[NX] chain
       arptables -E old-chain-name new-chain-name
       arptables -P chain target [options]
       arptables -h (print this help information)

Commands:
Either long or short options are allowed.
  --append  -A chain            Append to chain
  --delete  -D chain            Delete matching rule from chain
  --delete  -D chain rulenum
                                Delete rule rulenum (1 = first) from chain
  --insert  -I chain [rulenum]
                                Insert in chain as rulenum (default 1=first)
  --replace -R chain rulenum
                                Replace rule rulenum (1 = first) in chain
  --list    -L [chain]          List the rules in a chain or all chains
  --flush   -F [chain]          Delete all rules in  chain or all chains
  --zero    -Z [chain]          Zero counters in chain or all chains
  --new     -N chain            Create a new user-defined chain
  --delete-chain
            -X [chain]          Delete a user-defined chain
  --policy  -P chain target
                                Change policy on chain to target
  --rename-chain
            -E old-chain new-chain
                                Change chain name, (moving any references)
Options:
  --source-ip   -s [!] address[/mask]
                                source specification
  --destination-ip -d [!] address[/mask]
                                destination specification
  --source-mac [!] address[/mask]
  --destination-mac [!] address[/mask]
  --h-length   -l   length[/mask] hardware length (nr of bytes)
  --opcode code[/mask] operation code (2 bytes)
  --h-type   type[/mask]  hardware type (2 bytes, hexadecimal)
  --proto-type   type[/mask]  protocol type (2 bytes)
  --in-interface -i [!] input name[+]
                                network interface name ([+] for wildcard)
  --out-interface -o [!] output name[+]
                                network interface name ([+] for wildcard)
  --jump        -j target
                                target for rule (may load target extension)
  --match       -m match
                                extended match (may load extension)
  --numeric     -n              numeric output of addresses and ports
  --table       -t table        table to manipulate (default: `filter')
  --verbose     -v              verbose mode
  --line-numbers                print line numbers when listing
  --exact       -x              expand numbers (display exact values)
  --modprobe=<command>          try to insert modules using this command
  --set-counters -c PKTS BYTES  set the counter during insert/append
[!] --version   -V              print package version.
 opcode strings:
 1 = Request
 2 = Reply
 3 = Request_Reverse
 4 = Reply_Reverse
 5 = DRARP_Request
 6 = DRARP_Reply
 7 = DRARP_Error
 8 = InARP_Request
 9 = ARP_NAK
 hardware type string: 1 = Ethernet
 protocol type string: 0x800 = IPv4

MARK target v0.0.4 options:
--set-mark mark : set the mark value
--and-mark value : binary AND the mark with value
--or-mark value : binary OR the mark with value

CLASSIFY target v0.0.4 options:
--set-class major:minor : set the major and minor class value

mangle target v0.0.4 options:
--mangle-ip-s IP address
--mangle-ip-d IP address
--mangle-mac-s MAC address
--mangle-mac-d MAC address
--mangle-target target (DROP, CONTINUE or ACCEPT -- default is ACCEPT)

Standard v0.0.4 options:
(If target is DROP, ACCEPT, RETURN or nothing)
```

#### ash

```
Usage: ash [-/+OPTIONS] [-/+o OPT]... [-c 'SCRIPT' [ARG0 [ARGS]] / FILE [ARGS]]

Unix shell interpreter
```

#### askfirst
#### assocdenialnotify

```
Usage : assocdenialnotify
```

#### athdiag

```
usage:
athdiag commands and options:
                --get --address=<target word address> [--count=<wordcount>]
                --set --address=<target word address> --value=<value>
                --quiet
                --wifi=<index>
                The options can also be given in the abbreviated form --option=x or -o x.
                The options can be given in any order
```

#### athkey

```
usage to set: athkey -i athX -s keyix cipher keyval [mac]
usage to get: athkey -i athX -x keyix [mac]
usage to set default key as keyix: athkey -i athX -c keyix [mac]
usage to get for cfg: athkey -cfg80211 -i athX -x keyix [mac]
usage to set for cfg: athkey -cfg80211 -i athX -s -e -u -r <rxsc> <keyidx> <cipher> <keyval> <mac>
usage to set default key as keyix for cfg: athkey -cfg80211 -i athX -c keyix [mac]
```

#### athstats
#### athstatsclr
#### awk

```
Usage: awk [OPTIONS] [AWK_PROGRAM] [FILE]...

        -v VAR=VAL      Set variable
        -F SEP          Use SEP as field separator
        -f FILE         Read program from FILE
        -e AWK_PROGRAM
```

#### base64

```
Usage: base64 [-d] [FILE]

Base64 encode or decode FILE to standard output
        -d      Decode data
```

#### basename

```
Usage: basename FILE [SUFFIX]

Strip directory path and .SUFFIX from FILE
```

#### bgnd

```
Usage: bgnd [-s name|[-r name [-e cfg] cmdline arg1 arg2]]
```

#### board_detect

```
Usage: mv [-fin] SOURCE DEST
or: mv [-fin] SOURCE... DIRECTORY

Rename SOURCE to DEST, or move SOURCE(s) to DIRECTORY

        -f      Don't prompt before overwriting
        -i      Interactive, prompt before overwrite
        -n      Don't overwrite an existing file
```

#### brctl

```
Usage: brctl COMMAND [BRIDGE [INTERFACE]]

Manage ethernet bridges

Commands:
        show                    Show a list of bridges
        addbr BRIDGE            Create BRIDGE
        delbr BRIDGE            Delete BRIDGE
        addif BRIDGE IFACE      Add IFACE to BRIDGE
        delif BRIDGE IFACE      Delete IFACE from BRIDGE
        setageing BRIDGE TIME           Set ageing time
        setfd BRIDGE TIME               Set bridge forward delay
        sethello BRIDGE TIME            Set hello time
        setmaxage BRIDGE TIME           Set max message age
        setpathcost BRIDGE COST         Set path cost
        setportprio BRIDGE PRIO         Set port priority
        setbridgeprio BRIDGE PRIO       Set bridge priority
        stp BRIDGE [1/yes/on|0/no/off]  STP on/off
```

#### bridge

```
Usage: bridge [ OPTIONS ] OBJECT { COMMAND | help }
       bridge [ -force ] -batch filename
where   OBJECT := { link | fdb | mdb | vlan | monitor }
        OPTIONS := { -V[ersion] | -s[tatistics] | -d[etails] |
                     -o[neline] | -t[imestamp] | -n[etns] name |
                     -c[ompressvlans] }
```

#### bunzip2

```
Usage: bunzip2 [-cf] [FILE]...

Decompress FILEs (or stdin)

        -c      Write to stdout
        -f      Force
```

#### bunzip2busybox
#### bzcat

```
Usage: bzcat [FILE]...

Decompress to stdout
```

#### cat

> Writes files to terminal (normal bash `cat`)

#### cfg80211tool
#### cfg80211tool.1
#### cfg80211tool_mesh

```
    get_whc_wds
    get_whc_son
    get_whc_ul_rate
    g_curr_caprssi
    g_best_ob_bssid
    g_whc_ob_bssid
    get_whc_dist
    set_skip_hyst
    get_skip_hyst
    set_whc_sfactor
    set_whc_dist
    set_whc_ul_rate
    bsteerrssi_log
    otherband_bssid
    get_whc_sfactor
    get_whc_rate
    get_whc_bssid
    g_whc_cap_bssid
    whc_mixedbh_ul
    g_whc_mixedbh_ul
    whc_mixedbh_bh_type
    caprssi
    g_caprssi
    MapBSSType
    get_MapBSSType
    mapset_vapup
    mapget_vapup
    map
    get_map
    map_sta_vlan
    get_map_sta_vlan
    ssid_config
    get_ssid_config
    son_event_bcast
    g_son_event_bcast
    get_whc_ul_snr
    ul_hyst
    g_ul_hyst
    get_mesh_version
    son
    get_son
    get_vap_count
    rept_spl
    g_rept_spl
    ald_buf_thr
    g_ald_buf_thr
    set_innetwork_2g
    get_active_vdev_count
    g_bstaflag
    bstaflag
```

#### cfgmtd

```
Usage: cfgmtd [options]
        -t <type>                       - Configuration type to use [1(active)|2(backup)]. (Default: 1(active))
        -f <config file>                - Configuration file to use. (Default: /tmp/system.cfg)
        -p <persistent directory>       - Directory to persistent dir. (Default: none)
        -w                              - Write to flash action.
        -r                              - Read from flash action.
        -c                              - Clear flash action.
        -o <mtd|file name>              - Use mtd or file name. (Default: /dev/mmcblk0p5)
        -n                              - No check size when specify -o. (Default: Check)
        -h                              - This message.
```

#### cfr_test_app

```
Usage: cfr_test_app -i <interfacename>
```

#### chgrp

```
Usage: chgrp [-RhLHP]... GROUP FILE...

Change the group membership of each FILE to GROUP

        -R      Recurse
        -h      Affect symlinks instead of symlink targets
        -L      Traverse all symlinks to directories
        -H      Traverse symlinks on command line only
        -P      Don't traverse symlinks (default)
```

#### chmod

```
Usage: chmod [-R] MODE[,MODE]... FILE...

Each MODE is one or more of the letters ugoa, one of the
symbols +-= and one or more of the letters rwxst

        -R      Recurse
```

#### chown

```
Usage: chown [-Rh]... USER[:[GRP]] FILE...

Change the owner and/or group of each FILE to USER and/or GRP

        -R      Recurse
        -h      Affect symlinks instead of symlink targets
```

#### chroot

```
Usage: chroot NEWROOT [PROG ARGS]

Run PROG with root directory set to NEWROOT
```

#### clear

```
Usage: clear

Clear screen
```

#### cmp

```
Usage: cmp [-l] [-s] FILE1 [FILE2]

Compare FILE1 with FILE2 (or stdin)

        -l      Write the byte numbers (decimal) and values (octal)
                for all differing bytes
        -s      Quiet
```

#### cnss_diag

```
Usage:
    cnss_diag options
Options:
    -f, --logfile(Currently file path is fixed)
    -c, --console (prints the logs in the console)
    -s, --silent (No print will come when logging)
    -S, --syslog (Prints will logs in syslog)
    -p, --parse Diag log to syslog
    -q, --qxdm  (prints the logs in the qxdm)
    -x, --qxdm_sync (QXDM log packet format)
    -l, --qxdm_sync_log_file (QXDM log packet format QMDL2 file)
    -d, --debug  (more prints in logcat, check logcat
    -s ROME_DEBUG, example to use: -q -d or -c -d)
    -b --buffer_size ( example to use : -b 64(in KBs)
    -T --target_buffer_size ( example to use : -T 64(in KBs)
    -m --cnss_diag_config_file_loc ( example to use : -m /data/misc/cnss_diag.conf)
    -u, --Write fw/host logs to a local buffer
    -w, --This option along with '-u' facilitates to write decoded fw/host logs to buffer
    -D, --This option will disable FW logs to display on console
    -P, --This option point to continuous packet logs
    -n, --This option is to set host log netlink protocol
    -e, --This option is to set driver multi if name
    -z, --This option is to set absolute directory base path : -z /vendor/firmware

The options can also be given in the abbreviated form --option=x or -o x. The options can be given in any order
```

#### cnsscli

```
qmi_cci_xprt_qrtr_supported(101) qmi_cci_xprt_qrtr_supported: QRTR SUPPORTED

cnsscli Usage: [options]
   -i along with any other option is mandatory
   Sample Usage IPQ: cnsscli -i qcn9000_pci0 --qdss_start, cnsscli -i qcn9000_pci0 --qdss_stop 0x3f
   Sample Usage MCC: cnss_cli -i mcc --qdss_start, cnss_cli -i mcc --qdss_stop 0x3f

   -i, --interface            Interface selected, like integrated qcnXXXX_pciX
   --enable_qdss_tracing      Enable automatic starting of QDSS after FW ready
   --qdss_start               Do qdss_trace_load_config followed by qdss_trace_start
   --qdss_stop                Do qdss_trace_stop with option number
   --qdss_file_size           Set QDSS trace data file size between 1MB to 8MB
   --enable_daemon_support    Enable daemon support in kernel for given interface
   --enable_cold_boot_support Enable cold boot support in kernel for given interface
   --enable_hds_support       Enable HDS bin download for given interface
   --qmi_timeout              Set QMI timeout value in msec
   --enable_regdb_support       Enable REGDB bin download for given interface
   -h, --help                 Display this help text

qmi_cci_xport_ctrl_port_deinit(549) qmi_cci_xport_ctrl_port_deinit: Control port is not initilized yet
```

#### cnssdaemon

```
qmi_cci_xprt_qrtr_supported(101) qmi_cci_xprt_qrtr_supported: QRTR SUPPORTED

usage: cnssdaemon [options]
   -i, --interface specify interface name like integrated, qcnXXXX_pci0, qcnXXXX_pci1 (optional)
                    use interface "none" for starting daemon without connecting to any interface
   -n, --nodaemon  do not run as a daemon
   -d              show more debug messages (-dd for more)
   -f <path/file>  Log output to file
   -s              Log output to syslog
       --help      display this help and exit

cnss-daemon: !!EXITING FROM cnss-daemon!!
qmi_cci_xport_ctrl_port_deinit(549) qmi_cci_xport_ctrl_port_deinit: Control port is not initilized yet
```

#### config_generate
#### conntrack

```
Command line interface for the connection tracking system. Version 1.4.4

Usage: conntrack [commands] [options]

Commands:
  -L [table] [options]          List conntrack or expectation table
  -G [table] parameters         Get conntrack or expectation
  -D [table] parameters         Delete conntrack or expectation
  -I [table] parameters         Create a conntrack or expectation
  -U [table] parameters         Update a conntrack
  -E [table] [options]          Show events
  -F [table]                    Flush table
  -C [table]                    Show counter
  -S                            Show statistics

Tables: conntrack, expect, dying, unconfirmed

Conntrack parameters and options:
  -n, --src-nat ip                      source NAT ip
  -g, --dst-nat ip                      destination NAT ip
  -j, --any-nat ip                      source or destination NAT ip
  -m, --mark mark                       Set mark
  -c, --secmark secmark                 Set selinux secmark
  -e, --event-mask eventmask            Event mask, eg. NEW,DESTROY
  -z, --zero                            Zero counters while listing
  -o, --output type[,...]               Output format, eg. xml
  -l, --label label[,...]               conntrack labels

Expectation parameters and options:
  --tuple-src ip        Source address in expect tuple
  --tuple-dst ip        Destination address in expect tuple

Updating parameters and options:
  --label-add label     Add label
  --label-del label     Delete label

Common parameters and options:
  -s, --src, --orig-src ip              Source address from original direction
  -d, --dst, --orig-dst ip              Destination address from original direction
  -r, --reply-src ip            Source addres from reply direction
  -q, --reply-dst ip            Destination address from reply direction
  -p, --protonum proto          Layer 4 Protocol, eg. 'tcp'
  -f, --family proto            Layer 3 Protocol, eg. 'ipv6'
  -t, --timeout timeout         Set timeout
  -u, --status status           Set status, eg. ASSURED
  -w, --zone value              Set conntrack zone
  --orig-zone value             Set zone for original direction
  --reply-zone value            Set zone for reply direction
  -b, --buffer-size             Netlink socket buffer size
  --mask-src ip                 Source mask address
  --mask-dst ip                 Destination mask address
```

#### coredump

```
Usage: coredump <executable> <pid> <signal>

Options:
        -h Show this help text
```

#### cp

> copies files (normal bash `cp`)

#### crond

```
Usage: crond -fbS -l N -L LOGFILE -c DIR
    -f      Foreground
    -b      Background (default)
    -S      Log to syslog (default)
    -l N    Set log level. Most verbose:0, default:8
    -L FILE Log to FILE
    -c DIR  Cron dir. Default:/etc/crontabs
```

#### crontab

```
Usage: crontab [-c DIR] [-u USER] [-ler]|[FILE]
    -c      Crontab directory
    -u      User
    -l      List crontab
    -e      Edit crontab
    -r      Delete crontab
    FILE    Replace crontab by FILE ('-': stdin)
```

#### curl

> Use `curl --help` for a smaller output. The following is from `curl --help all`.

```
Usage: curl [options...] <url>
     --abstract-unix-socket <path> Connect via abstract Unix domain socket
     --alt-svc <file name> Enable alt-svc with this cache file
     --anyauth     Pick any authentication method
 -a, --append      Append to target file when uploading
     --aws-sigv4 <provider1[:provider2[:region[:service]]]> Use AWS V4 signature authentication
     --basic       Use HTTP Basic Authentication
     --ca-native   Use CA certificates from the native OS
     --cacert <file> CA certificate to verify peer against
     --capath <dir> CA directory to verify peer against
 -E, --cert <certificate[:password]> Client certificate file and password
     --cert-status Verify the status of the server cert via OCSP-staple
     --cert-type <type> Certificate type (DER/PEM/ENG/P12)
     --ciphers <list of ciphers> SSL ciphers to use
     --compressed  Request compressed response
     --compressed-ssh Enable SSH compression
 -K, --config <file> Read config from a file
     --connect-timeout <fractional seconds> Maximum time allowed for connection
     --connect-to <HOST1:PORT1:HOST2:PORT2> Connect to host
 -C, --continue-at <offset> Resumed transfer offset
 -b, --cookie <data|filename> Send cookies from string/file
 -c, --cookie-jar <filename> Write cookies to <filename> after operation
     --create-dirs Create necessary local directory hierarchy
     --create-file-mode <mode> File mode for created files
     --crlf        Convert LF to CRLF in upload
     --crlfile <file> Use this CRL list
     --curves <algorithm list> (EC) TLS key exchange algorithm(s) to request
 -d, --data <data> HTTP POST data
     --data-ascii <data> HTTP POST ASCII data
     --data-binary <data> HTTP POST binary data
     --data-raw <data> HTTP POST data, '@' allowed
     --data-urlencode <data> HTTP POST data URL encoded
     --delegation <LEVEL> GSS-API delegation permission
     --digest      Use HTTP Digest Authentication
 -q, --disable     Disable .curlrc
     --disable-eprt Inhibit using EPRT or LPRT
     --disable-epsv Inhibit using EPSV
     --disallow-username-in-url Disallow username in URL
     --dns-interface <interface> Interface to use for DNS requests
     --dns-ipv4-addr <address> IPv4 address to use for DNS requests
     --dns-ipv6-addr <address> IPv6 address to use for DNS requests
     --dns-servers <addresses> DNS server addrs to use
     --doh-cert-status Verify the status of the DoH server cert via OCSP-staple
     --doh-insecure Allow insecure DoH server connections
     --doh-url <URL> Resolve host names over DoH
 -D, --dump-header <filename> Write the received headers to <filename>
     --egd-file <file> EGD socket path for random data
     --engine <name> Crypto engine to use
     --etag-compare <file> Pass an ETag from a file as a custom header
     --etag-save <file> Parse ETag from a request and save it to a file
     --expect100-timeout <seconds> How long to wait for 100-continue
 -f, --fail        Fail fast with no output on HTTP errors
     --fail-early  Fail on first transfer error, do not continue
     --fail-with-body Fail on HTTP errors but save the body
     --false-start Enable TLS False Start
 -F, --form <name=content> Specify multipart MIME data
     --form-escape Escape multipart form field/file names using backslash
     --form-string <name=string> Specify multipart MIME data
     --ftp-account <data> Account data string
     --ftp-alternative-to-user <command> String to replace USER [name]
     --ftp-create-dirs Create the remote dirs if not present
     --ftp-method <method> Control CWD usage
     --ftp-pasv    Use PASV/EPSV instead of PORT
 -P, --ftp-port <address> Use PORT instead of PASV
     --ftp-pret    Send PRET before PASV
     --ftp-skip-pasv-ip Skip the IP address for PASV
     --ftp-ssl-ccc Send CCC after authenticating
     --ftp-ssl-ccc-mode <active/passive> Set CCC mode
     --ftp-ssl-control Require SSL/TLS for FTP login, clear for transfer
 -G, --get         Put the post data in the URL and use GET
 -g, --globoff     Disable URL sequences and ranges using {} and []
     --happy-eyeballs-timeout-ms <milliseconds> Time for IPv6 before trying IPv4
     --haproxy-clientip Sets client IP in HAProxy PROXY protocol v1 header
     --haproxy-protocol Send HAProxy PROXY protocol v1 header
 -I, --head        Show document info only
 -H, --header <header/@file> Pass custom header(s) to server
 -h, --help <category> Get help for commands
     --hostpubmd5 <md5> Acceptable MD5 hash of the host public key
     --hostpubsha256 <sha256> Acceptable SHA256 hash of the host public key
     --hsts <file name> Enable HSTS with this cache file
     --http0.9     Allow HTTP 0.9 responses
 -0, --http1.0     Use HTTP 1.0
     --http1.1     Use HTTP 1.1
     --http2       Use HTTP/2
     --http2-prior-knowledge Use HTTP 2 without HTTP/1.1 Upgrade
     --http3       Use HTTP v3
     --http3-only  Use HTTP v3 only
     --ignore-content-length Ignore the size of the remote resource
 -i, --include     Include protocol response headers in the output
 -k, --insecure    Allow insecure server connections
     --interface <name> Use network INTERFACE (or address)
     --ipfs-gateway <URL> Gateway for IPFS
 -4, --ipv4        Resolve names to IPv4 addresses
 -6, --ipv6        Resolve names to IPv6 addresses
     --json <data> HTTP POST JSON
 -j, --junk-session-cookies Ignore session cookies read from file
     --keepalive-time <seconds> Interval time for keepalive probes
     --key <key>   Private key file name
     --key-type <type> Private key file type (DER/PEM/ENG)
     --krb <level> Enable Kerberos with security <level>
     --libcurl <file> Dump libcurl equivalent code of this command line
     --limit-rate <speed> Limit transfer speed to RATE
 -l, --list-only   List only mode
     --local-port <num/range> Force use of RANGE for local port numbers
 -L, --location    Follow redirects
     --location-trusted Like --location, and send auth to other hosts
     --login-options <options> Server login options
     --mail-auth <address> Originator address of the original email
     --mail-from <address> Mail from this address
     --mail-rcpt <address> Mail to this address
     --mail-rcpt-allowfails Allow RCPT TO command to fail for some recipients
 -M, --manual      Display the full manual
     --max-filesize <bytes> Maximum file size to download
     --max-redirs <num> Maximum number of redirects allowed
 -m, --max-time <fractional seconds> Maximum time allowed for transfer
     --metalink    Process given URLs as metalink XML file
     --negotiate   Use HTTP Negotiate (SPNEGO) authentication
 -n, --netrc       Must read .netrc for user name and password
     --netrc-file <filename> Specify FILE for netrc
     --netrc-optional Use either .netrc or URL
 -:, --next        Make next URL use its separate set of options
     --no-alpn     Disable the ALPN TLS extension
 -N, --no-buffer   Disable buffering of the output stream
     --no-clobber  Do not overwrite files that already exist
     --no-keepalive Disable TCP keepalive on the connection
     --no-npn      Disable the NPN TLS extension
     --no-progress-meter Do not show the progress meter
     --no-sessionid Disable SSL session-ID reusing
     --noproxy <no-proxy-list> List of hosts which do not use proxy
     --ntlm        Use HTTP NTLM authentication
     --ntlm-wb     Use HTTP NTLM authentication with winbind
     --oauth2-bearer <token> OAuth 2 Bearer Token
 -o, --output <file> Write to file instead of stdout
     --output-dir <dir> Directory to save files in
 -Z, --parallel    Perform transfers in parallel
     --parallel-immediate Do not wait for multiplexing (with --parallel)
     --parallel-max <num> Maximum concurrency for parallel transfers
     --pass <phrase> Pass phrase for the private key
     --path-as-is  Do not squash .. sequences in URL path
     --pinnedpubkey <hashes> FILE/HASHES Public key to verify peer against
     --post301     Do not switch to GET after following a 301
     --post302     Do not switch to GET after following a 302
     --post303     Do not switch to GET after following a 303
     --preproxy [protocol://]host[:port] Use this proxy first
 -#, --progress-bar Display transfer progress as a bar
     --proto <protocols> Enable/disable PROTOCOLS
     --proto-default <protocol> Use PROTOCOL for any URL missing a scheme
     --proto-redir <protocols> Enable/disable PROTOCOLS on redirect
 -x, --proxy [protocol://]host[:port] Use this proxy
     --proxy-anyauth Pick any proxy authentication method
     --proxy-basic Use Basic authentication on the proxy
     --proxy-ca-native Use CA certificates from the native OS for proxy
     --proxy-cacert <file> CA certificate to verify peer against for proxy
     --proxy-capath <dir> CA directory to verify peer against for proxy
     --proxy-cert <cert[:passwd]> Set client certificate for proxy
     --proxy-cert-type <type> Client certificate type for HTTPS proxy
     --proxy-ciphers <list> SSL ciphers to use for proxy
     --proxy-crlfile <file> Set a CRL list for proxy
     --proxy-digest Use Digest authentication on the proxy
     --proxy-header <header/@file> Pass custom header(s) to proxy
     --proxy-http2 Use HTTP/2 with HTTPS proxy
     --proxy-insecure Do HTTPS proxy connections without verifying the proxy
     --proxy-key <key> Private key for HTTPS proxy
     --proxy-key-type <type> Private key file type for proxy
     --proxy-negotiate Use HTTP Negotiate (SPNEGO) authentication on the proxy
     --proxy-ntlm  Use NTLM authentication on the proxy
     --proxy-pass <phrase> Pass phrase for the private key for HTTPS proxy
     --proxy-pinnedpubkey <hashes> FILE/HASHES public key to verify proxy with
     --proxy-service-name <name> SPNEGO proxy service name
     --proxy-ssl-allow-beast Allow security flaw for interop for HTTPS proxy
     --proxy-ssl-auto-client-cert Use auto client certificate for proxy (Schannel)
     --proxy-tls13-ciphers <ciphersuite list> TLS 1.3 proxy cipher suites
     --proxy-tlsauthtype <type> TLS authentication type for HTTPS proxy
     --proxy-tlspassword <string> TLS password for HTTPS proxy
     --proxy-tlsuser <name> TLS username for HTTPS proxy
     --proxy-tlsv1 Use TLSv1 for HTTPS proxy
 -U, --proxy-user <user:password> Proxy user and password
     --proxy1.0 <host[:port]> Use HTTP/1.0 proxy on given port
 -p, --proxytunnel Operate through an HTTP proxy tunnel (using CONNECT)
     --pubkey <key> SSH Public key file name
 -Q, --quote <command> Send command(s) to server before transfer
     --random-file <file> File for reading random data from
 -r, --range <range> Retrieve only the bytes within RANGE
     --rate <max request rate> Request rate for serial transfers
     --raw         Do HTTP "raw"; no transfer decoding
 -e, --referer <URL> Referrer URL
 -J, --remote-header-name Use the header-provided filename
 -O, --remote-name Write output to a file named as the remote file
     --remote-name-all Use the remote file name for all URLs
 -R, --remote-time Set the remote file's time on the local output
     --remove-on-error Remove output file on errors
 -X, --request <method> Specify request method to use
     --request-target <path> Specify the target for this request
     --resolve <[+]host:port:addr[,addr]...> Resolve the host+port to this address
     --retry <num> Retry request if transient problems occur
     --retry-all-errors Retry all errors (use with --retry)
     --retry-connrefused Retry on connection refused (use with --retry)
     --retry-delay <seconds> Wait time between retries
     --retry-max-time <seconds> Retry only within this period
     --sasl-authzid <identity> Identity for SASL PLAIN authentication
     --sasl-ir     Enable initial response in SASL authentication
     --service-name <name> SPNEGO service name
 -S, --show-error  Show error even when -s is used
 -s, --silent      Silent mode
     --socks4 <host[:port]> SOCKS4 proxy on given host + port
     --socks4a <host[:port]> SOCKS4a proxy on given host + port
     --socks5 <host[:port]> SOCKS5 proxy on given host + port
     --socks5-basic Enable username/password auth for SOCKS5 proxies
     --socks5-gssapi Enable GSS-API auth for SOCKS5 proxies
     --socks5-gssapi-nec Compatibility with NEC SOCKS5 server
     --socks5-gssapi-service <name> SOCKS5 proxy service name for GSS-API
     --socks5-hostname <host[:port]> SOCKS5 proxy, pass host name to proxy
 -Y, --speed-limit <speed> Stop transfers slower than this
 -y, --speed-time <seconds> Trigger 'speed-limit' abort after this time
     --ssl         Try SSL/TLS
     --ssl-allow-beast Allow security flaw to improve interop
     --ssl-auto-client-cert Use auto client certificate (Schannel)
     --ssl-no-revoke Disable cert revocation checks (Schannel)
     --ssl-reqd    Require SSL/TLS
     --ssl-revoke-best-effort Ignore missing/offline cert CRL dist points (Schannel)
 -2, --sslv2       Use SSLv2
 -3, --sslv3       Use SSLv3
     --stderr <file> Where to redirect stderr
     --styled-output Enable styled output for HTTP headers
     --suppress-connect-headers Suppress proxy CONNECT response headers
     --tcp-fastopen Use TCP Fast Open
     --tcp-nodelay Use the TCP_NODELAY option
 -t, --telnet-option <opt=val> Set telnet option
     --tftp-blksize <value> Set TFTP BLKSIZE option
     --tftp-no-options Do not send any TFTP options
 -z, --time-cond <time> Transfer based on a time condition
     --tls-max <VERSION> Set maximum allowed TLS version
     --tls13-ciphers <ciphersuite list> TLS 1.3 cipher suites to use
     --tlsauthtype <type> TLS authentication type
     --tlspassword <string> TLS password
     --tlsuser <name> TLS user name
 -1, --tlsv1       Use TLSv1.0 or greater
     --tlsv1.0     Use TLSv1.0 or greater
     --tlsv1.1     Use TLSv1.1 or greater
     --tlsv1.2     Use TLSv1.2 or greater
     --tlsv1.3     Use TLSv1.3 or greater
     --tr-encoding Request compressed transfer encoding
     --trace <file> Write a debug trace to FILE
     --trace-ascii <file> Like --trace, but without hex output
     --trace-config <string> Details to log in trace/verbose output
     --trace-ids   Add transfer and connection identifiers to trace/verbose output
     --trace-time  Add time stamps to trace/verbose output
     --unix-socket <path> Connect through this Unix domain socket
 -T, --upload-file <file> Transfer local FILE to destination
     --url <url>   URL to work with
     --url-query <data> Add a URL query part
 -B, --use-ascii   Use ASCII/text transfer
 -u, --user <user:password> Server user and password
 -A, --user-agent <name> Send User-Agent <name> to server
     --variable <[%]name=text/@file> Set variable
 -v, --verbose     Make the operation more talkative
 -V, --version     Show version number and quit
 -w, --write-out <format> Use output FORMAT after completion
     --xattr       Store metadata in extended file attributes
```

#### cut

```
Usage: cut [OPTIONS] [FILE]...

Print selected fields from each input FILE to stdout
    -b LIST Output only bytes from LIST
    -c LIST Output only characters from LIST
    -d CHAR Use CHAR instead of tab as the field delimiter
    -s      Output only the lines containing delimiter
    -f N    Print only these fields
    -n      Ignored
```

#### dashboard.sh

```
Usage:
dashboard.sh OPTION
Show sytem information
    -s      start system test
            (Run all tests excluding Module info and Package info)
    -h      display this help and exit
    -m      show modules loaded
    -p      show packages installed
    -v      output version information and exit
```

#### date

```
Usage: date [OPTIONS] [+FMT] [TIME]

Display time (using +FMT), or set time
    [-s,--set] TIME Set time to TIME
    -u,--utc        Work in UTC (don't convert to local time)
    -R,--rfc-2822   Output RFC-2822 compliant date string
    -I[SPEC]        Output ISO-8601 compliant date string
                    SPEC='date' (default) for date only,
                    'hours', 'minutes', or 'seconds' for date and
                    time to the indicated precision
    -r,--reference FILE     Display last modification time of FILE
    -d,--date TIME  Display TIME, not 'now'
    -D FMT          Use FMT for -d TIME conversion
    -k              Set Kernel timezone from localtime and exit

Recognized TIME formats:
    hh:mm[:ss]
    [YYYY.]MM.DD-hh:mm[:ss]
    YYYY-MM-DD hh:mm[:ss]
    [[[[[YY]YY]MM]DD]hh]mm[.ss]
```

#### dbclient

```
Dropbear SSH client v2022.83 https://matt.ucc.asn.au/dropbear/dropbear.html

Usage: dbclient [options] [user@]host[/port] [command]
    -p <remoteport>
    -l <username>
    -t    Allocate a pty
    -T    Don't allocate a pty
    -N    Don't run a remote command
    -f    Run in background after auth
    -q    quiet, don't show remote banner
    -y    Always accept remote host key if unknown
    -y -y Don't perform any remote host key checking (caution)
    -s    Request a subsystem (use by external sftp)
    -o option     Set option in OpenSSH-like format ('-o help' to list options)
    -i <identityfile>   (multiple allowed, default ~/.ssh/id_dropbear)
    -L <[listenaddress:]listenport:remotehost:remoteport> Local port forwarding
    -g    Allow remote hosts to connect to forwarded ports
    -R <[listenaddress:]listenport:remotehost:remoteport> Remote port forwarding
    -W <receive_window_buffer> (default 24576, larger may be faster, max 10MB)
    -K <keepalive>  (0 is never, default 0)
    -I <idle_timeout>  (0 is never, default 0)
    -z    disable QoS
    -J <proxy_program> Use program pipe rather than TCP connection
    -c <cipher list> Specify preferred ciphers ('-c help' to list options)
    -m <MAC list> Specify preferred MACs for packet verification (or '-m help')
    -b    [bind_address][:bind_port]
    -V    Version
```

#### dd

```
Usage: dd [if=FILE] [of=FILE] [ibs=N] [obs=N] [bs=N] [count=N] [skip=N]
        [seek=N] [conv=notrunc|noerror|sync|fsync] [iflag=skip_bytes]

Copy a file with converting and formatting

        if=FILE         Read from FILE instead of stdin
        of=FILE         Write to FILE instead of stdout
        bs=N            Read and write N bytes at a time
        ibs=N           Read N bytes at a time
        obs=N           Write N bytes at a time
        count=N         Copy only N input blocks
        skip=N          Skip N input blocks
        seek=N          Skip N output blocks
        conv=notrunc    Don't truncate output file
        conv=noerror    Continue after read errors
        conv=sync       Pad blocks with zeros
        conv=fsync      Physically write data out before finishing
        conv=swab       Swap every pair of bytes
        iflag=skip_bytes        skip=N is in bytes

N may be suffixed by c (1), w (2), b (512), kB (1000), k (1024), MB, M, GB, G
```

#### devmem

```
Usage: devmem ADDRESS [WIDTH [VALUE]]

Read/write from physical address

    ADDRESS Address to act upon
    WIDTH   Width (8/16/...)
    VALUE   Data to be written
```

#### df

```
Usage: df [-PkmhT] [FILESYSTEM]...

Print filesystem usage statistics

    -P      POSIX output format
    -k      1024-byte blocks (default)
    -m      1M-byte blocks
    -h      Human readable (e.g. 1K 243M 2G)
    -T      Print filesystem type
```

#### diag_flash_logger

```
Usage for diag_flash_logger:

    -f, --filemsm:   mask file name for MSM
    -m, --filemdm:   mask file name for MDM
    -l, --filelist:  name of file containing list of mask files
    -o, --output:    output directory name
    -p, --peripheral:        bit mask for the peripherals interested
    -s, --size:      maximum file size in MB
    -w, --wait:      waiting for directory
    -k, --kill:      kill existing instance of diag_flash_logger
    -c  --cleanmask:         Send mask cleanup to modem at exit
    -d  --disablecon:        Disable console messages
    -e  --enablelock:        Run using wake lock to keep APPS processor on
    -b  --nonrealtime:       Have peripherals buffer data and send data in non-real-time
    -r  --renamefiles:       Rename dir/file names to time when closed
    -a  --hdlcdisable:       Disbale hdlc encoding
    -h, --help:      usage help

e.g. diag_flash_logger -m <mask_file name> -o <output dir> -s <size in bytes> -c
```

#### diag_lite_log

```
Usage: diag_lite_log [-r <id>] [-hcdpl]
       diag_lite_log [-f] <dumped_log.dump>

  Running without arguments, log messages will be printed to stdout
  and act as a log daemon

    -l   run as a log daemon
    -r   radio id (default: 0, which points to '/sys/class/net/soc0/target_type')
    -d   decode dumped log (default file: /var/run/r0_fw_log.dump)
    -m   data.msc file path (default file: /lib/firmware/<radio>/Data.mcs).
                    Note: in dual mac mode Data_dualmac.msc is used
    Daemon control:
    -p   receive log from daemon
    -c   clear log from daemon
    -f   create dump log from daemon (default file: /var/run/r0_fw_log.dump)
```

#### diag_socket_app

```
 Usage for diag_socket_app:

    -a, --address:   IP address
    -d, --device:    Device number(0: IPQ, 1: MDM1, 2: MDM2 3: MDM3)
    -p, --port:      Port number
    -r, --retry:     Number of retries for connect
    -e  --enable wakelock:   Run using wake lock to keep APPS processor on
    -k, --kill:      kill existing instance of diag_socket_log
    -h, --help:      usage help

e.g. diag_socket_log -a <ip address> -p <port number> -r <num retries>
```

#### diag_stress_app

```
Usage for diag_stress_app:

    -t, --threads: maximum number of stress test tasks to support
    -d, --verbose: prints stress test task information
    -h, --help:    help

e.g. test_diag -v -t 5 can support upto 5 stress test threads at the same time
```

#### diff

```
Usage: diff [-abBdiNqrTstw] [-L LABEL] [-S FILE] [-U LINES] FILE1 FILE2

Compare files line by line and output the differences between them.
This implementation supports unified diffs only.

    -a      Treat all files as text
    -b      Ignore changes in the amount of whitespace
    -B      Ignore changes whose lines are all blank
    -d      Try hard to find a smaller set of changes
    -i      Ignore case differences
    -L      Use LABEL instead of the filename in the unified header
    -N      Treat absent files as empty
    -q      Output only whether files differ
    -r      Recurse
    -S      Start with FILE when comparing directories
    -T      Make tabs line up by prefixing a tab when necessary
    -s      Report when two files are the same
    -t      Expand tabs to spaces in output
    -U      Output LINES lines of context
    -w      Ignore all whitespace
```

#### dirname

```
Usage: dirname FILENAME

Strip non-directory suffix from FILENAME
```

#### dmesg

```
Usage: dmesg [-c] [-n LEVEL] [-s SIZE]

Print or control the kernel ring buffer

        -c              Clear ring buffer after printing
        -n LEVEL        Set console logging level
        -s SIZE         Buffer size
        -r              Print raw message buffer
```

#### dnsmasq

```
Usage: dnsmasq [options]

Valid options are:
-a, --listen-address=<ipaddr>                          Specify local address(es) to listen on.
-A, --address=/<domain>/<ipaddr>                       Return ipaddr for all hosts in specified domains.
-b, --bogus-priv                                       Fake reverse lookups for RFC1918 private address ranges.
-B, --bogus-nxdomain=<ipaddr>                          Treat ipaddr as NXDOMAIN (defeats Verisign wildcard).
-c, --cache-size=<integer>                             Specify the size of the cache in entries (defaults to 150).
-C, --conf-file=<path>                                 Specify configuration file (defaults to /etc/dnsmasq.conf).
-d, --no-daemon                                        Do NOT fork into the background: run in debug mode.
-D, --domain-needed                                    Do NOT forward queries with no domain part.
-e, --selfmx                                           Return self-pointing MX records for local hosts.
-E, --expand-hosts                                     Expand simple names in /etc/hosts with domain-suffix.
-f, --filterwin2k                                      Don't forward spurious DNS requests from Windows hosts.
    --filter-A                                         Don't include IPv4 addresses in DNS answers.
    --filter-AAAA                                      Don't include IPv6 addresses in DNS answers.
    --filter-rr=<RR-type>                              Don't include resource records of the given type in DNS answers.
-F, --dhcp-range=<ipaddr>,...                          Enable DHCP in the range given with lease duration.
-g, --group=<groupname>                                Change to this group after startup (defaults to dip).
-G, --dhcp-host=<hostspec>                             Set address or hostname for a specified machine.
    --dhcp-hostsfile=<path>                            Read DHCP host specs from file.
    --dhcp-optsfile=<path>                             Read DHCP option specs from file.
    --dhcp-hostsdir=<path>                             Read DHCP host specs from a directory.
    --dhcp-optsdir=<path>                              Read DHCP options from a directory.
    --tag-if=tag-expression                            Evaluate conditional tag expression.
-h, --no-hosts                                         Do NOT load /etc/hosts file.
-H, --addn-hosts=<path>                                Specify a hosts file to be read in addition to /etc/hosts.
    --hostsdir=<path>                                  Read hosts files from a directory.
-i, --interface=<interface>                            Specify interface(s) to listen on.
-I, --except-interface=<interface>                     Specify interface(s) NOT to listen on.
-j, --dhcp-userclass=set:<tag>,<class>                 Map DHCP user class to tag.
    --dhcp-circuitid=set:<tag>,<circuit>               Map RFC3046 circuit-id to tag.
    --dhcp-remoteid=set:<tag>,<remote>                 Map RFC3046 remote-id to tag.
    --dhcp-subscrid=set:<tag>,<remote>                 Map RFC3993 subscriber-id to tag.
    --dhcp-pxe-vendor=<vendor>[,...]                   Specify vendor class to match for PXE requests.
-J, --dhcp-ignore=tag:<tag>...                         Don't do DHCP for hosts with tag set.
    --dhcp-broadcast[=tag:<tag>...]                    Force broadcast replies for hosts with tag set.
-k, --keep-in-foreground                               Do NOT fork into the background, do NOT run in debug mode.
-K, --dhcp-authoritative                               Assume we are the only DHCP server on the local network.
-l, --dhcp-leasefile=<path>                            Specify where to store DHCP leases (defaults to /var/lib/misc/dnsmasq.leases).
-L, --localmx                                          Return MX records for local hosts.
-m, --mx-host=<host_name>,<target>,<pref>              Specify an MX record.
-M, --dhcp-boot=<bootp opts>                           Specify BOOTP options to DHCP server.
-n, --no-poll                                          Do NOT poll /etc/resolv.conf file, reload only on SIGHUP.
-N, --no-negcache                                      Do NOT cache failed search results.
    --use-stale-cache[=<max_expired>]                  Use expired cache data for faster reply.
-o, --strict-order                                     Use nameservers strictly in the order given in /etc/resolv.conf.
-O, --dhcp-option=<optspec>                            Specify options to be sent to DHCP clients.
    --dhcp-option-force=<optspec>                      DHCP option sent even if the client does not request it.
-p, --port=<integer>                                   Specify port to listen for DNS requests on (defaults to 53).
-P, --edns-packet-max=<integer>                        Maximum supported UDP packet size for EDNS.0 (defaults to 1232).
-q, --log-queries                                      Log DNS queries.
-Q, --query-port=<integer>                             Force the originating port for upstream DNS queries.
    --port-limit=#ports                                Set maximum number of random originating ports for a query.
-R, --no-resolv                                        Do NOT read resolv.conf.
-r, --resolv-file=<path>                               Specify path to resolv.conf (defaults to /etc/resolv.conf).
    --servers-file=<path>                              Specify path to file with server= options
-S, --server=/<domain>/<ipaddr>                        Specify address(es) of upstream servers with optional domains.
    --rev-server=<addr>/<prefix>,<ipaddr>              Specify address of upstream servers for reverse address queries
    --local=/<domain>/                                 Never forward queries to specified domains.
-s, --domain=<domain>[,<range>]                        Specify the domain to be assigned in DHCP leases.
-t, --mx-target=<host_name>                            Specify default target in an MX record.
-T, --local-ttl=<integer>                              Specify time-to-live in seconds for replies from /etc/hosts.
    --neg-ttl=<integer>                                Specify time-to-live in seconds for negative caching.
    --max-ttl=<integer>                                Specify time-to-live in seconds for maximum TTL to send to clients.
    --max-cache-ttl=<integer>                          Specify time-to-live ceiling for cache.
    --min-cache-ttl=<integer>                          Specify time-to-live floor for cache.
    --fast-dns-retry=<milliseconds>                    Retry DNS queries after this many milliseconds.
-u, --user=<username>                                  Change to this user after startup. (defaults to nobody).
-U, --dhcp-vendorclass=set:<tag>,<class>               Map DHCP vendor class to tag.
-v, --version                                          Display dnsmasq version and copyright information.
-V, --alias=<ipaddr>,<ipaddr>,<netmask>                Translate IPv4 addresses from upstream servers.
-W, --srv-host=<name>,<target>,...                     Specify a SRV record.
-w, --help                                             Display this message. Use --help dhcp or --help dhcp6 for known DHCP options.
-x, --pid-file=<path>                                  Specify path of PID file (defaults to /var/run/dnsmasq.pid).
-X, --dhcp-lease-max=<integer>                         Specify maximum number of DHCP leases (defaults to 1000).
-y, --localise-queries                                 Answer DNS queries based on the interface a query was sent to.
-Y, --txt-record=<name>,<txt>[,<txt]                   Specify TXT DNS record.
    --ptr-record=<name>,<target>                       Specify PTR DNS record.
    --interface-name=<name>,<interface>                Give DNS name to IPv4 address of interface.
-z, --bind-interfaces                                  Bind only to interfaces in use.
-Z, --read-ethers                                      Read DHCP static host information from /etc/ethers.
-1, --enable-dbus[=<busname>]                          Enable the DBus interface for setting upstream servers, etc.
    --enable-ubus[=<busname>]                          Enable the UBus interface.
-2, --no-dhcp-interface=<interface>                    Do not provide DHCP on this interface, only provide DNS.
    --no-dhcpv6-interface=<interface>                  Do not provide DHCPv6 on this interface.
    --no-dhcpv4-interface=<interface>                  Do not provide DHCPv4 on this interface.
-3, --bootp-dynamic[=tag:<tag>]...                     Enable dynamic address allocation for bootp.
-4, --dhcp-mac=set:<tag>,<mac address>                 Map MAC address (with wildcards) to option set.
    --bridge-interface=<iface>,<alias>..               Treat DHCP requests on aliases as arriving from interface.
    --shared-network=<iface>|<addr>,<addr>             Specify extra networks sharing a broadcast domain for DHCP
-5, --no-ping                                          Disable ICMP echo address checking in the DHCP server.
-6, --dhcp-script=<path>                               Shell script to run on DHCP lease creation and destruction.
    --dhcp-luascript=path                              Lua script to run on DHCP lease creation and destruction.
    --dhcp-scriptuser=<username>                       Run lease-change scripts as this user.
    --script-arp                                       Call dhcp-script with changes to local ARP table.
-7, --conf-dir=<path>                                  Read configuration from all the files in this directory.
    --conf-script=<path>                               Execute file and read configuration from stdin.
-8, --log-facility=<facility>|<file>                   Log to this syslog facility or file. (defaults to DAEMON)
-9, --leasefile-ro                                     Do not use leasefile.
-0, --dns-forward-max=<integer>                        Maximum number of concurrent DNS queries. (defaults to 150)
    --clear-on-reload                                  Clear DNS cache when reloading /etc/resolv.conf.
    --dhcp-ignore-names[=tag:<tag>]...                 Ignore hostnames provided by DHCP clients.
    --dhcp-no-override                                 Do NOT reuse filename and server fields for extra DHCP options.
    --enable-tftp[=<intr>[,<intr>]]                    Enable integrated read-only TFTP server.
    --tftp-root=<dir>[,<iface>]                        Export files by TFTP only from the specified subtree.
    --tftp-unique-root[=ip|mac]                        Add client IP or hardware address to tftp-root.
    --tftp-secure                                      Allow access only to files owned by the user running dnsmasq.
    --tftp-no-fail                                     Do not terminate the service if TFTP directories are inaccessible.
    --tftp-max=<integer>                               Maximum number of concurrent TFTP transfers (defaults to 50).
    --tftp-mtu=<integer>                               Maximum MTU to use for TFTP transfers.
    --tftp-no-blocksize                                Disable the TFTP blocksize extension.
    --tftp-lowercase                                   Convert TFTP filenames to lowercase
    --tftp-port-range=<start>,<end>                    Ephemeral port range for use by TFTP transfers.
    --tftp-single-port                                 Use only one port for TFTP server.
    --log-dhcp                                         Extra logging for DHCP.
    --log-async[=<integer>]                            Enable async. logging; optionally set queue length.
    --stop-dns-rebind                                  Stop DNS rebinding. Filter private IP ranges when resolving.
    --rebind-localhost-ok                              Allow rebinding of 127.0.0.0/8, for RBL servers.
    --rebind-domain-ok=/<domain>/                      Inhibit DNS-rebind protection on this domain.
    --all-servers                                      Always perform DNS queries to all servers.
    --dhcp-match=set:<tag>,<optspec>                   Set tag if client includes matching option in request.
    --dhcp-name-match=set:<tag>,<string>[*]            Set tag if client provides given name.
    --dhcp-alternate-port[=<ports>]                    Use alternative ports for DHCP.
    --naptr-record=<name>,<naptr>                      Specify NAPTR DNS record.
    --min-port=<port>                                  Specify lowest port available for DNS query transmission.
    --max-port=<port>                                  Specify highest port available for DNS query transmission.
    --dhcp-fqdn                                        Use only fully qualified domain names for DHCP clients.
    --dhcp-generate-names[=tag:<tag>]                  Generate hostnames based on MAC address for nameless clients.
    --dhcp-proxy[=<ipaddr>]...                         Use these DHCP relays as full proxies.
    --dhcp-relay=<local-addr>,<server>[,<iface>]       Relay DHCP requests to a remote server
    --cname=<alias>,<target>[,<ttl>]                   Specify alias name for LOCAL DNS name.
    --pxe-prompt=<prompt>,[<timeout>]                  Prompt to send to PXE clients.
    --pxe-service=<service>                            Boot service for PXE menu.
    --test                                             Check configuration syntax.
    --add-mac[=base64|text]                            Add requestor's MAC address to forwarded DNS queries.
    --strip-mac                                        Strip MAC information from queries.
    --add-subnet=<v4 pref>[,<v6 pref>]                 Add specified IP subnet to forwarded DNS queries.
    --strip-subnet                                     Strip ECS information from queries.
    --add-cpe-id=<text>                                Add client identification to forwarded DNS queries.
    --proxy-dnssec                                     Proxy DNSSEC validation results from upstream nameservers.
    --dhcp-sequential-ip                               Attempt to allocate sequential IP addresses to DHCP clients.
    --dhcp-ignore-clid                                 Ignore client identifier option sent by DHCP clients.
    --conntrack                                        Copy connection-track mark from queries to upstream connections.
    --dhcp-client-update                               Allow DHCP clients to do their own DDNS updates.
    --enable-ra                                        Send router-advertisements for interfaces doing DHCPv6
    --dhcp-duid=<enterprise>,<duid>                    Specify DUID_EN-type DHCPv6 server DUID
    --host-record=<name>,<address>[,<ttl>]             Specify host (A/AAAA and PTR) records
    --dynamic-host=<name>,[<IPv4>][,<IPv6>],<interface-Specify host record in interface subnet
    --caa-record=<name>,<flags>,<tag>,<value>          Specify certification authority authorization record
    --dns-rr=<name>,<RR-number>,[<data>]               Specify arbitrary DNS resource record
    --bind-dynamic                                     Bind to interfaces in use - check for new interfaces
    --auth-server=<NS>,<interface>                     Export local names to global DNS
    --auth-zone=<domain>,[<subnet>...]                 Domain to export to global DNS
    --auth-ttl=<integer>                               Set TTL for authoritative replies
    --auth-soa=<serial>[,...]                          Set authoritative zone information
    --auth-sec-servers=<NS>[,<NS>...]                  Secondary authoritative nameservers for forward domains
    --auth-peer=<ipaddr>[,<ipaddr>...]                 Peers which are allowed to do zone transfer
    --ipset=/<domain>[/<domain>...]/<ipset>...         Specify ipsets to which matching domains should be added
    --nftset=/<domain>[/<domain>...]/<nftset>...       Specify nftables sets to which matching domains should be added
    --connmark-allowlist-enable[=<mask>]               Enable filtering of DNS queries with connection-track marks.
    --connmark-allowlist=<connmark>[/<mask>][,<pattern>Set allowed DNS patterns for a connection-track mark.
    --synth-domain=<domain>,<range>,[<prefix>]         Specify a domain and address range for synthesised names
    --dnssec                                           Activate DNSSEC validation
    --trust-anchor=<domain>,[<class>],...              Specify trust anchor key digest.
    --dnssec-debug                                     Disable upstream checking for DNSSEC debugging.
    --dnssec-check-unsigned                            Ensure answers without DNSSEC are in unsigned zones.
    --dnssec-no-timecheck                              Don't check DNSSEC signature timestamps until first cache-reload
    --dnssec-timestamp=<path>                          Timestamp file to verify system clock for DNSSEC
    --dnssec-limits=<limit>,..                         Set resource limits for DNSSEC validation
    --ra-param=<iface>,[mtu:<value>|<interface>|off,][<Set MTU, priority, resend-interval and router-lifetime
    --quiet-dhcp                                       Do not log routine DHCP.
    --quiet-dhcp6                                      Do not log routine DHCPv6.
    --quiet-ra                                         Do not log RA.
    --log-debug                                        Log debugging information.
    --local-service                                    Accept queries only from directly-connected networks.
    --dns-loop-detect                                  Detect and remove DNS forwarding loops.
    --ignore-address=<ipaddr>                          Ignore DNS responses containing ipaddr.
    --dhcp-ttl=<ttl>                                   Set TTL in DNS responses with DHCP-derived addresses.
    --dhcp-reply-delay=<integer>                       Delay DHCP replies for at least number of seconds.
    --dhcp-rapid-commit                                Enables DHCPv4 Rapid Commit option.
    --dumpfile=<path>                                  Path to debug packet dump file.
    --dumpmask=<hex>                                   Mask which packets to dump.
    --script-on-renewal                                Call dhcp-script when lease expiry changes.
    --umbrella[=<optspec>]                             Send Cisco Umbrella identifiers including remote IP.
    --quiet-tftp                                       Do not log routine TFTP.
    --no-round-robin                                   Suppress round-robin ordering of DNS records.
    --no-ident                                         Do not add CHAOS TXT records.
    --cache-rr=<RR-type>                               Cache this DNS resource record type.
    --max-tcp-connections=<integer>                    Maximum number of concurrent tcp connections.
```

#### dotlockfile

```
Usage:  dotlockfile [-l [-r retries] |-u|-t|-c] [-p] [-m|lockfile]
```

#### downlink-monitor

```
Dropbear server v2022.83 https://matt.ucc.asn.au/dropbear/dropbear.html

Usage: dropbear [options]

    -b bannerfile   Display the contents of bannerfile before user login
                    (default: none)
    -r keyfile      Specify hostkeys (repeatable)
                    defaults:
                    - dss /etc/dropbear/dropbear_dss_host_key
                    - rsa /etc/dropbear/dropbear_rsa_host_key
                    - ecdsa /etc/dropbear/dropbear_ecdsa_host_key
                    - ed25519 /etc/dropbear/dropbear_ed25519_host_key
    -R              Create hostkeys as required
    -F              Don't fork into background
    -e              Pass on server process environment to child process
    -E              Log to stderr rather than syslog
    -w              Disallow root logins
    -G              Restrict logins to members of specified group
    -s              Disable password logins
    -g              Disable password logins for root
    -B              Allow blank password logins
    -t              Enable two-factor authentication (both password and public key required)
    -T              Maximum authentication tries (default 10)
    -j              Disable local port forwarding
    -k              Disable remote port forwarding
    -a              Allow connections to forwarded ports from any host
    -c command      Force executed command
    -p [address:]port
                    Listen on specified tcp port (and optionally address),
                    up to 10 can be specified
                    (default port is 22 if none specified)
    -P PidFile      Create pid file PidFile
                    (default /var/run/dropbear.pid)
    -W <receive_window_buffer> (default 24576, larger may be faster, max 10MB)
    -K <keepalive>  (0 is never, default 0, in seconds)
    -I <idle_timeout>  (0 is never, default 0, in seconds)
    -z    disable QoS
    -V    Version
```

#### dropbear

```
Dropbear server v2022.83 https://matt.ucc.asn.au/dropbear/dropbear.html

Usage: dropbear [options]

    -b bannerfile   Display the contents of bannerfile before user login
                    (default: none)
    -r keyfile      Specify hostkeys (repeatable)
                    defaults:
                    - dss /etc/dropbear/dropbear_dss_host_key
                    - rsa /etc/dropbear/dropbear_rsa_host_key
                    - ecdsa /etc/dropbear/dropbear_ecdsa_host_key
                    - ed25519 /etc/dropbear/dropbear_ed25519_host_key
    -R              Create hostkeys as required
    -F              Don't fork into background
    -e              Pass on server process environment to child process
    -E              Log to stderr rather than syslog
    -w              Disallow root logins
    -G              Restrict logins to members of specified group
    -s              Disable password logins
    -g              Disable password logins for root
    -B              Allow blank password logins
    -t              Enable two-factor authentication (both password and public key required)
    -T              Maximum authentication tries (default 10)
    -j              Disable local port forwarding
    -k              Disable remote port forwarding
    -a              Allow connections to forwarded ports from any host
    -c command      Force executed command
    -p [address:]port
                    Listen on specified tcp port (and optionally address),
                    up to 10 can be specified
                    (default port is 22 if none specified)
    -P PidFile      Create pid file PidFile
                    (default /var/run/dropbear.pid)
    -W <receive_window_buffer> (default 24576, larger may be faster, max 10MB)
    -K <keepalive>  (0 is never, default 0, in seconds)
    -I <idle_timeout>  (0 is never, default 0, in seconds)
    -z    disable QoS
    -V    Version
```

#### dropbearkey

```
Usage: dropbearkey -t <type> -f <filename> [-s bits]

    -t type Type of key to generate. One of:
                    rsa
                    dss
                    ecdsa
                    ed25519
    -f filename    Use filename for the secret key.
                   ~/.ssh/id_dropbear is recommended for client keys.
    -s bits Key size in bits, should be a multiple of 8 (optional)
               DSS has a fixed size of 1024 bits
               ECDSA has sizes 256 384 521
               Ed25519 has a fixed size of 256 bits
    -y              Just print the publickey and fingerprint for the
                    private key in <filename>.
```

#### du

```
Usage: du [-aHLdclsxhmk] [FILE]...

Summarize disk space used for each FILE and/or directory

    -a      Show file sizes too
    -L      Follow all symlinks
    -H      Follow symlinks on command line
    -d N    Limit output to directories (and files with -a) of depth < N
    -c      Show grand total
    -l      Count sizes many times if hard linked
    -s      Display only a total for each argument
    -x      Skip directories on different filesystems
    -h      Sizes in human readable format (e.g., 1K 243M 2G)
    -m      Sizes in megabytes
    -k      Sizes in kilobytes (default)
```

#### e2fsck

```
Usage: e2fsck [-panyrcdfktvDFV] [-b superblock] [-B blocksize]
        [-l|-L bad_blocks_file] [-C fd] [-j external_journal]
        [-E extended-options] [-z undo_file] device

Emergency help:
    -p                   Automatic repair (no questions)
    -n                   Make no changes to the filesystem
    -y                   Assume "yes" to all questions
    -c                   Check for bad blocks and add them to the badblock list
    -f                   Force checking even if filesystem is marked clean
    -v                   Be verbose
    -b superblock        Use alternative superblock
    -B blocksize         Force blocksize when looking for superblock
    -j external_journal  Set location of the external journal
    -l bad_blocks_file   Add to badblocks list
    -L bad_blocks_file   Set badblocks list
    -z undo_file         Create an undo file
```

#### ebtables

```
ebtables v2.0.10-4 (December 2011)

Usage:
ebtables -[ADI] chain rule-specification [options]
ebtables -P chain target
ebtables -[LFZ] [chain]
ebtables -[NX] [chain]
ebtables -E old-chain-name new-chain-name

Commands:
    --append -A chain             : append to chain
    --delete -D chain             : delete matching rule from chain
    --delete -D chain rulenum     : delete rule at position rulenum from chain
    --change-counters -C chain
              [rulenum] pcnt bcnt : change counters of existing rule
    --insert -I chain rulenum     : insert rule at position rulenum in chain
    --list   -L [chain]           : list the rules in a chain or in all chains
    --flush  -F [chain]           : delete all rules in chain or in all chains
    --init-table                  : replace the kernel table with the initial table
    --zero   -Z [chain]           : put counters on zero in chain or in all chains
    --policy -P chain target      : change policy on chain to target
    --new-chain -N chain          : create a user defined chain
    --rename-chain -E old new     : rename a chain
    --delete-chain -X [chain]     : delete a user defined chain
    --atomic-commit               : update the kernel w/t table contained in <FILE>
    --atomic-init                 : put the initial kernel table into <FILE>
    --atomic-save                 : put the current kernel table into <FILE>
    --atomic-file file            : set <FILE> to file

Options:
    --proto  -p [!] proto         : protocol hexadecimal, by name or LENGTH
    --src    -s [!] address[/mask]: source mac address
    --dst    -d [!] address[/mask]: destination mac address
    --in-if  -i [!] name[+]       : network input interface name
    --out-if -o [!] name[+]       : network output interface name
    --logical-in  [!] name[+]     : logical bridge input interface name
    --logical-out [!] name[+]     : logical bridge output interface name
    --set-counters -c chain
              pcnt bcnt           : set the counters of the to be added rule
    --modprobe -M program         : try to insert modules using this program
    --concurrent                  : use a file lock to support concurrent scripts
    --version -V                  : print package version

Environment variable:
    EBTABLES_ATOMIC_FILE          : if set <FILE> (see above) will equal its value

Standard targets: DROP, ACCEPT, RETURN or CONTINUE;
The target can also be a user defined chain.

Supported chains for the filter table:
    INPUT FORWARD OUTPUT
```

#### echo

> Prints argument to std


#### ecm_dump.sh
#### edma_dump

```
sh edma_dump.sh [miami|alder] [general|txdesc|txcmpl|rxdesc|rxfill|full] [ring_num] [cache]
```

#### egrep
#### egtool

```
Usage: egtool [options]
Options:
    show - Show the available entropy, in bits
    add - Add some additional entropy to the input pool, incrementing the entropy count
```

#### eip_dump.sh

```
eip_dump.sh <param>
    all: Dumps Everything
    ipsec: Dumps statistics for all IPsec tunnel
    ipsectun<0|1|..>: Dumps statistics for specified ipsectunX
    reg: Dumps general Register configuration
    stats: Dumps all statistics
    desc [ring] [count] : Dumps recent command & result descriptor equal to count
    cmd [ring] [count] : Dumps recent command descriptor equal to count
    sh -x <script> : Run script in trace mode (optional)
```

#### element-adopt-monitor
#### env

```
Usage: env [-iu] [-] [name=value]... [PROG ARGS]

Print the current environment or run PROG after setting up
the specified environment

    -, -i   Start with an empty environment
    -u      Remove variable from the environment
```

#### ethtool

```
ethtool version 6.6
Usage:
        ethtool [ FLAGS ]  DEVNAME      Display standard information about device
        ethtool [ FLAGS ] -s|--change DEVNAME   Change generic options
                [ speed %d ]
                [ lanes %d ]
                [ duplex half|full ]
                [ port tp|aui|bnc|mii|fibre|da ]
                [ mdix auto|on|off ]
                [ autoneg on|off ]
                [ advertise %x[/%x] | mode on|off ... [--] ]
                [ phyad %d ]
                [ xcvr internal|external ]
                [ wol %d[/%d] | p|u|m|b|a|g|s|f|d... ]
                [ sopass %x:%x:%x:%x:%x:%x ]
                [ msglvl %d[/%d] | type on|off ... [--] ]
                [ master-slave preferred-master|preferred-slave|forced-master|forced-slave ]
        ethtool [ FLAGS ] -a|--show-pause DEVNAME       Show pause options
                [ --src aggregate | emac | pmac ]
        ethtool [ FLAGS ] -A|--pause DEVNAME    Set pause options
                [ autoneg on|off ]
                [ rx on|off ]
                [ tx on|off ]
        ethtool [ FLAGS ] -c|--show-coalesce DEVNAME    Show coalesce options
        ethtool [ FLAGS ] -C|--coalesce DEVNAME Set coalesce options
                [adaptive-rx on|off]
                [adaptive-tx on|off]
                [rx-usecs N]
                [rx-frames N]
                [rx-usecs-irq N]
                [rx-frames-irq N]
                [tx-usecs N]
                [tx-frames N]
                [tx-usecs-irq N]
                [tx-frames-irq N]
                [stats-block-usecs N]
                [pkt-rate-low N]
                [rx-usecs-low N]
                [rx-frames-low N]
                [tx-usecs-low N]
                [tx-frames-low N]
                [pkt-rate-high N]
                [rx-usecs-high N]
                [rx-frames-high N]
                [tx-usecs-high N]
                [tx-frames-high N]
                [sample-interval N]
                [cqe-mode-rx on|off]
                [cqe-mode-tx on|off]
                [tx-aggr-max-bytes N]
                [tx-aggr-max-frames N]
                [tx-aggr-time-usecs N]
        ethtool [ FLAGS ] -g|--show-ring DEVNAME        Query RX/TX ring parameters
        ethtool [ FLAGS ] -G|--set-ring DEVNAME Set RX/TX ring parameters
                [ rx N ]
                [ rx-mini N ]
                [ rx-jumbo N ]
                [ tx N ]
                [ rx-buf-len N ]
                [ cqe-size N ]
                [ tx-push on|off ]
                [ rx-push on|off ]
                [ tx-push-buf-len N]
        ethtool [ FLAGS ] -k|--show-features|--show-offload DEVNAME     Get state of protocol offload and other features
        ethtool [ FLAGS ] -K|--features|--offload DEVNAME       Set protocol offload and other features
                FEATURE on|off ...
        ethtool [ FLAGS ] -i|--driver DEVNAME   Show driver information
        ethtool [ FLAGS ] -d|--register-dump DEVNAME    Do a register dump
                [ raw on|off ]
                [ file FILENAME ]
        ethtool [ FLAGS ] -e|--eeprom-dump DEVNAME      Do a EEPROM dump
                [ raw on|off ]
                [ offset N ]
                [ length N ]
        ethtool [ FLAGS ] -E|--change-eeprom DEVNAME    Change bytes in device EEPROM
                [ magic N ]
                [ offset N ]
                [ length N ]
                [ value N ]
        ethtool [ FLAGS ] -r|--negotiate DEVNAME        Restart N-WAY negotiation
        ethtool [ FLAGS ] -p|--identify DEVNAME Show visible port identification (e.g. blinking)
                [ TIME-IN-SECONDS ]
        ethtool [ FLAGS ] -t|--test DEVNAME     Execute adapter self test
                [ online | offline | external_lb ]
        ethtool [ FLAGS ] -S|--statistics DEVNAME       Show adapter statistics
                [ --all-groups | --groups [eth-phy] [eth-mac] [eth-ctrl] [rmon] ]
                [ --src aggregate | emac | pmac ]
        ethtool [ FLAGS ] --phy-statistics DEVNAME      Show phy statistics
        ethtool [ FLAGS ] -n|-u|--show-nfc|--show-ntuple DEVNAME        Show Rx network flow classification options or rules
                [ rx-flow-hash tcp4|udp4|ah4|esp4|sctp4|tcp6|udp6|ah6|esp6|sctp6 [context %d] |
                  rule %d ]
        ethtool [ FLAGS ] -N|-U|--config-nfc|--config-ntuple DEVNAME    Configure Rx network flow classification options or rules
                rx-flow-hash tcp4|udp4|ah4|esp4|sctp4|tcp6|udp6|ah6|esp6|sctp6 m|v|t|s|d|f|n|r... [context %d] |
                flow-type ether|ip4|tcp4|udp4|sctp4|ah4|esp4|ip6|tcp6|udp6|ah6|esp6|sctp6
                        [ src %x:%x:%x:%x:%x:%x [m %x:%x:%x:%x:%x:%x] ]
                        [ dst %x:%x:%x:%x:%x:%x [m %x:%x:%x:%x:%x:%x] ]
                        [ proto %d [m %x] ]
                        [ src-ip IP-ADDRESS [m IP-ADDRESS] ]
                        [ dst-ip IP-ADDRESS [m IP-ADDRESS] ]
                        [ tos %d [m %x] ]
                        [ tclass %d [m %x] ]
                        [ l4proto %d [m %x] ]
                        [ src-port %d [m %x] ]
                        [ dst-port %d [m %x] ]
                        [ spi %d [m %x] ]
                        [ vlan-etype %x [m %x] ]
                        [ vlan %x [m %x] ]
                        [ user-def %x [m %x] ]
                        [ dst-mac %x:%x:%x:%x:%x:%x [m %x:%x:%x:%x:%x:%x] ]
                        [ action %d ] | [ vf %d queue %d ]
                        [ context %d ]
                        [ loc %d ] |
                delete %d
        ethtool [ FLAGS ] -T|--show-time-stamping DEVNAME       Show time stamping capabilities
        ethtool [ FLAGS ] -x|--show-rxfh-indir|--show-rxfh DEVNAME      Show Rx flow hash indirection table and/or RSS hash key
                [ context %d ]
        ethtool [ FLAGS ] -X|--set-rxfh-indir|--rxfh DEVNAME    Set Rx flow hash indirection table and/or RSS hash key
                [ context %d|new ]
                [ equal N | weight W0 W1 ... | default ]
                [ hkey %x:%x:%x:%x:%x:.... ]
                [ hfunc FUNC ]
                [ delete ]
        ethtool [ FLAGS ] -f|--flash DEVNAME    Flash firmware image from the specified file to a region on the device
                FILENAME [ REGION-NUMBER-TO-FLASH ]
        ethtool [ FLAGS ] -P|--show-permaddr DEVNAME    Show permanent hardware address
        ethtool [ FLAGS ] -w|--get-dump DEVNAME Get dump flag, data
                [ data FILENAME ]
        ethtool [ FLAGS ] -W|--set-dump DEVNAME Set dump flag of the device
                N
        ethtool [ FLAGS ] -l|--show-channels DEVNAME    Query Channels
        ethtool [ FLAGS ] -L|--set-channels DEVNAME     Set Channels
                [ rx N ]
                [ tx N ]
                [ other N ]
                [ combined N ]
        ethtool [ FLAGS ] --show-priv-flags DEVNAME     Query private flags
        ethtool [ FLAGS ] --set-priv-flags DEVNAME      Set private flags
                FLAG on|off ...
        ethtool [ FLAGS ] -m|--dump-module-eeprom|--module-info DEVNAME Query/Decode Module EEPROM information and optical diagnostics if available
                [ raw on|off ]
                [ hex on|off ]
                [ offset N ]
                [ length N ]
                [ page N ]
                [ bank N ]
                [ i2c N ]
        ethtool [ FLAGS ] --show-eee DEVNAME    Show EEE settings
        ethtool [ FLAGS ] --set-eee DEVNAME     Set EEE settings
                [ eee on|off ]
                [ advertise %x ]
                [ tx-lpi on|off ]
                [ tx-timer %d ]
        ethtool [ FLAGS ] --set-phy-tunable DEVNAME     Set PHY tunable
                [ downshift on|off [count N] ]
                [ fast-link-down on|off [msecs N] ]
                [ energy-detect-power-down on|off [msecs N] ]
        ethtool [ FLAGS ] --get-phy-tunable DEVNAME     Get PHY tunable
                [ downshift ]
                [ fast-link-down ]
                [ energy-detect-power-down ]
        ethtool [ FLAGS ] --get-tunable DEVNAME Get tunable
                [ rx-copybreak ]
                [ tx-copybreak ]
                [ tx-buf-size ]
                [ pfc-prevention-tout ]
        ethtool [ FLAGS ] --set-tunable DEVNAME Set tunable
                [ rx-copybreak N ]
                [ tx-copybreak N ]
                [ tx-buf-size N ]
                [ pfc-prevention-tout N ]
        ethtool [ FLAGS ] --reset DEVNAME       Reset components
                [ flags %x ]
                [ mgmt ]
                [ mgmt-shared ]
                [ irq ]
                [ irq-shared ]
                [ dma ]
                [ dma-shared ]
                [ filter ]
                [ filter-shared ]
                [ offload ]
                [ offload-shared ]
                [ mac ]
                [ mac-shared ]
                [ phy ]
                [ phy-shared ]
                [ ram ]
                [ ram-shared ]
                [ ap ]
                [ ap-shared ]
                [ dedicated ]
                [ all ]
        ethtool [ FLAGS ] --show-fec DEVNAME    Show FEC settings
        ethtool [ FLAGS ] --set-fec DEVNAME     Set FEC settings
                [ encoding auto|off|rs|baser|llrs [...] ]
        ethtool [ FLAGS ] -Q|--per-queue DEVNAME        Apply per-queue command.
The supported sub commands include --show-coalesce, --coalesce          [queue_mask %x] SUB_COMMAND
        ethtool [ FLAGS ] --cable-test DEVNAME  Perform a cable test
        ethtool [ FLAGS ] --cable-test-tdr DEVNAME      Print cable test time domain reflectrometery data
                [ first N ]
                [ last N ]
                [ step N ]
                [ pair N ]
        ethtool [ FLAGS ] --show-tunnels DEVNAME        Show NIC tunnel offload information
        ethtool [ FLAGS ] --show-module DEVNAME Show transceiver module settings
        ethtool [ FLAGS ] --set-module DEVNAME  Set transceiver module settings
                [ power-mode-policy high|auto ]
        ethtool [ FLAGS ] --get-plca-cfg DEVNAME        Get PLCA configuration
        ethtool [ FLAGS ] --set-plca-cfg DEVNAME        Set PLCA configuration
                [ enable on|off ]
                [ node-id N ]
                [ node-cnt N ]
                [ to-tmr N ]
                [ burst-cnt N ]
                [ burst-tmr N ]
        ethtool [ FLAGS ] --get-plca-status DEVNAME     Get PLCA status information
        ethtool [ FLAGS ] --show-mm DEVNAME     Show MAC merge layer state
        ethtool [ FLAGS ] --set-mm DEVNAME      Set MAC merge layer parameters
                [ verify-enabled on|off ]
                [ verify-time N ]
                [ tx-enabled on|off ]
                [ pmac-enabled on|off ]
                [ tx-min-frag-size 60-252 ]
        ethtool [ FLAGS ] --show-pse DEVNAME    Show settings for Power Sourcing Equipment
        ethtool [ FLAGS ] --set-pse DEVNAME     Set Power Sourcing Equipment settings
                [ podl-pse-admin-control enable|disable ]
        ethtool [ FLAGS ] -h|--help             Show this help
        ethtool [ FLAGS ] --version             Show version number

FLAGS:
        --debug MASK    turn on debugging messages
        --json          enable JSON output format (not supported by all commands)
        -I|--include-statistics         request device statistics related to the command (not supported by all commands)
```

#### expr

```
Usage: expr EXPRESSION

Print the value of EXPRESSION to stdout

EXPRESSION may be:
        ARG1 | ARG2     ARG1 if it is neither null nor 0, otherwise ARG2
        ARG1 & ARG2     ARG1 if neither argument is null or 0, otherwise 0
        ARG1 < ARG2     1 if ARG1 is less than ARG2, else 0. Similarly:
        ARG1 <= ARG2
        ARG1 = ARG2
        ARG1 != ARG2
        ARG1 >= ARG2
        ARG1 > ARG2
        ARG1 + ARG2     Sum of ARG1 and ARG2. Similarly:
        ARG1 - ARG2
        ARG1 * ARG2
        ARG1 / ARG2
        ARG1 % ARG2
        STRING : REGEXP         Anchored pattern match of REGEXP in STRING
        match STRING REGEXP     Same as STRING : REGEXP
        substr STRING POS LENGTH Substring of STRING, POS counted from 1
        index STRING CHARS      Index in STRING where any CHARS is found, or 0
        length STRING           Length of STRING
        quote TOKEN             Interpret TOKEN as a string, even if
                                it is a keyword like 'match' or an
                                operator like '/'
        (EXPRESSION)            Value of EXPRESSION

Beware that many operators need to be escaped or quoted for shells.
Comparisons are arithmetic if both ARGs are numbers, else
lexicographical. Pattern matches return the string matched between
\( and \) or null; if \( and \) are not used, they return the number
of characters matched or 0.
```

#### exttool

```
Usage:

1:
exttool
    --chanswitch
    --interface wifiX
    --band <dest channel band>
    --chan <dest primary channel>
    --chwidth <channel width>
    --numcsa <channel switch announcement count>
    --secoffset <1: PLUS, 3: MINUS>
    --cfreq2 <secondary 80 centre channel freq, applicable only for 80+80 MHz>
    --punc <puncturing bit map>
    --force <force CSA even if target channel parameters are same as current channel parameters>
    --cfg80211

2:
exttool
    --scan
    --interface wifiX
    --wideband <0: 20 MHz scan, 1: wide band scan.
        [If set to 1, upper 16 bits are treated as scan chan width]
    >
    --mindwell <min dwell time> allowed range [50ms to less than <max dwell>]
    --maxdwell <max dwell time> allowed range [greater than min dwell to 10000ms]
    --resttime <rest time> allowed range [greater than 0]
    --maxscantime <max scan time> allowed range [greater than resttime]
    --idletime <idle time > allowed range [greater than 50ms]
    --scanmode <1: ACTIVE, 2: PASSIVE>
    --band <dest band>
    --chcount <Channel count followed by list of channels
        [chancount(1 to 32) <16 bit scan channel width><16 bit channel number>]
    >

3:
exttool
    --rptrmove
    --interface wifiX
    --band <target root AP band>
    --chan <target root AP channel>
    --ssid <SSID of target Root AP>
    --bssid <BSSID of target Root AP>
    --numcsa <channel switch announcement count>
    --cfreq2 <secondary 80 centre channel freq, applicable only for 80+80 MHz>

4:
exttool
    --list_chan_info
    --interface wifiX

5:
exttool
    --list_chan_state
    --interface wifiX

Usage:
thermaltool
    -i wifiX
    -get/-set -e [0/1: enable/disable]
    -et [event time in dutycycle units]
    -dc [duty cycle in ms]
    -dl [debug level]
    -pN [policy for lvl N]
    -loN [low th for lvl N]
    -hiN [high th for lvl N]
    -offN [Tx Off time for lvl N]
    -qpN [TxQ priority lvl N]
    -g
```

#### factorytest

```
Usage: factorytest <test>
 Supported tests:
        setup
        flash
        throughput
```

#### false
#### fanctrl_wrapper.sh
#### fdisk

```
Usage:
    fdisk [options] <disk>      change partition table
    fdisk [options] -l [<disk>] list partition table(s)

Display or manipulate a disk partition table.

Options:
     -b, --sector-size <size>      physical and logical sector size
     -B, --protect-boot            don't erase bootbits when creating a new label
     -c, --compatibility[=<mode>]  mode is 'dos' or 'nondos' (default)
     -L, --color[=<when>]          colorize output (auto, always or never)
                                     colors are enabled by default
     -l, --list                    display partitions and exit
     -o, --output <list>           output columns
     -t, --type <type>             recognize specified partition table type only
     -u, --units[=<unit>]          display units: 'cylinders' or 'sectors' (default)
     -s, --getsz                   display device size in 512-byte sectors [DEPRECATED]
         --bytes                   print SIZE in bytes rather than in human readable format
     -w, --wipe <mode>             wipe signatures (auto, always or never)
     -W, --wipe-partitions <mode>  wipe signatures from new partitions (auto, always or never)

     -C, --cylinders <number>      specify the number of cylinders
     -H, --heads <number>          specify the number of heads
     -S, --sectors <number>        specify the number of sectors per track

     -h, --help     display this help and exit
     -V, --version  output version information and exit

Available columns (for -o):
    gpt: Device Start End Sectors Size Type Type-UUID Attrs Name UUID
    dos: Device Start End Sectors Cylinders Size Type Id Attrs Boot End-C/H/S Start-C/H/S
    bsd: Slice Start End Sectors Cylinders Size Type Bsize Cpg Fsize
    sgi: Device Start End Sectors Cylinders Size Type Id Attrs
    sun: Device Start End Sectors Cylinders Size Type Id Flags

For more details see fdisk(8).
```

#### fgrep
#### find

```
Usage: find [-HL] [PATH]... [OPTIONS] [ACTIONS]

Search for files and perform actions on them.
First failed action stops processing of current file.
Defaults: PATH is current directory, action is '-print'

    -L,-follow      Follow symlinks
    -H              ...on command line only
    -xdev           Don't descend directories on other filesystems
    -maxdepth N     Descend at most N levels. -maxdepth 0 applies
                    actions to command line arguments only
    -mindepth N     Don't act on first N levels
    -depth          Act on directory *after* traversing it

Actions:
    ( ACTIONS )     Group actions for -o / -a
    ! ACT           Invert ACT's success/failure
    ACT1 [-a] ACT2  If ACT1 fails, stop, else do ACT2
    ACT1 -o ACT2    If ACT1 succeeds, stop, else do ACT2
                    Note: -a has higher priority than -o
    -name PATTERN   Match file name (w/o directory name) to PATTERN
    -iname PATTERN  Case insensitive -name
    -path PATTERN   Match path to PATTERN
    -ipath PATTERN  Case insensitive -path
    -regex PATTERN  Match path to regex PATTERN
    -type X         File type is X (one of: f,d,l,b,c,...)
    -perm MASK      At least one mask bit (+MASK), all bits (-MASK),
                    or exactly MASK bits are set in file's mode
    -mtime DAYS     mtime is greater than (+N), less than (-N),
                    or exactly N days in the past
    -user NAME/ID   File is owned by given user
    -group NAME/ID  File is owned by given group
    -size N[bck]    File size is N (c:bytes,k:kbytes,b:512 bytes(def.))
                    +/-N: file size is bigger/smaller than N
    -prune          If current file is directory, don't descend into it
    If none of the following actions is specified, -print is assumed
    -print          Print file name
    -print0         Print file name, NUL terminated
    -exec CMD ARG ; Run CMD with all instances of {} replaced by
                    file name. Fails if CMD exits with nonzero
```

#### firstboot
#### flock

```
Usage:
    flock [options] <file>|<directory> <command> [<argument>...]
    flock [options] <file>|<directory> -c <command>
    flock [options] <file descriptor number>

Manage file locks from shell scripts.

Options:
    -s, --shared             get a shared lock
    -x, --exclusive          get an exclusive lock (default)
    -u, --unlock             remove a lock
    -n, --nonblock           fail rather than wait
    -w, --timeout <secs>     wait for a limited amount of time
    -E, --conflict-exit-code <number>  exit code after conflict or timeout
    -o, --close              close file descriptor before running command
    -c, --command <command>  run a single command string through the shell
    -F, --no-fork            execute command without forking
    --verbose            increase verbosity
    
    -h, --help     display this help and exit
    -V, --version  output version information and exit

For more details see flock(1).
```

#### free

```
Usage: free

Display the amount of free and used system memory
```

#### fsck.ext2

```
Usage: fsck.ext2 [-panyrcdfktvDFV] [-b superblock] [-B blocksize]
                [-l|-L bad_blocks_file] [-C fd] [-j external_journal]
                [-E extended-options] [-z undo_file] device

Emergency help:
    -p                   Automatic repair (no questions)
    -n                   Make no changes to the filesystem
    -y                   Assume "yes" to all questions
    -c                   Check for bad blocks and add them to the badblock list
    -f                   Force checking even if filesystem is marked clean
    -v                   Be verbose
    -b superblock        Use alternative superblock
    -B blocksize         Force blocksize when looking for superblock
    -j external_journal  Set location of the external journal
    -l bad_blocks_file   Add to badblocks list
    -L bad_blocks_file   Set badblocks list
    -z undo_file         Create an undo file
```

#### fsck.ext3

```
Usage: fsck.ext3 [-panyrcdfktvDFV] [-b superblock] [-B blocksize]
                [-l|-L bad_blocks_file] [-C fd] [-j external_journal]
                [-E extended-options] [-z undo_file] device

Emergency help:
    -p                   Automatic repair (no questions)
    -n                   Make no changes to the filesystem
    -y                   Assume "yes" to all questions
    -c                   Check for bad blocks and add them to the badblock list
    -f                   Force checking even if filesystem is marked clean
    -v                   Be verbose
    -b superblock        Use alternative superblock
    -B blocksize         Force blocksize when looking for superblock
    -j external_journal  Set location of the external journal
    -l bad_blocks_file   Add to badblocks list
    -L bad_blocks_file   Set badblocks list
    -z undo_file         Create an undo file
```

#### fsck.ext4

```
Usage: fsck.ext4 [-panyrcdfktvDFV] [-b superblock] [-B blocksize]
                [-l|-L bad_blocks_file] [-C fd] [-j external_journal]
                [-E extended-options] [-z undo_file] device

Emergency help:
    -p                   Automatic repair (no questions)
    -n                   Make no changes to the filesystem
    -y                   Assume "yes" to all questions
    -c                   Check for bad blocks and add them to the badblock list
    -f                   Force checking even if filesystem is marked clean
    -v                   Be verbose
    -b superblock        Use alternative superblock
    -B blocksize         Force blocksize when looking for superblock
    -j external_journal  Set location of the external journal
    -l bad_blocks_file   Add to badblocks list
    -L bad_blocks_file   Set badblocks list
    -z undo_file         Create an undo file
```

#### fsync

```
Usage: fsync [-d] FILE...

Write files' buffered blocks to disk

    -d      Avoid syncing metadata
```

#### fw_printenv

```
fw_printenv/fw_setenv, a command line interface to U-Boot environment

usage:  fw_printenv [-a key] [-n] [variable name]
        fw_setenv [-a key] [variable name] [variable value]
        fw_setenv -s [ file ]
        fw_setenv -s - < [ file ]

The file passed as argument contains only pairs name / value
Example:
# Any line starting with # is treated as comment

        netdev         eth0
        kernel_addr    400000
        var1
        var2          The quick brown fox jumps over the lazy dog

A variable without value will be dropped. It is possible
to put any number of spaces between the fields, but any
space inside the value is treated as part of the value itself.
```

#### fw_setenv

```
fw_printenv/fw_setenv, a command line interface to U-Boot environment

usage:  fw_printenv [-a key] [-n] [variable name]
        fw_setenv [-a key] [variable name] [variable value]
        fw_setenv -s [ file ]
        fw_setenv -s - < [ file ]

The file passed as argument contains only pairs name / value
Example:
# Any line starting with # is treated as comment

              netdev         eth0
              kernel_addr    400000
              var1
              var2          The quick brown fox jumps over the lazy dog

A variable without value will be dropped. It is possible
to put any number of spaces between the fields, but any
space inside the value is treated as part of the value itself.
```

#### fwtool

```
Usage: fwtool <options> <firmware>

Options:
    -S <file>:            Append signature file to firmware image
    -I <file>:            Append metadata file to firmware image
    -s <file>:            Extract signature file from firmware image
    -i <file>:            Extract metadata file from firmware image
    -t:                   Remove extracted chunks from firmare image (using -s, -i)
    -q:                   Quiet (suppress error messages)
```

#### fwupdate
#### fwupdate.real
#### getrandom
#### getty

```
BusyBox v1.25.1 () multi-call binary.

Usage: getty [OPTIONS] BAUD_RATE[,BAUD_RATE]... TTY [TERMTYPE]

Open TTY, prompt for login name, then invoke /bin/login

    -h              Enable hardware RTS/CTS flow control
    -L              Set CLOCAL (ignore Carrier Detect state)
    -m              Get baud rate from modem's CONNECT status message
    -n              Don't prompt for login name
    -w              Wait for CR or LF before sending /etc/issue
    -i              Don't display /etc/issue
    -f ISSUE_FILE   Display ISSUE_FILE instead of /etc/issue
    -l LOGIN        Invoke LOGIN instead of /bin/login
    -t SEC          Terminate after SEC if no login name is read
    -I INITSTR      Send INITSTR before anything else
    -H HOST         Log HOST into the utmp file as the hostname

BAUD_RATE of 0 leaves it unchanged
```


#### grep

```
Usage: grep [-HhnlLoqvsriwFE] [-m N] [-A/B/C N] PATTERN/-e PATTERN.../-f FILE [FILE]...

Search for PATTERN in FILEs (or stdin)

    -H      Add 'filename:' prefix
    -h      Do not add 'filename:' prefix
    -n      Add 'line_no:' prefix
    -l      Show only names of files that match
    -L      Show only names of files that don't match
    -c      Show only count of matching lines
    -o      Show only the matching part of line
    -q      Quiet. Return 0 if PATTERN is found, 1 otherwise
    -v      Select non-matching lines
    -s      Suppress open and read errors
    -r      Recurse
    -i      Ignore case
    -w      Match whole words only
    -x      Match whole lines only
    -F      PATTERN is a literal (not regexp)
    -E      PATTERN is an extended regexp
    -m N    Match up to N times per file
    -A N    Print N lines of trailing context
    -B N    Print N lines of leading context
    -C N    Same as '-A N -B N'
    -e PTRN Pattern to match
    -f FILE Read pattern from file
```

#### guest_portal_funcs.sh
#### gunzip

```
Usage: gunzip [-cft] [FILE]...

Decompress FILEs (or stdin)

    -c      Write to stdout
    -f      Force
    -t      Test file integrity
```

#### gzip

```
Usage: gzip [-cfd] [FILE]...

Compress FILEs (or stdin)

    -d      Decompress
    -c      Write to stdout
    -f      Force
```

#### halt

```
Usage: halt [-d DELAY] [-n] [-f]

Halt the system

    -d SEC  Delay interval
    -n      Do not sync
    -f      Force (don't go through init)
```

#### hapd
#### head

```
Usage: head [OPTIONS] [FILE]...

Print first 10 lines of each FILE (or stdin) to stdout.
With more than one FILE, precede each with a filename header.

    -n N[kbm]       Print first N lines
    -n -N[kbm]      Print all except N last lines
    -c [-]N[kbm]    Print first N bytes
    -q              Never print headers
    -v              Always print headers

N may be suffixed by k (x1024), b (x512), or m (x1024^2).
```

#### hexdump

```
Usage: hexdump [-bcCdefnosvx] [FILE]...

Display FILEs (or stdin) in a user specified format

    -b              One-byte octal display
    -c              One-byte character display
    -C              Canonical hex+ASCII, 16 bytes per line
    -d              Two-byte decimal display
    -e FORMAT_STRING
    -f FORMAT_FILE
    -n LENGTH       Interpret only LENGTH bytes of input
    -o              Two-byte octal display
    -s OFFSET       Skip OFFSET bytes
    -v              Display all input data
    -x              Two-byte hexadecimal display
```

#### hostapd

```
hostapd v2.10-devel
User space daemon for IEEE 802.11 AP management,
IEEE 802.1X/WPA/WPA2/EAP/RADIUS Authenticator
Copyright (c) 2002-2019, Jouni Malinen <j@w1.fi> and contributors

usage: hostapd [-hdBKtv] [-P <PID file>] [-e <entropy file>] \
        [-g <global ctrl_iface>] [-G <group>]\
        [-i <comma-separated list of interface names>]\
        [-l <seconds>]\
        <configuration file(s)>

options:
    -h   show this usage
    -d   show more debug messages (-dd for even more)
    -B   run daemon in the background
    -e   entropy file
    -g   global control interface path
    -G   group for control interfaces
    -P   PID file
    -K   include key data in debug messages
    -f   log output to debug file instead of stdout
    -i   list of interface names to use
    -s   log output to syslog instead of stdout
    -S   start all the interfaces synchronously
    -t   include timestamps in some debug messages
    -v   show hostapd version
    -l   optional startup delay in seconds
```

#### hostapd_cli

```
hostapd_cli v2.10-devel
Copyright (c) 2004-2019, Jouni Malinen <j@w1.fi> and contributors

usage: hostapd_cli [-p<path>] [-i<ifname>] [-hvBr] [-a<path>] \
                   [-P<pid file>] [-G<ping interval>] [command..]

Options:
    -h           help (show this usage text)
    -v           shown version information
    -p<path>     path to find control sockets (default: /var/run/hostapd)
    -s<dir_path> dir path to open client sockets (default: /var/run/hostapd)
    -a<file>     run in daemon mode executing the action file based on events
                    from hostapd
    -r           try to reconnect when client socket is disconnected.
                    This is useful only when used with -a.
    -B           run a daemon in the background
    -i<ifname>   Interface to listen on (default: first interface found in the
                    socket path)

commands:
    ping = pings hostapd
    mib = get MIB variables (dot1x, dot11, radius)
    relog = reload/truncate debug log output file
    close_log = disable debug log output file
    status = show interface status info
    sta <addr> = get MIB variables for one station
    all_sta = get MIB variables for all stations
    list_sta = list all stations
    new_sta <addr> = add a new station
    deauthenticate <addr> = deauthenticate a station
    reconfig-remove = reconfig remove interface
    disassociate <addr> = disassociate a station
    sa_query <addr> = send SA Query to a station
    wps_pin <uuid> <pin> [timeout] [addr] = add WPS Enrollee PIN
    wps_check_pin <PIN> = verify PIN checksum
    wps_pbc = indicate button pushed to initiate PBC
    wps_cancel = cancel the pending WPS operation
    wps_ap_pin <cmd> [params..] = enable/disable AP PIN
    wps_config <SSID> <auth> <encr> <key> = configure AP
    wps_get_status = show current WPS status
    disassoc_imminent = send Disassociation Imminent notification
    ess_disassoc = send ESS Dissassociation Imminent notification
    bss_tm_req = send BSS Transition Management Request
    get_config = show current configuration
    help = show this usage help
    interface [ifname] = show interfaces/select interface
    fst <params...> = send FST-MANAGER control interface command
    raw <params..> = send unprocessed command
    level <debug level> = change debug level
    license = show full hostapd_cli license
    quit = exit hostapd_cli
    set <name> <value> = set runtime variables
    get <name> = get runtime info
    set_qos_map_set <arg,arg,...> = set QoS Map set element
    send_qos_map_conf <addr> = send QoS Map Configure frame
    get_pmk <macaddr> = get STA PMK
    r0kh <R0KH> = Adds R0KH
    r1kh <R1KH> = Adds R1KH
    get_ptk <macaddr> = get STA PTK
    chan_switch <cs_count> <freq> [sec_channel_offset=] [center_freq1=]
    [center_freq2=] [bandwidth=] [blocktx] [ht|vht]
    = initiate channel switch announcement
    hs20_wnm_notif <addr> <url>
    = send WNM-Notification Subscription Remediation Request
    hs20_deauth_req <addr> <code (0/1)> <Re-auth-Delay(sec)> [url]
    = send WNM-Notification imminent deauthentication indication
    vendor <vendor id> <sub command id> [<hex formatted data>]
    = send vendor driver command
    enable = enable hostapd on current interface
    enable-reconfig = enable-reconfig hostapd on current interface
    reload = reload configuration for current interface
    disable = disable hostapd on current interface
    update_beacon = update Beacon frame contents
    
    erp_flush = drop all ERP keys
    log_level [level] = show/change log verbosity level
    pmksa  = show PMKSA cache entries
    pmksa_flush  = flush PMKSA cache
    set_neighbor <addr> <ssid=> <nr=> [lci=] [civic=] [stat]
    = add AP to neighbor database
    show_neighbor   = show neighbor database entries
    remove_neighbor <addr> [ssid=<hex>] = remove AP from neighbor database
    req_lci <addr> = send LCI request to a station
    req_range  = send FTM range request
    driver_flags  = show supported driver flags
    dpp_qr_code report a scanned DPP URI from a QR Code
    dpp_bootstrap_gen type=<qrcode> [chan=..] [mac=..] [info=..] [curve=..] [key=..] = generate DPP bootstrap information
    dpp_bootstrap_remove *|<id> = remove DPP bootstrap information
    dpp_bootstrap_get_uri <id> = get DPP bootstrap URI
    dpp_bootstrap_info <id> = show DPP bootstrap information
    dpp_bootstrap_set <id> [conf=..] [ssid=<SSID>] [ssid_charset=#] [psk=<PSK>] [pass=<passphrase>] [configurator=<id>] [conn_status=#] [akm_use_selector=<0|1>] [group_id=..] [expiry=#] [csrattrs=..] = set DPP configurator parameters
    dpp_auth_init peer=<id> [own=<id>] = initiate DPP bootstrapping
    dpp_listen <freq in MHz> = start DPP listen
    dpp_stop_listen = stop DPP listen
    dpp_configurator_add [curve=..] [key=..] = add DPP configurator
    dpp_configurator_remove *|<id> = remove DPP configurator
    dpp_configurator_get_key <id> = Get DPP configurator's private key
    dpp_configurator_sign conf=<role> configurator=<id> = generate self DPP configuration
    dpp_map_get_jwk_csign [curve=..][conf_obj=..]
    dpp_map_bss_conf_resp [curve=..][conf_obj=..]
    dpp_pkex_add add PKEX code
    dpp_pkex_remove *|<id> = remove DPP pkex information
    dpp_controller_start [tcp_port=<port>] [role=..] = start DPP controller
    dpp_controller_stop = stop DPP controller
    dpp_chirp own=<BI ID> iter=<count> = start DPP chirp
    dpp_stop_chirp = stop DPP chirp
    dpp_map_peer_disc_start = start MAP peer disc
    dpp_configurator_get_kid <id> = Get DPP configurator's csign hash
    dpp_csign_get_kid = Get DPP csign hash for configured csign value
    dpp_push_button = press DPP push button
    accept_acl =Add/Delete/Show/Clear accept MAC ACL
    deny_acl =Add/Delete/Show/Clear deny MAC ACL
    poll_sta <addr> = poll a STA to check connectivity with a QoS null frame
    req_beacon <addr> [req_mode=] <measurement request hexdump>  = send a Beacon report request to a station
    reload_wpa_psk = reload wpa_psk_file only
    reload_accept_mac = reload accept_mac_file only
    group_rekey = immediately rekey group key
```

#### hotplug-call
#### htb

```
Usage: /bin/htb start|stop [<args>]
```

#### hwcheck

```
Usage: hwcheck [options]

Options:
    -d Debug (logging to stdout)
    -v Increase verbosity
    -h Show this help text
```

#### hwclock

```
Usage: hwclock [-r] [-s] [-w] [-t] [-l] [-u] [-f FILE]

Query and set hardware clock (RTC)

    -r      Show hardware clock time
    -s      Set system time from hardware clock
    -w      Set hardware clock from system time
    -t      Set in-kernel timezone, correct system time
            if hardware clock is in local time
    -u      Assume hardware clock is kept in UTC
    -l      Assume hardware clock is kept in local time
    -f FILE Use specified device (e.g. /dev/rtc2)
```

#### i2cdetect

```
Usage: i2cdetect [-F I2CBUS] [-l] [-y] [-a] [-q|-r] I2CBUS [FIRST LAST]

Detect I2C chips.

    I2CBUS  i2c bus number
    FIRST and LAST limit the probing range
    
    -l      output list of installed busses
    -y      disable interactive mode
    -a      force scanning of non-regular addresses
    -q      use smbus quick write commands for probing (default)
    -r      use smbus read byte commands for probing
    -F      display list of functionalities
```

#### i2cdump

```
Usage: i2cdump [-f] [-r FIRST-LAST] [-y] BUS ADDR [MODE]

Examine I2C registers

    I2CBUS  i2c bus number
    ADDRESS 0x03 - 0x77

MODE is:
    b       byte (default)
    w       word
    W       word on even register addresses
    i       I2C block
    s       SMBus block
    c       consecutive byte
    Append p for SMBus PEC
    
    -f      force access
    -y      disable interactive mode
    -r      limit the number of registers being accessed
```

#### i2cget

```
Usage: i2cget [-f] [-y] BUS CHIP-ADDRESS [DATA-ADDRESS [MODE]]

Read from I2C/SMBus chip registers

    I2CBUS  i2c bus number
    ADDRESS 0x03 - 0x77

MODE is:
    b       read byte data (default)
    w       read word data
    c       write byte/read byte
    Append p for SMBus PEC
    
    -f      force access
    -y      disable interactive mode
```

#### i2cset

```
Usage: i2cset [-f] [-y] [-m MASK] BUS CHIP-ADDR DATA-ADDR [VALUE] ... [MODE]

Set I2C registers

    I2CBUS  i2c bus number
    ADDRESS 0x03 - 0x77

MODE is:
    c       byte, no value
    b       byte data (default)
    w       word data
    i       I2C block data
    s       SMBus block data
    Append p for SMBus PEC
    
    -f      force access
    -y      disable interactive mode
    -r      read back and compare the result
    -m MASK mask specifying which bits to write
```

#### icm

```
icm - usage
-----------------------------------------------------------
Options:
    e : run as daemon
    f : use nominal noisefloor
    h : display help
    n : enable usage of noise floor in channel selection
    r : policy regarding usage of representative Tx power in
        channel selection (if available from driver)
        0: do not use
        1: use representative Tx power, optimize for throughput
        2: use representative Tx power, optimize for range
    b : enable(1)/disable(0) preference for U-NII-3 band for
        802.11ax (if 802.11ax support is available on the system)
    s : socket type <0(tcp)/1(udp)>
    t : run tests
    v : server mode
    c : <ioctl | cfg>
    g : enable usage of channel grade info in channel selection
    i : dump selection debug information (file: /tmp/icmseldebug.csv)
    q : debug level <1(Minor)/2(Default)/3(Major)/4(Critical))>
    u : debug module bitmap, formed by ORing following
        bit positions, each corresponding to a module:
        <0x01(Main),      0x02(Scan), 0x04(Selector),
         0x08(Utilities), 0x10(Test), 0x20(Socket),
         0x40(Spectral),  0x80(Command)>
-----------------------------------------------------------
```

#### id

```
Usage: id [OPTIONS] [USER]

Print information about USER or the current user

    -u      User ID
    -g      Group ID
    -G      Supplementary group IDs
    -n      Print names instead of numbers
    -r      Print real ID instead of effective ID
```

#### iface-mgr
#### ifconfig

```
Usage: ifconfig [-a] interface [address]

Configure a network interface

    [add ADDRESS[/PREFIXLEN]]
    [del ADDRESS[/PREFIXLEN]]
    [[-]broadcast [ADDRESS]] [[-]pointopoint [ADDRESS]]
    [netmask ADDRESS] [dstaddr ADDRESS]
    [hw ether ADDRESS] [metric NN] [mtu NN]
    [[-]trailers] [[-]arp] [[-]allmulti]
    [multicast] [[-]promisc] [txqueuelen NN] [[-]dynamic]
    [up|down] ...
```

#### init
#### insmod

```
Usage:
    insmod filename [args]
```

#### iostat

```
Usage: iostat [-c] [-d] [-t] [-z] [-k|-m] [ALL|BLOCKDEV...] [INTERVAL [COUNT]]

Report CPU and I/O statistics

    -c      Show CPU utilization
    -d      Show device utilization
    -t      Print current time
    -z      Omit devices with no activity
    -k      Use kb/s
    -m      Use Mb/s
```

#### ip

```
Usage: ip [ OPTIONS ] OBJECT { COMMAND | help }
       ip [ -force ] -batch filename

where  OBJECT := { link | address | addrlabel | route | rule | neighbor | ntable |
                   tunnel | tuntap | maddress | mroute | mrule | monitor | xfrm |
                   netns | l2tp | fou | tcp_metrics | token | netconf }
       OPTIONS := { -V[ersion] | -s[tatistics] | -d[etails] | -r[esolve] |
                    -h[uman-readable] | -iec |
                    -f[amily] { inet | inet6 | ipx | dnet | mpls | bridge | link } |
                    -4 | -6 | -I | -D | -B | -0 |
                    -l[oops] { maximum-addr-flush-attempts } | -br[ief] |
                    -o[neline] | -t[imestamp] | -ts[hort] | -b[atch] [filename] |
                    -rc[vbuf] [size] | -n[etns] name | -a[ll] | -c[olor]}
```

#### ip6tables

```
ip6tables v1.4.21

Usage: ip6tables -[ACD] chain rule-specification [options]
       ip6tables -I chain [rulenum] rule-specification [options]
       ip6tables -R chain rulenum rule-specification [options]
       ip6tables -D chain rulenum [options]
       ip6tables -[LS] [chain [rulenum]] [options]
       ip6tables -[FZ] [chain] [options]
       ip6tables -[NX] chain
       ip6tables -E old-chain-name new-chain-name
       ip6tables -P chain target [options]
       ip6tables -h (print this help information)

Commands:
Either long or short options are allowed.
    --append  -A chain            Append to chain
    --check   -C chain            Check for the existence of a rule
    --delete  -D chain            Delete matching rule from chain
    --delete  -D chain rulenum
                            Delete rule rulenum (1 = first) from chain
    --insert  -I chain [rulenum]
                            Insert in chain as rulenum (default 1=first)
    --replace -R chain rulenum
                            Replace rule rulenum (1 = first) in chain
    --list    -L [chain [rulenum]]
                            List the rules in a chain or all chains
    --list-rules -S [chain [rulenum]]
                            Print the rules in a chain or all chains
    --flush   -F [chain]          Delete all rules in  chain or all chains
    --zero    -Z [chain [rulenum]]
                            Zero counters in chain or all chains
    --new     -N chain            Create a new user-defined chain
    --delete-chain
            -X [chain]          Delete a user-defined chain
    --policy  -P chain target
                            Change policy on chain to target
    --rename-chain
            -E old-chain new-chain
                            Change chain name, (moving any references)

Options:
    --ipv4      -4              Error (line is ignored by ip6tables-restore)
    --ipv6      -6              Nothing (line is ignored by iptables-restore)
[!] --protocol  -p proto        protocol: by number or name, eg. `tcp'
[!] --source    -s address[/mask][,...]
                                source specification
[!] --destination -d address[/mask][,...]
                                destination specification
[!] --in-interface -i input name[+]
                                network interface name ([+] for wildcard)
  --jump        -j target
                                target for rule (may load target extension)
  --goto        -g chain
                                jump to chain with no return
  --match       -m match
                                extended match (may load extension)
  --numeric     -n              numeric output of addresses and ports
[!] --out-interface -o output name[+]
                                network interface name ([+] for wildcard)
  --table       -t table        table to manipulate (default: `filter')
  --verbose     -v              verbose mode
  --wait        -w              wait for the xtables lock
  --line-numbers                print line numbers when listing
  --exact       -x              expand numbers (display exact values)
  --modprobe=<command>          try to insert modules using this command
  --set-counters PKTS BYTES     set the counter during insert/append
[!] --version   -V              print package version.
```

#### ip6tables-restore

```
Usage: ip6tables-restore [-b] [-c] [-v] [-t] [-h]
        [ --binary ]
        [ --counters ]
        [ --verbose ]
        [ --test ]
        [ --help ]
        [ --noflush ]
        [ --modprobe=<command>]
```

#### ip6tables-save
#### ipcalc.sh
#### iperf

```
Usage: iperf [-s|-c host] [options]
       iperf [-h|--help] [-v|--version]

Client/Server:
  -b, --bandwidth #[kmgKMG | pps]  bandwidth to read/send at in bits/sec or packets/sec
  -e, --enhanced    use enhanced reporting giving more tcp/udp and traffic information
  -f, --format    [kmgKMG]   format to report: Kbits, Mbits, KBytes, MBytes
      --hide-ips           hide ip addresses and host names within outputs
  -i, --interval  #        seconds between periodic bandwidth reports
  -l, --len       #[kmKM]    length of buffer in bytes to read or write (Defaults: TCP=128K, v4 UDP=1470, v6 UDP=1450)
  -m, --print_mss          print TCP maximum segment size
  -o, --output    <filename> output the report or error message to this specified file
  -p, --port      #        client/server port to listen/send on and to connect
      --permit-key         permit key to be used to verify client and server (TCP only)
      --sum-only           output sum only reports
  -u, --udp                use UDP rather than TCP
      --utc                use coordinated universal time (UTC) with time output
  -w, --window    #[KM]    TCP window size (socket buffer size)
  -z, --realtime           request realtime scheduler
  -B, --bind <host>[:<port>][%<dev>] bind to <host>, ip addr (including multicast address) and optional port and device
  -C, --compatibility      for use with older versions does not sent extra msgs
      --NUM_REPORT_STRUCTS increase the shared memory between the traffic threads and the reporter thread (default is 10,000 entries)
  -M, --mss       #        set TCP maximum segment size using TCP_MAXSEG
  -N, --nodelay            set TCP no delay, disabling Nagle's Algorithm
  -S, --tos       #        set the socket's IP_TOS (byte) field
  -Z, --tcp-congestion <algo>  set TCP congestion control algorithm (Linux only)

Server specific:
  -p, --port      #[-#]    server port(s) to listen on/connect to
  -s, --server             run in server mode
  -1, --singleclient       run one server at a time
      --histograms         enable latency histograms
      --jitter-histograms  enable jitter histograms
      --permit-key-timeout set the timeout for a permit key in seconds
      --tcp-rx-window-clamp set the TCP receive window clamp size in bytes
      --tap-dev   #[<dev>] use TAP device to receive at L2 layer
  -t, --time      #        time in seconds to listen for new connections as well as to receive traffic (default not set)
  -B, --bind <ip>[%<dev>]  bind to multicast address and optional device
  -U, --single_udp         run in single threaded UDP mode
      --sum-dstip          sum traffic threads based upon destination ip address (default is src ip)
  -D, --daemon             run the server as a daemon
  -V, --ipv6_domain        Enable IPv6 reception by setting the domain and socket to AF_INET6 (Can receive on both IPv4 and IPv6)

Client specific:
      --bounceback         request a bounceback test (use -l for size, defaults to 100 bytes)
      --bounceback-hold    request the server to insert a delay of n milliseconds between its read and write
      --bounceback-period  request the client schedule a send every n milliseconds
      --bounceback-no-quickack request the server not set the TCP_QUICKACK socket option (disabling TCP ACK delays) during a bounceback test
  -c, --client    <host>   run in client mode, connecting to <host>
      --connect-only       run a connect only test
      --connect-retries #  number of times to retry tcp connect
  -d, --dualtest           Do a bidirectional test simultaneously (multiple sockets)
      --fq-rate #[kmgKMG]  bandwidth to socket pacing
      --full-duplex        run full duplex test using same socket
      --ipg                set the the interpacket gap (milliseconds) for packets within an isochronous frame
      --isochronous <frames-per-second>:<mean>,<stddev> send traffic in bursts (frames - emulate video traffic)
      --incr-dstip         Increment the destination ip with parallel (-P) traffic threads
      --incr-dstport       Increment the destination port with parallel (-P) traffic threads
      --incr-srcip         Increment the source ip with parallel (-P) traffic threads
      --incr-srcport       Increment the source port with parallel (-P) traffic threads
      --local-only         Set don't route on socket
      --near-congestion=[w] Use a weighted write delay per the sampled TCP RTT (experimental)
      --no-connect-sync    No sychronization after connect when -P or parallel traffic threads
      --no-udp-fin         No final server to client stats at end of UDP test
  -n, --num       #[kmgKMG]    number of bytes to transmit (instead of -t)
  -r, --tradeoff           Do a fullduplexectional test individually
      --tcp-quickack       set the socket's TCP_QUICKACK option (off by default)
      --tcp-write-prefetch set the socket's TCP_NOTSENT_LOWAT value in bytes and use event based writes
      --tcp-write-times    measure the socket write times at the application level
  -t, --time      #        time in seconds to transmit for (default 10 secs)
      --trip-times         enable end to end measurements (requires client and server clock sync)
      --txdelay-time       time in seconds to hold back after connect and before first write
      --txstart-time       unix epoch time to schedule first write and start traffic
  -B, --bind [<ip> | <ip:port>] bind ip (and optional port) from which to source traffic
  -F, --fileinput <name>   input the data to be transmitted from a file
  -H, --ssm-host <ip>      set the SSM source, use with -B for (S,G)
  -I, --stdin              input the data to be transmitted from stdin
  -L, --listenport #       port to receive fullduplexectional tests back on
  -P, --parallel  #        number of parallel client threads to run
  -R, --reverse            reverse the test (client receives, server sends)
  -S, --tos                IP DSCP or tos settings
  -T, --ttl       #        time-to-live, for multicast (default 1)
      --working-load request a concurrent TCP stream
  -V, --ipv6_domain        Set the domain to IPv6 (send packets over IPv6)
  -X, --peer-detect        perform server version detection and version exchange

Miscellaneous:
  -x, --reportexclude [CDMSV]   exclude C(connection) D(data) M(multicast) S(settings) V(server) reports
  -y, --reportstyle C      report as a Comma-Separated Values
  -h, --help               print this message and quit
  -v, --version            print version information and quit

[kmgKMG] Indicates options that support a k,m,g,K,M or G suffix
Lowercase format characters are 10^3 based and uppercase are 2^n based
(e.g. 1k = 1000, 1K = 1024, 1m = 1,000,000 and 1M = 1,048,576)

Accepted tos values are: af11, af12, af13, af21, af22, af23, af31, af32, af33, af41, af42, af43,
cs0, cs1, cs2, cs3, cs4, cs5, cs6, cs7, ef, le, nqb, nqb2, ac_be, ac_bk, ac_vi, ac_vo, lowdelay, throughput,
reliability, or a numeric value.

The TCP window size option can be set by the environment variable
TCP_WINDOW_SIZE. Most other options can be set by an environment variable
IPERF_<long option name>, such as IPERF_BANDWIDTH.

Source at <http://sourceforge.net/projects/iperf2/>
Report bugs to <iperf-users@lists.sourceforge.net>
```

#### iperf3

```
Usage: iperf3 [-s|-c host] [options]
       iperf3 [-h|--help] [-v|--version]

Server or Client:
  -p, --port      #         server port to listen on/connect to
  -f, --format   [kmgtKMGT] format to report: Kbits, Mbits, Gbits, Tbits
  -i, --interval  #         seconds between periodic throughput reports
  -I, --pidfile file        write PID file
  -F, --file name           xmit/recv the specified file
  -A, --affinity n/n,m      set CPU affinity
  -B, --bind      <host>    bind to the interface associated with the address <host>
  --bind-dev      <dev>     bind to the network interface with SO_BINDTODEVICE
  -V, --verbose             more detailed output
  -J, --json                output in JSON format
  --logfile f               send output to a log file
  --forceflush              force flushing output at every interval
  --timestamps<=format>     emit a timestamp at the start of each output line
                            (optional "=" and format string as per strftime(3))
  --rcv-timeout #           idle timeout for receiving data
                            (default 120000 ms)
  -d, --debug               emit debugging output
  -v, --version             show version information and quit
  -h, --help                show this message and quit
Server specific:
  -s, --server              run in server mode
  -D, --daemon              run the server as a daemon
  -1, --one-off             handle one client connection then exit
  --server-bitrate-limit #[KMG][/#]   server's total bit rate limit (default 0 = no limit)
                            (optional slash and number of secs interval for averaging
                            total data rate.  Default is 5 seconds)
  --idle-timeout #          restart idle server after # seconds in case it
                            got stuck (default - no timeout)
Client specific:
  -c, --client    <host>    run in client mode, connecting to <host>
  -u, --udp                 use UDP rather than TCP
  --connect-timeout #       timeout for control connection setup (ms)
  -b, --bitrate #[KMG][/#]  target bitrate in bits/sec (0 for unlimited)
                            (default 1 Mbit/sec for UDP, unlimited for TCP)
                            (optional slash and packet count for burst mode)
  --pacing-timer #[KMG]     set the timing for pacing, in microseconds (default 1000)
  --fq-rate #[KMG]          enable fair-queuing based socket pacing in
                            bits/sec (Linux only)
  -t, --time      #         time in seconds to transmit for (default 10 secs)
  -n, --bytes     #[KMG]    number of bytes to transmit (instead of -t)
  -k, --blockcount #[KMG]   number of blocks (packets) to transmit (instead of -t or -n)
  -l, --length    #[KMG]    length of buffer to read or write
                            (default 128 KB for TCP, dynamic or 1460 for UDP)
  --cport         <port>    bind to a specific client port (TCP and UDP, default: ephemeral port)
  -P, --parallel  #         number of parallel client streams to run
  -R, --reverse             run in reverse mode (server sends, client receives)
  --bidir                   run in bidirectional mode.
                            Client and server send and receive data.
  -w, --window    #[KMG]    set window size / socket buffer size
  -C, --congestion <algo>   set TCP congestion control algorithm (Linux and FreeBSD only)
  -M, --set-mss   #         set TCP/SCTP maximum segment size (MTU - 40 bytes)
  -N, --no-delay            set TCP/SCTP no delay, disabling Nagle's Algorithm
  -4, --version4            only use IPv4
  -6, --version6            only use IPv6
  -S, --tos N               set the IP type of service, 0-255.
                            The usual prefixes for octal and hex can be used,
                            i.e. 52, 064 and 0x34 all specify the same value.
  --dscp N or --dscp val    set the IP dscp value, either 0-63 or symbolic.
                            Numeric values can be specified in decimal,
                            octal and hex (see --tos above).
  -L, --flowlabel N         set the IPv6 flow label (only supported on Linux)
  -Z, --zerocopy            use a 'zero copy' method of sending data
  -O, --omit N              omit the first n seconds
  -T, --title str           prefix every output line with this string
  --extra-data str          data string to include in client and server JSON
  --get-server-output       get results from server
  --udp-counters-64bit      use 64-bit counters in UDP test packets
  --repeating-payload       use repeating pattern in payload, instead of
                            randomized payload (like in iperf2)
  --dont-fragment           set IPv4 Don't Fragment flag

[KMG] indicates options that support a K/M/G suffix for kilo-, mega-, or giga-

iperf3 homepage at: https://software.es.net/iperf/
Report bugs to:     https://github.com/esnet/iperf
```

#### ipset

```
ipset v7.6

Usage: ipset [options] COMMAND

Commands:
create SETNAME TYPENAME [type-specific-options]
        Create a new set
add SETNAME ENTRY
        Add entry to the named set
del SETNAME ENTRY
        Delete entry from the named set
test SETNAME ENTRY
        Test entry in the named set
destroy [SETNAME]
        Destroy a named set or all sets
list [SETNAME]
        List the entries of a named set or all sets
save [SETNAME]
        Save the named set or all sets to stdout
restore
        Restore a saved state
flush [SETNAME]
        Flush a named set or all sets
rename FROM-SETNAME TO-SETNAME
        Rename two sets
swap FROM-SETNAME TO-SETNAME
        Swap the contect of two existing sets
help [TYPENAME]
        Print help, and settype specific help
version
        Print version information
quit
        Quit interactive mode

Options:
-o plain|save|xml
       Specify output mode for listing sets.
       Default value for "list" command is mode "plain"
       and for "save" command is mode "save".
-s
        Print elements sorted (if supported by the set type).
-q
        Suppress any notice or warning message.
-r
        Try to resolve IP addresses in the output (slow!)
-!
        Ignore errors when creating or adding sets or
        elements that do exist or when deleting elements
        that don't exist.
-n
        When listing, just list setnames from the kernel.

-t
        When listing, list setnames and set headers
        from kernel only.
-f
        Read from the given file instead of standard
        input (restore) or write to given file instead
        of standard output (list/save).

Supported set types:
    list:set            3       skbinfo support
    list:set            2       comment support
    list:set            1       counters support
    list:set            0       Initial revision
    hash:mac            0       Initial revision
    hash:ip,mac         0       Initial revision
    hash:net,iface      7       skbinfo and wildcard support
    hash:net,iface      6       skbinfo support
    hash:net,iface      5       forceadd support
    hash:net,iface      4       comment support
    hash:net,iface      3       counters support
    hash:net,iface      2       /0 network support
    hash:net,iface      1       nomatch flag support
    hash:net,iface      0       Initial revision
    hash:net,port       7       skbinfo support
    hash:net,port       6       forceadd support
    hash:net,port       5       comment support
    hash:net,port       4       counters support
    hash:net,port       3       nomatch flag support
    hash:net,port       2       Add/del range support
    hash:net,port       1       SCTP and UDPLITE support
    hash:net,port,net   2       skbinfo support
    hash:net,port,net   1       forceadd support
    hash:net,port,net   0       initial revision
    hash:net,net        2       skbinfo support
    hash:net,net        1       forceadd support
    hash:net,net        0       initial revision
    hash:net            6       skbinfo support
    hash:net            5       forceadd support
    hash:net            4       comment support
    hash:net            3       counters support
    hash:net            2       nomatch flag support
    hash:net            1       Add/del range support
    hash:net            0       Initial revision
    hash:ip,port,net    7       skbinfo support
    hash:ip,port,net    6       forceadd support
    hash:ip,port,net    5       comment support
    hash:ip,port,net    4       counters support
    hash:ip,port,net    3       nomatch flag support
    hash:ip,port,net    2       Add/del range support
    hash:ip,port,net    1       SCTP and UDPLITE support
    hash:ip,port,ip     5       skbinfo support
    hash:ip,port,ip     4       forceadd support
    hash:ip,port,ip     3       comment support
    hash:ip,port,ip     2       counters support
    hash:ip,port,ip     1       SCTP and UDPLITE support
    hash:ip,mark        2       skbinfo support
    hash:ip,mark        1       forceadd support
    hash:ip,mark        0       initial revision
    hash:ip,port        5       skbinfo support
    hash:ip,port        4       forceadd support
    hash:ip,port        3       comment support
    hash:ip,port        2       counters support
    hash:ip,port        1       SCTP and UDPLITE support
    hash:ip             4       skbinfo support
    hash:ip             3       forceadd support
    hash:ip             2       comment support
    hash:ip             1       counters support
    hash:ip             0       Initial revision
    bitmap:port         3       skbinfo support
    bitmap:port         2       comment support
    bitmap:port         1       counters support
    bitmap:port         0       Initial revision
    bitmap:ip,mac       3       skbinfo support
    bitmap:ip,mac       2       comment support
    bitmap:ip,mac       1       counters support
    bitmap:ip,mac       0       Initial revision
    bitmap:ip           3       skbinfo support
    bitmap:ip           2       comment support
    bitmap:ip           1       counters support
    bitmap:ip           0       Initial revision
```

#### iptables

```
iptables v1.4.21

Usage: iptables -[ACD] chain rule-specification [options]
       iptables -I chain [rulenum] rule-specification [options]
       iptables -R chain rulenum rule-specification [options]
       iptables -D chain rulenum [options]
       iptables -[LS] [chain [rulenum]] [options]
       iptables -[FZ] [chain] [options]
       iptables -[NX] chain
       iptables -E old-chain-name new-chain-name
       iptables -P chain target [options]
       iptables -h (print this help information)

Commands:
Either long or short options are allowed.
  --append  -A chain            Append to chain
  --check   -C chain            Check for the existence of a rule
  --delete  -D chain            Delete matching rule from chain
  --delete  -D chain rulenum
                                Delete rule rulenum (1 = first) from chain
  --insert  -I chain [rulenum]
                                Insert in chain as rulenum (default 1=first)
  --replace -R chain rulenum
                                Replace rule rulenum (1 = first) in chain
  --list    -L [chain [rulenum]]
                                List the rules in a chain or all chains
  --list-rules -S [chain [rulenum]]
                                Print the rules in a chain or all chains
  --flush   -F [chain]          Delete all rules in  chain or all chains
  --zero    -Z [chain [rulenum]]
                                Zero counters in chain or all chains
  --new     -N chain            Create a new user-defined chain
  --delete-chain
            -X [chain]          Delete a user-defined chain
  --policy  -P chain target
                                Change policy on chain to target
  --rename-chain
            -E old-chain new-chain
                                Change chain name, (moving any references)
Options:
    --ipv4      -4              Nothing (line is ignored by ip6tables-restore)
    --ipv6      -6              Error (line is ignored by iptables-restore)
[!] --protocol  -p proto        protocol: by number or name, eg. `tcp'
[!] --source    -s address[/mask][...]
                                source specification
[!] --destination -d address[/mask][...]
                                destination specification
[!] --in-interface -i input name[+]
                                network interface name ([+] for wildcard)
 --jump -j target
                                target for rule (may load target extension)
  --goto      -g chain
                              jump to chain with no return
  --match       -m match
                                extended match (may load extension)
  --numeric     -n              numeric output of addresses and ports
[!] --out-interface -o output name[+]
                                network interface name ([+] for wildcard)
  --table       -t table        table to manipulate (default: `filter')
  --verbose     -v              verbose mode
  --wait        -w              wait for the xtables lock
  --line-numbers                print line numbers when listing
  --exact       -x              expand numbers (display exact values)
[!] --fragment  -f              match second or further fragments only
  --modprobe=<command>          try to insert modules using this command
  --set-counters PKTS BYTES     set the counter during insert/append
[!] --version   -V              print package version.
```

#### iptables-restore

```
Usage: iptables-restore [-b] [-c] [-v] [-t] [-h]
        [ --binary ]
        [ --counters ]
        [ --verbose ]
        [ --test ]
        [ --help ]
        [ --noflush ]
        [ --table=<TABLE> ]
        [ --modprobe=<command>]
```

#### iptables-save
#### iw

```
Usage:  iw [options] command

Options:
    --debug         enable netlink debugging
    --version       show version (4.9)

Commands:
    help [command]
    event [-t|-r] [-f]
    features
    phy
    list
    phy <phyname> info
    phy <phyname> channels
    dev
    dev <devname> info
    dev <devname> del
    dev <devname> interface add <name> type <type> [mesh_id <meshid>] [4addr on|off] [flags <flag>*] [addr <mac-addr>]
    phy <phyname> interface add <name> type <type> [mesh_id <meshid>] [4addr on|off] [flags <flag>*] [addr <mac-addr>]
    dev <devname> ibss join <SSID> <freq in MHz> [NOHT|HT20|HT40+|HT40-|5MHz|10MHz|80MHz] [fixed-freq] [<fixed bssid>] [beacon-interval <TU>] [basic-rates <rate in Mbps,rate2,...>] [mcast-rate <rate in Mbps>] [key d:0:abcde]
    dev <devname> ibss leave
    dev <devname> station set <MAC address> plink_action <open|block>
    dev <devname> station set <MAC address> vlan <ifindex>
    dev <devname> station set <MAC address> mesh_power_mode <active|light|deep>
    dev <devname> station dump [-v]
    dev <devname> station del <MAC address> [subtype <subtype>] [reason-code <code>]
    dev <devname> station get <MAC address>
    dev <devname> survey dump
    dev <devname> ocb leave
    dev <devname> ocb join <freq in MHz> <5MHz|10MHz>
    dev <devname> mesh leave
    dev <devname> mesh join <mesh ID> [[freq <freq in MHz> <NOHT|HT20|HT40+|HT40-|80MHz>] [basic-rates <rate in Mbps,rate2,...>]], [mcast-rate <rate in Mbps>] [beacon-interval <time in TUs>] [dtim-period <value>] [vendor_sync on|off] [<param>=<value>]*
    dev <devname> mpath dump
    dev <devname> mpath set <destination MAC address> next_hop <next hop MAC address>
    dev <devname> mpath new <destination MAC address> next_hop <next hop MAC address>
    dev <devname> mpath del <MAC address>
    dev <devname> mpath get <MAC address>
    dev <devname> mpp dump
    dev <devname> mpp get <MAC address>
    dev <devname> scan [-u] [freq <freq>*] [ies <hex as 00:11:..>] [meshid <meshid>] [lowpri,flush,ap-force] [randomise[=<addr>/<mask>]] [ssid <ssid>*|passive]
    dev <devname> scan sched_stop
    dev <devname> scan sched_start [interval <in_msecs> | scan_plans [<interval_secs:iterations>*] <interval_secs>] [delay <in_secs>] [freqs <freq>+] [matches [ssid <ssid>]+]] [active [ssid <ssid>]+|passive] [randomise[=<addr>/<mask>]]
    dev <devname> scan abort
    dev <devname> scan trigger [freq <freq>*] [ies <hex as 00:11:..>] [meshid <meshid>] [lowpri,flush,ap-force] [randomise[=<addr>/<mask>]] [ssid <ssid>*|passive]
    dev <devname> scan dump [-u]
    phy <phyname> reg get
    reg get
    reg set <ISO/IEC 3166-1 alpha2>
    dev <devname> link
    dev <devname> offchannel <freq> <duration>
    dev <devname> cqm rssi <threshold|off> [<hysteresis>]
    dev <devname> vendor recvbin <oui> <subcmd> <filename|-|hex data>
    dev <devname> vendor recv <oui> <subcmd> <filename|-|hex data>
    dev <devname> vendor send <oui> <subcmd> <filename|-|hex data>
    phy <phyname> set antenna <bitmap> | all | <tx bitmap> <rx bitmap>
    dev <devname> set txpower <auto|fixed|limit> [<tx power in mBm>]
    phy <phyname> set txpower <auto|fixed|limit> [<tx power in mBm>]
    phy <phyname> set distance <auto|distance>
    phy <phyname> set coverage <coverage class>
    phy <phyname> set netns { <pid> | name <nsname> }
    phy <phyname> set retry [short <limit>] [long <limit>]
    phy <phyname> set rts <rts threshold|off>
    phy <phyname> set frag <fragmentation threshold|off>
    dev <devname> set channel <channel> [HT20|HT40+|HT40-]
    phy <phyname> set channel <channel> [HT20|HT40+|HT40-]
    dev <devname> set freq <freq> [HT20|HT40+|HT40-]
    dev <devname> set freq <control freq> [20|40|80|80+80|160] [<center freq 1>] [<center freq 2>]
    phy <phyname> set freq <freq> [HT20|HT40+|HT40-]
    phy <phyname> set name <new name>
    dev <devname> set mcast_rate <rate in Mbps>
    dev <devname> set peer <MAC address>
    dev <devname> set noack_map <map>
    dev <devname> set 4addr <on|off>
    dev <devname> set type <type>
    dev <devname> set meshid <meshid>
    dev <devname> set monitor <flag>*
    dev <devname> set mesh_param <param>=<value> [<param>=<value>]*
    dev <devname> set power_save <on|off>
    dev <devname> set bitrates [legacy-<2.4|5> <legacy rate in Mbps>*] [ht-mcs-<2.4|5> <MCS index>*] [vht-mcs-<2.4|5> <NSS:MCSx,MCSy... | NSS:MCSx-MCSy>*] [sgi-2.4|lgi-2.4] [sgi-5|lgi-5]
    dev <devname> get mesh_param [<param>]
    dev <devname> get power_save <param>

Commands that use the netdev ('dev') can also be given the
'wdev' instead to identify the device.

You can omit the 'phy' or 'dev' if the identification is unique,
e.g. "iw wlan0 info" or "iw phy0 info". (Don't when scripting.)

Do NOT screenscrape this tool, we don't consider its output stable.
```

#### iwconfig

(Currnet config output)

#### iwlist

```
Usage: iwlist [interface] scanning [essid NNN] [last]
              [interface] frequency
              [interface] channel
              [interface] bitrate
              [interface] rate
              [interface] encryption
              [interface] keys
              [interface] power
              [interface] txpower
```

#### iwpriv

```
Usage: iwpriv interface [private-command [private-arguments]]
```

#### jffs2mark
#### jffs2reset
#### jshn

```
Usage: jshn [-n] [-i] -r <message>|-w
```

#### jsonfilter

```
== Usage ==

  # jsonfilter [-i <file> | -s "json..."] {-t <pattern> | -e <pattern>}
  -q            Quiet, no errors are printed
  -h, --help    Print this help
  -i path       Specify a JSON file to parse
  -s "json"     Specify a JSON string to parse
  -l limit      Specify max number of results to show
  -F separator  Specify a field separator when using export
  -t <pattern>  Print the type of values matched by pattern
  -e <pattern>  Print the values matched by pattern
  -e VAR=<pat>  Serialize matched value for shell "eval"

== Patterns ==

  Patterns are JsonPath: http://goessner.net/articles/JsonPath/
  This tool implements $, @, [], * and the union operator ','
  plus the usual expressions and literals.
  It does not support the recursive child search operator '..' or
  the '?()' and '()' filter expressions as those would require a
  complete JavaScript engine to support them.

== Examples ==

  Display the first IPv4 address on lan:
  # ifstatus lan | jsonfilter -e '@["ipv4-address"][0].address'

  Extract the release string from the board information:
  # ubus call system board | jsonfilter -e '@.release.description'

  Find all interfaces which are up:
  # ubus call network.interface dump | \
        jsonfilter -e '@.interface[@.up=true].interface'

  Export br-lan traffic counters for shell eval:
  # devstatus br-lan | jsonfilter -e 'RX=@.statistics.rx_bytes' \
        -e 'TX=@.statistics.tx_bytes'
```

#### kill
#### killall
#### klogd

```
Usage: klogd [-c N] [-n]

Kernel logger

        -c N    Print to console messages more urgent than prio N (1-8)
        -n      Run in foreground
```

#### kmodloader
#### ldd

```
musl libc (armhf)
Version 1.1.19
Dynamic Program Loader

Usage: ldd [options] [--] pathname
```

#### led.sh
#### less

```
Usage: less [-ENh~] [FILE]...

View FILE (or stdin) one screenful at a time

    -E      Quit once the end of a file is reached
    -N      Prefix line number to each line
    -~      Suppress ~s displayed past EOF
```

#### license-pfm-upgrade.sh

```
Usage: ls [-1AaCxdLHRFplinsehrSXvctu] [-w WIDTH] [FILE]...

List directory contents

    -1      One column output
    -a      Include entries which start with .
    -A      Like -a, but exclude . and ..
    -C      List by columns
    -x      List by lines
    -d      List directory entries instead of contents
    -L      Follow symlinks
    -H      Follow symlinks on command line
    -R      Recurse
    -p      Append / to dir entries
    -F      Append indicator (one of */=@|) to entries
    -l      Long listing format
    -i      List inode numbers
    -n      List numeric UIDs and GIDs instead of names
    -s      List allocated blocks
    -e      List full date and time
    -h      List sizes in human readable format (1K 243M 2G)
    -r      Sort in reverse order
    -S      Sort by size
    -X      Sort by extension
    -v      Sort by version
    -c      With -l: sort by ctime
    -t      With -l: sort by mtime
    -u      With -l: sort by atime
    -w N    Assume the terminal is N columns wide
    --color[={always,never,auto}]   Control coloring

No license files in given directory --help
```

#### lite_mon

```
lite_mon wifiX <option> <arguments>

    --direction: Specify the direction <rx/tx>
    --level: Specify the level <MSDU/MPDU/PPDU>
    --disable: Disable lite mon filter
    --filter_fp: set filter for filter pass
    --filter_mo: set filter for monitor other
    --filter_md: set filter for monitor direct
    --filter_fpmo: set filter for filter pass monitor override
            filter format: 0xTSSSS, T:type, SSSS:Subtype mask
    --mgmt_len: Length of management frame to be filtered
    --ctrl_len: Length of control frame to be filtered
    --data_len: Length of data frame to be filtered
            length options: 0x40, 0x80, Default: Full packet
    --metadata: Enable metadata <0x1/0x2>
    --output: output vap to deliver <athX>
    --show_filter: Show the provided filter option
    --peer_add: Add peer into peer filter list <mac_addr1,mac_addr2,mac_addr3,....>
    --peer_remove: remove peer frm peer filer list <mac_addr1,mac_addr2,mac_addr3,....>
    --peer_list: List the peers added into peer filtering list
    --vap: ifname to which the peer is to be added
    --debug: Debug option for lite_mon <0/1/2/3/4>
    --help: Display help menu
```

#### lldpcli

```
Usage:   lldpcli [OPTIONS ...] [COMMAND ...]
Version: lldpd 1.0.15

    -d          Enable more debugging information.
    -u socket   Specify the Unix-domain socket used for communication with lldpd(8).
    -f format   Choose output format (plain, keyvalue, json, json0).
    -c conf     Read the provided configuration file.

see manual page lldpcli(8) for more information
```

#### lldpctl

```
Version: lldpd 1.0.15

Usage:   lldpctl [OPTIONS ...] [COMMAND ...]

    -d          Enable more debugging information.
    -u socket   Specify the Unix-domain socket used for communication with lldpd(8).
    -f format   Choose output format (plain, keyvalue, json, json0).

see manual page lldpcli(8) for more information
```

#### lldpd

```
Usage:   lldpd [OPTIONS ...]
Version: lldpd 1.0.15

    -d       Do not daemonize.
    -r       Receive-only mode
    -i       Disable LLDP-MED inventory TLV transmission.
    -k       Disable advertising of kernel release, version, machine.
    -S descr Override the default system description.
    -P name  Override the default hardware platform.
    -m IP    Specify the IP management addresses of this system.
    -u file  Specify the Unix-domain socket used for communication with lldpctl(8).
    -H mode  Specify the behaviour when detecting multiple neighbors.
    -I iface Limit interfaces to use.
    -C iface Limit interfaces to use for computing chassis ID.
    -L path  Override path for lldpcli command.
    -O file  Override default configuration locations processed by lldpcli(8) at start.
    -M class Enable emission of LLDP-MED frame. 'class' should be one of:
            1 Generic Endpoint (Class I)
            2 Media Endpoint (Class II)
            3 Communication Device Endpoints (Class III)
            4 Network Connectivity Device

Additional protocol support.
    -c       Enable the support of CDP protocol. (Cisco)
    -e       Enable the support of EDP protocol. (Extreme)
    -f       Enable the support of FDP protocol. (Foundry)
    -s       Enable the support of SONMP protocol. (Nortel)

see manual page lldpd(8) for more information
```

#### ln

```
Usage: ln [OPTIONS] TARGET... LINK|DIR

Create a link LINK or DIR/TARGET to the specified TARGET(s)

    -s      Make symlinks instead of hardlinks
    -f      Remove existing destinations
    -n      Don't dereference symlinks - treat like normal file
    -b      Make a backup of the target (if exists) before link operation
    -S suf  Use suffix instead of ~ when making backup files
    -T      2nd arg must be a DIR
    -v      Verbose
```

#### logger

```
Usage: logger [OPTIONS] [MESSAGE]

Write MESSAGE (or stdin) to syslog

    -s      Log to stderr as well as the system log
    -t TAG  Log using the specified tag (defaults to user name)
    -p PRIO Priority (numeric or facility.level pair)
```

#### login

```
Usage: login [-p] [-h HOST] [[-f] USER]

Begin a new session on the system

    -f      Don't authenticate (user already authenticated)
    -h HOST Host user came from (for network logins)
    -p      Preserve environment
```

#### logread

```
Usage: logread [-fF]

Show messages in syslogd's circular buffer

    -f      Output data as log grows
    -F      Same as -f, but dump buffer first
```

#### lowi-lib-test
#### lowi-server
#### lowi-test
#### ls

```
Usage: ls [-1AaCxdLHRFplinsehrSXvctu] [-w WIDTH] [FILE]...

List directory contents

    -1      One column output
    -a      Include entries which start with .
    -A      Like -a, but exclude . and ..
    -C      List by columns
    -x      List by lines
    -d      List directory entries instead of contents
    -L      Follow symlinks
    -H      Follow symlinks on command line
    -R      Recurse
    -p      Append / to dir entries
    -F      Append indicator (one of */=@|) to entries
    -l      Long listing format
    -i      List inode numbers
    -n      List numeric UIDs and GIDs instead of names
    -s      List allocated blocks
    -e      List full date and time
    -h      List sizes in human readable format (1K 243M 2G)
    -r      Sort in reverse order
    -S      Sort by size
    -X      Sort by extension
    -v      Sort by version
    -c      With -l: sort by ctime
    -t      With -l: sort by mtime
    -u      With -l: sort by atime
    -w N    Assume the terminal is N columns wide
    --color[={always,never,auto}]   Control coloring
```

#### lsmod
#### lsof
#### lspci
#### lsusb
#### macsec_shell

> This is a utility shell. Enter via `macsec_shell` -- Exit via `exit`

The following output was via:

```
U7Pro-BZ.7.0.66# macsec_shell

macsec> ?
```

```
macsec>
  exit                                            Exit current mode and down to previous mode
  quit                                            Exit current mode and down to previous mode
  nss_macsec_secy_tx_reg                          nss_macsec_secy_tx_reg
  nss_macsec_secy_tx_drop_sc_sa_invlid            nss_macsec_secy_tx_drop_sc_sa_invlid
  nss_macsec_secy_tx_unmatched_use_sc_0           nss_macsec_secy_tx_unmatched_use_sc_0
  nss_macsec_secy_tx_gcm_start                    nss_macsec_secy_tx_gcm_start
  nss_macsec_secy_tx_drop_class_miss              nss_macsec_secy_tx_drop_class_miss
  nss_macsec_secy_tx_drop_kay_pkt                 nss_macsec_secy_tx_drop_kay_pkt
  nss_macsec_secy_tx_ctl_filt                     nss_macsec_secy_tx_ctl_filt
  nss_macsec_secy_tx_ctl_filt_clear               nss_macsec_secy_tx_ctl_filt_clear
  nss_macsec_secy_tx_class_lut                    nss_macsec_secy_tx_class_lut
  nss_macsec_secy_tx_class_lut_clear              nss_macsec_secy_tx_class_lut_clear
  nss_macsec_secy_tx_sc                           nss_macsec_secy_tx_sc
  nss_macsec_secy_tx_sc_en                        nss_macsec_secy_tx_sc_en
  nss_macsec_secy_tx_sc_del                       nss_macsec_secy_tx_sc_del
  nss_macsec_secy_tx_sc_an                        nss_macsec_secy_tx_sc_an
  nss_macsec_secy_tx_sc_an_roll_over_en           nss_macsec_secy_tx_sc_an_roll_over_en
  nss_macsec_secy_tx_sc_in_used                   nss_macsec_secy_tx_sc_in_used
  nss_macsec_secy_tx_sc_tci_7_2                   nss_macsec_secy_tx_sc_tci_7_2
  nss_macsec_secy_tx_sc_confidentiality_offset    nss_macsec_secy_tx_sc_confidentiality_offset
  nss_macsec_secy_tx_sc_protect                   nss_macsec_secy_tx_sc_protect
  nss_macsec_secy_tx_sc_sci                       nss_macsec_secy_tx_sc_sci
  nss_macsec_secy_tx_sc_start_stop_time           nss_macsec_secy_tx_sc_start_stop_time
  nss_macsec_secy_tx_sa                           nss_macsec_secy_tx_sa
  nss_macsec_secy_tx_sa_en                        nss_macsec_secy_tx_sa_en
  nss_macsec_secy_tx_sa_del                       nss_macsec_secy_tx_sa_del
  nss_macsec_secy_tx_sa_next_pn                   nss_macsec_secy_tx_sa_next_pn
  nss_macsec_secy_tx_sa_in_used                   nss_macsec_secy_tx_sa_in_used
  nss_macsec_secy_tx_sa_start_stop_time           nss_macsec_secy_tx_sa_start_stop_time
  nss_macsec_secy_tx_sak                          nss_macsec_secy_tx_sak
  nss_macsec_secy_tx_pn_threshold                 nss_macsec_secy_tx_pn_threshold
  nss_macsec_secy_rx_reg                          nss_macsec_secy_rx_reg
  nss_macsec_secy_rx_ctl_filt                     nss_macsec_secy_rx_ctl_filt
  nss_macsec_secy_rx_ctl_filt_clear               nss_macsec_secy_rx_ctl_filt_clear
  nss_macsec_secy_rx_prc_lut                      nss_macsec_secy_rx_prc_lut
  nss_macsec_secy_rx_prc_lut_clear                nss_macsec_secy_rx_prc_lut_clear
  nss_macsec_secy_rx_sc                           nss_macsec_secy_rx_sc
  nss_macsec_secy_rx_sc_en                        nss_macsec_secy_rx_sc_en
  nss_macsec_secy_rx_sc_del                       nss_macsec_secy_rx_sc_del
  nss_macsec_secy_rx_sc_validate_frame            nss_macsec_secy_rx_sc_validate_frame
  nss_macsec_secy_rx_sc_replay_protect            nss_macsec_secy_rx_sc_replay_protect
  nss_macsec_secy_rx_sc_anti_replay_window        nss_macsec_secy_rx_sc_anti_replay_window
  nss_macsec_secy_rx_sc_in_used                   nss_macsec_secy_rx_sc_in_used
  nss_macsec_secy_rx_sc_an_roll_over              nss_macsec_secy_rx_sc_an_roll_over
  nss_macsec_secy_rx_sc_start_stop_time           nss_macsec_secy_rx_sc_start_stop_time
  nss_macsec_secy_rx_sa                           nss_macsec_secy_rx_sa
  nss_macsec_secy_rx_sa_en                        nss_macsec_secy_rx_sa_en
  nss_macsec_secy_rx_sa_next_pn                   nss_macsec_secy_rx_sa_next_pn
  nss_macsec_secy_rx_sa_del                       nss_macsec_secy_rx_sa_del
  nss_macsec_secy_rx_sak                          nss_macsec_secy_rx_sak
  nss_macsec_secy_rx_sa_in_used                   nss_macsec_secy_rx_sa_in_used
  nss_macsec_secy_rx_sa_start_stop_time           nss_macsec_secy_rx_sa_start_stop_time
  nss_macsec_secy_rx_pn_threshold                 nss_macsec_secy_rx_pn_threshold
  nss_macsec_secy                                 nss_macsec_secy
  nss_macsec_secy_tx_sw                           nss_macsec_secy_tx_sw
  nss_macsec_secy_sc_sa_mapping_mode              nss_macsec_secy_sc_sa_mapping_mode
  nss_macsec_secy_controlled_port_en              nss_macsec_secy_controlled_port_en
  nss_macsec_secy_ip_version                      nss_macsec_secy_ip_version
  nss_macsec_secy_cipher_suite                    nss_macsec_secy_cipher_suite
  nss_macsec_secy_mtu                             nss_macsec_secy_mtu
  nss_macsec_secy_id                              nss_macsec_secy_id
  nss_macsec_secy_en                              nss_macsec_secy_en
  nss_macsec_secy_tx_sc_mib                       nss_macsec_secy_tx_sc_mib
  nss_macsec_secy_tx_sa_mib                       nss_macsec_secy_tx_sa_mib
  nss_macsec_secy_tx_mib                          nss_macsec_secy_tx_mib
  nss_macsec_secy_rx_sa_mib                       nss_macsec_secy_rx_sa_mib
  nss_macsec_secy_rx_mib                          nss_macsec_secy_rx_mib
  g_fal_tx_sak_t                                  g_fal_tx_sak_t
  fal_tx_sak_t                                    fal_tx_sak_t
  g_fal_rx_ctl_filt_t                             g_fal_rx_ctl_filt_t
  fal_rx_ctl_filt_t                               fal_rx_ctl_filt_t
  g_fal_rx_prc_lut_t                              g_fal_rx_prc_lut_t
  fal_rx_prc_lut_t                                fal_rx_prc_lut_t
  g_fal_tx_ctl_filt_t                             g_fal_tx_ctl_filt_t
  fal_tx_ctl_filt_t                               fal_tx_ctl_filt_t
  g_fal_tx_mib_t                                  g_fal_tx_mib_t
  fal_tx_mib_t                                    fal_tx_mib_t
  g_fal_rx_mib_t                                  g_fal_rx_mib_t
  fal_rx_mib_t                                    fal_rx_mib_t
  g_fal_rx_sa_mib_t                               g_fal_rx_sa_mib_t
  fal_rx_sa_mib_t                                 fal_rx_sa_mib_t
  g_fal_rx_sak_t                                  g_fal_rx_sak_t
  fal_rx_sak_t                                    fal_rx_sak_t
  g_fal_tx_class_lut_t                            g_fal_tx_class_lut_t
  fal_tx_class_lut_t                              fal_tx_class_lut_t
  g_fal_tx_sa_mib_t                               g_fal_tx_sa_mib_t
  fal_tx_sa_mib_t                                 fal_tx_sa_mib_t
  g_fal_tx_sc_mib_t                               g_fal_tx_sc_mib_t
  fal_tx_sc_mib_t                                 fal_tx_sc_mib_t
  nss_macsec_secy_tx_qtag_parse                   nss_macsec_secy_tx_qtag_parse
  nss_macsec_secy_tx_stag_parse                   nss_macsec_secy_tx_stag_parse
  nss_macsec_secy_rx_replay_protect               nss_macsec_secy_rx_replay_protect
  nss_macsec_secy_rx_validate_frame               nss_macsec_secy_rx_validate_frame
  nss_macsec_secy_xpn_en                          nss_macsec_secy_xpn_en
  nss_macsec_secy_rx_sa_next_xpn                  nss_macsec_secy_rx_sa_next_xpn
  nss_macsec_secy_tx_sa_next_xpn                  nss_macsec_secy_tx_sa_next_xpn
  nss_macsec_secy_rx_sc_ssci                      nss_macsec_secy_rx_sc_ssci
  nss_macsec_secy_tx_sc_ssci                      nss_macsec_secy_tx_sc_ssci
  g_fal_tx_sa_ki_t                                g_fal_tx_sa_ki_t
  g_fal_rx_sa_ki_t                                g_fal_rx_sa_ki_t
  fal_tx_sa_ki_t                                  fal_tx_sa_ki_t
  fal_rx_sa_ki_t                                  fal_rx_sa_ki_t
  nss_macsec_secy_rx_sa_ki                        nss_macsec_secy_rx_sa_ki
  nss_macsec_secy_tx_sa_ki                        nss_macsec_secy_tx_sa_ki
  nss_macsec_secy_udf_ethtype                     nss_macsec_secy_udf_ethtype
  nss_macsec_secy_loopback                        nss_macsec_secy_loopback
  nss_macsec_secy_special_pkt_ctrl                nss_macsec_secy_special_pkt_ctrl
  nss_macsec_secy_flow_control_en                 nss_macsec_secy_flow_control_en
  g_fal_tx_udf_filt_t                             g_fal_tx_udf_filt_t
  fal_tx_udf_filt_t                               fal_tx_udf_filt_t
  nss_macsec_secy_tx_udf_filt                     nss_macsec_secy_tx_udf_filt
  g_fal_rx_udf_filt_t                             g_fal_rx_udf_filt_t
  fal_rx_udf_filt_t                               fal_rx_udf_filt_t
  nss_macsec_secy_rx_udf_filt                     nss_macsec_secy_rx_udf_filt
  g_fal_tx_udf_ufilt_cfg_t                        g_fal_tx_udf_ufilt_cfg_t
  fal_tx_udf_ufilt_cfg_t                          fal_tx_udf_ufilt_cfg_t
  nss_macsec_secy_tx_udf_ufilt_cfg                nss_macsec_secy_tx_udf_ufilt_cfg
  g_fal_tx_udf_cfilt_cfg_t                        g_fal_tx_udf_cfilt_cfg_t
  fal_tx_udf_cfilt_cfg_t                          fal_tx_udf_cfilt_cfg_t
  nss_macsec_secy_tx_udf_cfilt_cfg                nss_macsec_secy_tx_udf_cfilt_cfg
  g_fal_rx_udf_ufilt_cfg_t                        g_fal_rx_udf_ufilt_cfg_t
  fal_rx_udf_ufilt_cfg_t                          fal_rx_udf_ufilt_cfg_t
  nss_macsec_secy_rx_udf_ufilt_cfg                nss_macsec_secy_rx_udf_ufilt_cfg
```

#### mca-cli
#### mca-cli-op
#### mca-ctrl
#### mca-custom-alert.sh

```
generate a custom json formate payload and send out the payload as a notification

    -k: input key.   ex: UAP-arp-table
    -v: input value. ex: "$(cat /proc/net/arp)"
    -d: dry run, only generate the json payload and will not send out the notification

mca-custom-alert.sh -k "key1" -v "value1" -k "key2" -v "value2" ...
```

#### mca-dump

(Long json output)

#### mca-monitor
#### mca-scan

(Long json output)

#### mca-sta

```
Usage: /usr/bin/mca-sta [options] <args...>
    mca-dump     : dump all reporting stat
    mca-dump     : dump all wireless scan stat
    mca-sta <mac>: show stat for sta

options:
    -h: help
    -f: force dump stat
    -l: loop
```

#### mca.sh

```
Usage: /usr/bin/mca.sh [options] <args...>
    mca-dump     : dump all reporting stat
    mca-dump     : dump all wireless scan stat
    mca-sta <mac>: show stat for sta

options:
    -h: help
    -f: force dump stat
    -l: loop
```

#### mcad

```
Management Console Agent v1.5 (c) Ubiquiti Networks, Inc.
Usage: mcad [options]
        -n [N]           start instance with nid N (default 0)
        -s [path]        ubus socket path
        -d               debug (logging to stdout)
        -v               increase verbosity (accumulative)
        -h               print this help
```

#### mcsctl

```
Usage:
mcsctl -s brname state state(enable or disable)
mcsctl -s brname debug state(enable or disable)
mcsctl -s brname policy value(flood or drop)
mcsctl -s brname aging time(s)
mcsctl -s brname retag state(enable or disable) dscp
mcsctl -s brname route type(flood, drop, specify or default) ifname
mcsctl -s brname acl add type(igmp or mld) rule(Disable, Multicast, SystemWideManagement, Management, NonSnooping or Internal) pattern(ipv4, ipv6 or mac) ip(mac) ipmask(macmask)
mcsctl -s brname acl flush type(igmp or mld)
mcsctl -s brname convertall state(enable or disable)
mcsctl -s brname timeout from(GroupSpecificQueries, AllSystemQueries or GroupMembershipInterval) state(enable or disable)
mcsctl -s brname IGMPv3MLDv2Filter state(enable or disable)
mcsctl -s brname IgnoreTbit state(enable or disable)
mcsctl -s brname LocalQueryInterval value
mcsctl -s brname LocalInspect state(enable or disable)
mcsctl -s brname extraqueryresponse value
mcsctl -s brname QRVThreshold value
mcsctl -s brname mcrouter state(enable or disable)
mcsctl -g brname acltbl num_entries
mcsctl -g brname mdbtbl num_entries


example:
mcsctl -s br-lan state enable
mcsctl -s br-lan debug enable
mcsctl -s br-lan policy flood
mcsctl -s br-lan aging 260
mcsctl -s br-lan retag enable 40
mcsctl -s br-lan route specify eth0.5
mcsctl -s br-lan acl add igmp SystemWideManagement ipv4 224.0.0.1 255.255.255.255
mcsctl -s br-lan acl add igmp Multicast mac 01:00:5e:00:00:00 ff:ff:ff:00:00:00
mcsctl -s br-lan acl flush igmp
mcsctl -s br-lan convertall enable
mcsctl -s br-lan timeout AllSystemQueries disable
mcsctl -s br-lan LocalQueryInterval 125
mcsctl -g br-lan acltbl 20
mcsctl -g br-lan mdbtbl 20
```


#### mcsd
#### mcst

> This is a utility shell. Enter via `mcst` -- Exit via `exit` or `CTRL+Z`

```
Use `h' and `help' for help messages
Use `dbg here' to see log messages; other dbg cmds for log level

@ h
h [cmd] -- short help (first line of each help message).
help [cmd] -- long help.
q -- quit interactive menu
exit [<status>] -- terminate server
dbg -- debug printing control menu
md -- core module menu
evloop -- Event loop menu
wlan (wlanManager) -- WLAN Manager
mc (mcManager) -- Multicast manager service
dbgService -- debug service menu
```

#### md5sum
#### memtester

```
memtester version 4.3.0 (32-bit)
Copyright (C) 2001-2012 Charles Cazabon.
Licensed under the GNU General Public License version 2 (only).

pagesize is 4096
pagesizemask is 0xfffff000
need memory argument, in MB

Usage: memtester [-p physaddrbase [-d device]] <mem>[B|K|M|G] [loops]
```

#### mesh-monitor
#### mkdir

```
Usage: mkdir [OPTIONS] DIRECTORY...

Create DIRECTORY

    -m MODE Mode
    -p      No error if exists; make parent directories as needed
```

#### mke2fs

```
Usage: mke2fs [-c|-l filename] [-b block-size] [-C cluster-size]
        [-i bytes-per-inode] [-I inode-size] [-J journal-options]
        [-G flex-group-size] [-N number-of-inodes] [-d root-directory]
        [-m reserved-blocks-percentage] [-o creator-os]
        [-g blocks-per-group] [-L volume-label] [-M last-mounted-directory]
        [-O feature[,...]] [-r fs-revision] [-E extended-option[,...]]
        [-t fs-type] [-T usage-type ] [-U UUID] [-e errors_behavior][-z undo_file]
        [-jnqvDFSV] device [blocks-count]
```

#### mkfifo

```
Usage: mkfifo [-m MODE] NAME

Create named pipe

    -m MODE Mode (default a=rw)
```

#### mkfs.ext2

```
Usage: mkfs.ext2 [-c|-l filename] [-b block-size] [-C cluster-size]
        [-i bytes-per-inode] [-I inode-size] [-J journal-options]
        [-G flex-group-size] [-N number-of-inodes] [-d root-directory]
        [-m reserved-blocks-percentage] [-o creator-os]
        [-g blocks-per-group] [-L volume-label] [-M last-mounted-directory]
        [-O feature[,...]] [-r fs-revision] [-E extended-option[,...]]
        [-t fs-type] [-T usage-type ] [-U UUID] [-e errors_behavior][-z undo_file]
        [-jnqvDFSV] device [blocks-count]
```

#### mkfs.ext3

```
Usage: mkfs.ext3 [-c|-l filename] [-b block-size] [-C cluster-size]
        [-i bytes-per-inode] [-I inode-size] [-J journal-options]
        [-G flex-group-size] [-N number-of-inodes] [-d root-directory]
        [-m reserved-blocks-percentage] [-o creator-os]
        [-g blocks-per-group] [-L volume-label] [-M last-mounted-directory]
        [-O feature[,...]] [-r fs-revision] [-E extended-option[,...]]
        [-t fs-type] [-T usage-type ] [-U UUID] [-e errors_behavior][-z undo_file]
        [-jnqvDFSV] device [blocks-count]
```

#### mkfs.ext4

```
Usage: mkfs.ext4 [-c|-l filename] [-b block-size] [-C cluster-size]
        [-i bytes-per-inode] [-I inode-size] [-J journal-options]
        [-G flex-group-size] [-N number-of-inodes] [-d root-directory]
        [-m reserved-blocks-percentage] [-o creator-os]
        [-g blocks-per-group] [-L volume-label] [-M last-mounted-directory]
        [-O feature[,...]] [-r fs-revision] [-E extended-option[,...]]
        [-t fs-type] [-T usage-type ] [-U UUID] [-e errors_behavior][-z undo_file]
        [-jnqvDFSV] device [blocks-count]
```

#### mknod

```
Usage: mknod [-m MODE] NAME TYPE MAJOR MINOR

Create a special file (block, character, or pipe)

    -m MODE Creation mode (default a=rw)

TYPE:
    b       Block device
    c or u  Character device
    p       Named pipe (MAJOR and MINOR are ignored)
```

#### mksquashfs4

```
SYNTAX: mksquashfs4 source1 source2 ...  dest [options] [-e list of exclude dirs/files]

Filesystem build options:
    -comp <comp>            select <comp> compression
                            Compressors available:
                                    gzip (default)
                                    lzma
                                    xz
    -b <block_size>         set data block to <block_size>.  Default 131072 bytes
    -no-exports             don't make the filesystem exportable via NFS
    -no-sparse              don't detect sparse files
    -no-xattrs              don't store extended attributes (default)
    -xattrs                 store extended attributes (unsupported)
    -noI                    do not compress inode table
    -noD                    do not compress data blocks
    -noF                    do not compress fragment blocks
    -noX                    do not compress extended attributes
    -no-fragments           do not use fragments
    -always-use-fragments   use fragment blocks for files larger than block size
    -no-duplicates          do not perform duplicate checking
    -all-root               make all files owned by root
    -force-uid uid          set all file uids to uid
    -force-gid gid          set all file gids to gid
    -nopad                  do not pad filesystem to a multiple of 4K
    -keep-as-directory      if one source directory is specified, create a root
                            directory containing that directory, rather than the
                            contents of the directory

Filesystem filter options:
    -p <pseudo-definition>  Add pseudo file definition
    -pf <pseudo-file>       Add list of pseudo file definitions
    -sort <sort_file>       sort files according to priorities in <sort_file>.  One
                            file or dir with priority per line.  Priority -32768 to
                            32767, default priority 0
    -ef <exclude_file>      list of exclude dirs/files.  One per line
    -wildcards              Allow extended shell wildcards (globbing) to be used in
                            exclude dirs/files
    -regex                  Allow POSIX regular expressions to be used in exclude
                            dirs/files

Filesystem append options:
    -noappend               do not append to existing filesystem
    -root-becomes <name>    when appending source files/directories, make the
                            original root become a subdirectory in the new root
                            called <name>, rather than adding the new source items
                            to the original root

Mksquashfs runtime options:
    -version                print version, licence and copyright message
    -recover <name>         recover filesystem data using recovery file <name>
    -no-recovery            don't generate a recovery file
    -info                   print files written to filesystem
    -no-progress            don't display the progress bar
    -processors <number>    Use <number> processors.  By default will use number of
                            processors available
    -read-queue <size>      Set input queue to <size> Mbytes.  Default 64 Mbytes
    -write-queue <size>     Set output queue to <size> Mbytes.  Default 512 Mbytes
    -fragment-queue <size>  Set fragment queue to <size> Mbytes.  Default 64 Mbytes

Miscellaneous options:
    -root-owned             alternative name for -all-root
    -noInodeCompression     alternative name for -noI
    -noDataCompression      alternative name for -noD
    -noFragmentCompression  alternative name for -noF
    -noXattrCompression     alternative name for -noX

Compressors available and compressor specific options:
    gzip (no options) (default)
    lzma
        -Xpreset <preset>
            compression preset (0-9, default 6)
        -Xe
            Try to improve compression ratio by using more CPU time.
        -Xlc <lc>
            Number of literal context bits (0-4, default 3)
        -Xlp <lp>
            Number of literal position bits (0-4, default 0)
        -Xpb <pb>
            Number of position bits (0-4, default 2)
        -Xnice <nice>
            Nice length of a match (5-273, default 64)
        -Xdict-size <dict-size>
            Use <dict-size> as the LZMA dictionary size.  The dictionary size
            can be specified as a percentage of the block size, or as an
            absolute value.  The dictionary size must be less than or equal
            to the block size and 4096 bytes or larger.  It must also be
            storable in the lzma header as either 2^n or as 2^n+2^(n+1).
            Example dict-sizes are 75%, 50%, 37.5%, 25%, or 32K, 16K, 8K
            etc.
    xz
        -Xpreset <preset>
            compression preset (0-9, default 6)
        -Xe
            Try to improve compression ratio by using more CPU time.
        -Xlc <lc>
            Number of literal context bits (0-4, default 3)
        -Xlp <lp>
            Number of literal position bits (0-4, default 0)
        -Xpb <pb>
            Number of position bits (0-4, default 2)
        -Xnice <nice>
            Nice length of a match (5-273, default 64)
        -Xdict-size <dict-size>
            Use <dict-size> as the XZ dictionary size.  The dictionary size
            can be specified as a percentage of the block size, or as an
            absolute value.  The dictionary size must be less than or equal
            to the block size and 8192 bytes or larger.  It must also be
            storable in the lzma header as either 2^n or as 2^n+2^(n+1).
            Example dict-sizes are 75%, 50%, 37.5%, 25%, or 32K, 16K, 8K
            etc.
        -Xbcj filter1,filter2,...,filterN
            Compress using filter1,filter2,...,filterN in turn
            (in addition to no filter), and choose the best compression.
            Available filters: x86, arm, armthumb, powerpc, sparc, ia64
```

#### mkswap

```
Usage: mkswap [-L LBL] BLOCKDEV [KBYTES]

Prepare BLOCKDEV to be used as swap partition

        -L LBL  Label
```

#### mktemp

```
Usage: mktemp [-dt] [-p DIR] [TEMPLATE]

Create a temporary file with name based on TEMPLATE and print its name.
TEMPLATE must end with XXXXXX (e.g. [/dir/]nameXXXXXX).
Without TEMPLATE, -t tmp.XXXXXX is assumed.

    -d      Make directory, not file
    -q      Fail silently on errors
    -t      Prepend base directory name to TEMPLATE
    -p DIR  Use DIR as a base directory (implies -t)
    -u      Do not create anything; print a name

Base directory is: -p DIR, else $TMPDIR, else /tmp
```

#### mmc_info

```
USAGE: mmc_info <OPTIONS> (-n name |-b blk)

Lookup mmc info based on /usr/etc/mmc-table.txt
    -b  Lookup part name by block (ex: mmcblk0p3)
    -n  Lookup block by part name (ex: kernel0)

OPTIONS: Only one print type can be given
    -B  Print block device (default for name lookup)
    -F  Print full /dev/<blk> path
    -N  Print part name (default for block lookup)
    -O  Print part offset in bytes
    -S  Print part size in bytes
```

#### modinfo

```
Usage:
        modinfo module
```

#### modprobe

```
Usage:
        modprobe [-q] filename
```

#### mount

```
Usage: mount [OPTIONS] [-o OPT] DEVICE NODE

Mount a filesystem. Filesystem autodetection requires /proc.

    -a              Mount all filesystems in fstab
    -i              Don't run mount helper
    -r              Read-only mount
    -t FSTYPE[,...] Filesystem type(s)
    -O OPT          Mount only filesystems with option OPT (-a only)

-o OPT:
    loop            Ignored (loop devices are autodetected)
    [a]sync         Writes are [a]synchronous
    [no]atime       Disable/enable updates to inode access times
    [no]diratime    Disable/enable atime updates to directories
    [no]relatime    Disable/enable atime updates relative to modification time
    [no]dev         (Dis)allow use of special device files
    [no]exec        (Dis)allow use of executable files
    [no]suid        (Dis)allow set-user-id-root programs
    [r]shared       Convert [recursively] to a shared subtree
    [r]slave        Convert [recursively] to a slave subtree
    [r]private      Convert [recursively] to a private subtree
    [un]bindable    Make mount point [un]able to be bind mounted
    [r]bind         Bind a file or directory [recursively] to another location
    move            Relocate an existing mount point
    remount         Remount a mounted filesystem, changing flags
    ro              Same as -r
```

#### mount_root
#### mpstat

```
Usage: mpstat [-A] [-I SUM|CPU|ALL|SCPU] [-u] [-P num|ALL] [INTERVAL [COUNT]]

Per-processor statistics

    -A                      Same as -I ALL -u -P ALL
    -I SUM|CPU|ALL|SCPU     Report interrupt statistics
    -P num|ALL              Processor to monitor
    -u                      Report CPU utilization
```

#### mtd

```
Usage: mtd [<options> ...] <command> [<arguments> ...] <device>[:<device>...]

The device is in the format of mtdX (eg: mtd4) or its label.

mtd recognizes these commands:
    unlock                  unlock the device
    refresh                 refresh mtd partition
    erase                   erase all data on device
    verify <imagefile>|-    verify <imagefile> (use - for stdin) to device
    write <imagefile>|-     write <imagefile> (use - for stdin) to device
    jffs2write <file>       append <file> to the jffs2 partition on the device

Following options are available:
    -q                      quiet mode (once: no [w] on writing,
                                            twice: no status messages)
    -n                      write without first erasing the blocks
    -r                      reboot after successful command
    -f                      force write without trx checks
    -e <device>             erase <device> before executing the command
    -d <name>               directory for jffs2write, defaults to "tmp"
    -j <name>               integrate <file> into jffs2 data when writing an image
    -s <number>             skip the first n bytes when appending data to the jffs2 partiton, defaults to "0"
    -p <number>             write beginning at partition offset
    -l <length>             the length of data that we want to dump

Example: To write linux.trx to mtd4 labeled as linux and reboot afterwards
         mtd -r write linux.trx linux
```

#### mv

```
Usage: mv [-fin] SOURCE DEST
or: mv [-fin] SOURCE... DIRECTORY

Rename SOURCE to DEST, or move SOURCE(s) to DIRECTORY

    -f      Don't prompt before overwriting
    -i      Interactive, prompt before overwrite
    -n      Don't overwrite an existing file
```

#### myftm

```
usage: myftm [options]
   -n, --nodaemon      do not run as a daemon
   -d    show more debug messages (-dd for even more)
   -i <wlan interface>
       --interface=<wlan interface>
       wlan adapter name (wlan, eth, etc.) default wlan
   -B  <dbs/phya/phyb/sbs> (Phy RF Mode)
   -D  <DAC GAIN>
   -H  <0/1/2> (RX Mode)
   -I  <0/1> (Phy Id)
   -J  (TLV 2.0 Messages)
   -N  <BSSID>
   -O  <STA Addr>
   -o  <BT Addr>
   -Q  <Secondary Frequncy>
   -U  <0/1> (ShortGuard)
   -X  <TX Sta Addr>
   -Y  <RX Sta Addr>
   --sar <0/1/2/3>
   --sarindex <0/1/2/3/4/0xff>
   --sarchain <0/1>
   --sarcck2glimit <0 - 0xff>
   --sarofdm2glimit <0 - 0xff>
   --sarofdm5glimit <0 - 0xff>
   --dpdflag (enable)
   --regdomain <00:01> (Two reg domain values)
   --dpdstatus
   --rateBw <set bandwidth>
   --nss <set nss>
   --gI <set shortgi>
   --dcm <set ofdma dcm>
   --ppdutype <set ofdma ppdutype>
   --linkdir  <set ofdma link direction>
   --toneplan <set ofdma toneplan params>
   --fecpad <set prefecpad params>
   --ldpc <set extra symbol for ldpc>
   --ulofdmat <set ofdma uplink transmmit config>
   --dutycl <set duty cycle>
   --regw <set register address>
   --regd <read register address>
   --regval <write value to register address>
   --lowpower <set low power config for phyid>
   --lpw_mode <set low power mode>
   --phyidmask <set phyid mask>
   --lpwfmsk   <set feature mask>
   --caltxgain <Gain (RF gain for WCN) for open loop power control mode>
   --forcedrxidx <set Forced RX gain index>
   --rstdir <set RSSI self test direction, 0: chain0 to chain1 1: chain1 to chain0>
   --rst  <RSSI self test (need to enable dbs mode before this test
           per cmd myftm -J -B dbs)>
   --aifsn <set aifsn number>
   --pw_mode_6g <set 6g power mode 0-None 1-VLP 2-LPI 3-SP>
   --puncBw <set puncture bandwidth pattern eg:0x1>
   --help   display this help and exit
```

#### nc

```
Usage: nc [IPADDR PORT]

Open a pipe to IP:PORT
```

#### netmsg

```
usage: netmsg <ip> "<message>"
```

#### netstat

```
Usage: netstat [-ral] [-tuwx] [-enWp]

Display networking information

    -r      Routing table
    -a      All sockets
    -l      Listening sockets
            Else: connected sockets
    -t      TCP sockets
    -u      UDP sockets
    -w      Raw sockets
    -x      Unix sockets
            Else: all socket types
    -e      Other/more information
    -n      Don't resolve names
    -W      Wide display
    -p      Show PID/program name for sockets
```

#### nettool

```
Usage: nettool [options]

    -i ...: Detect if this IP Address is locally routable
```

#### nice

```
Usage: nice [-n ADJUST] [PROG ARGS]

Change scheduling priority, run PROG

    -n ADJUST       Adjust priority by ADJUST
```

#### nohup

```
Usage: nohup PROG ARGS

Run PROG immune to hangups, with output to a non-tty
```

#### nslookup

```
Usage: nslookup [HOST] [SERVER]

Query the nameserver for the IP address of the given HOST
optionally using a specified DNS server
```

#### nsm-app
#### nss-udp-st
#### ntpd

```
Usage: ntpd [-dnqNwl -I IFACE] [-S PROG] [-p PEER]...

NTP client/server

    -d      Verbose
    -n      Do not daemonize
    -q      Quit after clock is set
    -N      Run at high priority
    -w      Do not set time (only query peers), implies -n
    -S PROG Run PROG after stepping time, stratum change, and every 11 mins
    -p PEER Obtain time from PEER (may be repeated)
    -l      Also run as server on port 123
    -I IFACE Bind server to IFACE, implies -l
```

#### ntpd-hotplug
#### ol_regdomain

```
usage: ol_regdomain [options] [cc | rd]

Available options:
    -h - Help
    -c - display Channel numbers
    -C - Format output like the Linux db.txt
    -f - display Frequencies
    -i - display Indoor channels
    -o - display Outdoor channels
    -d - Debug output
    -j - Javascript addons
    -l - List country and regulatory domain codes
    -L - List countries
    -m - Mode <sta|ibss|adhoc|ap|hostap|monitor>
    -p - Passive channels
    -q - Query for all AP models
    -v - verbose - make logging more detailed
    -w - clock selection <0|1|2|3>
    -s - channel Shifting <0..40>
    -a - All channels
    -A - 11A channels
    -B - 11B channels
    -G - 11G channels
    -P - PSC channels only (6g frequencies)
    -T - 11a Turbo  channels
    -S - SuperG channels
    -X - 802.11ax channels
    -Z - include normally excluded channels
    -6 - 6Ghz extended channels
    -y - can provision channels with provided filters; returns 1 (allowed) or 0 (not allowed)
    -r - display obey (strict) regulatory requirements
```

#### oopsdump

```
Usage: oopsdump [-c]

    -c                  clear oops logs
```

#### openssl

```
help:

Standard commands
asn1parse     ca            ciphers       cmp           crl
crl2pkcs7     dgst          dhparam       dsa           dsaparam
ec            ecparam       enc           engine        errstr
fipsinstall   gendsa        genpkey       genrsa        help
info          kdf           list          mac           nseq
ocsp          passwd        pkcs12        pkcs7         pkcs8
pkey          pkeyparam     pkeyutl       prime         rand
rehash        req           rsa           rsautl        s_client
s_server      s_time        sess_id       smime         speed
spkac         storeutl      verify        version       x509

Message Digest commands (see the `dgst' command for more details)
md4           md5           sha1          sha224        sha256
sha3-224      sha3-256      sha3-384      sha3-512      sha384
sha512        sha512-224    sha512-256    shake128      shake256

Cipher commands (see the `enc' command for more details)
aes-128-cbc   aes-128-ecb   aes-192-cbc   aes-192-ecb   aes-256-cbc
aes-256-ecb   base64        des           des-cbc       des-cfb
des-ecb       des-ede       des-ede-cbc   des-ede-cfb   des-ede-ofb
des-ede3      des-ede3-cbc  des-ede3-cfb  des-ede3-ofb  des-ofb
des3          desx          rc4           rc4-40
```

#### passwd

```
Usage: passwd [OPTIONS] [USER]

Change USER's password (default: current user)

    -a ALG  Encryption method
    -d      Set password to ''
    -l      Lock (disable) account
    -u      Unlock (enable) account
```

#### peerratestats
#### pgrep

```
Usage: pgrep [-flnovx] [-s SID|-P PPID|PATTERN]

Display process(es) selected by regex PATTERN

    -l      Show command name too
    -f      Match against entire command line
    -n      Show the newest process only
    -o      Show the oldest process only
    -v      Negate the match
    -x      Match whole name (not substring)
    -s      Match session ID (0 for current)
    -P      Match parent process ID
```

#### pidof

```
Usage: pidof [NAME]...

List PIDs of all processes with names that match NAMEs
```

#### ping

```
Usage: ping [-LRUbdfnqrvVaAD] [-c count] [-i interval] [-w deadline]
            [-p pattern] [-s packetsize] [-t ttl] [-I interface]
            [-M pmtudisc-hint] [-m mark] [-S sndbuf]
            [-T tstamp-options] [-Q tos] [hop1 ...] destination
```

#### ping6

```
Usage: ping6 [-LUdfnqrvVaAD] [-c count] [-i interval] [-w deadline]
             [-p pattern] [-s packetsize] [-t ttl] [-I interface]
             [-M pmtudisc-hint] [-S sndbuf] [-F flowlabel] [-Q tclass]
             [hop1 ...] destination
```

#### pivot_root

```
Usage: pivot_root NEW_ROOT PUT_OLD

Move the current root file system to PUT_OLD and make NEW_ROOT
the new root file system
```

#### pkill

```
Usage: pkill [-l|-SIGNAL] [-fnovx] [-s SID|-P PPID|PATTERN]

Send a signal to process(es) selected by regex PATTERN

    -l      List all signals
    -f      Match against entire command line
    -n      Signal the newest process only
    -o      Signal the oldest process only
    -v      Negate the match
    -x      Match whole name (not substring)
    -s      Match session ID (0 for current)
    -P      Match parent process ID
```

#### pktgen.sh

```
Usage: /bin/pktgen.sh
    -i <if_name>
    -d <dst_ip>
    -m <dst_mac>
    -s <pkt_size>
    -c <pkt_count|0>
```

#### pktlogconf

```
Packet log configuration
usage: pktlogconf [-a adapter] [-e[event-list]] [-d adapter] [-s log-size] [-t -k -l]
                  [-b -p -i]
    -h    show this usage
    -a    configures packet logging for specific 'adapter';
          configures system-wide logging if this option is
          not specified
    -d    disable packet logging
    -e    enable logging events listed in the 'event-list'
          event-list is an optional comma separated list of one or more
          of the following: rx tx rcf rcu ani actnack lite latency  (eg., pktlogconf -erx,rcu,tx,cbf,hinfo,steering,actnack,lite,latency)
    -s    change the size of log-buffer to "log-size" bytes
    -t    enable logging of TCP headers
    -k    enable triggered stop by a threshold number of TCP SACK packets
    -l    change the number of packets to log after triggered stop
    -b    enable triggered stop by a throughput threshold
    -p    enable triggered stop by a PER threshold
    -i    change the time period of counting throughput/PER
    -r    reset the pktlog buffer
    -R    to enable remote packet logging
    -P    Remote packet log port
    -C    Remote packet log IP addr
```

#### pktlogdump

```
Packet log dump

usage: pktlogdump [-p [event-list]] [-s]

options:
    -h    show this usage
    -a    dumps log for specific 'adapter';
          dumps system-wide log if this option is
          not specified
    -l    print all log events listed in the 'event-list'
          event-list is a comma(,) seperated list of one or more
          of the foll: rx tx rcf rcu ani cbf hinfo steering[eg., pktlogdump -f rx,rcu]
          prints all events if 'event-list' is not specified
               cannot be used with -x option
    -x    Dump the packetlog buffer
    -P    print PER statistics
    -I    print detailed interpacket arrival time histogram stats
    -i    print distilled interpacket arrival time histogram stats
```

#### poweroff

```
Usage: poweroff [-d DELAY] [-n] [-f]

Halt and shut off power

    -d SEC  Delay interval
    -n      Do not sync
    -f      Force (don't go through init)
```

#### printf

```
usage: printf FORMAT [ARGUMENT...]
```

#### procd

```
Usage: procd [options]

Options:
    -s <path>       Path to ubus socket
    -h <path>       run as hotplug daemon
    -d <level>      Enable debug messages
    -S              Print messages to stdout
```

#### ps

```
Usage: ps

Show list of processes

    w       Wide output
```

#### pwd

> Command to print the current working directory.
>
> ~ "Print Working Directory"

#### qca_gensock
#### qcatestcmd

```
usage:
qcatestcmd [-i device] commands
commands:
--tx <frame/tx99/tx100/sine/off>
      --phyId <0/1>
      --txfreq <Tx channel or freq(default 2412)>
      --txfreq2 <Tx channel or freq(default 2412)>
      --txrate < 0 - 1L / 1 - 2L / 2 - 5L / 3 - 11L / 4 - 2S / 5 - 5S / 6 - 11S / 10 - 6Mbps / 11 - 9 Mbps / 12 - 12 Mbps / 13 - 18 Mbps / 14 - 24 Mbps / 15 - 36 Mbps / 16 - 48 Mbps / 17 - 54 Mbps / 20 - MCS0 / 21 - MCS1 / 22 - MCS2 / 23 - MCS3 / 24 - MCS4 / 25 -MCS5 / 26 - MCS6 / 27 - MCS7 / 28 - MCS8 / 29 - MCS9 / 30 - MCS / 31 - MCS11 / 32 - MCS12 / 33 - MCS13 / -1 - CW>
      --rateBw < -1 - CW / 0 - CCK / 1 - LegacyOFDM / 2 - HT20 / 3- HT40 / 4 - VHT20 / 5 - VHT40 / 6 - VHT80 / 7 - VHT80P80 / 8 - HE20 / 9 - HE40 / 10 - HE80 / 11 - HE80P80 / 12 - OFDMA_HE20 / 13 - OFDMA_HE40 / 14 - OFDMA_HE80 / 15 - OFDMA_HE80P80 / 16 - HE160 / 17 - OFDMA_HE160 / 18 - HE165 / 19 - OFDMA_HE165 / 20 - VHT160 / 21 - VHT165 / -1 - CW>
      --phy165Mode <0/1/2>
      --txpwr <0-30dBm (tx99/txframe: 0-60 in 0.5 dBm resolution, i.e 1=0.5dbm, 2=1dbm.....; sine: 0-60, PCDAC vaule)>
      --tgtpwr <target power>
      --pcdac <power control DAC>
      --gainIdx <tx gain table index>
      --dacGain <DAC gain>
      --forcedGain <power control DAC>
      --txantenna <1/2/0 (auto)>
      --txpktsz <pkt size, [32-1500](default 1500)>
      --txpattern <tx data pattern, 0: all zeros; 1: all ones; 2: repeating 10; 3: PN7; 4: PN9; 5: PN15
      --txchain (1:on chain 0, 2:on chain 1, 4: on chain2, 8: on chain3, 15 on all 4 chains  )
      --tpcm <forcedTgtPwr/forcedGainIdx/forcedGain/txpwr/tgtpwr/forcedGlutIdx> : Set transmit power control mode, by default tpcm is set to txpwr
      --ani (Enable ANI. The ANI is disabled if this option is not specified)
      --gI <Guard Interval. 0 - GI_0 / 1 - LTF_Mode0_GI_400 / 2 - LTF_Mode0_GI_800 / 3 - LTF_Mode0_GI_1600 / 4 - LTF_Mode0_GI_3200 / 17 - LTF_Mode1_GI_400 / 18 - LTF_Mode1_GI_800 / 19 - LTF_Mode1_GI_1600 / 20 - LTF_Mode1_GI_3200 / 33 - LTF_Mode2_GI_400 / 34 - LTF_Mode2_GI_800 / 35 - LTF_Mode2_GI_1600 / 36 - LTF_Mode2_GI_3200 / 49 - LTF_Mode4_GI_400 / 50 - LTF_Mode4_GI_800 / 51 - LTF_Mode4_GI_1600 / 52 - LTF_Mode4_GI_3200>
      --paprd (Enable PAPRD. The PAPRD is disabled if this option is not specified)
      --stbc (Enable STBC. STBC is disabled if this option is not specified)
      --ldpc (Enable LDPC. LDPC is disabled if this option is not specified)
      --scrambleroff (Disable scrambler. The scrambler is enabled by default)
      --aifsn <AIFS slots num,[0-252](Used only under '--tx frame' mode)>
      --shortguard (use short guard)
      --ofdmaDcm
      --ofdmaLinkDir (0->uplink, 1->downlink)
      --ofdmaPpduType (0->singleUser, 1-> multipleUsers, 2->extRangeSingleUser, 3->tigger)
      --mode <cbstate->legacy mapping - bw20->ht20/vht20 / bw40_low->ht40minus/vht40minus / bw40_high->ht40plus/vht40plus / bw80_x->vht80_x:x=0:3
                                        bw80p80->vht80p80 / bw160->vht160 / bw165  / bw80p80_x->vht80p80_x / bw160_x->vht160_x / bw165_x:x=0:7
        * bw20 ==> primary 20
        * bw40_low ==> primary low
        * bw40_high ==> primary high
      >
      --bw <full/half/quarter>
      --nss <1/2/3/4/5/6/7/8>
      --setlongpreamble <1/0>
      --numpackets <number of packets to send 0-65535>
          --setup <setup tx parameters without transmitting>
          --go <start transmitting>
--tx sine --txfreq <Tx channel or freq(default 2412)>
      --agg <number of aggregate packets>
      --bssid
      --srcmac <source MAC address>
      --dstmac <destination MAC address>
--tx sine --txfreq <Tx channel or freq(default 2412)>
--rx <promis/filter(default MacAddress: 01:00:00:C0:FF:EE)/report>
      --phyId <0/1>
      --rxfreq <Rx channel or freq(default 2412)>
      --rxfreq2 <Rx channel or freq(default 2412)>
      --rxantenna <1/2/0 (auto)>
      --rxchain <1:chain 0, 2:chain 1, 3:both>
      --mode <cbstate->legacy mapping - bw20->ht20/vht20 / bw40_low->ht40minus/vht40minus / bw40_high->ht40plus/vht40plus / bw80_x->vht80_x:x=0:3
                                        bw80p80->vht80p80 / bw160->vht160 / bw165  / bw80p80_x->vht80p80_x / bw160_x->vht160_x / bw165_x:x=0:7
        * bw20 ==> primary 20
        * bw40_low ==> primary low
        * bw40_high ==> primary high
      >
          --rxMac <mac addr like 00:03:7f:be:ef:11>
      --ack <Enable/Disable ACK, 0:disable; 1:enable, by default ACK is enabled>
      --bc <0:receive unicast frame (default), 1:receive broadcast frame>
      --lpl <0:LPL off(default), 1:reduced receive, 2:reduced search>
          --setup <setup rx parameters without receiving>
          --go <start receiving>
--pm <wakeup/sleep/deepsleep>
--setmac <mac addr like 00:03:7f:be:ef:11>
--setbssid <mac addr like 00:03:7f:be:ef:11>
--SetAntSwitchTable <table1 in hex value> <table2 in hex value>  (Set table1=0 and table2=0 will restore the default AntSwitchTable)
--efusedump --start <start address> --end <end address>
--efusewrite <start_offsetxx lengthxx contentsxx xx> (all in hex)
--otpwrite filename or sectionIdxx lengthxx dataxx(xx xx)  (could be one or multiple data in quotation marks)
--otpdump
--otpreset xx: xx=1-> OTPSTREAM_READ, xx=2->OTPSTREAM_WRITE
--btmode <put DUT into BT mode>
--eepromdump
--eepromwrite --bdfile fakeBoardData.bin
--eepromerase
--eepromcheck --totalsize xx --offset xx --blocksize xx
--hwcal <fullresetcal/reset1/reset2/reset3/hwreset/initbl/fullcal/rxdco/rxfilt/rxiq/txiq/txcl/pkdet/noisefloor/dpd/lna>
    --loop <loop count>
          --chmask <1:on chain 0, 2:on chain 1, 4: on chain2, 8: on chain3, 15 on all 4 chains>
          --loopback <0 or 1: loopBack parameter for rxdco cal>
    --savecal <0 or 1: save the calibration. Valid only when rxdco/rxfilt/rxiq/txiq/txcl/pkdet is specified>
    --nfcal <0 or 1: do noise floor cal after the calibration. Valid only when rxdco/rxfilt/rxiq/txiq/txcl/pkdet is specified>
--rr --addr xx
--rw --addr xx --value xx
--getnvmac
--setnvmac <mac addr like 00:03:7f:be:ef:11>
--nvbdcommit --nvtype xx --nvsegment xx  --nvcompressed xx
--getcalbdata --totalsize xx --offset xx --blocksize xx
--getbdatasize
--gettxpwr txfreq mode bflag txchain
--calLm
--calPwr
--mr --addr xx --numbytes xx
--mw --addr xx --numbytes xx --value
--dpdtimingidx
--dpdtrainingquality
--dpdatten
--dpdagc2power
--lmtxinit txpacketNum(0 or 1000)
--lmchannellist lm_flag (1) itemNum(no more than 6 for testing)
--lmquery cmdId (0 or 1)
--lmgo cmdId (0)
--lmrxinit promis
--norssiavg < disable rssi averaging in Rx and report last packet rssi >
--band <set band 0-5G 1-2G>
--chainidx <set chainindex>
--cus_ctrl_cal <xtal/opc/rx_gain: To specify the cal of interest >
--capin <set capIN value for xtal cal>
--capout <set capOUT value for xtal cal>
--xtal_opt <get_default: To Get default values programmed in bdf /
            set: To start CW and set capin and capout values for tuning /
            save: Save final capin and capout values to target /
            read:read final capin and capout values set in Target /
            stop:Stop Xtal cal /
            writeotp: capin and capout values to otp /
            readotp:read capin and capout values set in otp >
--opc_opt <init: To clear existing OPC caldata /
           get_target_params: To get GLUT offset and Thermal offset /
                        usage: qcatestcmd  -i wifiX --phyId X --cus_ctrl_cal opc --opc_opt get_target_params/
           set_target_params: To set poweroffset, GLUT offset and Thermal offset obtained from OPC Result> /
                        usage: qcatestcmd  -i wifiX --phyId X --cus_ctrl_cal opc –-freq <frequency> -–chainidx <tx chain> --opcband <value>
                        --poweroffset <poweroffset> --glutoffset <GLUT offset> --thermaloffset <Thermal offset> --opc_opt set_target_params /
    --poweroffset   <set calculated poweroffset value for OPC cal in 8dB steps format>
    --glutoffset    <set glutoffset value obtained from OPC Result>
    --thermaloffset <set thermaloffset value obtained from OPC Result>
--rxgaincal_opt <init: To clear existing RxGain caldata /
           get_target_params: To get NFdbr, NFdbm and minccathreshold /
                        usage: qcatestcmd  -i wifiX --phyId X --chainidx X --cus_ctrl_cal rx_gain --rxgaincal_opt get_target_params/
           set_target_params: To set NFdbr, NFdbm and minccathreshold obtained from RxGaincal Result> /
                        usage: qcatestcmd  -i wifiX --phyId X --txfreq <freq> --chainidx X --NFdbr <NFdbr value> --NFdbm <NFdbm value>
                         --minccathreshold <minccathreshold value> --cus_ctrl_cal rx_gain --rxgaincal_opt set_target_params
    --NFdbr            <To set NFdbr value obtained from RxGaincal Result>
    --NFdbm            <To set NFdbm value obtained from RxGaincal Result>
    --minccathreshold  <To set minccathreshold value obtained from RxGaincal Result>
--toneplan <load the tone plan file present in current directory or file path should be appended before the file if file present in other directory>
        <eg: /usr/lib/example.txt>
```

#### qdss_setup.sh
#### qld_server

```
Usage: qld_server <qld_port> <diag_port> stream_port
```

#### qldtool

```
qldtool for memory dump of important structures
usage: qldtool -B -i [-h]
options:
    -B run daemon in the background
    -i radio name wifiX
    -h help
```

#### qosLinkAddGroup.sh

```
/bin/qosLinkAddGroup.sh <interface name> <interface rate in mbit> <group id> <rate allocated in % >
```

#### qosLinkInit.sh

```
/bin/qosLinkInit.sh [<mode>] <interface name> <interface rate in mbit>
```

#### qos_control.sh

```
Usage: qos_control.sh (cmd) <args...>

CMDS:
    show        [-s] DEVS...
    add-root    DEV RATE
    del-root    DEV
    has-root    DEV
    add-vap     DEV VAPID RATE_MIN RATE_MAX
    del-vaps    DEV
    add-sta     DEV VAPID AID RATE_MIN RATE_MAX
    change-sta  DEV VAPID AID RATE_MIN RATE_MAX
    replace-sta DEV VAPID AID RATE_MIN RATE_MAX
    del-sta     DEV VAPID AID
```

#### qrtr-cfg

```
qrtr-cfg <node-id>
```

#### qrtr-lookup

```
Usage: qrtr-lookup [<service> [<instance> [<filter>]]]
```

#### qrtr-ns

```
qrtr-ns
    -f,     Run process in foreground
    -i,     Configure local node id to <node-id>
    -h,     Help option to print usage
```

#### radartool

> default output of `radartool`:

```
U7-Pro-BZ.7.0.21# radartool
Radar;
Use NOL: no
Firpwr (thresh to see if radar sig is gone):  0
Radar Rssi (thresh to start radar det in dB): 0
Height (thresh for pulse height (dB):         0
Pulse rssi (thresh if pulse is gone in dB):   0
Inband (thresh if pulse is inband (in 0.5dB): 0
Relative power check disabled
Relative step for pulse detection disabled
Max length of radar sig in 0.8us units: 0
```

> help output

```
Usage: radartool (-i <interface>) [cmd]
       for cfg : radartool -n (-i <interface>) [cmd]
firpwr X            set firpwr (thresh to check radar sig is gone) to X (int32)
rrssi X             set radar rssi (start det) to X dB (u_int32)
height X            set threshold for pulse height to X dB (u_int32)
prssi               set threshold to checkif pulse is gone to X dB (u_int32)
inband X            set threshold to check if pulse is inband to X (0.5 dB) (u_int32)
dfstime X           set dfs test time to X secs
en_relpwr_check X   enable/disable radar relative power check (AR5413 only)
relpwr X            set threshold to check the relative power of radar (AR5413 only)
usefir128 X         en/dis using in-band pwr measurement over 128 cycles(AR5413 only)
en_block_check X    en/dis to block OFDM weak sig as radar det(AR5413 only)
en_max_rrssi X      en/dis to use max rssi instead of last rssi (AR5413 only)
en_relstep X        en/dis to check pulse relative step (AR5413 only)
relstep X           set threshold to check relative step for pulse det(AR5413 only)
maxlen X            set max length of radar signal(in 0.8us step) (AR5413 only)
numdetects          get number of radar detects
chknol X            check NOL state with channel
getnol              get NOL channel information
setnol              set NOL channel information
dfsdebug            set the DFS debug mask
dfs_disable_radar_marking X
                    set this flag so that after radar detection on a DFS chan,
                    the channel is not marked as radar and is not blocked from
                    being set as AP's channel. However,the radar hit chan will
                    be added to NOL list.
g_dfs_disable_radar_marking
                    Retrieve the value of disable_radar_marking flag.
usenol X            set nol to X, where X is:
                    1 (default) make CSA and switch to a new channel on radar detect
                    0, make CSA with next channel same as current on radar detect
                    2, make CSA with next channel, switch to a new channel on radar detect
                    and add the radar hit channels to NOL.
                    In case of FO chipset, NOL resides in FW as well and the NOL timeout of the FW
                    cannot be modified. With usenol 2 option (used only for internal testing)
                    the nol timeout of the host can be configured and the channels are not
                    added to FW NOL.
ignorecac X         enable (X=0) or disable (X=1) CAC
setnoltimeout X     set nol timeout for X secs (Default value = 1800 sec)
injectSequence      Inject a synthetic sequence of pulses from a user file to DFS Module
allowHWPulses       Disable/Enable HW pulses and then inject the synthetic sequence
bangradar           simulate radar on entire current channel
bangradar X         simulate radar at the given segment ID, where
                    X is segment id(0, 1) or 0 in Pine
bangradar X Y Z     simulate radar at particular frequency, where
                    X is segment id(0, 1) or 0 in Pine
                    Y is chirp information(0 - Non chirp, 1 - Chirp)
                    Z is frequency offset(-40MHz <= Z <= 40MHz in HK,
                    -80MHz <= Z <= 80MHz in Pine)
                    Example:
                    To simulate chirp radar on segment 1 with frequency offset -10Mhz in HK:
                    radartool -i wifi0 bangradar 1 1 -10
bangradar X Y Z D   simulate radar at detector ID D, where
                    X is segment id(0, 1) or 0 in Pine
                    Y is chirp information(0 - Non chirp, 1 - Chirp)
                    Z is frequency offset(-40MHz <= Z <= 40MHz in HK,
                    -80MHz <= Z <= 80MHz in Pine)
                    D is detector ID (2 - Agile Detector in HK, 1 in pine)
                    Example:
                    To simulate radar on Agile Detector,
                    radartool -i wifi0 bangradar 0 0 0 2
showPreCACLists     show preCAC forest structure with current NOL and CAC status
resetPreCACLists    reset pre CAC list
shownol             show NOL channels
shownolhistory      show NOL channel history
disable             disable radar detection
enable              enable radar detection in software
false_rssi_thr X    set false rssi threshold to X (Default is 50)
rfsat_peak_mag X    set peak magnitude to X (Default is 40)
setcacvalidtime X   set CAC validity time to X secs
getcacvalidtime     get CAC validity time in secs
```

#### radartoolw

> default output of `radartool`:

```
U7-Pro-BZ.7.0.21# radartoolw

Radar;
Use NOL: no
Firpwr (thresh to see if radar sig is gone):  0
Radar Rssi (thresh to start radar det in dB): 0
Height (thresh for pulse height (dB):         0
Pulse rssi (thresh if pulse is gone in dB):   0
Inband (thresh if pulse is inband (in 0.5dB): 0
Relative power check disabled
Relative step for pulse detection disabled
Max length of radar sig in 0.8us units: 0
[  603.918579] wlan: [6236:E:SPECTRAL] ucfg_spectral_is_mode_specific_request: Invalid spectral cp request id 4
[  603.918709] wlan: [6236:E:SPECTRAL] ucfg_spectral_is_mode_specific_request: Invalid spectral cp request id 3
```

> help output

```
Usage: radartool (-i <interface>) [cmd]
       for cfg : radartool -n (-i <interface>) [cmd]

firpwr X            set firpwr (thresh to check radar sig is gone) to X (int32)
rrssi X             set radar rssi (start det) to X dB (u_int32)
height X            set threshold for pulse height to X dB (u_int32)
prssi               set threshold to checkif pulse is gone to X dB (u_int32)
inband X            set threshold to check if pulse is inband to X (0.5 dB) (u_int32)
dfstime X           set dfs test time to X secs
en_relpwr_check X   enable/disable radar relative power check (AR5413 only)
relpwr X            set threshold to check the relative power of radar (AR5413 only)
usefir128 X         en/dis using in-band pwr measurement over 128 cycles(AR5413 only)
en_block_check X    en/dis to block OFDM weak sig as radar det(AR5413 only)
en_max_rrssi X      en/dis to use max rssi instead of last rssi (AR5413 only)
en_relstep X        en/dis to check pulse relative step (AR5413 only)
relstep X           set threshold to check relative step for pulse det(AR5413 only)
maxlen X            set max length of radar signal(in 0.8us step) (AR5413 only)
numdetects          get number of radar detects
chknol X            check NOL state with channel
getnol              get NOL channel information
setnol              set NOL channel information
dfsdebug            set the DFS debug mask
dfs_disable_radar_marking X
                    set this flag so that after radar detection on a DFS chan,
                    the channel is not marked as radar and is not blocked from
                    being set as AP's channel. However,the radar hit chan will
                    be added to NOL list.
g_dfs_disable_radar_marking
                    Retrieve the value of disable_radar_marking flag.
usenol X            set nol to X, where X is:
                    1 (default) make CSA and switch to a new channel on radar detect
                    0, make CSA with next channel same as current on radar detect
                    2, make CSA with next channel, switch to a new channel on radar detect
                    and add the radar hit channels to NOL.
                    In case of FO chipset, NOL resides in FW as well and the NOL timeout of the FW
                    cannot be modified. With usenol 2 option (used only for internal testing)
                    the nol timeout of the host can be configured and the channels are not
                    added to FW NOL.
ignorecac X         enable (X=0) or disable (X=1) CAC
setnoltimeout X     set nol timeout for X secs (Default value = 1800 sec)
injectSequence      Inject a synthetic sequence of pulses from a user file to DFS Module
allowHWPulses       Disable/Enable HW pulses and then inject the synthetic sequence
bangradar           simulate radar on entire current channel
bangradar X         simulate radar at the given segment ID, where
                    X is segment id(0, 1) or 0 in Pine
bangradar X Y Z     simulate radar at particular frequency, where
                    X is segment id(0, 1) or 0 in Pine
                    Y is chirp information(0 - Non chirp, 1 - Chirp)
                    Z is frequency offset(-40MHz <= Z <= 40MHz in HK,
                    -80MHz <= Z <= 80MHz in Pine)
                    Example:
                    To simulate chirp radar on segment 1 with frequency offset -10Mhz in HK:
                    radartool -i wifi0 bangradar 1 1 -10
bangradar X Y Z D   simulate radar at detector ID D, where
                    X is segment id(0, 1) or 0 in Pine
                    Y is chirp information(0 - Non chirp, 1 - Chirp)
                    Z is frequency offset(-40MHz <= Z <= 40MHz in HK,
                    -80MHz <= Z <= 80MHz in Pine)
                    D is detector ID (2 - Agile Detector in HK, 1 in pine)
                    Example:
                    To simulate radar on Agile Detector,
                    radartool -i wifi0 bangradar 0 0 0 2
showPreCACLists     show preCAC forest structure with current NOL and CAC status
resetPreCACLists    reset pre CAC list
shownol             show NOL channels
shownolhistory      show NOL channel history
disable             disable radar detection
enable              enable radar detection in software
false_rssi_thr X    set false rssi threshold to X (Default is 50)
rfsat_peak_mag X    set peak magnitude to X (Default is 40)
setcacvalidtime X   set CAC validity time to X secs
getcacvalidtime     get CAC validity time in secs
```


#### ramdump

```
Usage: ramdump <dump_type> <dump_file>

Options:
    -h Show this help text
```

#### readlink

```
Usage: readlink [-fnv] FILE

Display the value of a symlink
    
    -f      Canonicalize by following all symlinks
    -n      Don't add newline
    -v      Verbose
```

#### reboot

```
Usage: reboot [-d DELAY] [-n] [-f]

Reboot the system

    -d SEC  Delay interval
    -n      Do not sync
    -f      Force (don't go through init)
```

#### redirector

```
Captive Portal Redirector (c) Ubiquiti Networks, Inc.

Usage: redirector [options]
    -c cfg           config file containing redirector servers
    -d               debug (logging to stdout)
    -v               increase verbosity (can be done multiple times)
    -h               print this help
```

#### registerReboot
#### reload_config
#### reset

> This appears to be the same as the `clear` command

```
Usage: reset

Reset the screen
```

#### reset-handler

```
reset button handler (c) Ubiquiti Networks, Inc.

Usage: reset-handler [options]
    -d               debug (logging to stdout)
    -h               print this help
```

#### rm

```
Usage: rm [-irf] FILE...

Remove (unlink) FILEs

    -i      Always prompt before removing
    -f      Never prompt
    -R,-r   Recurse
```

#### rmdir

```
Usage: rmdir [OPTIONS] DIRECTORY...

Remove DIRECTORY if it is empty

    -p      Include parents
```

#### rmmod

```
Usage:
    rmmod module
```

#### route

```
Usage: route [{add|del|delete}]

Edit kernel routing tables

    -n      Don't resolve names
    -e      Display other/more information
    -A inet{6}      Select address family
```

#### salqostest
#### salruletest

> Unable to find "help" output...
>
> Appears to print all routing rules. Below is example output.

```
Rule obj count 4
=================Config Rule=================
Attr_id = 1
Add_del_rule = 1
Precedence = 1
Rule_output = 1
User_priority = 2
src_mac = <mac address>
dst_mac = <mac address>
src_ipv4_addr = 192.168.1.1
src_ipv4_addr_mask = 255.255.255.255
dst_ipv4_addr = 192.168.1.1
dst_ipv4_addr_mask = 255.255.255.255
src_ipv6_addr = 2001:0db8:85a3:0000:0000:8a2e:0370:7334
src_ipv6_addr_mask = ffff:ffff:ffff:ffff:ffff:ffff:ffff:ffff
dst_ipv6_addr = 2001:0db8:85a3:0000:0000:8a2e:0370:7334
dst_ipv6_addr_mask = ffff:ffff:ffff:ffff:ffff:ffff:ffff:ffff
Src_port = 1
Dst_port = 1
Proto_num = 1
Vlan_id = 1
Dscp = 1
Dscp Remark= 1
Vlan_pcp = 1
Vlan_pcp_remark = 1
Service_class_id = 1
Source port range start = 0
Source port range end = 65535
Destination port range start = 0
Destination port range end = 65535
Rule operation successful
=================Config Rule=================
Attr_id = 2
Add_del_rule = 1
Precedence = 1
Rule_output = 1
User_priority = 2
src_mac = <mac address>
dst_mac = <mac address>
src_ipv4_addr = 192.168.1.1
src_ipv4_addr_mask = 255.255.255.255
dst_ipv4_addr = 192.168.1.1
dst_ipv4_addr_mask = 255.255.255.255
src_ipv6_addr = 2001:0db8:85a3:0000:0000:8a2e:0370:7334
src_ipv6_addr_mask = ffff:ffff:ffff:ffff:ffff:ffff:ffff:ffff
dst_ipv6_addr = 2001:0db8:85a3:0000:0000:8a2e:0370:7334
dst_ipv6_addr_mask = ffff:ffff:ffff:ffff:ffff:ffff:ffff:ffff
Src_port = 1
Dst_port = 1
Proto_num = 1
Vlan_id = 1
Dscp = 1
Dscp Remark= 1
Vlan_pcp = 1
Vlan_pcp_remark = 1
Service_class_id = 1
Source port range start = 0
Source port range end = 65535
Destination port range start = 0
Destination port range end = 65535
Rule operation successful
=================Config Rule=================
Attr_id = 1
Add_del_rule = 2
Illegal nla->nla_type == 0
Illegal nla->nla_type == 0
Illegal nla->nla_type == 0
=======Query Result=======
Rule id: 0x1
Rule precedence: 0x1
Rule output: 0x1
Dscp remark: 0x1
Vlan PCP remark: 0x1
Service_class_id: 0x1
Src port: 0x1
Dst port: 0x1
IP_version_type: 0x0
Classifier_type: 0x1
Src mac address: <mac address>
Dst mac address: <mac address>
Src ipv4 address: 192.168.1.1
Dst ipv4 address: 192.168.1.1
Src ipv4 address mask: 255.255.255.255
Dst ipv4 address mask: 255.255.255.255
Src ipv6 address: 2001:db8:85a3::8a2e:370:7334
Dst ipv6 address: 2001:db8:85a3::8a2e:370:7334
Src ipv6 address mask: ffff:ffff:ffff:ffff:ffff:ffff:ffff:ffff
Dst ipv6 address mask: ffff:ffff:ffff:ffff:ffff:ffff:ffff:ffff
Protocol_number: 0x1
Vlan_id: 0x1
Dscp: 0x1
Vlan_pcp: 0x1
Filter_value: 0
Filter_mask: 0
Source port range start value : 0
Source port range end value : ffff
Destination port range start value : 0
Destination port range end value : ffff
=================Config Rule=================
Attr_id = 2
Add_del_rule = 2
Illegal nla->nla_type == 0
Illegal nla->nla_type == 0
Illegal nla->nla_type == 0
=======Query Result=======
Rule id: 0x2
Rule precedence: 0x1
Rule output: 0x1
Dscp remark: 0x1
Vlan PCP remark: 0x1
Service_class_id: 0x1
Src port: 0x1
Dst port: 0x1
IP_version_type: 0x0
Classifier_type: 0x1
Src mac address: <mac address>
Dst mac address: <mac address>
Src ipv4 address: 192.168.1.1
Dst ipv4 address: 192.168.1.1
Src ipv4 address mask: 255.255.255.255
Dst ipv4 address mask: 255.255.255.255
Src ipv6 address: 2001:db8:85a3::8a2e:370:7334
Dst ipv6 address: 2001:db8:85a3::8a2e:370:7334
Src ipv6 address mask: ffff:ffff:ffff:ffff:ffff:ffff:ffff:ffff
Dst ipv6 address mask: ffff:ffff:ffff:ffff:ffff:ffff:ffff:ffff
Protocol_number: 0x1
Vlan_id: 0x1
Dscp: 0x1
Vlan_pcp: 0x1
Filter_value: 0
Filter_mask: 0
Source port range start value : 0
Source port range end value : ffff
Destination port range start value : 0
Destination port range end value : ffff
```

#### scp

```
usage: scp [-1246BCpqrv] [-c cipher] [-F ssh_config] [-i identity_file]
           [-l limit] [-P port] [-S program]
           [[user@]host1:]file1 [...] [[user@]host2:]file2
```

#### scs_tool

```
scs_tool : Receive SCS config parameters
and updates SPM rule database

Usage:
    scs_tool [-v][-h | ?]
    -v or verbose
        Prints verbose logs
```

#### sed

```
Usage: sed [-inrE] [-f FILE]... [-e CMD]... [FILE]...
or: sed [-inrE] CMD [FILE]...

    -e CMD  Add CMD to sed commands to be executed
    -f FILE Add FILE contents to sed commands to be executed
    -i[SFX] Edit files in-place (otherwise sends to stdout)
            Optionally back files up, appending SFX
    -n      Suppress automatic printing of pattern space
    -r,-E   Use extended regex syntax

If no -e or -f, the first non-option argument is the sed command string.
Remaining arguments are input files (stdin if none).
```

#### selfupgrade

```
Usage: selfupgrade [-d]
    -d - dry run
    -u - start upgrade automatically
    -f - force upgrade (skip version comparison)
```

#### seq

```
Usage: seq [-w] [-s SEP] [FIRST [INC]] LAST

Print numbers from FIRST to LAST, in steps of INC.
FIRST, INC default to 1.

    -w      Pad to last with leading zeros
    -s SEP  String separator
```

#### setsid

```
Usage: setsid [-c] PROG ARGS

Run PROG in a new session. PROG will have no controlling terminal
and will not be affected by keyboard signals (^C etc).

    -c      Set controlling terminal to stdin
```

#### sfe_dump

> some sort of exception dump..?
>
> unable to find "help" output. See below for example output.

```
<sfe_ipv4>
        <connections>
        </connections>
        <exceptions>
                <exception name="UDP_NO_CONNECTION" count="224" />
                <exception name="TCP_NO_CONNECTION_SLOW_FLAGS" count="2" />
                <exception name="TCP_NO_CONNECTION_FAST_FLAGS" count="194" />
                <exception name="ICMP_UNHANDLED_TYPE" count="22" />
                <exception name="ICMP_NO_CONNECTION" count="4" />
                <exception name="UNHANDLED_PROTOCOL" count="12" />
        </exceptions>
        <stats num_connections="0" pkts_dropped="0" pkts_fast_xmited="0" pkts_fast_qdisc_xmited="0" pkts_forwarded="0" pkts_not_forwarded="458" create_requests="0" create_collisions="0" create_failures="0" destroy_requests="0" destroy_misses="0" flushes="0" hash_hits="0" hash_reorders="0" pppoe_encap_pkts_fwded="0" pppoe_decap_pkts_fwded="0" pppoe_bridge_pkts_fwded="0" pppoe_bridge_pkts_3tuple_fwded="0" connection_create_requests_overflow64="0" bridge_vlan_passthorugh_forwarded64="0" />
</sfe_ipv4>
<sfe_ipv6>
        <connections>
        </connections>
        <exceptions>
                <exception name="UDP_NO_CONNECTION" count="38" />
                <exception name="TCP_NO_CONNECTION_SLOW_FLAGS" count="24" />
                <exception name="TCP_NO_CONNECTION_FAST_FLAGS" count="98" />
                <exception name="ICMP_UNHANDLED_TYPE" count="38" />
        </exceptions>
        <stats num_connections="0" pkts_dropped="0" pkts_fast_xmited="0" pkts_fast_qdisc_xmited="0" pkts_forwarded="0" pkts_not_forwarded="198" create_requests="0" create_collisions="0" create_failures="0" destroy_requests="0" destroy_misses="0" flushes="0" hash_hits="0" hash_reorders="0" pppoe_encap_pkts_fwded="0" pppoe_decap_pkts_fwded="0" pppoe_bridge_pkts_fwded="0" pppoe_bridge_pkts_3tuple_fwded="0" connection_create_requests_overflow64="0" fragment_id_lookup_fail="0" fragment_id_entity_alloc_fail="0" fragment_id_evict="0" fragment_id_hash_hits="0" fragments_forwarded="0" fragments_dropped="0" fragment_id_timeout="0" fragments_exception="0" bridge_vlan_passthorugh_forwarded64="0" />
</sfe_ipv6>
```

#### sh

```
Usage: sh [-/+OPTIONS] [-/+o OPT]... [-c 'SCRIPT' [ARG0 [ARGS]] / FILE [ARGS]]

Unix shell interpreter
```

#### sha256sum

```
Usage: sha256sum [-c[sw]] [FILE]...

Print or check SHA256 checksums

    -c      Check sums against list in FILEs
    -s      Don't output anything, status code shows success
    -w      Warn about improperly formatted checksum lines
```

#### show_node

```
Usage: show_node <radio> <mac_addr>
```

#### show_nt
#### signify

```
Usage: signify <command> <options>

Commands:
    -V:                   verify (needs at least -m and -p|-P)
    -S:                   sign (needs at least -m and -s)
    -F:                   print key fingerprint of public/secret key or signature
    -G:                   generate a new keypair

Options:
    -c <comment>:         add comment to keys
    -m <file>:            message file
    -p <file>:            public key file (verify/fingerprint only)
    -P <path>:            public key directory (verify only)
    -q:                   quiet (do not print verification result, use return code only)
    -s <file>:            secret key file (sign/fingerprint only)
    -x <file>:            signature file (defaults to <message file>.sig)
```

#### sleep

```
Usage: sleep [N]...

Pause for a time equal to the total of the args given, where each arg can
have an optional suffix of (s)econds, (m)inutes, (h)ours, or (d)ays
```

#### snmpd

```
Usage:  snmpd [OPTIONS] [LISTENING ADDRESSES]

        Version:  5.8
        Web:      http://www.net-snmp.org/
        Email:    net-snmp-coders@lists.sourceforge.net

  -a                    log addresses
  -A                    append to the logfile rather than truncating it
  -c FILE[,...]         read FILE(s) as configuration file(s)
  -C                    do not read the default configuration files
                          (config search path: /etc/snmp:/usr/share/snmp:/usr/lib/snmp:/etc/persistent/.snmp)
  -d                    dump sent and received SNMP packets
  -D[TOKEN[,...]]       turn on debugging output for the given TOKEN(s)
                          (try ALL for extremely verbose output)
                          Don't put space(s) between -D and TOKEN(s).
  -f                    do not fork from the shell
  -g GID                change to this numeric gid after opening
                          transport endpoints
  -h, --help            display this usage message
  -H                    display configuration file directives understood
  -I [-]INITLIST        list of mib modules to initialize (or not)
                          (run snmpd with -Dmib_init for a list)
  -L <LOGOPTS>          toggle options controlling where to log to
        e:           log to standard error
        o:           log to standard output
        n:           don't log at all
        f file:      log to the specified file
        s facility:  log to syslog (via the specified facility)

        (variants)
        [EON] pri:   log to standard error, output or /dev/null for level 'pri' and above
        [EON] p1-p2: log to standard error, output or /dev/null for levels 'p1' to 'p2'
        [FS] pri token:    log to file/syslog for level 'pri' and above
        [FS] p1-p2 token:  log to file/syslog for levels 'p1' to 'p2'
  -m MIBLIST            use MIBLIST instead of the default MIB list
  -M DIRLIST            use DIRLIST as the list of locations to look for MIBs
                          (default $HOME/.snmp/mibs:/usr/share/snmp/mibs)
  -p FILE               store process id in FILE
  -q                    print information in a more parsable format
  -r                    do not exit if files only accessible to root
                          cannot be opened
  -u UID                change to this uid (numeric or textual) after
                          opening transport endpoints
  -v, --version         display version information
  -V                    verbose display

Deprecated options:
    -l FILE               use -Lf <FILE> instead
    -P                    use -p instead
    -s                    use -Lsd instead
    -S d|i|0-7            use -Ls <facility> instead
```

#### sort

```
Usage: sort [-nru] [FILE]...

Sort lines of text

    -n      Sort numbers
    -r      Reverse sort order
    -u      Suppress duplicate lines
```

#### spectraltool

```
Usage: spectraltool [-i wifiX] [cmd] [cmd_parameter]
    <cmd> = startscan, stopscan, get_advncd, raw_data, diag_stats
            do not require a param
    <cmd> = fft_period, scan_period, fft_recapture, short_report, scan_count,
            priority, fft_size, gc_ena,restart_ena, noise_floor_ref,
            init_delay, nb_tone_thr, str_bin_thr, wb_rpt_mode,
            rssi_rpt_mode, rssi_thr, pwr_format, rpt_mode, bin_scale,
            dBm_adj, chn_mask, debug, frequency, sscan_bw require a param.
            Some of the above may or may not be available depending on
            whether advanced Spectral functionality is implemented
            in hardware, and details are documented in the Spectral
            configuration parameter description. Use the get_advncd command
            to determine if advanced Spectral functionality is supported
            by the interface.
            Also note that applications such as athssd may not work with
            some value combinations for the above parameters, or may
            choose to write values as required by their operation.
    <cmd> = get_samples : Get n samples. Spectral is started and
            stopped automatically. Mandatory argument after cmd
            is number of samples n.
            Optional arguments after number of samples:
            -l <separation_character>
            Where separation_character is a single character to be
            used to separate values in output (e.g. ',' for comma)
            -x <0/1>
            To disable (0) or enable (1) generation III linear bin
            format scaling (default: disabled). This is not applicable
            for other generations.
    <cmd> = dma_ring_debug: Enable(1) or disable(0) the debug of Spectral
            DMA ring. Head and tail pointers of Spectral DMA ring will be
            tracked along with the time at which each buffer is
            received and replenished.
    <cmd> = dma_buff_debug: Enable(1) or disable(0) the debug of Spectral
            DMA buffers. Spectral buffers will be poisoned before
            handing them over to the target and will be validated
            upon arrival, and the target will be asserted upon failure.
    <cmd> = -h : print this usage message
    <cmd> = -p : print description of Spectral configuration parameters.
```

#### ssdk_sh

> This is a utility shell.
>
> * Enter via `ssdk_sh`
> * Exit via `exit`
> * Get help via `?`

The following is help output:

```
dev0@qca>?

    port      config port control
    vlan      config VLAN table
    portVlan  config port base VLAN
    fdb       config FDB table
    acl       config ACL
    qos       config Qos
    igmp      config IGMP/MLD
    leaky     config leaky
    mirror    config mirror
    rate      config rate limit
    sec       config security
    stp       config STP
    mib       show MIB statistics information
    led       set/get led control pattern
    cosmap    set/get cosmap table
    misc      config miscellaneous
    ip        config ip
    flow      config flow
    nat       config nat
    trunk     config trunk
    interface config interface
    vsi       config vsi
    qm        config qm
    ctrlpkt   config control packet
    servcode  config service profile
    rsshash   config rss hash code
    policer   config policer
    shaper    config shaper
    bm        config bm
    debug     read/write register
    device    set device id
    ptp       config ptp
    sfp       sfp data
    vport     config vport
    tunnel    config tunnel
    vxlan     config vxlan
    geneve    config geneve
    mapt      config mapt
    tunnelprogramconfig tunnelprogram
    athtag    config athtag
    help      type ? get help
    quit      type quit/q quit shell
```

#### ssh

```
Dropbear SSH client v2022.83 https://matt.ucc.asn.au/dropbear/dropbear.html

Usage: ssh [options] [user@]host[/port] [command]
    -p <remoteport>
    -l <username>
    -t    Allocate a pty
    -T    Don't allocate a pty
    -N    Don't run a remote command
    -f    Run in background after auth
    -q    quiet, don't show remote banner
    -y    Always accept remote host key if unknown
    -y -y Don't perform any remote host key checking (caution)
    -s    Request a subsystem (use by external sftp)
    -o option     Set option in OpenSSH-like format ('-o help' to list options)
    -i <identityfile>   (multiple allowed, default ~/.ssh/id_dropbear)
    -L <[listenaddress:]listenport:remotehost:remoteport> Local port forwarding
    -g    Allow remote hosts to connect to forwarded ports
    -R <[listenaddress:]listenport:remotehost:remoteport> Remote port forwarding
    -W <receive_window_buffer> (default 24576, larger may be faster, max 10MB)
    -K <keepalive>  (0 is never, default 0)
    -I <idle_timeout>  (0 is never, default 0)
    -z    disable QoS
    -J <proxy_program> Use program pipe rather than TCP connection
    -c <cipher list> Specify preferred ciphers ('-c help' to list options)
    -m <MAC list> Specify preferred MACs for packet verification (or '-m help')
    -b    [bind_address][:bind_port]
    -V    Version
```

#### ssidsteering

```
Usage: ssidsteering [-d] [-C conf-file]
     -d: Do NOT fork into the background: run in debug mode.
     -C: Specify configuration file.
```

#### stahtd
#### stainfo

```
### -ash input ###
U7-Pro-BZ.7.0.59# stainfo -h

### -ash output ###
[U7-Pro] Radios = 3

usage: stainfo [options]
    -a          show all stations (not just the active ones)
    -i <sec>    interval (default is 1)
    -B <br>     Specify bridge device
    -b <band>   radio (ng | na)
    -c <fails>  min RSSI consecutive failures - threshold
    -e <eth0>   Specify ethernet device
    -K          Disable kicking of STAs on detection of ethernet presence
    -r <rssi>   kick sta when rssi is lower than specified
    -n <maxsta> kick sta when total connected sta exceed maxsta limit
    -v          toggle stats
    -t <secs>   kick sta after period of inactivity
    -1          print a one shot table of STAs
    -h          help
```

#### stamgr

```
### -ash input ###
U7-Pro-BZ.7.0.59# stamgr -h

### -ash output ###
[U7-Pro] Radios = 3

usage: stamgr [options]
    -a          show all stations (not just the active ones)
    -i <sec>    interval (default is 1)
    -B <br>     Specify bridge device
    -b <band>   radio (ng | na)
    -c <fails>  min RSSI consecutive failures - threshold
    -e <eth0>   Specify ethernet device
    -K          Disable kicking of STAs on detection of ethernet presence
    -r <rssi>   kick sta when rssi is lower than specified
    -n <maxsta> kick sta when total connected sta exceed maxsta limit
    -v          toggle stats
    -t <secs>   kick sta after period of inactivity
    -1          print a one shot table of STAs
    -h          help
```

#### start-stop-daemon

```
Usage: start-stop-daemon [OPTIONS] [-S|-K] ... [-- ARGS...]

Search for matching processes, and then
    -K: stop all matching processes.
    -S: start a process unless a matching process is found.

Process matching:
    -u USERNAME|UID Match only this user's processes
    -n NAME         Match processes with NAME
                    in comm field in /proc/PID/stat
    -x EXECUTABLE   Match processes with this command
                    command in /proc/PID/cmdline
    -p FILE         Match a process with PID from the file
    All specified conditions must match
-S only:
        -x EXECUTABLE   Program to run
        -a NAME         Zeroth argument
        -b              Background
        -c USER[:[GRP]] Change to user/group
        -m              Write PID to the pidfile specified by -p
-K only:
        -s SIG          Signal to send
        -t              Match only, exit with 0 if a process is found
Other:
        -q              Quiet
```

#### stat

```
Usage: stat [OPTIONS] FILE...

Display file status

    -c FMT  Use the specified format
    -L      Follow links
    -t      Terse display

FMT sequences:
    %a     Access rights in octal
    %A     Access rights in human readable form
    %b     Number of blocks allocated (see %B)
    %B     Size in bytes of each block reported by %b
    %d     Device number in decimal
    %D     Device number in hex
    %f     Raw mode in hex
    %F     File type
    %g     Group ID
    %G     Group name
    %h     Number of hard links
    %i     Inode number
    %n     File name
    %N     File name, with -> TARGET if symlink
    %o     I/O block size
    %s     Total size in bytes
    %t     Major device type in hex
    %T     Minor device type in hex
    %u     User ID
    %U     User name
    %x     Time of last access
    %X     Time of last access as seconds since Epoch
    %y     Time of last modification
    %Y     Time of last modification as seconds since Epoch
    %z     Time of last change
    %Z     Time of last change as seconds since Epoch
```

#### strings

```
Usage: strings [-afo] [-n LEN] [FILE]...

Display printable strings in a binary file

    -a      Scan whole file (default)
    -f      Precede strings with filenames
    -n LEN  At least LEN characters form a string (default 4)
    -o      Precede strings with decimal offsets
```

#### supp
#### swconfig

```
swconfig list

swconfig dev <dev> [port <port>|vlan <vlan>] (help|set <key> <value>|get <key>|load <config>|show)
```

#### switch_root

```
Usage: switch_root [-c /dev/console] NEW_ROOT NEW_INIT [ARGS]

Free initramfs and switch to another root fs:
chroot to NEW_ROOT, delete all in /, move NEW_ROOT to /,
execute NEW_INIT. PID must be 1. NEW_ROOT must be a mountpoint.

    -c DEV  Reopen stdio to DEV after switch
```

#### sync

```
Usage: sync

Write all buffered blocks to disk
```

#### sysctl

```
Usage: sysctl [OPTIONS] [KEY[=VALUE]]...

Show/set kernel parameters

    -e      Don't warn about unknown keys
    -n      Don't show key names
    -a      Show all values
    -w      Set values
    -p FILE Set values from FILE (default /etc/sysctl.conf)
    -q      Set values silently
```

#### syslogd

```
Usage: syslogd [OPTIONS]

System logging utility

    -n              Run in foreground
    -R HOST[:PORT]  Log to HOST:PORT (default PORT:514)
    -p LOGPREFIX    Log prefix to remote syslog server (default is empty)
    -E KEY          Encrypt using KEY
    -L              Log locally and via network (default is network only if -R)
    -C[size_kb]     Log to shared mem buffer (use logread to read it)
    -K              Log to kernel printk buffer (use dmesg to read it)
    -O FILE         Log to FILE (default: /var/log/messages, stdout if -)
    -s SIZE         Max size (KB) before rotation (default:200KB, 0=off)
    -b N            N rotated logs to keep (default:1, max=99, 0=purge)
    -l N            Log only messages more urgent than prio N (1-8)
    -S              Smaller output
    -D              Drop duplicates
    -f FILE         Use FILE as config (default:/etc/syslog.conf)
```

#### syslogd_wrapper.sh
#### sysmon

```
Usage: sysmon [options]

Options:
    -t Shared poll time (in seconds)
    -c System.cfg to use
    -d Debug (logging to stdout)
    -v Increase verbosity
    -h Show this help text
```

#### sysmon_ctrl

```
Usage: sysmon_ctrl [options] -t operation [-o value]

Operation:
     dump

Options:
     -i                 timeout
     -h                 display this help and exit
```

#### sysupgrade

```
Usage: /sbin/sysupgrade [<upgrade-option>...] <image file or URL>
       /sbin/sysupgrade [-q] [-i] <backup-command> <file>

upgrade-option:
    -d <delay>   add a delay before rebooting
    -f <config>  restore configuration from .tar.gz (file or url)
    -i           interactive mode
    -c           attempt to preserve all changed files in /etc/
    -n           do not save configuration over reflash
    -p           do not attempt to restore the partition table after flash.
    -T | --test
        Verify image and config .tar.gz but do not actually flash.
    -F | --force
        Flash image even if image checks fail, this is dangerous!
    -q           less verbose
    -v           more verbose
    -h | --help  display this help

backup-command:
    -b | --create-backup <file>
        create .tar.gz of files specified in sysupgrade.conf
        then exit. Does not flash an image. If file is '-',
        i.e. stdout, verbosity is set to 0 (i.e. quiet).
    -r | --restore-backup <file>
        restore a .tar.gz created with sysupgrade -b
        then exit. Does not flash an image. If file is '-',
        the archive is read from stdin.
    -l | --list-backup
        list the files that would be backed up when calling
        sysupgrade -b. Does not create a backup file.
```

#### syswrapper.sh
#### tail

```
Print last 10 lines of each FILE (or stdin) to stdout.
With more than one FILE, precede each with a filename header.

    -f              Print data as file grows
    -c [+]N[kbm]    Print last N bytes
    -n N[kbm]       Print last N lines
    -n +N[kbm]      Start on Nth line and print the rest
    -q              Never print headers
    -s SECONDS      Wait SECONDS between reads with -f
    -v              Always print headers
    -F              Same as -f, but keep retrying

N may be suffixed by k (x1024), b (x512), or m (x1024^2).
```

#### tar

```
Usage: tar -[cxtzJhvO] [-X FILE] [-T FILE] [-f TARFILE] [-C DIR] [FILE]...

Create, extract, or list files from a tar file

Operation:
    c       Create
    x       Extract
    t       List
    f       Name of TARFILE ('-' for stdin/out)
    C       Change to DIR before operation
    v       Verbose
    z       (De)compress using gzip
    J       (De)compress using xz
    O       Extract to stdout
    h       Follow symlinks
    exclude File to exclude
    X       File with names to exclude
    T       File with names to include
```

#### taskset

```
Usage: taskset [-p] [MASK] [PID | PROG ARGS]

Set or get CPU affinity

    -p      Operate on an existing PID
```

#### tc

```
Usage: tc [ OPTIONS ] OBJECT { COMMAND | help }
       tc [-force] -batch filename

where  OBJECT := { qdisc | class | filter | action | monitor | exec }
       OPTIONS := { -s[tatistics] | -d[etails] | -r[aw] | -p[retty] | -b[atch] [filename] | -n[etns] name |
                    -nm | -nam[es] | { -cf | -conf } path }
```

#### tcpdump

```
tcpdump version 4.9.2
libpcap version 1.8.1

Usage: tcpdump [-aAbdDefhHIJKlLnNOpqStuUvxX#] [ -B size ] [ -c count ]
                [ -C file_size ] [ -E algo:secret ] [ -F file ] [ -G seconds ]
                [ -i interface ] [ -j tstamptype ] [ -M secret ] [ --number ]
                [ -Q in|out|inout ]
                [ -r file ] [ -s snaplen ] [ --time-stamp-precision precision ]
                [ --immediate-mode ] [ -T type ] [ --version ] [ -V file ]
                [ -w file ] [ -W filecount ] [ -y datalinktype ] [ -z postrotate-command ]
                [ -Z user ] [ expression ]
```

#### tee

```
Usage: tee [-ai] [FILE]...

Copy stdin to each FILE, and also to stdout

    -a      Append to the given FILEs, don't overwrite
    -i      Ignore interrupt signals (SIGINT)
```

#### telnet

```
Usage: telnet HOST [PORT]

Connect to telnet server
```

#### tenureprobe.sh
#### test
#### thermald

```
Thermal daemon started

Temperature sensor daemon

Optional arguments:
    --config-file/-c <file>        config file
    --debug/-d                     debug output
    --help/-h                      this help screen
```

#### thermald_wrapper.sh

> This seems to give the same output as `thermald` but I can't find "help" output.

#### thermaltool

```
Uses:

thermaltool
    -i wifiX
    -get/-set
    -e [0/1: enable/disable]
    -et [event time in dutycycle units]
    -dc [duty cycle in ms]
    -dl [debug level]
    -pN [policy for lvl N]
    -loN [low th for lvl N]
    -hiN [high th for lvl N]
    -offN [Tx Off time for lvl N]
    -qpN [TxQ priority lvl N]
    -g
```

#### time

```
Usage: time [-v] PROG ARGS

Run PROG, display resource usage when it exits

    -v      Verbose
```

#### top

```
Usage: top [-b] [-nCOUNT] [-dSECONDS]

Provide a view of process activity in real time.
Read the status of all processes from /proc each SECONDS
and display a screenful of them.

Keys:
    N/M/P/T: sort by pid/mem/cpu/time
    R: reverse sort
    H: toggle threads, 1: toggle SMP
    Q,^C: exit

Options:
    -b      Batch mode
    -n N    Exit after N iterations
    -d N    Delay between updates
```

#### touch

```
Usage: touch [-c] [-d DATE] [-t DATE] [-r FILE] FILE...

Update the last-modified date on the given FILE[s]

    -c      Don't create files
    -d DT   Date/time to use
    -t DT   Date/time to use
    -r FILE Use FILE's date/time
```

#### tr

```
Usage: tr [-cds] STRING1 [STRING2]

Translate, squeeze, or delete characters from stdin, writing to stdout

    -c      Take complement of STRING1
    -d      Delete input characters coded STRING1
    -s      Squeeze multiple output characters of STRING2 into one character
```

#### traceroute

```
Usage: traceroute [-46FIlnrv] [-f 1ST_TTL] [-m MAXTTL] [-q PROBES] [-p PORT]
        [-t TOS] [-w WAIT_SEC] [-s SRC_IP] [-i IFACE]
        [-z PAUSE_MSEC] HOST [BYTES]

Trace the route to HOST

    -4,-6   Force IP or IPv6 name resolution
    -F      Set don't fragment bit
    -l      Display TTL value of the returned packet
    -n      Print numeric addresses
    -r      Bypass routing tables, send directly to HOST
    -v      Verbose
    -f N    First number of hops (default 1)
    -m N    Max number of hops
    -q N    Number of probes per hop (default 3)
    -p N    Base UDP port number used in probes
            (default 33434)
    -s IP   Source address
    -i IFACE Source interface
    -t N    Type-of-service in probe packets (default 0)
    -w SEC  Time to wait for a response (default 3)
    -g IP   Loose source route gateway (8 max)
```

#### traceroute6

```
Usage: traceroute6 [-nrv] [-m MAXTTL] [-q PROBES] [-p PORT]
        [-t TOS] [-w WAIT_SEC] [-s SRC_IP] [-i IFACE]
        HOST [BYTES]

Trace the route to HOST

    -n      Print numeric addresses
    -r      Bypass routing tables, send directly to HOST
    -v      Verbose
    -m N    Max number of hops
    -q N    Number of probes per hop (default 3)
    -p N    Base UDP port number used in probes
            (default 33434)
    -s IP   Source address
    -i IFACE Source interface
    -t N    Type-of-service in probe packets (default 0)
    -w SEC  Time wait for a response (default 3)
```

#### true
#### tx99tool

```
usage: tx99tool wifi0 [start|stop|set]
usage: tx99tool wifi0 set [freq||bandwidth|htext|rate|txchain|type|pwr|txmode|testmode]
```

#### ubiattach

```
ubiattach version 1.5.2 - a tool to attach MTD device to UBI.

Usage: ubiattach [<UBI control device node file name>]
        [-m <MTD device number>] [-d <UBI device number>] [-p <path to device>]
        [--mtdn=<MTD device number>] [--devn=<UBI device number>]
        [--dev-path=<path to device>]
        [--max-beb-per1024=<maximum bad block number per 1024 blocks>]

UBI control device defaults to /dev/ubi_ctrl if not supplied.

Example 1: ubiattach -p /dev/mtd0 - attach /dev/mtd0 to UBI
Example 2: ubiattach -m 0 - attach MTD device 0 (mtd0) to UBI
Example 3: ubiattach -m 0 -d 3 - attach MTD device 0 (mtd0) to UBI
           and create UBI device number 3 (ubi3)
Example 4: ubiattach -m 1 -b 25 - attach /dev/mtd1 to UBI and reserve
           25*C/1024 eraseblocks for bad block handling, where C is the flash
           is total flash chip eraseblocks count, that is flash chip size in
           eraseblocks (including bad eraseblocks). E.g., if the flash chip
           has 4096 PEBs, 100 will be reserved.

    -d, --devn=<number>   the number to assign to the newly created UBI device
                          (assigned automatically if this is not specified)
    -p, --dev-path=<path> path to MTD device node to attach
    -m, --mtdn=<number>   MTD device number to attach (alternative method, e.g
                          if the character device node does not exist)
    -O, --vid-hdr-offset  VID header offset (do not specify this unless you really
                          know what you are doing, the default should be optimal)
    -b, --max-beb-per1024 maximum expected bad block number per 1024 eraseblock.
                          The default value is correct for most NAND devices.
                          Allowed range is 0-768, 0 means the default kernel value.
    -h, --help            print help message
    -V, --version         print program version
```

#### ubiblock

```
ubiblock version 1.5.2 - a tool to create/remove block device interface from UBI volumes.

Usage: ubiblock [-c,-r] <UBI volume node file name>
Example: ubiblock --create /dev/ubi0_0

-c, --create               create block on top of a volume
-r, --remove               remove block from volume
-h, --help                 print help message
-V, --version              print program version
```

#### ubicrc32

```
ubicrc32 version 1.5.2 - a tool to calculate CRC32 with UBI start value (0xFFFFFFFF)

Usage: ubicrc32 <file to calculate CRC32 for> [-h] [--help]

    -h, --help                    print help message
    -V, --version                 print program version
```

#### ubidetach

```
ubidetach version 1.5.2 - tool to remove UBI devices (detach MTD devices from UBI)

Usage: ubidetach [<UBI control device node file name>]
        [-d <UBI device number>] [-m <MTD device number>] [-p <path to device>]
        [--devn=<UBI device number>] [--mtdn=<MTD device number>]
        [--dev-path=<path to device>]

UBI control device defaults to /dev/ubi_ctrl if not supplied.

Example 1: ubidetach -p /dev/mtd0 - detach MTD device /dev/mtd0
Example 2: ubidetach -d 2 - delete UBI device 2 (ubi2)
Example 3: ubidetach -m 0 - detach MTD device 0 (mtd0)

    -d, --devn=<UBI device number>  UBI device number to delete
    -p, --dev-path=<path to device> or alternatively, MTD device node path to detach
    -m, --mtdn=<MTD device number>  or alternatively, MTD device number to detach
    -h, --help                      print help message
    -V, --version                   print program version
```

#### ubiformat

```
ubiformat version 1.5.2 - a tool to format MTD devices and flash UBI images

Usage: ubiformat <MTD device node file name> [-s <bytes>] [-O <offs>] [-n]
                [-Q <num>] [-f <file>] [-S <bytes>] [-e <value>] [-x <num>] [-y] [-q] [-v] [-h]
                [--sub-page-size=<bytes>] [--vid-hdr-offset=<offs>] [--no-volume-table]
                [--flash-image=<file>] [--image-size=<bytes>] [--erase-counter=<value>]
                [--image-seq=<num>] [--ubi-ver=<num>] [--yes] [--quiet] [--verbose]
                [--help] [--version]

Example 1: ubiformat /dev/mtd0 -y - format MTD device number 0 and do
           not ask questions.
Example 2: ubiformat /dev/mtd0 -q -e 0 - format MTD device number 0,
           be quiet and force erase counter value 0.

    -s, --sub-page-size=<bytes>  minimum input/output unit used for UBI
                                 headers, e.g. sub-page size in case of NAND
                                 flash (equivalent to the minimum input/output
                                 unit size by default)
    -O, --vid-hdr-offset=<offs>  offset if the VID header from start of the
                                 physical eraseblock (default is the next
                                 minimum I/O unit or sub-page after the EC
                                 header)
    -n, --no-volume-table        only erase all eraseblock and preserve erase
                                 counters, do not write empty volume table
    -f, --flash-image=<file>     flash image file, or '-' for stdin
    -S, --image-size=<bytes>     bytes in input, if not reading from file
    -e, --erase-counter=<value>  use <value> as the erase counter value for all
                                 eraseblocks
    -x, --ubi-ver=<num>          UBI version number to put to EC headers
                                 (default is 1)
    -Q, --image-seq=<num>        32-bit UBI image sequence number to use
                                 (by default a random number is picked)
    -y, --yes                    assume the answer is "yes" for all question
                                 this program would otherwise ask
    -q, --quiet                  suppress progress percentage information
    -v, --verbose                be verbose
    -h, -?, --help               print help message
    -V, --version                print program version
```

#### ubimkvol

```
ubimkvol version 1.5.2 - a tool to create UBI volumes.

Usage: ubimkvol <UBI device node file name> [-h] [-a <alignment>] [-n <volume ID>] [-N <name>]
                        [-s <bytes>] [-S <LEBs>] [-t <static|dynamic>] [-V] [-m]
                        [--alignment=<alignment>][--vol_id=<volume ID>] [--name=<name>]
                        [--size=<bytes>] [--lebs=<LEBs>] [--type=<static|dynamic>] [--help]
                        [--version] [--maxavsize]

Example: ubimkvol /dev/ubi0 -s 20MiB -N config_data - create a 20 Megabytes volume
         named "config_data" on UBI device /dev/ubi0.

    -a, --alignment=<alignment>   volume alignment (default is 1)
    -n, --vol_id=<volume ID>      UBI volume ID, if not specified, the volume ID
                                  will be assigned automatically
    -N, --name=<name>             volume name
    -s, --size=<bytes>            volume size volume size in bytes, kilobytes (KiB)
                                  or megabytes (MiB)
    -S, --lebs=<LEBs count>       alternative way to give volume size in logical
                                  eraseblocks
    -m, --maxavsize               set volume size to maximum available size
    -t, --type=<static|dynamic>   volume type (dynamic, static), default is dynamic
    -h, -?, --help                print help message
    -V, --version                 print program version
```

#### ubinfo

```
ubinfo version 1.5.2 - a tool to print UBI information.

Usage 1: ubinfo [-d <UBI device number>] [-n <volume ID> | -N <volume name>] [-a] [-h] [-V]
                [--vol_id=<volume ID> | --name <volume name>] [--devn <UBI device number>] [--all] [--help] [--version]
Usage 2: ubinfo <UBI device node file name> [-a] [-h] [-V] [--all] [--help] [--version]
Usage 3: ubinfo <UBI volume node file name> [-h] [-V] [--help] [--version]

Example 1: ubinfo - (no arguments) print general UBI information
Example 2: ubinfo -d 1 - print information about UBI device number 1
Example 3: ubinfo /dev/ubi0 -a - print information about all volumes of UBI
           device /dev/ubi0
Example 4: ubinfo /dev/ubi1_0 - print information about UBI volume /dev/ubi1_0
Example 5: ubinfo -a - print all information


    -d, --devn=<UBI device number>  UBI device number to get information about
    -n, --vol_id=<volume ID>        ID of UBI volume to print information about
    -N, --name=<volume name>        name of UBI volume to print information about
    -a, --all                       print information about all devices and volumes,
                                    or about all volumes if the UBI device was
                                    specified
    -h, --help                      print help message
    -V, --version                   print program version
```

#### ubinize

```
ubinize version 1.5.2 - a tool to generate UBI images. An UBI image may contain
one or more UBI volumes which have to be defined in the input configuration
ini-file. The ini file defines all the UBI volumes - their characteristics and
the contents, but it does not define the characteristics of the flash the UBI
image is generated for. Instead, the flash characteristics are defined via the
command-line options. Note, if not sure about some of the command-line
parameters, do not specify them and let the utility use default values.

INI-file format.
The input configuration ini-file describes all the volumes which have to
be included to the output UBI image. Each volume is described in its own
section which may be named arbitrarily. The section consists on
"key=value" pairs, for example:

[jffs2-volume]
mode=ubi
image=../jffs2.img
vol_id=1
vol_size=30MiB
vol_type=dynamic
vol_name=jffs2_volume
vol_flags=autoresize
vol_alignment=1

This example configuration file tells the utility to create an UBI image
with one volume with ID 1, volume size 30MiB, the volume is dynamic, has
name "jffs2_volume", "autoresize" volume flag, and alignment 1. The
"image=../jffs2.img" line tells the utility to take the contents of the
volume from the "../jffs2.img" file. The size of the image file has to be
less or equivalent to the volume size (30MiB). The "mode=ubi" line is
mandatory and just tells that the section describes an UBI volume - other
section modes may be added in the future.

Notes:
  * size in vol_size might be specified kilobytes (KiB), megabytes (MiB),
    gigabytes (GiB) or bytes (no modifier);
  * if "vol_size" key is absent, the volume size is assumed to be
    equivalent to the size of the image file (defined by "image" key);
  * if the "image" is absent, the volume is assumed to be empty;
  * volume alignment must not be greater than the logical eraseblock size;
  * one ini file may contain arbitrary number of sections, the utility will
    put all the volumes which are described by these section to the output
    UBI image file.

Usage: ubinize [-o filename] [-p <bytes>] [-m <bytes>] [-s <bytes>] [-O <num>] [-e <num>]
                [-x <num>] [-Q <num>] [-v] [-h] [-V] [--output=<filename>] [--peb-size=<bytes>]
                [--min-io-size=<bytes>] [--sub-page-size=<bytes>] [--vid-hdr-offset=<num>]
                [--erase-counter=<num>] [--ubi-ver=<num>] [--image-seq=<num>] [--verbose] [--help]
                [--version] ini-file

Example: ubinize -o ubi.img -p 16KiB -m 512 -s 256 cfg.ini - create UBI image
         'ubi.img' as described by configuration file 'cfg.ini'

    -o, --output=<file name>     output file name
    -p, --peb-size=<bytes>       size of the physical eraseblock of the flash
                                 this UBI image is created for in bytes,
                                 kilobytes (KiB), or megabytes (MiB)
                                 (mandatory parameter)
    -m, --min-io-size=<bytes>    minimum input/output unit size of the flash
                                 in bytes
    -s, --sub-page-size=<bytes>  minimum input/output unit used for UBI
                                 headers, e.g. sub-page size in case of NAND
                                 flash (equivalent to the minimum input/output
                                 unit size by default)
    -O, --vid-hdr-offset=<num>   offset if the VID header from start of the
                                 physical eraseblock (default is the next
                                 minimum I/O unit or sub-page after the EC
                                 header)
    -e, --erase-counter=<num>    the erase counter value to put to EC headers
                                 (default is 0)
    -x, --ubi-ver=<num>          UBI version number to put to EC headers
                                 (default is 1)
    -Q, --image-seq=<num>        32-bit UBI image sequence number to use
                                 (by default a random number is picked)
    -v, --verbose                be verbose
    -h, --help                   print help message
    -V, --version                print program version
```

#### ubirename

```
Usage: ubirename <UBI device node file name> [<old name> <new name>|...]

Example: ubirename/dev/ubi0 A B C D - rename volume A to B, and C to D

This utility allows re-naming several volumes in one go atomically.
For example, if you have volumes A and B, then you may rename A into B
and B into A at one go, and the operation will be atomic. This allows
implementing atomic UBI volumes upgrades. E.g., if you have volume A
and want to upgrade it atomically, you create a temporary volume B,
put your new data to B, then rename A to B and B to A, and then you
may remove old volume B.
It is also allowed to re-name multiple volumes at a time, but 16 max.
renames at once, which means you may specify up to 32 volume names.
If you have volumes A and B, and re-name A to B, bud do not re-name
B to something else in the same request, old volume B will be removed
and A will be renamed into B.
```

#### ubirmvol

```
ubirmvol version 1.5.2 - a tool to remove UBI volumes.

Usage: ubirmvol <UBI device node file name> [-n <volume id>] [--vol_id=<volume id>]

        [-N <volume name>] [--name=<volume name>] [-h] [--help]

Example: ubirmvol /dev/ubi0 -n 1 - remove UBI volume 1 from UBI device corresponding
         to /dev/ubi0
         ubirmvol /dev/ubi0 -N my_vol - remove UBI named "my_vol" from UBI device
         corresponding to /dev/ubi0

    -n, --vol_id=<volume id>   volume ID to remove
    -N, --name=<volume name>   volume name to remove
    -h, -?, --help             print help message
    -V, --version              print program version
```

#### ubirsvol

```
ubirsvol version 1.5.2 - a tool to resize UBI volumes.

Usage: ubirsvol <UBI device node file name> [-n <volume id>] [--vol_id=<volume id>]

        [-N <volume name>] [--name=<volume name>] [-s <bytes>] [-S <LEBs>] [-h] [--help]

Example: ubirsvol /dev/ubi0 -n 1 -s 1MiB resize UBI volume 1 to 1 MiB on
        UBI device corresponding to /dev/ubi0
        ubirsvol /dev/ubi0 -N my_vol -s 1MiB - resize UBI volume named "my_vol" to 1 MiB
            on UBI device corresponding to /dev/ubi0

    -n, --vol_id=<volume id>   volume ID to resize
    -N, --name=<volume name>   volume name to resize
    -s, --size=<bytes>         volume size volume size in bytes, kilobytes (KiB)
                               or megabytes (MiB)
    -S, --lebs=<LEBs count>    alternative way to give volume size in logical
                               eraseblocks
    -h, -?, --help             print help message
    -V, --version              print program version
```

#### ubiupdatevol

```
ubiupdatevol version 1.5.2 - a tool to write data to UBI volumes.

Usage: ubiupdatevol <UBI volume node file name> [-t] [-s <size>] [-h] [-V] [--truncate]
                        [--size=<size>] [--help] [--version] <image file>

Example 1: ubiupdatevol /dev/ubi0_1 fs.img - write file "fs.img" to UBI volume /dev/ubi0_1
Example 2: ubiupdatevol /dev/ubi0_1 -t - wipe out UBI volume /dev/ubi0_1

    -t, --truncate             truncate volume (wipe it out)
    -s, --size=<bytes>         bytes to read from input
        --skip=<bytes>         leading bytes to skip from input
    -h, --help                 print help message
    -V, --version              print program version
```

#### ubnt-fanctrl

```
Usage: ubnt-fanctrl [-b] [-v] [-c config] [-h]

    -b, --background    Run in background
    -v, --verbose       Enable verbose output to console instead of log
    -c, --config path   Use specified configuration file at 'path'
    -h, --help          Show this help message and exit
```

#### ubnt-netmon

```
ubnt-netmon - usage

    -c file  : load a configuration (json)
    -h       : print this help message
    -v       : verbose - print out status info
    -d       : output to stdout instead of syslog
    -t       : track - track devices as info instead of debug
    -q       : No longer run as dnsmasq; now test and log
```

#### ubnt-regdomain

```
usage: ubnt-regdomain [options] [cc | rd]

Available options:
    -h - Help
    -c - display Channel numbers
    -C - Format output like the Linux db.txt
    -f - display Frequencies
    -i - display Indoor channels
    -o - display Outdoor channels
    -d - Debug output
    -e - Extended channel info
    -j - Javascript addons
    -l - List country and regulatory domain codes
    -L - List countries
    -m - Mode <sta|ibss|adhoc|ap|hostap|monitor>
    -p - Passive channels
    -q - Query for all AP models
    -v - verbose - make logging more detailed
    -w - clock selection <0|1|2|3>
    -s - channel Shifting <0..40>
    -a - All channels
    -A - 11A channels
    -B - 11B channels
    -G - 11G channels
    -P - PSC channels only (6g frequencies)
    -T - 11a Turbo  channels
    -S - SuperG channels
    -X - 802.11ax channels
    -Z - include normally excluded channels
    -6 - 6Ghz extended channels
    -y - can provision channels with provided filters; returns 1 (allowed) or 0 (not allowed)
    -r - display obey (strict) regulatory requirements
```

#### ubnt-rssimon

```
Usage: ubntbox <tool>

Supported tools:

    ubntconf
    cfgmtd
    fwupdate.real
    factorytest
    nettool
    bgnd
    ubntevent
    wevent
    vwirectl
    utermd
    oopsdump
    ubnt-gps-reader
    ubnt-netmon
    stahtd
    ramdump
    selfupgrade
    autohsr
```

#### ubntbox

```
Usage: ubntbox <tool>

Supported tools:
    ubntconf
    cfgmtd
    fwupdate.real
    factorytest
    nettool
    bgnd
    ubntevent
    wevent
    vwirectl
    utermd
    oopsdump
    ubnt-gps-reader
    ubnt-netmon
    stahtd
    ramdump
    selfupgrade
    autohsr
```

#### ubntconf

```
Usage: ubntconf [options]
    -c <config file>        - Configuration file to use. (Default: /tmp/system.cfg)
    -p <config file>        - Previous config file to differ with file specified in -c option. (Default: none)
    -d <file name>          - File name for script generated from the diff. (Default: none)
    -m                      - Only run minimal set of plugins required to init system.
    -o <output directory>   - Directory to output scripts. (Default: /etc/sysinit)
    -s <startup_list>       - Output file for plugins started. (Default: /etc/startup.list)
    -i <symlink>            - Create Symlink to default configuration file.
    -b                      - Detect the system and store in /etc/board.info
    -t                      - Print configuration
    -v                      - Increase verbosity
    -h                      - This message.
```

#### ubntevent
#### ubntrfclient
#### ubus
#### ubusd
#### udevtrigger
#### udhcpc
#### udhcpc6
#### umount
#### uname
#### unifi_util_funcs.sh
#### uniq
#### unsquashfs4
#### unxz
#### uplink-monitor
#### uptime
#### urandom_seed
#### usign
#### utermd
#### validate_data
#### vconfig
#### vi
#### vwirectl
#### walled_action.sh
#### wc
#### wevent
#### which
#### wifi
#### wifi_hw_mode
#### wifi_try
#### wifistate
#### wifitelemetry
#### wifitool

```
usage: wifitool athX cmd args

cmd: fips        args: interface_name input_file
        Input file format: Each set of inputs seperated by newline
        <FIPS Command> <MODE> <Key length> <Input Data Length> <Key> <Input Data> <Expected Output> <IV with 16 bytes><newline>      Example: wifitool ath0 fips input_file

Refer README_FIPS in drivers/wlan_modules/os/linux/tools

cmd: [sendaddba senddelba setaddbaresp getaddbastats sendaddts senddelts refusealladdbas]
cmd: [sendstastats sendchload sendnhist sendlcireq rrmstats bcnrpt setchanlist getchanlist]
cmd: [sendtsmrpt sendneigrpt sendlmreq sendbstmreq  sendbcnrpt sendcca sendrpihist]
cmd: [block_acs_channel]
cmd: [acs_chan_weightage]
cmd: [unblock_acs_channel]
cmd: [getblockchanlist]
cmd: [block_acs_retain]
cmd: [rrm_sta_list]
cmd: [btm_sta_list]
cmd: [mu_scan lteu_cfg ap_scan]
cmd: [atf_debug_size atf_dump_debug]
cmd: [atf_debug_nodestate]
cmd: [tr069_get_vap_stats]
cmd: [tr069_chanhist]
cmd: [tr069_chan_inuse]
cmd: [tr069_set_oper_rate]
cmd: [tr069_get_oper_rate]
cmd: [tr069_get_posiblrate]
cmd: [chmask_persta]
cmd: [peer_nss]
cmd: [frame_injector_en]
cmd: [beeliner_fw_test]
cmd: [init_rtt3]
cmd: [bsteer_getparams bsteer_setparams]
cmd: [bsteer_getdbgparams bsteer_setdbgparams]
cmd: [bsteer_enable] [bsteer_enable_events]
cmd: [bsteer_getoverload bsteer_setoverload]
cmd: [bsteer_getrssi]
cmd: [bsteer_setproberespwh bsteer_getproberespwh]
cmd: [bsteer_setauthallow]
cmd: [set_antenna_switch]
cmd: [set_usr_ctrl_tbl]
cmd: [offchan_tx_test]
cmd: [offchan_rx_test]
cmd: [sendbstmreq sendbstmreq_target]
cmd: [sendmscsresp]
cmd: [bsteer_getdatarateinfo]
cmd: [tr069_get_fail_retrans]
cmd: [tr069_get_success_retrans]
cmd: [tr069_get_success_mul_retrans]
cmd: [tr069_get_ack_failures]
cmd: [tr069_get_retrans]
cmd: [tr069_get_aggr_pkts]
cmd: [tr069_get_sta_stats] [STA MAC]
cmd: [tr069_get_sta_bytes_sent] [STA MAC]
cmd: [tr069_get_sta_bytes_rcvd] [STA MAC]
cmd: [bsteer_setsteering]
cmd: [custom_chan_list]
cmd: [vow_debug_set_param]
cmd: [vow_debug]
cmd: [setUnitTestCmd]
cmd: [setUnitTestCmdEvent]
cmd: [softblocking] [STA MAC] [0/1]
cmd: [softblocking_get] [STA MAC]
cmd: [ap_twt_enable]
cmd: [ap_twt_add_dialog]
cmd: [ap_twt_del_dialog]
cmd: [ap_twt_pause_dialog]
cmd: [ap_twt_resume_dialog]
cmd: [ap_twt_btwt_invite_sta]
cmd: [ap_twt_btwt_remove_sta]
cmd: [bsscolor_collision_ap_period]
cmd: [bsscolor_color_change_announcemt_count]
cmd: [get_chan_survey]
cmd: [get_scan_chan_util]
cmd: [reset_chan_survey]
cmd: [add_tpe]
cmd: [peer_latency_param_config]
cmd: [get_scan_spcl_vap_stats]
cmd: [set_wfa_test_param]
cmd: [trigger_txbf_sounding]
cmd: [get_triggered_fb_type]
main:11225
```

#### wlanconfig

```
usage: wlanconfig athX create wlandev wifiX
                  wlanmode [sta|adhoc|ap|monitor|wrap|p2pgo|p2pcli|p2pdev|specialvap|smart_monitor|lp_iot_mode]
                  [wlanaddr <mac_addr>] [mataddr <mac_addr>] [bssid|-bssid] [vapid <0-15>] [nosbeacon] [ppe_vp <0-3>]
usage: wlanconfig athX destroy
usage: wlanconfig athX nawds mode (0-4)
usage: wlanconfig athX nawds defcaps CAPS [PP]
usage: wlanconfig athX nawds override (0-1)
usage: wlanconfig athX nawds add-repeater MAC (0-1) [PP]
usage: wlanconfig athX nawds del-repeater MAC
usage: wlanconfig athX nawds list
usage: wlanconfig athX mlnawds <mld_mac> mode (0-2)
usage: wlanconfig athX mlnawds add-repeater <self_link_mac> <peer_nawds_mld_mac> <peer_nawds_link_mac> <CAPS> <PP> <link_id>
usage: wlanconfig athX mlnawds del-repeater <peer_nawds_mld_mac>
usage: wlanconfig athX mlnawds <mld_mac> override (0-1)
usage: wlanconfig athX mlnawds list
usage: wlanconfig athX mlnawds start <peer_nawds_mld_mac>
usage: wlanconfig athX hmwds add-addr wds_ni_macaddr wds_macaddr
usage: wlanconfig athX hmwds reset-addr macaddr
usage: wlanconfig athX hmwds reset-table
usage: wlanconfig athX hmwds read-addr wds_ni_macaddr
usage: wlanconfig athX hmwds dump-wdstable
usage: wlanconfig athX hmwds read-table
usage: wlanconfig athX hmwds rem-addr <mac_addr>
usage: wlanconfig athX ald sta-enable <sta_mac_addr> <0/1>
usage: wlanconfig athX hmmc add ip mask
usage: wlanconfig athX hmmc del ip mask
usage: wlanconfig athX hmmc dump
usage: wlanconfig athX deny_list add ip mask
usage: wlanconfig athX deny_list del ip mask
usage: wlanconfig athX deny_list dump
usage: wlanconfig athX hmmc_v6 add ip prefix
usage: wlanconfig athX hmmc_v6 del ip prefix
usage: wlanconfig athX hmmc_v6 dump
usage: wlanconfig athX deny_list_v6 add ip prefix
usage: wlanconfig athX deny_list_v6 del ip prefix
usage: wlanconfig athX deny_list_v6 dump
usage: wlanconfig athX wnm setbssmax <idle period in seconds> [<idle option>]
usage: wlanconfig athX wnm getbssmax
usage: wlanconfig athX wnm tfsreq <filename>
usage: wlanconfig athX wnm deltfs
usage: wlanconfig athX wnm timintvl <Interval>
usage: wlanconfig athX wnm gettimparams
usage: wlanconfig athX wnm timrate <highrateEnable> <lowRateEnable>
usage: wlanconfig athX wnm bssterm <delay in TBTT> [<duration in minutes>]
usage: wlanconfig athX addssid ssidname per_value(0--100)
usage: wlanconfig athX addsta  macaddr(example:112233445566) per_value(0--100)
usage: wlanconfig athX delssid ssidname
usage: wlanconfig athX delsta  macaddr
usage: wlanconfig athX showatftable [show_per_peer_table<1>]
usage: wlanconfig athX showairtime
usage: wlanconfig athX flushatftable
usage: wlanconfig athX addatfgroup groupname ssid
usage: wlanconfig athX configatfgroup groupname value (0 - 100)
usage: wlanconfig athX atfgroupsched <groupname> <group_scheduling_policy>
       group_scheduling_policy : 0 - Fair, 1 - Strict, 2 - Fair with UB
usage: wlanconfig athX delatfgroup groupname
usage: wlanconfig athX showatfgroup
usage: wlanconfig athX addtputsta macaddr tput airtime(opt)
usage: wlanconfig athX deltputsta macaddr
usage: wlanconfig athX showtputtbl
usage: wlanconfig athX atfstat
usage: wlanconfig athX atfaddac <ssid/groupname> <ac_name>:<val> <ac_name>:<val> <ac_name>:<val> <ac_name>:<val>
       ac_name: BE,BK,VI,VO
       val: 0 - 100
usage: wlanconfig athX atfdelac <ssid/groupname> <ac_name> <ac_name> <ac_name> <ac_name>
       ac_name: BE,BK,VI,VO
usage: wlanconfig athX showatfsubgroup
usage: wlanconfig athX showatfstats
usage: wlanconfig athX showatfacstats
usage: wlanconfig athX vendorie add len <oui+pcap_data in bytes> oui <eg:xxxxxx> pcap_data <eg:xxxxxxxx> ftype_map <eg:xx>
usage: wlanconfig athX vendorie update len <oui+pcap_data in bytes> oui <eg:xxxxxx> pcap_data <eg:xxxxxxxx> ftype_map <eg:xx>
usage: wlanconfig athX vendorie remove len <oui+pcap_data in bytes> oui <eg:xxxxxx> pcap_data <eg:xx>
usage: wlanconfig athX vendorie list
usage: wlanconfig athX vendorie list len <oui in bytes> oui <eg:xxxxxx>
usage: wlanconfig athX addie ftype <frame type> len < data len> data <data>
       ftype: 0/2/4('0'-Beacon,'2'-Probe Resp,'4'-Assoc Resp)
       len: Data length(IE length + 2)
       data: Data(in hex)
usage: wlanconfig athX nac add/del bssid <ad1 eg: xx:xx:xx:xx:xx:xx> <ad2> <ad3> ... <ad8>
usage: wlanconfig athX nac add/del client <ad1 eg: xx:xx:xx:xx:xx:xx> <ad2> <ad3> <ad4> <ad5>  <ad6> <ad7>  <ad8> ... <ad24>
usage: wlanconfig athX nac list bssid/client
usage: wlanconfig athX peer_isolation add <addr eg: xx:xx:xx:xx:xx:xx>
usage: wlanconfig athX peer_isolation del <addr eg: xx:xx:xx:xx:xx:xx>
usage: wlanconfig athX peer_isolation list
usage: wlanconfig athX peer_isolation flush
                  wlanmode [sta|adhoc|ap|monitor|wrap|p2pgo|p2pcli|p2pdev|specialvap|mesh|smart_monitor|lp_iot_mode]
                  [wlanaddr <mac_addr>] [mataddr <mac_addr>] [bssid|-bssid] [vapid <0-15>] [nosbeacon]
wlanconfig athX cfr start <peer MAC> <bw> <periodicity> <capture type>
wlanconfig athX cfr stop <peer MAC>
wlanconfig athX cfr list
wlanconfig athx cfr m_ta_ra_filter <enable/disable>
wlanconfig athx cfr m_directed_ndpa_ndp <enable/disable>
wlanconfig athx cfr m_ndpa_ndp_all <enable/disable>
wlanconfig athx cfr disable_all
wlanconfig athx cfr ta_ra_addr <group_id> <ta> <ta_mask> <ra> <ra_mask>
wlanconfig athx cfr bw_nss <group_id> <bw> <nss>
wlanconfig athx cfr subtype <group_id> <mgmt> <ctrl> <data>
wlanconfig athx cfr en_cfg <bitmask>
wlanconfig athx cfr reset_cfg <bitmask>
wlanconfig athx cfr capture_dur <value>
wlanconfig athx cfr capture_intval <value>
wlanconfig athx cfr ul_mu_user_mask <mask_lower_32> <mask_upper_32>
wlanconfig athx cfr freeze_tlv_delay_cnt <freeze_tlv_delay_cnt_en> <threshold>
wlanconfig athx cfr commit
wlanconfig athx cfr rcc_config_details
wlanconfig athx cfr rcc_debug_counters
wlanconfig athx cfr clr_dbg_counters
wlanconfig athx cfr rcc_dump_lut
wlanconfig athx cfr capture_count <16 bit count_value>
wlanconfig athx cfr capture_intervalmode_sel <value 0:duration mode 1:count mode>
wlanconfig wifix service_class create <service_id> <app_name> <min_thruput_rate> <max_thruput_rate> <burst_size> <service_interval> <delay_bound> <msdu_ttl> <priority> <tid> <msdu_rate_loss> <ul_burst_size> <ul_service_interval> <dl_disabled_mode> <ul_disabled_mode> <ul_min_tput> <ul_max_latency>
 wlanconfig wifix service_class disable <service_id>
 wlanconfig wifix service_class view
 wlanconfig wifix sawf_telemetry <mv_avg_pkt> <mv_avg_window> <sla_num_pkt> <sla_time_sec>
usage: wlanconfig wifiX rx_flow_tag_op <opcode> <ipversion> <source_ip> <dest_ip> <src_port> <dest_port> <L4_protocol_num> <tag>
wlanconfig athx rtt lcr <Country code string> <civic info>
wlanconfig athx rtt lci <latitude> <longitude> <altitude> <latitude_unc> <longitude_unc> <altitude_unc> <motion_pattern> <floor> <height_above_floor> <height_unc>
wlanconfig athx rtt ftmrr <STA MAC_addr> <random_interval> <num_elements> [<BSSID> <BSSID info> <channel number> <center_ch1> <center_ch2> <chwidth> <opclass> <phytype>] [...]
usage: wlanconfig athx mu_snif <mode> <max_user> <aid0> <aid1> <aid2> <aid3>
       mode: dis,match,wildcard
       max_user: 1 - 4 (max mu user to sniff)
wlanconfig athX t2lm_test_cmd request assoc_frm <1/0> peer_mld_mac <peer MLD macaddr> dir <direction> default_mapping <default mapping> link_mapping_size <size> num_tids <num_tids> <TID0> <TID0_link_map> <TID1> <TID1_link_map> [dir <direction> ...]
wlanconfig athX t2lm_test_cmd response assoc_frm <1/0> peer_mld_mac <peer MLD macaddr> status <status> unsolicited_t2lm_resp <unsolicited T2LM response> [dir <direction> default_mapping <default mapping> link_mapping_size <size> num_tids <num_tids> <TID0> <TID0_link_map> <TID1> <TID1_link_map> [dir <direction> ...]
wlanconfig athX t2lm_test_cmd teardown peer_mld_mac <peer MLD macaddr>
wlanconfig athX link_map_config_test_cmd ieee_link_map <ieee_link_map_values> map_switch_time <map_switch_time> expected_dur <expected_dur> link_mapping_size <size>
wlanconfig wifiX link_map_config_test_cmd ieee_link_map <ieee_link_map_values> map_switch_time <map_switch_time> expected_dur <expected_dur> link_mapping_size <size>
wlanconfig wifiX tdma_test_cmd sched_type <value> is_last_schedule <value> sched_id <value> bssid <macaddr> start_time_tsf_low <value> start_time_tsf_high <value> num_busy_slots <value> busy_slot_dur_ms <value> busy_slot_intvl_ms <value> edca_params_valid <value> aifsn <val0> <val1> <val2> <val3> cwmin <val0> <val1> <val2> <val3> cwmax <val0> <val1> <val2> <val3>
```

#### wlanfw-upgrade.sh
#### wpa_cli

```
wpa_cli [-p<path to ctrl sockets>] [-i<ifname>] [-hvBr] [-a<action file>] \
        [-P<pid file>] [-g<global ctrl>] [-G<ping interval>] \
        [-s<wpa_client_socket_file_path>] [command..]
  -h = help (show this usage text)
  -v = shown version information
  -a = run in daemon mode executing the action file based on events from
       wpa_supplicant
  -r = try to reconnect when client socket is disconnected.
       This is useful only when used with -a.
  -B = run a daemon in the background
  default path: /var/run/wpa_supplicant
  default interface: first interface found in socket path

commands:
  status [verbose] = get current WPA/EAPOL/EAP status
  ifname = get current interface name
  ping = pings wpa_supplicant
  relog = re-open log-file (allow rolling logs)
  note <text> = add a note to wpa_supplicant debug log
  mib = get MIB variables (dot1x, dot11)
  help [command] = show usage help
  interface [ifname] = show interfaces/select interface
  level <debug level> = change debug level
  license = show full wpa_cli license
  quit = exit wpa_cli
  set = set variables (shows list of variables when run without arguments)
  dump = dump config variables
  get <name> = get information
  driver_flags = list driver flags
  logon = IEEE 802.1X EAPOL state machine logon
  logoff = IEEE 802.1X EAPOL state machine logoff
  pmksa = show PMKSA cache
  pmksa_flush = flush PMKSA cache entries
  pmksa_get <network_id> = fetch all stored PMKSA cache entries
  pmksa_add <network_id> <BSSID> <PMKID> <PMK> <reauth_time in seconds> <expiration in seconds> <akmp> <opportunistic> = store PMKSA cache entry from external storage
  reassociate = force reassociation
  reattach = force reassociation back to the same BSS
  preauthenticate <BSSID> = force preauthentication
  identity <network id> <identity> = configure identity for an SSID
  password <network id> <password> = configure password for an SSID
  new_password <network id> <password> = change password for an SSID
  pin <network id> <pin> = configure pin for an SSID
  otp <network id> <password> = configure one-time-password for an SSID
  psk_passphrase <network id> <PSK/passphrase> = configure PSK/passphrase for an SSID
  passphrase <network id> <passphrase> = configure private key passphrase
    for an SSID
  sim <network id> <pin> = report SIM operation result
  preferred_ap_mld_addr <network id> <PREFERRED_AP_MLD_ADDR> = set preferred
   AP MLD addr for an SSID
  bssid <network id> <BSSID> = set preferred BSSID for an SSID
  bssid_ignore <BSSID> = add a BSSID to the list of temporarily ignored BSSs
  bssid_ignore clear = clear the list of temporarily ignored BSSIDs
  bssid_ignore = display the list of temporarily ignored BSSIDs
  blacklist = deprecated alias for bssid_ignore
  log_level <level> [<timestamp>] = update the log level/timestamp
  log_level = display the current log level and log options
  list_networks = list configured networks
  select_network <network id> = select a network (disable others)
  enable_network <network id> = enable a network
  disable_network <network id> = disable a network
  add_network = add a network
  remove_network <network id> = remove a network
  set_network <network id> <variable> <value> = set network variables (shows
    list of variables when run without arguments)
  get_network <network id> <variable> = get network variables
  dup_network <src network id> <dst network id> <variable> = duplicate network variables
  list_creds = list configured credentials
  add_cred = add a credential
  remove_cred <cred id> = remove a credential
  set_cred <cred id> <variable> <value> = set credential variables
  get_cred <cred id> <variable> = get credential variables
  save_config = save the current configuration
  disconnect = disconnect and wait for reassociate/reconnect command before
    connecting
  reconnect = like reassociate, but only takes effect if already disconnected
  scan = request new BSS scan
  scan_results = get latest scan results
  abort_scan = request ongoing scan to be aborted
  bss <<idx> | <bssid>> = get detailed scan result info
  get_capability <eap/pairwise/group/key_mgmt/proto/auth_alg/channels/freq/modes> = get capabilities
  reconfigure = force wpa_supplicant to re-read its configuration file
  terminate = terminate wpa_supplicant
  interface_add <ifname> <confname> <driver> <ctrl_interface> <driver_param>
    <bridge_name> <create> <type> = adds new interface, all parameters but
    <ifname> are optional. Supported types are station ('sta') and AP ('ap')
  interface_remove <ifname> = removes the interface
  interface_list = list available interfaces
  ap_scan <value> = set ap_scan parameter
  scan_interval <value> = set scan_interval parameter (in seconds)
  bss_expire_age <value> = set BSS expiration age parameter
  bss_expire_count <value> = set BSS expiration scan count parameter
  bss_flush <value> = set BSS flush age (0 by default)
  ft_ds <addr> = request over-the-DS FT with <addr>
  get_pmk get_pmk
  get_ptk get_ptk
  wps_pbc [BSSID] = start Wi-Fi Protected Setup: Push Button Configuration
  wps_pin <BSSID> [PIN] = start WPS PIN method (returns PIN, if not hardcoded)
  wps_check_pin <PIN> = verify PIN checksum
  wps_cancel Cancels the pending WPS operation
  wps_reg <BSSID> <AP PIN> = start WPS Registrar to configure an AP
  wps_ap_pin [params..] = enable/disable AP PIN
  wps_er_start [IP address] = start Wi-Fi Protected Setup External Registrar
  wps_er_stop = stop Wi-Fi Protected Setup External Registrar
  wps_er_pin <UUID> <PIN> = add an Enrollee PIN to External Registrar
  wps_er_pbc <UUID> = accept an Enrollee PBC using External Registrar
  wps_er_learn <UUID> <PIN> = learn AP configuration
  wps_er_set_config <UUID> <network id> = set AP configuration for enrolling
  wps_er_config <UUID> <PIN> <SSID> <auth> <encr> <key> = configure AP
  ibss_rsn <addr> = request RSN authentication with <addr> in IBSS
  sta <addr> = get information about an associated station (AP)
  all_sta = get information about all associated stations (AP)
  list_sta = list all stations (AP)
  deauthenticate <addr> = deauthenticate a station
  disassociate <addr> = disassociate a station
  chan_switch <cs_count> <freq> [sec_channel_offset=] [center_freq1=] [center_freq2=] [bandwidth=] [blocktx] [ht|vht] = CSA parameters
  update_beacon = update Beacon frame contents
  suspend = notification of suspend/hibernate
  resume = notification of resume/thaw
  roam <addr> = roam to the specified BSS
  p2p_find [timeout] [type=*] = find P2P Devices for up-to timeout seconds
  p2p_stop_find = stop P2P Devices search
  p2p_asp_provision <addr> adv_id=<adv_id> conncap=<conncap> [info=<infodata>] = provision with a P2P ASP Device
  p2p_asp_provision_resp <addr> adv_id=<adv_id> [role<conncap>] [info=<infodata>] = provision with a P2P ASP Device
  p2p_connect <addr> <"pbc"|PIN> [ht40] = connect to a P2P Device
  p2p_listen [timeout] = listen for P2P Devices for up-to timeout seconds
  p2p_group_remove <ifname> = remove P2P group interface (terminate group if GO)
  p2p_group_add [ht40] = add a new P2P group (local end as GO)
  p2p_group_member <dev_addr> = Get peer interface address on local GO using peer Device Address
  p2p_prov_disc <addr> <method> = request provisioning discovery
  p2p_get_passphrase = get the passphrase for a group (GO only)
  p2p_serv_disc_req <addr> <TLVs> = schedule service discovery request
  p2p_serv_disc_cancel_req <id> = cancel pending service discovery request
  p2p_serv_disc_resp <freq> <addr> <dialog token> <TLVs> = service discovery response
  p2p_service_update = indicate change in local services
  p2p_serv_disc_external <external> = set external processing of service discovery
  p2p_service_flush = remove all stored service entries
  p2p_service_add <bonjour|upnp|asp> <query|version> <response|service> = add a local service
  p2p_service_rep asp <auto> <adv_id> <svc_state> <svc_string> [<svc_info>] = replace local ASP service
  p2p_service_del <bonjour|upnp> <query|version> [|service] = remove a local service
  p2p_reject <addr> = reject connection attempts from a specific peer
  p2p_invite <cmd> [peer=addr] = invite peer
  p2p_peers [discovered] = list known (optionally, only fully discovered) P2P peers
  p2p_peer <address> = show information about known P2P peer
  p2p_set <field> <value> = set a P2P parameter
  p2p_flush = flush P2P state
  p2p_cancel = cancel P2P group formation
  p2p_unauthorize <address> = unauthorize a peer
  p2p_presence_req [<duration> <interval>] [<duration> <interval>] = request GO presence
  p2p_ext_listen [<period> <interval>] = set extended listen timing
  p2p_remove_client <address|iface=address> = remove a peer from all groups
  vendor_elem_add <frame id> <hexdump of elem(s)> = add vendor specific IEs to frame(s)
    0: Probe Req (P2P), 1: Probe Resp (P2P) , 2: Probe Resp (GO), 3: Beacon (GO), 4: PD Req, 5: PD Resp, 6: GO Neg Req, 7: GO Neg Resp, 8: GO Neg Conf, 9: Inv Req, 10: Inv Resp, 11: Assoc Req (P2P), 12: Assoc Resp (P2P)
  vendor_elem_get <frame id> = get vendor specific IE(s) to frame(s)
    0: Probe Req (P2P), 1: Probe Resp (P2P) , 2: Probe Resp (GO), 3: Beacon (GO), 4: PD Req, 5: PD Resp, 6: GO Neg Req, 7: GO Neg Resp, 8: GO Neg Conf, 9: Inv Req, 10: Inv Resp, 11: Assoc Req (P2P), 12: Assoc Resp (P2P)
  vendor_elem_remove <frame id> <hexdump of elem(s)> = remove vendor specific IE(s) in frame(s)
    0: Probe Req (P2P), 1: Probe Resp (P2P) , 2: Probe Resp (GO), 3: Beacon (GO), 4: PD Req, 5: PD Resp, 6: GO Neg Req, 7: GO Neg Resp, 8: GO Neg Conf, 9: Inv Req, 10: Inv Resp, 11: Assoc Req (P2P), 12: Assoc Resp (P2P)
  fetch_anqp = fetch ANQP information for all APs
  stop_fetch_anqp = stop fetch_anqp operation
  interworking_select [auto] = perform Interworking network selection
  interworking_connect <BSSID> = connect using Interworking credentials
  interworking_add_network <BSSID> = connect using Interworking credentials
  anqp_get <addr> <info id>[,<info id>]... = request ANQP information
  gas_request <addr> <AdvProtoID> [QueryReq] = GAS request
  gas_response_get <addr> <dialog token> [start,len] = Fetch last GAS response
  hs20_anqp_get <addr> <subtype>[,<subtype>]... = request HS 2.0 ANQP information
  nai_home_realm_list <addr> <home realm> = get HS20 nai home realm list
  hs20_icon_request <addr> <icon name> = get Hotspot 2.0 OSU icon
  fetch_osu = fetch OSU provider information from all APs
  cancel_fetch_osu = cancel fetch_osu command
  sta_autoconnect <0/1> = disable/enable automatic reconnection
  tdls_discover <addr> = request TDLS discovery with <addr>
  tdls_setup <addr> = request TDLS setup with <addr>
  tdls_teardown <addr> = tear down TDLS with <addr>
  tdls_link_status <addr> = TDLS link status with <addr>
  wmm_ac_addts <uplink/downlink/bidi> <tsid=0..7> <up=0..7> [nominal_msdu_size=#] [mean_data_rate=#] [min_phy_rate=#] [sba=#] [fixed_nominal_msdu] = add WMM-AC traffic stream
  wmm_ac_delts <tsid> = delete WMM-AC traffic stream
  wmm_ac_status = show status for Wireless Multi-Media Admission-Control
  tdls_chan_switch <addr> <oper class> <freq> [sec_channel_offset=] [center_freq1=] [center_freq2=] [bandwidth=] [ht|vht] = enable channel switching with TDLS peer
  tdls_cancel_chan_switch <addr> = disable channel switching with TDLS peer <addr>
  signal_poll = get signal parameters
  signal_monitor = set signal monitor parameters
  pktcnt_poll = get TX/RX packet counters
  reauthenticate = trigger IEEE 802.1X/EAPOL reauthentication
  wnm_sleep <enter/exit> [interval=#] = enter/exit WNM-Sleep mode
  wnm_bss_query <query reason> [list] [neighbor=<BSSID>,<BSSID information>,<operating class>,<channel number>,<PHY type>[,<hexdump of optional subelements>] = Send BSS Transition Management Query
  raw <params..> = Sent unprocessed command
  flush = flush wpa_supplicant state
  radio_work = radio_work <show/add/done>
  vendor <vendor id> <command id> [<hex formatted command argument>] = Send vendor command
  neighbor_rep_request [ssid=<SSID>] [lci] [civic] = Trigger request to AP for neighboring AP report (with optional given SSID in hex or enclosed in double quotes, default: current SSID; with optional LCI and location civic request)
  twt_setup [dialog=<token>] [exponent=<exponent>] [mantissa=<mantissa>] [min_twt=<Min TWT>] [setup_cmd=<setup-cmd>] [twt=<u64>] [requestor=0|1] [trigger=0|1] [implicit=0|1] [flow_type=0|1] [flow_id=<3-bit-id>] [protection=0|1] [twt_channel=<twt chanel id>] [control=<control-u8>] = Send TWT Setup frame
  twt_teardown [flags=<value>] = Send TWT Teardown frame
  erp_flush = flush ERP keys
  mac_rand_scan <scan|sched|pno|all> enable=<0/1> [addr=mac-address mask=mac-address-mask] = scan MAC randomization
  get_pref_freq_list <interface type> = retrieve preferred freq list for the specified interface type
  p2p_lo_start <freq> <period> <interval> <count> = start P2P listen offload
  p2p_lo_stop = stop P2P listen offload
  dpp_qr_code report a scanned DPP URI from a QR Code
  dpp_bootstrap_gen type=<qrcode> [chan=..] [mac=..] [info=..] [curve=..] [key=..] = generate DPP bootstrap information
  dpp_bootstrap_remove *|<id> = remove DPP bootstrap information
  dpp_bootstrap_get_uri <id> = get DPP bootstrap URI
  dpp_bootstrap_info <id> = show DPP bootstrap information
  dpp_bootstrap_set <id> [conf=..] [ssid=<SSID>] [ssid_charset=#] [psk=<PSK>] [pass=<passphrase>] [configurator=<id>] [conn_status=#] [akm_use_selector=<0|1>] [group_id=..] [expiry=#] [csrattrs=..] = set DPP configurator parameters
  dpp_auth_init peer=<id> [own=<id>] = initiate DPP bootstrapping
  dpp_listen <freq in MHz> = start DPP listen
  dpp_stop_listen = stop DPP listen
  dpp_configurator_add [curve=..] [key=..] = add DPP configurator
  dpp_configurator_remove *|<id> = remove DPP configurator
  dpp_configurator_get_key <id> = Get DPP configurator's private key
  dpp_configurator_sign conf=<role> configurator=<id> = generate self DPP configuration
  dpp_map_bss_conf_resp [curve=..][conf_obj=..]
  dpp_pkex_add add PKEX code
  dpp_pkex_remove *|<id> = remove DPP pkex information
  dpp_controller_start [tcp_port=<port>] [role=..] = start DPP controller
  dpp_controller_stop = stop DPP controller
  dpp_chirp own=<BI ID> iter=<count> = start DPP chirp
  dpp_stop_chirp = stop DPP chirp
  dpp_map_peer_disc_start = start map peer disc
  dpp_reconfig = DPP reconfig
  all_bss = list all BSS entries (scan results)
  pasn_start bssid=<BSSID> akmp=<WPA key mgmt> cipher=<WPA cipher> group=<group>= Start PASN
  pasn_auth_start bssid=<BSSID> akmp=<WPA key mgmt> cipher=<WPA cipher> group=<group> nid=<network id> = Start PASN authentication
  pasn_auth_stop = Stop PASN authentication
  ptksa_cache_list = Get the PTKSA Cache
  pasn_deauth bssid=<BSSID> = Remove PASN PTKSA state
  mscs <add|remove|change> [up_bitmap=<hex byte>] [up_limit=<integer>] [stream_timeout=<in TUs>] [frame_classifier=<hex bytes>] = Configure MSCS request
  scs [scs_id=<decimal number>] <add|remove|change> [scs_up=<0-7>] [classifier_type=<4|10>] [classifier params based on classifier type] [tclas_processing=<0|1>] [scs_id=<decimal number>] ... = Send SCS request
  dscp_resp <[reset]>/<[solicited] [policy_id=1 status=0...]> [more] = Send DSCP response
  dscp_query wildcard/domain_name=<string> = Send DSCP Query
```

#### wpa_supplicant

```
wpa_supplicant v2.10-devel
Copyright (c) 2003-2019, Jouni Malinen <j@w1.fi> and contributors

This software may be distributed under the terms of the BSD license.
See README for more details.

This product includes software developed by the OpenSSL Project
for use in the OpenSSL Toolkit (http://www.openssl.org/)

usage:

  wpa_supplicant [-BddhKLqqstvW] [-P<pid file>] [-g<global ctrl>] \
        [-G<group>] \
        -i<ifname> -c<config file> [-C<ctrl>] [-D<driver>] [-H<hostapd path>] [-p<driver_param>] \
        [-b<br_ifname>] [-e<entropy file>] [-f<debug file>] \
        [-o<override driver>] [-O<override ctrl>] \
        [-N -i<ifname> -c<conf> [-C<ctrl>] [-D<driver>] \
        [-m<P2P Device config file>] \
        [-p<driver_param>] [-b<br_ifname>] [-I<config file>] ...]

drivers:
    nl80211 = Linux nl80211/cfg80211
    swconfig = swconfig ethernet driver

options:
    -b = optional bridge interface name
    -B = run daemon in the background
    -c = Configuration file
    -C = ctrl_interface parameter (only used if -c is not)
    -d = increase debugging verbosity (-dd even more)
    -D = driver name (can be multiple drivers: nl80211,wext)
    -e = entropy file
    -f = log output to debug file instead of stdout
    -g = global ctrl_interface
    -G = global ctrl_interface group
    -h = show this help text
    -H = connect to a hostapd instance to manage state changes
    -i = interface name
    -I = additional configuration file
    -K = include keys (passwords, etc.) in debug output
    -L = show license (BSD)
    -m = Configuration file for the P2P Device interface
    -N = start describing new interface
    -o = override driver parameter for new interfaces
    -O = override ctrl_interface parameter for new interfaces
    -p = driver parameters
    -P = PID file
    -q = decrease debugging verbosity (-qq even less)
    -s = log output to syslog instead of stdout
    -t = include timestamp in debug messages
    -v = show version
    -W = wait for a control interface monitor before starting

example:
    wpa_supplicant -Dnl80211 -iwlan0 -c/etc/wpa_supplicant.conf
```

#### wps_enhc
#### wpsd

```
USAGE: wpsd <ifname> <enable/disable/reconfig>
```

#### xargs

```
Usage: xargs [OPTIONS] [PROG ARGS]

Run PROG on every item given by stdin

    -p      Ask user whether to run each command
    -r      Don't run command if input is empty
    -0      Input is separated by NUL characters
    -t      Print the command on stderr before execution
    -e[STR] STR stops input processing
    -n N    Pass no more than N args to PROG
    -s N    Pass command line of no more than N bytes
    -x      Exit if size is exceeded
```

#### xtables-multi

TODO

```
Valid subcommands:
    * iptables
    * main4
    * iptables-save
    * save4
    * iptables-restore
    * restore4
    * ip6tables
    * main6
    * ip6tables-save
    * save6
    * ip6tables-restore
    * restore6
```

#### xz

```
Usage: xz -d [-cf] [FILE]...

Decompress FILE (or stdin)

    -d      Decompress
    -c      Write to stdout
    -f      Force
```

#### xzcat

```
Usage: xzcat [FILE]...

Decompress to stdout
```

#### yes

```
Usage: yes [STRING]

Repeatedly output a line with STRING, or 'y'
```

#### zcat

```
Usage: zcat [FILE]...

Decompress to stdout
```

