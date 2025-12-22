# Digisantuy — Situs Statis 

Ringkasan  
File `indeks.html` adalah halaman statis yang berisi landing page layanan "Digisantuy" (layanan akademik & karir). Halaman ini dibangun tanpa bundler: HTML + Tailwind via CDN + JavaScript murni (data dan interaksi di-*inline*). Cocok untuk di-publish langsung di GitHub Pages.

Fitur utama
- Daftar layanan (filter, pencarian)
- Banner promo dengan countdown
- Testimoni (slider + preview)
- FAQ interaktif
- Tombol WhatsApp untuk order/konsultasi (link sudah disiapkan)
- Responsif (Tailwind CSS)
- Fallback UX saat tidak ada hasil pencarian

Catatan penting tentang penamaan
- Nama file yang Anda punya adalah `indeks.html`. Untuk GitHub Pages agar otomatis menampilkan halaman utama, file utama harus bernama `index.html` (dengan "x"). Jika Anda tetap pakai `indeks.html` Anda akan mendapat 404 saat membuka root situs kecuali Anda:
  - Menggantinya menjadi `index.html` di root repo, atau
  - Meletakkan `indeks.html` di folder `docs/` dan konfigurasi Pages diarahkan ke folder `docs`, atau
  - Menambahkan `index.html` kecil yang melakukan redirect ke `indeks.html`.

Rekomendasi cepat: ganti nama `indeks.html` → `index.html` sebelum publish.

Persiapan & cara preview lokal
1. Simpan file sebagai `index.html` (direkomendasikan) di root repo.
2. Buka secara langsung di browser:
   - Klik dua kali file `index.html`, atau
   - Jalankan server sederhana di folder project:
     - Python 3: `python -m http.server 8000` lalu buka `http://localhost:8000`
     - Node (http-server): `npx http-server . -p 8000`

Cara publish ke GitHub Pages (cara mudah)
1. Push repository Anda ke GitHub (branch `main`/`master`).
2. Letakkan `index.html` di root repo (atau `docs/index.html` bila Anda memilih folder `docs`).
3. Buka halaman repo → Settings → Pages.
4. Pilih Source:
   - Branch: `main` (atau `master`)
   - Folder: `/ (root)` (atau `/docs`)
5. Klik Save. Tunggu beberapa menit, GitHub akan memberikan URL `https://<username>.github.io/<repo>/` (atau custom domain bila diatur).

Jika muncul 404:
- Pastikan file bernama `index.html` berada di lokasi yang benar sesuai source Pages.
- Jika Anda memakai `indeks.html`, buat file `index.html` sederhana dengan redirect ke `indeks.html`:
  ```html
  <!doctype html>
  <meta http-equiv="refresh" content="0; url=indeks.html">
  ```
  (lebih baik langsung rename jadi `index.html`)

Penyesuaian yang biasa diperlukan
- Nomor WhatsApp: ubah semua `https://wa.me/6289630181621` ke nomor Anda bila perlu.
- Konten layanan, testimoni, atau FAQ: berada di bagian data JavaScript di dalam file. Cari variabel `services`, `testimonials`, `faqs`.
- Ganti teks alamat/email/jam operasional pada footer sesuai kebutuhan.
- Jika ingin optimasi/performa lebih baik, pindahkan Tailwind ke build pipeline (Tailwind CLI / PostCSS) untuk mengurangi ukuran CSS.

Keamanan & privasi
- Saat menggunakan data klien nyata, pastikan tidak menempatkan data sensitif secara publik.
- Aplikasi statis ini tidak menyimpan data di server—semua interaksi WhatsApp membuka aplikasi WA pengguna.

Troubleshooting singkat
- Tampilan berantakan / Tailwind tidak jalan → pastikan koneksi CDN aktif dan tidak ada CSP yang memblokir.
- Gambar placeholder rusak → URL placeholder menggunakan `https://placehold.co` (periksa kebijakan hotlink atau ganti dengan gambar Anda).
- Countdown tidak muncul → tekan tombol "Lihat Semua Layanan" (fitur memicu countdown untuk promo).
