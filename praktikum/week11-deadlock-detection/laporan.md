
# Laporan Praktikum Minggu 11
Topik: Simulasi dan Deteksi Deadlock
---

## Identitas
- **Nama**  : SASKIA ISTIQOMAH
- **NIM**   : 250202967
- **Kelas** : 1 IKRA

---

## Tujuan
Setelah menyelesaikan tugas ini, mahasiswa mampu:
1. Membuat program sederhana untuk mendeteksi deadlock.  
2. Menjalankan simulasi deteksi deadlock dengan dataset uji.  
3. Menyajikan hasil analisis deadlock dalam bentuk tabel.  
4. Memberikan interpretasi hasil uji secara logis dan sistematis.  
5. Menyusun laporan praktikum sesuai format yang ditentukan.
---

## Dasar Teori
 - Deadlock adalah kondisi ketika dua atau lebih proses saling menunggu sumber daya yang sedang digunakan proses lain, sehingga tidak ada proses yang dapat melanjutkan eksekusi.
 - Konsep Deteksi Deadlock : Deteksi deadlock memungkinkan deadlock terjadi, kemudian sistem operasi melakukan pemeriksaan secara berkala untuk mendeteksi adanya deadlock dan mengambil tindakan pemulihan.
- Resource Allocation Graph (RAG) : RAG digunakan untuk merepresentasikan hubungan proses dan sumber daya. Deadlock terdeteksi jika terdapat siklus (cycle) pada graf, khususnya pada sistem dengan satu instance sumber daya.
- Algoritma Deteksi Deadlock : Pada sistem dengan satu instance resource, deadlock dideteksi dengan pencarian siklus pada RAG. Pada sistem dengan banyak instance, digunakan algoritma berbasis matriks (Available, Allocation, Request) untuk mengidentifikasi proses yang terjebak deadlock.
- Pemulihan Deadlock (Recovery) : Setelah deadlock terdeteksi, sistem melakukan pemulihan dengan cara menghentikan proses, melakukan *resource preemption*, atau melakukan *rollback* ke kondisi aman sebelumnya.

---

## Langkah Praktikum
1. **Menyiapkan Dataset**

   Gunakan dataset sederhana yang berisi:
   - Daftar proses  
   - Resource Allocation  
   - Resource Request / Need

   Contoh tabel:

   | Proses | Allocation | Request |
   |:--:|:--:|:--:|
   | P1 | R1 | R2 |
   | P2 | R2 | R3 |
   | P3 | R3 | R1 |

2. **Implementasi Algoritma Deteksi Deadlock**

   Program minimal harus:
   - Membaca data proses dan resource.  
   - Menentukan apakah sistem berada dalam kondisi deadlock.  
   - Menampilkan proses mana saja yang terlibat deadlock.

3. **Eksekusi & Validasi**

   - Jalankan program dengan dataset uji.  
   - Validasi hasil deteksi dengan analisis manual/logis.  
   - Simpan hasil eksekusi dalam bentuk screenshot.

4. **Analisis Hasil**

   - Sajikan hasil deteksi dalam tabel (proses deadlock / tidak).  
   - Jelaskan mengapa deadlock terjadi atau tidak terjadi.  
   - Kaitkan hasil dengan teori deadlock (empat kondisi).

5. **Commit & Push**

   ```bash
   git add .
   git commit -m "Minggu 11 - Deadlock Detection"
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

### Tugas
1. Buat program simulasi deteksi deadlock.  
2. Jalankan program dengan dataset uji.  
3. Sajikan hasil analisis dalam tabel dan narasi. 


---
## Quiz
1. Apa perbedaan antara *deadlock prevention*, *avoidance*, dan *detection*?
   **Jawaban:**  
2. Mengapa deteksi deadlock tetap diperlukan dalam sistem operasi?  
   **Jawaban:**  
3.  Apa kelebihan dan kekurangan pendekatan deteksi deadlock?
   **Jawaban:**  

---

## Refleksi Diri
Tuliskan secara singkat:
- Apa bagian yang paling menantang minggu ini?  
- Bagaimana cara Anda mengatasinya?  

---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
