
# Laporan Praktikum Minggu 3
Topik: Manajemen File dan Permission di Linux

---

## Identitas
- **Nama**  : SASKIA ISTIQOMAH
- **NIM**   : 250202967
- **Kelas** : 1IKRA

---

## Tujuan

Setelah menyelesaikan tugas ini, mahasiswa mampu:

1.Menggunakan perintah ls, pwd, cd, cat untuk navigasi file dan direktori.

2.Menggunakan chmod dan chown untuk manajemen hak akses file.

3.Menjelaskan hasil output dari perintah Linux dasar.

4.Menyusun laporan praktikum dengan struktur yang benar.

5.Mengunggah dokumentasi hasil ke Git Repository tepat waktu.

---

## Dasar Teori

Manajemen file dan permission di Linux merupakan bagian penting dari sistem operasi yang berfungsi untuk mengatur penyimpanan, pengelolaan, serta pengamanan data. Setiap file di Linux memiliki struktur izin (permission) dan identitas kepemilikan yang menentukan siapa saja yang dapat membaca, menulis, atau mengeksekusi file tersebut. Kernel berperan dalam mengatur akses file melalui sistem berkas yang terstruktur secara hierarki, dimulai dari direktori root (`/`). Dengan adanya pengaturan hak akses ini, Linux dapat menjaga keamanan sistem, mencegah penyalahgunaan data, dan memastikan setiap pengguna hanya dapat melakukan operasi sesuai dengan hak yang diberikan.

1. Manajemen file di Linux menggunakan sistem hierarki direktori dengan *root directory (`/`)* sebagai pusatnya.
2. Setiap file memiliki tiga jenis hak akses utama: *read (r)*, *write (w)*, dan *execute (x)* untuk *user*, *group*, dan *others*.
3. Pengaturan permission berperan penting dalam menjaga keamanan, keteraturan, dan integritas sistem operasi Linux.


---

## Langkah Pengerjaan
1. **Setup Environment**
   - Gunakan Linux (Ubuntu/WSL).
   - Pastikan folder kerja berada di dalam direktori repositori Git praktikum:
     ```
     praktikum/week3-linux-fs-permission/
     ```

2. **Eksperimen 1 – Navigasi Sistem File**
   Jalankan perintah berikut:
   ```bash
   pwd
   ls -l
   cd /tmp
   ls -a
   ```
   - Jelaskan hasil tiap perintah.
   - Catat direktori aktif, isi folder, dan file tersembunyi (jika ada).

3. **Eksperimen 2 – Membaca File**
   Jalankan perintah:
   ```bash
   cat /etc/passwd | head -n 5
   ```
   - Jelaskan isi file dan struktur barisnya (user, UID, GID, home, shell).

4. **Eksperimen 3 – Permission & Ownership**
   Buat file baru:
   ```bash
   echo "Hello <NAME><NIM>" > percobaan.txt
   ls -l percobaan.txt
   chmod 600 percobaan.txt
   ls -l percobaan.txt
   ```
   - Analisis perbedaan sebelum dan sesudah chmod.  
   - Ubah pemilik file (jika memiliki izin sudo):
   ```bash
   sudo chown root percobaan.txt
   ls -l percobaan.txt
   ```
   - Catat hasilnya.

5. **Eksperimen 4 – Dokumentasi**
   - Ambil screenshot hasil terminal dan simpan di:
     ```
     praktikum/week3-linux-fs-permission/screenshots/
     ```
   - Tambahkan analisis hasil pada `laporan.md`.

6. **Commit & Push**
   ```bash
   git add .
   git commit -m "Minggu 3 - Linux File System & Permission"
   git push origin main
   ```

---
## D. Tugas & Quiz
### Tugas
1. Dokumentasikan hasil seluruh perintah pada tabel observasi di `laporan.md`.  
2. Jelaskan fungsi tiap perintah dan arti kolom permission (`rwxr-xr--`).  
3. Analisis peran `chmod` dan `chown` dalam keamanan sistem Linux.  
4. Upload hasil dan laporan ke repositori Git sebelum deadline.


---

## Kode / Perintah
Tuliskan potongan kode atau perintah utama:
```pwd
ls -l
cd /tmp
ls -a```
```cat /etc/passwd | head -n 5```
```echo "Hello <NAME><NIM>" > percobaan.txt
ls -l percobaan.txt
chmod 600 percobaan.txt
ls -l percobaan.txt```
```sudo chown root percobaan.txt
ls -l percobaan.txt



