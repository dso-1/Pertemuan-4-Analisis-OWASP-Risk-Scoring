# Narasi Analisis OWASP (Berdasarkan Hasil Scan Aktual)

## A02 - Cryptographic Failures
Temuan utama pada kategori ini adalah aplikasi masih berjalan pada HTTP tanpa HTTPS. Kondisi ini meningkatkan risiko penyadapan kredensial, cookie sesi, dan data sensitif saat trafik melewati jaringan yang tidak tepercaya. Dalam konteks layanan jurnal yang melibatkan akun editor, reviewer, dan penulis, absennya TLS dapat berdampak langsung pada kerahasiaan akun dan integritas proses editorial.

Rekomendasi cepat:
- Wajibkan HTTPS penuh (redirect 301 HTTP ke HTTPS).
- Aktifkan HSTS setelah TLS stabil.

## A03 - Injection
Semgrep mendeteksi penggunaan backticks command pada komponen instalasi. Pola ini berisiko tinggi karena command shell dieksekusi langsung di level sistem operasi. Walau bukti eksploitasi remote dari input pengguna belum ditunjukkan pada data saat ini, praktik ini tetap berbahaya dan perlu refactor.

Di sisi lain, pengujian SQLMap tidak menemukan SQL Injection pada endpoint yang diuji. Artinya, untuk saat ini risiko injection lebih dominan dari aspek command execution pattern di source code dibanding SQLi terkonfirmasi.

Rekomendasi cepat:
- Hindari backticks untuk eksekusi shell.
- Gunakan API sistem yang aman dan whitelist command ketat bila benar-benar dibutuhkan.

## A05 - Security Misconfiguration
Kategori ini adalah yang paling dominan. Bukti yang ditemukan meliputi:
- Directory browsing/indexing aktif pada `/cache/`.
- Header keamanan belum lengkap (CSP, X-Frame-Options, X-Content-Type-Options).
- Cookie hardening belum optimal (HttpOnly/SameSite).
- Endpoint sensitif `/install` masih terdeteksi.

Kombinasi kelemahan konfigurasi ini memperbesar attack surface dan mempermudah fase reconnaissance penyerang sebelum eksploitasi lanjutan.

Rekomendasi cepat:
- Matikan directory listing.
- Lengkapi security headers di level web server/reverse proxy.
- Hardening cookie: HttpOnly, Secure, SameSite.
- Batasi atau nonaktifkan endpoint instalasi setelah deployment selesai.

## A06 - Vulnerable and Outdated Components
ZAP melaporkan library JavaScript rentan (ua-parser-js) dengan severity tinggi. Komponen pihak ketiga yang rentan berpotensi menjadi jalur kompromi walaupun aplikasi inti tidak memiliki bug eksploitasi langsung pada endpoint tertentu.

Rekomendasi cepat:
- Inventaris versi dependensi.
- Patch/upgrade komponen rentan.
- Terapkan proses dependency monitoring rutin.

## A08 - Software and Data Integrity Failures
Semgrep menemukan pola insecure deserialization (`unserialize`) dan ZAP melaporkan tidak adanya Subresource Integrity (SRI). Pada kasus `unserialize`, data saat ini menunjukkan kemungkinan false positive pada aliran data internal, namun tetap perlu validasi lanjutan karena pola ini secara prinsip rawan object injection jika sumber data dapat dimanipulasi.

Rekomendasi cepat:
- Audit alur data pada seluruh pemanggilan `unserialize`.
- Hindari deserialisasi object dari sumber yang tidak dipercaya.
- Tambahkan SRI untuk aset eksternal/static dependencies.

## A10 - SSRF
Pengujian SSRF untuk skenario CVE-2021-27188 tidak berhasil dieksploitasi pada lingkungan ini karena ada hambatan otorisasi dan tidak ada journal context aktif. Artinya, risiko SSRF belum tervalidasi sebagai celah aktif saat ini.

Rekomendasi cepat:
- Tetap lakukan hardening endpoint manajemen.
- Uji ulang jika konfigurasi journal context/admin berubah.

## Kesimpulan Prioritas
Prioritas remediation paling awal:
1. Patch komponen rentan (A06) dan amankan endpoint `/install`.
2. Terapkan HTTPS dan hardening konfigurasi server (A02, A05).
3. Refactor pola command execution dan audit deserialization (A03, A08).
