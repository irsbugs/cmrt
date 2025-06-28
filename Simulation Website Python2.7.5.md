# Simulation Website - Adding Python 2.7.5

## Introduction

Ventraip, hosting cmrailtrail.org.au, use Cloudlinux 7.9 OS and provide Python 2.7.5 from the C-Panel Terminal screen. Python is ideal as a language for writing system admistration scripts.

The Python [versions](https://devguide.python.org/versions/#full-chart) chart shows Python 2.7 having been released in 2010 and going end-of-life in 2000. Ventraip claim they need Python 2.7.5 to support the LiteSpeed HTTP Server they use.

The Simulation Website is hosted on Ubuntu 24.04 distro which is currently supported and includes Python 3.12. Thus, to write Python programs on the Simulation Website that will also run on `cmrailtrail.org.au`, it is necessary to install `Python 2.7.5`.

Python 2.7.5 is no longer available as a debian distribution from the Ubuntu repository. The various source code versions for Python 2.7.5 may be downloaded from: https://www.python.org/downloads/release/python-275/

The Gzipped source-code tar ball of Python 2.7.5 is downloadable from: https://www.python.org/ftp/python/2.7.5/Python-2.7.5.tgz

## Steps to install Python 2.7.5.

* In the home directory create a directory `python_source`.
* Change to this `python_source` directory.
* Download the Python-2.7.5.tgz file with wget.
* Run MD5SUM on the downloaded file and check it is: `b4f01a1d0ba0b46b05c73b2ac909b1df`.
* Untar and unzip the file. This will create the sub-directory  `Python-2.7.5` with all the source off this directory.
* Change to the `Python-2.7.5` directory.
* Run `./configure`
* Run `make`
* Run `sudo make install`. This moves the compiled python to `/usr/local/bin/python2.7` and its library files to `/usr/local/lib/python2.7`.
* Type `$ python<tab><tab>` to see the python versions installed. The command `python2.7` is now assigned to `python`.
* Type `$ python` and Version 2.7.5 of python should launch.
* If you need the Python 3 that is installed, then launch it with `$ python3`

## Console output when installing Python 2.7.5.

Connect from the normal computer to the simulation computer:
```
ian@hp:~$ ssh cmrailtr@192.168.1.101
cmrailtr@192.168.1.101's password: 
Welcome to Ubuntu 24.04.2 LTS (GNU/Linux 6.11.0-28-generic x86_64)

cmrailtr@CMRT-Demo:~$ 
```

* Create the directory `python_source` and change to this `python_source` directory.
```
cmrailtr@CMRT-Demo:~$ pwd
/home/cmrailtr
cmrailtr@CMRT-Demo:~$ mkdir python_source
cmrailtr@CMRT-Demo:~$ cd python_source

cmrailtr@CMRT-Demo:~/python_source$ pwd
/home/cmrailtr/python_source
```

Download the Python-2.7.5.tgz file with wget.
```
cmrailtr@CMRT-Demo:~/python_source$ wget https://www.python.org/ftp/python/2.7.5/Python-2.7.5.tgz
--2025-06-28 17:38:59--  https://www.python.org/ftp/python/2.7.5/Python-2.7.5.tgz
Resolving www.python.org (www.python.org)... 151.101.64.223, 151.101.128.223, 151.101.192.223, ...
Connecting to www.python.org (www.python.org)|151.101.64.223|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 14492759 (14M) [application/octet-stream]
Saving to: ‘Python-2.7.5.tgz’

Python-2.7.5.tgz                    100%[=================================================================>]  13.82M  1.72MB/s    in 9.5s    

2025-06-28 17:40:31 (1.46 MB/s) - ‘Python-2.7.5.tgz’ saved [14492759/14492759]

cmrailtr@CMRT-Demo:~/python_source$ ls -l
total 14156
-rw-rw-r-- 1 cmrailtr cmrailtr 14492759 May 12  2013 Python-2.7.5.tgz
```

Run MD5SUM on the downloaded file and check it is: `b4f01a1d0ba0b46b05c73b2ac909b1df`.
```
cmrailtr@CMRT-Demo:~/python_source$ md5sum Python-2.7.5.tgz
b4f01a1d0ba0b46b05c73b2ac909b1df  Python-2.7.5.tgz
```
Untar and unzip the file. This will create the sub-directory  `Python-2.7.5` with all the source off this directory.
```
cmrailtr@CMRT-Demo:~/python_source$ tar -xvzf Python-2.7.5.tgz
Python-2.7.5/
Python-2.7.5/Grammar/
Python-2.7.5/Grammar/Grammar
Python-2.7.5/config.guess

...snip ~4,600 directories and files...

Python-2.7.5/Misc/RPM/python-2.7.spec
Python-2.7.5/Misc/valgrind-python.supp
Python-2.7.5/Misc/README.klocwork
cmrailtr@CMRT-Demo:~/python_source$ 
```
Using the tree command the `Python-2.7.5` source code has 345 directories, 4732 files.

Change to the `Python-2.7.5` directory.
```
cmrailtr@CMRT-Demo:~/python_source$ ls -l
total 14160
drwxr-xr-x 17 cmrailtr cmrailtr     4096 May 12  2013 Python-2.7.5
-rw-rw-r--  1 cmrailtr cmrailtr 14492759 May 12  2013 Python-2.7.5.tgz

cmrailtr@CMRT-Demo:~/python_source$ cd Python-2.7.5
cmrailtr@CMRT-Demo:~/python_source/Python-2.7.5$

cmrailtr@CMRT-Demo:~/python_source/Python-2.7.5$ ls
Demo     Include  Mac              Modules  PCbuild  README  config.guess  configure.ac   setup.py
Doc      LICENSE  Makefile.pre.in  Objects  Parser   RISCOS  config.sub    install-sh
Grammar  Lib      Misc             PC       Python   Tools   configure     pyconfig.h.in
```

Run `./configure`
```
cmrailtr@CMRT-Demo:~/python_source/Python-2.7.5$ ./configure
checking build system type... x86_64-unknown-linux-gnu
checking host system type... x86_64-unknown-linux-gnu

...snip ~540 lines...

config.status: creating pyconfig.h
creating Modules/Setup
creating Modules/Setup.local
creating Makefile
cmrailtr@CMRT-Demo:~/python_source/Python-2.7.5$ 
```

Run `make`
```
cmrailtr@CMRT-Demo:~/python_source/Python-2.7.5$ make
gcc -c -fno-strict-aliasing -g -O2 -DNDEBUG -g -fwrapv -O3 -Wall -Wstrict-prototypes  -I. -IInclude -I./Include   -DPy_BUILD_CORE -o Modules/python.o ./Modules/python.c
gcc -c -fno-strict-aliasing -g -O2 -DNDEBUG -g -fwrapv -O3 -Wall -Wstrict-prototypes  -I. -IInclude -I./Include   -DPy_BUILD_CORE -o Parser/acceler.o Parser/acceler.c

...snip ~1400 lines...

changing mode of build/scripts-2.7/2to3 from 664 to 775
changing mode of build/scripts-2.7/smtpd.py from 664 to 775
/usr/bin/install -c -m 644 ./Tools/gdb/libpython.py python-gdb.py
cmrailtr@CMRT-Demo:~/python_source/Python-2.7.5$ 
```

`Run `sudo make install`. This compiles and moves python to `/usr/local/bin/python2.7` and its library files to `/usr/local/lib/python2.7`.
```
cmrailtr@CMRT-Demo:~/python_source/Python-2.7.5$ sudo make install
[sudo] password for cmrailtr: 
/usr/bin/install -c python /usr/local/bin/python2.7
if test -f libpython2.7.a; then \
	if test -n "" ; then \
		/usr/bin/install -c -m 555  /usr/local/bin; \
	else \
		/usr/bin/install -c -m 555 libpython2.7.a /usr/local/lib/libpython2.7.a; \
		if test libpython2.7.a != libpython2.7.a; then \
			(cd /usr/local/lib; ln -sf libpython2.7.a libpython2.7.a) \
		fi \
	fi; \
else	true; \
fi
running build

...snip ~4700 lines...

rm -f /usr/local/share/man/man1/python2.1
(cd /usr/local/share/man/man1; ln -s python2.7.1 python2.1)
rm -f /usr/local/share/man/man1/python.1
(cd /usr/local/share/man/man1; ln -s python2.1 python.1)
cmrailtr@CMRT-Demo:~/python_source/Python-2.7.5$ 
```

Type `$ python<tab><tab>` to see the python versions installed. The command `python2.7` is now assigned to `python`.
```
cmrailtr@CMRT-Demo:~/python_source/Python-2.7.5$ python<tab><tab>
python             python2            python2.7          python3            pythoncalls-bpfcc  pythongc-bpfcc     
python-config      python2-config     python2.7-config   python3.12         pythonflow-bpfcc   pythonstat-bpfcc 
```

Type `$ python` and Version 2.7.5 of python should launch.
```
cmrailtr@CMRT-Demo:~/python_source/Python-2.7.5$ python
Python 2.7.5 (default, Jun 28 2025, 17:59:47) 
[GCC 13.3.0] on linux2
Type "help", "copyright", "credits" or "license" for more information.
>>> 
```

Review the Python 2.7.5. modules available
```
>>> help("modules")

Please wait a moment while I gather a list of all available modules...

BaseHTTPServer      array               imghdr              shelve
Bastion             ast                 imp                 shlex
CDROM               asynchat            importlib           shutil
CGIHTTPServer       asyncore            imputil             signal
Canvas              atexit              inspect             site
ConfigParser        audiodev            io                  smtpd
Cookie              audioop             itertools           smtplib
DLFCN               base64              json                sndhdr
Dialog              bdb                 keyword             socket
DocXMLRPCServer     binascii            lib2to3             spwd
FileDialog          binhex              linecache           sqlite3
FixTk               bisect              linuxaudiodev       sre
HTMLParser          bsddb               locale              sre_compile
IN                  cPickle             logging             sre_constants
MimeWriter          cProfile            macpath             sre_parse
Queue               cStringIO           macurl2path         ssl
ScrolledText        calendar            mailbox             stat
SimpleDialog        cgi                 mailcap             statvfs
SimpleHTTPServer    cgitb               markupbase          string
SimpleXMLRPCServer  chunk               marshal             stringold
SocketServer        cmath               math                stringprep
StringIO            cmd                 md5                 strop
TYPES               code                mhlib               struct
Tix                 codecs              mimetools           subprocess
Tkconstants         codeop              mimetypes           sunau
Tkdnd               collections         mimify              sunaudio
Tkinter             colorsys            mmap                symbol
UserDict            commands            modulefinder        symtable
UserList            compileall          multifile           sys
UserString          compiler            multiprocessing     sysconfig
_LWPCookieJar       contextlib          mutex               syslog
_MozillaCookieJar   cookielib           netrc               tabnanny
__builtin__         copy                new                 tarfile
__future__          copy_reg            nntplib             telnetlib
_abcoll             crypt               ntpath              tempfile
_ast                csv                 nturl2path          termios
_bisect             ctypes              numbers             test
_codecs             curses              opcode              textwrap
_codecs_cn          datetime            operator            this
_codecs_hk          dbhash              optparse            thread
_codecs_iso2022     decimal             os                  threading
_codecs_jp          difflib             os2emxpath          time
_codecs_kr          dircache            ossaudiodev         timeit
_codecs_tw          dis                 parser              tkColorChooser
_collections        distutils           pdb                 tkCommonDialog
_csv                doctest             pickle              tkFileDialog
_ctypes             dumbdbm             pickletools         tkFont
_ctypes_test        dummy_thread        pipes               tkMessageBox
_elementtree        dummy_threading     pkgutil             tkSimpleDialog
_functools          email               platform            toaiff
_heapq              encodings           plistlib            token
_hotshot            errno               popen2              tokenize
_io                 exceptions          poplib              trace
_json               fcntl               posix               traceback
_locale             filecmp             posixfile           ttk
_lsprof             fileinput           posixpath           tty
_md5                fnmatch             pprint              turtle
_multibytecodec     formatter           profile             types
_multiprocessing    fpformat            pstats              unicodedata
_osx_support        fractions           pty                 unittest
_pyio               ftplib              pwd                 urllib
_random             functools           py_compile          urllib2
_sha                future_builtins     pyclbr              urlparse
_sha256             gc                  pydoc               user
_sha512             genericpath         pydoc_data          uu
_socket             getopt              pyexpat             uuid
_sre                getpass             quopri              warnings
_strptime           gettext             random              wave
_struct             glob                re                  weakref
_symtable           grp                 repr                webbrowser
_sysconfigdata      gzip                resource            whichdb
_testcapi           hashlib             rexec               wsgiref
_threading_local    heapq               rfc822              xdrlib
_warnings           hmac                rlcompleter         xml
_weakref            hotshot             robotparser         xmllib
_weakrefset         htmlentitydefs      runpy               xmlrpclib
abc                 htmllib             sched               xxsubtype
aifc                httplib             select              zipfile
antigravity         idlelib             sets                zipimport
anydbm              ihooks              sgmllib             
argparse            imaplib             sha                 
```
The total modules in the Ubuntu Python 2.7.5 is 322, while the total modules in CloundLinux python 2.7.5 is 502.

These five modules are in Ubuntu Python 2.7.5 and not in CloudLinux Python 2.7.5:
```
_md5, _sha, _sha256, _sha512 ,_testcapi
```
These 187 modules are in CloudLinu Python 2.7.5 and not in Ubuntu Python 2.7.5:
```
IPy, M2Crypto, OpenSSL, _audit, _bsddb, _cffi_backend, _curses_panel, _dbus_bindings, _dbus_glib_bindings, _elementtree, _hashlib,
_markerlib, _semanage, _snack, _sqlite3, _sqlitecache, _ssl, _tkinter, _yaml, acutil, audit, auparse, autofs_pb2, babel, backports, 
binfmt_misc_pb2, bz2, cffi, cgroup_pb2, chardet, clcommon, clsudo, configobj, core_aarch64_pb2, core_arm_pb2, core_pb2, core_ppc64_pb2, 
core_s390_pb2, core_x86_pb2, cpuinfo_pb2, creds_pb2, cryptography, curl, dbm, dbus, decorator, dl, dmidecode, dmidecodemod, dns, 
drv_libxml2, dsextras, easy_install, engines, enum, ethtool, euca2ools, eventfd_pb2, eventpoll_pb2, ext_file_pb2, fdinfo_pb2, fh_pb2, 
fifo_pb2, file_lock_pb2, firewall, fown_pb2, fs_pb2, fsnotify_pb2, gdbm, ghost_file_pb2, gi, gio, glib, gobject, gpgme, gudev, hacks, 
hwdata, idna, imageop, images, iniparse, inventory_pb2, iotop, ipaddr, ipaddress, ipc_desc_pb2, ipc_msg_pb2, ipc_sem_pb2, ipc_shm_pb2, 
ipc_var_pb2, isc, jinja2, kitchen, liblzma, libxml2, libxml2mod, lve_pb2, lxml, lzma, macvlan_pb2, magic, markupsafe, mm_pb2, mnt_pb2, 
netdev_pb2, nis, ns_pb2, opts_pb2, packet_sock_pb2, pagemap_pb2, paramiko, pb2dict, pdb, perf, pipe_data_pb2, pipe_pb2, pkg_resources, 
ply, policycoreutils, procfs, progressbar, pstree_pb2, pyasn1, pycparser, pycriu, pycurl, pygtk, pygtkcompat, pylve, pynche, pyparsing, 
pyudev, pyzor, readline, regfile_pb2, remap_file_path_pb2, requestbuilder, requests, rhn, rlimit_pb2, rpm, rpmUtils, sa_pb2, schedutils, 
seccomp_pb2, secureio, selinux, semanage, seobject, sepolgen, sepolicy, setuptools, siginfo_pb2, signalfd_pb2, simplejson, sit_pb2, six, 
sk_inet_pb2, sk_netlink_pb2, sk_opts_pb2, sk_packet_pb2, sk_unix_pb2, slip, snack, sqlitecachec, stats_pb2, sysctl_pb2, tcp_stream_pb2, 
time_pb2, timer_pb2, timerfd_pb2, timing, tty_pb2, tun_pb2, tuned, urlgrabber, urllib3, userns_pb2, utsns_pb2, validate, vma_pb2, xattr, 
yaml, yum, yumutils, zlib
```
In writing Python programs on the simulator computer which will later be used on the cmrailtrail.org.au computer, then avoid importing any of the above 192 modules.


Note that he Python 3 that is installed on the simulaton may still be used. Launch it with `$ python3`
```
cmrailtr@CMRT-Demo:~/python_source/Python-2.7.5$ python3
Python 3.12.3 (main, Jun 18 2025, 17:59:45) [GCC 13.3.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> 
```

Whereis python2.7 and how big is it?
```
cmrailtr@CMRT-Demo:~/python_source/Python-2.7.5$ whereis python2.7
python2.7: /usr/local/bin/python2.7 /usr/local/lib/python2.7

cmrailtr@CMRT-Demo:~/python_source/Python-2.7.5$ ls -l /usr/local/bin/python2.7
-rwxr-xr-x 1 root root 6844608 Jun 28 18:04 /usr/local/bin/python2.7
```

The Python 2.7.5 source code .tgz file and the source code off the `Python-2.7.5` may be removed. From the ~/ home file:
WARNING: Be careful when using the bash rm command to remove files and directories
```
cmrailtr@CMRT-Demo:~$ rm -rf python_source
```



```
