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


# Petunjuk UAS 3

1. Pelajari keluaran/script berkas "K01-TEST-RESULT.txt". <br>
2. Setiap anggota memilih berkas mulai dari "p00.c", "p01.c", dst.<br>
3. Berkas "share.c" dan "share.h" dibagi (share) bersama.<br>
4. Agar tidak mulai dari NOL, telah disediakan rangka program/ fungsi ala kadarnya.<br>
5. Tugas kelompok ialah melengkapi/ memodifikasi berkas "share.c" dan "share.h" bersama-sama.<br>
6. Harap mencantumkan (akunGitHub), pihak yang melakukan pelengkapan/ memodifikasi.<br>
7. Jika diinginkan, silakan mengubah TOTAL isi program/ fungsi yang telah disiapkan.<br>
6. Yang harus tetap:<br>
a. isi "struct usrinfo" dan "struct myshare" dalam "share.h" tidak boleh diubah.<br>
b. nama berkas untuk "SharedMemory" harus "SharedMemoryFile.bin".<br>
c. nama berkas masing-masing anggota harus p00.c, p01.c, dst.<br>
d. kerjakan dalam folder "TUGAS/", lalu buat berkas "tar" bernama "0003-TUGAS.tar.bz2" (sebelum dienkripsi).<br>
e. berkas "0003-TUGAS.tar.bz2" HARUS dienkripsi dengan key dari "operatingsystems@vlsm.org".<br>
7. Yang perlu diubah ialah nilai "delay":<br>
a. Nilai default "delay" berturut-turut: (p00.c: 3), (p01.c: 2), (p02.c: 1), (p03.c: 5), (p04.c: 4).<br>
b. Berapa pun nilai delay, program tidak boleh "hang".<br>
c. Bagaimana pun urutan delay, "p00" harus selalu exit paling akhir.<br>
8. Ganti isi variabel "akunGitHub" dengan nama akun GitHub masing-masing anggota kelompok.<br>
9. Akses "SharedMemory" secara MUTEX.  Gunakan semafor "mutex".<br>
a. Setiap kali mengakses "mutex", "mutexctr++".<br>
b. Setiap kali mengakses "mutex", untuk "usrinfo" dari akunGitHub tersebut, "stamp++"<br>
c. Pengecualian, "state" (OPEN/CLOSED/0) diakses tanpa memeriksa semafor "mutex".<br>
d. Pengecualian, inisialisasi semafor "mutex" TENTUNYA tanpa memeriksa semafor "mutex".<br>
e. Inisialisasi semafor (SharedMemory) dengan fungsi "sem_init (&(mymap->mutex), 1, MUTEX)".<br>
10. Proses "p00":<br>
a. Saat inisialisasi, "state=0";<br>
b. Hanya "p00" yang dapat menset "state" menjadi "OPEN" atau "CLOSED".<br>
c. Tanpa argumen, proses "p00" yang memanggil "p01", "p02", dst. <br>
d. Tanpa argumen, proses "p00" selalu exit paling akhir dengan "state=CLOSED".<br>
e. Dengan sembarang argumen, proses "p00" membuat "state=OPEN", lalu langsung EXIT.<br>
11. Proses "p01", "p01", "p02", ...<br>
a. Tanpa berkas SharedMemory, "p01", "p02", dst. langsung exit.<br>
b. Jika "state==CLOSED", "p01", "p02", dst. langsung exit.<br>
c. Jika "state==OPEN",   "p01", "p02", dst. dapat mengakses SharedMemory.<br>
12. Berkas "K00-TEST-KIT.txt"<br>
a. Setiap anggota melakukan test terpisah.<br>
b. Gunakan berkas "K00-TEST-KIT.txt" sebagai patokan testing.<br>
13. Berkas "K01-TEST-RESULT.txt"<br>
a. Masukkan hasil test ke berkas "K01-TEST-RESULT.txt"<br>
14. Info Tambahan
```
#define AKUNSIZE     30    // Jumlah karakter dalam string "akunGitHub" (minus 1).
#define CLOSED       127   // "state==CLOSED"; "SharedMemory" TIDAK boleh diakses.
#define MAXPROGS     20    // Maximum program. Jika diperlukan, silakan ubah.
#define OPEN         255   // "state==OPEN";   "SharedMemory" boleh diakses.
#define SHAREMEM     "SharedMemoryFile.bin" // nama berkas "SharedMemory"
typedef struct {
    char  akun [AKUNSIZE]; // penempatan string "akunGitHub".
    int   stamp;           // posisi "mutex"
} usrinfo;
typedef struct {
    usrinfo progs[MAXPROGS+1];
    int     entry;        // usrinfo yang kosong.
    int     state;        // lihat OPEN/CLOSED.     
    int     mutexctr;     // jumlah penggunaan semafor mutex.
    sem_t   mutex;        // semafor mutex agar hanya satu yang akses ShareMemory pada satu saat.
} myshare;
=====================
void checkOpen(void);
Langsung exit, jika "state=CLOSED".
========================
void display(int entry);  // tampilkan
// akunGH0[progs[01] TIME[16] MUTEX[04] MMAP[OPEN] [akunGH3][akunGH0][akunGH2][akunGH1]]
// akunGitHub entry  "mutexctr""stamp"   "OPEN/CLOSE" "entry akunGitHub dalam memory"
========================
int  getEntry(char* akunGitHub);
jika sudah ada dalam SharedMemory, kembalikan nomor posisi.
jika belum ada dalam SharedMemory, kembalikan nomor ++entry.
==============================================
void init(int isboss, int argc, char* argv[]);
// init sistem;
=====================================
void myprint(char* str1, char* str2);
// cetak str1 dan str2.
=================================
void myWait(int boss, int entry);
jika BOSS: 1) "state=CLOSED" dan 2) tunggu hingga semua proses lain exit.
====================================
void putInfo(char* akun, int entry);
// masukkan string "akunGitHub" ke dalam ShareMemory.
```
15. Jangan lupa bersih-bersih.<br>
== a. Harap "make clean" sebelum mengumpulkan berkas.

