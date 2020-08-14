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


# 1. Scripting

## 1.1. Scripting Sederhana<br>
**Perintah dasar linux dan fungsinya<br>**
* ls  = melihat isi direktori <br>
* mkdir =  menciptakan direktori <br>
* cd  = mengubah direktori <br>
* rmdir = menghapus direktori <br>
* cat = Menampilkan isi file dan menciptakan file<br>
* cp = Menyalin file<br>
* rm = menghapus file<br>
* mv = mengganti nama file/direktori dan memindahkan file ke direktori lain<br>
* ln = link ke file lain<br>
* lp = Mencetak isi file<br>
* find = mencari file<br>
* chmod = untuk mengubah model akses terhadap file atau direktori<br>
* chgrp = mengubah grup fie<br>
* chown = mengubah kepemilikan dari file<br>
* echo = Menampilkan tulisan yang dibuat setelah perintah echo dan itu tidak disimpan<br>
* sort = Mengurutkan suatu file teks menurut abjad<br>
* cut = Mengambil kolom tertentu dari baris-baris masukannya yang ditentukan pada option–c<br>
* uniq = Menghilangkan baris – baris berurutan yang mengalami duplikasi<br>
* locate = Mencari suatu file pada direktori lain yang sedang tidak dikunjungi<br>
* finger = Melihat informasi user yang telah ditambahkan oleh perintah chfn<br>

## 1.2. Contoh Bash Script
Ini merupakan contoh penggunaan bash pada mode non-interaktif, yaitu dengan membuat dan menjalankan dua bash script sederhana.<br><br>

**Contoh 1:<br>**
Buat sebuah file dengan nama hello. Anda dapat menggunakan editor apa saja yang Anda kehendaki, vi, vim, emacs, nano, gedit, atau yang lainnya. Kemudian ketikkan script berikut:
```#!/bin/bash
echo "Hello World!"
echo "Anda sedang berada di direktori $PWD"
```

Simpan file, kemudian ubah hak akses file tersebut agar dapat dieksekusi:
```
$ chmod 755 hello
```

Jalankan shell script pertama:
```
$ ./hello
Hello World!
Anda sedang berada di direktori /home/user/Documents/Writing/Code/bash
```
Penjelasan untuk script hello:<br>
#!/bin/bash menyatakan bahwa script tersebut harus dijalankan di bash shell. /bin/bash merupakan lokasi dari bash interpreter yang akan menerjemahkan dan menjalankan bash script. Anda dapat mendapatkan lokasi ini dengan menjalankan perintah:
```
$ which bash
/bin/bash
```

$PWD merupakan sebuah variabel yang sudah didefinisikan oleh bash. Dengan meletakkan variabel dalam tanda petik dua (“), bash akan mengganti pernyataan variabel tersebut dengan nilainya, kemudian barulah perintah (dalam kasus ini perintah echo) dijalankan. Nilai variabel $PWD adalah path direktori aktif, layaknya output dari perintah pwd.

**Contoh 2:**
```
!/bin/bash
```
Menampilkan beberapa informasi
 
Menampilkan nama user
```
echo "Halo $USER!"
```

Menampilkan nama Host
```
echo "Halo $HOSTNAME!"
```
 
Menampilkan nama file shell script yang sedang dijalankan
```
echo "Anda sedang menjalankan file bash script '$0'"
```
 
Menampilkan tanggal lokal
```
echo -n "Hari ini tanggal "; date +"%d %B %Y"
```
 
Menampilkan nama direktori aktif
```
echo -n "Anda sedang berada di lokasi "; pwd
```
 
Menampilkan isi direktori aktif
```
echo "Berikut merupakan beberapa file yang terdapat pada direktori aktif:";
ls
```

Menghapus file 
```
rm file1.txt
```

Memindahkan file
```
mv file1.txt tujuandirektori
```

Pindah direktori
```
cd tujuandirektori
```

Mengcopy file
```
cp file.txt tujuandirektori
```

Simpan file tersebut dengan nama tampilkaninfo, kemudian rubah hak akses file agar dapat dieksekusi, dan jalankan.
```
$ chmod 755 tampilkaninfo
$ ./tampilkaninfo
Halo user!
Anda sedang menjalankan file bash script './tampilkaninfo'
Hari ini tanggal 04 Agustus 2020
Anda sedang berada di lokasi /home/user/Documents/Writing/Code/bash
```

Berikut merupakan beberapa file yang terdapat pada direktori aktif:
```
hello tampilkaninfo
```

Penjelasan untuk script tampilkaninfo:
<br>
Variabel $USER menyimpan nama user. $USER merupakan salah satu variabel lingkungan (environment variable) yang telah didefinisikan nilainya oleh sistem, dan perubahan terhadap nilai variabel lingkungan mempengaruhi kerja sistem. Telah dijelaskan sebelumnya, jika variabel $0 digunakan di shell script, maka akan memiliki nilai nama file script tersebut.<br><br>
Dengan menggunakan argumen -n pada echo, teks tidak diakhiri dengan newline (ganti baris). Sehingga tulisan Hari ini tanggal dan hasil pemanggilan perintah date +"%d %B %Y" (untuk menampilkan tanggal lokal saat script dijalankan dengan format tanggal “tanggal nama bulan tahun”) dapat ditampilkan dalam baris yang sama. Tulisan Anda sedang berada di lokasi dengan hasil pemanggilan perintah pwd juga dapat ditampilkan pada baris yang sama dengan meniadakan newline pada akhir output pemanggilan echo.

