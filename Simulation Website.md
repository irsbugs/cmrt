# Simulation Website

Building a WordPress/CiviCRM local website that is a simulation of the Ventraip / cmrailttrail.org.au website

The computer that hosts this simulation website is expected to be in the same local network as the computer you normally use. 

The simulation computer will only provide support for IPV4 i.e. no IPV6, and http i.e. no https.

## Computer Hardware - Minimum Specifications

* CPU: Quad core, >= 2.5GHz
* RAM: >= 4GB
* Disk: Solid State Sata Disk (SSD). 128GB seems to be the minimum available these days.
* Ethernet: 1000Mb/sec at a static ip address. If a cable can be connected from the computer to the router.
* Wifi: If not using ethernet, then the wifi connection to the router needs a static ip address.
* Operating System: Linux. Recommend Ubuntu Mate 24.04.x

## Installation Steps

* Download Operating System iso file. E.g. `https://ubuntu-mate.org/download/`
* Copy iso to make a bootable USB drive.
* Boot the USB drive.
* Install Ubuntu on SSD
* Set initial account to be `cmrailtr` with a User name of `Administrator`
* Set a static/fixed address to the router on the ethernet or wifi connection. e.g. 192.168.1.100
* Perform updates to get the latest patches.
* Install openssh-server.
* Install Apache2 and change Owner and Group from `www-data` to `cmrailtr`.
* Install MariaDB. `mariadb-server` and `mariadb-client`
* Install WordPress. With top-level directory in home folder. All files nd folders have the Owner and Group of `cmrailtr`.
* WordPress database is: 
* Rename `wordpress` top-level directory as `public_html`
* Install CiviCRM with its own database.


### On the computer you normally use on your local network
* Make sure that openssh-client is installed.
* Check you can *ssh* into the simulation computer. `$ ssh cmrailtr@192.168.1.100`
* Check you can *scp* and transfer files between computers.

## Tailoring:
In the home folder create a bin folder for bash and Python scripts. `$ mkdir bin`
In the home folder create a backup folder. `$ mkdir civicrm_backup`


[cmrailtr@s03dd public_html]$ mysql -u root -p
Enter password:
ERROR 1045 (28000): Access denied for user 'root'@'localhost' (using password: YES)
[cmrailtr@s03dd public_html]$

// ** MySQL settings - You can get this info from your web host ** //
/** The name of the database for WordPress */
define( 'DB_NAME', 'cmrailtr_czhn1' );

/** MySQL database username */
define( 'DB_USER', 'cmrailtr_czhn1' );

/** MySQL database password */
define( 'DB_PASSWORD', '[ Secret ]' );

cmrailtr_civicrm

Data tables prefix: bsen_ instead of wp

    Account Name: cmrailtr
    WordPress top level directory. Default is wordpress: public_html
    WordPress Maria database name. default is wordpress: cmrailtr_czhn1
    WordPress MariaDB database User name: cmrailtr_czhn1
    WordPress tables prefix. Default is wp_: bsen_
    CiviCRM MariaDB database name. Default is civicrm: cmrailtr_civicrm
    CiviCRM tables prefix: civicrm_

```
MariaDB [(none)]> show databases;
+--------------------+
| Database           |
+--------------------+
| cmrailtr_civicrm   |
| cmrailtr_czhn1     |
| information_schema |
+--------------------+
3 rows in set (0.004 sec)
```

For CiviCRM Installation:

https://github.com/irsbugs/cmrt/blob/main/CiviCRM%20Installation.md

User name for dataabase = cmrailtr_czhn1

mysql://cmrailtr_czhn1:HiDDEN@localhost:3306/cmailtr_civicrm

Username  Host Localhost 192.168.1.101
cmrailtr@CMRT-Demo:~$ 
