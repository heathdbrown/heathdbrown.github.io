# Smokeping on 16.04 Master with raspberrypi slave

# 16.04 Master install

## Install smokeping package for Ubuntu
```
sudo apt-get install smokeping sendmail -y
```

## Update ownership for RRD files for smokeping and apache user
```
find . -type f -name '*.rrd' | xargs chown smokeping:www-data
find . -type f -name '*.rrd' | xargs chmod 0664
```

## Version check on master

Due to installing via packages on the master I am getting the 2.0006011 version.

```
smokeping --version
2.006011
```

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



# Background Information
* https://oss.oetiker.ch/smokeping/doc/smokeping_master_slave.en.html
* https://github.com/oetiker/SmokePing/wiki/FAQ
