# SSH Implementation

## Introduction

SSH, *Secure SHell*, access into the VentraIP *cmrailtr* account allows a remote PC terminal to issue bash commands to run applications. For example, backing up the sql database. It provides a similar service as C-Panel *Terminal*.

SCP, *Secure CoPy*, is a partner application to *SSH*, which allows the copying of files from a remote PC terminal to the VentraIP *cmrailtr* account and vice versa.

Allowing SSH access is a potential VentraIP security issue, so it is not enabled by default. The following describes the steps to enable SSH on the VentraIP system. 

## C-Panel


```
ian@hp:~$ cd ~/
ian@hp:~$ ls -l .ssh/
total 64
-rw-rw-r-- 1 ian ian  1766 May 19 11:19 id_rsa
-rw-rw-r-- 1 ian ian  1766 May 17 18:16 id_rsa_another_o0ld
-rw-rw-r-- 1 ian ian  1766 May 17 12:04 id_rsa_new_private_21026-05-17
-rw------- 1 ian ian  3389 Jun 13  2025 id_rsa_old
-rw------- 1 ian ian  1766 Jun 13  2025 id_rsa_old_2025-05-17
-rw-rw-r-- 1 ian ian  1766 May 17 12:23 id_rsa_old_2026-05-17_1800
-rw-rw-r-- 1 ian ian  1615 May 17 12:17 id_rsa.ppk
-rw-rw-r-- 1 ian ian   382 May 17 19:34 id_rsa.pub
-rw-rw-r-- 1 ian ian   382 May 17 12:07 id_rsa.pub_old
-rw-r--r-- 1 ian ian   745 Mar  6  2025 id_rsa.pub_old_2026-05-17
-rw------- 1 ian ian 10018 May 19 12:17 known_hosts
-rw------- 1 ian ian  9796 May 19 12:16 known_hosts.old
ian@hp:~$ chmod 600 .ssh/id_rsa
ian@hp:~$ ls -l .ssh/
total 64
-rw------- 1 ian ian  1766 May 19 11:19 id_rsa
-rw-rw-r-- 1 ian ian  1766 May 17 18:16 id_rsa_another_o0ld
-rw-rw-r-- 1 ian ian  1766 May 17 12:04 id_rsa_new_private_21026-05-17
-rw------- 1 ian ian  3389 Jun 13  2025 id_rsa_old
-rw------- 1 ian ian  1766 Jun 13  2025 id_rsa_old_2025-05-17
-rw-rw-r-- 1 ian ian  1766 May 17 12:23 id_rsa_old_2026-05-17_1800
-rw-rw-r-- 1 ian ian  1615 May 17 12:17 id_rsa.ppk
-rw-rw-r-- 1 ian ian   382 May 17 19:34 id_rsa.pub
-rw-rw-r-- 1 ian ian   382 May 17 12:07 id_rsa.pub_old
-rw-r--r-- 1 ian ian   745 Mar  6  2025 id_rsa.pub_old_2026-05-17
-rw------- 1 ian ian 10018 May 19 12:17 known_hosts
-rw------- 1 ian ian  9796 May 19 12:16 known_hosts.old
ian@hp:~$ 

```

```
[cmrailtr@s03dd ~]$ ls -l .ssh/
total 28
-rw-r--r-- 1 cmrailtr cmrailtr  381 May 17 10:22 authorized_keys
-rw------- 1 cmrailtr cmrailtr 1766 May 17 08:22 id_rsa
-rw-r--r-- 1 cmrailtr cmrailtr  382 May 17 08:22 id_rsa.pub
drwx------ 2 cmrailtr cmrailtr 4096 May 17 10:17 putty

```


