
https://think.hm/docs/90266/standalone/

Permissions: Grant write access to public, private and ext directories on Linux server

In most Linux distributions, the web server runs with a special user+group (such as www-data or www).

You must specifically grant access for this user to write to data folders. Typically you will want to grant access for the group www-data to private, public and ext folders.

cd /var/www/example.com/web

chmod 2770 private public ext
chmod g+rwX -R private public ext
chgrp -R www-data private public ext




 Use the octal CHMOD Command:

chmod -R 2770 folder_name
OR use the symbolic CHMOD Command:

chmod -R a+rwx,o-rwx,ug+s,+t,u-s,-t folder_name

Chmod 2770 (chmod a+rwx,o-rwx,ug+s,+t,u-s,-t) sets permissions so that, 

(U)ser / owner can read, can write and can execute. 
(G)roup can read, can write and can execute. 
(O)thers can't read, can't write and can't execute.

===

ian@hp:~/testx$ ls -l
total 4
-rw-rw-r-- 1 ian ian    0 May 11 11:20 test
drwxrwxr-x 2 ian ian 4096 May 11 11:22 testy
ian@hp:~/testx$ chmod 2770 testy
ian@hp:~/testx$ ls -l
total 4
-rw-rw-r-- 1 ian ian    0 May 11 11:20 test
drwxrws--- 2 ian ian 4096 May 11 11:22 testy
ian@hp:~/testx$ chmod g+rwX -R testy
ian@hp:~/testx$ ls -l
total 4
-rw-rw-r-- 1 ian ian    0 May 11 11:20 test
drwxrws--- 2 ian ian 4096 May 11 11:22 testy
ian@hp:~/testx$ 
ian@hp:~/testx$ chgrp -R www-data testy
ian@hp:~/testx$ ls -l
total 4
-rw-rw-r-- 1 ian ian         0 May 11 11:20 test
drwxrws--- 2 ian www-data 4096 May 11 11:22 testy


===
For files

After changing a file's mode to 2770 the file's mode will be displayed in Unix style file lsting as:
-rwxrws---
For folders

After changing a directory's mode to 2770 the folder's mode will be displayed in Unix style file lsting as:
drwxrws---




The s you are seeing in the "execute" position in the user and group column are the SetUID (Set User ID on Execution) and SetGID (Set Group ID on execution) bits.

Unix file permissions are actually a 4-digit octal number SUGO

    S controls the SetUID (4), SetGID (2) and "Sticky" (1) bits
    U controls Read(4)/Write(2)/Execute(1) bits for the file owner
    G controls the Read/Write/Execute bits for the file's group
    O controls the Read/Write/Execute bits for everyone else.



To clear the setuid bit on a directory on Linux, use chmod 00755; see unix.stackexchange.com/q/393531/46851 – 
Roger Lipscombe
Commented Mar 26, 2019 at 8:11


http://en.wikipedia.org/wiki/Setuid

In Unix-like systems, the access rights flags setuid and setgid (short for set user identity and set group identity)[1] 
allow users to run an executable with the file system permissions of the executable's owner or group respectively and to change behaviour in directories. They are often used to allow users on a computer system to run programs with temporarily elevated privileges to perform a specific task. While the assumed user id or group id privileges provided are not always elevated, at a minimum they are specific. 

Effects

The setuid and setgid flags have different effects, depending on whether they are applied to a file, to a directory or binary executable or non-binary executable file. The setuid and setgid flags have an effect only on binary executable files and not on scripts (e.g., Bash, Perl, Python).[3] 



When set on a directory

Setting the setgid permission on a directory causes files and subdirectories created within to inherit its group ownership, rather than the primary group of the file-creating process. Created subdirectories also inherit the setgid bit. The policy is only applied during creation and, thus, only prospectively. Directories and files existing when the setgid bit is applied are unaffected, as are directories and files moved into the directory on which the bit is set.

This allows a group of users to work with files without explicitly setting permissions, but limited by the security model expectation that existing files permissions do not implicitly change.

This is generally not needed on most systems derived from BSD, since by default directories are treated as if their setgid bit is always set, regardless of the actual value.[6]

On FreeBSD, setting the setuid bit on a directory on a UFS file system mounted with the suiddir option causes files and subdirectories created within to inherit its ownership, rather than the user ID of the file-creating process.[

=====

In most Linux distributions, the web server runs with a special user+group (such as `www-data` or `www`).

You must specifically grant access for this user to write to data folders. Typically you will want to grant access for the group `www-data` to `private`, `public` and `ext` folders.

cd /var/www/example.com/web

chmod 2770 private public ext
chmod g+rwX -R private public ext
chgrp -R www-data private public ext


Should we recommend `setfacl` (Linux) and `chmod +a` (MacOS)? Or is this assuming that current-user is also in `www-data`?
These are the configs I've liked: https://github.com/amp-cli/amp/blob/0.7.3/app/defaults/services.yml#L189-L199

=====




Standalone sites should have a main folder which in Standalone is known as the _"project root"_.

After the system has been fully installed and used, you can expect the contents of that folder to look like this:

| File/Folder | Contents |
| -- | -- |
| `civicrm.standalone.php` | Standalone boot file. This identifies the Standalone Project Root, and identifies the locations of the CiviCRM code and settings files. |
| `core/`                     | Core source code for CiviCRM |
| `private/`                          | Private site files which should not be accessible over the web |
| `private/civicrm.settings.php`      | Configuration file with low level settings for CiviCRM. |
| `private/log/`             | Log files |
| `private/cache/`             | Cache files for CiviCRM's template compiler |
| `private/l10n/`             | Translation files |
| `private/attachment/`             | Private files uploaded to your CiviCRM site - such as files uploaded to a specific contact |
| `public/`                          | Public site files which *should* be accessible over the web |
| `public/media/`                  | Public files uploaded to your site, like images that appear on a contribution page or in a mass email |
| `public/ang/`                  | Angular templates - e.g. for custom forms added to your site with FormBuilder |
| `ext/`                  | CiviCRM extensions you have added to your site |

<!-- FIXME: Describe more items from `web/upload/` -->


https://beta.docs.civicrm.org/installation/standalone/


==== 

video

civicrm-standalone

files directly 

move civicrm files in civicrm-standalone to public_html


