---
[HOME  |  ](index.md)
[README  |  ](README.md)
[Scripting  |  ](#scripting)
[Editor-Linux  |  ](#editorlinux)
[Gcc  |  ](#gcc)
[MakeFile  |  ](#makefile)
[TAR  |  ](#tar)
[Git  |  ](#git)
[GitHub  |  ](#github)
[SHA1  |  ](#sha1)
[GnuPG  |  ](#gnupg)
[UAS-3  |  ](uas3.md)
[UAS-4  |  ](uas4.md)
[UAS-5](uas5.md)

# Petunjuk UAS 4

1. Pelajari keluaran/script berkas "K04-TEST-RESULT.txt".
2. Setiap anggota memilih berkas mulai dari "p00.c", "p01.c", dst.
3. Berkas "share.c" dan "share.h" dibagi (share) bersama.
4. Agar tidak mulai dari NOL, telah disediakan rangka program/ fungsi ala kadarnya.
5. Tugas kelompok ialah melengkapi/ memodifikasi berkas "share.c" dan "share.h" bersama-sama.
6. Harap mencantumkan (akunGitHub), pihak yang melakukan pelengkapan/ memodifikasi.
7. Jika diinginkan, silakan mengubah TOTAL isi program/ fungsi yang telah disiapkan.
6. Yang harus tetap:
== a. isi "struct usrinfo" dan "struct myshare" dalam "share.h" tidak boleh diubah.
== b. nama berkas untuk "SharedMemory" harus "SharedMemoryFile.bin".
== c. nama berkas masing-masing anggota harus p00.c, p01.c, dst.
7. Yang perlu diubah ialah nilai "delay":
== a. Nilai default "delay" berturut-turut: (p00.c: 3), (p01.c: 1), (p02.c: 1), (p03.c: 2), (p04.c: 1), (p05.c: 8).
== b. Berapa pun nilai delay, program tidak boleh "hang".
== c. Bagaimana pun urutan delay, "p00" harus selalu exit paling akhir.
8. Ganti isi variabel "akunGitHub" dengan nama akun GitHub masing-masing.
9. Akses "SharedMemory" secara MUTEX.  Gunakan semafor "mutex".
== a. Setiap kali mengakses "mutex", "mutexctr++".
== b. Pengecualian, state (OPEN/CLOSED/0) diakses tanpa memeriksa semafor "mutex".
== c. Pengecualian, inisialisasi semafor "mutex" tanpa memeriksa semafor "mutex".
== d. Inisialisasi semafor (SharedMemory) dengan fungsi "sem_init (&(mymap->mutex), 1, MUTEX)".
10. Proses "p00":
== a. Saat inisialisasi, state=0;
== b. Hanya "p00" yang dapat menset state menjadi "OPEN" atau "CLOSED".
== c. Tanpa argumen, proses "p00" akan memanggil "p01", "p02", dst. 
== d. Tanpa argumen, proses "p00" selalu exit paling akhir, serta merubah state=CLOSED.
== e. Dengan sembarang argumen, proses "p00" membuat state=OPEN, lalu langsung exit.
== f. Kecuali state=OPEN, "p00" akan reset ShareMemory.
11. Proses "p01", "p01", "p02", ...
== a. Tanpa berkas  SharedMemory, p01, p02, dst. langsung exit.
== b. Jika state=CLOSED, p01, p02, dst. langsung exit.
== c. Jika state=OPEN, p01, p02, dst. dapat mengakses SharedMemory.
12. Berkas "K00-TEST-KIT.txt"
== a. Setiap anggota melakukan test terpisah
== b. Gunakan berkas "K00-TEST-KIT.txt" sebagai patokan testing.
13. Berkas "K04-TEST-RESULT.txt"
== a. akunGH0[Boss is Waiting] dalam "initBoss()", p00 akan menunggu hingga semua "NoBosses" dalam keadaan siap.
== b. akunGH0[All NoBosses are ready!] p00 selesai menunggu.
== c. akunGH1[Good Bye initNoBoss()!] p01, p02, ... selesai menjalankan "initNoBoss()".
== d. akunGH1[Yes, I am ready!] Siapa pun (p00, p01, p02, ...) harus menunggu isyarat dari p00.
===== Isyarat p00 baru diberikan setelah  "All NoBosses are ready!" (butir 13.b di atas).
== e. Masukkan hasil test ke berkas "K04-TEST-RESULT.txt"
== f. Jika DEADLINE masih jauh, silakan mengembangkan "doBoss()" dan "doNotBoss()".
===== Tentunya, sesuai dengan kreatifitas masing-masing.
14. Info Tambahan
```
#define AKUNSIZE     30    // Jumlah karakter dalam string "akinGitHub" (minus 1).
#define BOSS         0     // Boss (p00)
#define NOTBOSS      1     // NOTBOSS (p01, p02, ...)
#define CHMOD        0666  // Mode -rw-rw-rw (read-write)
#define CLOSED       127   // state==CLOSED; "SharedMemory" TIDAK boleh diakses.
#define MAXPROGS     20    // Maximum program. Jika diperlukan, silakan diubah.
#define OPEN         255   // state==OPEN;   "SharedMemory" boleh diakses.
#define SHAREMEM     "SharedMemoryFile.bin" // nama berkas "SharedMemory"
#define SSYNC         0    // sem_init (&(mymap->sync),  SSHARE, SSYNC);
#define SMUTEX        1    // sem_init (&(mymap->mutex), SSHARE, SMUTEX);
#define SSHARE        1    // 
#define tmpSize      1024  // alokasi cetak
typedef struct {
    char  akun [AKUNSIZE]; // penempatan string "akunGitHub".
    int   value;           // sebuah nilai
    sem_t sync;            // semafor untuk sinkronisasi
} usrinfo;
typedef struct {
    usrinfo progs[MAXPROGS+1]; 
    int     entry;        // usrinfo yang kosong.
    int     state;        // lihat OPEN/CLOSED.     
    int     mutexctr;     // jumlah penggunaan semafor mutex.
    sem_t   mutex;        // semafor mutex agar hanya satu yang akses ShareMemory pada satu saat.
    sem_t    sync;        // semafor untuk sinkronisasi
} myshare;
=====================
void checkOpen(void);
Langsing exit, jika state=CLOSED.
========================
void display(int entry);  // menampilkan
// akunGH5[progs[05] TIME[035] MMAP[OPEN] VALUE[400] [akunGH1][akunGH4][akunGH2][akunGH3][akunGH0][akunGH5]]
// akunGitHub entry "mutexctr""OPEN/CLOSE""value"    "entry akunGitHub dalam memory"
=======================
void doBoss(int entry);
// Hal spesifik bagi Boss (p00).
// Untuk pengembangan lanjut.
=======================
void doNotBoss(int entry);
// Hal spesifik bagi yang bukan Boss (p01, p02, ...)
// Untuk pengembangan lanjut.
========================
int  getEntry(char* akunGitHub);
jika sudah ada dalam SharedMemory, kembalikan nomor posisi.
jika belum ada dalam SharedMemory, kembalikan nomor ++entry.
==============================================
void init(int isboss, int argc, char* argv[]);
// init sistem;
==============================================
void initBoss(int argc, char* argv[]);
// init sistem spesifik Boss (p00).
==============================================
void initNotBoss(void);
// init sistem yang bukan Boss (p01, p02, ...).

=====================================
void myprint(char* str1, char* str2);
// cetak str1 dan str2.
=================================
void myWait(int boss, int entry);
jika BOSS: 1) state=CLOSED dan 2) tunggu hingga semua proses lain exit.
====================================
void putInfo(char* akun, int entry);
// masukkan string "akunGitHub" ke dalam ShareMemory.
```
15. Jangan lupa bersih-bersih.
== a. Harap "make clean" sebelum mengumpulkan berkas.

# Pengerjaan UAS 4

* Modifikasi file p00.c, p01.c dan p02.c ganti akun GitHub dan urutan Delay sesuai dengan petunjuk UAS 4. p00.c delay = 3, p01.c delay = 1, p02.c delay = 1
* Modifikasi file share.c
```
#include     "share.h"
char*        progs[]={P01, P02};
char         tmpStr[tmpSize]={};
extern char* akunGitHub;
extern int   delay;
extern int   boss;
extern int   initValue;
myshare*     mymap;

void initBoss(int argc, char* argv[]) {
        myPrint(akunGitHub, "Boss is Waiting");
        int ssize=sizeof(myshare);
        int fd   =open(SHAREMEM, MYFLAGS, CHMOD);
        fchmod   (fd, CHMOD);
        ftruncate(fd, ssize);
        mymap=mmap(NULL, ssize, MYPROTECTION, MYVISIBILITY, fd, 0);
        close(fd);
        mymap->state = OPEN;
  
        sem_init (&(mymap->mutex),  1, SMUTEX);
        sem_init (&(mymap->sync),  SSHARE, SSYNC);

        if(mymap->mutexctr == 0){
        for(int a=0; a<MAXPROGS; a++){
          mymap->progs[a].value = 0;
          strcpy(mymap->progs[a].akun, "");
                  }}
        sem_init (&(mymap->progs[0].sync),  SSHARE, SSYNC);
  		
        if (argc > 1){
          mymap->state = OPEN;
          printf("ShareMemory is OPEN, BYE BYE ==== ====\n");
          exit(1);
        }

        for(int a=0; a<2; a++){
          if (fork() == 0) {
            execlp(progs[a], progs[a], NULL);
            break;
          } else {
            sleep(delay);
          }
        }
  
        for (int ii=0; ii < 2; ii++){
            // printf("1. ke- %d \n", ii);
            sem_post(&(mymap->sync));
            sleep(delay);
        }
        
        myPrint(akunGitHub, "All NoBosses are ready!");
        for (int ii=0; ii < 2; ii++){
         
            sem_post(&(mymap->progs[0].sync));
            sleep(delay);
        }
}

void initNotBoss(void) {
    sleep(delay);
    if( access(SHAREMEM, F_OK ) == -1 ) {
            printf("No \"%s\" file.\n", SHAREMEM);
            exit(-1);    
    }
    int fd=open(SHAREMEM, O_RDWR, CHMOD);
    int ssize=sizeof(myshare);
    mymap=mmap(NULL, ssize, MYPROTECTION, MYVISIBILITY, fd, 0);
    close(fd);
  	
    if(mymap->state!=OPEN){
        myPrint(akunGitHub, "Good Bye initNoBoss()!");
    }
    else{
    sem_wait(&(mymap->sync));
    myPrint(akunGitHub, "Good Bye initNoBoss()!");
    sleep(delay);
    sem_wait(&(mymap->progs[0].sync));
    sleep(delay);
    }
}

void init(int isboss, int argc, char* argv[]) {
    if (isboss == BOSS){
      initBoss(argc, argv);
    }else{
      initNotBoss();
    }
}

void myPrint(char* str1, char* str2) {
    printf("%s[%s]\n", str1, str2);
    fflush(NULL);
}

void myprint2(char* str1, char* str2) {
    printf("%s[", str1);
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
        sem_post (&(mymap->mutex));
        return i;
      }
    }
    entry = mymap->entry;
    mymap->entry++;
    mymap->mutexctr++;
    sem_post (&(mymap->mutex));
    return entry;
}

void display(int entry) {
    sem_wait (&(mymap->mutex));
    mymap->mutexctr++;
    myprint2(akunGitHub, akunGitHub);
    printf("progs[%02d] TIME[%03d] MMAP[%s] VALUE[%03d] ", entry, mymap->mutexctr,"OPEN", mymap->progs[entry].value);

    for(int a=0; a<mymap->entry; a++){
      printf("[%s]", mymap->progs[a].akun);
    }
      printf("]\n");

    sem_post (&(mymap->mutex));
}


void putInfo(char* akun, int entry) {
    sem_wait (&(mymap->mutex));
    strcpy(mymap->progs[entry].akun, akun);
        setValue(entry, initValue);
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
    sleep(delay);
                if(boss == BOSS){
      mymap->state = CLOSED;
      while(wait(NULL) > 0);

    }
}

void setValue(int entry, int initValue) {
    mymap->progs[entry].value = initValue;
}

void doBoss(int entry) {
  }

void doNotBoss(int entry) {
}


int main(int argc, char* argv[]) {
    sprintf(tmpStr, "START PID[%5.5d] PPID[%5.5d]", getpid(), getppid());
    myPrint(akunGitHub, tmpStr);
    init(boss, argc, argv);
    checkOpen();

     myPrint(akunGitHub, "Yes, I am ready!");
    
    sleep  (delay);
    int entry = getEntry(akunGitHub);
    sleep  (delay);
    display(entry);
       sleep  (delay);
    putInfo(akunGitHub, entry);
       sleep  (delay);
    display(entry);
       sleep  (delay);
    myWait (boss, entry);
    myPrint(akunGitHub, "BYEBYE === ===== ===== =====");
}
```

# Hasil Test UAS 4
* Persiapan 
```
$ export akunGitHub="abdulazis02"
$ export PSTAMP="TMP1=\"\$(date +%y%m%d-%H%M%S)\"; TMP2=\"\$(sleep 1;
Mulai Scripting
$ script K-04-TEST-RESULT.txt
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
./p00
./p01
```

# HASIL TEST
```
Script started on 2020-08-05 14:40:42+07:00
azispro@ubuntu: ~/TUGAS4 
$ PS1="$ "
$ date
Rab 05 Agu 2020 02:40:52  WIB
$ echo $HOSTNAME
ubuntu
$ echo $akunGitHub
abdulazis02
$ echo $PSTAMP
TMP1="$(date +%y%m%d-%H%M%S)"; TMP2="$(sleep 1;echo $TMP1-$akunGitHub-${PWD##*/}|sha1sum|cut -c1-4)"; 
echo "$TMP1-$TMP2-${PWD##*/}/> ";
$ PS1="\$(eval \$PSTAMP)"
200805-144114-be5e-TUGAS4/> make clean
rm -f p00 p01 p02 SharedMemoryFile.bin
200805-144118-d886-TUGAS4/> ./p00
bash: ./p00: No such file or directory
200805-144122-3c38-TUGAS4/> make
gcc -std=gnu11 -pthread    p00.c share.c share.h   -o p00
gcc -std=gnu11 -pthread    p01.c share.c share.h   -o p01
gcc -std=gnu11 -pthread    p02.c share.c share.h   -o p02
200805-144125-1f77-TUGAS4/> ./p00
abdulazis02[START PID[04911] PPID[04845]]
abdulazis02[Boss is Waiting]
imamsetyo96[START PID[04912] PPID[04911]]
Gusni-Lusiana[START PID[04913] PPID[04911]]
imamsetyo96[Good Bye initNoBoss()!]
Gusni-Lusiana[Good Bye initNoBoss()!]
abdulazis02[All NoBosses are ready!]
imamsetyo96[Yes, I am ready!]
imamsetyo96[progs[00] TIME[002] MMAP[OPEN] VALUE[000] []]
imamsetyo96[progs[00] TIME[004] MMAP[OPEN] VALUE[800] [imamsetyo96]]
Gusni-Lusiana[Yes, I am ready!]
abdulazis02[Yes, I am ready!]
imamsetyo96[BYEBYE === ===== ===== =====]
Gusni-Lusiana[progs[01] TIME[007] MMAP[OPEN] VALUE[000] [imamsetyo96][][]]
abdulazis02[progs[02] TIME[009] MMAP[OPEN] VALUE[000] [imamsetyo96][Gusni-Lusiana][]]
Gusni-Lusiana[progs[01] TIME[010] MMAP[OPEN] VALUE[700] [imamsetyo96][Gusni-Lusiana][]]
Gusni-Lusiana[BYEBYE === ===== ===== =====]
abdulazis02[progs[02] TIME[012] MMAP[OPEN] VALUE[900] [imamsetyo96][Gusni-Lusiana][abdulazis02]]
abdulazis02[BYEBYE === ===== ===== =====]
200805-144205-691a-TUGAS4/> ./p01
imamsetyo96[START PID[04922] PPID[04845]]
imamsetyo96[Good Bye initNoBoss()!]
ShareMemory is NOT OPEN, BYE BYE ==== ==== 
200805-144212-38ea-TUGAS4/> exit
exit
Script done on 2020-08-05 14:42:15+07:00 [COMMAND_EXIT_CODE="0"]
```
