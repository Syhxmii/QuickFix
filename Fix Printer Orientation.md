# Panduan Konfigurasi Printer di Fedora

Panduan ini menjelaskan cara menghapus printer lama, mendeteksi printer jaringan, menambahkan printer baru, serta mengatur konfigurasi **Auto Rotate** agar orientasi cetak mengikuti pengaturan aplikasi.

---

## 📋 Prasyarat

Sebelum memulai, pastikan:

* Sistem menggunakan Fedora.
* Printer dan komputer berada pada jaringan (LAN/Wi-Fi) yang sama.
* Memiliki hak akses `sudo`.
* Layanan **CUPS** sudah berjalan.

---

## 🗑 Bagian 1: Menghapus Seluruh Printer yang Terdaftar

Apabila sebelumnya sudah pernah menambahkan printer dan ingin melakukan konfigurasi dari awal, hapus seluruh printer yang terdaftar menggunakan perintah berikut:

```bash
sudo lpstat -p | awk '{print $2}' | xargs -I {} sudo lpadmin -x {}
```

> **Catatan:** Perintah ini akan menghapus semua printer yang telah terdaftar pada sistem CUPS.

---

## 🔍 Bagian 2: Mendeteksi Printer di Jaringan

Untuk melihat seluruh printer yang tersedia pada jaringan lokal, jalankan:

```bash
driverless
```

Perintah tersebut akan menampilkan daftar printer beserta alamat **IPP/IPPS** yang dapat digunakan saat proses registrasi printer.

Contoh hasil:

```text
ipps://EPSON L14150 Series._ipps._tcp.local/
```

---

## ➕ Bagian 3: Menambahkan Printer Baru

Gunakan format berikut untuk menambahkan printer yang ditemukan.

```bash
sudo lpadmin -p NAMA-PRINTER -E -v "ALAMAT_IPPS" -m everywhere
```

Keterangan:

* `-p` : Nama printer yang akan muncul di sistem.
* `-E` : Mengaktifkan printer setelah didaftarkan.
* `-v` : Alamat printer (IPP/IPPS/SMB).
* `-m everywhere` : Menggunakan driver bawaan (Driverless IPP Everywhere).

---

## 🔄 Bagian 4: Mengatur Auto Rotate

Agar orientasi cetak mengikuti pengaturan aplikasi dan tidak diputar otomatis oleh printer, jalankan:

```bash
sudo lpadmin -p NAMA_PRINTER -o orientation-requested-default=none
```

Disarankan menjalankan perintah ini setelah printer berhasil didaftarkan.

---

# 📄 Konfigurasi Printer Gedung A

## 🖨 Printer Epson L14150 – Lantai 1

Daftarkan printer:

```bash
sudo lpadmin -p Printer-A3-Lt1 -E -v "ipps://EPSON%20L14150%20Series._ipps._tcp.local/" -m everywhere
```

Atur Auto Rotate:

```bash
sudo lpadmin -p Printer-A3-Lt1 -o orientation-requested-default=none
```

---

## 🖨 Printer Epson L14150 – Lantai 2

Daftarkan printer:

```bash
sudo lpadmin -p Printer-A3-Lt2 -E -v "ipps://EPSON%20L14150%20Series-C8D481._ipps._tcp.local/" -m everywhere
```

Atur Auto Rotate:

```bash
sudo lpadmin -p Printer-A3-Lt2 -o orientation-requested-default=none
```

---

## 🖨 Printer Epson LQ-310 – Lantai 1

Printer ini menggunakan koneksi **SMB (Windows Shared Printer)** sehingga menggunakan model **raw**.

Daftarkan printer:

```bash
sudo lpadmin -p Printer-LQ310-Lt1 -E -v "smb://aiojam-16:0000@192.168.105.150/EPSONLQ-310" -m raw
```

Atur Auto Rotate:

```bash
sudo lpadmin -p Printer-LQ310-Lt1 -o orientation-requested-default=none
```

---

## ✅ Verifikasi Printer

Pastikan printer telah berhasil terdaftar dengan menjalankan:

```bash
lpstat -p
```

Untuk melihat daftar perangkat beserta alamatnya:

```bash
lpstat -v
```

Apabila printer muncul pada daftar tersebut, berarti proses konfigurasi telah berhasil.

---

## 🎉 Selesai

Seluruh printer telah berhasil dikonfigurasi pada Fedora dan siap digunakan melalui aplikasi yang mendukung sistem pencetakan CUPS.
