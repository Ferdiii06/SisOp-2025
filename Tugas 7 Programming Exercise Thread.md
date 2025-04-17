Programming Exercise
Sumber: osc10e - ch4

a. Penerapan Thread pada SumTask.java (Java)
Penjelasan
File SumTask.java menggunakan framework Fork/Join di Java untuk membagi tugas penjumlahan array besar menjadi sub-tugas yang lebih kecil. Kelas ini memperluas RecursiveTask dan mengimplementasikan metode compute() untuk memproses bagian dari array. Jika ukuran bagian lebih kecil dari ambang batas tertentu, penjumlahan dilakukan secara langsung; jika tidak, tugas dibagi lagi dan diproses secara rekursif. Pendekatan ini memanfaatkan kemampuan multi-core untuk meningkatkan kinerja komputasi.

​# Analisis Implementasi Thread

## A. Implementasi Thread di Java (SumTask.java)

### Konsep dan Implementasi
File `SumTask.java` menunjukkan penerapan dasar multithreading di Java dengan membagi tugas penjumlahan besar ke beberapa thread.

**Komponen Utama**:

1. **Pembuatan Thread**:
```java
// Membuat array thread
Thread[] threads = new Thread[NUM_THREADS];
for (int i = 0; i < NUM_THREADS; i++) {
    threads[i] = new Thread(new SumWorker(start, end));
    start = end + 1;
    end += range;
}

Setiap thread mengolah range angak yang berbeda

2. Kelas Worker :

class SumWorker implements Runnable {
    private final int start;
    private final int end;
    
    public void run() {
        int partialSum = 0;
        for (int i = start; i <= end; i++) {
            partialSum += i;
        }
        synchronized(this) {
            totalSum += partialSum;
        }
    }
}

Mengimplementasikan antarmuka Runnable

3. Manajemen thread

// Memulai semua thread
for (Thread thread : threads) {
    thread.start();
}

// Menunggu penyelesaian
for (Thread thread : threads) {
    thread.join();
}

Analisis
Kelebihan: Portabel di semua platform yang mendukung JVM
Keterbatasan: Terikat pada implementasi thread JVM
Sinkronisasi: Menggunakan blok synchronized

B. Implementasi Thread Spesifik Platform
1. Thread POSIX (Linux) - thrd-posix.c
Gambaran Arsitektur:
Thread POSIX (pthread) menyediakan API standar untuk sistem UNIX/Linux.
Implementasi:

1. Pembuatan Thread:
pthread_t threads[THREAD_COUNT];
struct thread_params params[THREAD_COUNT];

for (int i = 0; i < THREAD_COUNT; i++) {
    params[i].thread_num = i;
    pthread_create(&threads[i], NULL, worker, &params[i]);
}

2. Fungsi thread:
void *worker(void *arg) {
    struct thread_params *params = (struct thread_params *)arg;
    printf("Thread %d bekerja\n", params->thread_num);
    return NULL;
}

3. Penggabungan thread :
for (int i = 0; i < THREAD_COUNT; i++) {
    pthread_join(threads[i], NULL);
}

2. Thread Win32 (Windows) - thrd-win32.c
Integrasi Sistem:
Thread Win32 terintegrasi dengan Windows API.

Implementasi:

Pembuatan Thread:
HANDLE threads[THREAD_COUNT];
DWORD threadIDs[THREAD_COUNT];

for (int i = 0; i < THREAD_COUNT; i++) {
    threads[i] = CreateThread(
        NULL,                   
        0,                      
        worker,                 
        &params[i],             
        0,                      
        &threadIDs[i]           
    );
}

2. Fungsi thread
DWORD WINAPI worker(LPVOID arg) {
    struct thread_params *params = (struct thread_params *)arg;
    printf("Thread %d bekerja\n", params->thread_num);
    return 0;
}
