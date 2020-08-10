---
---

[HOME](index.md)
[ABOUT](README.md)
[TOP](#)
[SCRIPTING](#scripting)

# Scripting

1. Scripting Sederhana
1.1. Perintah dasar linux dan fungsinya
  a. ls  = melihat isi direktori
  b. mkdir =  menciptakan direktori
  c. cd  = mengubah direktori
  d. rmdir = menghapus direktori
  e. cat = Menampilkan isi file dan menciptakan file
  f. cp = Menyalin file
  g. rm = menghapus file
  h. mv = mengganti nama file/direktori dan memindahkan file ke direktori lain
  i. ln = link ke file lain
  j. lp = Mencetak isi file
  k. find = mencari file
  l. chmod = untuk mengubah model akses terhadap file atau direktori
  m. chgrp = mengubah grup fie
  n. chown = mengubah kepemilikan dari file
  o. echo = Menampilkan tulisan yang dibuat setelah perintah echo dan itu tidak disimpan
  p. sort = Mengurutkan suatu file teks menurut abjad
  q. cut = Mengambil kolom tertentu dari baris-baris masukannya yang ditentukan pada option–c
  r.  uniq = Menghilangkan baris – baris berurutan yang mengalami duplikasi
  s. locate = Mencari suatu file pada direktori lain yang sedang tidak dikunjungi
  t. finger = Melihat informasi user yang telah ditambahkan oleh perintah chfn

1.2 Contoh Bash Script
Ini merupakan contoh penggunaan bash pada mode non-interaktif, yaitu dengan membuat dan menjalankan dua bash script sederhana.

Contoh 1:
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
Penjelasan untuk script hello:
#!/bin/bash menyatakan bahwa script tersebut harus dijalankan di bash shell. /bin/bash merupakan lokasi dari bash interpreter yang akan menerjemahkan dan menjalankan bash script. Anda dapat mendapatkan lokasi ini dengan menjalankan perintah:
```
$ which bash
/bin/bash
```

$PWD merupakan sebuah variabel yang sudah didefinisikan oleh bash. Dengan meletakkan variabel dalam tanda petik dua (“), bash akan mengganti pernyataan variabel tersebut dengan nilainya, kemudian barulah perintah (dalam kasus ini perintah echo) dijalankan. Nilai variabel $PWD adalah path direktori aktif, layaknya output dari perintah pwd.

Contoh 2:
!/bin/bash
Menampilkan beberapa informasi
 
Menampilkan nama user
echo "Halo $USER!"
 
Menampilkan nama file shell script yang sedang dijalankan
echo "Anda sedang menjalankan file bash script '$0'"
 
Menampilkan tanggal lokal
echo -n "Hari ini tanggal "; date +"%d %B %Y"
 
Menampilkan nama direktori aktif
echo -n "Anda sedang berada di lokasi "; pwd
 
Menampilkan isi direktori aktif
echo "Berikut merupakan beberapa file yang terdapat pada direktori aktif:";
ls

Simpan file tersebut dengan nama tampilkaninfo, kemudian rubah hak akses file agar dapat dieksekusi, dan jalankan.
$ chmod 755 tampilkaninfo
$ ./tampilkaninfo
Halo user!
Anda sedang menjalankan file bash script './tampilkaninfo'
Hari ini tanggal 04 Agustus 2020
Anda sedang berada di lokasi /home/user/Documents/Writing/Code/bash

Berikut merupakan beberapa file yang terdapat pada direktori aktif:
hello tampilkaninfo


