
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
![Screenshot hasil](screenshots/ScreenshotDeadlock_Week11.png)

---

## Analisis
Tabel hasil deteksi :
| Proses | Resource Dialokasikan | Resource Diminta | Status   |
| ------ | --------------------- | ---------------- | -------- |
| P1     | R1                    | R2               | Deadlock |
| P2     | R2                    | R3               | Deadlock |
| P3     | R3                    | R1               | Deadlock |

Seluruh proses dalam status deadlock.
Deadlock terjadi karena setiap proses saling menunggu resource yang sedang dipegang oleh proses lain, sehingga tidak ada satu pun proses yang dapat melanjutkan eksekusi.

Secara rinci:

a. Proses P1 memegang resource R1 dan menunggu R2 yang sedang dipegang oleh P2

b. Proses P2 memegang resource R2 dan menunggu R3 yang sedang dipegang oleh P3

c. Proses P3 memegang resource R3 dan menunggu R1 yang sedang dipegang oleh P1

Kondisi ini membentuk circular wait, sehingga sistem mengalami kebuntuan permanen (deadlock).

Berdasarkan teori sistem operasi, deadlock terjadi apabila keempat kondisi berikut terpenuhi secara bersamaan. Pada kasus ini, seluruh kondisi tersebut terpenuhi:

1. Mutual Exclusion

Resource bersifat eksklusif, artinya hanya dapat digunakan oleh satu proses pada satu waktu. Terpenuhi, karena R1, R2, dan R3 tidak dapat dibagi.

2. Hold and Wait

Proses memegang satu resource sambil menunggu resource lain. Terpenuhi, karena setiap proses memegang satu resource dan menunggu resource berikutnya.

3. No Preemption

Resource tidak dapat direbut secara paksa dari proses yang sedang menggunakannya. Terpenuhi, karena resource hanya dilepas setelah proses selesai.

4. Circular Wait

Terdapat siklus ketergantungan antar proses. Terpenuhi, karena P1 → P2 → P3 → P1.
Karena keempat kondisi deadlock terpenuhi secara simultan dan tidak terdapat proses yang dapat dieksekusi hingga selesai, maka sistem berada dalam kondisi deadlock. Program deteksi deadlock berhasil mengidentifikasi proses-proses yang terlibat dalam deadlock secara tepat.

Solusi pencegahan deadlock
Deadlock dapat dicegah dengan menghilangkan salah satu dari empat kondisi deadlock. Pada kasus ini, penerapan resource ordering untuk mencegah circular wait merupakan solusi paling efektif. Alternatif lain adalah penggunaan algoritma penghindaran seperti Banker atau pendekatan deteksi dan pemulihan dengan menghentikan salah satu proses yang terlibat.

---

## Kesimpulan
Praktikum ini berhasil mensimulasikan dan mendeteksi kondisi deadlock pada sistem operasi menggunakan pendekatan algoritmik berbasis alokasi dan permintaan resource.
Hasil pengujian menunjukkan bahwa deadlock terjadi ketika seluruh proses saling menunggu resource yang sedang dipegang proses lain, sehingga tidak ada proses yang dapat diselesaikan.
Deteksi deadlock dapat digunakan sebagai dasar analisis untuk memahami penyebab deadlock, meskipun solusi pencegahan atau penghindaran tidak diimplementasikan dalam praktikum ini.


---
## Quiz
1. Apa perbedaan antara *deadlock prevention*, *avoidance*, dan *detection*?
   **Jawaban:**

* Deadlock prevention: Mencegah deadlock sejak awal dengan menghilangkan salah satu syarat deadlock. Deadlock dijamin tidak terjadi, tetapi penggunaan resource kurang efisien.

* Deadlock avoidance: Menghindari deadlock dengan mengecek kondisi aman (*safe state*) sebelum memberi resource. Lebih fleksibel, tetapi membutuhkan perhitungan dan informasi kebutuhan proses.

* Deadlock detection: Membiarkan deadlock terjadi lalu mendeteksinya dan melakukan pemulihan. Lebih sederhana dan efisien jika deadlock jarang terjadi, namun perlu mekanisme recovery.

2. Mengapa deteksi deadlock tetap diperlukan dalam sistem operasi?  
   **Jawaban:**

   Deteksi deadlock tetap diperlukan dalam sistem operasi karena tidak semua deadlock bisa dicegah atau dihindari secara efisien. Pendekatan prevention dan avoidance sering membatasi penggunaan resource atau membutuhkan informasi lengkap yang tidak selalu tersedia. Oleh karena itu, sistem operasi membiarkan resource digunakan secara bebas, lalu mendeteksi deadlock jika benar-benar terjadi. Dengan deteksi deadlock, sistem dapat menjaga efisiensi dan fleksibilitas, serta memulihkan sistem melalui penghentian proses atau pengambilan kembali resource agar sistem tetap berjalan normal.

   
3.  Apa kelebihan dan kekurangan pendekatan deteksi deadlock?
   **Jawaban:**

   Kelebihan:
Deteksi deadlock memungkinkan penggunaan resource lebih efisien karena sistem tidak membatasi proses secara ketat dan hanya menangani masalah saat deadlock benar-benar terjadi.

   Kekurangan:
Deadlock baru ditangani setelah terjadi, sehingga proses dapat berhenti sementara dan sistem memerlukan mekanisme pemulihan yang bisa mengganggu jalannya program.


---

## Refleksi Diri
Tuliskan secara singkat:
- Apa bagian yang paling menantang minggu ini?  
- Bagaimana cara Anda mengatasinya?  

---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
