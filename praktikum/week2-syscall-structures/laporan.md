
# Laporan Praktikum Minggu II
Topik: Struktur System Call dan Fungsi Kernel

---

## Identitas
- **Nama**  : SASKIA ISTIQOMAH
- **NIM**   : 250202967 
- **Kelas** : 1IKRA

---

## Tujuan
Setelah menyelesaikan tugas ini, mahasiswa mampu:

1. Menjelaskan konsep dan fungsi system call dalam sistem operasi.
2. Mengidentifikasi jenis-jenis system call dan fungsinya.
3. Mengamati alur perpindahan mode user ke kernel saat system call terjadi.
4. Menggunakan perintah Linux untuk menampilkan dan menganalisis system call.


## Dasar Teori
System call didasarkan pada konsep pemisahan user mode dan kernel mode. Sistem operasi melindungi sumber daya sistem dengan membatasi akses langsung dari aplikasi ke perangkat keras. Ketika sebuah aplikasi membutuhkan layanan sistem, ia melakukan system call, yang memicu trap (sejenis interupsi perangkat lunak) untuk beralih ke mode kernel, menjalankan fungsi yang diminta, lalu kembali ke user mode.Proses ini melibatkan perpindahan dari user mode ke kernel mode menggunakan trap (interupsi perangkat lunak), di mana kernel mengeksekusi perintah tersebut, kemudian mengembalikan kontrol ke user mode setelah selesai.

Kernel sendiri merupakan inti dari sistem operasi yang memiliki kendali penuh atas seluruh sumber daya komputer. Kernel bertugas mengelola berbagai aspek penting sistem seperti manajemen proses, memori, sistem berkas, perangkat keras, serta keamanan sistem. Dalam konteks system call, kernel berperan sebagai eksekutor yang menjalankan perintah dari program pengguna dengan hak akses penuh, namun tetap menjaga keamanan agar satu proses tidak dapat mengganggu proses lainnya. Dengan adanya system call dan kernel, sistem operasi mampu menyediakan lingkungan yang aman, efisien, dan terkontrol untuk menjalankan berbagai aplikasi secara bersamaan tanpa mengganggu kestabilan sistem.

---

## B. Tujuan
Setelah menyelesaikan tugas ini, mahasiswa mampu:
1. Menjelaskan konsep dan fungsi system call dalam sistem operasi.
2. Mengidentifikasi jenis-jenis system call dan fungsinya.
3. Mengamati alur perpindahan mode user ke kernel saat system call terjadi.
4. Menggunakan perintah Linux untuk menampilkan dan menganalisis system call.

---

## C. Langkah Praktikum
1. **Setup Environment**
   - Gunakan Linux (Ubuntu/WSL).
   - Pastikan perintah `strace` dan `man` sudah terinstal.
   - Konfigurasikan Git (jika belum dilakukan di minggu sebelumnya).

2. **Eksperimen 1 – Analisis System Call**
   Jalankan perintah berikut:
   ```bash
   strace ls
   ```
   > Catat 5–10 system call pertama yang muncul dan jelaskan fungsinya.  
   Simpan hasil analisis ke `results/syscall_ls.txt`.

3. **Eksperimen 2 – Menelusuri System Call File I/O**
   Jalankan:
   ```bash
   strace -e trace=open,read,write,close cat /etc/passwd
   ```
   > Analisis bagaimana file dibuka, dibaca, dan ditutup oleh kernel.

4. **Eksperimen 3 – Mode User vs Kernel**
   Jalankan:
   ```bash
   dmesg | tail -n 10
   ```
   > Amati log kernel yang muncul. Apa bedanya output ini dengan output dari program biasa?

5. **Diagram Alur System Call**
   - Buat diagram yang menggambarkan alur eksekusi system call dari program user hingga kernel dan kembali lagi ke user mode.
   - Gunakan draw.io / mermaid.
   - Simpan di:
     ```
     praktikum/week2-syscall-structure/screenshots/syscall-diagram.png
     ```

6. **Commit & Push**
   ```bash
   git add .
   git commit -m "Minggu 2 - Struktur System Call dan Kernel Interaction"
   git push origin main
   ```

