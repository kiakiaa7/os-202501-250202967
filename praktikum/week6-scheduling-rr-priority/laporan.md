
# Laporan Praktikum Minggu 6
Topik: Penjadwalan CPU – Round Robin (RR) dan Priority Scheduling

---

## Identitas
- **Nama**  : SASKIA ISTIQOMAH 
- **NIM**   : 250202967
- **Kelas** : 1IKRA

---

## Tujuan
Setelah menyelesaikan tugas ini, mahasiswa mampu:
1. Menghitung waiting time dan turnaround time pada algoritma RR dan Priority.
2. Menyusun tabel hasil perhitungan dengan benar dan sistematis.
3. Membandingkan performa algoritma RR dan Priority.
4. Menjelaskan pengaruh time quantum dan prioritas terhadap keadilan eksekusi proses.
5. Menarik kesimpulan mengenai efisiensi dan keadilan kedua algoritma.

---

## Dasar Teori

Penjadwalan CPU adalah mekanisme dalam sistem operasi yang bertugas menentukan urutan eksekusi proses yang berada dalam antrian siap (ready queue). Tujuannya adalah untuk memaksimalkan penggunaan CPU, meminimalkan waktu tunggu, serta meningkatkan efisiensi dan kinerja sistem secara keseluruhan. Salah satu algoritma penjadwalan yang paling umum digunakan adalah Round Robin (RR). Algoritma ini bersifat preemptive dan menggunakan time quantum atau jatah waktu yang sama untuk setiap proses. Proses akan dieksekusi secara bergiliran; jika waktu yang dialokasikan habis sebelum proses selesai, maka CPU akan menghentikan sementara proses tersebut dan memberikannya kembali giliran setelah semua proses lain mendapatkan jatahnya.

Round Robin memiliki karakteristik yang adil karena setiap proses memperoleh kesempatan eksekusi yang sama, sehingga cocok untuk sistem time-sharing atau sistem interaktif. Namun, ukuran quantum harus ditentukan dengan hati-hati. Quantum yang terlalu kecil dapat menyebabkan terlalu banyak context switching, sehingga meningkatkan overhead sistem, sedangkan quantum yang terlalu besar akan membuat algoritma ini berperilaku seperti First Come First Serve (FCFS).

Sementara itu, Priority Scheduling adalah algoritma penjadwalan yang memilih proses berdasarkan tingkat prioritas. Proses dengan prioritas tertinggi akan dieksekusi terlebih dahulu, baik dengan cara preemptive (menghentikan proses lain yang sedang berjalan) maupun non-preemptive (menunggu proses selesai terlebih dahulu). Algoritma ini efisien dalam menangani proses penting atau kritis, terutama dalam sistem real-time.

Namun, kelemahan utama Priority Scheduling adalah kemungkinan terjadinya starvation, yaitu kondisi di mana proses dengan prioritas rendah tidak pernah mendapat giliran eksekusi karena selalu kalah oleh proses dengan prioritas tinggi. Untuk mengatasinya, dapat digunakan teknik aging, yaitu menaikkan prioritas proses yang telah menunggu terlalu lama. Secara umum, Round Robin lebih menekankan pada keadilan waktu eksekusi, sedangkan Priority Scheduling berfokus pada pentingnya urutan eksekusi berdasarkan tingkat kepentingan proses.

---

## Langkah Praktikum
1. **Siapkan Data Proses**
   Gunakan contoh data berikut (boleh dimodifikasi sesuai kebutuhan):
   | Proses | Burst Time | Arrival Time | Priority |
   |:--:|:--:|:--:|:--:|
   | P1 | 5 | 0 | 2 |
   | P2 | 3 | 1 | 1 |
   | P3 | 8 | 2 | 4 |
   | P4 | 6 | 3 | 3 |

2. **Eksperimen 1 – Round Robin (RR)**
   - Gunakan *time quantum (q)* = 3.  
   - Hitung *waiting time* dan *turnaround time* untuk tiap proses.  
   - Simulasikan eksekusi menggunakan Gantt Chart (manual atau spreadsheet).  
     ```
     | P1 | P2 | P3 | P4 | P1 | P3 | ...
     0    3    6    9   12   15   18  ...
     ```
   - Catat sisa *burst time* tiap putaran.

