
# Laporan Praktikum Minggu 1
Topik: Praktikum week1-intro-arsitektur-os

---

## Identitas
- **Nama**  : SASKIA ISTIQOMAH
- **NIM**   : 250202967 
- **Kelas** : 1IKRA

---

## Tujuan
memahami fungsi dasar sistem operasi dan kernel, memahami insalasi serta penggunaan WSL untuk menjalankan Linux di Windows, dan mengidentifikasi microkernel, monolitik, hybird kernel.

---

## Dasar Teori

Kernel adalah inti dari sistem operasi yang bertugas mengatur komunikasi antara perangkat keras dan perangkat lunak. Fungsi utama kernel meliputi manajemen proses, manajemen memori, manajemen file, dan manajemen perangkat I/O. Kernel bekerja dalam mode kernel (privileged mode), yang memiliki akses penuh ke seluruh sistem. Terdapat beberapa jenis kernel: monolitik (seperti Linux), microkernel, hybrid, dan exokernel.
System call menyediakan antarmuka antara aplikasi user-space dan fungsi sistem di kernel-space.Proses system call melibatkan perpindahan dari mode user ke mode kernel.Error handling penting dalam system call untuk memastikan stabilitas sistem saat terjadi kesalahan. 
 Kernel Linux dikembangkan secara kolaboratif dan tersedia di bawah lisensi GNU General Public License (GPL).  Distribusi Linux (distro) mencakup sistem lengkap yang menggabungkan kernel, library, utilitas, dan manajer paket (seperti Ubuntu, Fedora, Arch). 
Monolitik (semua fungsi dalam satu modul besar, seperti Linux). Microkernel (fungsi inti minimal, layanan lain berjalan sebagai proses terpisah). Layered dan Modular (memisahkan fungsi ke dalam lapisan/modul dengan tanggung jawab spesifik). Tujuan utama arsitektur OS adalah efisiensi, skalabilitas, dan keamanan. Komponen utama dalam arsitektur OS: manajer proses, manajer memori, sistem file, sistem I/O, dan antarmuka pengguna.

---

## Langkah Praktikum
1. Langkah-langkah yang dilakukan.  
2. Perintah yang dijalankan.  
3. File dan kode yang dibuat.  
4. Commit message yang digunakan.

---

1. **Setup Environtment**

