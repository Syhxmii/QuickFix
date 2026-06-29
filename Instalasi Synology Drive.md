# Panduan Instalasi Synology Drive Client & Konfigurasi Backup

Panduan ini menjelaskan cara menginstal **Synology Drive Client** pada Fedora dan Linux Mint, kemudian melakukan konfigurasi **Backup Task** agar data penting di komputer secara otomatis tersalin ke Synology NAS.

---

## 📋 Prasyarat

Sebelum memulai, pastikan:

* Komputer telah terhubung ke jaringan yang sama dengan Synology NAS, atau memiliki akses melalui VPN/internet.
* Memiliki akun Synology Drive yang aktif.
* Mengetahui alamat IP atau hostname Synology NAS.
* Paket **Synology Drive Server** telah terpasang pada NAS.

---

# 🐧 Bagian 1: Instalasi di Fedora

Aktifkan repository COPR terlebih dahulu:

```bash
sudo dnf copr enable emixampp/synology-drive
```

Kemudian install Synology Drive Client:

```bash
sudo dnf --refresh install synology-drive
```

Tunggu hingga proses instalasi selesai.

---

# 🍃 Bagian 2: Instalasi di Linux Mint

Unduh paket installer terbaru:

```bash
wget -O synology-drive.deb "https://global.download.synology.com/download/Utility/SynologyDriveClient/latest/Ubuntu/x86_64/synology-drive-client-latest.x86_64.deb"
```

Install paket tersebut:

```bash
sudo apt install ./synology-drive.deb -y
```

Setelah selesai, aplikasi **Synology Drive Client** akan muncul pada menu aplikasi.

---

# 🚀 Bagian 3: Membuat Koneksi ke Synology NAS

1. Buka **Synology Drive Client**.
2. Klik **Start Now**.
3. Pilih **Backup Task**.
4. Masukkan informasi berikut:

   * **Server Address**: IP Address atau hostname Synology NAS.
   * **Username**: Akun Synology.
   * **Password**: Password akun Synology.
5. Klik **Next**.
6. Apabila muncul peringatan sertifikat, pilih **Trust** atau **Accept** sesuai kebijakan perusahaan.

---

# 📂 Bagian 4: Membuat Backup Task

## 1. Pilih Folder yang Akan Dibackup

Klik **Add Folder**, kemudian pilih folder yang ingin diamankan, misalnya:

* Documents
* Desktop
* Downloads
* Pictures

Klik **Next**.

---

## 2. Pilih Folder Tujuan di Synology NAS

Tentukan folder tujuan backup pada NAS.

Contoh:

```
Backup-PC
```

atau

```
Backup/Nama-Komputer
```

Klik **Next**.

---

## 3. Atur Jadwal Backup (Schedule)

Pilih **Scheduled Backup**, kemudian gunakan konfigurasi berikut:

| Pengaturan   | Nilai          |
| ------------ | -------------- |
| Schedule     | **Daily**      |
| Frequency    | **Once a day** |
| Time         | **09:00**      |
| After Backup | **When done**  |

Setelah selesai, klik **Next**.

> **Catatan:** Dengan konfigurasi ini, proses backup akan berjalan otomatis setiap hari pada pukul **09.00** dan akan selesai secara otomatis (**When done**) setelah seluruh file berhasil dibackup.

---

## 4. Konfirmasi

Periksa kembali seluruh konfigurasi, kemudian klik:

```
Done
```

Backup akan dibuat sesuai jadwal yang telah ditentukan.

---

# 🔄 Melihat Status Backup

Untuk melihat proses backup:

1. Buka **Synology Drive Client**.
2. Pilih **Backup Task**.
3. Status akan ditampilkan, misalnya:

* Syncing
* Backing Up
* Up to Date
* Error

Apabila status menunjukkan **Up to Date**, berarti seluruh file telah berhasil dibackup.

---

# ⚙️ Mengubah Konfigurasi Backup

Apabila ingin mengubah folder, jadwal, atau pengaturan lainnya:

1. Buka **Synology Drive Client**.
2. Pilih **Backup Task**.
3. Klik **Edit**.
4. Lakukan perubahan sesuai kebutuhan.
5. Simpan perubahan.

---

# 🧪 Verifikasi Backup

Pastikan file telah berhasil tersimpan di Synology NAS dengan:

1. Login ke DSM melalui browser.
2. Buka **Synology Drive** atau **File Station**.
3. Masuk ke folder tujuan backup.
4. Pastikan seluruh file telah muncul.

---

# 🎉 Selesai

Synology Drive Client telah berhasil dikonfigurasi. Dengan pengaturan di atas, backup akan berjalan **setiap hari pada pukul 09.00**, sehingga data penting di komputer akan tersimpan secara rutin di Synology NAS.
