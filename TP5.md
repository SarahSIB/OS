#I - 1 - 

sarah@vbox:~$ pwd
/home/sarah
sarah@vbox:~$ mkdir work
sarah@vbox:~$ ls
Bureau     Images   Musique  Téléchargements  work
Documents  Modèles  Public   Vidéos
sarah@vbox:~$ cd work
sarah@vbox:~/work$ pwd
/home/sarah/work

#I - 2
sarah@vbox:~/work$ gcc -nostdlib -fno-stack-protector -g -m32 -o hello1 hello1.c

sarah@vbox:~/work$ readelf -h hello1
En-tête ELF:
  Magique:   7f 45 4c 46 01 01 01 00 00 00 00 00 00 00 00 00
  Classe:                            ELF32
  Données:                          complément à 2, système à octets de poids faible d'abord (little endian)
  Version:                           1 (actuelle)
  OS/ABI:                            UNIX - System V
  Version ABI:                       0
  Type:                              DYN (fichier exécutable indépendant de la position)
  Machine:                           Intel 80386
  Version:                           0x1
  Adresse du point d'entrée:         0x1000
  Début des en-têtes de programme :  52 (octets dans le fichier)
  Début des en-têtes de section :    13304 (octets dans le fichier)
  Fanions:                           0x0
  Taille de cet en-tête:             52 (octets)
  Taille de l'en-tête du programme:  32 (octets)
  Nombre d'en-tête du programme:     11
  Taille des en-têtes de section:    40 (octets)
  Nombre d'en-têtes de section:      21
  Table d'index des chaînes d'en-tête de section: 20

sarah@vbox:~/work$ readelf -S hello1
Il y a 21 en-têtes de section, débutant à l'adresse de décalage 0x33f8 :

En-têtes de section :
  [Nr] Nom               Type            Adr      Décala.Taille ES Fan LN Inf Al
  [ 0]                   NULL            00000000 000000 000000 00      0   0  0
  [ 1] .interp           PROGBITS        00000194 000194 000013 00   A  0   0  1
  [ 2] .note.gnu.bu[...] NOTE            000001a8 0001a8 000024 00   A  0   0  4
  [ 3] .gnu.hash         GNU_HASH        000001cc 0001cc 000018 04   A  4   0  4
  [ 4] .dynsym           DYNSYM          000001e4 0001e4 000010 10   A  5   1  4
  [ 5] .dynstr           STRTAB          000001f4 0001f4 000001 00   A  0   0  1
  [ 6] .text             PROGBITS        00001000 001000 00005d 00  AX  0   0  1
  [ 7] .eh_frame_hdr     PROGBITS        00002000 002000 00001c 00   A  0   0  4
  [ 8] .eh_frame         PROGBITS        0000201c 00201c 000058 00   A  0   0  4
  [ 9] .dynamic          DYNAMIC         00003f8c 002f8c 000068 08  WA  5   0  4
  [10] .got.plt          PROGBITS        00003ff4 002ff4 00000c 04  WA  0   0  4
  [11] .comment          PROGBITS        00000000 003000 00001f 01  MS  0   0  1
  [12] .debug_aranges    PROGBITS        00000000 00301f 000020 00      0   0  1
  [13] .debug_info       PROGBITS        00000000 00303f 000070 00      0   0  1
  [14] .debug_abbrev     PROGBITS        00000000 0030af 000062 00      0   0  1
  [15] .debug_line       PROGBITS        00000000 003111 000054 00      0   0  1
  [16] .debug_str        PROGBITS        00000000 003165 000085 01  MS  0   0  1
  [17] .debug_line_str   PROGBITS        00000000 0031ea 00001a 01  MS  0   0  1
  [18] .symtab           SYMTAB          00000000 003204 0000b0 10     19   6  4
  [19] .strtab           STRTAB          00000000 0032b4 00006a 00      0   0  1
  [20] .shstrtab         STRTAB          00000000 00331e 0000d9 00      0   0  1
