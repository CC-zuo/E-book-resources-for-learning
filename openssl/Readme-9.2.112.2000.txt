This is OpenSSH-9.2p1 (VRMF: 9.2.112.2000) for AIX 7.1, 7.2 and AIX 7.3. 

This version of OpenSSH is compiled with OpenSSL 1.1.1t version. Hence, the required minimum level of openssl fileset installed has to be at :
- 1.1.2.2000 (for customers using strong ciphers only)

Please note that:
1. This fileset installation will fail if any version of 0.9.8, 1.0.1 or 1.0.2 openSSL is installed on the system. 
2. The behavior of ssh is unpredictable if any version of openssl below 1.1.1t is installed on the system.

It is recommended that the latest version of OpenSSL be used to address known security vulnerabilities.
OpenSSL can be downloaded from IBM site:
https://www.ibm.com/resources/mrs/assets/packageList?source=aixbp&lang=en_US


-----------------------------------------------------------------------------
I) Releases:
-----------------------------------------------------------------------------

OpenSSH version 9.2p1: VRMF: 9.2.112.2000

Changes in this version :
-------------------------

1. New options added between 8.1p1 and 9.2p1 community version :

scp
-A - Allows forwarding of ssh-agent(1) to the remote system. The default is not to forward an authentication agent.
-O - Use the legacy SCP protocol for file transfers instead of the SFTP protocol.
-R - Copies between two remote hosts are performed by connecting to the origin host and executing scp there.
-D sftp_server_path - Connect directly to a local SFTP server program rather than a remote one via ssh(1). 
-X sftp_option - Specify an option that controls aspects of SFTP protocol behaviour.

sftp
-D sftp_server_command (in place of [-D sftp_server_path]) - Connect directly to a local sftp server (rather than via ssh).
-X sftp_option - Specify an option that controls aspects of SFTP protocol behaviour.

ssh-keygen
-a rounds - When saving a private key, this option specifies the number of KDF (key derivation function) rounds used. 
-O option - Specify a key/value option. 
-t dsa | ecdsa | ecdsa-sk | ed25519 | ed25519-sk | rsa - New possible values are "ecdsa-sk" & "ed25519-sk"
-w provider - Specifies a path to a library that will be used when creating FIDO authenticator-hosted keys, overriding the default of using the internal USB HID support.
-Z cipher - Specifies the cipher to use for encryption when writing an OpenSSH-format private key file. 
-M generate - Generate candidate Diffie-Hellman Group Exchange (DH-GEX) parameters 
	The desired length of the primes may be specified by the -O bits option. For example:
	# ssh-keygen -M generate -O bits=2048 moduli-2048.candidates
	A number of options are available for moduli generation and screening via the -O flag:
		lines=number
 		start-line=line-number
  		checkpoint=filename
  		memory=mbytes
		start=hex-value
		generator=value
-M screen - Screen candidate parameters for Diffie-Hellman Group Exchange. 
-Y find-principals - Find the principal(s) associated with the public key of a signature, provided using the -s flag in an authorised signers file provided using the -f flag.
-Y match-principals - Find principal matching the principal name provided using the -I flag in the authorized signers file specified using the -f flag. 

ssh-agent
-O option - Specify an option when starting ssh-agent. 
[-P allowed_providers] in place of [-P pkcs11_whitelist] is being used.

ssh-add
-H hostkey_file - Specifies a known hosts file to look up hostkeys when using destination-constrained keys via the -h flag.
-h destination_constraint - When adding keys, constrain them to be usable only through specific hosts or to specific destinations.

sshd
-V - Display the version number and exit.

sftp-server
[-P denied_requests] in place of [-P blacklisted_requests] is being used.
[-p allowed_requests] in place of [-p whitelisted_requests] is being used.


2. Deprecated option:
ssh-keygen
-G - It was used to generate candidate primes for DH-GEX. But now, we use "-M generate" option for generation of primes.

3. Deprecated Cipher:
rijndael-cbc@lysator.liu.se is deprecated & no longer used.

