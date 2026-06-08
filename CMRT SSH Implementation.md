# SSH Implementation

## Introduction

SSH, *Secure SHell*, access into the VentraIP *cmrailtr* account allows a remote PC terminal to issue bash commands to run applications. For example, backing up the sql database. It provides a similar service as C-Panel *Terminal*.

SCP, *Secure CoPy*, is a partner application to *SSH*, which allows the copying of files from a remote PC terminal to the VentraIP *cmrailtr* account and vice versa.

Allowing SSH access is a potential VentraIP security issue, so it is not enabled by default. The following describes the steps to enable SSH on the VentraIP system. 

## C-Panel
File permissions on Desktop PC
```
700
drwx------  2 ian      ian          4096 May 20 09:55  .ssh
600
-rw------- 1 ian ian  1766 May 19 11:19 id_rsa
644
-rw-rw-r-- 1 ian ian   382 May 17 19:34 id_rsa.pub
```

File permissions on the VentraIP server
```
[cmrailtr@s03dd ~]$ ls -l .ssh/
total 28
-rw-r--r-- 1 cmrailtr cmrailtr  381 May 17 10:22 authorized_keys
-rw------- 1 cmrailtr cmrailtr 1766 May 17 08:22 id_rsa
-rw-r--r-- 1 cmrailtr cmrailtr  382 May 17 08:22 id_rsa.pub
drwx------ 2 cmrailtr cmrailtr 4096 May 17 10:17 putty

```

After changing the id_rsa to chmod 600

ian@hp:~$ ssh cmrailtr@s03dd.syd6.hostingplatform.net.au -p 2683
sign_and_send_pubkey: signing failed for RSA "/home/ian/.ssh/id_rsa" from agent: agent refused operation
cmrailtr@s03dd.syd6.hostingplatform.net.au's password: 
[cmrailtr@s03dd ~]$ 
[cmrailtr@s03dd ~]$ 


The local desktop PC that will be used to make SSH connections to the VentraIP server, needs to have OpenSSH-client installed on it, to provide the *ssh* related applications. With Ubunutu desktop OpenSSH can be installed with the command:
```
$ sudo apt install openssh-client
```
Note that there is also a product called *openssh-server*. It should not be necessaryu to instyall this on the desktop PC. This application is on the VentraIP server and it is what the ssh application on the desktop PC commimnicates with on the server.

THe VertraIP server contains a private key in the file *id_rsa* and a public key in the file id_rsa.pub. The private key is downloaded/copied to the file ~/.ssh/id_rsa. This private key file is the same as the file in the VentraIP *cmrailtr* account ~/.ssh/id_rsa directory.

When this file id_rsa is added to the dektop PC ~/.ssh/ directory. It should be set with Owner Read/Write Only. i.e.
```
$ chmod 600 ~/.ssh/id_rsa
```
It then needs to be added to the desktop PC's local ssh. The *ssh-add* application is used as follows:
```
ian@hp:~$ ssh-add
Enter passphrase for /home/ian/.ssh/id_rsa:   <-- The passphrase is the password to the VentraIP cmrailtr account. E.g *S-12-]* 
Identity added: /home/ian/.ssh/id_rsa (/home/ian/.ssh/id_rsa)

A Passkey window may open and ask for a passphrase. Enter the $-12-] password.
```
Now, when making a connection from the desktop PC to the VertraIP server, it will not prompt for the password and will directly login to the cmrailtr account:
Note that the ssh port used by VentraIP is not the default of 22, but is 2683.
```
ian@hp:~$ ssh cmrailtr@s03dd.syd6.hostingplatform.net.au -p 2683
[cmrailtr@s03dd ~]$
```
```
ls
access-logs                             etc         public_ftp
bin                                     index.html  public_html
civicrm-6.14.0-standalone.tar.gz        index.php   ssl
civicrm_backup_2026-04-09_11:11:33.sql  logs        tmp
civicrm_backup_2026-04-09_12:12:44.sql  lscache     virtualenv
civicrm_log                             lscmData    wordpress-backups
civicrm_logs                            mail        www
civicrm-standalone                      php
[cmrailtr@s03dd ~]$ 

```

## SCP

Sending a file from the desktop PC to the VentrIP server. Note -P 2683 is the SSH port to use at VentraIP
```
$ scp -P 2683 test_scp.txt cmrailtr@s03dd.syd6.hostingplatform.net.au:
test_scp.txt                                  100%  116     2.1KB/s   00:00    

```

Checking the file got to the VentraIP server cmrailtr account
```
[cmrailtr@s03dd ~]$ ls -l test_scp.txt
-rw-rw-r-- 1 cmrailtr cmrailtr 116 May 19 19:10 test_scp.txt
[cmrailtr@s03dd ~]$ cat test_scp.txt
This is test_scp.txt

It is used to test if a file can be scp'ed from a PC to the VentraIP server.

Ian 2026-05-19
```

## SSH Server Setup

The server is setup to accept SSH connections from C-Panel


## SSH Server Whitelisting

The VentraIP server needs to *whitelist* the IP addresses of the remote desktop PC's that will make SSH connections. The remote PC may be on a network that hands out IP addresses from a pool. Thus the IP address of the desktop PC change. For example, when the modem is restarted. If this happens the desktop PC receives a new IP address and the *whitewlist* at VentraIP needs to be updated before a SSH connection can be re-established.

To find out the IP address of the desktop PC. Use a browser to open [https://www.showmyip.com/](https://www.showmyip.com/)

It will display an IPV4 address like: `122.63.67.51` OR an IPV6 address, like `2001:8004:6fe2:30b1:c3fe:02c4:3c50`. Make a note of this IP address.

On the browser connect to the VIP account at VentraIP: `https://vip.ventraip.com.au/login`. As well as a *username* and *password* being required there is 2FA and an authorization code is sent.

Upon logging into this, top level, VIP account: 

* Click on **Websites & Hosting** tab.
* Then, below the tab, click on **Web Hosting** button.
* Then, on the right hand side, click on **Manage** button
* The left-hand column provides a list of items that can be managed. Under the Configuration section, Click on **SSH Access**.
* The SSH Access will display something like:
```
Your hosting account can be enabled for SSH access by allowing the IP address you want to give access to.
Username: cmrailtr
Hostname: s03dd.syd6.hostingplatform.net.au
Port: 2683
This device's IP Address: 122.63.67.51
```
* Confirm that the *This device's IP Address* is the same address as was observer when using **www.showmyip.com/**
* Click the button **ADD IP ADDRESS +**.
* A new screen is displayed to **Add IP Address for SSH Access** with radio buttons to choose:
    * Add my IP address
    * Add my IPV6 address
    * Add a different address
* Select one of the above and click on **Enable SSH Access**.
* On returning to the previous screen the address should now have been added to the *whitelist* table.
* Note that there is an option to Enable IPv6 Management.
  
Finished: Log-out of VIP services account.





