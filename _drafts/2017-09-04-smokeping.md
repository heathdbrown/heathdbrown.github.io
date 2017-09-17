# Smokeping on 16.04 Master with raspberrypi slave

# 16.04 Master install

## Install smokeping package for Ubuntu
```
sudo apt-get install smokeping sendmail -y
```

## Update ownership for RRD files for smokeping and web user
```
find . -type f -name '*.rrd' | xargs chown smokeping:www-data
find . -type f -name '*.rrd' | xargs chmod 0664
```

## Make sure folders are setup correctly for master-slave relationship
See: https://fabianfischer.de/smokeping-under-debian-with-master-slave-configuration/


## Version check on master

Due to installing via packages on the master I am getting the 2.0006011 version.

```
smokeping --version
2.006011
```
## Web Front End on Master

### Apache

### NGINX
See: 
* http://blog.imitran.com/2013/08/smokeping-on-nginx/
* 


# Raspberrypi Slave install

## Install on raspberrypi

```
sudo apt-get install smokeping
```

## Version of smokeping

```
smokeping --version
2.006009
```

## Issue: permission denied on `/etc/smokeping/smokeping_secrets`

```
root@homepib:~# smokeping --master-url=http://smokeping_master/smokeping/smokeping.cgi --shared-secret=/var/smokeping/secret.txt --cache-dir=/tmp/
WARNING: Opening secrets file /etc/smokeping/smokeping_secrets: Permission denied

ERROR: we did not get config from the master. Maybe we are not configured as a slave for any of the targets on the master ?
```

Fix: Update permissions on the MASTER so that the apache or web-server user can read the file.

```
chown smokeping:www-data /etc/smokeping/smokeping_secrets
```

## Issue: Dig not installed

Test by performing dig localhost

```
root@homepib:/etc/smokeping# smokeping --master-url=http://smokeping_master/smokeping/smokeping.cgi --shared-secret=/var/smokeping/secret.txt --cache-dir=/tmp/
Sent data to Server and got new config in response.
ERROR: output of '/usr/bin/dig localhost' does not match (?^i:query time:\s+([0-9.]+)\smsec.*)
 at (eval 28) line 1.
```

Fix: Install dig

```
sudo apt-get update -y
sudo apt-get install dnsutils -y
```

** I had issues with missing packages and found an `apt-get update` was necessary but also included `--fix-missing` on the install of dnsutils.

## Issue: Slave not updating to master graphs

This one is frustrating as the client says it is updating but nothing shows on the master.

```
Sep  9 23:57:03 homepib smokeping[23509]: FPing: Executing /usr/bin/fping -C 20 -q -B1 -r1 -i10 192.168.0.1 www.google.com
Sep  9 23:57:22 homepib smokeping[23509]: FPing: Got fping output: '192.168.0.1 : 48.70 48.68 49.17 47.82 49.19 48.66 49.20 49.01 49.01 48.59 48.84 48.72 49.15 49.02 48.36 48.82 48.37 48.63 47.71 48.95'
Sep  9 23:57:22 homepib smokeping[23509]: FPing: Got fping output: 'www.google.com : 38.56 38.52 41.37 38.44 40.06 39.53 39.09 38.90 40.04 39.47 38.74 38.61 39.01 39.88 39.26 38.71 40.71 38.52 38.55 38.85'
Sep  9 23:57:25 homepib smokeping[23509]: Sent data to Server. Server said OK
Sep  9 23:57:25 homepib smokeping[23509]: FPing: Sleeping 278 seconds.
Sep  9 23:57:30 homepib smokeping[23508]: DNS: forks 5, timeout for each target 76
Sep  9 23:57:30 homepib smokeping[16145]: DNS: query=/usr/bin/dig @68.94.156.9 www.google.com
Sep  9 23:57:30 homepib smokeping[16147]: DNS: query=/usr/bin/dig @208.67.220.220 www.google.com
Sep  9 23:57:30 homepib smokeping[16153]: DNS: query=/usr/bin/dig @68.94.157.9 www.google.com
Sep  9 23:57:30 homepib smokeping[16156]: DNS: query=/usr/bin/dig @208.67.222.222 www.google.com
Sep  9 23:57:45 homepib smokeping[23508]: DNS: 68.94.156.9: got 1.4000000000e-02 1.4000000000e-02 3.2000000000e-02 3.3000000000e-02 4.3000000000e-02
Sep  9 23:57:45 homepib smokeping[23508]: DNS: 208.67.220.220: got 1.3000000000e-02 1.4000000000e-02 1.5000000000e-02 2.9000000000e-02 4.5000000000e-02
Sep  9 23:57:45 homepib smokeping[23508]: DNS: 68.94.157.9: got 1.1000000000e-02 1.3000000000e-02 1.3000000000e-02 1.8000000000e-02 2.0000000000e-02
Sep  9 23:57:45 homepib smokeping[23508]: DNS: 208.67.222.222: got 1.4000000000e-02 1.4000000000e-02 1.8000000000e-02 3.0000000000e-02 4.0000000000e-02
Sep  9 23:57:51 homepib smokeping[23508]: Sent data to Server. Server said OK
Sep  9 23:57:51 homepib smokeping[23508]: DNS: Sleeping 279 seconds.
```
Fix: this is a permission issue on the master

See: See: https://fabianfischer.de/smokeping-under-debian-with-master-slave-configuration/

# Background Information
* https://oss.oetiker.ch/smokeping/doc/smokeping_master_slave.en.html
* https://github.com/oetiker/SmokePing/wiki/FAQ
* https://fabianfischer.de/smokeping-under-debian-with-master-slave-configuration/
