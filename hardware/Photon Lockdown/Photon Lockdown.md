# lesson learned
- importance of scoping the search - paying attention for the file size
- extracting compressed squashfs files
- 
# challenge description 

We've located the adversary's location and must now secure access to their Optical Network Terminal to disable their internet connection.
Fortunately, we've obtained a copy of the device's firmware, which is suspected to contain hardcoded credentials. 
Can you extract the password from it?
## note
- The goal is to find any credentialds/password in the firmware copy

# enum
Checking the filetype of the rootfs file
```
$ file *  
fwu_ver: ASCII text  
hw_ver:  X1 archive data  
rootfs:  Squashfs filesystem, little endian, version 4.0, zlib compressed, 10936182 bytes, 910 inodes, blocksize: 131072 bytes, created: Sun Oct  1 07:02:43 2023
```

```
$ ls -la 
-rw-r--r-- 1 september september        6 Oct 11  2023 fwu_ver  
-rw-r--r-- 1 september september        3 Oct 11  2023 hw_ver  
-rw-r--r-- 1 september september 10936320 Oct  1  2023 rootfs
```
the file rootfs is by far the biggest, It is a [squashfs](https://en.wikipedia.org/wiki/SquashFS) compressed read-only file , following the  size it might contain the root filesystem.
To extract the data from a SquashFS file (unsquashfs)  
```
sudo unsquashfs rootfs                                                               
Parallel unsquashfs: Using 3 processors  
865 inodes (620 blocks) to write  
  
[====================================================================================================================================================|] 1485/1485 100%  
  
created 440 files  
created 45 directories  
created 187 symlinks  
created 238 devices  
created 0 fifos  
created 0 sockets  
created 0 hardlinks
```

locate files  that has password
```
$ grep -lr password                                                  
etc/config_default.xml  
etc/smb.conf  
etc/wscd.conf  
bin/cwmpClient  
bin/spppd  
bin/wscd  
bin/ftpd  
bin/updatedd  
bin/cupsd  
bin/hsinfo  
bin/omci_app  
bin/backend/ipp  
bin/boa  
bin/oamcli  
bin/omcicli  
bin/busybox  
bin/Upgrade  
bin/mib  
bin/eponoamd  
bin/ftp  
bin/configd  
bin/diag  
bin/loadconfig  
bin/samba_multicall  
bin/flash  
bin/saveconfig  
lib/omci/mib_Ontg.so  
lib/omci/mib_SIPUserData.so  
lib/libcrypto.so.1.1  
lib/libmib.so  
lib/libut.so  
lib/voip/voice_rtk_wrapper.so  
lib/librtk.so  
lib/libcups.so.2
```
we got 34 folders with `password`  
```
$grep -lr password | wc -l       
34
```
start with the first file `etc/config_default.xml  ` seems like a defualt config with xml format 
![](https://github.com/sinSeptember/CTF/blob/main/hardware/flag.png))
