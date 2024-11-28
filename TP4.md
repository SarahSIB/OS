# I.Clean install - 3.Verification

sarah@vbox:~$ sudo lsblk
[sudo] Mot de passe de sarah :
NAME                 MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
sda                    8:0    0   20G  0 disk
└─sda1                 8:1    0   20G  0 part
  ├─groupe-swap      254:0    0  1,9G  0 lvm  [SWAP]
  ├─groupe-root      254:1    0  9,3G  0 lvm  /
  ├─groupe-home      254:2    0  1,9G  0 lvm  /home
  ├─groupe-var       254:3    0  2,8G  0 lvm  /var
  └─groupe-espacelib 254:4    0  2,8G  0 lvm
sr0                   11:0    1 1024M  0 rom

sarah@vbox:~$ df -h
Sys. de fichiers        Taille Utilisé Dispo Uti% Monté sur
udev                      951M       0  951M   0% /dev
tmpfs                     197M    1,5M  196M   1% /run
/dev/mapper/groupe-root   9,1G    5,7G  3,0G  66% /
tmpfs                     984M       0  984M   0% /dev/shm
tmpfs                     5,0M    8,0K  5,0M   1% /run/lock
/dev/mapper/groupe-var    2,7G    639M  1,9G  25% /var
/dev/mapper/groupe-home   1,8G    1,3G  483M  73% /home
tmpfs                     197M    124K  197M   1% /run/user/1000
tmpfs                     197M     68K  197M   1% /run/user/114

# 4. Tailles et Inodes

sarah@vbox:~$ df -i
Sys. de fichiers        Inœuds IUtil. ILibre IUti% Monté sur
udev                    243442    435 243007    1% /dev
tmpfs                   251812    875 250937    1% /run
/dev/mapper/groupe-root 610800 178953 431847   30% /
tmpfs                   251812      1 251811    1% /dev/shm
tmpfs                   251812      5 251807    1% /run/lock
/dev/mapper/groupe-var  183264  11918 171346    7% /var
/dev/mapper/groupe-home 121920   5793 116127    5% /home
tmpfs                    50362    133  50229    1% /run/user/1000
tmpfs                    50362     84  50278    1% /run/user/114

sarah@vbox:~$ du -h /boot/vmlinuz-6.1.0-27-amd64  && ls -i /boot/vmlinuz-6.1.0-27-amd64
7,9M    /boot/vmlinuz-6.1.0-27-amd64
260626 /boot/vmlinuz-6.1.0-27-amd64

# II. Partitioning -1 disk

sarah@vbox:~$ lsblk
NAME                 MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
sda                    8:0    0   10G  0 disk
sdb                    8:16   0   10G  0 disk
sdc                    8:32   0   20G  0 disk
└─sdc1                 8:33   0   20G  0 part
  ├─groupe-swap      254:0    0  1,9G  0 lvm  [SWAP]
  ├─groupe-root      254:1    0  9,3G  0 lvm  /
  ├─groupe-home      254:2    0  1,9G  0 lvm  /home
  ├─groupe-var       254:3    0  2,8G  0 lvm  /var
  └─groupe-espacelib 254:4    0  2,8G  0 lvm
sr0                   11:0    1 1024M  0 rom

sarah@vbox:~$ sudo pvcreate /dev sdb
Physical volume "/dev/sdb" successfully created.
sarah@vbox:~$ sudo pvcreate /dev/sdc
Physical volume "/dev/sdc" successfully created.
sarah@vbox:~$ sudo vgcreate cat /dev/sdb /dev/sdc
Volume group "cat" successfully created

sarah@vbox:~$ sudo lvcreate -L 3G -n meoooow cat
Logical volume "meoooow" created.

sarah@vboxbc@abc:~$ lsblk
NAME          MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
sda             8:0    0   20G  0 disk
└─sda1          8:1    0   20G  0 part
├─ok-root   254:0    0  9.3G  0 lvm  /
├─ok-swap   254:1    0  1.9G  0 lvm  [SWAP]
├─ok-home   254:2    0  1.9G  0 lvm  /home
└─ok-var    254:3    0  2.8G  0 lvm  /var
sdb             8:16   0   10G  0 disk
└─cat-meoooow 254:4    0    3G  0 lvm
sdc             8:32   0   10G  0 disk
sr0            11:0    1 1024M  0 rom



sarah@vbox:~$ sudo apt install btrfs-progs
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following additional packages will be installed:
  liblzo2-2
Suggested packages:
  duperemove
The following NEW packages will be installed:
  btrfs-progs liblzo2-2
0 upgraded, 2 newly installed, 0 to remove and 0 not upgraded.
Need to get 811 kB of archives.
After this operation, 4,769 kB of additional disk space will be used.
Do you want to continue? [Y/n] Y
Get:1 http://deb.debian.org/debian bookworm/main amd64 liblzo2-2 amd64 2.10-2 [56.9 kB]
Get:2 http://deb.debian.org/debian bookworm/main amd64 btrfs-progs amd64 6.2-1+deb12u1 [754 kB]
Fetched 811 kB in 1s (1,161 kB/s)
Selecting previously unselected package liblzo2-2:amd64.
(Reading database ... 113761 files and directories currently installed.)
Preparing to unpack .../liblzo2-2_2.10-2_amd64.deb ...
Unpacking liblzo2-2:amd64 (2.10-2) ...
Selecting previously unselected package btrfs-progs.
Preparing to unpack .../btrfs-progs_6.2-1+deb12u1_amd64.deb ...
Unpacking btrfs-progs (6.2-1+deb12u1) ...
Setting up liblzo2-2:amd64 (2.10-2) ...
Setting up btrfs-progs (6.2-1+deb12u1) ...
Processing triggers for man-db (2.11.2-2) ...
Processing triggers for initramfs-tools (0.142+deb12u1) ...
update-initramfs: Generating /boot/initrd.img-6.1.0-27-amd64
Processing triggers for libc-bin (2.36-9+deb12u9) ...
sarah@vbox:~$ sudo mkfs.btrfs /dev/mapper/cat-meoooow
btrfs-progs v6.2
See http://btrfs.wiki.kernel.org for more information.

