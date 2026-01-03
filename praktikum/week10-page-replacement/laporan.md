
# Laporan Praktikum Minggu 10
Topik: Manajemen Memori – Page Replacement (FIFO & LRU)
---

## Identitas
- **Nama**  : SASKIA ISTIQOMAH
- **NIM**   : 250202967
- **Kelas** : 1 IKRA

---

## Tujuan
Setelah menyelesaikan tugas ini, mahasiswa mampu:
1. Mengimplementasikan algoritma page replacement FIFO dalam program.
2. Mengimplementasikan algoritma page replacement LRU dalam program.
3. Menjalankan simulasi page replacement dengan dataset tertentu.
4. Membandingkan performa FIFO dan LRU berdasarkan jumlah *page fault*.
5. Menyajikan hasil simulasi dalam laporan yang sistematis.

---

## Dasar Teori

1. Manajemen memori : dalam sistem operasi bertujuan mengatur penggunaan memori utama secara efisien, terutama pada sistem memori virtual yang menggunakan mekanisme *page* dan *page fault*.

2. Page replacement : diperlukan ketika terjadi *page fault* dan memori sudah penuh, sehingga sistem harus menentukan halaman mana yang akan dikeluarkan untuk memberi ruang bagi halaman baru.

3. FIFO (First In, First Out) : mengganti halaman berdasarkan urutan masuk, dengan kelebihan berupa implementasi yang sederhana, tetapi memiliki kelemahan karena tidak mempertimbangkan pola akses dan dapat menyebabkan *Belady’s Anomaly*.

4. LRU (Least Recently Used) : mengganti halaman yang paling lama tidak digunakan, sehingga lebih sesuai dengan prinsip *locality of reference* dan umumnya menghasilkan jumlah *page fault* yang lebih rendah.

5. Perbandingan FIFO dan LRU : menunjukkan bahwa FIFO unggul dalam kesederhanaan, sedangkan LRU unggul dalam efisiensi kinerja, meskipun membutuhkan kompleksitas dan overhead implementasi yang lebih tinggi.

---

## Langkah Praktikum
1. **Menyiapkan Dataset**

   Gunakan *reference string* berikut sebagai contoh:
   ```
   7, 0, 1, 2, 0, 3, 0, 4, 2, 3, 0, 3, 2
   ```
   Jumlah frame memori: **3 frame**.

2. **Implementasi FIFO**

   - Simulasikan penggantian halaman menggunakan algoritma FIFO.
   - Catat setiap *page hit* dan *page fault*.
   - Hitung total *page fault*.

3. **Implementasi LRU**

   - Simulasikan penggantian halaman menggunakan algoritma LRU.
   - Catat setiap *page hit* dan *page fault*.
   - Hitung total *page fault*.

4. **Eksekusi & Validasi**

   - Jalankan program untuk FIFO dan LRU.
   - Pastikan hasil simulasi logis dan konsisten.
   - Simpan screenshot hasil eksekusi.

5. **Analisis Perbandingan**

   Buat tabel perbandingan seperti berikut:

   | Algoritma | Jumlah Page Fault | Keterangan |
   |:--|:--:|:--|
   | FIFO | ... | ... |
   | LRU | ... | ... |


   - Jelaskan mengapa jumlah *page fault* bisa berbeda.
   - Analisis algoritma mana yang lebih efisien dan alasannya.

