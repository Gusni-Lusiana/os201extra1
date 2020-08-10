---
---

[HOME](index.md)
[ABOUT](README.md)
[TOP](#)
[SCRIPTING](#scripting)

# Scripting

## 1. Scripting Sederhana<br>
**1.1. Perintah dasar linux dan fungsinya<br>**
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

## 1.2 Contoh Bash Script
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
```hello tampilkaninfo```

Penjelasan untuk script tampilkaninfo:
<br>
Variabel $USER menyimpan nama user. $USER merupakan salah satu variabel lingkungan (environment variable) yang telah didefinisikan nilainya oleh sistem, dan perubahan terhadap nilai variabel lingkungan mempengaruhi kerja sistem. Telah dijelaskan sebelumnya, jika variabel $0 digunakan di shell script, maka akan memiliki nilai nama file script tersebut.<br><br>
Dengan menggunakan argumen -n pada echo, teks tidak diakhiri dengan newline (ganti baris). Sehingga tulisan Hari ini tanggal dan hasil pemanggilan perintah date +"%d %B %Y" (untuk menampilkan tanggal lokal saat script dijalankan dengan format tanggal “tanggal nama bulan tahun”) dapat ditampilkan dalam baris yang sama. Tulisan Anda sedang berada di lokasi dengan hasil pemanggilan perintah pwd juga dapat ditampilkan pada baris yang sama dengan meniadakan newline pada akhir output pemanggilan echo.