- Pastikan Linux (Ubuntu/WSL) sudah terinstal.
   - Pastikan Git sudah dikonfigurasi dengan benar:
     ```bash
     git config --global user.name "Nama Anda"
     git config --global user.email "email@contoh.com"
     
2. **Diskusi konsep**
   - Baca materi pengantar tentang komponen OS.
   - Identifikasi komponen yang ada pada Linux/Windows/Android.

3. **Eksperimen Dasar**
   Jalankan perintah berikut di terminal:
   ```bash
   uname -a
   whoami
   lsmod | head
   dmesg | head
   ```
   Catat dan analisis modul kernel yang tampil.

---

## Hasil Eksekusi
Sertakan screenshot hasil percobaan atau diagram:
![Screenshot hasil](screenshots/example.png)
Praktikum/week1-intro-arsitektur/screenshot
Praktikum/week1-intro-arsitektur/screenshot/diagram arsitektur os.jpeg


## Analisis
- Jelaskan makna hasil percobaan.  
- Hubungkan hasil dengan teori (fungsi kernel, system call, arsitektur OS).  
- Apa perbedaan hasil di lingkungan OS berbeda (Linux vs Windows)?


*Makna hasil percobaan
  Dari hasil percobaan tersebut, dapat di peroleh bahwa instalasi WSL berhasil menciptakan lingkungan Linux di dalam sistem operasi       Windows tanpa perlu dual boot/virtual machine. Perintah yang saya coba seperti :
  ```bash
   uname -a
   whoami
   lsmod | head
   dmesg | head
   ```
   menunjukan bahwa kernel Linux aktif dan dapat berinteraksi dengan user melalui terminal. Membuktikan bahwa Windows mampu menjalankan    sistem Linux secara langsung dengan memanfaatkan lapisan hubungan kernel yang di sediakan WSl.Berikut penjelasan mengenai **makna hasil percobaan dari WSL ke Linux**, kaitannya dengan teori **fungsi kernel, system call, dan arsitektur OS**, serta **perbedaan hasil antara lingkungan OS berbeda (Linux vs Windows)**:


---

**2. Hubungan Hasil dengan Teori (Fungsi Kernel, System Call, Arsitektur OS)**

 kernel Linux mengatur langsung manajemen memori, proses, dan perangkat keras.Di wsl tidak ada kernel Linux yang sebenarnya  Windows menerjemahkan instruksi Linux ke API Windows, sehingga tidak semua fungsi kernel Linux tersedia. ada kernel Linux yang berjalan dalam VM ringan, namun tetap terisolasi dari kernel Windows. Aplikasi Linux berkomunikasi dengan kernel melalui system call. Di WSL system call Linux diterjemahkan ke dalam Windows API, yang bisa menimbulkan perbedaan hasil atau bahkan kegagalan fungsi.Hasil percobaan yang melibatkan banyak system call (misalnya, proses fork(), exec(), atau file descriptor) bisa menunjukkan kinerja lebih lambat atau hasil berbeda di WSL. Karena arsitektur berbeda, interaksi komponen (proses, memori, file system) juga berbeda, sehingga percobaan lintas platform bisa menghasilkan perilaku atau performa yang tidak identik.


**3. Perbedaan Hasil di Lingkungan OS (Linux vs Windows)**

**Menjalankan program 
multithread (pthreads)** 
linux : Hasil stabil dan dapat diamati
Windows : Bisa jalan, tapi API berbeda (WinAPI)

**Uji fork() dan exec()**
Linux : Berhasil dan efisien
Windows : Tidak tersedia – ganti dengan CreateProcess()

**File permission (chmod, chown)**
Linux : Berfungsi sesuai POSIX
Windows : Tidak berlaku(NTFS ACL berbeda)

**Shell script untuk automasi backup**
Linux : Jalankan dengan cron + bash script
Windows : Perlu adaptasi di Task scheduler + powersell

---

## Kesimpulan 
-Linux memberikan hasil percobaan yang lebih sesuai untuk studi sistem operasi karena memberikan akses langsung ke kernel, system call, dan struktur OS.
-Windows membatasi beberapa eksperimen teknis (seperti manajemen proses tingkat rendah atau device driver), dan memerlukan pendekatan berbeda untuk hal yang serupa.
-Percobaan yang berhubungan dengan kernel behavior, system call tracing, memory/proses monitoring, scripting, akan memberikan hasil yang sangat berbeda antara Linux dan Windows.Perbedaan Monolithic Kernel, Microkernel, dan Layered Architectur

## PERBEDAAN MONOLITHIC KERNEL, MICROKERNEL ,LAYERED ARCHITECTURE
- Monolithic Kernel: Semua komponen kernel (seperti driver perangkat, manajemen memori, scheduler proses, dan sistem file) diintegrasikan dalam satu ruang alamat tunggal (kernel space). Komunikasi antar-komponen cepat melalui panggilan fungsi langsung, menghasilkan performa tinggi dengan overhead rendah. Namun, kurang modular: kesalahan di satu modul bisa meruntuhkan seluruh sistem, mengurangi keamanan dan sulit untuk dikembangkan atau diperbaiki.

- Microkernel: Kernel inti sangat minimalis, hanya mencakup fungsi dasar seperti komunikasi antar-proses (IPC), manajemen thread sederhana, dan penjadwalan. Komponen lain (driver, sistem file, jaringan) berjalan sebagai proses terpisah di user space. Komunikasi via pesan, yang meningkatkan modularitas, keamanan, dan kemudahan isolasi kegagalan. Kekurangannya: overhead komunikasi tinggi, menyebabkan performa lebih lambat untuk operasi intensif.

- Layered Architecture: OS dibagi menjadi lapisan-lapisan hierarkis, di mana setiap lapisan bergantung pada lapisan bawahnya (misalnya, lapisan hardware di bawah, lapisan abstraksi tinggi di atas). Alur data vertikal, mirip model OSI. Ini menawarkan modularitas sedang dan kemudahan pemeliharaan, karena perubahan lapisan atas tidak memengaruhi yang bawah. Kekurangannya: ketergantungan ketat bisa menyebabkan bottleneck performa, dan kurang fleksibel untuk tugas parallel.

##Contoh OS Nyata yang Menggunakan Masing-Masing Model
- Monolithic Kernel: Linux (basis Ubuntu, Android, dan server seperti CentOS) adalah contoh utama, di mana modul kernel dimuat secara dinamis untuk kecepatan. FreeBSD (variasi Unix) juga monolithic, meskipun dengan elemen modular.

- Microkernel: Minix (OS pendidikan oleh Andrew Tanenbaum) murni microkernel dengan driver di user space. QNX digunakan di sistem real-time seperti otomotif (misalnya, infotainment mobil) dan medis, karena isolasi modul untuk keandalan. seL4 (keluarga L4) diterapkan di perangkat militer dan embedded untuk verifikasi keamanan formal.

- Layered Architecture: Multics (pendahuluan Unix) membagi lapisan untuk keamanan dan file system. Windows NT (dan Windows 10/11) menggunakan varian layered-hybrid, dengan Hardware Abstraction Layer (HAL) di bawah untuk portabilitas hardware. THE System (1960-an oleh Dijkstra) adalah contoh historis murni dengan enam lapisan untuk multiprogramming. Model yang Paling Relevan untuk Sistem Modern? Untuk sistem modern seperti cloud, IoT, mobile, dan AI, monolithic kernel (seperti Linux) paling relevan secara luas. Alasannya: performa tinggi mendukung skalabilitas masif (misalnya, di AWS atau Android), efisiensi energi untuk edge devices, dan ekosistem developer besar. Mitigasi keamanan modern (seperti SELinux, container Docker) mengatasi kerentanan tanpa mengorbankan kecepatan. Microkernel relevan untuk domain spesifik seperti safety-critical (mobil otonom via QNX atau drone dengan seL4), di mana isolasi absolut krusial. Dengan kemajuan hardware (multi-core,fast IPC), overheadnya berkurang, tapi belum dominan untuk penggunaan umum.Layered architecture kurang relevan hari ini, lebih cocok untuk OS lama atau embedded sederhana; digantikan hybrid (seperti Windows) yang gabungkan layered dengan monolithic. Tren masa depan: hybrid model, dengan monolithic sebagai basis dan elemen microkernel untuk keamanan di era 5G dan komputasi terdistribusi. Linux tetap "raja" karena fleksibilitas dan adopsi global.

Secara keseluruhan, perbedaan ini menunjukkan bahwa tidak ada arsitektur yang "paling baik" secara universal. Desain kernel harus disesuaikan dengan konteks penggunaan: misalnya, untuk perangkat mobile yang memerlukan keamanan, Microkernel mungkin lebih baik; sedangkan untuk komputasi berat, Monolithic Kernel lebih disukai. Di era modern, banyak sistem operasi hybrid (seperti Windows NT) yang menggabungkan elemen dari ketiganya untuk memaksimalkan manfaat.
---

##QUIZ
1. Sebutkan tiga fungsi utama sistem operasi?
   jawaban :
- Manajemen Proses: Mengelola eksekusi program, termasuk membuat, menjadwalkan, dan menghentikan proses.
- Manajemen Memori: Mengalokasikan dan memantau penggunaan memori, memastikan proses tidak saling mengganggu.
- Manajemen Perangkat (I/O Management): Menangani interaksi dengan perangkat keras seperti keyboard, mouse, disk, dll

2. Jelaskan perbedaan antara *kernel mode* dan *user mode*.
   jawaban :
   Kernel mode adalah mode operasi di sistem operasi di mana kernel (inti dari OS) menjalankan fungsi-fungsi kritis dengan akses penuh dan tidak terbatas ke semua sumber daya sistem, seperti hardware (CPU, memori, dan perangkat I/O). Dalam mode ini, kernel dapat menangani tugas-tugas penting seperti manajemen memori, penanganan interrupt, manajemen proses, dan interaksi langsung dengan perangkat keras. sedangkan User mode adalah mode operasi non-privileged dalam sistem operasi, di mana program aplikasi pengguna (seperti browser, editor teks, atau game) berjalan dengan akses terbatas ke sumber daya sistem. Ini berarti program di user mode tidak bisa langsung mengakses hardware atau fungsi kritis seperti memori atau CPU; mereka harus meminta bantuan dari kernel melalui mekanisme seperti system calls atau interrupt.

3.  Sebutkan contoh OS dengan arsitektur monolithic dan microkernel.
   jawaban :
  contoh os monolicthic kernel : Linux, Unix, Windows (versi awal)
  contoh os microkernel : Minix, QNX, Match

---

## Refleksi Diri
Tuliskan secara singkat:
- Apa bagian yang paling menantang minggu ini?  
- Bagaimana cara Anda mengatasinya?

**Bagian yang paling menantang dalam pembelajaran sistem operasi minggu ini adalah memahami perbedaan mendasar antara kernel mode dan user mode, terutama bagaimana sistem operasi mengelola hak akses dan keamanan di kedua mode tersebut. Selain itu, interaksi antara aplikasi dengan kernel melalui system call juga cukup sulit untuk saya pahami secara mendalam.**

**Untuk mengatasi tantangan ini, saya mengambil beberapa langkah, seperti membaca ulang materi dari berbagai sumber, termasuk buku teks dan artikel online yang membahas topik tersebut dengan cara yang lebih sederhana. Saya juga menonton video tutorial agar mendapatkan gambaran visual yang lebih jelas tentang proses kerja kernel dan user mode. Selain itu, saya membuat catatan dan ringkasan untuk membantu memperkuat pemahaman saya. Saya juga berdiskusi dengan teman untuk menanyakan hal-hal yang masih membingungkan.

---


**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
