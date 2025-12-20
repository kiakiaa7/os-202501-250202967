
# Laporan Praktikum Minggu [X]
Topik: Simulasi Algoritma Penjadwalan CPU

---

## Identitas
- **Nama**  : SASKIA ISTIQOMAH
- **NIM**   : 250202967 
- **Kelas** : 1 IKRA

---

## Tujuan
Setelah menyelesaikan tugas ini, mahasiswa mampu:
1. Membuat program simulasi algoritma penjadwalan FCFS dan/atau SJF.  
2. Menjalankan program dengan dataset uji yang diberikan atau dibuat sendiri.  
3. Menyajikan output simulasi dalam bentuk tabel atau grafik.  
4. Menjelaskan hasil simulasi secara tertulis.  
5. Mengunggah kode dan laporan ke Git repository dengan rapi dan tepat waktu.

---

## Dasar Teori

1. Sistem Operasi dan Manajemen Proses
   Sistem operasi berfungsi mengelola sumber daya komputer, salah satunya adalah manajemen proses. Manajemen proses bertugas mengatur eksekusi beberapa proses agar dapat berjalan secara efisien dengan memanfaatkan CPU secara optimal.

2. Konsep Penjadwalan CPU
   Penjadwalan CPU adalah mekanisme penentuan urutan proses yang akan dieksekusi oleh CPU. Karena CPU hanya dapat memproses satu proses pada satu waktu, penjadwalan diperlukan untuk mengatur giliran eksekusi proses.

3. Algoritma Penjadwalan CPU
   Algoritma penjadwalan CPU merupakan aturan yang digunakan untuk memilih proses yang akan dijalankan, seperti First Come First Served (FCFS), Shortest Job First (SJF), Priority Scheduling, dan Round Robin (RR). Setiap algoritma memiliki karakteristik serta kelebihan dan kekurangan masing-masing.

4. Parameter Kinerja Penjadwalan
   Kinerja algoritma penjadwalan dievaluasi menggunakan parameter seperti waiting time, turnaround time, response time, dan CPU utilization. Parameter ini digunakan untuk menilai efisiensi dan keadilan suatu algoritma penjadwalan.

5.  Simulasi Algoritma Penjadwalan CPU
   Simulasi algoritma penjadwalan CPU digunakan untuk memodelkan dan menganalisis cara kerja algoritma dalam kondisi tertentu. Melalui simulasi, performa berbagai algoritma dapat dibandingkan dan dipahami tanpa harus diterapkan langsung pada sistem operasi nyata.


---

## Langkah Praktikum
1. **Menyiapkan Dataset**

   Buat dataset proses minimal berisi:

   | Proses | Arrival Time | Burst Time |
   |:--:|:--:|:--:|
   | P1 | 0 | 6 |
   | P2 | 1 | 8 |
   | P3 | 2 | 7 |
   | P4 | 3 | 3 |

2. **Implementasi Algoritma**

   Program harus:
   - Menghitung *waiting time* dan *turnaround time*.  
   - Mendukung minimal **1 algoritma (FCFS atau SJF non-preemptive)**.  
   - Menampilkan hasil dalam tabel.

3. **Eksekusi & Validasi**

   - Jalankan program menggunakan dataset uji.  
   - Pastikan hasil sesuai dengan perhitungan manual minggu sebelumnya.  
   - Simpan hasil eksekusi (screenshot).

4. **Analisis**

   - Jelaskan alur program.  
   - Bandingkan hasil simulasi dengan perhitungan manual.  
   - Jelaskan kelebihan dan keterbatasan simulasi.

5. **Commit & Push**

   ```bash
   git add .
   git commit -m "Minggu 9 - Simulasi Scheduling CPU"
   git push origin main
   ```
---

## Kode / Perintah
Tuliskan potongan kode atau perintah utama:
```bash
uname -a
lsmod | head
dmesg | head
```
---

## Hasil Eksekusi
Sertakan screenshot hasil percobaan atau diagram:
![Screenshot hasil](screenshots/example.png)

---

## Analisis
- Jelaskan makna hasil percobaan.  
- Hubungkan hasil dengan teori (fungsi kernel, system call, arsitektur OS).  
- Apa perbedaan hasil di lingkungan OS berbeda (Linux vs Windows)?  

---

## Kesimpulan
Tuliskan 2–3 poin kesimpulan dari praktikum ini.

--- 

## Tugas 
1. Buat program simulasi FCFS atau SJF.  
2. Jalankan program dengan dataset uji.  
3. Sajikan output dalam tabel atau grafik.  
4. Tulis laporan praktikum pada `laporan.md`.
   
---

## Quiz
1. Mengapa simulasi diperlukan untuk menguji algoritma scheduling?
   **Jawaban:**
   Simulasi diperlukan untuk menguji algoritma scheduling karena memungkinkan pengujian dilakukan tanpa risiko mengganggu sistem operasi nyata. Melalui simulasi, berbagai algoritma dapat diuji dan dibandingkan secara objektif menggunakan kondisi yang sama, sehingga analisis kinerjanya lebih akurat. Selain itu, simulasi menghemat waktu dan biaya karena tidak memerlukan perubahan pada perangkat keras maupun sistem operasi. Simulasi juga memungkinkan pengujian berbagai skenario, termasuk kondisi beban sistem yang tinggi, serta membantu pemahaman konsep penjadwalan melalui visualisasi alur eksekusi proses.

2. Apa perbedaan hasil simulasi dengan perhitungan manual jika dataset besar?  
   **Jawaban:**
    Pada dataset yang besar, perbedaan antara hasil simulasi dan perhitungan manual lebih terlihat pada proses pengerjaannya. Perhitungan manual menjadi sulit, memakan waktu lama, dan sangat rentan terhadap kesalahan karena banyaknya data yang harus dihitung satu per satu. Sebaliknya, simulasi dapat mengolah data dalam jumlah besar dengan cepat dan konsisten, sehingga hasilnya lebih akurat dan dapat diandalkan. Selain itu, simulasi mampu menangani kondisi yang kompleks yang sulit dilakukan secara manual. Oleh karena itu, meskipun secara teori hasilnya sama, simulasi jauh lebih efektif dan praktis dibandingkan perhitungan manual pada dataset besar.

3. Algoritma mana yang lebih mudah diimplementasikan? Jelaskan. 
   **Jawaban:**  
    Algoritma yang paling mudah diimplementasikan adalah First Come First Served (FCFS). Hal ini karena FCFS menggunakan prinsip sederhana, yaitu proses dieksekusi sesuai urutan kedatangannya tanpa adanya prioritas atau pembagian waktu khusus. Implementasinya hanya memerlukan satu antrean (queue) dan tidak membutuhkan perhitungan tambahan seperti estimasi burst time, prioritas, atau time quantum. Selain itu, FCFS bersifat non-preemptive, sehingga tidak perlu mekanisme interupsi proses yang sedang berjalan. Karena kesederhanaan inilah, FCFS sering digunakan sebagai algoritma dasar dalam pembelajaran penjadwalan CPU.

---

## Refleksi Diri
Tuliskan secara singkat:
- Apa bagian yang paling menantang minggu ini?  
- Bagaimana cara Anda mengatasinya?  

---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