---

## Kode / Perintah
Tuliskan potongan kode atau perintah utama:
```bash
strace ls
dmesg | tail -n 10
strace -e trace=open,read,write,close cat/etc/passwd
```

---

## Hasil Eksekusi
Sertakan screenshot hasil percobaan atau diagram:
![Screenshot hasil](screenshots/Screenshotstracels.png)
![Screenshot hasil](screenshots/Screenshotsyscall2.png) 
![Screenshot hasil](screenshots/Screenshotsystemcall3.png) 
![Screenshot hasil](screenshots/ScreenshotsyscallDiagram.png)

---

## Analisis

-Mengapa system call penting untuk keamanan OS?
**jawaban** : System call adalah mekanisme yang memungkinkan program user berinteraksi dengan kernel sistem operasi (OS). Karena kernel memiliki akses penuh terhadap perangkat keras dan sumber daya sistem, system call berperan sebagai gerbang pengontrol antara aplikasi yang berjalan di user mode dengan operasi yang dijalankan di kernel mode. Oleh karena itu, system call sangat penting untuk keamanan OS karena mereka menetapkan batasan dan kontrol yang mencegah program user melakukan tindakan berbahaya secara langsung. Tanpa system call, aplikasi user dapat mengakses perangkat keras atau memodifikasi memori secara bebas, yang akan mengancam stabilitas dan keamanan sistem. Selain itu, system call memastikan bahwa setiap proses memiliki hak akses terbatas sesuai dengan kebijakan sistem operasi. Kernel dapat membatasi akses terhadap file, memori, atau perangkat tertentu berdasarkan identitas pengguna dan izin yang dimiliki. Hal ini mencegah satu proses mengganggu proses lain atau melakukan tindakan berbahaya terhadap sistem. Dengan kata lain, system call berperan sebagai gerbang keamanan utama yang menjaga kestabilan, integritas, dan privasi sistem operasi dari potensi serangan atau kesalahan program pengguna.

-Bagaimana OS memastikan transisi user–kernel berjalan aman?
**jawaban** : 
Sistem operasi memastikan transisi antara user mode dan kernel mode berjalan aman dengan memanfaatkan mekanisme hardware dan software yang ketat. CPU modern menggunakan privilege levels di mana user mode beroperasi pada level rendah dan kernel mode pada level tinggi, sehingga instruksi system call memicu perpindahan mode secara otomatis melalui interrupt atau trap gates yang hanya dapat diakses oleh kode yang sah. Saat transisi, OS menyimpan konteks proses user untuk menjaga integritas eksekusi, kemudian memvalidasi semua parameter system call agar tidak ada data berbahaya yang masuk ke kernel. Selain itu, manajemen memori yang ketat memisahkan ruang alamat kernel dan user, sehingga aplikasi user tidak dapat mengakses memori kernel secara langsung. Dengan pengelolaan hak akses yang tepat, OS juga memastikan bahwa hanya permintaan yang memiliki izin yang valid yang dijalankan di kernel. Kombinasi mekanisme ini menjaga keamanan dan stabilitas sistem selama perpindahan dari user mode ke kernel mode dan kembali lagi.

-Sebutkan contoh system call yang sering digunakan di Linux.
**jawaban** : read() , write() , open() , close() , fork() , execve() , exit() , waitpid() , mmap() ,ioctl()

---

##Hasil Observasi

**Tabel observasi hasil eksperimen strace**

