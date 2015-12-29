# Pull /24 from all interfaces

Command:

```
show ip interface vrf <vrf> | i 'IP address' | i /24 | cut -d ',' -f 1 | cut -d ':' -f 2
```

Output:

```
1.2.3.2
```

# TCL for rates on interfaces

```
tclsh
foreach interface {
interface1
interface2
} { cli show int $interface | i rate }
```

# TCL for ARPs on interfaces

```
tclsh
set vrf = <vrf>
foreach interface {
interface1
interface2
} { cli show ip arp $interface vrf $vrf}
```

# TCL to ping a list of addresses

```
tclsh
set vrf = <vrf>
foreach address {
address1
address2
} { cli ping $address vrf $vrf}
```
