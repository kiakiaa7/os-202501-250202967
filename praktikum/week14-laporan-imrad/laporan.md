
# Laporan Praktikum Minggu 14
Topik: Penyusunan Laporan Praktikum Format IMRAD

---

## Identitas
- **Nama**  : SASKIA ISTIQOMAH
- **NIM**   : 250202967
- **Kelas** : 1 IKRA

---
# DEADLOCK DETECTION

---
## Pendahuluan

Sistem operasi memiliki peran penting dalam mengatur penggunaan sumber daya komputer seperti CPU, memori, dan perangkat input/output agar dapat digunakan oleh banyak proses secara bersamaan. Dalam pengelolaan sumber daya tersebut, dapat terjadi kondisi di mana beberapa proses saling menunggu sumber daya yang sedang digunakan oleh proses lain. Akibatnya, tidak ada proses yang dapat melanjutkan eksekusi. Kondisi ini dikenal sebagai deadlock.

Deadlock merupakan salah satu permasalahan klasik dalam sistem operasi karena dapat menyebabkan sistem menjadi tidak responsif dan proses tidak dapat diselesaikan. Oleh sebab itu, diperlukan mekanisme untuk mengenali atau mendeteksi kondisi deadlock agar sistem dapat melakukan tindakan pemulihan, seperti menghentikan proses tertentu atau merebut kembali sumber daya.

Pada praktikum minggu ke-11 ini dilakukan simulasi sederhana untuk memahami bagaimana deadlock terjadi dan bagaimana cara mendeteksinya menggunakan pendekatan algoritmik. Simulasi dilakukan dengan data proses dan alokasi resource tertentu untuk melihat apakah sistem berada dalam kondisi aman atau mengalami deadlock.

---
## Rumusan Masalah

 Berdasarkan latar belakang di atas, rumusan masalah pada praktikum ini adalah:

1. Bagaimana cara mensimulasikan kondisi deadlock pada sistem operasi?

2. Bagaimana mekanisme pendeteksian deadlock menggunakan data alokasi dan permintaan resource?

3. Proses mana saja yang terlibat dalam kondisi deadlock pada dataset uji?

4. Mengapa deadlock dapat terjadi berdasarkan empat kondisi deadlock?

## Tujuan

Tujuan dari praktikum ini adalah:

1. Memahami konsep deadlock dalam sistem operasi.

2. Membuat program atau simulasi sederhana untuk mendeteksi kondisi deadlock.

3. Menjalankan pengujian menggunakan dataset proses dan resource.

4. Mengidentifikasi proses yang terlibat dalam kondisi deadlock.

5. Menganalisis hasil deteksi deadlock berdasarkan teori sistem operasi.

---
## Metode

1. Dataset Uji
Pada praktikum ini digunakan dataset sederhana yang merepresentasikan hubungan antara proses dan resource dalam sistem dengan satu instance untuk setiap resource.


| Proses | Resource Dialokasikan | Resource Diminta |
| ------ | --------------------- | ---------------- |
| P1     | R1                    | R2               |
| P2     | R2                    | R3               |
| P3     | R3                    | R1               |

Dataset ini menunjukkan bahwa setiap proses sedang memegang satu resource dan meminta resource lain yang sedang digunakan proses berbeda.

## 2. Langkah Eksperimen

Langkah-langkah yang dilakukan dalam praktikum ini adalah:

1. Menentukan daftar proses dan resource yang digunakan.
2. Memasukkan data alokasi dan permintaan resource ke dalam program/simulasi.
3. Merepresentasikan kondisi tersebut dalam bentuk **Resource Allocation Graph (RAG)**.
4. Menganalisis graf untuk mendeteksi adanya **siklus (cycle)**.
5. Menentukan apakah sistem berada dalam kondisi deadlock.
6. Mencatat proses yang terlibat dalam deadlock.
   
## 3. Metode Deteksi Deadlock

Metode yang digunakan adalah pendekatan pendeteksian siklus pada Resource Allocation Graph (RAG).

Pada sistem dengan satu instance resource, deadlock terjadi jika:

* Terdapat siklus dalam graf, dan
* Tidak ada proses yang dapat menyelesaikan eksekusi.

Siklus menunjukkan bahwa setiap proses menunggu resource yang sedang dipegang proses lain.