# 2. EditorLinux 

Editor atau biasa disebut text editor, merupakan suatu program yang digunakan untuk keperluan editing file teks. Ada beberapa hal yang 
membedakan editor Linux dengan editor biasa pada umumnya. Ada beberapa editor Linux yang hanya berbasis CLI seperti VIM, Emacs atau Nano. 
Jika di Windows, kita menemukan Notepad sebagai editor sederhana maka di Linux kita juga akan menemukan Gedit atau Geany. Jika di Windows, 
kita dimanjakan dengan tampilan yang menarik dan serba GUI maka di Linux berbeda.
<br>
```
Selengkapnya: https://www.domainesia.com/tips/5-editor-linux-yang-wajib-kamu-tahu/
```

# 3. GCC

## 3.1. Perintah GCC
Untuk melakukan pemrograman C di Linux, kita dapat memanfaatkan kompilator GCC (GNU C Compiler) atau (GNU Collection Compiler).

**Contoh :<br>**

Perintah untuk kompilasi program C
```
gcc kode_program.c -o nama_program
```

Perintah untuk menjalankan program
```
./nama_program
```

Contoh kode program
```
#include <stdio.h>

void main(){
    printf("Hello World\n");
}
```

# 4. MakeFile

Contoh aplikasi pada bahasa C dengan menggunakan compiler GCC pada linux / Cygwin.

**Contoh 1:<br>**
Misalkan, telah dibuat program “latihan.c”, maka cara untuk meng-compile-nya adalah dengan mengetikkan syntax berikut pada terminal:
```
gcc -Wall -I. -O2 -o latihan latihan.c
```
Jika file-nya dua dan dalam satu folder, misalkan “latihan.c” dan “latihan2.c” dan ingin di compile menjadi executable file “latihan”, maka:
```
gcc -o latihan latihan.c latihan2.c
```

**Contoh 2:<br>**

Jika dalam suatu project di mana ada ratusan file dan lokasi file berada pada folder yang berbeda-beda, maka yang kita ketikkan di terminal akan lebih banyak lagi, misal:
```
gcc -Wall -I. -I../coba -I../coba2 … -I../cobaX -O2 -o latihan latihan1.c ../coba1/latihan2.c ../coba2/latihan3.c … ../cobaX/latihanX.c
```
Maka syntax yang harus diketik akan semakin banyak jika menerapkan Contoh 1. Pada kasus ini, “makefile” adalah jalan keluarnya. 
Secara sederhana, makefile dapat diartikan sebagai suatu file yang berisi sekumpulan instruksi yang dipanggil saat kita mengetikkan “make” 
atau “makefile” di terminal. Dengan adanya makefile, programmer cukup memasukkan nama file yang akan di-compile lalu mengetikkan “make” di terminal, 
dan semuanya langsung selesai.

Secara umum, makefile terdiri dari macro yg berisi suatu definisi-definisi tertentu dan juga command yang akan dijalankan. Sebagai contoh 
kasus meng-compile file yang cukup banyak tadi, dapat dituliskan dalam makefile yang akan diuraikan di bawah ini.

Makro
```
TARGET = Latihan
XCC = gcc
DEBUG = -g
CFLAGS = -Wall $(DEBUG)
OBJS = latihan1.o latihan2.o latihan3.o
PATH = ../coba1 ../coba2 ../coba3
```

Syntax untuk compile
```
$(TARGET) : $(OBJS)
$(XCC) $(CFLAGS) $(OBJS) -I$(PATH) -o $(TARGET)

latihan1.o : latihan1.c latihan1.h
$(XCC) $(CFLAGS) -I$(PATH) -c latihan1.c

latihan2.o : latihan2.c latihan2.h
$(XCC) $(CFLAGS) -I$(PATH) -c latihan2.c

latihan3.o : latihan3.c latihan3.h
$(XCC) $(CFLAGS) -I$(PATH) -c latihan3.c
```

Syntax untuk membersihkan file yang tidak perlu
```
clean :
rm -rf *.o
```

# 5. TAR

## 5.1. Cara menggunakan TAR Linux
Berikut akan dijelaskan operasi dasar yang bisa dilakukan dengan menggunakan Linux tar. Namun sebelumnya, kita harus masuk ke VPS server 
terlebih dulu melalui SSH. (link dimasukkan ke bagian SSH)

Membuat File Arsip .tar di Linux, kita dapat membuat kompresi .tar untuk file dan direktori. Contoh arsipnya adalah sebagai berikut:
```
tar -cvf sampleArchive.tar /home/sampleArchive

/home/sampleArchive adalah direktori yang perlu di-compress untuk membuat sampleArchive.tar.
```

Command tersebut menggunakan opsi –cvf yang merupakan singkatan dari:
```
c – untuk membuat file .tar baru
v – menunjukkan deskripsi verbose dari proses kompresi
f – nama file
```

