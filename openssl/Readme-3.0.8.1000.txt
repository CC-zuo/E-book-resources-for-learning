This is the readme file of openSSL 3.0.8.1000 VRMF for AIX 7.1, 7.2 and 7.3 which contains openssl 3.0.8 version

This readme is divided into following sections:
SECTION I   - Vulnerabilities related information
SECTION II  - VRMF specific information 
SECTION III - Additional information 
SECTION IV  - Support Policy

---------
SECTION I
---------

OpenSSL 3.0.8.1000 addresses all vulnerabilities reported upto and including openssl 3.0.8 version.

Vulnerabilities fixed in openssl 3.0.8 version:

1. CVE-2023-0401: NULL dereference during PKCS7 data verification

2. CVE-2023-0286: X.400 address type confusion in X.509 GeneralName

3. CVE-2023-0217: NULL dereference validating DSA public key

4. CVE-2023-0216: Invalid pointer dereference in d2i_PKCS7 functions

5. CVE-2023-0215: Use-after-free following BIO_new_NDEF

6. CVE-2022-4450: Double free after calling PEM_read_bio_ex

7. CVE-2022-4304: Timing Oracle in RSA Decryption

8. CVE-2022-4203: X.509 Name Constraints Read Buffer Overflow

9. CVE-2022-3996: Fixed X.509 Policy Constraints Double Locking

----------
SECTION II
----------

1. Configure option used in openssl 3.0.8.1000 VRMF: "--api=1.0.2 no-deprecated no-idea no-rc5 no-weak-ssl-ciphers no-psk no-srp"
   This includes support for APIs that are deprecated from 1.0.2

2. The following defect has been addressed in this VRMF:
   - Fix issue related to exploiting crypto hardware accelerator on Power10.

3. Other AIX specific features retained:
i. Support to display vulnerability patched version as output of openssl version command:
        Set DISPLAY_PATCH_VERSION=yes in /var/ssl/ssl_version.cnf to display community
        openssl version from which the vulnerability is patched.
ii.Support to display IBM openssl VRMF as output of openssl version command. 
        Set DISPLAY_IBM_VERSION=yes in /var/ssl/ssl_version.cnf to display IBM openssl VRMF.

4. This version is not fully backward compatible with 1.1.1 and below openssl versions.
   Some of the compatibility issues are removal of weak ciphers, no engine support etc. 
   New feature added in 3.0 openssl version are support for TLS version 1.3, introduction of provider concepts etc. 
   For complete information about this, please refer to https://www.openssl.org/docs/man3.0/man7/migration_guide.html

   There are new symbols introduced in openssl config file /var/ssl/openssl.cnf. 
   Hence it is advised to backup old configuration before installation.

-----------
SECTION III
-----------

1. Libraries libssl.a, libcrypto.a, libcrypto.a.min will be installed in /usr/lib path.

2. legacy.so provider will be installed at /usr/lib/ossl-modules/32 and /usr/lib/ossl-modules/64

3. Header files will be installed in /usr/include/openssl.

4. Binaries openssl, openssl64 will be installed in /usr/bin.

5. LICENSE, README will be installed in /usr/openssl.

6. Openssl configuration file will be installed in /var/ssl path.

7. Openssl tools will be available in /var/ssl/misc.

8. There are various versioned shared object (.so) provided within openssl library(.a) to maintain compatibility as listed below
   These shared objects can be listed using ar -tv <-X64> /usr/lib/library_name(libcrypto.a or libssl.a) command 

   libcrypto.a contains the following shared objects :
   libcrypto.so
   libcrypto.so.1.0.0
   libcrypto.so.1.0.2
   libcrypto.so.1.1
   libcrypto.so.3

   libcrypto.a also contains the following 64-bit shared objects : 
   libcrypto64.so
   libcrypto64.so.1.0.0
   libcrypto.so
   libcrypto.so.1.0.0
   libcrypto.so.1.0.2
   libcrypto.so.1.1
   libcrypto.so.3

   libssl.a contains the following shared objects :
   libssl.so
   libssl.so.1.0.0
   libssl.so.1.0.2
   libssl.so.1.1
   libssl.so.3

   libssl.a also contains the following 64-bit shared objects :
   libssl64.so
   libssl64.so.1.0.0
   libssl.so
   libssl.so.1.0.0
   libssl.so.1.0.2
   libssl.so.1.1
   libssl.so.3


