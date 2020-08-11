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

# BAGIAN A: ISTILAH

## 1. "akunGitHub" -- Nama akun yang digunakan untuk mengakses GitHub.com.
== PERHATIAN: Dalam bash akan digunakan variable "GitHubUser".

## 2. "PRIBADI"    -- Proyek OS201 pribadi, yaitu 
== == https://github.com/akunGitHun/os201/
== a. "UAS-PRIBADI/" -- Folder "UAS/" dalam "PRIBADI".
== b. "UAS-PRIBADI/.dummy" -- Berkas "UAS/.dummy" dalam "PRIBADI".
== c. "WEB-PRIBADI/" -- situs GitHub page pribadi 
== == https://akunGitHub.github.io/os201/.

## 3. "BERSAMA" -- Proyek OS201 bersama, yaitu 
== == https://github.com/UI-FASILKOM-OS/os201/.
== a. "UAS-BERSAMA/" -- Folder "UAS/" dalam "BERSAMA".
== b. "UAS-BERSAMA/.dummy" -- Berkas "UAS/.dummy" dalam "BERSAMA".

# BAGIAN B: Ketentuan UAS 201 untuk kelas A, B, C, M

## 1. GitHub.com:
== a. memiliki: "akunGitHub".
== b. membuka proyek "PRIBADI".
== c. membuat GitHub Page "WEB-PRIBADI/".
== d. memiliki akses ke proyek "BERSAMA".
== == HARAP SEGERA MEMBERI TAHU via SCELE, jika belum memiliki AKSES!
== e. memahami cara membuat/memodifikasi/menghapus berkas maupun folder.
== f. menambahkan baris "OS201 akunGitHub" pada log setiap "commit".
== g. membuat berkas baru "UAS-PRIBADI/.dummy" dan "UAS-BERSAMA/akunGitHub/.dummy".
== == menghapus berkas .dummy tersebut jika sudah tidak diperlukan.
== h. memilih menggunakan "antarmuka Web", "CLI", atau pun keduanya.
== == Lihat juga SCELE:
== == https://scele.cs.ui.ac.id/mod/forum/discuss.php?d=16744

## 2. GNUPG:
== a. memiliki gnupg private/public key yang masih berlaku.
== b. silakan menggunakan keys yang pernah dibuat sebelumnya.
== c. jika yang lama hilang, silakan membuat pasangan keys baru.
== d. jika ragu, silakan menghapus total sistem gpg yang lama.
== e. Dapat membuat tanda-tangan digital, enkripsi/dekripsi.
== f. Meletakkan text "public key" (armor) ke dalam berkas: 
== == "UAS-PRIBADI/0000-mypub.txt"
== == MOHON JANGAN MELETAKKAN "public key" tersebut di "UAS-BERSAMA/"!
== g. Mengimport "public key" yang tersedia di:
== == "UAS-BERSAMA/0003-OSPUB.txt" (67DF6DDE)
== == Recipient: Operating Systems (OS) <operatingsystems@vlsm.org>

## 3. Memiliki akses ke sistem linux (contoh badak):
== a. Memahami cara menggunakan CLI berbasis "bash".
== b. Memahami cara GSGS.
== c. Dapat membuat/memodifikasi script bash, awk, sed, dst.
== d. Dapat membuat/memodifikasi program berbasis C.
== e. Memahami konsep "C Standard Library" 
== == Contoh: printf() ---> #include <stdio.h>.
== f. Dapat membuat berkas "Makefile" sederhana.
== g. Dapat membuka/membuat arsip "tar" dengan kompresi "bzip2".
== h. Telah mencoba serta memahami SELURUH demo Week00-Week10.

## 4. SELALU setelah "commit", menambahkan baris "OS201 akunGitHub" ke log.

## 5. Jika ada yang kurang/tidak jelas, silakan SEGERA menanyakan di SCELE.
== a. Harap membuka post (thread) baru!
== b. Posting SCELE biasanya akan dibalas dalam kurun waktu 1-2 hari kerja.

## 6. Secara berkala memeriksa log di:
== https://github.com/UI-FASILKOM-OS/SistemOperasi/tree/master/Log/201/


# BAGIAN C: PERSIAPAN UAS
=======================
0. STOP mengisi ABSEN MINGGUAN di SCELE mau pun di GitHub! Fokus ke UAS!

1. Telah mengisi absen di "UAS-BERSAMA/0000-ABSEN.txt"

2. Telah meletakkan "public key" yang berlaku di "UAS-PRIBADI/0000-mypub.txt"

3. Jalankan perintah berikut pada akun bash anda (ganti "rms46" dengan "akunGitHub" anda):

