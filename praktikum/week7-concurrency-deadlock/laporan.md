
# Laporan Praktikum Minggu 7
Topik: Sinkronisasi Proses dan Masalah Deadlock 

---

## Identitas
- **Nama**  : SASKIA ISTIQOMAH 
- **NIM**   : 250202967  
- **Kelas** : 1IKRA
---

## Tujuan
Setelah menyelesaikan tugas ini, mahasiswa mampu:
1. Mengidentifikasi empat kondisi penyebab deadlock (*mutual exclusion, hold and wait, no preemption, circular wait*).  
2. Menjelaskan mekanisme sinkronisasi menggunakan *semaphore* atau *monitor*.  
3. Menganalisis dan memberikan solusi untuk kasus deadlock.  
4. Berkolaborasi dalam tim untuk menyusun laporan analisis.  
5. Menyajikan hasil studi kasus secara sistematis. 

---

## Dasar Teori
Tuliskan ringkasan teori (3–5 poin) yang mendasari percobaan.

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



##EKSPERIMEN 1

```
import threading
import time
import random

# jumlah filsuf
N = 5

# setiap garpu = 1 lock
forks = [threading.Lock() for _ in range(N)]

def philosopher(i):
    left = i
    right = (i + 1) % N

    while True:
        print(f"Filsuf {i} sedang berpikir...")
        time.sleep(random.uniform(0.5, 1.5))

        print(f"Filsuf {i} mencoba mengambil garpu kiri {left}")
        forks[left].acquire()
        print(f"Filsuf {i} mengambil garpu kiri {left}")

        print(f"Filsuf {i} mencoba mengambil garpu kanan {right}")
        forks[right].acquire()  # <-- DI SINI DEADLOCK TERJADI
        print(f"Filsuf {i} mengambil garpu kanan {right}")

        print(f"Filsuf {i} sedang makan...")
        time.sleep(random.uniform(0.5, 1.5))

        forks[left].release()
        forks[right].release()
        print(f"Filsuf {i} selesai makan dan meletakkan garpu\n")

# Membuat thread
threads = []
for i in range(N):
    t = threading.Thread(target=philosopher, args=(i,))
    threads.append(t)
    t.start()
```

## EKSPERIMEN 2

```
import threading
import time
import random

N = 5
forks = [threading.Lock() for _ in range(N)]
mutex = threading.Semaphore(1)  # mencegah deadlock

def philosopher(i):
    left = i
    right = (i + 1) % N

    while True:
        print(f"Filsuf {i} sedang berpikir...")
        time.sleep(random.uniform(0.2, 0.6))

        mutex.acquire()  # hanya 1 filsuf yang boleh ambil garpu
        forks[left].acquire()
        forks[right].acquire()
        mutex.release()

        print(f"Filsuf {i} mulai makan...")
        time.sleep(random.uniform(0.3, 0.7))

        forks[left].release()
        forks[right].release()
        print(f"Filsuf {i} selesai makan.\n")

threads = []
for i in range(N):
    t = threading.Thread(target=philosopher, args=(i,))
    t.start()
```

```
import threading
import time
import random

N = 5
forks = [threading.Lock() for _ in range(N)]

def philosopher(i):
    left = i
    right = (i + 1) % N

    # odd = right-first, even = left-first
    first = left if i % 2 == 0 else right
    second = right if i % 2 == 0 else left

    while True:
        print(f"Filsuf {i} sedang berpikir...")
        time.sleep(random.uniform(0.2, 0.6))

        forks[first].acquire()
        forks[second].acquire()

        print(f"Filsuf {i} makan (urutan garpu dibalik)...")
        time.sleep(random.uniform(0.3, 0.7))

        forks[first].release()
        forks[second].release()
        print(f"Filsuf {i} selesai makan.\n")

threads = []
for i in range(N):
    t = threading.Thread(target=philosopher, args=(i,))
    t.start()
```