6. **Commit & Push**

   ```bash
   git add .
   git commit -m "Minggu 10 - Page Replacement FIFO & LRU"
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
## Tugas dan Analisis

**Simulasi Algoritma FIFO (First In First Out)**
Reference String: [7, 0, 1, 2, 0, 3, 0, 4, 2, 3, 0, 3, 2]*
  *Jumlah Frame: 3*
  
  FIFO (First-In First-Out)
  
    | Step  | Akses  | Status  | Frames |
    |---|---|---|---|
    | 1     | 7      | FAULT   | [7]
    | 2     | 0      | FAULT   | [7, 0]
    | 3     | 1      | FAULT   | [7, 0, 1]
    | 4     | 2      | FAULT   | [2, 0, 1]
    | 5     | 0      | HIT     | [2, 0, 1]
    | 6     | 3      | FAULT   | [2, 3, 1]
    | 7     | 0      | FAULT   | [2, 3, 0]
    | 8     | 4      | FAULT   | [4, 3, 0]
    | 9     | 2      | FAULT   | [4, 2, 0]
    | 10    | 3      | FAULT   | [4, 2, 3]
    | 11    | 0      | FAULT   | [0, 2, 3]
    | 12    | 3      | HIT     | [0, 2, 3]
    | 13    | 2      | HIT     | [0, 2, 3]


HASIL AKHIR:
Total Akses      : 13
Total Page Hits  : 3
Total Page Faults: 10

 **Simulasi Algoritma LRU (Least Recently Used)**

    | Step  | Akses  | Status  | Frames (Urutan LRU) |
    |---|---|---|---|
    | 1     | 7      | FAULT   | [7] |
    | 2     | 0      | FAULT   | [7, 0] |
    | 3     | 1      | FAULT   | [7, 0, 1] |
    | 4     | 2      | FAULT   | [0, 1, 2] |
    | 5     | 0      | HIT     | [1, 2, 0] |
    | 6     | 3      | FAULT   | [2, 0, 3] |
    | 7     | 0      | HIT     | [2, 3, 0] |
    | 8     | 4      | FAULT   | [3, 0, 4] |
    | 9     | 2      | FAULT   | [0, 4, 2] |
    | 10    | 3      | FAULT   | [4, 2, 3] |
    | 11    | 0      | FAULT   | [2, 3, 0] |
    | 12    | 3      | HIT     | [2, 0, 3] |
    | 13    | 2      | HIT     | [0, 3, 2] |


HASIL AKHIR (LRU):
Total Page Hits  : 4
Total Page Faults: 9

**Tabel Perbandingan**

| Algoritma | Jumlah Page Fault | Keterangan                          |
| --------- | ----------------- | ----------------------------------- |
| FIFO      | 10                | Tidak mempertimbangkan pola akses   |
| LRU       | 9                 | Mempertimbangkan histori penggunaan |

**Mengapa jumlah page fault bisa berbeda?**

Jumlah page fault dapat berbeda karena adanya perbedaan mekanisme kerja pada setiap algoritma penggantian halaman. Pada algoritma FIFO (First-In, First-Out), halaman yang paling awal masuk ke memori akan diganti terlebih dahulu tanpa mempertimbangkan apakah halaman tersebut masih sering digunakan. Kondisi ini dapat menyebabkan halaman yang masih dibutuhkan justru dikeluarkan dari memori, sehingga meningkatkan jumlah page fault. Sementara itu, algoritma LRU (Least Recently Used) mengganti halaman yang paling lama tidak digunakan berdasarkan riwayat akses sebelumnya. Pendekatan ini lebih selaras dengan pola akses program yang nyata, di mana halaman yang baru saja digunakan cenderung akan digunakan kembali, sehingga LRU lebih adaptif dan umumnya menghasilkan jumlah *page fault* yang lebih sedikit dibandingkan FIFO.

Perbedaan jumlah page fault juga dipengaruhi oleh beberapa faktor, seperti urutan akses halaman. Jika program sering mengakses ulang halaman yang baru digunakan, LRU akan bekerja lebih efisien karena mempertahankan halaman tersebut di memori. Sebaliknya, FIFO dapat secara keliru mengganti halaman yang masih dibutuhkan jika halaman tersebut merupakan halaman yang masuk lebih awal. Selain itu, jumlah frame atau slot memori juga berpengaruh, di mana semakin banyak frame biasanya akan mengurangi page fault. Namun, pada FIFO dapat terjadi fenomena *Belady’s Anomaly*, yaitu kondisi ketika penambahan jumlah frame justru menyebabkan page fault meningkat. Secara keseluruhan, perbedaan aturan penggantian halaman pada setiap algoritma menjadi alasan utama mengapa jumlah page fault yang dihasilkan bisa berbeda.

**Analisis algoritma mana yang lebih efisien dan alasannya?**

Algoritma LRU (Least Recently Used) dinilai lebih efisien dibandingkan FIFO karena mampu menyesuaikan diri dengan pola penggunaan memori program. LRU mengganti halaman yang sudah lama tidak digunakan, sehingga halaman yang masih aktif dan sering diakses tetap berada di dalam memori. Pendekatan ini membantu mengurangi terjadinya page fault. Sementara itu, FIFO mengganti halaman berdasarkan urutan masuk tanpa melihat apakah halaman tersebut masih dibutuhkan, sehingga dapat menyebabkan penggantian halaman yang kurang tepat dan meningkatkan jumlah page fault. Oleh karena itu, dari segi efisiensi penggunaan memori dan minimisasi page fault, LRU lebih unggul dibandingkan FIFO.

---
## Kesimpulan

* Praktikum membandingkan algoritma *page replacement* FIFO dan LRU menggunakan dataset dan jumlah frame yang sama.
* Hasil simulasi menunjukkan bahwa **LRU menghasilkan jumlah page fault lebih sedikit dibandingkan FIFO**.
* FIFO mengganti halaman berdasarkan urutan masuk tanpa mempertimbangkan pola penggunaan halaman.
* LRU mengganti halaman yang paling lama tidak digunakan sehingga lebih sesuai dengan pola akses program (*locality of reference*).
* FIFO berpotensi membuang halaman yang masih dibutuhkan dan dapat mengalami **Belady’s Anomaly**.
* LRU lebih efisien dalam penggunaan memori, namun memiliki tingkat kompleksitas implementasi yang lebih tinggi dibandingkan FIFO.

---
## Quiz
1. Apa perbedaan utama FIFO dan LRU?
   **Jawaban:**
   
 Perbedaan utama antara FIFO dan LRU terletak pada dasar penentuan data yang dikeluarkan dari penyimpanan. FIFO menghapus data berdasarkan urutan waktu masuk, sehingga data yang pertama kali disimpan akan dikeluarkan lebih dahulu tanpa memperhatikan apakah data tersebut masih sering digunakan atau tidak.
Sebaliknya, LRU menghapus data berdasarkan *waktu terakhir penggunaan*, yaitu data yang paling lama tidak diakses akan dikeluarkan terlebih dahulu, sehingga lebih mempertimbangkan pola dan frekuensi akses data.

2. Mengapa FIFO dapat menghasilkan *Belady’s Anomaly*?
   **Jawaban:**
   
 FIFO dapat menyebabkan *Belady’s Anomaly* karena mekanisme penggantian halamannya hanya bergantung pada urutan halaman masuk ke memori, bukan pada seberapa sering atau seberapa baru halaman tersebut digunakan. Ketika jumlah frame memori ditambah, FIFO tetap akan mengeluarkan halaman yang paling lama berada di memori, meskipun halaman tersebut masih dibutuhkan dalam waktu dekat. Akibatnya, penambahan frame tidak menjamin berkurangnya *page fault* dan dalam kondisi tertentu justru dapat meningkat.

Hal ini terjadi karena FIFO tidak menjamin konsistensi isi memori saat kapasitas bertambah, sehingga halaman yang tersimpan pada memori kecil belum tentu tetap ada pada memori yang lebih besar. Ketidakstabilan inilah yang memicu *Belady’s Anomaly*, di mana lebih banyak sumber daya memori tidak selalu berbanding lurus dengan peningkatan kinerja sistem.

3. Mengapa LRU umumnya menghasilkan performa lebih baik dibanding FIFO?
   **Jawaban:**  

LRU cenderung menghasilkan performa yang lebih baik dibanding FIFO karena algoritma ini mengikuti kebiasaan alami akses memori, di mana data yang baru digunakan memiliki kemungkinan besar untuk diakses kembali dalam waktu dekat. Dengan menjadikan riwayat penggunaan sebagai dasar penggantian, LRU mampu menjaga halaman yang masih relevan tetap berada di memori dan mengeluarkan halaman yang sudah tidak aktif digunakan.

Sebaliknya, FIFO tidak memperhatikan apakah suatu halaman masih sering dipakai atau tidak, sehingga berpotensi mengganti halaman yang sebenarnya masih dibutuhkan oleh proses. Akibatnya, FIFO lebih sering mengalami *page fault*. Karena LRU menyesuaikan isi memori dengan kebutuhan aktual sistem, algoritma ini umumnya memberikan kinerja yang lebih konsisten dan efisien dibanding FIFO.

---

## Refleksi Diri
Tuliskan secara singkat:
- Apa bagian yang paling menantang minggu ini?  
- Bagaimana cara Anda mengatasinya?  

---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