```
$ export GitHubUser="rms46"
$ export PSTAMP="TMP1=\"\$(date +%y%m%d-%H%M%S)\"; TMP2=\"\$(echo \$TMP1-\$GitHubUser-\${PWD##*/}|sha1sum|cut -c1-4)\"; echo \"\$TMP1-\$TMP2-\${PWD##*/}/> \";"; echo $PSTAMP ;  eval $PSTAMP;
TMP1="$(date +%y%m%d-%H%M%S)"; TMP2="$(echo $TMP1-$GitHubUser-${PWD##*/}|sha1sum|cut -c1-4)"; echo "$TMP1-$TMP2-${PWD##*/}/> ";
200528-165038-801d-UAS/> 
$ script 0001-mytest.txt
```

4. Isi "0001-mytest.txt" KIRA-KIRA sebagai berikut:
```
Script started on Thu 28 May 2020 04:51:16 PM WIB
$ PS1="$ "
$ echo $GitHubUser
rms46
$ echo $PSTAMP
TMP1="$(date +%y%m%d-%H%M%S)"; TMP2="$(echo $TMP1-$GitHubUser-${PWD##*/}|sha1sum|cut -c1-4)"; echo "$TMP1-$TMP2-${PWD##*/}/> ";
$ eval $PSTAMP
200528-165332-3846-UAS/> 
$ PS1="\$(eval \$PSTAMP)"
200528-165353-de16-UAS/> date
Thu May 28 16:54:02 WIB 2020
200528-165402-cdb3-UAS/> gpg2 --list-keys
/home/demo/.gnupg/pubring.gpg
-----------------------------
pub   4096R/4762F757 2020-05-28 [expires: 2021-05-23]
uid       [ultimate] Cicak Bin Kadal (CBK) <cbkadal@vlsm.org>
sub   4096R/2825FDE2 2020-05-28 [expires: 2021-05-23]

pub   4096R/67DF6DDE 2020-02-13 [expires: 2021-02-12]
uid       [ultimate] Operating Systems (OS) <operatingsystems@vlsm.org>
sub   4096R/44170902 2020-02-13 [expires: 2021-02-12]

200528-165436-592f-UAS/> exit
exit

Script done on Thu 28 May 2020 04:54:59 PM WIB
```

5. Berkas "0002-mytest.txt.asc"
===============================
== a. menandatangani dan mengenkripsi (armor) berkas: "0001-mytest.txt".
== b. CONTOH, pengirim dan penanda-tangan: cbkadal@vlsm.org (JANGAN LUPA GANTI)
== c. penerima berkas (recipient): operatingsystems@vlsm.org
== d. Keluaran: "0002-mytest.txt.asc"
== e. List keys
==================
$ gpg2 --list-keys
/home/demo/.gnupg/pubring.gpg
-----------------------------
pub   4096R/4762F757 2020-05-28 [expires: 2021-05-23]
uid       [ultimate] Cicak Bin Kadal (CBK) <cbkadal@vlsm.org>
sub   4096R/2825FDE2 2020-05-28 [expires: 2021-05-23]

pub   4096R/67DF6DDE 2020-02-13 [expires: 2021-02-12]
uid       [ultimate] Operating Systems (OS) <operatingsystems@vlsm.org>
sub   4096R/44170902 2020-02-13 [expires: 2021-02-12]

== f. "-o" = outfile; "-e" = encrypt; "-a" = armor; "-r" = recipient "-s" = sign
================================================================================
$ gpg2 -o 0002-mytest.txt.asc -e -a -r operatingsystems@vlsm.org -r cbkadal@vlsm.org -s 0001-mytest.txt

== g. "-d" = decrypt
====================
$ gpg2 -o coba.txt -d 0002-mytest.txt.asc 
gpg: encrypted with 4096-bit RSA key, ID 44170902, created 2020-02-13
      "Operating Systems (OS) <operatingsystems@vlsm.org>"
gpg: encrypted with 4096-bit RSA key, ID 2825FDE2, created 2020-05-28
      "Cicak Bin Kadal (CBK) <cbkadal@vlsm.org>"
gpg: Signature made Fri 29 May 2020 08:31:52 PM WIB using RSA key ID 4762F757
gpg: Good signature from "Cicak Bin Kadal (CBK) <cbkadal@vlsm.org>" [ultimate]
$ 
== h. Silakan verifikasi isi berkas: "coba.txt"

6. PERHATIAN:
=============
== a. Sistem "badak" agak ketinggalan zaman.
== b. Pada kebanyakan sistem lain, "gpg2" telah berubah menjadi "gpg".
== c. Keluaran "gpg2 --list-keys" akan bervariasi dari sistem ke sistem.

