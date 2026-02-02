
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
- Arsitektur Docker :
Docker menjalankan aplikasi dalam container yang terisolasi namun tetap menggunakan kernel sistem operasi host, sehingga penggunaan resource menjadi lebih efisien.

- Tujuan Pembatasan Resource :
Pembatasan CPU dan memori bertujuan untuk mencegah satu container menghabiskan seluruh resource sistem yang dapat mengganggu kinerja aplikasi lain.

- Pengaturan CPU Container :
Docker memungkinkan pengaturan batas penggunaan CPU sehingga container hanya dapat menggunakan sebagian kapasitas prosesor sesuai konfigurasi yang ditetapkan.

- Pengaturan Memori Container :
Batas memori pada container menentukan jumlah maksimum memori yang dapat digunakan. Jika melewati batas tersebut, container akan dihentikan oleh sistem.

- Dampak dan Keuntungan :
Dengan adanya resource limit, sistem menjadi lebih stabil, penggunaan resource lebih terkontrol, dan pengelolaan container dalam jumlah banyak menjadi lebih aman.
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
![Screenshot hasil](screenshots/Dockerweek_13.png)


## 1. Deskipsi Sistem
Sistem yang dibangun berupa:

* Bahasa pemrograman: Python
* Lingkungan:** Docker container
* Fungsi program: Mensimulasikan alokasi memori secara bertahap dalam beberapa siklus.

Program akan:

1. Menjalankan proses simulasi.
2. Menambahkan blok memori sedikit demi sedikit.
skripsi Sistem

3. Menampilkan jumlah blok memori yang telah tersimpan pada setiap siklus.

Contoh output program:

```
Simulasi resource berjalan...
Siklus 1 selesai | blok memori tersimpan: 1
Siklus 2 selesai | blok memori tersimpan: 2
...
```

## 2. Implementasi Docker

2.1 Struktur Proyek

Folder proyek berisi:

* `app.py` → Program utama simulasi resource
* `Dockerfile` → Konfigurasi pembuatan image Docker


2.2 Isi Dockerfile

```dockerfile
FROM python:3.10-slim
WORKDIR /app
COPY . .
CMD ["python", "app.py"]
```

Penjelasan:

| Perintah                   | Fungsi                                        |
| -------------------------- | --------------------------------------------- |
| `FROM python:3.10-slim`    | Menggunakan base image Python versi ringan    |
| `WORKDIR /app`             | Menentukan direktori kerja dalam container    |
| `COPY . .`                 | Menyalin semua file proyek ke dalam container |
| `CMD ["python", "app.py"]` | Menjalankan program saat container dijalankan |


## 3. Proses Build Image

Perintah yang digunakan:

```bash
docker build -t week13 .
```

Keterangan:

* `-t week13` → Memberi nama image
* `.` → Menggunakan Dockerfile di direktori saat ini

Hasilnya, image berhasil dibuat tanpa error.


## 4. Proses Menjalankan Container

Perintah yang digunakan:

```bash
docker run -it --rm week13
```

Keterangan:

* `-it` → Mode interaktif
* `--rm` → Container otomatis dihapus setelah berhenti
* `week13` → Nama image

## 5. Hasil Pengujian

Saat container dijalankan, program menghasilkan output:

* Program berjalan normal
* Setiap siklus menambah blok memori
* Nilai blok memori terus meningkat sesuai logika program

Hal ini menunjukkan bahwa:

* Aplikasi berhasil dijalankan dalam container
* Docker environment berjalan dengan benar
* Proses simulasi resource dapat diamati secara real-time

---

## Analisis


Berdasarkan hasil implementasi dan pengujian, program Python yang dijalankan di dalam container Docker menunjukkan perilaku seperti proses pada sistem operasi yang melakukan alokasi memori secara bertahap. Setiap siklus program menambahkan blok memori baru, sehingga penggunaan memori meningkat sedikit demi sedikit, bukan langsung dalam jumlah besar. Pola ini menggambarkan konsep *dynamic memory allocation*, di mana suatu proses akan terus menggunakan memori selama masih tersedia resource pada sistem. Selama pengujian, program dapat berjalan dengan normal tanpa gangguan, yang menunjukkan bahwa sistem masih mampu menangani permintaan memori tersebut.

Dari sisi container, Docker berhasil menyediakan lingkungan yang terisolasi untuk menjalankan aplikasi. Program berjalan di dalam container tanpa memengaruhi proses lain di sistem utama, karena Docker memanfaatkan mekanisme isolasi seperti *namespaces* dan *cgroups*. Hal ini membuktikan bahwa container bekerja seperti ruang terpisah yang memiliki lingkungan sendiri, sehingga penggunaan resource oleh aplikasi tetap terkontrol dan tidak langsung berdampak pada keseluruhan sistem.

