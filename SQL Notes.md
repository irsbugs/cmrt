## SQL notes

### CMRT Database for Wordpress.
The *Wordpess* normally has a naming convention of prefixing everything with *wp_*.
Thus the table *posts* is normally *wp_posts*.

The way the CMRT wordpress has been set up the prefix is *bsen_*, so *posts* are *bsen_posts*.

### Filtering out the old revisions in wp-posts

When viewing the Wordpress database *wp_posts* table, there may be many entries that are old revisions of web-pages.

The total fields (columns) in the *wp_posts* are:

```
MariaDB [wordpress]> show columns from wp_posts;
+-----------------------+---------------------+------+-----+---------------------+----------------+
| Field                 | Type                | Null | Key | Default             | Extra          |
+-----------------------+---------------------+------+-----+---------------------+----------------+
| ID                    | bigint(20) unsigned | NO   | PRI | NULL                | auto_increment |
| post_author           | bigint(20) unsigned | NO   | MUL | 0                   |                |
| post_date             | datetime            | NO   |     | 0000-00-00 00:00:00 |                |
| post_date_gmt         | datetime            | NO   |     | 0000-00-00 00:00:00 |                |
| post_content          | longtext            | NO   |     | NULL                |                |
| post_title            | text                | NO   |     | NULL                |                |
| post_excerpt          | text                | NO   |     | NULL                |                |
| post_status           | varchar(20)         | NO   |     | publish             |                |
| comment_status        | varchar(20)         | NO   |     | open                |                |
| ping_status           | varchar(20)         | NO   |     | open                |                |
| post_password         | varchar(255)        | NO   |     |                     |                |
| post_name             | varchar(200)        | NO   | MUL |                     |                |
| to_ping               | text                | NO   |     | NULL                |                |
| pinged                | text                | NO   |     | NULL                |                |
| post_modified         | datetime            | NO   |     | 0000-00-00 00:00:00 |                |
| post_modified_gmt     | datetime            | NO   |     | 0000-00-00 00:00:00 |                |
| post_content_filtered | longtext            | NO   |     | NULL                |                |
| post_parent           | bigint(20) unsigned | NO   | MUL | 0                   |                |
| guid                  | varchar(255)        | NO   |     |                     |                |
| menu_order            | int(11)             | NO   |     | 0                   |                |
| post_type             | varchar(20)         | NO   | MUL | post                |                |
| post_mime_type        | varchar(100)        | NO   |     |                     |                |
| comment_count         | bigint(20)          | NO   |     | 0                   |                |
+-----------------------+---------------------+------+-----+---------------------+----------------+
23 rows in set (0.001 sec)

```
The *post_type* provides information like, `post`, `page`, and `revision`. The `revision` indicates that it is an old version of a previous `post` or `page` that has been superseded.

The following shows a selection of *wp_posts* columns with the *CiviCRM* post having been edited multiple times, and hence it has four `revision`'s.

The `ID` that was initially assigned to the page when it was created, remains the same after any page is edited and re-published. The old revision of the *wp_posts* record is appended to the table and assigned the next highest `ID`. 

```
MariaDB [wordpress]> select ID, post_name, post_date, post_title, post_type from wp_posts;
+----+-----------------------------------+---------------------+----------------+------------------+
| ID | post_name                         | post_date           | post_title     | post_type        |
+----+-----------------------------------+---------------------+----------------+------------------+
|  1 | hello-world                       | 2025-05-27 10:49:09 | Hello world!   | post             |
|  2 | sample-page                       | 2025-05-27 10:49:09 | Sample Page    | page             |
|  3 | privacy-policy                    | 2025-05-27 10:49:09 | Privacy Policy | page             |
|  4 | navigation                        | 2025-05-27 10:49:09 | Navigation     | wp_navigation    |
|  5 |                                   | 2025-05-27 10:51:08 | Auto Draft     | post             |
|  6 | civicrm                           | 2025-05-28 07:19:09 | CiviCRM v6     | page             |
|  7 | wp-global-styles-twentytwentyfive | 2025-05-28 07:18:09 | Custom Styles  | wp_global_styles |
| 11 | 6-revision-v1                     | 2025-05-28 23:32:13 | CiviCRM v4     | revision         |
| 12 | 6-revision-v1                     | 2025-05-28 23:32:32 | CiviCRM v5     | revision         |
| 13 | 6-revision-v1                     | 2025-05-29 00:18:04 | CiviCRM v6     | revision         |
| 14 | 6-autosave-v1                     | 2025-05-29 08:22:17 | CiviCRM v6     | revision         |
+----+-----------------------------------+---------------------+----------------+------------------+
11 rows in set (0.000 sec)
```

