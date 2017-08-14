Version: 7.0.3.I6.1

Issues: VPC peer link does not come up.

```
2017 Aug 14 16:48:35 N9k-1 %ETHPORT-3-IF_ERROR_VLANS_SUSPENDED: VLANs 1 on Inter
face port-channel999 are being suspended. (Reason: vPC peer is not reachable ove
r cfs)

2017 Aug 14 16:53:05 N9k-1 %ETHPORT-3-IF_ERROR_VLANS_SUSPENDED: VLANs 1 on Inter
face port-channel999 are being suspended. (Reason: vPC domain/system id /system
priority mismatch)
```
Configuration:
```
version 7.0(3)I6(1)
feature vpc

vpc domain 100
  peer-switch
  role priority 4096
  system-priority 4096
  peer-keepalive destination 192.168.1.2 source 192.168.1.1
  peer-gateway
  ip arp synchronize

interface port-channel999
  vpc peer-link

N9k-1#

version 7.0(3)I6(1)
feature vpc

vpc domain 100
  peer-switch
  role priority 8192
  system-priority 8192
  peer-keepalive destination 192.168.1.1 source 192.168.1.2
  peer-gateway
  ip arp synchronize

interface port-channel999
  vpc peer-link
```

Issue: Kernel log message when configuring ethernet ports

```
2017 Aug 14 16:54:34 N9k-1 %L2FM-2-L2FM_INVALID_PORT_NUM: Invalid port num 1, ma
x_ports 0
2017 Aug 14 16:55:31 N9k-1 Aug 14 16:55:31 %KERN-3-SYSTEM_MSG: [  616.861435] sy
sconf checkum failed expected 30 Got 0   - kernel
2017 Aug 14 16:55:31 N9k-1 Aug 14 16:55:31 %KERN-3-SYSTEM_MSG: [  616.861436]  r
ead_from_sysconf: No Valid sysconf - kernel
```


Follow-up Reading:
* https://www.cisco.com/c/en/us/td/docs/switches/datacenter/nexus9000/sw/7-x/nx-osv/configuration/guide/b_NX-OSv_9000/b_NX-OSv_chapter_01.html
