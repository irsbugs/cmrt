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
*
*


## Server Initial Setup

* Obtained a PC with 3GHz quad core, 8GB RAM, and 240GB SSD.
* Downloaded latest Ubuntu Server 26.04 iso file. from [https://ubuntu.com/download/server](https://ubuntu.com/download/server)
* Used *Startup Disk Creator* to copy iso file to USB drive.
* Installed USB iso image to the PC.
* Configured the server as:
  * Your name: CMRT
  * Server name: cmrailtr
  * Username: cmrailtr
  * password: f8
* Release has corrupted */etc/apt/sources.list.d/ubuntu.sources* file. Was missing the line: *URIs: http://nz.archive.ubuntu.com/ubuntu/*
* Performed update and upgrqade. Doesn't use any snap applications.
* Setup fixed wifi address of *192.168.1.101* for connection to the local lan.
* Installed open-ssh server
* Able to connect, viua SSH, from a remote system into this server.

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






