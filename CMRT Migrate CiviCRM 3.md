# CMRT Migrate CiviCRM 3.md

## The Directories on the Drupal / Spark Essentials System.

The documentation at https://www.beeches.it/civicrm-migration-guide-wordpress-to-standalone/ descibes migrating from a WordPress CMS to CiviCRM Standalone. 

The following is an investigation of the equivalent directories on the Drupal / Spark Essentials to determine if files needs to be migrated. 

## Conclusion

The conclusion is the the currently implementation of *cmrailtrail.civicrm.com* does not have any files to be migrated.


## File migration

File to be migrated should be copied from: 

### ext

Extensions will need to be copied 

On Wordpress: /wp-content/uploads/civicrm/ext on the source 

On Drupal: usa_civi/files/civicrm/ext

EMPTY...
```
ian@hp:~/ken8/mysql_data/usa_civi$ ls -l files/civicrm/ext
total 0
```
...to /ext on the target.

### persist/contribute

Image files typically move from 

On Wordpress: /wp-content/uploads/civicrm/persist/contribute 

On Drupal: usa_civi/files/civicrm/persist/contribute

EMPTY...
```
ian@hp:~/ken8/mysql_data/usa_civi$ ls -l files/civicrm/persist/contribute
total 8
drwxrws--- 2 ian ian 4096 Jun 19 04:26 dyn
drwxrws--- 3 ian ian 4096 Jan 28 10:55 images
-rw-rw---- 1 ian ian    0 Dec 15  2017 index.html
```

...to /public/media.

### custom

Custom files typically move from 

On Wordpress: /wp-content/uploads/civicrm/custom 

On Drupal: usa_civi/files/civicrm/custom/

EMPTY...
```
ian@hp:~/ken8/mysql_data/usa_civi$ tree files/civicrm/custom/
files/civicrm/custom/
├── CiviMail.ignored
│   └── 2026
│       └── 05
│           └── 22
│               ├── cur
│               ├── new
│               └── tmp
└── CiviMail.processed
    └── 2026
        └── 05
            └── 22
                ├── cur
                ├── new
                └── tmp
```

...to /private/attachment.

## All directories on Drupal / Spark Essentials

The equivalent of the Wordpress /wp-content/uploads/civicrm/ in Drupal is /files/civicrm/

Directories from Drupal install in USA

```
ian@hp:~/ken8/mysql_data/usa_civi$ tree -d
.
├── files
│   ├── advagg_css
│   ├── advagg_js
│   ├── civicrm
│   │   ├── ConfigAndLog
│   │   ├── custom  <--- /wp-content/uploads/civicrm/custom 
│   │   │   ├── CiviMail.ignored
│   │   │   │   └── 2026
│   │   │   │       └── 05
│   │   │   │           └── 22
│   │   │   │               ├── cur
│   │   │   │               ├── new
│   │   │   │               └── tmp
│   │   │   └── CiviMail.processed
│   │   │       └── 2026
│   │   │           └── 05
│   │   │               └── 22
│   │   │                   ├── cur
│   │   │                   ├── new
│   │   │                   └── tmp
│   │   ├── dynamic
│   │   ├── ext <--- /wp-content/uploads/civicrm/ext
│   │   ├── persist
│   │   │   └── contribute <--- /wp-content/uploads/civicrm/persist/contribute 
│   │   │       ├── dyn
│   │   │       └── images
│   │   │           └── uploads
│   │   │               ├── static
│   │   │               └── thumbnails
│   │   ├── templates_c
│   │   │   ├── en_AU
│   │   │   │   ├── 00
│   │   │   │   │   ├── 03
│   │   │   │   │   │   └── c3
│ 

...snip.../

│   │   │       │   ├── FD2
│   │   │       │   └── FD7
│   │   │       └── fe
│   │   │           └── e3
│   │   │               └── b0
│   │   └── upload
│   ├── css
│   ├── ctools
│   ├── deployment
│   ├── feeds
│   ├── imagecache
│   ├── images
│   ├── js
│   ├── locations
│   ├── pictures
│   ├── styles
│   ├── tmp
│   └── xmlsitemap
├── libraries
├── modules
│   └── extensions
├── private
│   ├── config
│   │   └── sync
│   ├── files
│   │   ├── backup_migrate
│   │   │   ├── manual
│   │   │   └── scheduled
│   │   ├── civicrm
│   │   │   ├── ConfigAndLog
│   │   │   └── templates_c
│   │   │       └── en_US
│   │   │           ├── 00
│   │   │           │   └── 1c
│   │   │           │       └── 50
│   │   │           ├── 02
│   │   │           │   └── 16
│   │   │           │       └── c6

...snip...

│   │   │           └── fd
│   │   │               └── df
│   │   │                   └── 80
│   │   ├── config
│   │   │   └── sync
│   │   ├── feeds
│   │   └── files
│   │       ├── backup_migrate
│   │       │   ├── manual
│   │       │   └── scheduled
│   │       └── feeds
│   └── temp
├── themes
└── vendor

5231 directories
ian@hp:~/ken8/mysql_data/usa_civi$ 
```

Checking the private directories. All empty...

```
ian@hp:~/ken8/mysql_data/usa_civi$ tree private/config
private/config
└── sync

2 directories, 0 files
ian@hp:~/ken8/mysql_data/usa_civi$ tree private/files/backup_migrate
private/files/backup_migrate
├── manual
└── scheduled

3 directories, 0 files
ian@hp:~/ken8/mysql_data/usa_civi$ tree private/files/civicrm/ConfigAndLog
private/files/civicrm/ConfigAndLog

0 directories, 0 files
ian@hp:~/ken8/mysql_data/usa_civi$ tree private/files/config
private/files/config
└── sync

2 directories, 0 files
ian@hp:~/ken8/mysql_data/usa_civi$ tree private/files/feeds
private/files/feeds

0 directories, 0 files
ian@hp:~/ken8/mysql_data/usa_civi$ tree private/files/files
private/files/files
├── backup_migrate
│   ├── manual
│   └── scheduled
└── feeds

5 directories, 0 files
```
