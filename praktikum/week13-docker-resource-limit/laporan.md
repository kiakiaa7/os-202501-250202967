
# Laporan Praktikum Minggu 13
Topik: Docker – Resource Limit (CPU & Memori)
---

## Identitas
- **Nama**  : SASKIA ISTIQOMAH
- **NIM**   : 250202967 
- **Kelas** : 1 IKRA

---

## Tujuan
Setelah menyelesaikan tugas ini, mahasiswa mampu:
1. Menulis Dockerfile sederhana untuk sebuah aplikasi/skrip.
2. Membangun image dan menjalankan container.
3. Menjalankan container dengan pembatasan **CPU** dan **memori**.
4. Mengamati dan menjelaskan perbedaan eksekusi container dengan dan tanpa limit resource.
5. Menyusun laporan praktikum secara runtut dan sistematis.

---

## Dasar Teori
Tuliskan ringkasan teori (3–5 poin) yang mendasari percobaan.

---

## Langkah Praktikum
1. **Persiapan Lingkungan**

   - Pastikan Docker terpasang dan berjalan.
   - Verifikasi:
     ```bash
     docker version
     docker ps
     ```

2. **Membuat Aplikasi/Skrip Uji**

   Buat program sederhana di folder `code/` (bahasa bebas) yang:
   - Melakukan komputasi berulang (untuk mengamati limit CPU), dan/atau
   - Mengalokasikan memori bertahap (untuk mengamati limit memori).

3. **Membuat Dockerfile**

   - Tulis `Dockerfile` untuk menjalankan program uji.
   - Build image:
     ```bash
     docker build -t week13-resource-limit .
     ```

4. **Menjalankan Container Tanpa Limit**

   - Jalankan container normal:
     ```bash
     docker run --rm week13-resource-limit
     ```
   - Catat output/hasil pengamatan.

5. **Menjalankan Container Dengan Limit Resource**

   Jalankan container dengan batasan resource (contoh):
   ```bash
   docker run --rm --cpus="0.5" --memory="256m" week13-resource-limit
   ```
   Catat perubahan perilaku program (mis. lebih lambat, error saat memori tidak cukup, dll.).

6. **Monitoring Sederhana**

   - Jalankan container (tanpa `--rm` jika perlu) dan amati penggunaan resource:
     ```bash
     docker stats
     ```
   - Ambil screenshot output eksekusi dan/atau `docker stats`.

7. **Commit & Push**

   ```bash
   git add .
   git commit -m "Minggu 13 - Docker Resource Limit"
   git push origin main
   ```

---

## Kode app.py
```bash
import time
import sys

storage = []
counter = 0

print("Aplikasi uji resource berjalan...")
sys.stdout.flush()

try:
    while True:
        # Beban CPU (perhitungan sederhana berulang)
        total = 0
        for n in range(3_000_000):
            total += n % 5

        # Alokasi memori bertahap (~3 MB per siklus)
        block = "#" * 3_000_000
        storage.append(block)

        counter += 1
        print(f"Siklus {counter} selesai | blok memori tersimpan: {len(storage)}")
        sys.stdout.flush()

        time.sleep(0.8)

except MemoryError:
    print("ERROR: Batas memori container telah tercapai")

```
Program ini dirancang sebagai aplikasi uji untuk mengamati pengaruh pembatasan resource pada Docker container. Penggunaan CPU disimulasikan melalui proses perhitungan berulang dalam jumlah besar, sedangkan penggunaan memori dilakukan dengan menambahkan data berukuran tertentu ke dalam sebuah list secara terus-menerus. Proses ini berjalan secara berulang hingga container mencapai batas resource yang ditetapkan atau dihentikan secara manual.

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

## Quiz
1. Mengapa container perlu dibatasi CPU dan memori?
   **Jawaban:**  
2. Apa perbedaan VM dan container dalam konteks isolasi resource?
   **Jawaban:**  
3.  Apa dampak limit memori terhadap aplikasi yang boros memori?
   **Jawaban:**  

---

## Refleksi Diri
Tuliskan secara singkat:
- Apa bagian yang paling menantang minggu ini?  
- Bagaimana cara Anda mengatasinya?  

---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
