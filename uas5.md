---
![Header](header.jpg)

[HOME  |  ](index.md)
[README  |  ](README.md)
[Scripting  |  ](index.md)
[Editor-Linux  |  ](index.md#editorlinux)
[Gcc  |  ](index.md#gcc)
[MakeFile  |  ](index.md#makefile)
[TAR  |  ](index.md#tar)
[Git  |  ](index.md#git)
[GitHub  |  ](index.md#github)
[SHA1  |  ](index.md#sha1)
[GnuPG  |  ](index.md#gnupg)
[UAS-0  |  ](uas0.md)
[UAS-3  |  ](uas3.md)
[UAS-4  |  ](uas4.md)
[UAS-5](uas5.md)



# SOAL TUGAS5
* Keluaran bbfs.log kira-kira seperti berikut:
```
bb_init()
     conn:
     proto_major = 7
     proto_minor = 26
     async_read = 1
     max_write = 131072
     max_readahead = 131072
     capable = 00000ffb
     want = 00000010
     max_background = 0
     congestion_threshold = 0
     context:
     fuse = 9866b790
     uid = 0
     gid = 0
     pid = 0
     private_data = 9866a260
     logfile = 9866b290
     rootdir = /home/fuse/rootdir
     umask = 00000
     bb_access(path="/", mask=04)
bb_fullpath:  rootdir = "/home/fuse/rootdir", path = "/", fpath = "/home/fuse/rootdir/"
[...DST...]
```

* Modifikasi program, sehingga log dimulai dengan nomor baris. <br>
(Contoh baris 00000 hingga 00022)
```
00000 
bb_init()
00001     conn:
00002     proto_major = 7
00003     proto_minor = 26
00004     async_read = 1
00005     max_write = 131072
00006     max_readahead = 131072
00007     capable = 00000ffb
00008     want = 00000010
00009     max_background = 0
00010     congestion_threshold = 0
00011     context:
00012     fuse = 9866b790
00013     uid = 0
00014     gid = 0
00015     pid = 0
00016     private_data = 9866a260
00017     logfile = 9866b290
00018     rootdir = /home/fuse/rootdir
00019     umask = 00000
00020     bb_access(path="/", mask=04)
00021  bb_fullpath:  rootdir = "/home/fuse/rootdir", path = "/", fpath = "/home/fuse/rootdir/"
00022 
[...DST...]
```

* Modifikasi program, agar log menampilkan operasi baca. <br>
(Contoh isi berkas "mountdir/theFuseFile.txt" baris 00209 hingga 00210) <br>
```
[...DST...]
00209 
ZCZC READ ==== ====
Hello:
This is file "theFuseFile.txt" inside  a mounted FUSE directory.
Jolan Tru!
NNNN DONE ==== ====
00210 
[...DST...]
```

* Jalankan serupa yang ada di "K00-TEST-KIT.txt" <br>
Rekam sebagai berkas "K01-TEST-RESULT.txt".

# EDITING PROGRAM
Hal pertama yang perlu dilakukan adalah setting file konfigurasi bbfs, lakukan copy file pada config.h.in yang terdapat pada folder src dan edit menjadi config.h. Selanjutnya Define to 1 untuk semua fungsi #define pada konfigurasi config.h karena kita menggunakan semua fungsi tersebut pada bbfs.

```
 /* Define to 1 if your system has a working `chown' function. */
#define HAVE_CHOWN 1
/* Define to 1 if you have the <fcntl.h> header file. */
#define HAVE_FCNTL_H 1
/* Define to 1 if you have the `fdatasync' function. */
#define HAVE_FDATASYNC 1
/* Define to 1 if you have the `ftruncate' function. */
#define HAVE_FTRUNCATE 1
/* Define to 1 if you have the <inttypes.h> header file. */
#define HAVE_INTTYPES_H 1
/* Define to 1 if you have the <limits.h> header file. */
#define HAVE_LIMITS_H 1
/* Define to 1 if your system has a GNU libc compatible `malloc' function, and
   to 0 otherwise. */
#define HAVE_MALLOC 1
/* Define to 1 if you have the <memory.h> header file. */
#define HAVE_MEMORY_H 1
/* Define to 1 if you have the `mkdir' function. */
#define HAVE_MKDIR 1
/* Define to 1 if you have the `mkfifo' function. */
#define HAVE_MKFIFO 1
/* Define to 1 if you have the `realpath' function. */
#define HAVE_REALPATH 1
/* Define to 1 if you have the `rmdir' function. */
#define HAVE_RMDIR 1
/* Define to 1 if you have the <stdint.h> header file. */
#define HAVE_STDINT_H 1
/* Define to 1 if you have the <stdlib.h> header file. */
#define HAVE_STDLIB_H 1
/* Define to 1 if you have the `strerror' function. */
#define HAVE_STRERROR 1
/* Define to 1 if you have the <strings.h> header file. */
#define HAVE_STRINGS_H 1
/* Define to 1 if you have the <string.h> header file. */
#define HAVE_STRING_H 1
/* Define to 1 if `st_blksize' is a member of `struct stat'. */
#define HAVE_STRUCT_STAT_ST_BLKSIZE 1
/* Define to 1 if `st_blocks' is a member of `struct stat'. */
#define HAVE_STRUCT_STAT_ST_BLOCKS 1
/* Define to 1 if `st_rdev' is a member of `struct stat'. */
#define HAVE_STRUCT_STAT_ST_RDEV 1
/* Define to 1 if your `struct stat' has `st_blocks'. Deprecated, use
   `HAVE_STRUCT_STAT_ST_BLOCKS' instead. */
#define HAVE_ST_BLOCKS 1
/* Define to 1 if you have the <sys/statvfs.h> header file. */
#define HAVE_SYS_STATVFS_H 1
/* Define to 1 if you have the <sys/stat.h> header file. */
#define HAVE_SYS_STAT_H 1
/* Define to 1 if you have the <sys/types.h> header file. */
#define HAVE_SYS_TYPES_H 1
/* Define to 1 if you have the <sys/xattr.h> header file. */
#define HAVE_SYS_XATTR_H 1
/* Define to 1 if you have the <unistd.h> header file. */
#define HAVE_UNISTD_H 1
/* Define to 1 if you have the `utime' function. */
#define HAVE_UTIME 1
/* Define to 1 if you have the <utime.h> header file. */
#define HAVE_UTIME_H 1
/* Define to 1 if `lstat' dereferences a symlink specified with a trailing
   slash. */
#define LSTAT_FOLLOWS_SLASHED_SYMLINK 1
```

* Setting file konfigurasi package pada config.h, sesuaikan dengan nama folder, versi, dan author.

```
/* Name of package */
#define PACKAGE "fuse-tutorial"
/* Define to the address where bug reports for this package should be sent. */
#define PACKAGE_BUGREPORT "joseph@pfeifferfamily.net"
/* Define to the full name of this package. */
#define PACKAGE_NAME "fuse-tutorial"
/* Define to the full name and version of this package. */
#define PACKAGE_STRING "fuse-tutorial 2018-02-04"
/* Define to the one symbol short name of this package. */
#define PACKAGE_TARNAME "fuse-tutorial"
/* Define to the home page for this package. */
#define PACKAGE_URL ""
/* Define to the version of this package. */
#define PACKAGE_VERSION "2018-02-04"
/* Define to 1 if you have the ANSI C header files. */
#define STDC_HEADERS 1
/* Version number of package */
#define VERSION "2018-02-04"
```

* Hide beberapa fungsi yang tidak digunakan pada config.h, hal ini dilakukan karena kita menggunakan semua fungsi / define yang sebelumnya telah dibuat.

```
/* Define for Solaris 2.5.1 so the uint64_t typedef from <sys/synch.h>,
   <pthread.h>, or <semaphore.h> is not used. If the typedef were allowed,the
   #define below would cause a syntax error. */
/* #undef _UINT64_T */
/* Define to `int' if <sys/types.h> doesn't define. */
/* #undef gid_t */
/* Define to rpl_malloc if the replacement function should be used. */
/* #undef malloc */
/* Define to `int' if <sys/types.h> does not define. */
/* #undef mode_t */
/* Define to `long int' if <sys/types.h> does not define. */
/* #undef off_t */
/* Define to `int' if <sys/types.h> does not define. */
/* #undef pid_t */
/* Define to `unsigned int' if <sys/types.h> does not define. */
/* #undef size_t */
/* Define to `int' if <sys/types.h> doesn't define. */
/* #undef uid_t */
/* Define to the type of an unsigned integer type of width exactly 64 bits if
   such a type exists and the standard includes do not define it. */
/* #undef uint64_t */
```

* Selanjutnya buka file bbfs.c, kemudian lakukan searching character pada file bbfs.c sehingga didapat fungsi bb_read. Fungsi bb_read disini berguna untuk menampilkan operasi baca pada bbfs. Lakukan editing pada fungsi bb_read dan tambahkan:

```
if (retstat < 0)
	    retstat = log_error("bb_read read");
log_msg("\nZCZC READ ==== ==== \n%s\n%s\n",buf, "NNNN DONE ==== ====");
```

* Dimana fungsi tersebut dibuat agar pada saat operasi baca bbfs dijalankan dan terdapat eror, maka akan menampilkan log message `CZC READ ==== ==== \n%s\n%s\n",buf, "NNNN DONE ==== ====`

* Berikut fungsi lengkapnya:

```
int bb_read(const char *path, char *buf, size_t size, off_t offset, struct fuse_file_info *fi)
{
    int retstat = 0;
    log_msg("\nbb_read(path=\"%s\", buf=0x%08x, size=%d, offset=%lld, fi=0x%08x)\n",
    path, buf, size, offset, fi);
    // no need to get fpath on this one, since I work from fi->fh not the path
    log_fi(fi);
    retstat = pread(fi->fh, buf, size, offset);
    if (retstat < 0)
	    retstat = log_error("bb_read read");
    log_msg("\nZCZC READ ==== ==== \n%s\n%s\n",buf, "NNNN DONE ==== ====");
    return log_syscall("pread", pread(fi->fh, buf, size, offset), 0);
}
```

* Selanjutnya buka file log.c, kemudian lakukan searching character pada file log.c sehingga didapat fungsi log_msg. Fungsi log_msg disini berguna untuk menampilkan / mencetak pesan log pada proses pada bbfs. Lakukan editing pada fungsi log_msg dan tambahkan: <br>

Deklarasi variabel i dengan tipe data integer yang dimulai dari angka 0: <br>
int i = 0;
<br><br>
Deklarasi isi fungsi dimana fungsi ini nantinya yang akan menampilkan urutan log yang dimulai dengan nomor baris. 
```
va_list ap;
    char str[10];
    sprintf(str, "%0.4d", i);
    fprintf(BB_DATA->logfile, str);
    va_start(ap, format);
    i++;
    vfprintf(BB_DATA->logfile, format, ap);
```

Berikut fungsi lengkapnya:

```
int i = 0;
void log_msg(const char *format, ...)
{
    va_list ap;
    char str[10];
    sprintf(str, "%0.4d", i);
    fprintf(BB_DATA->logfile, str);
    va_start(ap, format);
    i++;
    vfprintf(BB_DATA->logfile, format, ap);
}
```

# TEST KIT

* Berikut kode Bash yang digunakan dalam proses scripting Fuse pada TUGAS5:

```
$ export akunGitHub="imamsetyo96"
$ export PSTAMP="TMP1=\"\$(date +%y%m%d-%H%M%S)\"; TMP2=\"\$(sleep 1;echo \$TMP1-\$akunGitHub-\${PWD##*/}|sha1sum|cut -c1-4)\"; 
$ echo \"\$TMP1-\$TMP2-\${PWD##*/}/> \";";
$ echo $PSTAMP ;  
$ eval $PSTAMP;
```
* Masuk ke dalam folder TUGAS5 untuk memulai proses scripting pada file. Lakukan tahap awal proses scripting dengan melakukan echo pada hostname dan akun github masing-masing yang sudah di export
```
$ script K01-TEST-RESULT.txt
$ PS1="$ "
$ date
$ echo $HOSTNAME
$ echo $akunGitHub
$ echo $PSTAMP
$ PS1="\$(eval \$PSTAMP)"
```

* Masuk ke dalam folder fuse-tutorial-2018-02-04:
```
$ cd fuse-tutorial-2018-02-04
```

* Instalasi Fuse dengan cara sebagai berikut. Cek konfigurasi paket fuse pada masing-masing versi yang digunakan:
```
$ ./configure
```

* Membuat file:
```
$ make
```

* Masuk ke dalam folder example:
```
$ cd example/
```

* Membuat dan menampilkan seluruh isi pada folder rootdir dan mountdir:
```
$ ls -al rootdir/
$ ls -al mountdir/
```

* Duplikasi file ke dalam folder rootdir:
```
$ cp ../../theFuseFile.txt rootdir/
$ echo 'Bandingkan! (df)'
```

* Menjalankan fungsi bbfs pada fuse. Perintah df menampilkan penggunaan disk saat ini pada sistem Linux file sistem statistik. Perintah grep digunakan untuk menemukan teks termasuk subdirektori
```
$ df | grep bbfs
$ ../src/bbfs rootdir/ mountdir/
$ echo 'Bandingkan! (df)'
$ df | grep bbfs
```

* Cek kembali folder rootdir dan mountdir apakah virtual file system berhasil/tidak Jika berhasil, maka isi file pada direktori rootdir adalah sama dengan mountdir.
```
$ ls -al rootdir/
$ ls -al mountdir/

$ cat mountdir/theFuseFile.txt
$ sleep 1
$ echo ''
```

* Perintah fusemounter digunakan untuk menghentikan proses fuse
```
$ echo 'Penting!!! Selalu akhiri dengan perintah fusemounter'
```

* Perintah sleep digunakan untuk menghentikan sementara eksekusi pada perintah berikutnya selama beberapa detik. Perintah sleep sangat berguna ketika digunakan dalam skrip bash shell, misalnya ketika mencoba kembali operasi yang gagal atau di dalam loop.
```
$ sleep 1

$ echo ''
$ fusermount -u mountdir
$ sleep 1
$ echo ''
$ echo 'Bandingkan! (df)'
$ df | grep bbfs
$ ls -al rootdir/
$ ls -al mountdir/
```

* Menampilkan isi berkas salinan log pada log bbfs.log:
```
$ echo 'Berkas log bbfs.log'
$ cat bbfs.log

```
* Mengakhiri proses scripting:
```
$ exit
```

* Keluar folder TUGAS5 untuk membuat file tar.bz2 pada folder TUGAS5:
``` 
$ tar -zcvf 0007-TUGAS5.tar.bz2 TUGAS5
```

* Enkripsi asimetris pada file 0007-TUGAS5.tar.bz2 yang sudah dibuat:
```
$ gpg2 -o 0007-TUGAS5.tar.bz2.asc -e -r operatingsystems@vlsm.org -r imam.setyo@ui.ac.id -a 0007-TUGAS5.tar.bz2
```

# CATATAN:
/etc/fstab: configuration of filesystems<br>
/etc/mtab -->  /proc/mounts: mounted filesystems<br>
/proc/swaps: swap filesistems<br>
df: checking diskspace and filesystems<br>
GUID (Globally Unique IDentifiers) ls -al /dev/disk/by-uuid<br>

# TESTING
Berikut merupakan hasil testing program TUGAS5 menggunakan ssh badak.cs.ui.ac.id:

```
Script started on Thu Aug  6 00:09:50 2020
imam.setyo@badak:~/UASJULI/TUGAS5$ PS1="$ "
$ date
Thu Aug  6 00:10:03 WIB 2020
$ echo $HOSTNAME
badak
$ echo $akunGitHub
imamsetyo96
$ echo $PSTAMP
TMP1="$(date +%y%m%d-%H%M%S)"; TMP2="$(sleep 1;echo $TMP1-$akunGitHub-${PWD##*/}|sha1sum|cut -c1-4)"; echo "$TMP1-$TMP2-${PWD##*/}/> ";
$ PS1="\$(eval \$PSTAMP)"
200806-001027-a120-TUGAS5/> cd fuse-tutorial-2018-02-04
200806-001036-d353-fuse-tutorial-2018-02-04/> ./configure
checking for a BSD-compatible install... /usr/bin/install -c
checking whether build environment is sane... yes
checking for a thread-safe mkdir -p... /bin/mkdir -p
checking for gawk... gawk
checking whether make sets $(MAKE)... yes
checking whether make supports nested variables... yes
checking for gcc... gcc
checking whether the C compiler works... yes
checking for C compiler default output file name... a.out
checking for suffix of executables... 
checking whether we are cross compiling... no
checking for suffix of object files... o
checking whether we are using the GNU C compiler... yes
checking whether gcc accepts -g... yes
checking for gcc option to accept ISO C89... none needed
checking whether gcc understands -c and -o together... yes
checking for style of include used by make... GNU
checking dependency style of gcc... gcc3
checking how to run the C preprocessor... gcc -E
checking for grep that handles long lines and -e... /bin/grep
checking for egrep... /bin/grep -E
checking for ANSI C header files... yes
checking for sys/types.h... yes
checking for sys/stat.h... yes
checking for stdlib.h... yes
checking for string.h... yes
checking for memory.h... yes
checking for strings.h... yes
checking for inttypes.h... yes
checking for stdint.h... yes
checking for unistd.h... yes
checking fcntl.h usability... yes
checking fcntl.h presence... yes
checking for fcntl.h... yes
checking limits.h usability... yes
checking limits.h presence... yes
checking for limits.h... yes
checking for stdlib.h... (cached) yes
checking for string.h... (cached) yes
checking sys/statvfs.h usability... yes
checking sys/statvfs.h presence... yes
checking for sys/statvfs.h... yes
checking for unistd.h... (cached) yes
checking utime.h usability... yes
checking utime.h presence... yes
checking for utime.h... yes
checking sys/xattr.h usability... yes
checking sys/xattr.h presence... yes
checking for sys/xattr.h... yes
checking for pkg-config... /usr/bin/pkg-config
checking pkg-config is at least version 0.9.0... yes
checking for FUSE... yes
checking for uid_t in sys/types.h... yes
checking for mode_t... yes
checking for off_t... yes
checking for pid_t... yes
checking for size_t... yes
checking for struct stat.st_blksize... yes
checking for struct stat.st_blocks... yes
checking for struct stat.st_rdev... yes
checking for uint64_t... yes
checking for unistd.h... (cached) yes
checking for working chown... yes
checking whether lstat correctly handles trailing slash... yes
checking for stdlib.h... (cached) yes
checking for GNU libc compatible malloc... yes
checking for ftruncate... yes
checking for mkdir... yes
checking for mkfifo... yes
checking for realpath... yes
checking for rmdir... yes
checking for strerror... yes
checking for utime... yes
checking for fdatasync... yes
checking that generated files are newer than configure... done
configure: creating ./config.status
config.status: creating Makefile
config.status: creating html/Makefile
config.status: creating src/Makefile
config.status: creating src/config.h
config.status: src/config.h is unchanged
config.status: executing depfiles commands
200806-001049-8210-fuse-tutorial-2018-02-04/> make
Making all in example
make[1]: Entering directory '/home/fasilkom/mahasiswa/i/imam.setyo/UASJULI/TUGAS5/fuse-tutorial-2018-02-04/example'
mkdir -p mountdir
mkdir -p rootdir
echo "bogus file" > rootdir/bogus.txt
make[1]: Leaving directory '/home/fasilkom/mahasiswa/i/imam.setyo/UASJULI/TUGAS5/fuse-tutorial-2018-02-04/example'
Making all in html
make[1]: Entering directory '/home/fasilkom/mahasiswa/i/imam.setyo/UASJULI/TUGAS5/fuse-tutorial-2018-02-04/html'
make[1]: Nothing to be done for 'all'.
make[1]: Leaving directory '/home/fasilkom/mahasiswa/i/imam.setyo/UASJULI/TUGAS5/fuse-tutorial-2018-02-04/html'
Making all in src
make[1]: Entering directory '/home/fasilkom/mahasiswa/i/imam.setyo/UASJULI/TUGAS5/fuse-tutorial-2018-02-04/src'
make  all-am
make[2]: Entering directory '/home/fasilkom/mahasiswa/i/imam.setyo/UASJULI/TUGAS5/fuse-tutorial-2018-02-04/src'
gcc -DHAVE_CONFIG_H -I.    -D_FILE_OFFSET_BITS=64 -I/usr/include/fuse -g -O2 -MT bbfs.o -MD -MP -MF .deps/bbfs.Tpo -c -o bbfs.o bbfs.c
mv -f .deps/bbfs.Tpo .deps/bbfs.Po
gcc -DHAVE_CONFIG_H -I.    -D_FILE_OFFSET_BITS=64 -I/usr/include/fuse -g -O2 -MT log.o -MD -MP -MF .deps/log.Tpo -c -o log.o log.c
mv -f .deps/log.Tpo .deps/log.Po
gcc -D_FILE_OFFSET_BITS=64 -I/usr/include/fuse -g -O2   -o bbfs bbfs.o log.o -lfuse -pthread 
make[2]: Leaving directory '/home/fasilkom/mahasiswa/i/imam.setyo/UASJULI/TUGAS5/fuse-tutorial-2018-02-04/src'
make[1]: Leaving directory '/home/fasilkom/mahasiswa/i/imam.setyo/UASJULI/TUGAS5/fuse-tutorial-2018-02-04/src'
make[1]: Entering directory '/home/fasilkom/mahasiswa/i/imam.setyo/UASJULI/TUGAS5/fuse-tutorial-2018-02-04'
make[1]: Nothing to be done for 'all-am'.
make[1]: Leaving directory '/home/fasilkom/mahasiswa/i/imam.setyo/UASJULI/TUGAS5/fuse-tutorial-2018-02-04'
200806-001059-6d51-fuse-tutorial-2018-02-04/> cd example/
200806-001109-908f-example/> ls -al rootdir/
total 12
drwxr-xr-x 2 imam.setyo StafCS 4096 Aug  5 18:58 .
drwxr-xr-x 4 imam.setyo StafCS 4096 Aug  5 17:13 ..
-rw-r--r-- 1 imam.setyo StafCS   11 Aug  6 00:10 bogus.txt
200806-001116-a87d-example/> ls -al mountdir/
total 8
drwxr-xr-x 2 imam.setyo StafCS 4096 Aug  5 17:13 .
drwxr-xr-x 4 imam.setyo StafCS 4096 Aug  5 17:13 ..
200806-001125-4fd2-example/> cp ../../theFuseFile.txt rootdir/
200806-001134-a792-example/> echo 'Bandingkan! (df)'
Bandingkan! (df)
200806-001142-b0de-example/> df | grep bbfs
200806-001155-08f0-example/> ../src/bbfs rootdir/ mountdir/
Fuse library version 2.9
about to call fuse_main
200806-001203-3ca4-example/> echo 'Bandingkan! (df)'
Bandingkan! (df)
200806-001210-5f7a-example/> df | grep bbfs
bbfs           412322216 39054852 352279516  10% /home/fasilkom/mahasiswa/i/imam.setyo/UASJULI/TUGAS5/fuse-tutorial-2018-02-04/example/mountdir
200806-001216-083a-example/> ls -al rootdir/
total 16
drwxr-xr-x 2 imam.setyo StafCS 4096 Aug  6 00:11 .
drwxr-xr-x 4 imam.setyo StafCS 4096 Aug  5 17:13 ..
-rw-r--r-- 1 imam.setyo StafCS   11 Aug  6 00:10 bogus.txt
-rw-r--r-- 1 imam.setyo StafCS   83 Aug  6 00:11 theFuseFile.txt
200806-001225-540e-example/> ls -al mountdir/
total 16
drwxr-xr-x 2 imam.setyo StafCS 4096 Aug  6 00:11 .
drwxr-xr-x 4 imam.setyo StafCS 4096 Aug  5 17:13 ..
-rw-r--r-- 1 imam.setyo StafCS   11 Aug  6 00:10 bogus.txt
-rw-r--r-- 1 imam.setyo StafCS   83 Aug  6 00:11 theFuseFile.txt
200806-001234-0c72-example/> cat mountdir/theFuseFile.txt
Hello:
This is file "theFuseFile.txt" inside  a mounted FUSE directory.
Jolan Tru!
200806-001242-9d1b-example/> sleep 1
200806-001252-67ea-example/> echo ''

200806-001259-3e18-example/> echo 'Penting!!! Selalu akhiri dengan perintah fuse 
mounter'
Penting!!! Selalu akhiri dengan perintah fusemounter
200806-001310-7bad-example/> sleep 1
200806-001320-63c6-example/> echo ''

200806-001329-7640-example/> fusermount -u mountdir
200806-001337-ab41-example/> sleep 1
200806-001344-23be-example/> echo ''

200806-001348-63d2-example/> echo 'Bandingkan! (df)'
Bandingkan! (df)
200806-001354-b4bd-example/> df | grep bbfs
200806-001359-6da0-example/> ls -al rootdir/
total 16
drwxr-xr-x 2 imam.setyo StafCS 4096 Aug  6 00:11 .
drwxr-xr-x 4 imam.setyo StafCS 4096 Aug  5 17:13 ..
-rw-r--r-- 1 imam.setyo StafCS   11 Aug  6 00:10 bogus.txt
-rw-r--r-- 1 imam.setyo StafCS   83 Aug  6 00:11 theFuseFile.txt
200806-001404-51e4-example/> ls -al mountdir/
total 8
drwxr-xr-x 2 imam.setyo StafCS 4096 Aug  5 17:13 .
drwxr-xr-x 4 imam.setyo StafCS 4096 Aug  5 17:13 ..
200806-001410-8c44-example/> echo 'Berkas log bbfs.log'
Berkas log bbfs.log
200806-001426-cbb9-example/> cat bbfs.log
0000
bb_init()
0001    conn:
0002    proto_major = 7
0003    proto_minor = 26
0004    async_read = 1
0005    max_write = 131072
0006    max_readahead = 131072
0007    capable = 00000ffb
0008    want = 00000010
0009    max_background = 0
0010    congestion_threshold = 0
0011    context:
0012    fuse = 0125b580
0013    uid = 0
0014    gid = 0
0015    pid = 0
0016    private_data = 0125a010
0017    logfile = 0125b040
0018    rootdir = /home/fasilkom/mahasiswa/i/imam.setyo/UASJULI/TUGAS5/fuse-tutorial-2018-02-04/example/rootdir
0019    umask = 00000
0020
bb_getattr(path="/", statbuf=0x4e81bc60)
0021    bb_fullpath:  rootdir = "/home/fasilkom/mahasiswa/i/imam.setyo/UASJULI/TUGAS5/fuse-tutorial-2018-02-04/example/rootdir", path = "/", fpath = "/home/fasilkom/mahasiswa/i/imam.setyo/UASJULI/TUGAS5/fuse-tutorial-2018-02-04/example/rootdir/"
0022    lstat returned 0
0023    si:
0024    st_dev = 2081
0025    st_ino = 12324292
0026    st_mode = 040755
0027    st_nlink = 2
0028    st_uid = 52039
0029    st_gid = 2200
0030    st_rdev = 0
0031    st_size = 4096
0032    st_blksize = 4096
0033    st_blocks = 8
0034    st_atime = 0x5f2ae834
0035    st_mtime = 0x5f2ae846
0036    st_ctime = 0x5f2ae846
0037
bb_statfs(path="/", statv=0x4f01cc40)
0038    bb_fullpath:  rootdir = "/home/fasilkom/mahasiswa/i/imam.setyo/UASJULI/TUGAS5/fuse-tutorial-2018-02-04/example/rootdir", path = "/", fpath = "/home/fasilkom/mahasiswa/i/imam.setyo/UASJULI/TUGAS5/fuse-tutorial-2018-02-04/example/rootdir/"
0039    statvfs returned 0
0040    sv:
0041    f_bsize = 4096
0042    f_frsize = 4096
0043    f_blocks = 103080554
0044    f_bfree = 93316841
0045    f_bavail = 88069879
0046    f_files = 26214400
0047    f_ffree = 25505162
0048    f_favail = 25505162
0049    f_fsid = -7444248716403684756
0050    f_flag = 0x00001000
0051    f_namemax = 255
0052
bb_getattr(path="/", statbuf=0x4e81bc60)
0053    bb_fullpath:  rootdir = "/home/fasilkom/mahasiswa/i/imam.setyo/UASJULI/TUGAS5/fuse-tutorial-2018-02-04/example/rootdir", path = "/", fpath = "/home/fasilkom/mahasiswa/i/imam.setyo/UASJULI/TUGAS5/fuse-tutorial-2018-02-04/example/rootdir/"
0054    lstat returned 0
0055    si:
0056    st_dev = 2081
0057    st_ino = 12324292
0058    st_mode = 040755
0059    st_nlink = 2
0060    st_uid = 52039
0061    st_gid = 2200
0062    st_rdev = 0
0063    st_size = 4096
0064    st_blksize = 4096
0065    st_blocks = 8
0066    st_atime = 0x5f2ae879
0067    st_mtime = 0x5f2ae846
0068    st_ctime = 0x5f2ae846
0069
bb_getxattr(path = "/", name = "security.selinux", value = 0x48000af0, size = 255)
0070    bb_fullpath:  rootdir = "/home/fasilkom/mahasiswa/i/imam.setyo/UASJULI/TUGAS5/fuse-tutorial-2018-02-04/example/rootdir", path = "/", fpath = "/home/fasilkom/mahasiswa/i/imam.setyo/UASJULI/TUGAS5/fuse-tutorial-2018-02-04/example/rootdir/"
0071    lgetxattr returned -1
0072    ERROR lgetxattr: No data available
0073
bb_getxattr(path = "/", name = "system.posix_acl_access", value = 0x00000000, size = 0)
0074    bb_fullpath:  rootdir = "/home/fasilkom/mahasiswa/i/imam.setyo/UASJULI/TUGAS5/fuse-tutorial-2018-02-04/example/rootdir", path = "/", fpath = "/home/fasilkom/mahasiswa/i/imam.setyo/UASJULI/TUGAS5/fuse-tutorial-2018-02-04/example/rootdir/"
0075    lgetxattr returned -1
0076    ERROR lgetxattr: No data available
0077
bb_getxattr(path = "/", name = "system.posix_acl_default", value = 0x00000000, size = 0)
0078    bb_fullpath:  rootdir = "/home/fasilkom/mahasiswa/i/imam.setyo/UASJULI/TUGAS5/fuse-tutorial-2018-02-04/example/rootdir", path = "/", fpath = "/home/fasilkom/mahasiswa/i/imam.setyo/UASJULI/TUGAS5/fuse-tutorial-2018-02-04/example/rootdir/"
0079    lgetxattr returned -1
0080    ERROR lgetxattr: No data available
0081
bb_opendir(path="/", fi=0x4e81bc80)
0082    bb_fullpath:  rootdir = "/home/fasilkom/mahasiswa/i/imam.setyo/UASJULI/TUGAS5/fuse-tutorial-2018-02-04/example/rootdir", path = "/", fpath = "/home/fasilkom/mahasiswa/i/imam.setyo/UASJULI/TUGAS5/fuse-tutorial-2018-02-04/example/rootdir/"
0083    opendir returned 0x0x7f0340000b20
0084    fi:
0085    flags = 0x00018800
0086    fh_old = 0x00000000
0087    writepage = 0
0088    direct_io = 0
0089    keep_cache = 0
0090    fh = 0x00007f0340000b20
0091    lock_owner = 0x0000000000000000
0092
bb_readdir(path="/", buf=0x40000990, filler=0x4f7f2c40, offset=0, fi=0x4f01cc80)
0093    readdir returned 0x0x7f0340000b50
0094calling filler with name .
0095calling filler with name bogus.txt
0096calling filler with name theFuseFile.txt
0097calling filler with name ..
0098    fi:
0099    flags = 0x00000000
0100    fh_old = 0x7f0340000b20
0101    writepage = 0
0102    direct_io = 0
0103    keep_cache = 0
0104    fh = 0x00007f0340000b20
0105    lock_owner = 0x0000000000000000
0106
bb_getattr(path="/", statbuf=0x4e81bc60)
0107    bb_fullpath:  rootdir = "/home/fasilkom/mahasiswa/i/imam.setyo/UASJULI/TUGAS5/fuse-tutorial-2018-02-04/example/rootdir", path = "/", fpath = "/home/fasilkom/mahasiswa/i/imam.setyo/UASJULI/TUGAS5/fuse-tutorial-2018-02-04/example/rootdir/"
0108    lstat returned 0
0109    si:
0110    st_dev = 2081
0111    st_ino = 12324292
0112    st_mode = 040755
0113    st_nlink = 2
0114    st_uid = 52039
0115    st_gid = 2200
0116    st_rdev = 0
0117    st_size = 4096
0118    st_blksize = 4096
0119    st_blocks = 8
0120    st_atime = 0x5f2ae879
0121    st_mtime = 0x5f2ae846
0122    st_ctime = 0x5f2ae846
0123
bb_getxattr(path = "/", name = "security.selinux", value = 0x48000af0, size = 255)
0124    bb_fullpath:  rootdir = "/home/fasilkom/mahasiswa/i/imam.setyo/UASJULI/TUGAS5/fuse-tutorial-2018-02-04/example/rootdir", path = "/", fpath = "/home/fasilkom/mahasiswa/i/imam.setyo/UASJULI/TUGAS5/fuse-tutorial-2018-02-04/example/rootdir/"
0125    lgetxattr returned -1
0126    ERROR lgetxattr: No data available
0127
bb_getxattr(path = "/", name = "system.posix_acl_access", value = 0x00000000, size = 0)
0128    bb_fullpath:  rootdir = "/home/fasilkom/mahasiswa/i/imam.setyo/UASJULI/TUGAS5/fuse-tutorial-2018-02-04/example/rootdir", path = "/", fpath = "/home/fasilkom/mahasiswa/i/imam.setyo/UASJULI/TUGAS5/fuse-tutorial-2018-02-04/example/rootdir/"
0129    lgetxattr returned -1
0130    ERROR lgetxattr: No data available
0131
bb_getxattr(path = "/", name = "system.posix_acl_default", value = 0x00000000, size = 0)
0132    bb_fullpath:  rootdir = "/home/fasilkom/mahasiswa/i/imam.setyo/UASJULI/TUGAS5/fuse-tutorial-2018-02-04/example/rootdir", path = "/", fpath = "/home/fasilkom/mahasiswa/i/imam.setyo/UASJULI/TUGAS5/fuse-tutorial-2018-02-04/example/rootdir/"
0133    lgetxattr returned -1
0134    ERROR lgetxattr: No data available
0135
bb_getattr(path="/bogus.txt", statbuf=0x4e81bc90)
0136    bb_fullpath:  rootdir = "/home/fasilkom/mahasiswa/i/imam.setyo/UASJULI/TUGAS5/fuse-tutorial-2018-02-04/example/rootdir", path = "/bogus.txt", fpath = "/home/fasilkom/mahasiswa/i/imam.setyo/UASJULI/TUGAS5/fuse-tutorial-2018-02-04/example/rootdir/bogus.txt"
0137    lstat returned 0
0138    si:
0139    st_dev = 2081
0140    st_ino = 12324293
0141    st_mode = 0100644
0142    st_nlink = 1
0143    st_uid = 52039
0144    st_gid = 2200
0145    st_rdev = 0
0146    st_size = 11
0147    st_blksize = 4096
0148    st_blocks = 8
0149    st_atime = 0x5f2ae5ef
0150    st_mtime = 0x5f2ae823
0151    st_ctime = 0x5f2ae823
0152
bb_getxattr(path = "/bogus.txt", name = "security.selinux", value = 0x48000af0, size = 255)
0153    bb_fullpath:  rootdir = "/home/fasilkom/mahasiswa/i/imam.setyo/UASJULI/TUGAS5/fuse-tutorial-2018-02-04/example/rootdir", path = "/bogus.txt", fpath = "/home/fasilkom/mahasiswa/i/imam.setyo/UASJULI/TUGAS5/fuse-tutorial-2018-02-04/example/rootdir/bogus.txt"
0154    lgetxattr returned -1
0155    ERROR lgetxattr: No data available
0156
bb_getxattr(path = "/bogus.txt", name = "system.posix_acl_access", value = 0x00000000, size = 0)
0157    bb_fullpath:  rootdir = "/home/fasilkom/mahasiswa/i/imam.setyo/UASJULI/TUGAS5/fuse-tutorial-2018-02-04/example/rootdir", path = "/bogus.txt", fpath = "/home/fasilkom/mahasiswa/i/imam.setyo/UASJULI/TUGAS5/fuse-tutorial-2018-02-04/example/rootdir/bogus.txt"
0158    lgetxattr returned -1
0159    ERROR lgetxattr: No data available
0160
bb_getattr(path="/theFuseFile.txt", statbuf=0x4f01cc90)
0161    bb_fullpath:  rootdir = "/home/fasilkom/mahasiswa/i/imam.setyo/UASJULI/TUGAS5/fuse-tutorial-2018-02-04/example/rootdir", path = "/theFuseFile.txt", fpath = "/home/fasilkom/mahasiswa/i/imam.setyo/UASJULI/TUGAS5/fuse-tutorial-2018-02-04/example/rootdir/theFuseFile.txt"
0162    lstat returned 0
0163    si:
0164    st_dev = 2081
0165    st_ino = 12324331
0166    st_mode = 0100644
0167    st_nlink = 1
0168    st_uid = 52039
0169    st_gid = 2200
0170    st_rdev = 0
0171    st_size = 83
0172    st_blksize = 4096
0173    st_blocks = 8
0174    st_atime = 0x5f2ae846
0175    st_mtime = 0x5f2ae846
0176    st_ctime = 0x5f2ae846
0177
bb_getxattr(path = "/theFuseFile.txt", name = "security.selinux", value = 0x40000a10, size = 255)
0178    bb_fullpath:  rootdir = "/home/fasilkom/mahasiswa/i/imam.setyo/UASJULI/TUGAS5/fuse-tutorial-2018-02-04/example/rootdir", path = "/theFuseFile.txt", fpath = "/home/fasilkom/mahasiswa/i/imam.setyo/UASJULI/TUGAS5/fuse-tutorial-2018-02-04/example/rootdir/theFuseFile.txt"
0179    lgetxattr returned -1
0180    ERROR lgetxattr: No data available
0181
bb_getxattr(path = "/theFuseFile.txt", name = "system.posix_acl_access", value = 0x00000000, size = 0)
0182    bb_fullpath:  rootdir = "/home/fasilkom/mahasiswa/i/imam.setyo/UASJULI/TUGAS5/fuse-tutorial-2018-02-04/example/rootdir", path = "/theFuseFile.txt", fpath = "/home/fasilkom/mahasiswa/i/imam.setyo/UASJULI/TUGAS5/fuse-tutorial-2018-02-04/example/rootdir/theFuseFile.txt"
0183    lgetxattr returned -1
0184    ERROR lgetxattr: No data available
0185
bb_releasedir(path="/", fi=0x4f01cc90)
0186    fi:
0187    flags = 0x00000000
0188    fh_old = 0x7f0340000b20
0189    writepage = 0
0190    direct_io = 0
0191    keep_cache = 0
0192    fh = 0x00007f0340000b20
0193    lock_owner = 0x0000000000000000
0194
bb_getattr(path="/theFuseFile.txt", statbuf=0x4e81bc90)
0195    bb_fullpath:  rootdir = "/home/fasilkom/mahasiswa/i/imam.setyo/UASJULI/TUGAS5/fuse-tutorial-2018-02-04/example/rootdir", path = "/theFuseFile.txt", fpath = "/home/fasilkom/mahasiswa/i/imam.setyo/UASJULI/TUGAS5/fuse-tutorial-2018-02-04/example/rootdir/theFuseFile.txt"
0196    lstat returned 0
0197    si:
0198    st_dev = 2081
0199    st_ino = 12324331
0200    st_mode = 0100644
0201    st_nlink = 1
0202    st_uid = 52039
0203    st_gid = 2200
0204    st_rdev = 0
0205    st_size = 83
0206    st_blksize = 4096
0207    st_blocks = 8
0208    st_atime = 0x5f2ae846
0209    st_mtime = 0x5f2ae846
0210    st_ctime = 0x5f2ae846
0211
bb_open(path"/theFuseFile.txt", fi=0x4f01cd40)
0212    bb_fullpath:  rootdir = "/home/fasilkom/mahasiswa/i/imam.setyo/UASJULI/TUGAS5/fuse-tutorial-2018-02-04/example/rootdir", path = "/theFuseFile.txt", fpath = "/home/fasilkom/mahasiswa/i/imam.setyo/UASJULI/TUGAS5/fuse-tutorial-2018-02-04/example/rootdir/theFuseFile.txt"
0213    open returned 5
0214    fi:
0215    flags = 0x00008000
0216    fh_old = 0x00000000
0217    writepage = 0
0218    direct_io = 0
0219    keep_cache = 0
0220    fh = 0x0000000000000005
0221    lock_owner = 0x0000000000000000
0222
bb_read(path="/theFuseFile.txt", buf=0x40000af0, size=4096, offset=0, fi=0x4e81bd40)
0223    fi:
0224    flags = 0x00008000
0225    fh_old = 0x00000005
0226    writepage = 0
0227    direct_io = 0
0228    keep_cache = 0
0229    fh = 0x0000000000000005
0230    lock_owner = 0x0000000000000000
0231
ZCZC READ ==== ==== 
Hello:
This is file "theFuseFile.txt" inside  a mounted FUSE directory.
Jolan Tru!
ˇˇˇˇ
NNNN DONE ==== ====
0232    pread returned 83
0233
bb_fgetattr(path="/theFuseFile.txt", statbuf=0x4f01cc60, fi=0x4f01cd40)
0234    fi:
0235    flags = 0x00000000
0236    fh_old = 0x00000005
0237    writepage = 0
0238    direct_io = 0
0239    keep_cache = 0
0240    fh = 0x0000000000000005
0241    lock_owner = 0x0000000000000000
0242    si:
0243    st_dev = 2081
0244    st_ino = 12324331
0245    st_mode = 0100644
0246    st_nlink = 1
0247    st_uid = 52039
0248    st_gid = 2200
0249    st_rdev = 0
0250    st_size = 83
0251    st_blksize = 4096
0252    st_blocks = 8
0253    st_atime = 0x5f2ae88a
0254    st_mtime = 0x5f2ae846
0255    st_ctime = 0x5f2ae846
0256
bb_flush(path="/theFuseFile.txt", fi=0x4e81bd40)
0257    fi:
0258    flags = 0x00000000
0259    fh_old = 0x00000005
0260    writepage = 0
0261    direct_io = 0
0262    keep_cache = 0
0263    fh = 0x0000000000000005
0264    lock_owner = 0x334b3bff9ad8eeed
0265
bb_release(path="/theFuseFile.txt", fi=0x4f01cd40)
0266    fi:
0267    flags = 0x00008000
0268    fh_old = 0x00000005
0269    writepage = 0
0270    direct_io = 0
0271    keep_cache = 0
0272    fh = 0x0000000000000005
0273    lock_owner = 0x0000000000000000
0274    close returned 0
0275
bb_destroy(userdata=0x0125a010)
200806-001432-80cc-example/> exit
exit

Script done on Thu Aug  6 00:14:43 2020
```