4. Fix for CVE-2023-28531 : ssh-add in OpenSSH before 9.3 adds smartcard keys to ssh-agent without the intended per-hop 
   destination constraints. The earliest affected version is 8.9.

For complete list of supported and non-supported features refer to openssh community release notes : https://www.openssh.com/releasenotes.html

This version includes other fixes part of previous fileset release:
-------------------------------------------------------------------------------------------------------
Fix for APAR Draft 17902: sshd may corrupt SYSENVIRON and affect at jobs
Fix for APAR IJ40247: sshd memory leak and core when multiplexing/connection sharing
Fix for Apar Draft 17855 : ssh public key authentication fails if no password defined
Fix for APAR IJ38179 : sshd won't work in Trusted Aix environment.
Fix for CVE-2021-41617 : privilege escalation when AuthorizedKeysCommand/AuthorizedPrincipalsCommand are configured
Fix for APAR IJ32806 : A PIPED COMMAND TO SSH COULD RETURN EAGAIN.
Fix for APAR IJ33264 : OPENSSH 8.X DOES NOT SET PAG VALUE
Introducing new configuration option fipsforopenssh which enforces the following configuration:
  - PubkeyAcceptedKeyTypes rsa-sha2-256,rsa-sha2-512,ecdsa-sha2-nistp256,ecdsa-sha2-nistp384
  - Ciphers aes128-ctr,aes256-ctr,aes128-cbc,aes256-cbc,aes128-gcm@openssh.com,aes256-gcm@openssh.com
  - MACs hmac-sha1,hmac-sha2-256,hmac-sha2-512
  - KexAlgorithms ecdh-sha2-nistp256,ecdh-sha2-nistp384,ecdh-sha2-nistp521
  - DRBG uses aes256-ctr as the default
Addition of a new configuration option EnableHwCompression to make use of Hardware compression feature in Power9 and above
Fix for case TS004154625 : Problems with EFS and CHROOT
Fix for case TS004259337 : Match group could fail for openssh/sshd
Fix for case TS004983362 : nohup <command> & does not work as expected via ssh
Fix for APAR IJ31964: ldap name become case sensitive
Fixed man pages of 8.1 version
Feature addition to support hardware compression provided in Power 9 through libzNX library.
New openssh.base fails during 71c install
Incorect signature seen with 6.0 ssh server 
Hash mic verify error seen with 7.5 ssh server when gssapi keyex is enable.
APAR 16156: SSH may overwrite server key files during upgrade.
APAR 16396: ldap user unable to login
Windows server does not works with AIX SSH client
TS002773362 : scp -C command fails.
APAR 15764 : ssh may allow wrong case in username
openssh EFS autokeystoreopen authentcation failed error
Error in trustchklog during update installation
Signature generation fails.
APAR IJ15009: Winbind users can no longer login via ssh
APAR IJ15189: sshd daemon is not starting on AIX5.3
RFE 132022: show ssh arguments in process table
APAR IV99241: locked accounts are able to log in via SSH
APAR IJ05383: sshd crash with kerberos
APAR IJ07376: sshd does not honor loginretries
APAR IJ11428: ssh may not exit when sent a SIGTERM 
APAR IJ03680: compression broken in OpenSSH7.5
APAR IJ02099: Allowpkcs12keystoreautoopen fails in openssh 7 server.
APAR IJ03122: openssh 7.5 does not create user's home directory
APAR IJ05383: sshd crash with kerberos
APAR IJ01208: man pages broken in OpenSSH7.5
APAR IV94291: scp/sftp file copy performance drops in openssh 7.1
APAR IV97965: The default cipher list of sshd is incorrect
RFE 120277: Enhancement to ignore ?AllowPKCS12keystoreAutoOpen? on the destination AIX server  
            for non-AIX ssh clients request