Clé des fanions :
  W (écriture), A (allocation), X (exécution), M (fusion), S (chaînes), I (info),
  L (ordre des liens), O (traitement supplémentaire par l'OS requis), G (groupe),
  T (TLS), C (compressé), x (inconnu), o (spécifique à l'OS), E (exclu),
  D (mbind), p (processor specific)

  sarah@vbox:~/work$ objdump -M intel -j .text -d hello1

hello1:     format de fichier elf32-i386


Déassemblage de la section .text :

00001000 <_start>:
    1000:       55                      push   ebp
    1001:       89 e5                   mov    ebp,esp
    1003:       57                      push   edi
    1004:       56                      push   esi
    1005:       53                      push   ebx
    1006:       83 ec 10                sub    esp,0x10
    1009:       e8 4b 00 00 00          call   1059 <__x86.get_pc_thunk.ax>
    100e:       05 e6 2f 00 00          add    eax,0x2fe6
    1013:       c7 45 e5 48 65 6c 6c    mov    DWORD PTR [ebp-0x1b],0x6c6c6548
    101a:       c7 45 e9 6f 2c 20 57    mov    DWORD PTR [ebp-0x17],0x57202c6f
    1021:       c7 45 ed 6f 72 6c 64    mov    DWORD PTR [ebp-0x13],0x646c726f
    1028:       c7 45 f0 64 21 0a 00    mov    DWORD PTR [ebp-0x10],0xa2164
    102f:       8d 75 e5                lea    esi,[ebp-0x1b]
    1032:       bf 0e 00 00 00          mov    edi,0xe
    1037:       b8 04 00 00 00          mov    eax,0x4
    103c:       bb 01 00 00 00          mov    ebx,0x1
    1041:       89 f1                   mov    ecx,esi
    1043:       89 fa                   mov    edx,edi
    1045:       cd 80                   int    0x80
    1047:       b8 01 00 00 00          mov    eax,0x1
    104c:       31 db                   xor    ebx,ebx
    104e:       cd 80                   int    0x80
    1050:       90                      nop
    1051:       83 c4 10                add    esp,0x10
    1054:       5b                      pop    ebx
    1055:       5e                      pop    esi
    1056:       5f                      pop    edi
    1057:       5d                      pop    ebp
    1058:       c3                      ret

00001059 <__x86.get_pc_thunk.ax>:
    1059:       8b 04 24                mov    eax,DWORD PTR [esp]
    105c:       c3                      ret

#I - 3

sarah@vbox:~/work$ sudo nano
[sudo] Mot de passe de sarah :
sarah@vbox:~/work$ nano hello2.c
sarah@vbox:~/work$ gcc -fno-stack-protector -g -m32 -o hello2 hello2.c
In file included from hello2.c:1:
/usr/include/stdio.h:27:10: fatal error: bits/libc-header-start.h: Aucun fichier ou dossier de ce type
   27 | #include <bits/libc-header-start.h>
      |          ^~~~~~~~~~~~~~~~~~~~~~~~~~
compilation terminated.
sarah@vbox:~/work$ gcc -fno-stack-protector -g -m32 -o hello2 hello2.c
In file included from hello2.c:1:
/usr/include/stdio.h:27:10: fatal error: bits/libc-header-start.h: Aucun fichier ou dossier de ce type
   27 | #include <bits/libc-header-start.h>
      |          ^~~~~~~~~~~~~~~~~~~~~~~~~~
compilation terminated.
sarah@vbox:~/work$ sudo apt install gcc-multilib -y
Lecture des listes de paquets... Fait
Construction de l'arbre des dépendances... Fait
Lecture des informations d'état... Fait
Les paquets suivants ont été installés automatiquement et ne sont plus nécessaires :
  binutils-i686-linux-gnu binutils-mips-linux-gnu
  binutils-mipsel-linux-gnu binutils-powerpc-linux-gnu
  binutils-powerpc64-linux-gnu binutils-riscv64-linux-gnu
  binutils-sparc64-linux-gnu cpp-12-i686-linux-gnu
  cpp-12-mips-linux-gnu cpp-12-mipsel-linux-gnu
  cpp-12-powerpc-linux-gnu cpp-12-powerpc64-linux-gnu
  cpp-12-riscv64-linux-gnu cpp-12-sparc64-linux-gnu
  cpp-i686-linux-gnu cpp-mips-linux-gnu cpp-mipsel-linux-gnu
  cpp-powerpc-linux-gnu cpp-powerpc64-linux-gnu
  cpp-sparc64-linux-gnu gcc-12-cross-base gcc-12-cross-base-mipsen
  gcc-12-cross-base-ports gcc-12-i686-linux-gnu-base
  gcc-12-mips-linux-gnu-base gcc-12-mipsel-linux-gnu-base
  gcc-12-powerpc-linux-gnu-base gcc-12-powerpc64-linux-gnu-base
  gcc-12-riscv64-linux-gnu-base gcc-12-sparc64-linux-gnu-base
  libasan8-i386-cross libasan8-powerpc-cross libasan8-ppc64-cross
  libasan8-riscv64-cross libasan8-sparc64-cross
  libatomic1-i386-cross libatomic1-mips-cross
  libatomic1-mipsel-cross libatomic1-powerpc-cross
  libatomic1-ppc64-cross libatomic1-riscv64-cross
  libatomic1-sparc64-cross libc6-dev-i386-cross
  libc6-dev-mips-cross libc6-dev-mipsel-cross
  libc6-dev-powerpc-cross libc6-dev-ppc64-cross
  libc6-dev-riscv64-cross libc6-dev-sparc64-cross libc6-i386-cross
  libc6-mips-cross libc6-mipsel-cross libc6-powerpc-cross
  libc6-ppc64-cross libc6-riscv64-cross libc6-sparc64-cross
  libgcc-12-dev-i386-cross libgcc-12-dev-mips-cross
  libgcc-12-dev-mipsel-cross libgcc-12-dev-powerpc-cross
  libgcc-12-dev-ppc64-cross libgcc-12-dev-riscv64-cross
  libgcc-12-dev-sparc64-cross libgcc-s1-i386-cross
  libgcc-s1-mips-cross libgcc-s1-mipsel-cross
  libgcc-s1-powerpc-cross libgcc-s1-ppc64-cross
  libgcc-s1-riscv64-cross libgcc-s1-sparc64-cross
  libgomp1-i386-cross libgomp1-mips-cross libgomp1-mipsel-cross
  libgomp1-powerpc-cross libgomp1-ppc64-cross
  libgomp1-riscv64-cross libgomp1-sparc64-cross libitm1-i386-cross
  libitm1-ppc64-cross libitm1-sparc64-cross liblsan0-ppc64-cross
  libquadmath0-i386-cross libstdc++6-i386-cross
  libstdc++6-powerpc-cross libstdc++6-ppc64-cross
  libstdc++6-sparc64-cross libtsan2-ppc64-cross
  libubsan1-i386-cross libubsan1-powerpc-cross
  libubsan1-ppc64-cross libubsan1-sparc64-cross
  linux-libc-dev-i386-cross linux-libc-dev-mips-cross
  linux-libc-dev-mipsel-cross linux-libc-dev-powerpc-cross
  linux-libc-dev-ppc64-cross linux-libc-dev-riscv64-cross
  linux-libc-dev-sparc64-cross
Veuillez utiliser « sudo apt autoremove » pour les supprimer.
Les paquets supplémentaires suivants seront installés :
  gcc-12-multilib lib32asan8 lib32atomic1 lib32gcc-12-dev
  lib32gcc-s1 lib32gomp1 lib32itm1 lib32quadmath0 lib32stdc++6
  lib32ubsan1 libc6-dev-i386 libc6-dev-x32 libc6-i386 libc6-x32
  libx32asan8 libx32atomic1 libx32gcc-12-dev libx32gcc-s1
  libx32gomp1 libx32itm1 libx32quadmath0 libx32stdc++6 libx32ubsan1
Les paquets suivants seront ENLEVÉS :
  gcc-12-i686-linux-gnu gcc-12-mips-linux-gnu
  gcc-12-mipsel-linux-gnu gcc-12-powerpc-linux-gnu
  gcc-12-powerpc64-linux-gnu gcc-12-riscv64-linux-gnu
  gcc-12-sparc64-linux-gnu gcc-i686-linux-gnu gcc-mips-linux-gnu
  gcc-mipsel-linux-gnu gcc-powerpc-linux-gnu
  gcc-powerpc64-linux-gnu gcc-sparc64-linux-gnu
Les NOUVEAUX paquets suivants seront installés :
  gcc-12-multilib gcc-multilib lib32asan8 lib32atomic1
  lib32gcc-12-dev lib32gcc-s1 lib32gomp1 lib32itm1 lib32quadmath0
  lib32stdc++6 lib32ubsan1 libc6-dev-i386 libc6-dev-x32 libc6-i386
  libc6-x32 libx32asan8 libx32atomic1 libx32gcc-12-dev libx32gcc-s1
  libx32gomp1 libx32itm1 libx32quadmath0 libx32stdc++6 libx32ubsan1
0 mis à jour, 24 nouvellement installés, 13 à enlever et 0 non mis à jour.
Il est nécessaire de prendre 20,2 Mo dans les archives.
Après cette opération, 292 Mo d'espace disque seront libérés.
Réception de :1 http://deb.debian.org/debian bookworm/main amd64 libc6-i386 amd64 2.36-9+deb12u9 [2 459 kB]
Réception de :2 http://deb.debian.org/debian bookworm/main amd64 libc6-dev-i386 amd64 2.36-9+deb12u9 [1 353 kB]
Réception de :3 http://deb.debian.org/debian bookworm/main amd64 libc6-x32 amd64 2.36-9+deb12u9 [2 591 kB]
Réception de :4 http://deb.debian.org/debian bookworm/main amd64 libc6-dev-x32 amd64 2.36-9+deb12u9 [1 518 kB]
Réception de :5 http://deb.debian.org/debian bookworm/main amd64 lib32gcc-s1 amd64 12.2.0-14 [59,7 kB]
Réception de :6 http://deb.debian.org/debian bookworm/main amd64 libx32gcc-s1 amd64 12.2.0-14 [50,2 kB]
Réception de :7 http://deb.debian.org/debian bookworm/main amd64 lib32gomp1 amd64 12.2.0-14 [121 kB]
Réception de :8 http://deb.debian.org/debian bookworm/main amd64 libx32gomp1 amd64 12.2.0-14 [116 kB]
Réception de :9 http://deb.debian.org/debian bookworm/main amd64 lib32itm1 amd64 12.2.0-14 [27,7 kB]
Réception de :10 http://deb.debian.org/debian bookworm/main amd64 libx32itm1 amd64 12.2.0-14 [26,5 kB]
Réception de :11 http://deb.debian.org/debian bookworm/main amd64 lib32atomic1 amd64 12.2.0-14 [7 732 B]
Réception de :12 http://deb.debian.org/debian bookworm/main amd64 libx32atomic1 amd64 12.2.0-14 [9 264 B]
Réception de :13 http://deb.debian.org/debian bookworm/main amd64 lib32asan8 amd64 12.2.0-14 [2 081 kB]
Réception de :14 http://deb.debian.org/debian bookworm/main amd64 libx32asan8 amd64 12.2.0-14 [2 063 kB]
Réception de :15 http://deb.debian.org/debian bookworm/main amd64 lib32stdc++6 amd64 12.2.0-14 [644 kB]
Réception de :16 http://deb.debian.org/debian bookworm/main amd64 lib32ubsan1 amd64 12.2.0-14 [870 kB]
Réception de :17 http://deb.debian.org/debian bookworm/main amd64 libx32stdc++6 amd64 12.2.0-14 [599 kB]
Réception de :18 http://deb.debian.org/debian bookworm/main amd64 libx32ubsan1 amd64 12.2.0-14 [875 kB]
Réception de :19 http://deb.debian.org/debian bookworm/main amd64 lib32quadmath0 amd64 12.2.0-14 [227 kB]
Réception de :20 http://deb.debian.org/debian bookworm/main amd64 libx32quadmath0 amd64 12.2.0-14 [146 kB]
Réception de :21 http://deb.debian.org/debian bookworm/main amd64 lib32gcc-12-dev amd64 12.2.0-14 [2 269 kB]
Réception de :22 http://deb.debian.org/debian bookworm/main amd64 libx32gcc-12-dev amd64 12.2.0-14 [2 041 kB]
Réception de :23 http://deb.debian.org/debian bookworm/main amd64 gcc-12-multilib amd64 12.2.0-14 [1 020 B]
Réception de :24 http://deb.debian.org/debian bookworm/main amd64 gcc-multilib amd64 4:12.2.0-3 [1 520 B]
20,2 Mo réceptionnés en 4s (4 611 ko/s)



(Lecture de la base de données... 174710 fichiers et répertoires déjà installés.)
Suppression de gcc-i686-linux-gnu (4:12.2.0-3) ...
Suppression de gcc-12-i686-linux-gnu (12.2.0-14cross1) ...
Suppression de gcc-mips-linux-gnu (4:12.2.0-4) ...
Suppression de gcc-12-mips-linux-gnu (12.2.0-14cross5) ...
Suppression de gcc-mipsel-linux-gnu (4:12.2.0-4) ...
Suppression de gcc-12-mipsel-linux-gnu (12.2.0-14cross5) ...
Suppression de gcc-powerpc-linux-gnu (4:12.2.0-5) ...
Suppression de gcc-12-powerpc-linux-gnu (12.2.0-13cross1) ...
Suppression de gcc-powerpc64-linux-gnu (4:12.2.0-5) ...
Suppression de gcc-12-powerpc64-linux-gnu (12.2.0-13cross1) ...
Suppression de gcc-12-riscv64-linux-gnu (12.2.0-13cross1) ...
Suppression de gcc-sparc64-linux-gnu (4:12.2.0-5) ...
Suppression de gcc-12-sparc64-linux-gnu (12.2.0-13cross1) ...
Sélection du paquet libc6-i386 précédemment désélectionné.
(Lecture de la base de données... 174357 fichiers et répertoires déjà installés.)
Préparation du dépaquetage de .../00-libc6-i386_2.36-9+deb12u9_amd64.deb ...
Dépaquetage de libc6-i386 (2.36-9+deb12u9) ...
Sélection du paquet libc6-dev-i386 précédemment désélectionné.
Préparation du dépaquetage de .../01-libc6-dev-i386_2.36-9+deb12u9_amd64.deb ...
Dépaquetage de libc6-dev-i386 (2.36-9+deb12u9) ...



Sélection du paquet libc6-x32 précédemment désélectionné.
Préparation du dépaquetage de .../02-libc6-x32_2.36-9+deb12u9_amd64.deb ...
Dépaquetage de libc6-x32 (2.36-9+deb12u9) ...






Sélection du paquet libc6-dev-x32 précédemment désélectionné.
Préparation du dépaquetage de .../03-libc6-dev-x32_2.36-9+deb12u9_amd64.deb ...
Dépaquetage de libc6-dev-x32 (2.36-9+deb12u9) ...
Sélection du paquet lib32gcc-s1 précédemment désélectionné.
Préparation du dépaquetage de .../04-lib32gcc-s1_12.2.0-14_amd64.deb ...
Dépaquetage de lib32gcc-s1 (12.2.0-14) ...
Sélection du paquet libx32gcc-s1 précédemment désélectionné.
Préparation du dépaquetage de .../05-libx32gcc-s1_12.2.0-14_amd64.deb ...
Dépaquetage de libx32gcc-s1 (12.2.0-14) ...
Sélection du paquet lib32gomp1 précédemment désélectionné.
Préparation du dépaquetage de .../06-lib32gomp1_12.2.0-14_amd64.deb ...
Dépaquetage de lib32gomp1 (12.2.0-14) ...
Sélection du paquet libx32gomp1 précédemment désélectionné.
Préparation du dépaquetage de .../07-libx32gomp1_12.2.0-14_amd64.deb ...
Dépaquetage de libx32gomp1 (12.2.0-14) ...
Sélection du paquet lib32itm1 précédemment désélectionné.
Préparation du dépaquetage de .../08-lib32itm1_12.2.0-14_amd64.deb ...
Dépaquetage de lib32itm1 (12.2.0-14) ...
Sélection du paquet libx32itm1 précédemment désélectionné.
Préparation du dépaquetage de .../09-libx32itm1_12.2.0-14_amd64.deb ...
Dépaquetage de libx32itm1 (12.2.0-14) ...
Sélection du paquet lib32atomic1 précédemment désélectionné.
Préparation du dépaquetage de .../10-lib32atomic1_12.2.0-14_amd64.deb ...
Dépaquetage de lib32atomic1 (12.2.0-14) ...
Sélection du paquet libx32atomic1 précédemment désélectionné.
Préparation du dépaquetage de .../11-libx32atomic1_12.2.0-14_amd64.deb ...
Dépaquetage de libx32atomic1 (12.2.0-14) ...
Sélection du paquet lib32asan8 précédemment désélectionné.
Préparation du dépaquetage de .../12-lib32asan8_12.2.0-14_amd64.deb ...
Dépaquetage de lib32asan8 (12.2.0-14) ...
Sélection du paquet libx32asan8 précédemment désélectionné.
Préparation du dépaquetage de .../13-libx32asan8_12.2.0-14_amd64.deb ...
Dépaquetage de libx32asan8 (12.2.0-14) ...
Sélection du paquet lib32stdc++6 précédemment désélectionné.
Préparation du dépaquetage de .../14-lib32stdc++6_12.2.0-14_amd64.deb ...
Dépaquetage de lib32stdc++6 (12.2.0-14) ...
Sélection du paquet lib32ubsan1 précédemment désélectionné.
Préparation du dépaquetage de .../15-lib32ubsan1_12.2.0-14_amd64.deb ...
Dépaquetage de lib32ubsan1 (12.2.0-14) ...
Sélection du paquet libx32stdc++6 précédemment désélectionné.
Préparation du dépaquetage de .../16-libx32stdc++6_12.2.0-14_amd64.deb ...
Dépaquetage de libx32stdc++6 (12.2.0-14) ...
Sélection du paquet libx32ubsan1 précédemment désélectionné.
Préparation du dépaquetage de .../17-libx32ubsan1_12.2.0-14_amd64.deb ...
Dépaquetage de libx32ubsan1 (12.2.0-14) ...
Sélection du paquet lib32quadmath0 précédemment désélectionné.
Préparation du dépaquetage de .../18-lib32quadmath0_12.2.0-14_amd64.deb ...
Dépaquetage de lib32quadmath0 (12.2.0-14) ...
Sélection du paquet libx32quadmath0 précédemment désélectionné.
Préparation du dépaquetage de .../19-libx32quadmath0_12.2.0-14_amd64.deb ...
Dépaquetage de libx32quadmath0 (12.2.0-14) ...
Sélection du paquet lib32gcc-12-dev précédemment désélectionné.
Préparation du dépaquetage de .../20-lib32gcc-12-dev_12.2.0-14_amd64.deb ...
Dépaquetage de lib32gcc-12-dev (12.2.0-14) ...
Sélection du paquet libx32gcc-12-dev précédemment désélectionné.
Préparation du dépaquetage de .../21-libx32gcc-12-dev_12.2.0-14_amd64.deb ...
Dépaquetage de libx32gcc-12-dev (12.2.0-14) ...
Sélection du paquet gcc-12-multilib précédemment désélectionné.
Préparation du dépaquetage de .../22-gcc-12-multilib_12.2.0-14_amd64.deb ...
Dépaquetage de gcc-12-multilib (12.2.0-14) ...
Sélection du paquet gcc-multilib précédemment désélectionné.
Préparation du dépaquetage de .../23-gcc-multilib_4%3a12.2.0-3_amd64.deb ...
Dépaquetage de gcc-multilib (4:12.2.0-3) ...
Paramétrage de libc6-x32 (2.36-9+deb12u9) ...
Paramétrage de libx32gomp1 (12.2.0-14) ...
Paramétrage de libc6-i386 (2.36-9+deb12u9) ...
Paramétrage de libx32quadmath0 (12.2.0-14) ...
Paramétrage de lib32atomic1 (12.2.0-14) ...
Paramétrage de libx32atomic1 (12.2.0-14) ...
Paramétrage de libc6-dev-i386 (2.36-9+deb12u9) ...
Paramétrage de lib32itm1 (12.2.0-14) ...
Paramétrage de libx32gcc-s1 (12.2.0-14) ...
Paramétrage de libx32itm1 (12.2.0-14) ...
Paramétrage de libx32asan8 (12.2.0-14) ...
Paramétrage de libc6-dev-x32 (2.36-9+deb12u9) ...
Paramétrage de lib32gomp1 (12.2.0-14) ...
Paramétrage de lib32gcc-s1 (12.2.0-14) ...
Paramétrage de lib32stdc++6 (12.2.0-14) ...
Paramétrage de lib32asan8 (12.2.0-14) ...
Paramétrage de lib32quadmath0 (12.2.0-14) ...
Paramétrage de libx32stdc++6 (12.2.0-14) ...
Paramétrage de libx32ubsan1 (12.2.0-14) ...
Paramétrage de lib32ubsan1 (12.2.0-14) ...
Paramétrage de lib32gcc-12-dev (12.2.0-14) ...
Paramétrage de libx32gcc-12-dev (12.2.0-14) ...
Paramétrage de gcc-12-multilib (12.2.0-14) ...
Paramétrage de gcc-multilib (4:12.2.0-3) ...
Traitement des actions différées (« triggers ») pour man-db (2.11.2-2) ...
Traitement des actions différées (« triggers ») pour libc-bin (2.36-9+deb12u9) ...
sarah@vbox:~/work$
sarah@vbox:~/work$
sarah@vbox:~/work$ gcc -fno-stack-protector -g -m32 -o hello2 hello2.c
sarah@vbox:~/work$ ls
hello1  hello1.c  hello2  hello2.c
sarah@vbox:~/work$ ./hello2
Hello, World!

#I-C 
sarah@vbox:~/work$ ldd hello2
        linux-gate.so.1 (0xf7fa8000)
        libc.so.6 => /lib32/libc.so.6 (0xf7d61000)
        /lib/ld-linux.so.2 (0xf7faa000)

sarah@vbox:~/work$ ls
hello1  hello1.c  hello2  hello2.c
sarah@vbox:~/work$ ./hello2
Hello, World!
sarah@vbox:~/work$ ldd hello2
        linux-gate.so.1 (0xf7fa8000)
        libc.so.6 => /lib32/libc.so.6 (0xf7d61000)
        /lib/ld-linux.so.2 (0xf7faa000)
sarah@vbox:~/work$ ldd hello1
        statically linked
sarah@vbox:~/work$ ls
hello1  hello1.c  hello2  hello2.c
sarah@vbox:~/work$ file /bin/ls
/bin/ls: ELF 64-bit LSB pie executable, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, BuildID[sha1]=15dfff3239aa7c3b16a71e6b2e3b6e4009dab998, for GNU/Linux 3.2.0, stripped
sarah@vbox:~/work$ ldd /bin/ls
        linux-vdso.so.1 (0x00007ffeed236000)
        libselinux.so.1 => /lib/x86_64-linux-gnu/libselinux.so.1 (0x00007fa74fb45000)
        libc.so.6 => /lib/x86_64-linux-gnu/libc.so.6 (0x00007fa74f964000)
        libpcre2-8.so.0 => /lib/x86_64-linux-gnu/libpcre2-8.so.0 (0x00007fa74f8ca000)
        /lib64/ld-linux-x86-64.so.2 (0x00007fa74fbaf000)

sarah@vbox:~/work$ file /bin/firefox
/bin/firefox: POSIX shell script, ASCII text executable

## Parmi les librairies appelées par hello2, déterminer le type du fichier nommé libc.so.X A FAIRE

# I - 3 COMPILER STATIQUE
sarah@vbox:~/work$ cp hello2.c hello3.c
sarah@vbox:~/work$ gcc -static -fno-stack-protector -g -m32 -o hello3 hello3.c

sarah@vbox:~/work$ file hello2
hello2: ELF 32-bit LSB pie executable, Intel 80386, version 1 (SYSV), dynamically linked, interpreter /lib/ld-linux.so.2, BuildID[sha1]=62dcb66ff4080182d2eceb4fd1470745558226b9, for GNU/Linux 3.2.0, with debug_info, not stripped
sarah@vbox:~/work$ file hello3
hello3: ELF 32-bit LSB executable, Intel 80386, version 1 (GNU/Linux), statically linked, BuildID[sha1]=c94c2e040f56c0450a3795dede00126ee459a666, for GNU/Linux 3.2.0, with debug_info, not stripped
sarah@vbox:~/work$ du -h hello2
16K     hello2

sarah@vbox:~/work$ du -h hello3
728K    hello3

# I - 4 Compilation cross-platform
sarah@vbox:~/work$ lscpu
Architecture :                            x86_64
  Mode(s) opératoire(s) des processeurs : 32-bit, 64-bit
  Tailles des adresses:                   39 bits physical, 48 bits v
                                          irtual
  Boutisme :                              Little Endian
Processeur(s) :                           1
  Liste de processeur(s) en ligne :       0
Identifiant constructeur :                GenuineIntel
  Nom de modèle :                         12th Gen Intel(R) Core(TM)
                                          i7-1255U
    Famille de processeur :               6
    Modèle :                              154
    Thread(s) par cœur :                  1
    Cœur(s) par socket :                  1
    Socket(s) :                           1
    Révision :                            4
    BogoMIPS :                            5222,41
    Drapeaux :                            fpu vme de pse tsc msr pae
                                          mce cx8 apic sep mtrr pge m
                                          ca cmov pat pse36 clflush m
                                          mx fxsr sse sse2 ht syscall
                                           nx rdtscp lm constant_tsc
                                          rep_good nopl xtopology non
                                          stop_tsc cpuid tsc_known_fr
                                          eq pni pclmulqdq ssse3 cx16
                                           sse4_1 sse4_2 movbe popcnt
                                           aes rdrand hypervisor lahf
                                          _lm abm 3dnowprefetch ibrs_
                                          enhanced fsgsbase bmi1 bmi2
                                           invpcid rdseed adx clflush
                                          opt sha_ni arat md_clear fl
                                          ush_l1d arch_capabilities
Fonctionnalités de virtualisation :
  Constructeur d'hyperviseur :            KVM
  Type de virtualisation :                complet
Caches (somme de toutes) :
  L1d :                                   48 KiB (1 instance)
  L1i :                                   32 KiB (1 instance)
  L2 :                                    1,3 MiB (1 instance)
  L3 :                                    12 MiB (1 instance)
NUMA :
  Nœud(s) NUMA :                          1
  Nœud NUMA 0 de processeur(s) :          0
Vulnérabilités :
  Gather data sampling :                  Not affected
  Itlb multihit :                         Not affected
  L1tf :                                  Not affected
  Mds :                                   Not affected
  Meltdown :                              Not affected
  Mmio stale data :                       Not affected
  Reg file data sampling :                Mitigation; Clear Register
                                          File
  Retbleed :                              Mitigation; Enhanced IBRS
  Spec rstack overflow :                  Not affected
  Spec store bypass :                     Vulnerable
  Spectre v1 :                            Mitigation; usercopy/swapgs
                                           barriers and __user pointe
                                          r sanitization
  Spectre v2 :                            Mitigation; Enhanced / Auto
                                          matic IBRS; RSB filling; PB
                                          RSB-eIBRS SW sequence; BHI
                                          SW loop, KVM SW loop
  Srbds :                                 Not affected
  Tsx async abort :                       Not affected
sarah@vbox:~/work$ cat//proc/cpuinfo
-bash: cat//proc/cpuinfo: Aucun fichier ou dossier de ce type
sarah@vbox:~/work$ cat /proc/cpuinfo
processor       : 0
vendor_id       : GenuineIntel
cpu family      : 6
model           : 154
model name      : 12th Gen Intel(R) Core(TM) i7-1255U
stepping        : 4
microcode       : 0xffffffff
cpu MHz         : 2611.208
cache size      : 12288 KB
physical id     : 0
siblings        : 1
core id         : 0
cpu cores       : 1
apicid          : 0
initial apicid  : 0
fpu             : yes
fpu_exception   : yes
cpuid level     : 22
wp              : yes
flags           : fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush mmx fxsr sse sse2 ht syscall nx rdtscp lm constant_tsc rep_good nopl xtopology nonstop_tsc cpuid tsc_known_freq pni pclmulqdq ssse3 cx16 sse4_1 sse4_2 movbe popcnt aes rdrand hypervisor lahf_lm abm 3dnowprefetch ibrs_enhanced fsgsbase bmi1 bmi2 invpcid rdseed adx clflushopt sha_ni arat md_clear flush_l1d arch_capabilities
bugs            : spectre_v1 spectre_v2 spec_store_bypass swapgs retbleed eibrs_pbrsb rfds bhi
bogomips        : 5222.41
clflush size    : 64
cache_alignment : 64
address sizes   : 39 bits physical, 48 bits virtual
power management: 