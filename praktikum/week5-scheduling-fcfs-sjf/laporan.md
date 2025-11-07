
# Laporan Praktikum Minggu 5
Topik: Penjadwalan CPU – FCFS dan SJF

---

## Identitas
- **Nama**  : SASKIA ISTIQOMAH 
- **NIM**   : 250202967
- **Kelas** : 1IKRA

---

## Tujuan
Setelah menyelesaikan tugas ini, mahasiswa mampu:

1. Menghitung waiting time dan turnaround time untuk algoritma FCFS dan SJF.
2. Menyajikan hasil perhitungan dalam tabel yang rapi dan mudah dibaca.
3. Membandingkan performa FCFS dan SJF berdasarkan hasil analisis.
4. Menjelaskan kelebihan dan kekurangan masing-masing algoritma.
5. Menyimpulkan kapan algoritma FCFS atau SJF lebih sesuai digunakan.

---

## Dasar Teori

Penjadwalan CPU adalah proses yang dilakukan sistem operasi untuk menentukan urutan eksekusi proses yang menunggu giliran menggunakan prosesor. Tujuannya agar CPU dapat digunakan secara efisien dan setiap proses mendapat waktu eksekusi secara adil. Penjadwalan dapat bersifat *preemptive* (dapat digantikan) atau *non-preemptive* (tidak dapat digantikan hingga selesai).

*Pertama*, penjadwalan CPU bertujuan mengoptimalkan kinerja sistem melalui peningkatan *throughput*, pengurangan *waiting time*, serta pemanfaatan CPU yang maksimal.
**Kedua*, algoritma FCFS (First Come First Served) menjalankan proses berdasarkan urutan kedatangan. Algoritma ini mudah diterapkan namun dapat menyebabkan *convoy effect*, yaitu proses dengan waktu lama membuat proses lain menunggu.
*Ketiga*, algoritma SJF (Shortest Job First) memilih proses dengan waktu eksekusi (*burst time*) paling singkat. Metode ini dapat menurunkan waktu tunggu rata-rata, tetapi sulit diterapkan karena waktu eksekusi proses sering tidak diketahui.
*Keempat*, perbandingan keduanya menunjukkan bahwa FCFS unggul dalam kesederhanaan dan keadilan urutan, sedangkan SJF lebih efisien jika informasi durasi proses tersedia.
*Kelima*, kriteria evaluasi penjadwalan meliputi *CPU utilization*, *throughput*, *waiting time*, *turnaround time*, dan *response time* untuk menilai seberapa baik algoritma bekerja dalam mengelola proses.

---

---

## Langkah Praktikum
1. Langkah-langkah yang dilakukan.  
2. Perintah yang dijalankan.  
3. File dan kode yang dibuat.  
4. Commit message yang digunakan.

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
Tugas
1. Hitung waiting time dan turnaround time dari minimal 2 skenario FCFS dan SJF.
2. Sajikan hasil perhitungan dalam tabel perbandingan (FCFS vs SJF).
3. Analisis kelebihan dan kelemahan tiap algoritma.




---
## Quiz
1. Apa perbedaan utama antara FCFS dan SJF?
   **Jawaban:**  
2. Mengapa SJF dapat menghasilkan rata-rata waktu tunggu minimum?
   **Jawaban:**  
3. Apa kelemahan SJF jika diterapkan pada sistem interaktif? 
   **Jawaban:**  

---

## Refleksi Diri
Tuliskan secara singkat:
- Apa bagian yang paling menantang minggu ini?  
- Bagaimana cara Anda mengatasinya?  

---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
