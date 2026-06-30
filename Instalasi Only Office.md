# Panduan Instalasi ONLYOFFICE Desktop Editors & Font Microsoft di Fedora 43

Panduan ini menjelaskan cara mengunduh, menginstal **ONLYOFFICE Desktop Editors** serta **Microsoft TrueType Core Fonts** pada Fedora 43 agar dokumen Microsoft Office dapat ditampilkan dengan font yang sesuai.

---

# 📋 Prasyarat

Sebelum memulai, pastikan:

- Sistem menggunakan **Fedora 43**.
- Koneksi internet aktif.
- Memiliki hak akses `sudo`.

---

# 📥 Bagian 1: Download ONLYOFFICE Desktop Editors

1. Buka website resmi ONLYOFFICE:

   https://www.onlyoffice.com/download-desktop

2. Pilih:

- **Linux**
- **RPM (Fedora, RHEL, CentOS, OpenSUSE)**

3. Unduh paket **RPM 64-bit** sesuai versi terbaru.

Contoh nama file:

```text
onlyoffice-desktopeditors.x86_64.rpm
```

> **Catatan:** Nama file dapat berubah mengikuti versi terbaru yang tersedia di website ONLYOFFICE.

---

# 💻 Bagian 2: Install ONLYOFFICE Desktop Editors

Buka Terminal kemudian masuk ke folder tempat file RPM berada.

Misalnya:

```bash
cd ~/Downloads
```

Install menggunakan DNF:

```bash
sudo dnf install ./onlyoffice-desktopeditors.x86_64.rpm
```

Atau jika nama file berbeda:

```bash
sudo dnf install ./onlyoffice-*.rpm
```

Apabila terdapat proses konfirmasi, tekan:

```text
y
```

Tunggu hingga proses instalasi selesai.

---

# ✅ Verifikasi Instalasi

Pastikan aplikasi telah berhasil dipasang:

```bash
rpm -q onlyoffice-desktopeditors
```

Contoh hasil:

```text
onlyoffice-desktopeditors-9.x.x
```

Atau jalankan:

```bash
onlyoffice-desktopeditors
```

Atau buka melalui menu:

```
Applications
    Office
        ONLYOFFICE Desktop Editors
```

---

# 🔤 Bagian 3: Install Microsoft TrueType Fonts

Agar dokumen Word, Excel, dan PowerPoint memiliki tampilan yang sama seperti di Windows, instal font Microsoft dengan langkah berikut.

## 1. Install dependency

```bash
sudo dnf install cabextract wget fontconfig
```

---

## 2. Install Microsoft Core Fonts

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

# ⚠️ Jika Instalasi Gagal atau Muncul Pesan "Already Installed"

Apabila muncul pesan seperti:

```text
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

# ✅ Verifikasi Instalasi Font

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

# 🔄 Update ONLYOFFICE

Apabila tersedia versi RPM terbaru, cukup unduh paket terbaru kemudian jalankan:

```bash
sudo dnf install ./onlyoffice-*.rpm
```

DNF akan melakukan proses upgrade secara otomatis tanpa menghapus data pengguna.

---

# ❌ Uninstall ONLYOFFICE

Jika ingin menghapus aplikasi:

```bash
sudo dnf remove onlyoffice-desktopeditors
```

---

# 🎉 Selesai

ONLYOFFICE Desktop Editors kini telah terpasang di Fedora 43 beserta Microsoft TrueType Core Fonts sehingga kompatibilitas dokumen Microsoft Office menjadi lebih baik.