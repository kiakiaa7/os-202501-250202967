
# Laporan Praktikum Minggu 12
Topik: Virtualisasi Menggunakan Virtual Machine  

---

## Identitas
- **Nama**  : SASKIA ISTIQOMAH
- **NIM**   : 250202967
- **Kelas** : 1 IKRA

---

## Tujuan
Setelah menyelesaikan tugas ini, mahasiswa mampu:
1. Menginstal perangkat lunak virtualisasi (VirtualBox/VMware).  
2. Membuat dan menjalankan sistem operasi guest di dalam VM.  
3. Mengatur konfigurasi resource VM (CPU, RAM, storage).  
4. Menjelaskan mekanisme proteksi OS melalui virtualisasi.  
5. Menyusun laporan praktikum instalasi dan konfigurasi VM secara sistematis.

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
1. Apa perbedaan antara host OS dan guest OS?
   **Jawaban:**

   Host OS dan Guest OS adalah dua jenis sistem operasi yang digunakan dalam konsep virtualisasi.
Host OS merupakan sistem operasi utama yang terinstal langsung pada perangkat keras komputer dan bertugas mengelola seluruh sumber daya fisik seperti prosesor, memori, penyimpanan, dan perangkat input/output. Host OS juga menjadi platform tempat aplikasi virtualisasi (hypervisor) dijalankan.
Sementara itu, Guest OS adalah sistem operasi yang berjalan di dalam mesin virtual yang dibuat oleh hypervisor di atas Host OS. Guest OS tidak berinteraksi langsung dengan perangkat keras, melainkan menggunakan sumber daya yang dialokasikan oleh Host OS. Dengan demikian, Host OS berperan sebagai pengelola utama sistem, sedangkan Guest OS berfungsi sebagai sistem operasi tambahan yang berjalan secara terisolasi untuk keperluan tertentu, seperti pengujian aplikasi, pembelajaran, atau menjalankan sistem operasi yang berbeda dalam satu komputer.

2. Apa peran hypervisor dalam virtualisasi?
   **Jawaban:**
   
Hypervisor memiliki peran sebagai lapisan kontrol utama dalam teknologi virtualisasi yang bertanggung jawab menciptakan, menjalankan, dan mengelola mesin virtual. Hypervisor bekerja dengan mengabstraksi perangkat keras fisik sehingga dapat digunakan oleh beberapa sistem operasi secara bersamaan. Ia menentukan pembagian sumber daya seperti waktu pemrosesan CPU, kapasitas memori, ruang penyimpanan, dan akses jaringan untuk setiap Guest OS. Selain itu, hypervisor menjaga keamanan dan stabilitas sistem dengan memisahkan satu mesin virtual dari mesin virtual lainnya, sehingga kegagalan atau kesalahan pada satu Guest OS tidak memengaruhi sistem yang lain. Dengan fungsi ini, hypervisor memungkinkan pemanfaatan hardware yang lebih optimal dan mendukung efisiensi operasional dalam lingkungan virtual dan komputasi awan.

   
3. Mengapa virtualisasi meningkatkan keamanan sistem?  
   **Jawaban:**

   Virtualisasi meningkatkan keamanan sistem karena setiap sistem operasi dan aplikasi dijalankan dalam lingkungan yang terisolasi satu sama lain melalui mesin virtual. Isolasi ini membuat serangan, malware, atau kesalahan pada satu Guest OS tidak langsung menyebar ke Guest OS lain maupun ke Host OS. Selain itu, virtualisasi memungkinkan penerapan kontrol akses dan pembatasan sumber daya yang ketat, sehingga dampak dari penyalahgunaan sistem dapat diminimalkan. Fitur seperti snapshot dan rollback juga meningkatkan keamanan karena sistem dapat dengan cepat dikembalikan ke kondisi aman sebelum terjadi gangguan. Dengan demikian, virtualisasi membantu menjaga stabilitas, mencegah eskalasi serangan, dan mempermudah pemulihan sistem ketika terjadi masalah keamanan.


---

## Refleksi Diri
Tuliskan secara singkat:
- Apa bagian yang paling menantang minggu ini?  
- Bagaimana cara Anda mengatasinya?  

---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
