
# Laporan Praktikum Minggu 2
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

| No | System Call                                                         | Parameter Utama                    | Hasil / Return Value                      | Keterangan / Fungsi                                     |                                      |                                    |
| -- | ------------------------------------------------------------------- | ---------------------------------- | ----------------------------------------- | ------------------------------------------------------- | ------------------------------------ | ---------------------------------- |
| 1  | `execve("/usr/bin/ls", ["ls"], ...)`                                | Menjalankan program `/usr/bin/ls`  | `= 0`                                     | Memulai eksekusi program `ls`                           |                                      |                                    |
| 2  | `brk(NULL)`                                                         | -                                  | `= 0x59656cad7000`                        | Mengatur atau mengambil posisi akhir segmen data (heap) |                                      |                                    |
| 3  | `mmap(NULL, 8192, PROT_READ                                         | PROT_WRITE, MAP_PRIVATE            | MAP_ANONYMOUS, -1, 0)`                    | Alokasi memori anonim                                   | `= 0x7ba119567000`                   | Memetakan area memori untuk proses |
| 4  | `access("/etc/ld.so.preload", R_OK)`                                | Mengecek file preload              | `= -1 ENOENT (No such file or directory)` | File preload tidak ditemukan                            |                                      |                                    |
| 5  | `openat(AT_FDCWD, "/etc/ld.so.cache", O_RDONLY                      | O_CLOEXEC)`                        | Membuka file cache linker dinamis         | `= 3`                                                   | Berhasil membuka file cache          |                                    |
| 6  | `fstat(3, {...})`                                                   | Mengambil status file descriptor 3 | `= 0`                                     | Berhasil membaca informasi file                         |                                      |                                    |
| 7  | `mmap(NULL, 17575, PROT_READ, MAP_PRIVATE, 3, 0)`                   | Memetakan file ke memori           | `= 0x7ba119562000`                        | Digunakan oleh dynamic linker                           |                                      |                                    |
| 8  | `openat(AT_FDCWD, "/lib/x86_64-linux-gnu/libselinux.so.1", O_RDONLY | O_CLOEXEC)`                        | Membuka library selinux                   | `= 3`                                                   | Library sistem berhasil dibuka       |                                    |
| 9  | `read(3, "177ELF...", 832)`                                         | Membaca isi file library           | `= 832`                                   | Membaca header ELF dari library                         |                                      |                                    |
| 10 | `mmap(NULL, 181960, PROT_READ, MAP_PRIVATE, 3, 0)`                  | Memetakan library ke memori        | `= 0x7ba119535000`                        | Memuat library `libselinux.so.1`                        |                                      |                                    |
| 11 | `openat(AT_FDCWD, "/lib/x86_64-linux-gnu/libc.so.6", O_RDONLY       | O_CLOEXEC)`                        | Membuka library utama libc                | `= 3`                                                   | Library C standar berhasil dibuka    |                                    |
| 12 | `mmap(NULL, 2170256, PROT_READ, MAP_PRIVATE, 3, 0)`                 | Memetakan `libc.so.6` ke memori    | `= 0x7ba119228000`                        | Memuat fungsi-fungsi dasar C ke memori                  |                                      |                                    |
| 13 | `openat(AT_FDCWD, "/lib/x86_64-linux-gnu/libcpre2-8.so.0", O_RDONLY | O_CLOEXEC)`                        | Membuka library tambahan                  | `= 3`                                                   | Library regex atau C tambahan dimuat |                                    |


**Tabel observasi hasil eksperimen dmesg**
| No | Waktu (detik) | Komponen / Proses      | Pesan Log / Keterangan                                                    | Keterangan Tambahan                                          |
| -- | ------------- | ---------------------- | ------------------------------------------------------------------------- | ------------------------------------------------------------ |
| 1  | 5.137236      | `kvm_intel`            | Using Hyper-V Enlightened VMCS                                            | Sistem virtualisasi Intel KVM menggunakan fitur Hyper-V      |
| 2  | 5.276021      | `intel_rapl_msr`       | PL4 support detected                                                      | Dukungan power limit (PL4) Intel terdeteksi                  |
| 3  | 6.438310      | `WSL (217)`            | ERROR: CheckConnection: getaddrinfo() failed: -5                          | Terjadi error koneksi pada subsystem WSL                     |
| 4  | 7.206783      | `systemd-journald[43]` | Journal file uses a different sequence number ID, rotating                | File log jurnal berbeda ID, dilakukan rotasi log             |
| 5  | 24.441361     | `systemd-journald[43]` | Time jumped backwards, rotating                                           | Waktu sistem mundur, dilakukan rotasi log                    |
| 6  | 48.352914     | `hv_balloon`           | Max. dynamic memory size: 3942 MB                                         | Memori dinamis maksimum pada Hyper-V sebesar 3942 MB         |
| 7  | 48.512153     | `systemd-journald[43]` | Time jumped backwards, rotating                                           | Waktu sistem mundur kembali, rotasi log ulang                |
| 8  | 72.589832     | `systemd-journald[43]` | Time jumped backwards, rotating                                           | Waktu mundur lagi, rotasi log berulang                       |
| 9  | 189.867356    | `TCP: eth0`            | Driver has suspect GRO implementation, TCP performance may be compromised | Implementasi GRO mencurigakan, kinerja TCP mungkin terganggu |
| 10 | 646.493119    | `mini_init (201)`      | drop_caches: 1                                                            | Cache memori dibersihkan oleh sistem                         |


      

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
