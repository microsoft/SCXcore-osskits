# System Center Cross Platform Provider for Operations Manager (Open Source Kits)

The files in this directory reflect bundle files for each of our
open-source OMI providers bundled with the System Center Cross
Platform provider. Note that there are no hard-coded file paths
here. Instead, filenames are determined dynamically.

At the time of this README file creation, this directory contains:

    apache-cimprov-1.0.1-3.universal.1.i686.sh
    apache-cimprov-1.0.1-3.universal.1.x86_64.sh
    apache-oss-test.sh
    mysql-cimprov-1.0.1-1.universal.1.i686.sh
    mysql-cimprov-1.0.1-1.universal.1.x86_64.sh
    mysql-oss-test.sh
    README.md

The bundle creation software expects the following for each open-source
provider:

    <provider-name>-oss-test.sh
    <provider-name>-cimprov.*.i686.sh    (Only one match allowed)
    <provider-name>-cimprov.*.x86_64.sh  (Only one match allowed)


It is assumed that each bundle will conform to the following:

1. Will at least create a directory named<br>
   `/opt/microsoft/<provider-name>-cimprov`<br>
   This is used for removal of the package during SCX removal,
2. For purposes of purging, after removal of the kit, the following
   directories will be deleted:
```
/etc/opt/microsoft/<provider-name>-cimprov
/opt/microsoft/<provider-name>-cimprov
/var/opt/microsoft/<provider-name>-cimprov
```

If files are created in other locations, the package should remove the files
as part of the uninstall (purge) process.

Bundle creation software works as follows: For each *-oss-test.sh file,
** Include the file itself into the bundle,
** Include the associated i686.sh file for i386 builds,
** Include the associated x86_64.sh file for x86_64 builds

Bundle installation works as follows: For each *-oss-test.sh file,
** Run the file.
** If it returns 0, that means that the associated bundle file should be
installed (otherwise, the associated bundle file is NOT installed).


To add a new OSS provider to this directory, do the following:

1. Create <provider>-oss-test.sh file to determine if bundle should be installed,
2. Check in associated <provider>-cimprov-*.sh binary bundle files
(built for release and for distribution to customers). Two should
be checked in, one ending in .i686.sh and another ending in .x86_64.sh.

If you are updating old kits, remove the old kits, add the new kits, and commit.