# Server for Wordpress and Standalone CiviCRM

2026-05-13
Ian

## Objective

VentraIP host the [cmrailtrial.org.au](cmrailtrial.org.au) WordPress website, while CiviCRM is hosted on [cmrailtrail.civicrm.org](cmrailtrail.civicrm.org). The intention is to have CiviCRM Standalone installed on VentraIP hosting system. The Wordpress website would rremain as the main domain, *cmrailtril.org.au* and the CiviCRM would be moved to the VentraIP sub-domain *crm.cmrailtrail.org.au*.

A simulation of this WordPress/CiviCRM, domain/sub-domain, configuration will be performed on a standalone PC running the Ubuntu Server version of Linux. This server will be configured to replicate the VentraIP hosting server.

Upon sucessful testing of the PC, a request will be made to VentraIP top provide the sub-domain. CiviCRM Standalone will the be installed into the sub-domain and tested. The CMRT data on the civicrm.org system will be moved to the subn-domain CiviCRM.

The sub-domain will go-live and the civicrm.org system will be decommissioned.

This document describes the steps in building the simulation PC.

## TODO List


## Aspects of the VentraIP hosting system

The following are aspects of the current VentraIP hosting configuration. These features will be replicated on the server.

* The webserver used is Apache2. However there is no permission to */etc/apqache2/sites-available/xxx.conf* to help understand the configuration. 
* The user account name is *cmrailtr*. All files and directories have owner and group of *cmrailtr*.
* Files have chmod permissions of 664 by default.
* Directories have chmod permissions of 775 by default.
* public_html is the directory for WordPress. i.e. */home/cmtailtr/public_html*.
* A symbolic link exists from www to public_html. Thus */home/cmrailtr/www* is also a path to WordPress
* home directory listing
```bash
[cmrailtr@s03dd ~]$ ls -l
total 68
lrwxrwxrwx  1 cmrailtr cmrailtr    34 Feb 12  2021 access-logs -> /etc/apache2/logs/domlogs/cmrailtr
drwxr-x---  3 cmrailtr mail      4096 Apr  8 00:17 etc
drwx------  3 cmrailtr cmrailtr  4096 May 13 03:35 logs
drwxrws--- 19 nobody   cmrailtr  4096 May 20  2021 lscache
drwx------  2 cmrailtr cmrailtr  4096 Jun  9  2025 lscmData
drwxr-x--x 12 cmrailtr cmrailtr  4096 May 11 18:08 mail
drwxr-x---  3 cmrailtr cmrailtr  4096 Feb 12  2021 public_ftp
drwxr-x---  6 cmrailtr nobody    4096 May 13 00:57 public_html
drwxr-xr-x  5 cmrailtr cmrailtr  4096 May  2 17:44 ssl
drwxr-xr-x  8 cmrailtr cmrailtr 12288 May 13 08:27 tmp
drwxr-xr-x  2 cmrailtr cmrailtr  4096 Jun  3  2025 virtualenv
drwx------  2 cmrailtr cmrailtr  4096 Mar 23  2022 wordpress-backups
lrwxrwxrwx  1 cmrailtr cmrailtr    11 Feb 12  2021 www -> public_html

[cmrailtr@s03dd ~]$ ls /etc/apache2/logs/domlogs/cmrailtr -l
total 876
-rw-r----- 2 root cmrailtr  39930 May 13 08:45 cmrailtrail.org.au
-rw-r----- 2 root cmrailtr 846564 May 13 08:44 cmrailtrail.org.au-ssl_log
```

## Server Initial Setup

* Obtained a PC with 3GHz quad core, 8GB RAM, and 240GB SSD.
* Downloaded latest Ubuntu Server 26.04 iso file. from [https://ubuntu.com/download/server](https://ubuntu.com/download/server)
* Used *Startup Disk Creator* to copy iso file to USB drive.
* Installed USB iso image to the PC.
* Configured the server as:
  * Your name: CMRT
  * Server name: cmrailtr
  * Username: cmrailtr <-- This is a replication of the Username for the VentraIP account. Resulting in *Owner* and *Group* being *cmrailtr*.
  * password: f8
* Release has corrupted */etc/apt/sources.list.d/ubuntu.sources* file. Was missing the line: *URIs: http://nz.archive.ubuntu.com/ubuntu/*
* Performed update and upgrqade. Doesn't use any snap applications.
* Setup fixed wifi address of *192.168.1.101* for connection to the local lan.
* Installed open-ssh server. Check with: *$ systemctl status ssh*
* Able to connect, viua SSH, from a remote system into this server.
* A bin directory was created to hold python or bash scripts. E.g. Backup utilities. Need to disconnect SSH, then reconnect SSH, to invoke.

## Static wifi address

The following /etc/netplan/01-wifi-101-config.yaml file was created, so *$ netplan apply* would invoke the wifi at address *192.168.1.101*

```yaml
# This is the network config written by 'subiquity'
# Modified by Ian Stewart 2026-05-12
# File: /etc/netplan/01-wifi-101-config.yaml
# After making any changes: $ sudo netplan apply 
network:
  ethernets:
    eno1:
      match:
        macaddress: a0:d3:c1:0a:b8:3e
      set-name: eno1
  version: 2

  # Fixed wifi address of 192.168.1.101 for server in the shed
  wifis:
    wlp2s0:
      dhcp4: false
      addresses:
        - 192.168.1.101/24
      nameservers:
        addresses:
          -  8.8.8.8
          -  192.168.1.254
      access-points:
        AJ:
          password: Stewart77
      routes:
        - to: default
          via: 192.168.1.254
```