# Pengerjaan UAS 3

* Modifikasi file p00.c, p01.c dan p02.c ganti akun GitHub dan urutan Delay sesuai dengan petunjuk UAS 3. p00.c delay = 3, p01.c delay = 2, p02.c delay = 1
* Modifikasi file share.c
```
#include     "share.h"
char*        progs[]={P01, P02};
char         tmpStr[256]={};
extern char* akunGitHub;
extern int   delay;
extern int   boss;
myshare*     mymap;

		void init(int isboss, int argc, char* argv[]) {
    if (isboss == BOSS) {
        int ssize=sizeof(myshare);
        int fd   =open(SHAREMEM, MYFLAGS, CHMOD);
        fchmod   (fd, CHMOD);
        ftruncate(fd, ssize);
        mymap=mmap(NULL, ssize, MYPROTECTION, MYVISIBILITY, fd, 0);
        close(fd);
        mymap->state = OPEN;
        sem_init (&(mymap->mutex),  1, MUTEX);
        if(mymap->mutexctr == 0){
        for(int a=0; a<MAXPROGS; a++){
          mymap->progs[a].stamp = 0;
          strcpy(mymap->progs[a].akun, "");
        }}
        if (argc > 1){
          mymap->state = OPEN;
          printf("ShareMemory is OPEN, BYE BYE ==== ====\n");
          exit(1);
        }
        for(int a=0; a<2; a++){
        if (fork() == 0) {
           execl(progs[a], progs[a], NULL);
	break;
        } else {
	sleep(delay);
        }
                }
    } else {
        sleep(delay);
        if( access(SHAREMEM, F_OK ) == -1 ) {
            printf("No \"%s\" file.\n", SHAREMEM);
            exit(-1);
        }
        int fd=open(SHAREMEM, O_RDWR, CHMOD);
        int ssize=sizeof(myshare);
        mymap=mmap(NULL, ssize, MYPROTECTION, MYVISIBILITY, fd, 0);
        close(fd);
    }
}

void myPrint(char* str1, char* str2) {
    printf("%s[%s]\n", str1, str2);
    fflush(NULL);
}

int getEntry(char* akunGitHub) {
    int entry=0;
    sem_wait (&(mymap->mutex));
		char temp[30];
    strcpy(temp, akunGitHub);
    for(int i=0;i<MAXPROGS;i++){
char temp2[30];
    strcpy(temp2, mymap->progs[i].akun);

      if(strcmp(temp2,temp)== 0) {
        mymap->mutexctr++;
        mymap->progs[entry].stamp++;
        sem_post (&(mymap->mutex));
        return i;
      }
    }
    entry = mymap->entry;
    mymap->entry++;
    mymap->mutexctr++;
    mymap->progs[entry].stamp++;
    sem_post (&(mymap->mutex));
    return entry;
}
void myprint2(char* str1, char* str2) {
    printf("%s[", str1);
}

void display(int entry) {
    sem_wait (&(mymap->mutex));
    mymap->mutexctr++;
    mymap->progs[entry].stamp++;
    myprint2(akunGitHub, akunGitHub);
   	printf("progs[%02d] TIME[%02d] MUTEX[%02d] MMAP[%s] ", entry, mymap->mutexctr, mymap->progs[entry].stamp, "OPEN");

    for(int a=0; a<mymap->entry; a++){
      printf("[%s]", mymap->progs[a].akun);
    }
        printf("]\n");

    sem_post (&(mymap->mutex));

void putInfo(char* akun, int entry) {
    sem_wait (&(mymap->mutex));
    strcpy(mymap->progs[entry].akun, akun);
    mymap->progs[entry].stamp++;
    mymap->mutexctr++;
    sem_post (&(mymap->mutex));
}

void checkOpen(void) {
    if(mymap->state!=OPEN){
        printf("ShareMemory is NOT OPEN, BYE BYE ==== ==== \n");
        exit(0);
    }
}

void myWait(int boss, int entry) {
    if(boss == BOSS){
      mymap->state = CLOSED;
      while(wait(NULL) > 0);
    }
}

int main(int argc, char* argv[]) {
    sprintf(tmpStr, "START PID[%d] PPID[%d]", getpid(), getppid());
    myPrint(akunGitHub, tmpStr);
    init(boss, argc, argv);
    checkOpen();
    sleep  (delay);
    int entry = getEntry(akunGitHub);
    sleep  (delay);
    display(entry);
    sleep  (delay);
    putInfo(akunGitHub, entry);
    sleep  (delay);
    display(entry);
    myWait (boss, entry);
    myPrint(akunGitHub, "BYEBYE =====  ===== =====");
}
```

