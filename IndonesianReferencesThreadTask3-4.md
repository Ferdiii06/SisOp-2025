# TEORI TUGAS OPERASI SISTEM  
## REFERENCES INDONESIA THREAD, TASK NUMBER 3-4  

**Nama**: Ferry Ferdiansyah  
**NRP**: 3124500050  
**Dosen Pengajar**: Dr Ferry Astika Saputra ST, M.Sc  

**PROGRAM STUDI D3 TEKNIK INFORMATIKA**  
**POLITEKNIK ELEKTRONIKA NEGERI SURABAYA (PENS)**  
**TAHUN 2025**  

---

## References Indonesian Thread, Task Number 3-4  

### 2.11.1. Proses  

#### 3. Tindakan Kernel saat Alih Konteks Antar Proses  
Alih konteks (context switching) adalah proses ketika sistem operasi:  
1. Menyimpan konteks proses saat ini (register CPU, program counter)  
2. Memperbarui Process Control Block (PCB)  
3. Memuat konteks proses baru  
4. Memperbarui manajemen memori  
5. Mengatur ulang register CPU  

#### 4. Informasi dalam Tabel Proses saat Alih Konteks  
- Register CPU (general & special purpose)  
- Program Counter  
- Stack Pointer  
- Status proses (ready/running/waiting)  
- Manajemen memori (base/limit register, page table)  
- Informasi akun (UID, GID, waktu CPU)  
- I/O dan file yang digunakan  

---

### 2.11.2. Thread  

#### 3. Perbedaan User-Level vs Kernel-Level Thread  
| **Aspek**          | **User-Level Thread**               | **Kernel-Level Thread**            |  
|---------------------|-------------------------------------|-------------------------------------|  
| Manajemen           | Pustaka pengguna                    | Kernel                              |  
| Overhead            | Lebih cepat                         | Lebih lambat                        |  

**Kondisi Penggunaan:**  
- *User-level*: Cocok untuk aplikasi dengan banyak thread ringan tanpa blocking system call  
- *Kernel-level*: Ideal untuk multi-core CPU dan paralelisme  

#### 4. Tindakan Kernel saat Alih Konteks Kernel-Level Thread  
1. Menyimpan register & program counter thread lama  
2. Memuat register & program counter thread baru  
3. Memperbarui scheduler  
4. Memastikan konsistensi memori (cache/TLB)  

---

### 2.11.3. Penjadualan CPU  

#### 3. Keuntungan Time Quantum Berbeda di Multilevel Queue  
- **Prioritas Proses**: Quantum kecil untuk proses interaktif, besar untuk batch  
- **Hindari Starvation**: Proses prioritas rendah tetap dieksekusi  
- **Efisiensi CPU**: Kurangi overhead context switching  
- **Fleksibilitas**: Adaptasi kebutuhan tiap level queue  

#### 4. Ilustrasi Eksekusi Proses  

**Data Proses:**  
| Proses | Burst Time | Prioritas |  
|--------|------------|-----------|  
| P1     | 10         | 3         |  
| P2     | 1          | 1         |  
| P3     | 2          | 4         |  
| P4     | 1          | 4         |  
| P5     | 5          | 2         |  

**Gantt Chart:**  

**a) FCFS**  
`P1 | P2 | P3 | P4 | P5`  
Waktu: `0 → 10 → 11 → 13 → 14 → 19`  

**b) SJF**  
`P2 | P4 | P3 | P5 | P1`  
Waktu: `0 → 1 → 2 → 4 → 9 → 19`  

**c) Prioritas Non-Preemptive**  
`P2 | P5 | P1 | P3 | P4`  
Waktu: `0 → 1 → 6 → 16 → 18 → 19`  

**d) Round Robin (Quantum=2)**  
`P1 | P2 | P3 | P4 | P5 | P1 | P5 | P1 | P5 | P1 | P1`  
Waktu: `0 → 2 → 3 → 5 → 6 → 8 → 10 → 12 → 13 → 15 → 17 → 19`  
