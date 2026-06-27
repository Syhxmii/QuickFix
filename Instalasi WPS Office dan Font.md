# Panduan Instalasi WPS Office & Font Microsoft di Fedora

Panduan ini menjelaskan cara mengunduh, menginstal **WPS Office** serta **Microsoft TrueType Core Fonts** pada Fedora agar dokumen Microsoft Office dapat ditampilkan dengan font yang sesuai.

---

## 📋 Prasyarat

Sebelum memulai, pastikan:

- Sistem menggunakan Fedora.
- Koneksi internet aktif.
- Memiliki hak akses `sudo`.

---

## 📥 Bagian 1: Download WPS Office

1. Buka situs resmi WPS Office untuk Linux:

   https://id.wps.com/office/linux/

2. Unduh paket **RPM 64-bit** sesuai versi terbaru yang tersedia.

3. Simpan file hasil unduhan, misalnya:

```
wps-office-11.1.0.11723.XA-1.x86_64.rpm
```

> **Catatan:** Nama file dapat berbeda tergantung versi terbaru yang tersedia di website.

---

## 💻 Bagian 2: Install WPS Office

Buka Terminal, lalu masuk ke folder tempat file RPM berada.

Jalankan perintah berikut:

```bash
sudo dnf install --nogpgcheck --setopt=tsflags=nocrypto wps-office-11.1.0.11723.XA-1.x86_64.rpm
```

> **Keterangan:**
>
> - `--nogpgcheck` digunakan untuk melewati proses verifikasi GPG.
> - `--setopt=tsflags=nocrypto` digunakan apabila sistem mengalami kendala verifikasi kriptografi saat proses instalasi.

Tunggu hingga proses instalasi selesai.

---

## 🔤 Bagian 3: Install Microsoft TrueType Fonts

Agar dokumen Word, Excel, dan PowerPoint memiliki tampilan yang sama seperti di Windows, instal font Microsoft dengan langkah berikut.

### 1. Install dependency

```bash
sudo dnf install cabextract wget fontconfig
```

---

### 2. Install Microsoft Core Fonts

```bash
sudo rpm -i --nodeps --nodigest https://downloads.sourceforge.net/project/mscorefonts2/rpms/msttcore-fonts-installer-2.6-1.noarch.rpm
```

Proses ini akan mengunduh dan memasang berbagai font Microsoft seperti:

- Arial
- Times New Roman
- Calibri (jika tersedia)
- Verdana
- Tahoma
- Courier New
- Comic Sans MS
- Georgia
- Trebuchet MS
- Webdings
- Wingdings

---

## ⚠️ Jika Instalasi Gagal atau Muncul Pesan "Already Installed"

Apabila muncul pesan seperti:

```
already installed
```

atau proses instalasi gagal karena paket sudah pernah terpasang, hapus paket installer terlebih dahulu menggunakan:

```bash
sudo rpm -e msttcore-fonts-installer
```

Setelah proses uninstall selesai, jalankan kembali perintah instalasi:

```bash
sudo rpm -i --nodeps --nodigest https://downloads.sourceforge.net/project/mscorefonts2/rpms/msttcore-fonts-installer-2.6-1.noarch.rpm
```

---

## ✅ Verifikasi Instalasi Font

Untuk memastikan font Microsoft telah berhasil dipasang, jalankan:

```bash
fc-list | grep -i "Arial"
```

atau

```bash
fc-list | grep -i "Times New Roman"
```

Jika font muncul pada daftar, berarti instalasi berhasil.

---

## 🎉 Selesai

Setelah seluruh proses selesai, buka kembali **WPS Office**. Font Microsoft seharusnya sudah tersedia dan dokumen Office akan tampil dengan lebih sesuai seperti di Windows.