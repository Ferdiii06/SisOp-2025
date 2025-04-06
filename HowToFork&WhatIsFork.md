# TEORI TUGAS 5 SISTEM OPERASI  
## PENJELASAN FORKING DAN ANALISIS KODE  

**Nama**: Ferry Ferdiansyah  
**NRP**: 3124500050  
**Dosen Pengajar**: Dr Ferry Astika Saputra ST, M.Sc  

**PROGRAM STUDI D3 TEKNIK INFORMATIKA**  
**POLITEKNIK ELEKTRONIKA NEGERI SURABAYA (PENS)**  
**TAHUN 2025**  

---

## Penjelasan Forking dan Analisis Kode  

### Forking dalam Sistem Operasi  
Forking adalah konsep dalam sistem operasi di mana sebuah proses membuat salinan dirinya sendiri (proses anak) yang berjalan secara independen dari proses asal (proses induk). Ini adalah cara utama untuk membuat proses baru dalam sistem Unix/Linux.  

#### Contoh Forking dalam C  
```c
#include <stdio.h>
#include <unistd.h>
#include <sys/types.h>

int main() {
    pid_t pid;

    printf("Proses induk (PID: %d)\n", getpid());

    // Membuat proses anak
    pid = fork();

    if (pid < 0) {
        // Gagal membuat fork
        fprintf(stderr, "Fork gagal\n");
        return 1;
    } else if (pid == 0) {
        // Kode untuk proses anak
        printf("Proses anak (PID: %d), Induk PID: %d\n", getpid(), getppid());
    } else {
        // Kode untuk proses induk
        printf("Proses induk (PID: %d) membuat anak dengan PID: %d\n", getpid(), pid);
    }

    return 0;
}

Analisis Kode Forking:
#include <unistd.h> - Header file yang berisi deklarasi fork()
pid_t - Tipe data khusus untuk Process ID
fork() - Fungsi sistem yang membuat proses baru
Mengembalikan 0 ke proses anak

Mengembalikan PID anak ke proses induk
Mengembalikan -1 jika gagal
getpid() - Mendapatkan PID proses saat ini
getppid() - Mendapatkan PID proses induk

Kelebihan
1.Implementasi rekursif mudah dibaca
2.Ada validasi input untuk bilangan negatif
3.Struktur kode sederhana dan jelas

Kekurangan
4.Rentan stack overflow untuk input besar
5.Tidak menangani input non-integer
6.Tidak ada batasan atas untuk input

Analisis Kode
Analisis kode adalah proses memeriksa, memahami, dan mengevaluasi kode sumber untuk berbagai tujuan seperti debugging, optimasi, atau pemahaman fungsionalitas.