7. Letakan berkas di:
=====================
== a. "UAS-PRIBADI/0001-mytest.txt"
== b. "UAS-PRIBADI/0002-mytest.txt.asc"
== c. "UAS-PRIBADI/.dummy" (HAPUS)


BAGIAN D: JADWAL/TAHAPAN/NILAI UAS
===================================
a. Tidak seperti biasa, nilai maksimum UAS ialah (30/30).
b. Untuk tidak mengubah template SIAK, nilai akan dibagi 5 (soal 6-10).
c. Secara berkala, silakan memeriksa log:
== https://github.com/UI-FASILKOM-OS/SistemOperasi/tree/master/Log/201/
d. Prasyarat mengikuti UAS ialah mencapai "PAS0".
== Batas waktu: 8 Juni 2020 jam 12:59.
== Jika "H"="0", maka nilai UAS=0.
== == tidak diperkenankan mengikuti UAS/akan diabaikan.
== == diberi kesempatan melengkapi PAS0.
== Jika belum mencapai PAS0, maka:
== == nilai UAS=6.
== == tidak diperkenankan mengikuti UAS/akan diabaikan.
== == diberi kesempatan melengkapi PAS0.
== Jika mencapai PAS0, maka;
== == nilai UAS=12.
== == diperbolehkan untuk mengikuti "UAS TAHAP I".
e. Bagi yang sudah "PAS0", silakan konfirmasi dengan berkas (kosong):
== "UAS-BERSAMA/akunGitHub/0000-PAS0.txt".
== "PAS0" tidak menjamin bahwa telah betul mengisi/membuat: P0, P1, dan P2.
== Jangan lupa menghapus ".dummy", ya!
f. UAS TAHAP I KELAS A, B, C, M
== Pengumuman Tugas:  8 Juni 2020 secepatnya setelah jam 13:00.
== Tugas akan diumumkan melalui WhatsApp Group "os201".
== Batas waktu: 9 Juni 2020 jam 13:01.
== Jika melewati batas waktu:
== == Nilai UAS=12.
== == Diberi kesempatan menyelesaikan/merampungkan tugas UAS TAHAP I.
== == Tidak diberi kesempatan melanjutkan ke tugas UAS TAHAP II.
== Jika lulus:
== == Nilai UAS=17.5.
== == Rincian nilai dan tugas akan diumumkan.
== == Diberi kesempatan melanjutkan ke tugas UAS TAHAP II.
g. UAS TAHAPAN SELANJUTNYA.
== Akan diumumkan diberkas lain (tunggu pengumuman lanjut).
h. NILAI SIAK
== Batas waktu: 7 Agustus 2020 jam 15:59.

BAGIAN E: Masukan Umpan Balik (Feedback)
========================================
Mengingat ini baru pertama kali, silakan memberikan masukan (feedback).
Untuk itu, gunakan berkas "UAS-BERSAMA/akunGitHub/0000-PAS0.txt" di atas.
Hal-hal yang ingin diketahui (namun tidak terbatas pada):
1) Berapa lama dibutuhkan untuk memahami dokumen ini?
2) Apakah anda GSGS?
3) Apakah anda tanya-sana/tanya-sini?
4) Sebutkan apakah ada hal yang "betul betul baru"/"belum pernah" dilakukan 
   sebelumnya.
5) Dst.


Jolan Tru!
RMS

APPENDIX (git diff HEAD)
========================
 
-*** Berkas ini sudah relatif stabil hingga titik PAS0  ***
 
+URL: https://scele.cs.ui.ac.id/mod/forum/discuss.php?d=19137
+LOG: https://github.com/UI-FASILKOM-OS/SistemOperasi/tree/master/Log/201
 
 1. "akunGitHub" -- Nama akun yang digunakan untuk mengakses GitHub.com.
+== PERHATIAN: Dalam bash akan digunakan variable "GitHubUser".
 
-== g. membuat berkas baru "UAS-PRIBADI/.dummy" dan "UAS-BERSAMA/.dummy".
+== g. membuat berkas baru "UAS-PRIBADI/.dummy" dan "UAS-BERSAMA/akunGitHub/.dummy".

-== Pengumuman Tugas:  8 Juni 2020 (sekitar) jam 13:00.
+== Pengumuman Tugas:  8 Juni 2020 secepatnya setelah jam 13:00.
+== Tugas akan diumumkan melalui WhatsApp Group "os201".

+== == Rincian nilai dan tugas akan diumumkan.

 g. UAS TAHAPAN SELANJUTNYA.
-== TBA.
+== Akan diumumkan diberkas lain (tunggu pengumuman lanjut).