-----------------------------------------------------------------------------
II) Addition Information:
-----------------------------------------------------------------------------
- Support for ssh Protocol 1 is removed by OpenSSH community 
- Support for TCP_Wrappers is removed by OpenSSH community
- PermitRootLogin has been set to yes in /etc/ssh/sshd_config file 
- Default behavior for DSA keys has been changed by community as it is a weak key and not recommended
- Ciphers blowfish-cbc, cast128-cbc, arcfour, arcfour128, arcfour256 are no longer supported by the community.
- Macs hmac-ripemd160, hmac-ripemd160@openssh.com, hmac-ripemd160-etm@openssh.com are no longer supported by the community.
- Following configuration recommendations are made and can be uncommented to get the required GSSAPI function. To get them active on your machine, uncomment them and restart sshd.
---------------------------------------------
	In /etc/ssh/ssh_config file:
	# GSSAPIAuthentication yes
	# GSSAPIDelegateCredentials yes
	# GSSAPIKeyExchange yes
	# GSSAPITrustDNS yes
	# GSSAPIRenewalForcesRekey yes

	In /etc/ssh/sshd_config file:
	# KerberosAuthentication yes
	# KerberosTicketCleanup yes
	# GSSAPIAuthentication yes
	# GSSAPICleanupCredentials yes
	# GSSAPIKeyExchange yes 
	# GSSAPIStoreCredentialsOnRekey yes
----------------------------------------------
- Encrypted File System [EFS] support with Public Key authentication is allowed only with config option "FingerprintHash md5" set in /etc/ssh/sshd_config and /etc/ssh/ssh_config.

- If a user with expired password tries to login, then there will be prompt to change password and user will have to relogin.

- From release OpenSSH 7.5.102.1600, there is a change of existing behavior in EFS functionality: 
  - Please note that for 'auto open of EFS keystore' functionality, both the SSH server and client machine need to be update to openSSH 7.5.102.1600 version and above.
  - If only AIX SSH client machine is updated to openSSH 7.5.102.1600 version or above, and:
    - when configured with AIX SSH server, then 'auto open of EFS keystore' functionality will fail.
      - This can be rectified by updating AIX SSH server to openSSH 7.5.102.1600 version or above
    - when configured with non-AIX server, then connection terminates with message 'Authentication failed'.
      - This can be rectified by adding the line
        AllowPKCS12keystoreAutoOpen no 
        in /etc/ssh/ssh_config file 
  - If only AIX SSH server machine is updated to openSSH 7.5.102.1600 version or above, then 'auto open of EFS keystore' functionality will fail irrespective of connecting
    from AIX / non-AIX SSH client machine. 
- If the user wants to enable hardware compression then the keyword 'EnableHwCompression' should be added in both ssh_config and sshd_config with value as 'yes' as below. 
        EnableHwCompression yes
     By default this keyword will not be there in config file. This means when compression is enabled either through configuration or with -C option then software compression happens 
with system provided libz.a library. If user specifies for Hardware compression using above keyword with 'yes' then Hardware compression happens. When this keyword is set to 'yes', 
then openssh will make use of hardware compression library for AIX 7.2 and above and exploit the Power9 hardware compression functionality

-----------------------------------------------------------------------------
III) Known Limitations:
-----------------------------------------------------------------------------
- ssh sessions will not function properly when the user root is disabled in Enhanced RBAC mode on the server side (by using the setsecconf command)
- ssh daemon fails when started by RBAC user
- EFS is currently not enabled for default fingerprint hash on OpenSSH8.1 with SHA256
- EFS with Public Key authentication along with non-RSA keys fails
- ssh -C fails if it is configured for 'auto open of EFS keystore' functionality.
- Unsupported flags from AIX: ssh -w <tunnel device> and ssh -I pkcs & ssh-keygen -D pkcs
- Compatibility issue : when either of ssh server or client is updated to this version and when kerberos gssapi key  exchange is enabled, 
  then this version is not compatible with 8.1.102.2000 VRMF openssh  version. It can be worked around by updating both server and client to latest version

-----------------------------------------------------------------------------
IV) Revision:
-----------------------------------------------------------------------------
Date: 27th June 2023
Initial release

Date : 4th August 2023
Update readme to add CVE fixed details

--------------------- E N D - O F - D O C U M E N T ---------------------



用pikpak打开