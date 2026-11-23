# Landing Page Kujang 10K Virtual Run (by Budayarun)

Landing page event virtual run bertema *Neo-Sunda Sporty* yang dirancang **khusus untuk kecepatan loading maksimal, ringan, responsif di layar smartphone**, dan siap di-deploy secara instan ke server **CloudPanel** tanpa database maupun dependensi backend yang rumit.

---

## 📁 Struktur File Proyek

```text
Kujang Virtual Run/
├── index.html                   # Halaman utama landing page (Tailwind CSS + Alpine.js)
├── PRD_KUJANG_10K.md             # Dokumen Spesifikasi Produk (PRD)
├── DESIGN_PLAN_KUJANG_10K.md     # Dokumen Rencana Desain & Wireframe
└── README.md                    # Panduan deploy & konfigurasi
```

---

## ⚙️ Cara Mengubah Link Transaksi / Registrasi

Semua tombol CTA pendaftaran (*Daftar Sekarang*, *Ambil Tiket Early Bird*, *Mobile Sticky Bar*, dll.) sudah terpusat pada satu konfigurasi di file `index.html`.

Buka file [index.html](file:///Users/bangnahan/Kujang%20Virtual%20Run/index.html), gulir ke bagian paling bawah (baris $\approx 515$), dan temukan bagian ini:

```javascript
// Ganti URL di bawah dengan link Google Form, Mayar, Loket, Midtrans, atau platform tiket Anda:
registrationUrl: 'https://larivirtual.com/events/kujang-virtual/register',
whatsappUrl: 'https://wa.me/6281916444458?text=Halo%20Admin%20Budayarun...',
```

* Cukup ganti nilai `'https://larivirtual.com/events/kujang-virtual/register'` dengan URL formulir / platform pembayaran Anda.
* Seluruh tombol pendaftaran di sekeliling halaman akan otomatis mengarah ke link baru tersebut.

---

## 🚀 Panduan Deploy di CloudPanel (Hanya 2 Menit)

CloudPanel sangat ideal untuk landing page statis karena dilayani langsung oleh Nginx pada level memori (*raw web server speed*), menghasilkan skor Google PageSpeed 95–100.

### Langkah 1: Buat Situs di CloudPanel
1. Masuk ke dashboard **CloudPanel** Anda.
2. Klik tombol **+ Add Site** di pojok kanan atas.
3. Pilih tipe: **Create a Static HTML Site**.
4. Masukkan nama domain Anda (contoh: `kujang10k.budayarun.com` atau `budayarun.com`).
5. Buat Site User atau pilih user yang sudah ada.
6. Klik **Create**.

### Langkah 2: Upload File
1. Di dashboard CloudPanel untuk domain tersebut, buka tab **File Manager**.
2. Masuk ke direktori: `/htdocs/domain-anda.com/`.
3. Upload file `index.html` langsung ke folder tersebut (atau upload file `.zip` lalu extract).
4. Pastikan file `index.html` berada tepat di dalam folder root situs tersebut.

### Langkah 3: Aktifkan SSL Gratis (HTTPS)
1. Buka tab **SSL/TLS** pada pengaturan domain di CloudPanel.
2. Pilih tab **Let's Encrypt**.
3. Centang domain Anda dan klik **Issue and Install**.
4. Selesai! Landing page Anda sekarang live dengan enkripsi HTTPS resmi dan kecepatan kilat.

---

## 💻 Cara Menjalankan & Pratinjau Lokal (Local Preview)

Jika Anda ingin melihat hasilnya di laptop Anda sebelum di-upload ke server:

### Opsi 1: Buka Langsung di Browser
Cukup klik ganda (*double click*) file `index.html`, halaman akan langsung terbuka di Google Chrome / Safari.

### Opsi 2: Jalankan Local Server via Terminal
Jalankan perintah berikut di terminal:
```bash
python3 -m http.server 8080
```
Buka browser di: [http://localhost:8080](http://localhost:8080)

---

## 🌟 Fitur Unggulan yang Sudah Aktif di Landing Page Ini:
* **Countdown Timer Real-time**: Hitung mundur dinamis menuju penutupan kuota Early Bird.
* **Showcase Medali 3D Kujang**: Ilustrasi detail medali Kujang berbahan solid zinc alloy dengan motif tradisional Sunda.
* **Interactive Tabs Rewards**: Tab interaktif untuk melihat Finisher Jersey dry-fit, Medali 3D, dan Running Pouch.
* **Modal Size Chart Interaktif**: Panduan ukuran jersey XS hingga 3XL.
* **Mobile Floating Sticky Bar**: Tombol daftar melayang otomatis saat pengunjung scroll di layar smartphone.
* **Accordion FAQ**: Tanya jawab interaktif yang rapi dan responsif.
* **Zero Database & Zero Backend Lag**: Sangat tahan menampung ribuan pengunjung serentak saat kampanye media sosial diluncurkan.