# Hasil Test UAS 3

## Persiapan Test
* Persiapan 
```
$ export akunGitHub="abdulazis02"
$ export PSTAMP="TMP1=\"\$(date +%y%m%d-%H%M%S)\"; TMP2=\"\$(sleep 1;
```
* Mulai Scripting
```
$ script K-01-TEST-RESULT.txt
```
# TEST-KIT
```
PS1="$ "
date
echo $HOSTNAME
echo $akunGitHub
echo $PSTAMP
PS1="\$(eval \$PSTAMP)"
make clean
./p00
make
./p01
./p00
./p01
./p00 x
./p01
./p00
./p01
```

# HASIL TEST
```
Script started on 2020-08-05 14:31:42+07:00 
azispro@ubuntu: ~/TUGAS
$ PS1="$ "
$ date
Rab 05 Agu 2020 02:31:52  WIB
$ echo $HOSTNAME
ubuntu
$ echo $akunGitHub
abdulazis02
$ echo $PSTAMP
TMP1="$(date +%y%m%d-%H%M%S)"; TMP2="$(sleep 1;echo $TMP1-$akunGitHub-${PWD##*/}|sha1sum|cut -c1-4)"; 
echo "$TMP1-$TMP2-${PWD##*/}/> ";
$ PS1="\$(eval \$PSTAMP)"
200805-143216-60b5-TUGAS/> n[Kmake clean
rm -f p00 p01 p02 SharedMemoryFile.bin
200805-143221-1774-TUGAS/> ./p00
bash: ./p00: No such file or directory
200805-143227-95cd-TUGAS/> make
gcc -std=gnu11 -pthread    p00.c share.c share.h   -o p00
gcc -std=gnu11 -pthread    p01.c share.c share.h   -o p01
gcc -std=gnu11 -pthread    p02.c share.c share.h   -o p02
200805-143231-39f6-TUGAS/> ./p01
imamsetyo96[START PID[4549] PPID[4483]]
No "SharedMemoryFile.bin" file.
200805-143237-3137-TUGAS/> ./p00
abdulazis02[START PID[4557] PPID[4483]]
imamsetyo96[START PID[4558] PPID[4557]]
Gusni-Lusiana[START PID[4559] PPID[4557]]
imamsetyo96[progs[00] TIME[03] MUTEX[02] MMAP[OPEN] [][]]
Gusni-Lusiana[progs[01] TIME[04] MUTEX[02] MMAP[OPEN] [][]]
Gusni-Lusiana[progs[01] TIME[07] MUTEX[04] MMAP[OPEN] [imamsetyo96][Gusni-Lusiana]]
Gusni-Lusiana[BYEBYE =====  ===== =====]
imamsetyo96[progs[00] TIME[09] MUTEX[04] MMAP[OPEN] [imamsetyo96][Gusni-Lusiana][]]
imamsetyo96[BYEBYE =====  ===== =====]
abdulazis02[progs[02] TIME[10] MUTEX[02] MMAP[OPEN] [imamsetyo96][Gusni-Lusiana][]]
abdulazis02[progs[02] TIME[12] MUTEX[04] MMAP[OPEN] [imamsetyo96][Gusni-Lusiana][abdulazis02]]
abdulazis02[BYEBYE =====  ===== =====]
200805-143300-70a2-TUGAS/> ./p01
imamsetyo96[START PID[4568] PPID[4483]]
ShareMemory is NOT OPEN, BYE BYE ==== ==== 
200805-143308-8e43-TUGAS/> ./p00 x
abdulazis02[START PID[4576] PPID[4483]]
ShareMemory is OPEN, BYE BYE ==== ====
200805-143313-6934-TUGAS/> ./p01
imamsetyo96[START PID[4585] PPID[4483]]
imamsetyo96[progs[00] TIME[14] MUTEX[06] MMAP[OPEN] [imamsetyo96][Gusni-Lusiana][abdulazis02]]
imamsetyo96[progs[00] TIME[16] MUTEX[08] MMAP[OPEN] [imamsetyo96][Gusni-Lusiana][abdulazis02]]
imamsetyo96[BYEBYE =====  ===== =====]
200805-143327-17fb-TUGAS/> ./p00
abdulazis02[START PID[4594] PPID[4483]]
imamsetyo96[START PID[4595] PPID[4594]]
Gusni-Lusiana[START PID[4597] PPID[4594]]
imamsetyo96[progs[00] TIME[19] MUTEX[11] MMAP[OPEN] [imamsetyo96][Gusni-Lusiana][abdulazis02]]
Gusni-Lusiana[progs[01] TIME[20] MUTEX[05] MMAP[OPEN] [imamsetyo96][Gusni-Lusiana][abdulazis02]]
Gusni-Lusiana[progs[01] TIME[23] MUTEX[07] MMAP[OPEN] [imamsetyo96][Gusni-Lusiana][abdulazis02]]
Gusni-Lusiana[BYEBYE =====  ===== =====]
imamsetyo96[progs[00] TIME[25] MUTEX[14] MMAP[OPEN] [imamsetyo96][Gusni-Lusiana][abdulazis02]]
imamsetyo96[BYEBYE =====  ===== =====]
abdulazis02[progs[02] TIME[26] MUTEX[05] MMAP[OPEN] [imamsetyo96][Gusni-Lusiana][abdulazis02]]
abdulazis02[progs[02] TIME[28] MUTEX[07] MMAP[OPEN] [imamsetyo96][Gusni-Lusiana][abdulazis02]]
abdulazis02[BYEBYE =====  ===== =====]
200805-143349-4ada-TUGAS/> ./p01
imamsetyo96[START PID[4605] PPID[4483]]
ShareMemory is NOT OPEN, BYE BYE ==== ==== 
200805-143358-cb27-TUGAS/> exit
exit
Script done on 2020-08-05 14:34:01+07:00
```
