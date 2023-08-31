This is openSSL 1.0.2.2107 for AIX 7.1, 7.2 and 7.3 which contains the latest version OpenSSL 1.0.2u along with additional vulnerability fixes as noted below

***********
NOTE
***********
Support for openssl 1.0.2 version will be discontinued by End of 2023.
Customers are adviced to update to openssl 1.1.1, 3.0 or later versions.
This is the last fileset released under 1.0.2 version.


SECTION I   - Vulnerabilities fixed
SECTION II  - Other Information 
SECTION III - Differences between deprecated OpenSSL RPM and the OpenSSL installp package
SECTION IV  - SUPPORT POLICY


---------
SECTION I
---------

OpenSSL 1.0.2.2107 addresses all vulnerabilties reported upto and including openssl 1.0.2zi version shown below :

CVE-2023-3817 Excessive time spent checking DH q parameter value 

CVE-2023-3446 Excessive time spent checking DH keys and parameters

CVE-2023-2650 Possible DoS translating ASN.1 object identifiers 

CVE-2023-0465 Invalid certificate policies in leaf certificates are silently ignored

CVE-2023-0466 Certificate policy check not enabled

CVE-2023-0464 Excessive Resource Usage Verifying X.509 Policy Constraints

CVE-2023-0286: X.400 address type confusion in X.509 GeneralName

CVE-2023-0215: Use-after-free following BIO_new_NDEF

CVE-2022-4304: Timing Oracle in RSA Decryption

CVE-2022-2068: The c_rehash script allows command injection

CVE-2022-1292: The c_rehash script allows command injection

CVE-2022-0778: Infinite loop in BN_mod_sqrt() reachable when parsing certificates 

CVE-2021-3712: Read buffer overruns processing ASN.1 strings 

CVE-2021-23839: Incorrect SSLv2 rollback protection 

CVE-2021-23840: Integer overflow in CipherUpdate

CVE-2021-23841: Null pointer deref in X509_issuer_and_serial_hash()

CVE-2020-1968: Raccoon attack 

CVE-2020-1971: EDIPARTYNAME NULL pointer dereference 


Additionally contains the following fixes:
- Openssl update to exploit crypto hardware accelerator on Power10.
- DISPLAY_PATCH_VERSION configuration option:
  When this option is set 'yes' in /var/ssl/ssl_version.cnf then the community
  openssl version from which the vulnerability is patched will be displayed
  instead of build version.

----------
SECTION II
----------
A. OpenSSL 1.0.2.2107 version contains other fixes that were part of earlier releases:
- Missing shared objects in 64-bit libssl library 
- TS002131610: RSA keys not properly generated in 64-bit library
- APAR IJ14769: ssh dumps core after lpm
- APAR IJ11962: degraded openssl performance on P8 and P9
- Others: 
         Change in c_rehash script to use absolute path.
         Signature generation fails
- Provide support to display IBM openssl VRMF as output of openssl version command.
	Set DISPLAY_IBM_VERSION=yes in /var/ssl/ssl_version.cnf config file to display IBM openssl VRMF.
- Support for installation of Openssl fileset in Relocatable location
- Support for .crt files for ca-certificates package
- Execute updtvpkg during the post install of openssl fileset
- ship .pc files as part of fileset
B. An additional library libcrypto.a.min has been added which is required for secure boot. This contains only the unversioned shared object.

-----------
SECTION III
-----------

1. Libraries libssl.a, libcrypto.a, libcrypto.a.min will be installed in /usr/lib path.

2. Header files will be installed in /usr/include/openssl.

3. Binaries openssl,openssl64 will be installed in /usr/bin.

4. LICENSE,README will be installed in /usr/openssl.

5. Openssl configuration file will be installed in /var/ssl path.

6. Openssl tools will be made available in /var/ssl/misc.

7. In the 32-bit case,
      - libcrypto.a contains libcrypto.so, libcrypto.so.1.0.0, libcrypto.so.0.9.8 and libcrpto.so.1.0.2 shared objects.
      - libssl.a contains libssl.so, libssl.so.1.0.0, libssl.so.0.9.8 and libssl.1.0.2 shared objects.

8. In the 64-bit case,
      - libcrypto.a contains libcrypto64.so, libcrypto64.so.1.0.0, libcrypto64.so.0.9.8, libcrypto.so, libcrypto.so.0.9.8, libcrypto.so.1.0.0 and libcrypto.so.1.0.2 .
      - libssl.a contains libssl64.so, libssl64.so.1.0.0, libssl64.so.0.9.8, libssl.so, libssl.so.0.9.8, libssl.so.1.0.0 & libssl.so.1.0.2 .

9. To ensure that applications are aware of which version of openssl shared object is used libcrypto.so.1.0.2 and libssl.1.0.2 is introduced.
   Symbols will be exported from these shared objects, and henceforth any application compiled will get linked to these version shared objects.

10. libcrypto.so.0.9.8 (32-bit & 64-bit), libcrypto64.so.0.9.8, libssl.so.0.9.8(32-bit & 64-bit), libssl64.so.0.9.8 are from OpenSSL v0.9.8.2507 release

11. Unversioned shared objects are copies of versioned 1.0.2 shared object. That is
    - libcrypto.so is copy of libcrypto.so.1.0.2, libcrypto64.so.1.0.0 shared objects.
    - libcrypto64.so is copy of 64-bit libcrypto.so.1.0.2
    - libssl.so is copy of libssl.so.1.0.2
    - libssl64.so is copy of 64-bit libssl.so.1.0.2
    - However, all the above 4 shared objects are stripped and will not be exporting symbol. These are kept only for backward compatibility.

12. Remaining versioned shared objects are also copies of versioned 1.0.2 shared object. That is
    - libcrypto.so.1.0.0 is copy of libcrypto.so.1.0.2
    - libcrypto64.so.1.0.0 is copy of 64-bit libcrypto.so.1.0.2
    - 64-bit libcrypto.so.1.0.0 is copy of 64-bit libcrypto.so.1.0.2
    - libssl.so.1.0.0 is copy of libssl.so.1.0.2
    - libssl64.so.1.0.0 is copy of 64-bit libssl.so.1.0.2
    - 64-bit libssl.so.1.0.0 is copy of 64-bit libssl.so.1.0.2
    - However, all the above 4 shared objects are stripped and will not be exporting symbol. These are kept only for backward compatibility.

13. Support for MD2 hash algorithm has been disabled

14. The Openssl installp would contain the following filesets,
   openssl.base    - Mainly contains the libraries libcrypto.a,libssl.a, binaries openssl,openssl64,header files and README.
   openssl.license - Contains the License files.
   openssl.man     - Contains the Man files.

15. Support for PKCS11, which was part of openSSL 1.0.1.5xx fileset, has been removed.

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