Notice that *ID* entries 11 to 14 have a *post_type* of `revision`. 

The SQL command to display the above without the entries that are revisions is:

```
MariaDB [wordpress]> select ID, post_name, post_date, post_title, post_type from wp_posts where not post_type = "revision";
+----+-----------------------------------+---------------------+----------------+------------------+
| ID | post_name                         | post_date           | post_title     | post_type        |
+----+-----------------------------------+---------------------+----------------+------------------+
|  1 | hello-world                       | 2025-05-27 10:49:09 | Hello world!   | post             |
|  2 | sample-page                       | 2025-05-27 10:49:09 | Sample Page    | page             |
|  3 | privacy-policy                    | 2025-05-27 10:49:09 | Privacy Policy | page             |
|  4 | navigation                        | 2025-05-27 10:49:09 | Navigation     | wp_navigation    |
|  5 |                                   | 2025-05-27 10:51:08 | Auto Draft     | post             |
|  6 | civicrm                           | 2025-05-28 07:19:09 | CiviCRM v6     | page             |
|  7 | wp-global-styles-twentytwentyfive | 2025-05-28 07:18:09 | Custom Styles  | wp_global_styles |
+----+-----------------------------------+---------------------+----------------+------------------+
7 rows in set (0.001 sec)
```

To delete the rows that have a *wp_posts* of `revision` the following SQL command is performed:

```
MariaDB [wordpress]> DELETE FROM wp_posts WHERE post_type = "revision";
```

For example

```
MariaDB [wordpress]> select ID, post_author, post_date, post_title, post_type from wp_posts;

+----+-------------+---------------------+----------------+------------------+
| ID | post_author | post_date           | post_title     | post_type        |
+----+-------------+---------------------+----------------+------------------+
|  1 |           1 | 2025-05-27 10:49:09 | Hello world!   | post             |
|  2 |           1 | 2025-05-27 10:49:09 | Sample Page    | page             |
|  3 |           1 | 2025-05-27 10:49:09 | Privacy Policy | page             |
|  4 |           0 | 2025-05-27 10:49:09 | Navigation     | wp_navigation    |
|  5 |           1 | 2025-05-27 10:51:08 | Auto Draft     | post             |
|  6 |           1 | 2025-05-28 07:19:09 | CiviCRM        | page             |<-- Current active page
|  7 |           1 | 2025-05-28 07:18:09 | Custom Styles  | wp_global_styles |
|  8 |           1 | 2025-05-28 07:19:09 | CiviCRM        | revision         |<-- Old revision of page
+----+-------------+---------------------+----------------+------------------+
8 rows in set (0.000 sec)
```
Using the following command it removes any page that has been flagged as a `revision`.
```
MariaDB [wordpress]> DELETE FROM wp_posts WHERE post_type = "revision";
Query OK, 1 row affected (0.001 sec)
```
The result:
```
MariaDB [wordpress]> select ID, post_author, post_date, post_title, post_type from wp_posts;
+----+-------------+---------------------+----------------+------------------+
| ID | post_author | post_date           | post_title     | post_type        |
+----+-------------+---------------------+----------------+------------------+
|  1 |           1 | 2025-05-27 10:49:09 | Hello world!   | post             |
|  2 |           1 | 2025-05-27 10:49:09 | Sample Page    | page             |
|  3 |           1 | 2025-05-27 10:49:09 | Privacy Policy | page             |
|  4 |           0 | 2025-05-27 10:49:09 | Navigation     | wp_navigation    |
|  5 |           1 | 2025-05-27 10:51:08 | Auto Draft     | post             |
|  6 |           1 | 2025-05-28 07:19:09 | CiviCRM        | page             |<-- Still have the active page
|  7 |           1 | 2025-05-28 07:18:09 | Custom Styles  | wp_global_styles |
+----+-------------+---------------------+----------------+------------------+<-- Old revision entry has gone.
7 rows in set (0.000 sec)
```

### Setting the number of revisions

Wordpress may be setup to limit the number of revisions that exits.
This is done by assigning an integer value to the `WP_POST_REVISIONS` variable.

It is explained here...

https://www.wpkube.com/how-to-disable-post-revisions-in-wordpress/

Adding the following two lines to the wp-config.php file...
```
define( 'WP_POST_REVISIONS', 3 );
define( 'AUTOSAVE_INTERVAL', 600 );
```
...will keep 3 old revisions and increase the autosave time to 600 seconds (Ten minutes).

The autosave feature creates new revisions each time iit performs a save. 


As of the end of May 2025, CMRT Wordpress `bsen_posts` table contained 2406 rows.
Most of these will be revisions of previous posts.