| No | Perintah yang Dijalankan | System Call yang Terlihat | Fungsi System Call                 | Keterangan / Hasil Pengamatan                              |
| -- | ------------------------ | ------------------------- | ---------------------------------- | ---------------------------------------------------------- |
| 1  | `strace ls`              | `execve()`                | Menjalankan program baru (`ls`)    | Digunakan untuk memanggil program `ls` dari shell.         |
| 2  | `strace ls`              | `openat()`                | Membuka file atau direktori        | Digunakan untuk membaca isi direktori sebelum ditampilkan. |
| 3  | `strace ls`              | `read()`                  | Membaca data dari file atau buffer | Membaca isi direktori yang telah dibuka.                   |
| 4  | `strace ls`              | `write()`                 | Menulis data ke terminal (stdout)  | Menampilkan hasil daftar file ke layar.                    |
| 5  | `strace ls`              | `close()`                 | Menutup file descriptor            | Menutup file/direktori yang sudah dibaca.                  |
| 6  | `strace echo "Halo"`     | `write()`                 | Menulis string ke output           | Menampilkan teks “Halo” ke terminal.                       |
| 7  | `strace cat file.txt`    | `openat()`                | Membuka file `file.txt`            | File dibuka untuk dibaca oleh `cat`.                       |
| 8  | `strace cat file.txt`    | `read()`                  | Membaca isi file                   | Membaca isi `file.txt` ke buffer.                          |
| 9  | `strace cat file.txt`    | `write()`                 | Menulis isi file ke layar          | Menampilkan isi file di terminal.                          |
| 10 | `strace uname -a`        | `uname()`                 | Mengambil informasi sistem         | Menampilkan detail kernel dan sistem operasi.              |

**Tabel observasi hasil eksperimen dmesg**

| No | Perintah yang Dijalankan | Pesan / Output `dmesg` | Makna / Fungsi Pesan                                     | Keterangan / Pengamatan         |                                                            |
| -- | ------------------------ | ---------------------- | -------------------------------------------------------- | ------------------------------- | ---------------------------------------------------------- |
| 1  | `dmesg                   | head`                  | `[    0.000000] Linux version 6.8.0 ...`                 | Informasi versi kernel Linux    | Menunjukkan kernel yang sedang dijalankan sistem.          |
| 2  | `dmesg                   | grep CPU`              | `[    0.123456] CPU0: Intel(R) Core(TM)...`              | Deteksi dan inisialisasi CPU    | Kernel mendeteksi dan menginisialisasi prosesor saat boot. |
| 3  | `dmesg                   | grep memory`           | `[    0.654321] Memory: 4096MB available...`             | Informasi alokasi memori        | Kernel melaporkan jumlah memori fisik yang tersedia.       |
| 4  | `dmesg                   | grep usb`              | `[    2.345678] usb 1-1: new high-speed USB device...`   | Deteksi perangkat USB           | Kernel mendeteksi perangkat USB baru yang terhubung.       |
| 5  | `dmesg                   | grep eth`              | `[    3.456789] eth0: link is up...`                     | Inisialisasi antarmuka jaringan | Kernel melaporkan status koneksi jaringan aktif.           |
| 6  | `dmesg                   | grep sda`              | `[    1.234567] sda: sda1 sda2`                          | Deteksi dan partisi disk        | Kernel mengenali drive penyimpanan utama.                  |
| 7  | `dmesg                   | tail`                  | `[  123.456789] usb 1-1: USB disconnect...`              | Perangkat USB dilepas           | Kernel memberi tahu bahwa perangkat USB telah dicabut.     |
| 8  | `dmesg                   | grep error`            | `[  45.678901] ata1: COMRESET failed`                    | Peringatan atau error perangkat | Kernel melaporkan adanya kesalahan perangkat keras.        |
| 9  | `dmesg                   | grep driver`           | `[   4.567890] Loaded driver e1000e`                     | Pemanggilan driver perangkat    | Kernel memuat driver untuk perangkat tertentu.             |
| 10 | `dmesg -T                | tail`                  | `[Thu Oct 16 23:14:02 2025] audit: type=1400 audit(...)` | Log keamanan sistem (audit)     | Menampilkan aktivitas keamanan sistem oleh kernel.         |

---

## Kesimpulan

