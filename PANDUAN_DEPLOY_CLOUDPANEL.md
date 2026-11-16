# PANDUAN LENGKAP DEPLOY KE CLOUDPANEL
## Landing Page "Kujang 10K Virtual Run by Budayarun"

Repositori GitHub: `git@github.com:bangnahan/kujangrun.git` / `https://github.com/bangnahan/kujangrun`

---

## 📋 Prasyarat Sebelum Deploy
1. Akses ke Dashboard **CloudPanel** VPS Anda (misal: `https://ip-server:8443`).
2. Domain / Subdomain yang sudah disiapkan (misal: `kujang10k.budayarun.com` atau `kujangrun.com`).
3. Akses DNS Manager (Cloudflare, Niagahoster, Domainesia, dll.) untuk mengarahkan domain ke IP VPS Anda.

---

## 🌐 Langkah 1: Pointing DNS Domain ke IP CloudPanel
Sebelum membuat situs di CloudPanel, arahkan DNS domain/subdomain Anda ke IP Public VPS:

1. Buka DNS Management domain Anda.
2. Tambahkan **DNS Record**:
   * **Type**: `A`
   * **Name / Host**: `@` (untuk domain utama) atau `kujang10k` (untuk subdomain)
   * **IPv4 Address**: Masukkan IP Server CloudPanel Anda (contoh: `103.xxx.xxx.xxx`)
   * **TTL**: Auto / 3600
   * **Proxy status**: Jika menggunakan Cloudflare, bisa disetel *DNS Only* terlebih dahulu agar verifikasi SSL Let's Encrypt lancar.

---

## 🛠️ Langkah 2: Buat Situs "Static HTML" di CloudPanel

1. Login ke Dashboard CloudPanel Anda.
2. Di menu sebelah kiri atau pojok kanan atas, klik tombol **+ Add Site**.
3. Pilih opsi: **Create a Static HTML Site**.
4. Isi data konfigurasi situs:
   * **Domain Name**: Masukkan nama domain Anda (contoh: `kujang10k.budayarun.com`).
   * **Site User**: Pilih user yang sudah ada (atau buat user baru, misal: `budayarun`).
   * **Site User Password**: Buat password yang kuat (simpan jika sewaktu-waktu dibutuhkan untuk SSH/SFTP).
5. Klik tombol **Create**.

---

## 🚀 Langkah 3: Deploy Kode dari GitHub ke CloudPanel

Ada dua cara untuk memasukkan file proyek ke CloudPanel:

### OPSI A (Rekomendasi): Menggunakan Git di Terminal CloudPanel / SSH
Dengan cara ini, ke depannya jika ada perubahan kode, Anda cukup menjalankan `git pull`.

1. Login SSH ke server CloudPanel Anda melalui Terminal Mac:
   ```bash
   ssh root@IP_SERVER_ANDA
   ```
2. Pindah ke direktori situs yang baru dibuat:
   ```bash
   cd /home/NAMA_SITE_USER/htdocs/DOMAIN_ANDA/
   ```
   *(Contoh: `cd /home/budayarun/htdocs/kujang10k.budayarun.com/`)*

3. Hapus file *dummy default* bawaan CloudPanel:
   ```bash
   rm -rf *
   ```

4. Clone repositori proyek:
   ```bash
   git clone https://github.com/bangnahan/kujangrun.git .
   ```
   *(Tanda titik `.` di akhir sangat penting agar file langsung diekstrak ke folder root tanpa membuat sub-folder baru).*

5. Pastikan hak akses file sesuai kepemilikan user CloudPanel:
   ```bash
   chown -R NAMA_SITE_USER:NAMA_SITE_USER /home/NAMA_SITE_USER/htdocs/DOMAIN_ANDA/
   ```

---

### OPSI B: Menggunakan File Manager di Dashboard CloudPanel
Jika tidak ingin menggunakan SSH terminal:

1. Di Dashboard CloudPanel, klik domain situs Anda.
2. Buka tab **File Manager**.
3. Masuk ke folder `/htdocs/DOMAIN_ANDA/`.
4. Hapus file `index.html` default bawaan CloudPanel.
5. Klik **Upload**:
   * Upload file `index.html`.
   * Buat folder `assets`, lalu di dalamnya buat folder `images`, dan upload ketiga file gambar:
     * `medali_kujang_poster.jpg`
     * `jersey_royal_blue.png`
     * `jersey_volt_finisher.jpg`
6. Selesai.

---

## 🔒 Langkah 4: Pasang SSL Gratis (Let's Encrypt / HTTPS)

1. Di Dashboard CloudPanel, masuk ke menu domain situs Anda.
2. Klik tab **SSL/TLS**.
3. Pilih sub-tab **Let's Encrypt**.
4. Centang nama domain Anda.
5. Klik tombol hijau **Issue and Install**.
6. Tunggu beberapa detik hingga muncul pesan sukses (*Certificate installed successfully*).
7. Sekarang situs Anda sudah aman dengan gembok hijau HTTPS resmi.

---

## ⚡ Langkah 5: Optimasi Kecepatan Nginx (Opsional tapi Disarankan)

Karena landing page ini berbasis static file murni, kita bisa mengaktifkan *browser caching* untuk aset gambar dan font agar loading ultra-cepat:

1. Di menu domain CloudPanel Anda, buka tab **Vhost (Nginx Configuration)**.
2. Pastikan atau tambahkan konfigurasi cache untuk gambar dan static assets:
   ```nginx
   location ~* \.(jpg|jpeg|png|gif|ico|webp|svg|woff2|woff)$ {
       expires 30d;
       add_header Cache-Control "public, no-transform";
       access_log off;
   }
   ```
3. Klik **Save**. Nginx akan otomatis memuat ulang konfigurasi tanpa *downtime*.

---

## 🔄 Cara Update Kode di Masa Mendatang

Jika nanti Anda mengubah harga, tanggal, atau link di komputer lokal dan sudah di-push ke GitHub:

Di server CloudPanel via SSH, cukup jalankan:
```bash
cd /home/NAMA_SITE_USER/htdocs/DOMAIN_ANDA/
git pull origin main
```
Halaman di web Anda akan langsung terupdate secara instan!