Membuat File .tar.gz pada Linux, jika kita menginginkan proses kompresi yang lebih baik, gunakan .tar.gz. Sebagai contoh:
```
tar -cvzf sampleArchive.tar.gz /home/sampleArchive
```

Penambahan opsi z merepresentasikan kompresi gzip. Cara lainnya, kita dapat membuat file .tgz yang command-nya mirip dengan tar.gz. Contohnya seperti yang ditunjukkan di bawah ini:
```
tar -cvzf sampleArchive.tgz /home/sampleArchive
```

Membuat File .tar.bz2 pada Linux. File .bz2 menyediakan lebih banyak kompresi dibandingkan dengan gzip. Namun, kita akan membutuhkan lebih banyak waktu untuk melakukan compress dan decompress. Untuk membuat ini, kita perlu menggunakan opsi -j. Contoh operasi adalah:
```
tar -cvjf sampleArchive.tar.bz2 /home/sampleArchive
```

Operasi ini mirip dengan .tar.tbz atau .tar.tb2. Contohnya seperti yang ditunjukkan di bawah ini:
```
tar -cvjf sampleArchive.tar.tbz /home/sampleArchive
tar -cvjf sampleArchive.tar.tb2 /home/sampleArchive
```

Cara Unzip File .tar pada Linux. Command tar juga dapat digunakan untuk mengekstrak file. Command di bawah ini akan mengekstrak file yang ada di dalam direktori saat ini:
```
tar -xvf sampleArchive.tar
```

Jika kita ingin mengekstrak file ke direktori yang berbeda, gunakan opsi -C. Salah satu contohnya seperti di bawah ini:
```
tar -xvf sampleArchive.tar -C /home/ExtractedFiles/
```

Command serupa dapat digunakan untuk membuka kompresi file .tar.gz seperti yang ditunjukkan di bawah ini:
```
tar -xvf sampleArchive.tar.gz
tar -xvf sampleArchive.tar.gz -C /home/ExtractedFiles/
```

File .tar.bz2 atau .tar.tbz atau .tar.tb2 dapat dikompresi dengan cara yang sama. Gunakan command di bawah ini:
```
tar -xvf sampleArchive.tar.bz2
```

Cara Menampilkan Daftar Isi Arsip di Linux. Setelah arsip dibuat, kita dapat menampilkan daftar konten menggunakan command yang mirip dengan yang di bawah ini:
```
tar -tvf sampleArchive.tar
```

Command ini akan menampilkan daftar semua file lengkap dengan timestamps dan permission. Demikian pula, untuk .tar.gz, kita dapat menggunakan command seperti:
```
tar -tvf sampleArchive.tar.gz
```

Command di atas juga dapat digunakan untuk file .tar.bz2 seperti yang ditunjukkan di bawah ini:
```
tar -tvf sampleArchive.tar.bz2
```

Cara Unzip File Tunggal .tar. Setelah arsip dibuat, kita dapat mengekstrak sebuah file. Berikut salah satu contohnya:
```
tar -xvf sampleArchive.tar example.sh
```

example.sh adalah file tunggal yang akan diekstra dari sampleArchive.tar. kita juga bisa menggunakan command berikut:
```
tar --extract --file= sampleArchive.tar example.sh
```

Untuk mengekstrak satu file dari .tar.gz, gunakan command yang mirip dengan yang ditunjukkan di bawah ini:
```
tar -zxvf sampleArchive.tar.gz example.sh
```

Atau cara lain seperti berikut ini:
```
tar --extract --file= sampleArchive.tar.gz example.sh
```

Untuk mengekstrak satu file dari .tar.bz2, gunakan command seperti ini:
```
tar -jxvf sampleArchive.tar.bz2 example.sh
```

Atau cara lain seperti berikut ini:
```
tar --extract --file= sampleArchive.tar.bz2 example.sh
```

Cara Ekstrak Banyak File dari Arsip .tar. Jika kita ingin mengekstrak banyak file sekaligus, gunakan format command berikut:
```
tar -xvf sampleArchive.tar "file1" "file2"
```

Untuk .tar.gz, gunakan:
```
tar -zxvf sampleArchive.tar.gz "file1" "file2"
```

Untuk .tar.gz2, gunakan command:
```
tar -jxvf sampleArchive.tar.bz2 "file1" "file2"
```

Ekstrak Banyak File dengan Pattern. Jika kita ingin mengekstraksi pattern file tertentu seperti hanya mengekstrak file .jpg dari arsip, kita dapat gunakan wildcard. Contoh dari command tersebut adalah seperti yang ditunjukkan di bawah ini:
```
tar -xvf sampleArchive.tar --wildcards '*.jpg'
```

Untuk .tar.gz, gunakan:
```
tar -zxvf sampleArchive.tar.gz --wildcards '*.jpg'
```

Untuk .tar.gz2, gunakan command:
```
tar -jxvf sampleArchive.tar.bz2 --wildcards '*.jpg'
```

Cara Menambahkan File ke Arsip .tar. Selain mengekstrak file, kita juga dapat menambahkan file ke dalam arsip yang ada. Untuk melakukannya, kita akan menggunakan opsi -r yang merupakan singkatan dari append. Tar dapat menambahkan file dan direktori.
Di bawah ini adalah contoh di mana kita akan menambahkan example.jpg ke sampleArchive.tar yang ada.
```
tar -rvf sampleArchive.tar example.jpg
```

