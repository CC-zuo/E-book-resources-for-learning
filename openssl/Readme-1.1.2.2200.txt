This is the readme file of openSSL 1.1.2.2200 VRMF for AIX 7.1, 7.2 and 7.3 which contains openssl 1.1.1v version

*******
NOTE:
*******
The libraries provided as part of this fileset are built using "no-idea no-rc5 no-weak-ssl-ciphers no-psk no-srp" compile time options.
Hence these libraries are considered as 'strong-ciphers' supported libraries, compared to openssl 1.1.1.xxxx VRMF libraries where 'all-ciphers' are supported.

The library shared objects of this version will be provided in openssl 3.0 version.
Hence, customers are adviced to use this fileset for compilation with openssl 1.1.1 version libraries.


SECTION I   - Vulnerabilities fixed
SECTION II  - Other Information 
SECTION III - Differences between deprecated OpenSSL RPM and the OpenSSL installp package
SECTION IV  - SUPPORT POLICY

---------
SECTION I
---------

OpenSSL 1.1.2.2200 addresses all vulnerabilities reported upto and including openssl 1.1.1v version.

The following are the vulnerabilities fixed in openssl 1.1.1v version:
CVE-2023-3817 Excessive time spent checking DH q parameter value 
CVE-2023-3446 Excessive time spent checking DH keys and parameters
CVE-2023-2650 Possible DoS translating ASN.1 object identifiers 
CVE-2023-0465 Invalid certificate policies in leaf certificates are silently ignored
CVE-2023-0466 Certificate policy check not enabled
CVE-2023-0464 Excessive Resource Usage Verifying X.509 Policy Constraints

This fileset also has the following additional fixes:

CVE-2023-0286: X.400 address type confusion in X.509 GeneralName
CVE-2023-0215: Use-after-free following BIO_new_NDEF
CVE-2022-4450: Double free after calling PEM_read_bio_ex
CVE-2022-4304: Timing Oracle in RSA Decryption
Openssl update to exploit crypto hardware accelerator on Power10.
DISPLAY_PATCH_VERSION:
        Set DISPLAY_PATCH_VERSION=yes in in /var/ssl/ssl_version.cnf to display
        community openssl version from which the vulnerability is patched instead of build version.

----------
SECTION II
----------
A. OpenSSL 1.1.2.2200 version provides support to display IBM openssl VRMF as output of openssl version command.
   Set DISPLAY_IBM_VERSION=yes in /var/ssl/ssl_version.cnf config file to display IBM openssl VRMF.

-----------
SECTION III
-----------

1. Libraries libssl.a, libcrypto.a, libcrypto.a.min will be installed in /usr/lib path.

2. Header files will be installed in /usr/include/openssl.

3. Binaries openssl,openssl64 will be installed in /usr/bin.

4. LICENSE,README will be installed in /usr/openssl.

5. Openssl configuration file will be installed in /var/ssl path.

6. Openssl tools will be available in /var/ssl/misc.

7. There are various versioned shared object versions(.so) provided within openssl library(.a) to maintain compatibility as listed below
   These shared objects can be listed using ar -tv <-X64> /usr/lib/library_name(libcrypto.a or libssl.a) command 

   libcrypto.a contains the following shared objects :
   libcrypto.so
   libcrypto.so.1.0.0
   libcrypto.so.0.9.8
   libcrpto.so.1.0.2
   libcrypto.so.1.1

   libcrypto.a also contains the following 64-bit shared objects : 
   libcrypto64.so
   libcrypto64.so.1.0.0
   libcrypto64.so.0.9.8
   libcrypto.so
   libcrypto.so.0.9.8
   libcrypto.so.1.0.0
   libcrypto.so.1.0.2
   libcrypto.so.1.1

   libssl.a contains the following shared objects :
   libssl.so
   libssl.so.1.0.0
   libssl.so.0.9.8
   libssl.1.0.2
   libssl.so.1.1

   libssl.a also contains the following 64-bit shared objects :
   libssl64.so
   libssl64.so.1.0.0
   libssl64.so.0.9.8
   libssl.so
   libssl.so.0.9.8
   libssl.so.1.0.0
   libssl.so.1.0.2
   libssl.so.1.1