3. **Eksperimen 2 – Priority Scheduling (Non-Preemptive)**
   - Urutkan proses berdasarkan nilai prioritas (angka kecil = prioritas tinggi).  
   - Lakukan perhitungan manual untuk:
     ```
     WT[i] = waktu mulai eksekusi - Arrival[i]
     TAT[i] = WT[i] + Burst[i]
     ```
   - Buat tabel perbandingan hasil RR dan Priority.

4. **Eksperimen 3 – Analisis Variasi Time Quantum (Opsional)**
   - Ubah *quantum* menjadi 2 dan 5.  
   - Amati perubahan nilai rata-rata *waiting time* dan *turnaround time*.  
   - Buat tabel perbandingan efek *quantum*.

5. **Eksperimen 4 – Dokumentasi**
   - Simpan semua hasil tabel dan screenshot ke:
     ```
     praktikum/week6-scheduling-rr-priority/screenshots/
     ```
   - Buat tabel perbandingan seperti berikut:

     | Algoritma | Avg Waiting Time | Avg Turnaround Time | Kelebihan | Kekurangan |
     |------------|------------------|----------------------|------------|-------------|
     | RR | ... | ... | Adil terhadap semua proses | Tidak efisien jika quantum tidak tepat |
     | Priority | ... | ... | Efisien untuk proses penting | Potensi *starvation* pada prioritas rendah |