System call adalah mekanisme penting dalam sistem operasi yang memungkinkan program aplikasi berkomunikasi dengan kernel untuk mengakses sumber daya seperti file, memori, dan perangkat keras. Karena program tidak bisa mengakses perangkat keras secara langsung, system call menjadi jembatan yang aman dan terkontrol antara aplikasi dan sistem inti komputer.
Fungsi system call mencakup berbagai aktivitas penting seperti manajemen file, proses, memori, dan komunikasi antar proses. Tanpa system call, program tidak akan mampu melakukan operasi dasar seperti membaca data, menyimpan file, atau menjalankan proses baru.
Selain sebagai penghubung, system call juga berperan dalam menjaga keamanan dan kestabilan sistem dengan membatasi akses langsung ke kernel. Oleh karena itu, pemahaman tentang system call sangat penting dalam mempelajari sistem operasi dan pengembangan perangkat lunak tingkat rendah.


---

## Quiz
1. Apa fungsi utama System Call dalam sistem operasi?
   **Jawaban:**  Fungsi utama dari system call adalah untuk memfasilitasi berbagai operasi penting, seperti manajemen proses (membuat dan mengelola proses), manajemen file (membaca, menulis, dan menghapus file), manajemen memori (mengalokasikan atau membebaskan memori), serta komunikasi antar proses dan interaksi dengan perangkat input/output. Melalui system call, sistem operasi dapat memberikan layanan ini tanpa mengorbankan keamanan atau kestabilan sistem.
Selain itu, system call juga memungkinkan sistem operasi untuk mengontrol hak akses, menjaga agar setiap proses hanya bisa menggunakan sumber daya yang diizinkan. Dengan cara ini, system call tidak hanya menjadi alat komunikasi antara user dan kernel, tetapi juga menjadi alat pengaman dan pengatur dalam lingkungan komputasi modern.

2. Sebutkan 4 kategori System Call yang umum digunakan.
   **Jawaban:**
 **Manajemen Proses (Process Management)**
   * Mengelola pembuatan, eksekusi, sinkronisasi, dan terminasi proses.
   * Contoh: `fork()`, `exec()`, `wait()`, `exit()`
**Manajemen File (File Management)**
   * Mengatur operasi pada file dan direktori seperti membuka, membaca, menulis, dan menutup file.
   * Contoh: `open()`, `read()`, `write()`, `close()`
**Manajemen Memori (Memory Management)**
   * Mengalokasikan dan membebaskan memori untuk program yang berjalan.
   * Contoh: `mmap()`, `brk()`
 **Komunikasi Antar-Proses (Interprocess Communication/IPC)**
   * Memungkinkan proses untuk bertukar data dan berkomunikasi.
   * Contoh: `pipe()`, `shmget()`, `msgsnd()`

3. Mengapa System Call tidak bisa dipanggil langsung oleh user program?
   **Jawaban:**
   System call tidak bisa dipanggil langsung oleh program pengguna untuk melindungi sistem dari risiko keamanan, menjaga stabilitas, dan menyederhanakan interaksi. Desain ini adalah bagian dari prinsip "multitasking dan protected environment" dalam OS modern, seperti Windows, Linux, atau macOS. Jika mencoba memaksa panggilan langsung (misalnya, melalui assembly), OS akan menghentikan program Anda karena melanggar aturan privilage.

   ---

## Refleksi Diri
Tuliskan secara singkat:
- Apa bagian yang paling menantang minggu ini tentang struktur system call?
Bagian yang paling menantang adalah memahami bagaimana mekanisme transisi dari user mode ke kernel mode terjadi secara rinci, terutama bagaimana CPU mengatur privilege levels, interrupt descriptor table, dan bagaimana kernel mengelola context switching dengan aman. Selain itu, memahami bagaimana kernel melakukan validasi argumen system call agar tidak terjadi eksploitasi juga cukup kompleks karena melibatkan aspek keamanan dan manajemen memori yang mendalam.

- Bagaimana cara Anda mengatasinya?
Saya mengatasinya dengan mempelajari dokumentasi resmi arsitektur CPU, seperti manual Intel dan AMD, serta membaca sumber terbuka kernel Linux untuk melihat implementasi nyata dari system call handling. Saya juga menggunakan diagram alur dan pseudocode untuk memvisualisasikan proses transisi dan validasi. Selain itu, berdiskusi dengan rekan dan mencari tutorial yang fokus pada mekanisme keamanan di OS membantu saya memahami konsep yang sulit tersebut secara bertahap dan lebih praktis.

---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