## 4. Parameter Pengamatan

Parameter yang diamati selama eksperimen:

* Status setiap proses (deadlock / tidak)
* Pola hubungan antar proses dan resource
* Keberadaan siklus pada graf

## 5. Implementasi Program

Program deteksi deadlock dibuat menggunakan bahasa Python dengan membaca dataset berbentuk file CSV yang berisi informasi proses, resource yang dialokasikan, dan resource yang diminta.

Program bekerja dengan pendekatan berikut:

* Membaca data proses dari file dataset_deadlock.csv.

* Menyimpan informasi alokasi dan permintaan resource tiap proses.

* Melakukan simulasi penyelesaian proses:

Jika resource yang diminta tersedia, proses dianggap selesai.

Resource yang sebelumnya dipegang proses tersebut menjadi tersedia.

Proses yang tidak pernah bisa selesai dianggap mengalami deadlock.

Berikut potongan kode utama yang digunakan:

```bash
import csv
import os

base_dir = os.path.dirname(os.path.abspath(__file__))
file_path = os.path.join(base_dir, "dataset_deadlock.csv")

processes = []
allocation = {}
request = {}

with open(file_path, "r") as file:
    reader = csv.DictReader(file)
    for row in reader:
        p = row["Process"]
        processes.append(p)
        allocation[p] = row["Allocation"]
        request[p] = row["Request"]

finished = {}
for p in processes:
    finished[p] = False

available = set()

progress = True
while progress:
    progress = False
    for p in processes:
        if not finished[p]:
            if request[p] in available:
                finished[p] = True
                available.add(allocation[p])
                progress = True

deadlock = []
for p in processes:
    if not finished[p]:
        deadlock.append(p)

print("HASIL DETEKSI DEADLOCK")
if deadlock:
    print("Deadlock terdeteksi!")
    print("Proses yang terlibat deadlock:")
    for p in deadlock:
        print("-", p)
else:
    print("Tidak terjadi deadlock.")
```

---

## Hasil 
1. Hasil Eksekusi Program
![Screenshot hasil](screenshots/week14.png)

Program dijalankan menggunakan dataset proses dan resource yang telah disiapkan. Berdasarkan hasil eksekusi, program menampilkan bahwa sistem mengalami kondisi deadlock.

Output program menunjukkan bahwa tidak ada proses yang dapat diselesaikan karena setiap proses menunggu resource yang tidak tersedia.

2. Tabel hasil deteksi
   | Proses | Resource Dialokasikan | Resource Diminta | Status   |
| ------ | --------------------- | ---------------- | -------- |
| P1     | R1                    | R2               | Deadlock |
| P2     | R2                    | R3               | Deadlock |
| P3     | R3                    | R1               | Deadlock |

3. Ringkasan Temuan

Berdasarkan hasil eksekusi:

Tidak ada proses yang berhasil menyelesaikan eksekusi.

Resource yang dibutuhkan tiap proses selalu dipegang oleh proses lain.

Program mengidentifikasi seluruh proses sebagai bagian dari deadlock.

Dengan demikian, sistem berada dalam kondisi deadlock total.


---

## Pembahasan

Berdasarkan hasil eksekusi program, seluruh proses (P1, P2, dan P3) teridentifikasi berada dalam kondisi deadlock. Hal ini terjadi karena terdapat ketergantungan siklik antar proses dalam penggunaan resource.

Secara rinci:

* **P1** memegang resource **R1** dan menunggu **R2**
* **P2** memegang resource **R2** dan menunggu **R3**
* **P3** memegang resource **R3** dan menunggu **R1**

Hubungan ini membentuk pola siklus:

**P1 → P2 → P3 → P1**

Siklus ini menyebabkan tidak ada proses yang dapat melanjutkan eksekusi, karena setiap proses menunggu resource yang sedang digunakan proses lain.

## Kesesuaian dengan Teori Deadlock

Hasil praktikum sesuai dengan teori sistem operasi bahwa deadlock terjadi jika empat kondisi berikut terpenuhi secara bersamaan.

1. Mutual Exclusion
   Resource R1, R2, dan R3 hanya dapat digunakan satu proses dalam satu waktu.

2. Hold and Wait
   Setiap proses memegang satu resource sambil menunggu resource lain.

3. No Preemption
   Resource tidak dapat diambil paksa dari proses yang sedang menggunakannya.