6. **Commit & Push**
   ```bash
   git add .
   git commit -m "Minggu 6 - CPU Scheduling RR & Priority"
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
![Screenshot hasil](screenshots/ScreenshotWeek6.png)

## *EKSPERIMEN 1*

**Round Robin**(RR) _time quantum = 3_

| Proses | Arrival | Burst | Completion Time | Turnaround (CT - Arrival) | Waiting (TAT - Burst) |
| -----: | ------: | ----: | --------------: | ------------------------: | --------------------: |
|     P1 |       0 |     5 |              14 |                        14 |                     9 |
|     P2 |       1 |     3 |               6 |                         5 |                     2 |
|     P3 |       2 |     8 |              22 |                        20 |                    12 |
|     P4 |       3 |     6 |              20 |                        17 |                    11 |
|        |         |       |        Averange | 14                        |         8,5           |


**Simulasikan eksekusi menggunakan Gantt Chart**

```
| P1 | P2 | P3 | P4 | P1 | P3 | P4 | P3 |
0    3    6    9   12   14   17   20   22
```

**Sisa burst time tiap putaran.**

| No | Proses | Start | End | Exec (ms) |    Remaining sebelum   |    Remaining sesudah   |
| -: | :----: | ----: | --: | --------: | :--------------------: | :--------------------: |
|  1 |   P1   |     0 |   3 |         3 | P1:5, P2:3, P3:8, P4:6 | P1:2, P2:3, P3:8, P4:6 |
|  2 |   P2   |     3 |   6 |         3 | P1:2, P2:3, P3:8, P4:6 | P1:2, P2:0, P3:8, P4:6 |
|  3 |   P3   |     6 |   9 |         3 | P1:2, P2:0, P3:8, P4:6 | P1:2, P2:0, P3:5, P4:6 |
|  4 |   P4   |     9 |  12 |         3 | P1:2, P2:0, P3:5, P4:6 | P1:2, P2:0, P3:5, P4:3 |
|  5 |   P1   |    12 |  14 |         2 | P1:2, P2:0, P3:5, P4:3 | P1:0, P2:0, P3:5, P4:3 |
|  6 |   P3   |    14 |  17 |         3 | P1:0, P2:0, P3:5, P4:3 | P1:0, P2:0, P3:2, P4:3 |
|  7 |   P4   |    17 |  20 |         3 | P1:0, P2:0, P3:2, P4:3 | P1:0, P2:0, P3:2, P4:0 |
|  8 |   P3   |    20 |  22 |         2 | P1:0, P2:0, P3:2, P4:0 | P1:0, P2:0, P3:0, P4:0 |



## *Eksperimen 2*

**Priority Scheduling**

| Proses | Arrival | Burst | Start | Completion | WT = Start − Arrival | TAT = WT + Burst |
| -----: | ------: | ----: | ----: | ---------: | -------------------: | ---------------: |
|     P1 |       0 |     5 |     0 |          5 |                    0 |                5 |
|     P2 |       1 |     3 |     5 |          8 |                    4 |                7 |
|     P4 |       3 |     6 |     8 |         14 |                    5 |               11 |
|     P3 |       2 |     8 |    14 |         22 |                   12 |               20 |
|        |         |       |       | Average    | 5,24                 |         10,75    |

**Tabel Perbandingan RR dan Priority Scheduling**

| Proses | RR WT | RR TAT | RR Completion | Priority WT | Priority TAT | Priority Completion |
| -----: | ----: | -----: | ------------: | ----------: | -----------: | ------------------: |
|     P1 |     9 |     14 |            14 |           0 |            5 |                   5 |
|     P2 |     2 |      5 |             6 |           4 |            7 |                   8 |
|     P3 |    12 |     20 |            22 |          12 |           20 |                  22 |
|     P4 |    11 |     17 |            20 |           5 |           11 |                  14 |



## Eksperimen 3

**Analisis Variasi Time Quantum (Opsional)**

**Round Robin(RR)** _time quantum (q) = 2_

| Proses | Arrival | Burst | Completion | Turnaround (CT − Arrival) | Waiting (TAT − Burst) |
| -----: | ------: | ----: | ---------: | ------------------------: | --------------------: |
|     P1 |       0 |     5 |         14 |                        14 |                     9 |
|     P2 |       1 |     3 |         11 |                        10 |                     7 |
|     P3 |       2 |     8 |         22 |                        20 |                    12 |
|     P4 |       3 |     6 |         20 |                        17 |                    11 |
|        |         |       |    Averang | 15,25                     |         9,75          |


**Round Robin(RR)** _time quantum (q) = 5_

| Proses | Arrival | Burst | Completion | Turnaround (CT − Arrival) | Waiting (TAT − Burst)|
| -----: | ------: | ----: | ---------: | ---------:                | ------:              |
|     P1 |       0 |     5 |          5 |          5                |       0              |
|     P2 |       1 |     3 |          8 |          7                |       4              |
|     P3 |       2 |     8 |         21 |         19                |      11              |
|     P4 |       3 |     6 |         22 |         19                |      13              |
|        |         |       |  Averange  | 15,25                     |         9,75         |


**Tabel perbandingan efek quantum**

| Quantum | Avg Waiting Time | Avg Turnaround Time | Jumlah Slices (dispatches) | Context switches | CPU busy time | Total makespan |
| ------- | ---------------- | ------------------- |--------                    |-----             |-----          |-----           |
| **2**   | **10.75**        | **16.25**           | 12                         | 11               |22 / 22 (100%) |             22 |
| **3**   | **8.50**         | **14.00**           |8                           |                7 | 22 / 22 (100%)| 22             |
| **5**   | **7.00**         | **12.50**           |6                           | 5                | 22 / 22 (100%)| 22             |

Saya menghitung context switch sebagai jumlah perpindahan CPU dari satu proses ke proses lain. Semakin kecil quantum, semakin sering CPU memotong proses dan berpindah, sehingga jumlah context switch menjadi lebih banyak. Semakin besar quantum, proses berjalan lebih lama tanpa dipotong sehingga switching menjadi lebih sedikit. Efeknya berpengaruh langsung pada waiting time dan turnaround time.
penjelasan untuk tiap nilai quantum:


- Quantum = 2 (kecil)

Quantum kecil membuat setiap proses hanya berjalan sebentar sebelum dipotong.
Akibatnya:

- CPU berpindah-pindah sangat sering, sehingga context switch jadi paling banyak.

- Waiting time dan turnaround time menjadi paling tinggi, karena proses harus menunggu gilirannya berkali-kali.

- Cocok hanya untuk sistem yang butuh respons cepat, tetapi kurang efisien karena overhead besar.

Intinya: Quantum kecil = proses sering dipotong → banyak antrian → waktu tunggu lama.

- Quantum = 3 (menengah)

Quantum ini berada di tengah-tengah antara potongan kecil dan besar.
Efeknya:

- Jumlah context switch lebih sedikit dibanding q=2.

- Waiting time dan turnaround time lebih baik, tidak terlalu tinggi.

- Setiap proses masih mendapat giliran secara adil, tetapi overhead tidak terlalu besar.

Intinya: Seimbang — tidak terlalu sering memotong proses, tapi tetap menjaga keadilan.

- Quantum = 5 (besar)

Quantum besar membuat proses bisa berjalan cukup lama sebelum dihentikan.
Dampaknya:

- Context switch paling sedikit, sehingga overhead sangat kecil.

- Waiting time dan turnaround time menjadi yang paling rendah.

- Perilaku Round Robin mulai mirip FCFS, karena proses cenderung selesai tanpa banyak gangguan.

 Intinya: Paling efisien, tetapi keadilan sedikit berkurang karena proses awal bisa selesai duluan




## Eksperimen 4

 | Algoritma | Avg Waiting Time | Avg Turnaround Time | Kelebihan                     | Kekurangan                             |
 |-----------|------------------|---------------------|-----------                    |-------------                           |
 | RR        | 8,5              | 14                  | Adil terhadap semua proses    | Tidak efisien jika quantum tidak tepat |
 | Priority  | 5,25             | 10,75               | Efisien untuk proses penting  | Potensi *starvation* pada prioritas rendah |


---


## Kesimpulan

Dapat disimpulkan bahwa algoritma penjadwalan Priority Scheduling memberikan hasil yang paling efisien dengan rata-rata waktu tunggu sebesar 5,25 dan rata-rata turnaround time sebesar 10,75. Sementara itu, algoritma Round Robin dengan berbagai nilai time quantum menunjukkan perbedaan performa. Round Robin dengan time quantum 5 memiliki rata-rata turnaround time sebesar 12,5 dan rata-rata waktu tunggu 7, yang lebih baik dibandingkan dengan time quantum 3 (turnaround 14 dan waktu tunggu 8,5) dan time quantum 2 (turnaround 15,25 dan waktu tunggu 9,75). Hal ini menunjukkan bahwa pemilihan time quantum yang tepat pada algoritma Round Robin sangat mempengaruhi efisiensi penjadwalan, di mana time quantum yang lebih besar (q=5) dapat menghasilkan kinerja yang lebih baik dibandingkan time quantum yang lebih kecil. Secara keseluruhan, Priority Scheduling dianggap lebih optimal dalam mengurangi waktu tunggu dan turnaround dibandingkan Round Robin dengan variasi time quantum yang diuji.

---
## Tugas

1. Hitung waiting time dan turnaround time untuk algoritma RR dan Priority.

  **Round Robin(RR)** _time quantum (q) = 3_

| Proses | Arrival | Burst | Completion Time | Turnaround (CT - Arrival) | Waiting (TAT - Burst) |
| -----: | ------: | ----: | --------------: | ------------------------: | --------------------: |
|     P1 |       0 |     5 |              14 |                        14 |                     9 |
|     P2 |       1 |     3 |               6 |                         5 |                     2 |
|     P3 |       2 |     8 |              22 |                        20 |                    12 |
|     P4 |       3 |     6 |              20 |                        17 |                    11 |
|        |         |       | Average         | 14                        |         8,5           |

**Priority Scheduling (Non-Preemptive)**

| Proses | Arrival | Burst | Start | Completion | WT = Start − Arrival | TAT = WT + Burst |
| -----: | ------: | ----: | ----: | ---------: | -------------------: | ---------------: |
|     P1 |       0 |     5 |     0 |          5 |                    0 |                5 |
|     P2 |       1 |     3 |     5 |          8 |                    4 |                7 |
|     P4 |       3 |     6 |     8 |         14 |                    5 |               11 |
|     P3 |       2 |     8 |    14 |         22 |                   12 |               20 |
|        |         |       |       | Average    | 5,24                 |         10,75    |


**Round Robin(RR)** _time quantum (q) = 2_

| Proses | Arrival | Burst | Completion | Turnaround (CT − Arrival) | Waiting (TAT − Burst) |
| -----: | ------: | ----: | ---------: | ------------------------: | --------------------: |
|     P1 |       0 |     5 |         14 |                        14 |                     9 |
|     P2 |       1 |     3 |         11 |                        10 |                     7 |
|     P3 |       2 |     8 |         22 |                        20 |                    12 |
|     P4 |       3 |     6 |         20 |                        17 |                    11 |
|        |         |       | Average    | 15,25                     |         9,75          |


**Round Robin(RR)** _time quantum (q) = 5_

| Proses | Arrival | Burst | Completion | Turnaround (CT − Arrival) | Waiting (TAT − Burst)|
| -----: | ------: | ----: | ---------: | ---------:                | ------:              |
|     P1 |       0 |     5 |          5 |          5                |       0              |
|     P2 |       1 |     3 |          8 |          7                |       4              |
|     P3 |       2 |     8 |         21 |         19                |      11              |
|     P4 |       3 |     6 |         22 |         19                |      13              |
|        |         |       | Average    | 15,25                     |         9,75         |



2. Sajikan hasil perhitungan dan Gantt Chart dalam laporan.md.

RR _quantum 3_

```
| P1 | P2 | P3 | P4 | P1 | P3 | P4 | P3 |
0    3    6    9   12   14   17   20   22
```

RR _quantum 2_
```
| P1 | P2 | P3 | P1 | P4 | P2 | P3 | P1 | P4 | P3 | P4 | P3 |
0    2    4    6    8   10   11   13   14   16   18   20   22
```

RR _quantum 5_
```
| P1 | P2 | P3   | P4   | P3  | P4 |
0    5    8    13   18   21   22
```

_Priority Scheduling (Non-Preemptive)_
```
|  P1  |  P2  |   P4   |    P3    |
0      5      8        14        22
```


3. Bandingkan performa dan jelaskan pengaruh time quantum serta prioritas.

| Algoritma (konfigurasi)   | Avg Waiting Time | Avg Turnaround Time | Jumlah Slices (dispatches) | Context switches* | Makespan | Throughput (job/ms) | CPU busy time |
| ------------------------- | ---------------: | ------------------: | -------------------------: | ----------------: | -------: | ------------------: | ------------: |
| RR (q = 2)                |             9.75 |               15.25 |                         12 |                11 |       22 |     4 / 22 ≈ 0.1818 |     22 (100%) |
| RR (q = 3)                |             8.50 |               14.00 |                          8 |                 7 |       22 |              0.1818 |     22 (100%) |
| RR (q = 5)                |             7.00 |               12.50 |                          6 |                 5 |       22 |              0.1818 |     22 (100%) |
| Priority (non-preemptive) |             5.25 |               10.75 |                          4 |                 3 |       22 |              0.1818 |     22 (100%) |

**Tabel Pengaruh**

| Algoritma                 |                          Responsiveness |                             Fairness |      Overhead switching |                     Risiko starvation | Kapan direkomendasikan                                            |
| ------------------------- | --------------------------------------: | -----------------------------------: | ----------------------: | ------------------------------------: | ----------------------------------------------------------------- |
| RR (q small, e.g. 2)      | Tinggi (responsif ke proses interaktif) |       Tinggi (setiap job bergantian) |  Tinggi (banyak switch) |                                Rendah | Sistem interaktif dengan job pendek & switching murah             |
| RR (q medium, e.g. 3)     |                                Seimbang |                                 Baik |                  Sedang |                                Rendah | General-purpose time-sharing, trade-off responsivitas/overhead    |
| RR (q large, e.g. 5)      |         Lebih rendah (lebih mirip FCFS) |     Kurang (proses awal diuntungkan) |                  Rendah |                         Rendah–sedang | Kalau switching mahal atau ingin throughput/turnaround lebih baik |
| Priority (non-preemptive) | Rendah untuk job yang datang belakangan | Rendah (prioritas menentukan urutan) | Rendah (sedikit switch) | Ada kemungkinan (terutama preemptive) | Jika beberapa job jelas lebih penting (SLA/real-time soft)        |

penjelasan : 

a. Pengaruh time quantum

Pada algoritma Round Robin (RR), ukuran time quantum sangat memengaruhi cara CPU menangani setiap proses. 
- Jika quantum terlalu kecil, proses memang mendapat respon sangat cepat karena sering diputar, tetapi hal ini membuat context switching terjadi terlalu sering sehingga menambah overhead dan dapat memperpanjang waktu tunggu.
  
- Sebaliknya, quantum yang terlalu besar membuat RR menjadi kurang responsif, terutama untuk proses kecil atau proses interaktif, meskipun jumlah context switch menjadi lebih sedikit dan overhead berkurang. Dalam kondisi ini, RR mulai berperilaku seperti FCFS karena proses dapat berjalan lebih lama tanpa digantikan.
  
-  Oleh karena itu, time quantum yang ideal biasanya berada di tengah—cukup kecil untuk menjaga responsivitas, namun tidak terlalu kecil agar sistem tetap efisien dan tidak membuang waktu pada pergantian konteks yang berlebihan.

b. Pengaruh prioritas

- CPU selalu mengeksekusi proses dengan prioritas tertinggi terlebih dahulu. Akibatnya, proses yang memiliki prioritas tinggi akan memperoleh waktu eksekusi yang lebih cepat, menghasilkan waiting time dan turnaround time yang lebih baik untuk proses-proses tersebut.
  
- Namun, proses dengan prioritas rendah bisa tertunda sangat lama, terutama jika proses prioritas tinggi datang terus-menerus. Kondisi ini dapat menyebabkan starvation, yaitu proses prioritas rendah hampir tidak pernah dijalankan. Selain itu, sistem menjadi kurang “fair” karena tidak semua proses diperlakukan sama, yang menentukan cepat atau lamanya eksekusi hanyalah level prioritasnya.
  
c.  Overhead context switch

Semakin sering pergantian terjadi, semakin besar waktu yang terbuang untuk menyimpan dan memuat konteks proses. Pada algoritma seperti Round Robin dengan quantum kecil, switching terjadi sangat sering sehingga overhead meningkat dan membuat eksekusi keseluruhan jadi kurang efisien. Sementara itu, algoritma dengan pergantian proses yang lebih jarang akan memiliki overhead lebih kecil dan kinerja sistem lebih stabil.

d. Makespan & Throughput
 
Dalam simulasi tanpa memperhitungkan context switching, semua algoritma menghasilkan makespan yang sama, yaitu total waktu penyelesaian seluruh proses tetap *22 ms*, apa pun metode penjadwalannya. Karena total waktunya sama, throughput-nya juga identik, yaitu *4 proses selesai dalam 22 ms*. Dengan kata lain, jumlah proses dan total waktu penyelesaiannya tidak berubah, sehingga nilai makespan dan throughput tetap konstan. Perbedaan antar algoritma baru terlihat pada WT dan TT , karena setiap algoritma mengatur urutan eksekusi proses dengan cara yang berbeda.



---
## Quiz
1. Apa perbedaan utama antara Round Robin dan Priority Scheduling? 
   **Jawaban:**

  Perbedaan utama antara Round Robin (RR) dan Priority Scheduling terletak pada dasar pemilihan proses yang akan dieksekusi oleh CPU. Round Robin memilih proses secara bergiliran berdasarkan urutan kedatangan dan memberikan setiap proses jatah waktu eksekusi (time quantum) yang sama, sehingga lebih menekankan pada keadilan dan cocok untuk sistem time-sharing atau interaktif. 
  Sebaliknya, Priority Scheduling memilih proses berdasarkan tingkat prioritas, di mana proses dengan prioritas tertinggi akan dijalankan terlebih dahulu, baik secara preemptive maupun non-preemptive. Algoritma ini lebih efisien untuk menangani proses penting, namun dapat menyebabkan proses dengan prioritas rendah mengalami kelaparan (starvation) jika tidak diatasi dengan teknik seperti aging.

2. Apa pengaruh besar/kecilnya time quantum terhadap performa sistem?
   **Jawaban:**

   Besar atau kecilnya time quantum dalam algoritma Round Robin memiliki pengaruh yang sangat penting terhadap performa sistem. Jika time quantum terlalu kecil, maka CPU akan sering melakukan context switching (perpindahan antar proses), yang menyebabkan overhead tinggi karena waktu CPU lebih banyak digunakan untuk pergantian proses daripada eksekusi sebenarnya. Hal ini membuat sistem menjadi tidak efisien, meskipun respons terhadap proses interaktif menjadi cepat. Sebaliknya, jika time quantum terlalu besar, maka setiap proses dapat berjalan terlalu lama sebelum berganti, sehingga sistem akan berperilaku mirip dengan First Come First Serve (FCFS). Akibatnya, waktu respons untuk proses lain menjadi lebih lambat dan sistem kehilangan keadilan antar proses. Oleh karena itu, pemilihan ukuran time quantum harus seimbang cukup besar untuk mengurangi overhead, namun cukup kecil agar sistem tetap responsif.

3. Mengapa algoritma Priority dapat menyebabkan starvation?
   **Jawaban:**

   karena proses dengan prioritas rendah bisa terus-menerus tertunda eksekusinya apabila selalu ada proses baru dengan prioritas lebih tinggi yang datang ke sistem. Dalam kondisi seperti ini, proses berprioritas rendah bisa menunggu sangat lama bahkan tidak pernah dijalankan sama sekali. Dengan kata lain, starvation terjadi karena tidak adanya mekanisme pembatas waktu atau penyeimbang antara proses prioritas tinggi dan rendah. Untuk mengatasinya, sistem dapat menerapkan aging, yaitu menaikkan prioritas proses yang sudah lama menunggu agar tetap mendapat kesempatan dieksekusi dan mencegah kelaparan proses di antrian.

---

## Refleksi Diri
Tuliskan secara singkat:
- Apa bagian yang paling menantang minggu ini?  
- Bagaimana cara Anda mengatasinya?  

---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
