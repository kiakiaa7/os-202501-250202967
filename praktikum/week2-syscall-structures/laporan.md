
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
System call didasarkan pada konsep pemisahan user mode dan kernel mode. Sistem operasi melindungi sumber daya sistem dengan membatasi akses langsung dari aplikasi ke perangkat keras. Ketika sebuah aplikasi membutuhkan layanan sistem, ia melakukan system call, yang memicu trap (sejenis interupsi perangkat lunak) untuk beralih ke mode kernel, menjalankan fungsi yang diminta, lalu kembali ke user mode.


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
![Screenshot hasil](screenshots/Screenshotstracels.png)
![Screenshot hasil](screenshots/Screenshotsyscall2.png) 
![Screenshot hasil](screenshots/Screenshotsystemcall3.png) 
![Screenshot hasil](screenshots/ScreenshotsyscallDiagram.png)



---

## Analisis
Tugas
1.Dokumentasikan hasil eksperimen strace dan dmesg dalam bentuk tabel observasi.
2.Buat diagram alur system call dari aplikasi → kernel → hardware → kembali ke aplikasi.
3.Tulis analisis 400–500 kata tentang:
-Mengapa system call penting untuk keamanan OS?
-Bagaimana OS memastikan transisi user–kernel berjalan aman?
-Sebutkan contoh system call yang sering digunakan di Linux.

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
- Apa bagian yang paling menantang minggu ini?  
- Bagaimana cara Anda mengatasinya?  

---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