Kita juga dapat menambahkan direktori. Pada contoh di bawah ini, direktori image_dir ditambahkan ke sampleArchive.tar
```
tar -rvf sampleArchive.tar image_dir
```

Kita tidak dapat menambahkan file atau folder ke file .tar.gz atau .tar.bz2. Karena file tersebut untuk single file saja.
Cara Memverifikasi Arsip .tar di Linux. Kita dapat memverifikasi arsip dengan menggunakan tar . Berikut ini adalah salah satu cara untuk melakukannya:
```
tar -tvf sampleArchive.tar
```

Command di atas tidak dapat diterapkan pada file .tar.gz atau .tar.bz2.
Cara Memeriksa Ukuran Arsip di Linux. Setelah arsip dibuat, Anda dapat mengecek ukurannya. Satuan ukuran arsip akan ditampilkan dalam format KB (Kilobyte). Di bawah ini adalah contoh dari command tersebut dengan file arsip yang berbeda:
```
tar -czf - sampleArchive.tar | wc -c
tar -czf - sampleArchive.tar.gz | wc -c
tar -czf - sampleArchive.tar.bz2 | wc -c
```

# 6. GIT

# 7. GitHub

# 8. SHA1

## 8.1. Cara mendapatkan SHA-1 file
Untuk mendapatkan SHA-1 file, lakukan perintah sha1sum. <br>
SHA-1 akan dicetak terlebih dahulu SHA-1 checksum kemudian nama file.<br>
Contoh:
```
azispro@DESKTOP-F1JL3Q7:~$ ls -F
Buku.txt  Jadwal.txt  Panduan.txt  Project.txt  Tugas.txt

azispro@DESKTOP-F1JL3Q7:~$ sha1sum Buku.txt  Jadwal.txt  Panduan.txt  Project.txt  Tugas.txt
da39a3ee5e6b4b0d3255bfef95601890afd80709 *Buku.txt
da39a3ee5e6b4b0d3255bfef95601890afd80709 *Jadwal.txt
da39a3ee5e6b4b0d3255bfef95601890afd80709 *Panduan.txt
da39a3ee5e6b4b0d3255bfef95601890afd80709 *Project.txt
da39a3ee5e6b4b0d3255bfef95601890afd80709 *Tugas.txt
```

## 8.2. Cara menulis SHA-1 dari sebuah file
Untuk menulis SHA-1 dari file  dapat menggunakan standard shell redirection<br>
Contoh:
```
azispro@DESKTOP-F1JL3Q7:~$ sha1sum Buku.txt  Jadwal.txt  Panduan.txt  Project.txt  Tugas.txt > SHA1SUM
azispro@DESKTOP-F1JL3Q7:~$ cat SHA1SUM
da39a3ee5e6b4b0d3255bfef95601890afd80709 *Buku.txt
da39a3ee5e6b4b0d3255bfef95601890afd80709 *Jadwal.txt
da39a3ee5e6b4b0d3255bfef95601890afd80709 *Panduan.txt
da39a3ee5e6b4b0d3255bfef95601890afd80709 *Project.txt
da39a3ee5e6b4b0d3255bfef95601890afd80709 *Tugas.txt
```

## 8.3. Cara memeriksa SHA-1 file
Jika file SHA-1 telah disediakan dari download, ini dapat digunakan untuk memeriksa integritas file yang diunduh apakah sempurna atau corrupt <br>
Untuk memeriksa SHA-1 file, gunakan opsi -c dan berikan file SHA-1 checksum yang sesuai dengan file atau file yang ingin Anda periksa <br>
Jika file tidak disediakan dengan unduhan, penulis file biasanya akan mempublikasikan intisari pesan SHA-1 dan ini dapat diperiksa secara manual dengan membandingkan output dari sha1sum [file] dengan intisari pesan yang diterbitkan.<br>
**Contoh :**
```
azispro@DESKTOP-F1JL3Q7:~$ ls -F
Buku.txt  Jadwal.txt  Panduan.txt  Project.txt  SHA1SUM  Tugas.txt
azispro@DESKTOP-F1JL3Q7:~$ sha1sum -c SHA1SUM
Buku.txt: OK
Jadwal.txt: OK
Panduan.txt: OK
Project.txt: OK
Tugas.txt: OK
```

Jika verifikasi gagal, mungkin ada perubahan terhadap file atau terjadi corrupt ketika download selesai maka akan muncul FAILED <br>
Contoh:
```
azispro@DESKTOP-F1JL3Q7:~$ ls -F
Buku.txt  Jadwal.txt  Panduan.txt  Project.txt  SHA1SUM  Tugas.txt
azispro@DESKTOP-F1JL3Q7:~$ sha1sum -c SHA1SUM
Buku.txt: FAILED
Jadwal.txt: FAILED
Panduan.txt: FAILED
Project.txt: FAILED
Tugas.txt: FAILED
sha1sum: WARNING: 5 computed checksums did NOT match
```

# 9. GnuPG

## 9.1. Cara Install GnuPG

