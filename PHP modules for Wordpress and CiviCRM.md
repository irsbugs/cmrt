## PHP modules that should be installed for Wordpress and CiviCRM

https://make.wordpress.org/hosting/handbook/server-environment/

###PHP modules that should be installed for Wordpress

    apcu
    bc
    curl 
    dom 
    exif 
    fileinfo 
    filter
    ftp
    hash 
    iconv 
    igbinary
    image 
    ImageMagick
    imagick  <-- (requires ImageMagick >= 6.2.4) 
    intl 
    json 
    mbstring 
    memcached 
    mysqli 
    mysqlnd <-- Can be deleted using mysqli - mysql is EOL
    opcache
    openssl 
    pcre 
    redis
    shmop
    simplexml 
    sockets
    sodium
    ssh2  
    timezonedb
    xml 
    xmlreader  
    zip 
    zlib 


  Above list with dependency notes.    	
    apcu	
    bc	
    curl 	 (PHP >= 8.0 requires libcurl >= 7.29.0 ; PHP >= 8.4 requires libcurl >= 7.61.0)
    dom 	 (requires libxml)
    exif 	 (requires php
    fileinfo 	 (bundled in PHP)
    filter	
    ftp	
    hash 	 (bundled in PHP >=5.1.2)
    iconv 	 (requires libiconv/POSIX)
    igbinary	
    image 	 (requires libgd >= 2.1.0; requires zlib >= 1.2.0.4; optional freetype2)
    ImageMagick  	  (recommended ImageMagick >= 7.1) 
    imagick 	 equires ImageMagick >= 6.2.4)
    intl 	 HP >= 7.4.0 requires ICU >= 50.1)
    json 	 (bundled in >=8.0.0)
    mbstring 	
    memcached 	 (requires libmemcached >= 1.0.0)
    mysqli 	 (bundled in >=5.0.0), 
    mysqlnd	
    opcache	
    openssl 	 PHP >= 8.4 requires OpenSSL >= 1.1.1 / < 4.0)
    pcre 	 (bundled in PHP >= 7.0 recommended PCRE 8.10)
    redis	
    shmop	
    simplexml 	 (requires libxml)
    sockets	
    sodium	
    ssh2  	 (requires OpenSSL and libssh >= 1.2; recommended libssh >= 1.2.9)
    timezonedb	
    xml 	 (requires libxml)
    xmlreader  	 (requires libxml)
    zip 	 (requires libzip >= 0.11; recommended libzip >= 1.6)
    zlib 	 (requires zlib >= 1.2.0.4)

      
###  CiviCRM documentation on PHP modules required...

https://docs.civicrm.org/installation/en/latest/requirements/

Required for CiviCRM Core¶

*bcmath - BCMath - required for calculating financial values in CiviCRM Core.
curl - Curl - required for many payment processors, the extension manager, and the CiviCRM News dashlet.
dom - DOM XML - required by CiviCase.
mbstring - Multibyte - required for internationalisation and proper encoding of fields.
zip - Zip - required for unzipping auto-downloaded extensions so they can be installed from the browser.
intl - INTL - required for outputting localized formatted number strings from CiviCRM 5.28 onwards
fileinfo - File Information - required for spreadsheet support from 5.44 onwards

Required for Third-Party Functionality or CiviCRM Extensions¶
* soap - SOAP - required to use the SOAP processor (required for the CiviSMTP service)

Only need to add bcmath and soap after ensuring all Wordpress php reqirements have been met.
      