9. From the various shared objects listed above
  
   The following shared objects are provided only for backward compatibility purpose with applications that use 1.0.2 version of shared object :

   libcrypto.so (copy of 32-bit libcrypto.so.1.0.2)
   libcrypto.so.1.0.0 (copy of 32-bit libcrypto.so.1.0.2)
   libcrpto.so.1.0.2 (32-bit)
   libcrypto64.so (copy of 64-bit libcrypto.so.1.0.2)
   libcrypto64.so.1.0.0 (copy of 64-bit libcrypto.so.1.0.2)
   libcrypto.so  (copy of 64-bit libcrypto.so.1.0.2)
   libcrypto.so.1.0.0  (copy of 64-bit libcrypto.so.1.0.2)
   libcrypto.so.1.0.2 (64-bit)

   libssl.so  (copy of 32-bit libssl.so.1.0.2)
   libssl.so.1.0.0  (copy of 32-bit libssl.so.1.0.2)
   libssl.so.1.0.2 (32-bit)
   libssl64.so  (copy of 64-bit libssl.so.1.0.2)
   libssl64.so.1.0.0  (copy of 64-bit libssl.so.1.0.2)
   libssl.so  (copy of 64-bit libssl.so.1.0.2)
   libssl.so.1.0.0  (copy of 64-bit libssl.so.1.0.2)
   libssl.so.1.0.2 (64-bit)
   
   Note that, most of the existing AIX applications which are dependent on openssl library link with libssl.so.1.0.2 and libcrypto.so.1.0.2 shared objects.
   These shared objects are from AIX OpenSSL with VRMF 1.0.2.2106 which contains the latest version OpenSSL 1.0.2u along with
   security vulnerability fixes reported upto and including openssl 1.0.2zg version.

   
   The following shared objects are provided only for backward compatibility purpose with applications that use 1.1 (strong ciphers support) version shared object :

   libcrypto.so.1.1 (32-bit)
   libcrypto.so.1.1 (64-bit)

   libssl.so.1.1 (32-bit)
   libssl.so.1.1 (64-bit) 
   
   These shared objects are from AIX OpenSSL with VRMF 1.1.2.2000 which contains 1.1.1t openssl version.

   The following shared objects are newly introduced in the library of this fileset :
   libcrypto.so.3 (32-bit)
   libcrypto.so.3 (64-bit)

   libssl.so.3 (32-bit)
   libssl.so.3 (64-bit)
   
   These are the shared objects which export symbols, and any application compiled with libcrypto.a or libssl.a will get linked to these shared objects.
   Applications that are required to make use of openssl 3.0.8 version capabilities has to be recompiled with the libraries provided as part of this
   fileset.
 
NOTE: In Openssl 3.0.8.1000 - 
	
	The shared objects of OpenSSL version 0.9.8 are no longer supported and hence 3.0 libraries doesn't contain 0.9.8 shared objects.
	libcrypto_compat.a and libssl_compat.a libraries have been removed.

	The command line tool openssl and openssl64 is linked with shared object of OpenSSL 3.0. 
      Note that there could be compatibility issue while using these commands and also new options are added to these commands. 

10. libcrypto.a.min is kept same-as provided in 1.0.2 version.It contains 32-bit and 64-bit libcrypto.so of 1.0.2 version.

11. Support for MD2 hash algorithm has been disabled

12. The Openssl installp would contain the following filesets,
   openssl.base    - Mainly contains the libraries libcrypto.a, libssl.a, binaries openssl, openssl64, header files and README.
   openssl.license - Contains the License files.
   openssl.man     - Contains the Man files.

13. Support for PKCS11, which was part of openSSL 1.0.1.5xx fileset, has been removed.

14. For any additional information on migrating to 3.0, community provided migration guide can also be referred: 
    https://www.openssl.org/docs/manmaster/man7/migration_guide.html

--------------
SUPPORT POLICY
--------------
For those customers with an agreement for software maintenance for AIX (SWMA),
IBM will provide support for OpenSSL in accordance with SWMA.

-----------------------------------------------------------------------------
Revision:
-----------------------------------------------------------------------------
Date: 8th March 2023
Initial release