NOTE: several default settings have changed in version 5.15, please make sure
      this does not affect your deployments:
      - DUP for metadata (-m dup)
      - enabled no-holes (-O no-holes)
      - enabled free-space-tree (-R free-space-tree)

Label:              (null)
UUID:               c3b0326d-8c2e-448c-9c40-2b684b1bb856
Node size:          16384
Sector size:        4096
Filesystem size:    3.00GiB
Block group profiles:
  Data:             single            8.00MiB
  Metadata:         DUP             256.00MiB
  System:           DUP               8.00MiB
SSD detected:       no
Zoned device:       no
Incompat features:  extref, skinny-metadata, no-holes
Runtime features:   free-space-tree
Checksum:           crc32c
Number of devices:  1
Devices:
ID        SIZE  PATH
1     3.00GiB  /dev/mapper/cat-meoooow

sarah@vbox:~$ sudo mkdir /mnt/meow
sarah@vbox:~$ ls -ld /mnt/meow
drwxr-xr-x 2 root root 4096 Nov 17 14:01 /mnt/meow

sarah@vbox:~$ sudo mount /dev/mapper/cat-meoooow /mnt/meow

sarah@vbox:~$ df -h /mnt/meow
Filesystem               Size  Used Avail Use% Mounted on
/dev/mapper/cat-meoooow  3.0G  5.8M  2.5G   1% /mnt/meow

sarah@vbox:~$ sudo lvextend -L +2G /dev/ok/home
Size of logical volume ok/home changed from <1.86 GiB (476 extents) to <3.86 GiB (988 extents).
Logical volume ok/home successfully resized.
sarah@vbox:~$ sudo resize2fs /dev/ok/home
resize2fs 1.47.0 (5-Feb-2023)
Filesystem at /dev/ok/home is mounted on /home; on-line resizing required
old_desc_blocks = 1, new_desc_blocks = 1
The filesystem on /dev/ok/home is now 1011712 (4k) blocks long.

sarah@vbox:~$ df -h /home
Filesystem           Size  Used Avail Use% Mounted on
/dev/mapper/ok-home  3.8G  1.6M  3.6G   1% /home

sarah@vbox:~$ sudo vgs
  VG  #PV #LV #SN Attr   VSize   VFree
  cat   2   1   0 wz--n-  19.99g 16.99g
  ok    1   4   0 wz--n- <20.00g  2.17g
sarah@vbox:~$ sudo lvextend -l +100%FREE /dev/cat/meoooow
  Size of logical volume cat/meoooow changed from 3.00 GiB (768 extents) to 19.99 GiB (5118 extents).
  Logical volume cat/meoooow successfully resized.
  sarah@vbox:~$ sudo btrfs filesystem resize max /mnt/meow
Resize device id 1 (/dev/mapper/cat-meoooow) from 3.00GiB to max
sarah@vbox:~$ df -h
Filesystem               Size  Used Avail Use% Mounted on
udev                     448M     0  448M   0% /dev
tmpfs                     97M 1020K   96M   2% /run
/dev/mapper/ok-root      9.1G  4.0G  4.7G  46% /
tmpfs                    481M     0  481M   0% /dev/shm
tmpfs                    5.0M     0  5.0M   0% /run/lock
/dev/mapper/ok-home      3.8G  1.6M  3.6G   1% /home
/dev/mapper/ok-var       2.7G  368M  2.2G  15% /var
tmpfs                     97M   52K   97M   1% /run/user/1000
tmpfs                     97M   48K   97M   1% /run/user/108
/dev/mapper/cat-meoooow   20G  5.8M   20G   1% /mnt/meow

sarah@vbox:~$ lsblk -f
NAME          FSTYPE      FSVER    LABEL UUID                                   FSAVAIL FSUSE% MOUNTPOINTS
sda
└─sda1        LVM2_member LVM2 001       5p4Mxx-aRB1-14n5-znPx-hNrv-E4SX-YsEbdl
  ├─ok-root   ext4        1.0            73fdb08c-912b-4ec9-aed9-1ff1cace002f      4.7G    43% /
  ├─ok-swap   swap        1              38fac470-c2c8-4e82-9332-c05b94660cff                  [SWAP]
  ├─ok-home   ext4        1.0            11c123f7-681d-4d95-a708-ade43dfef8a8      3.6G     0% /home
  └─ok-var    ext4        1.0            e1f58f05-6f87-4f3b-8620-ad4309ad8e0f      2.2G    13% /var
sdb           LVM2_member LVM2 001       Biyi8r-aDI2-VlfR-S0Km-juPE-SjCt-dTVG4g
└─cat-meoooow btrfs                      c3b0326d-8c2e-448c-9c40-2b684b1bb856     19.5G     0% /mnt/meow
sdc           LVM2_member LVM2 001       erTzzU-04pK-Ghq1-q1o7-yZRH-1yKF-5ygWCR
└─cat-meoooow btrfs                      c3b0326d-8c2e-448c-9c40-2b684b1bb856     19.5G     0% /mnt/meow
sr0