Karena container dijalankan tanpa pembatasan resource seperti memori atau CPU, aplikasi dapat menggunakan resource sesuai ketersediaan pada host. Hal ini menunjukkan bahwa secara bawaan Docker tidak membatasi penggunaan resource, kecuali pengguna secara eksplisit menentukan batasnya. Kondisi ini relevan dengan konsep manajemen resource pada sistem operasi, di mana proses dapat terus berjalan dan meminta resource selama sistem masih mampu menyediakannya.

Secara keseluruhan, percobaan ini memperlihatkan hubungan yang jelas antara konsep manajemen memori pada sistem operasi dan pengelolaan resource pada Docker. Program berhasil mensimulasikan proses yang terus meminta memori, Docker menyediakan isolasi proses, dan sistem tetap stabil selama resource mencukupi. Praktikum ini membantu memahami bagaimana proses berjalan, bagaimana memori digunakan secara bertahap, serta bagaimana container berperan dalam mengontrol dan mengisolasi penggunaan resource.


---

## Kesimpulan

Berdasarkan praktikum yang telah dilakukan, dapat disimpulkan bahwa Docker dapat digunakan untuk menjalankan aplikasi dalam lingkungan yang terisolasi serta mengelola penggunaan resource sistem. Program Python yang dibuat berhasil mensimulasikan proses yang mengalokasikan memori secara bertahap, sehingga menggambarkan bagaimana suatu proses pada sistem operasi menggunakan memori selama masih tersedia. Selama pengujian, aplikasi berjalan dengan baik di dalam container tanpa mengganggu sistem utama, yang menunjukkan bahwa mekanisme isolasi Docker bekerja dengan efektif. Selain itu, percobaan ini juga memperlihatkan bahwa tanpa pembatasan resource, container dapat menggunakan memori sesuai kapasitas host. Dengan demikian, praktikum ini membantu memahami konsep manajemen memori, isolasi proses, serta peran Docker dalam pengelolaan resource pada lingkungan komputasi modern.


---

## Quiz
1. Mengapa container perlu dibatasi CPU dan memori?
   **Jawaban:**

   Container perlu dibatasi CPU dan memori agar penggunaan resource sistem tetap terkendali dan tidak mengganggu container atau aplikasi lain yang berjalan pada host yang sama. Tanpa pembatasan, sebuah container dapat menggunakan seluruh CPU atau memori yang tersedia, sehingga menyebabkan penurunan performa sistem atau bahkan membuat sistem menjadi tidak responsif. Dengan adanya pembatasan resource, setiap container hanya menggunakan jatah yang telah ditentukan sehingga sistem menjadi lebih stabil, adil, dan aman terutama pada lingkungan server atau produksi.
   
2. Apa perbedaan VM dan container dalam konteks isolasi resource?
   **Jawaban:**

   Virtual Machine (VM) melakukan isolasi resource dengan cara memvirtualisasikan seluruh hardware melalui hypervisor, sehingga setiap VM memiliki sistem operasi sendiri dan alokasi CPU, memori, serta storage yang benar-benar terpisah. Isolasi pada VM bersifat kuat namun membutuhkan resource yang lebih besar.

Sementara itu, container melakukan isolasi pada level sistem operasi dengan berbagi kernel host. Pembatasan CPU dan memori pada container diatur menggunakan mekanisme kernel seperti cgroups dan namespace, sehingga lebih ringan dan efisien, tetapi tingkat isolasinya tidak sekuat VM.

3.  Apa dampak limit memori terhadap aplikasi yang boros memori?
   **Jawaban:**
    
Penerapan limit memori pada aplikasi yang boros memori dapat menyebabkan aplikasi tersebut tidak dapat berjalan secara optimal. Ketika penggunaan memori melebihi batas yang telah ditentukan, sistem akan menghentikan proses aplikasi secara otomatis (Out of Memory / OOM Kill). Akibatnya, aplikasi dapat berhenti secara tiba-tiba, menimbulkan error, atau kehilangan data yang belum tersimpan. Namun demikian, pembatasan ini penting untuk menjaga kestabilan sistem agar aplikasi lain tidak terdampak oleh penggunaan memori yang berlebihan.


---

## Refleksi Diri
Tuliskan secara singkat:
- Apa bagian yang paling menantang minggu ini?  
- Bagaimana cara Anda mengatasinya?  

---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