```
import threading
import time
import random

N = 5
forks = [threading.Lock() for _ in range(N)]
room = threading.Semaphore(4)   # hanya 4 boleh mencoba makan

def philosopher(i):
    left = i
    right = (i + 1) % N

    while True:
        print(f"Filsuf {i} sedang berpikir...")
        time.sleep(random.uniform(0.2, 0.6))

        room.acquire()
        forks[left].acquire()
        forks[right].acquire()

        print(f"Filsuf {i} makan...")
        time.sleep(random.uniform(0.3, 0.7))

        forks[left].release()
        forks[right].release()
        room.release()
        print(f"Filsuf {i} selesai makan.\n")

threads = []
for i in range(N):
    t = threading.Thread(target=philosopher, args=(i,))
    t.start()
```

















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
1. Analisis versi *Dining Philosophers* yang menyebabkan deadlock dan versi fixed yang bebas deadlock.  
2. Sertakan diagram atau screenshot hasil simulasi/pseudocode.  
3. Laporkan temuan penyebab deadlock dan solusi pencegahannya. 


## Quiz

1. Sebutkan empat kondisi utama penyebab deadlock.
   **Jawaban:**
   
   Empat kondisi utama (syarat) terjadinya *deadlock* menurut teori klasikal (Coffman conditions) adalah:
1. Mutual Exclusion
   Setiap resource hanya dapat digunakan oleh satu proses pada satu waktu.

2. Hold and Wait
   Proses sudah memegang satu resource dan menunggu resource lain yang sedang dipegang proses lain.

3. No Preemption
   Resource yang sedang digunakan proses tidak dapat diambil paksa; hanya dapat dilepaskan secara sukarela oleh proses tersebut.

4. Circular Wait
   Terjadi rantai proses yang saling menunggu, misalnya P1 menunggu resource yang dipegang P2, P2 menunggu resource yang dipegang P3, dan seterusnya hingga kembali ke P1.


2. Mengapa sinkronisasi diperlukan dalam sistem operasi?  
   **Jawaban:**
   
Sinkronisasi diperlukan dalam sistem operasi untuk memastikan bahwa proses atau thread yang berjalan secara bersamaan dapat mengakses resource bersama dengan aman. Tanpa sinkronisasi, kondisi seperti *race condition* dapat terjadi ketika beberapa proses mengubah data secara bersamaan sehingga menghasilkan output yang tidak dapat diprediksi. Mekanisme sinkronisasi juga menjaga konsistensi dan integritas data, mencegah terjadinya kerusakan atau ketidaksesuaian akibat akses yang tak terkoordinasi. Selain itu, sinkronisasi memungkinkan koordinasi eksekusi antar-proses, memastikan bahwa proses tertentu berjalan dalam urutan yang benar sesuai kebutuhan. Dengan penerapan sinkronisasi yang baik, sistem dapat terhindar dari *deadlock* serta memanfaatkan resource secara lebih optimal dan efisien.


3. Jelaskan perbedaan antara *semaphore* dan *monitor*
   **Jawaban:**  
**Semaphore** dan **monitor** adalah dua mekanisme sinkronisasi, tetapi keduanya memiliki konsep dan cara kerja yang berbeda secara mendasar:

Semaphore adalah struktur sinkronisasi berbasis variabel counter yang dapat memiliki nilai integer, dan penggunaannya bergantung pada operasi dasar wait (P) dan signal (V). Semaphore bersifat *low-level*, sehingga programmer harus mengatur sendiri kapan harus memanggil wait atau signal. Hal ini membuat semaphore fleksibel tetapi rawan kesalahan seperti *deadlock* atau *missed wakeup* jika urutan pemanggilan tidak tepat. Semaphore juga tidak memiliki batasan bahwa operasi harus terikat pada satu blok kode tertentu.

sebaliknya, MOnitor adalah mekanisme sinkronisasi *high-level* yang menggabungkan data, operasi, dan pengendalian akses dalam satu abstraksi. Monitor memastikan bahwa hanya satu thread yang dapat mengeksekusi fungsi di dalamnya pada satu waktu, sehingga memberikan *mutual exclusion* secara otomatis. Selain itu, monitor biasanya menggunakan *condition variable* untuk mengatur thread yang harus menunggu dan bangun pada keadaan tertentu. Karena sifatnya yang terstruktur, monitor lebih aman dan mudah digunakan dibanding semaphore, tetapi fleksibilitasnya lebih rendah.

---

## Refleksi Diri
Tuliskan secara singkat:
- Apa bagian yang paling menantang minggu ini?  
- Bagaimana cara Anda mengatasinya?  

---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
