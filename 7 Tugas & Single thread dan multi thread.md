TUGAS SISTEM BILANGAN

Nama: Ferry Ferdiansyah
NRP: 3124500051
Dosen Pengajar: Dr. Ferry Astika Saputra ST, M.Sc
Program Studi: D3 Teknik Informatika
Institusi: Politeknik Elektronika Negeri Surabaya (PENS)
Tahun: 2025

Konsep Single Thread dan Multithread

Single Thread

Dalam komputasi, single thread merujuk pada eksekusi proses secara berurutan menggunakan satu jalur eksekusi. Artinya, program hanya dapat melakukan satu tugas pada satu waktu. Jika ada beberapa tugas yang harus diselesaikan, maka tugas-tugas tersebut harus dilakukan secara bergantian, menunggu tugas sebelumnya selesai. Ini bisa menjadi kendala ketika program harus menangani operasi yang memakan waktu, seperti membaca file besar atau menunggu data dari jaringan, karena seluruh program akan berhenti hingga tugas tersebut selesai.

Multithread

Sementara itu, multithread memungkinkan program untuk menjalankan beberapa thread (jalur eksekusi) secara bersamaan. Setiap thread dapat mengerjakan tugas berbeda dalam waktu yang bersamaan, sehingga meningkatkan efisiensi dan kecepatan program. Misalnya, dalam aplikasi berbasis antarmuka grafis (GUI), satu thread bisa menangani input pengguna sementara thread lain memproses data di latar belakang. Pendekatan ini sangat berguna untuk meningkatkan kinerja sistem, terutama pada prosesor multi-core yang bisa menjalankan banyak thread sekaligus.

Ilustrasi :

![gambar singlethread dan multithread](https://github.com/user-attachments/assets/a637f687-7f7f-4483-9294-2b3e833aa562)