Silahkan download GnuPG
[https://gnupg.org/download/index.html](https://gnupg.org/download/index.html)

## 9.2. Informasi GnuPG

* Version `--version` <br>
Perintah `--version` digunakan untuk mendapatkan informasi tentang versi gpg (GnuPG)<br>
Contoh:
```
azispro@DESKTOP-F1JL3Q7:~$ gpg --version
```

* Help `--help` <br>
Perintah `--help` untuk menampilkan informasi pilihan baris perintah yang paling berguna<br>
Contoh:
```
azispro@DESKTOP-F1JL3Q7:~$ gpg --help
```

* Warranty `--warranty`  <br>
Perintah `--warranty` ini digunakan untuk menampilkan informasi tentang jaminan<br>
Contoh:
```
azispro@DESKTOP-F1JL3Q7:~$ gpg --warranty
```

* Dump Options `--dump-options` <br>
Perintah `--dump-options` ini digunakan untuk menampilkan daftar semua pilihan perintah yang tersedia<br>
Contoh:
```
azispro@DESKTOP-F1JL3Q7:~$ gpg --dump-options
```


## 9.3. Perintah Menjalankan GnuPG


* PEMBUATAN KEY BARU
`--gen-key` <br>
Perintah `--gen-key` digunakan untuk membuat keypair primer baru<br>
Contoh:
```
azispro@DESKTOP-F1JL3Q7:~$ gpg --gen-key
gpg (GnuPG) 2.2.19; Copyright (C) 2019 Free Software Foundation, Inc.
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.

Note: Use gpg --full-generate-key for a full featured key generation dialog.

GnuPG needs to construct a user ID to identify your key.

Real name: Abdul Azis
Email address: abdul.azis02@ui.ac.id
You selected this USER-ID:
   Abdul Azis <abdul.azis02@ui.ac.id>

Change (N)ame, (E)mail, or (O)kay/(Q)uit? O
We need to generate a lot of random bytes. It is a good idea to perform
some other action (type on the keyboard, move the mouse, utilize the
disks) during the prime generation; this gives the random number
generator a better chance to gain enough entropy.
We need to generate a lot of random bytes. It is a good idea to perform
some other action (type on the keyboard, move the mouse, utilize the
disks) during the prime generation; this gives the random number
generator a better chance to gain enough entropy.
gpg: key 76E13F79CB6E215B marked as ultimately trusted
gpg: revocation certificate stored as '/home/azispro/.gnupg/openpgp-revocs.d/1963BE483E02BA97D749BEBA76E13F79CB6E215B.rev'
public and secret key created and signed.

pub   rsa3072 2020-07-14 [SC] [expires: 2022-07-14]
      1963BE483E02BA97D749BEBA76E13F79CB6E215B
uid                      Abdul Azis <abdul.azis02@ui.ac.id>
sub   rsa3072 2020-07-14 [E] [expires: 2022-07-14]
```

* PENCABUTAN SERTIFIKASI
`--gen-revoke` <br>
Perintah `--gen-revoke` digunakan untuk membuat certificate pembatalan<br>
Contoh:
```
azispro@DESKTOP-F1JL3Q7:~$ gpg --output azis.asc --gen-revoke abdul.azis02@ui.ac.id
sec  rsa3072/76E13F79CB6E215B 2020-07-14 Abdul Azis <abdul.azis02@ui.ac.id>
Create a revocation certificate for this key? (y/N) y
Please select the reason for the revocation:
   0 = No reason specified
   1 = Key has been compromised
   2 = Key is superseded
   3 = Key is no longer used
   Q = Cancel
(Probably you want to select 1 here)
Your decision? 1
Enter an optional description; end it with an empty line:
>
Reason for revocation: Key has been compromised
(No description given)
Is this okay? (y/N) y
ASCII armored output forced.
Revocation certificate created.

Please move it to a medium which you can hide away; if Mallory gets
access to this certificate he can use it to make your key unusable.
It is smart to print this certificate and store it away, just in case
your media become unreadable.  But have some caution:  The print system of
your machine might store the data and make it available to others!
```

* MELIHAT DAFTAR KEY
`--list-keys` <br>
Perintah `--list-keys` digunakan untuk menampilkan daftar key
Contoh:
```
azispro@DESKTOP-F1JL3Q7:~$ gpg --list-keys
gpg: checking the trustdb
gpg: marginals needed: 3  completes needed: 1  trust model: pgp
gpg: depth: 0  valid:   2  signed:   0  trust: 0-, 0q, 0n, 0m, 0f, 2u
gpg: next trustdb check due at 2022-07-14
/home/azispro/.gnupg/pubring.kbx
--------------------------------
pub   rsa2048 2020-06-03 [SC]
      AD438A6627B1B80466E2B4583B7001D914CC44BE
uid           [ unknown] Abdul Azis (Universitas Indonesia) <abdulazis483@gmail.com>
sub   rsa2048 2020-06-03 [E]

pub   rsa3072 2020-07-14 [SC] [expires: 2022-07-14]
      D9CD602CFC312D18A5A90F7B6F1768519CF3C290
uid           [ultimate] Abdul Azis <azispro@icloud.com>
sub   rsa3072 2020-07-14 [E] [expires: 2022-07-14]

pub   rsa3072 2020-07-14 [SC] [expires: 2022-07-14]
      1963BE02BA97D749BEBA76E13F79CB6E215B
uid           [ultimate] Abdul Azis <abdu2@ui.ac.id>
sub   rsa3072 2020-07-14 [E] [expires: 2022-07-14]
```

* EXPORT PUBLIC KEY
`--export` <br>
Perintah `--export` digunakan untuk mengirim public key<br>
Contoh:
```
azispro@DESKTOP-F1JL3Q7:~$ gpg --armor --export abdul.azis02@ui.ac.id
-----BEGIN PGP PUBLIC KEY BLOCK-----

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
p9VNCekOKGinLU4vt+SHk7nLFCE9TPCHj8M=
=ka/1
-----END PGP PUBLIC KEY BLOCK-----
```

* IMPORT PUBLIC KEY
`--import` <br>
Perintah `--import` digunakan untuk memasukan public key<br>
Contoh: 
```
azispro@DESKTOP-F1JL3Q7:~$ gpg --import azispub.gpg
gpg: key 76E13F79CB6E215B: public key Abdul Azis <abdul.azis02@ui.ac.id> imported
gpg: Total number processed: 1
gpg:               imported: 1
```

* ENKRIPSI PESAN
--encrypt <br>
Perintah `--encrypt` digunakan untuk mengenkripsi pesan<br>
Contoh:
```
azispro@DESKTOP-F1JL3Q7:~$ gpg --output enkripsipesan.asc --encrypt --recipient azispro@icloud.com Cara-Mean-GnuPG.txt
```


* DEKRIP PESAN
`--decrypt` <br>
Perintah `--decrypt` digunaka mengenkripsi pesan<br>
Contoh:
```
azispro@DESK-F1JL3Q7:~$ gpg --output dsan.txt --decrypt enkripsipesan.asc
gpg: encrypted with 3072-bit key, ID BD53FCC7D21719A0, created 2020-07-14
      Abdul Azis <azispro@icloud.com>
```

* MENANDATANGANI BERKAS
`--sign` <br>
Perintah `--sign` digunakan untuk menandatangani berkas dengan mengenkripsi dokumen.<br>
Contoh:
```
azispro@DESKTOP-F1JL3Q7:~$ gpg --output ttdberkas.asc --sign Cara-Menggunakan-GnuPG.txt
```

* VERIFIKASI BERKAS
`--verify` <br>
Perintah `--verify` digunakan untuk memverifikasi berkas yang telah ditandatangani<br>
Contoh:
```
azispro@DESKTOP-F1JL3Q7:~$ gpg --verify ttdberkas.asc
gpg: Signature made Tue Jul 14 18:14:59 2020 +07
gpg:                using RSA key D9CDFC312D18A5A90F7B6F1768519CF3C290
gpg: Good signature from Abdul Azis <azispro@icloud.com> [ultim
```

* CLEARSIGNED BERKAS
`--clearsign` <br>
Perintah `--clearsign` digunakan untuk menandatangani berkas tanpa mengenkripsi dokumen <br>
Contoh:
```
azispro@DESKTOP-F1JL3Q7:~$ gpg --clearsign Cara-Menggunakan-GnuPG.txt
```

* VERIFIKASI CLEARSIGNED BERKAS
`--verify` <br>
Perintah `--verify` digunakan untuk memverifikasi berkas yang telah ditandatangani<br>
Contoh:
```
azispro@DESKTOP-F1JL3Q7:~$ gpg --verify Cara-Menggunakan-GnuPG.txt.asc
gpg: Signature made Tue Jul 14 18:20:31 2020 +07
gpg:                using RSA key D9CD602CFC312D18A5A90F7B6F1768519CF3C290
gpg: Good signature from Abdul Azis <azispro@icloud.com> [ultimate]
gpg: WARNING: not a detached signature; file 'Cara-Menggunakan-GnuPG.txt' was NOT verified!
```

*  TANDA TANGAN TERPISAH
`--detach-sig` <br>
Perintah `--detach-sig` untuk membuat tanda tangan terpisah dari berkas<br>
Contoh: 
```
azispro@DESKTOP-F1JL3Q7:~$ gpg --output ttdterpisah.sig --detach Cara-Menggunakan-GnuPG.txt
```

*  VERIFIKASI TANDA TANGAN TISAH
`--verify` <br>
Perintah `--verify` digunakan untuk memverifikasi berkas yang telah ditandatangani dengan tandan tangan yang terpisah <br>
Contoh: 
```
azispro@DESKTOP-F1JL3Q7:~$ gpg --verify ttdterpg Cara-Menggunakan-GnuPG.txt
gpg: Signature made Tue Jul 14 18:23:09 2020 +07
gpg:                using RSA key D9CD602CFC312D18A5A90F7B6F1768519CF3C290
gpg: Good signature from Abdul Azis <azispro@icloud.com> [ultimate]
```

* ENKRIPSI SIMETRIS
`--symmetric` <br>
Perintah `--symmetric` digunakan untuk mengenkripsi simetris sebuah file<br>
Contoh: 
```
azispro@DESKTOP-F1JL3Q7:~$ gpg --symmetric Cara-Menggunakan-GnuPG.txt
```

* DEKRIPSI SIMETRIS
`--decrypt`<br>
Perintah `--symmetric` digunakan untuk mendekripsi sebuah file yang telah dienkripsi<br>
Contoh: 
```
azispro@DESKTOP-F1JL3Q7:~$ gpg --output dekripsifile.txt --decrypt Cara-Menggunakan-GnuPG.txt.gpg
gpg: AES256 encrypted data
gpg: encrypted with 1 passphrase
```

* MULTIFILE
`--multifile`<br>
Perintah `--multifile` digunakan untuk mengakses beberapa file<br>
Contoh:
```
azispro@DESKTOP-F1JL3Q7:~$ gpg --le --encrypt --recipient abdulazis483@gmail.com --recipient azispro@icloud.com azis1.txt azis2.txt
gpg: 0D2BBA731F7DA2A4: There is no assurance this key belongs to the named user

sub  rsa2048/0D2BBA731F7DA2A4 2020-06-03 Abdul Azis (Universitas Indonesia) <abdulazis483@gmail.com>
 Primary key fingerprint: AD43 8A66 27B1 B804 66E2  B458 3B70 01D9 14CC 44BE
      Subkey fingerprint: 12EF A0EA 798B B186 CCE0  2625 0D2B BA73 1F7D A2A4

It is NOT certain that the key belongs to the person named
in the user ID.  If you *really* know what you are doing,
you may answer the next question with yes.

Use this key anyway? (y/N) y
gpg: 0D2BBA731F7DA2A4: There is no assurance this key belongs to the named user

sub  rsa2048/0D2BBA731F7DA2A4 2020-06-03 Abdul Azis (Universitas Indonesia) <abdulazis483@gmail.com>
 Primary key fingerprAD43 8A66 27B1 B804 66E2  B458 3B70 01D9 14CC 44BE
      Subkey fingerprint: 12EF A0EA 798B B186 CCE0  2625 0D2B BA73 1F7D A2A4

It is NOT certain that the key belongs to the person named
in the user ID.  If you *really* know what you are doing,
you may answer the next question with yes.

Use this key anyway? (y/N) y
```

* DAFTAR PUBLIC KEY
`--list-public-key`<br>
Perintah --list-public-key digunakan untuk menampilkan daftar public key<br>
Contoh:
```
azispro@DESKTOP-F1JL3Q7:~$ gpg --list-public-keys
/home/azispro/.gnupg/pubring.kbx
--------------------------------
pub   rsa2048 2020-06-03 [SC]
      AD438A6627B1B80466E2B4583B7001D914CC44BE
uid           [ unknown] Abdul Azis (Universitas Indonesia) <abdulazis483@gmail.com>
sub   rsa2048 2020-06-03 [E]

pub   rsa3072 2020-07-14 [SC] [expires: 2022-07-14]
      D9CD602CFC312D18A5A90F7B6F1768519CF3C290
uid           [ultimate] Abdul Azis <azispro@icloud.com>
sub   rsa3072 2020-07-14 [E] [expires: 2022-07-14]

pub   rsa3072 2020-07-14 [SC] [expires: 2022-07-14]
      1963BE483E97D749BEBA76E13F79CB6E215B
uid           [ unknown] Abdul Azis <abdul.azis02@ui.ac.id>
sub   rsa3072 2020-07-14 [E] [expires: 2022-07-14]
```

* DAFTAR SECRET KEY
`--list-secret-key`<br>
Perintah `--list-secret-key`  digunakan untuk menampilkan daftar secret key<br>
Contoh:
```
azispro@DESKTOP-F1JL3Q7:~$ gpg --list-secret-keys
/home/azispro/.gnupg/pubring.kbx
--------------------------------
sec   rsa3072 2020-07-14 [SC] [expires: 2022-07-14]
      D9CD602CFC312D18A5A90F7B6F1768519CF3C290
uid           [ultimate] Abdul Azis <azispro@icloud.com>
ssb   rsa3072 2020-07-14 [E] [expires: 2022-07-14]
```

* DAFTAR TANDA TANGAN
`--list-sigs`<br>
Perintah `--list-sigs`  digunakan untuk menampilkan daftar tanda tangan yang tersimpan<br>
Contoh:
```
azispro@DESKTOP-F1JL3Q7:~$ gpg --list-sigs
/home/azispro/.gnupg/pubring.kbx
--------------------------------
pub   rsa2048 2020-06-03 [SC]
      AD438A6627B1B80466E2B4583B7001D914CC44BE
uid           [ unknown] Abdul Azis (Universitas Indonesia) <abdulazis483@gmail.com>
sig 3        3B7001D914CC44BE 2020-06-03  Abdul Azis (Universitas Indonesia) <abdulazis483@gmail.com>
sub   rsa2048 2020-06-03 [E]
sig          3B7001D914CC44BE 2020-06-03  Abdul Azis (Universitas Indonesia) <abdulazis483@gmail.com>

pub   rsa3072 2020-07-14 [SC] [expires: 2022-07-14]
      D9CD602CFC312D18A5A90F7B6F1768519CF3C290
uid           [ultimate] Abdul Azis <azispro@icloud.com>
sig 3        6F1768519CF3C290 2020-07-14  Abdul Azis <azispro@icloud.com>
sub   rsa3072 2020-07-14 [E] [expires: 2022-07-14]
sig          6F1768519CF3C290 2020-07-14  Abdul Azis <azispro@icloud.com>

pub   rsa3072 2020-07-14 [SC] [expi022-07-14]
      1963BE483E02BA97D749BEBA76E13F79CB6E215B
uid           [ unknown] Abdul Azis <abdul.azis02@ui.ac.id>
sig 3        76E13F79CB6E215B 2020-07-14  Abdul Azis <abdul.azis02@ui.ac.id>
sub   rsa3072 2020-07-14 [E] [expires: 2022-07-14]
sig          76E13F79CB6E215B 2020-07-14  Abdul Azis <abdul.azis02@ui.ac.id>
```

* MENGECEK TANDA TANGAN
`--check-sigs`<br>
Perintah `--check-sigs`  digunakan untuk menampilkan daftar tanda tangan yang terverifikasi<br>
Contoh:
```
azispro@DESKTOP-F1JL3Q7:~$ gpg --check-sigs
/home/azispro/.gnupg/pubring.kbx
--------------------------------
pub   rsa2048 2020-06-03 [SC]
      AD438A6627B1B80466E2B4583B7001D914CC44BE
uid           [ unknown] Abdul Azis (Universitas Indonesia) <abdulazis483@gmail.com>
sub   rsa2048 2020-06-03 [E]
sig!         3B7001D914CC44BE 2020-06-03  Abdul Azis (Universitas Indonesia) <abdulazis483@gmail.com>

pub   rsa3072 2020-07-14 [SC] [expires: 2022-07-14]
      D9CD602CFC312D18A5A90F7B6F1768519CF3C290
uid           [ultimate] Abdul Azis <azispro@icloud.com>
sub   rsa3072 2020-07-14 [E] [expires: 2022-07-14]
sig!         6F1768519CF3C290 2020-07-14  Abdul Azis <azispro@icloud.com>

pub   rsa3072 2020-07-14 [SC] [expires: 2022-07-14]
      1963BE483E02BA97D749BEBA76E13F79CB6E215B
uid           [ unknown] Abdul Azis <abdul.azis02@ui.ac.id>
sub   rsa3072 2020-07-14 [E] [expires: 2022-07-14]
sig!         76E13F79CB6E215B 2020-07-14  Abdul Azis <abdul.azis02@ui.ac.id>

gpg: 6 good signatures
```

* FINGERPRINT
`--fingerprint` <br>
Perintah  `--fingerprint`  digunakan enampilkan daftar fingerprint<br>
Contoh:
```
azispro@DESKTOP-F1JL3Q7:~$ gpg --fingerprint
/home/azispro/.gnupg/pubring.kbx
--------------------------------
pub   rsa2048 2020-06-03 [SC]
      AD43 8A66 27B1 B804 66E2  B458 3B70 01D9 14CC 44BE
uid           [ unknown] Abdul Azis (Universitas Indonesia) <abdulazis483@gmail.com>
sub   rsa2048 2020-06-03 [E]

pub   rsa3072 2020-07-14 [SC] [expires: 2022-07-14]
      D9CD 602C FC31 2D18 A5A9  0F7B 6F17 6851 9CF3 C290
uid           [ultimate] Abdul Azis <azispro@icloud.com>
sub   rsa3072 2020-07-14 [E] [expires: 2022-07-14]

pub   rsa3072 2020-07-14 [SC] [expires: 2022-07-14]
      1963 BE48 3E02 BA97 D749  BEBA 76E1 3F79 CB6E 215B
uid           [ unknown] Abdul Azis <abdul.azis02@ui.ac.id>
sub   rsa3072 2020-07-14 [E] [expires: 2022-07-14]
```

* HAPUS PUBLIC KEY
`--delete-key`<br>
Perintah `--delete-key` digunakan untuk menghapus public key<br>
Contoh:
```
azispro@DESKTOP-F1JL3Q7:~$ gpg --delete-key abdulazis483@gmail.com
gpg (GnuPG) 2.2.19; Copyright (C) 2019 Free Software Foundation, Inc.
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.


pub  rsa2048/3B7001D914CC44BE 2020-06-03 Abdul Azis (Universitas Indonesia) <abdulazis483@gmail.com>

Delete this key from the keyring? (y/N) y
```

* HAPUS SECRET KEY
`--delete-secret-key`<br>
Perintah `--delete-secret-key` digunakan untuk menghapus secret key<br>
Contoh:
```
gpg --delete-secret-key abdulazis483@gmail.com
gpg (GnuPG) 2.2.19; Copyright (C)Free Software Foundation, Inc.
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.


sec  rsa3072/8D2AEFE497EA8BDF 2020-07-14 Abdul Azis <abdulazis483@gmail.com>

Delete this key from the keyring? (y/N) y
This is a secret key! - really delete? (y/N) y
```

* EXPORT SECRET KEY
 `--export-secret-keys`<br>
Perintah `--export-secret-keys` digunakan untuk mengirim secret key<br>
Contoh:
```
azispro@DESKTOP-F1JL3Q7:~$ gpg --output secretazis.asc --export-secret-keys azispro@icloud.com
```