4. Circular Wait
   Terdapat siklus ketergantungan antar proses.

Karena keempat kondisi ini terjadi secara simultan, sistem mengalami kebuntuan permanen.

## Keterbatasan Praktikum

Simulasi hanya menggunakan contoh kecil dengan jumlah proses dan resource terbatas. Pada sistem nyata, jumlah resource lebih banyak dan deteksi deadlock lebih kompleks karena melibatkan matriks alokasi, permintaan, serta ketersediaan resource.

## Upaya Penanganan Deadlock

Deadlock dapat ditangani dengan beberapa pendekatan:

Prevention: Menghilangkan salah satu kondisi deadlock, misalnya dengan resource ordering.

Avoidance: Menggunakan algoritma seperti Banker untuk memastikan sistem tetap dalam keadaan aman.

Detection & Recovery: Mendeteksi deadlock lalu menghentikan salah satu proses atau melakukan resource preemption.

---

## Kesimpulan

Berdasarkan hasil praktikum simulasi dan deteksi deadlock, dapat disimpulkan bahwa sistem mengalami kondisi deadlock ketika seluruh proses saling menunggu resource yang sedang digunakan oleh proses lain. Pada dataset uji, proses P1, P2, dan P3 membentuk siklus ketergantungan resource sehingga tidak ada proses yang dapat menyelesaikan eksekusi.

Program yang dibuat berhasil mendeteksi kondisi deadlock dengan mengidentifikasi proses-proses yang tidak dapat diselesaikan dalam simulasi alokasi resource. Hasil ini sesuai dengan teori sistem operasi yang menyatakan bahwa deadlock terjadi apabila empat kondisi, yaitu mutual exclusion, hold and wait, no preemption, dan circular wait, terpenuhi secara bersamaan.

Praktikum ini membantu memahami bagaimana deadlock dapat terjadi, bagaimana cara mendeteksinya, serta pentingnya mekanisme pengelolaan resource dalam sistem operasi untuk mencegah kebuntuan sistem.

---
## Daftar Pustaka

Silberschatz, A., Galvin, P. B., & Gagne, G. (2018). Operating System Concepts (10th ed.). Wiley.

Tanenbaum, A. S., & Bos, H. (2015). Modern Operating Systems (4th ed.). Pearson.

Stallings, W. (2018). Operating Systems: Internals and Design Principles (9th ed.). Pearson.

## Quiz
1. Mengapa format IMRAD membantu membuat laporan praktikum lebih ilmiah dan mudah dievaluasi?
   **Jawaban:**
   
Format IMRAD membuat laporan lebih ilmiah karena menyusun isi secara sistematis seperti penelitian. Pendahuluan menjelaskan tujuan, Metode menjelaskan cara kerja sehingga bisa direplikasi, Hasil menampilkan data secara objektif, dan Pembahasan menghubungkan hasil dengan teori. Struktur ini memudahkan dosen mengevaluasi pemahaman, proses, dan hasil secara terpisah dan jelas.

2. Apa perbedaan antara bagian **Hasil** dan **Pembahasan**? 
   **Jawaban:**
   
   Hasil (Results) berisi data atau output percobaan secara objektif tanpa penjelasan panjang. Isinya fakta, seperti tabel, angka, atau hasil program.

Pembahasan (Discussion) berisi analisis dan penjelasan dari hasil tersebut. Di bagian ini dijelaskan mengapa hasil itu terjadi dan dikaitkan dengan teori.

3. Mengapa sitasi dan daftar pustaka penting, bahkan untuk laporan praktikum?
   **Jawaban:**  

Sitasi dan daftar pustaka penting karena menunjukkan bahwa laporan didasarkan pada sumber ilmiah yang terpercaya, bukan pendapat pribadi. Sitasi juga menghindari plagiarisme dengan memberi penghargaan kepada penulis asli. Selain itu, dosen dapat menilai bahwa konsep yang digunakan (seperti deadlock, algoritma deteksi, dll.) sesuai teori, serta memudahkan pembaca menelusuri referensi untuk mempelajari materi lebih lanjut.

---

## Refleksi Diri
Tuliskan secara singkat:
- Apa bagian yang paling menantang minggu ini?  
- Bagaimana cara Anda mengatasinya?  

---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