8. From the various shared objects listed above
   The following shared objects are provided only for backward compatibility purpose with applications that use 0.9.8 version of shared object :
   libcrypto.so.0.9.8(32-bit)
   libcrypto64.so.0.9.8 (copy of 64-bit libcrypto.so.0.9.8)
   libcrypto.so.0.9.8(64-bit)

   libssl.so.0.9.8(32-bit)
   libssl64.so.0.9.8 (copy of 64-bit libssl.so.0.9.8)
   libssl.so.0.9.8(64-bit) 
   These shared objects are from AIX OpenSSL with VRMF 0.9.8.2507

   The following shared objects are provided only for backward compatibility purpose with applications that use 1.0.2 version of shared object :
   libcrypto.so (copy of 32-bit libcrpto.so.1.0.2)
   libcrypto.so.1.0.0 (copy of 32-bit libcrpto.so.1.0.2)
   libcrpto.so.1.0.2 (32-bit)
   libcrypto64.so (copy of 64-bit libcrpto.so.1.0.2)
   libcrypto64.so.1.0.0 (copy of 64-bit libcrpto.so.1.0.2)
   libcrypto.so  (copy of 64-bit libcrpto.so.1.0.2)
   libcrypto.so.1.0.0  (copy of 64-bit libcrpto.so.1.0.2)
   libcrypto.so.1.0.2 (64-bit)

   libssl.so  (copy of 32-bit libssl.so.1.0.2)
   libssl.so.1.0.0  (copy of 32-bit libssl.so.1.0.2)
   libssl.1.0.2 (32-bit)
   libssl64.so  (copy of 64-bit libssl.so.1.0.2)
   libssl64.so.1.0.0  (copy of 64-bit libssl.so.1.0.2)
   libssl.so  (copy of 64-bit libssl.so.1.0.2)
   libssl.so.1.0.0  (copy of 64-bit libssl.so.1.0.2)
   libssl.so.1.0.2 (64-bit)
   Note that, most of the existing AIX applications which are dependent on openssl library, are linking with libssl.so.1.0.2 and 
   libcrypto.so.1.0.2 shared objects.
   These shared objects are from AIX OpenSSL with VRMF 1.0.2.2106 which contains the latest version OpenSSL 1.0.2u along with
   addressing all vulnerabilties reported till openssl 1.0.2zg version.

   The following shared objects are newly introduced in the library of this fileset :
   libcrypto.so.1.1 (32-bit)
   libcrypto.so.1.1 (64-bit)

   libssl.so.1.1 (32-bit)
   libssl.so.1.1 (64-bit)
   These are the shared objects which are exporting symbols, and any application compiled with libcrypto.a or libssl.a will get 
   linked to these shared objects
   Applications that are required to make use of openssl 1.1.1 version capabilities has to be recompiled with the libraries provided
   as part of this fileset.


9. Following files are kept same as 1.0.2 version : libcrypto.a.min, and openssl.cnf
   libcrypto.a.min contains only 32-bit and 64-bit libcrypto.so of 1.0.2 version.

10. Support for MD2 hash algorithm has been disabled

11. The Openssl installp would contain the following filesets,
    openssl.base    - Mainly contains the libraries libcrypto.a,libssl.a, binaries openssl,openssl64,header files and README.
    openssl.license - Contains the License files.
    openssl.man     - Contains the Man files.

12. Support for PKCS11, which was part of openSSL 1.0.1.5xx fileset, has been removed.

--------------
SUPPORT POLICY
--------------
For those customers with an agreement for software maintenance for AIX (SWMA),
IBM will provide support for OpenSSL in accordance with SWMA.

-----------------------------------------------------------------------------
Revision:
-----------------------------------------------------------------------------
Date: 29th August 2023
Initial release
--------------------- E N D - O F - D O C U M E N T -------------------------
