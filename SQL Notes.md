## SQL notes

### Filtering out the old revisions

When viewing the Wordpress database *wp_posts* table, there may be many entries that are old revisions of web-pages.

The total fields in the wp_posts is:

The following shows a selection of wp_posts columns

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
|  6 |           1 | 2025-05-28 07:19:09 | CiviCRM v6     | page             |
|  7 |           1 | 2025-05-28 07:18:09 | Custom Styles  | wp_global_styles |
| 11 |           1 | 2025-05-28 23:32:13 | CiviCRM v4     | revision         |
| 12 |           1 | 2025-05-28 23:32:32 | CiviCRM v5     | revision         |
| 13 |           1 | 2025-05-29 00:18:04 | CiviCRM v6     | revision         |
| 14 |           1 | 2025-05-29 08:22:17 | CiviCRM v6     | revision         |
+----+-------------+---------------------+----------------+------------------+
11 rows in set (0.000 sec)
```

Notice that *ID* entries 11 to 14 have a *post_type* of `revision`. 

The SQL command to display the above without the entries that are revisions is:

```
MariaDB [wordpress]> select ID, post_author, post_date, post_title, post_type from wp_posts where not post_type = "revision";
+----+-------------+---------------------+----------------+------------------+
| ID | post_author | post_date           | post_title     | post_type        |
+----+-------------+---------------------+----------------+------------------+
|  1 |           1 | 2025-05-27 10:49:09 | Hello world!   | post             |
|  2 |           1 | 2025-05-27 10:49:09 | Sample Page    | page             |
|  3 |           1 | 2025-05-27 10:49:09 | Privacy Policy | page             |
|  4 |           0 | 2025-05-27 10:49:09 | Navigation     | wp_navigation    |
|  5 |           1 | 2025-05-27 10:51:08 | Auto Draft     | post             |
|  6 |           1 | 2025-05-28 07:19:09 | CiviCRM v6     | page             |
|  7 |           1 | 2025-05-28 07:18:09 | Custom Styles  | wp_global_styles |
+----+-------------+---------------------+----------------+------------------+
7 rows in set (0.001 sec)
```
