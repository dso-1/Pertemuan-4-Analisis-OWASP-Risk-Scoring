# Analisis OWASP Berdasarkan Kategori Ditemukan

Analisis kualitatif detail mengenai eksploitasi kerentanan spesifik yang direkam menggunakan tool Automated/Manual, yang mempresentasikan risiko-risiko sesuai referensi top 10 OWASP Top 10 (2021).

### 1. A01 — Broken Access Control
**Temuan**: Open Redirect pada parameter `source` di endpoint login.

**Narasi dan Dampak Logis**:
Validasi endpoint masukan seperti `source` yang lengah dapat menipu pengguna. Pengguna cenderung mempercayai sebuah URL jika URL dasar berasal dari domain aplikasi yang legal (dalam konteks ini OJS). Begitu login berhasil, OJS akan mengarahkan (redirect) token/sesi ke URL berbahaya yang telah direncanakan penyerang, hal ini bisa mengakibatkan kerugian dari segi Social Engineering / Pishing.

### 2. A03 — Injection
**Temuan**: SQL Injection (Login), Parameter Exec Evaluasi/Injection di PHP (`eval()`).

**Narasi dan Dampak Logis**:
Injeksi mendominasi skala kritikal akibat kurangnya filter *input* ketat yang diterima dari sumber yang tak divalidasi. *SQL Injection* di form login berpotensi mencuri data kredensial Administrator/Editor, lalu menargetkan kerahasiaan publikasi jurnal atau komite reviewer.

### 3. A05 — Security Misconfiguration
**Temuan**: Missing HTTP Response Headers, Directory `/cache/` Browsing aktif, Exposed `/server-status` IP Private.

**Narasi dan Dampak Logis**:
Secara kuantitas, ini yang paling banyak ditemukan (Mulai dari hilangnya Header CSP hingga directory indexing aktif). 
Ini menandakan fase *deployment/hosting* OJS ini dilakukan dengan *default-stack*, dengan Apache yang belum dikonfigurasi hardening. Meskipun risikonya cenderung Medium-Low, penyerang pada fase Recon (Discovery) bisa leluasa memetakan file mana saja yang rentan. Tereksposnya file statis atau cookie API tanpa pengamanan membuat layer proteksi lain bisa diterobos dengan mudah (contoh: mencuri token OTP di log atau file `.json` *cache*).

### 4. A06 — Vulnerable and Outdated Components
**Temuan**: OS Outdated, OJS Version Exposed, Library JS (`ua-parser-js`) usang terekspos serta PHP (7.4) yg sudah tidak lagi disupport resmi keamanan.

**Narasi dan Dampak Logis**:
Pengelolaan Server *(Patch Management)* absen atau gagal terlaksana. Menjalankan PHP versi usang sangat berisiko manakala ada "0-day discovery". Penyerang tak perlu pusing membedah OJS-nya sendiri jika celah RCE sudah ada pada dependensi Library eksternalnya (contoh modul JS NPM-nya atau versi PHP itu sendiri). Dampak utama adalah infrastruktur secara kolektif (satu VM bisa disusupi).

### 5. A07 — Identification & Authentication Failures
**Temuan**: Penyimpanan Hardcoded Credentials pada source-code yang rawan terbaca oleh attacker.

**Narasi dan Dampak Logis**:
Sebuah sistem terautentikasi runtuh segera setelah "kunci rumah" tertulis di "karpet teras". Credential Hardcoding DB akan memberikan penyerang root akses mutlak di ekosistem MariaDB/MySQL jika penyerang memanfaatkan LFI / Path Traversal atau SSRF. Tanpa autentikasi ganda atau rotasi *password*, eksploitasinya bisa sulit dideteksi sejak awal.

### 6. A08 — Software and Data Integrity Failures
**Temuan**: Insecure File Upload pada FileManager OJS, tak memadainya validasi integrasi metadata unggahan. Subresource Integrity belum terpasang. 

**Narasi dan Dampak Logis**:
Aplikasi OJS merupakan jurnal berbasis submitter file (mahasiswa, eksternal reviewer) sehingga fitur utama *FileUpload Document/PDF* sangat tinggi trafficnya. Kegagalan melakukan Validasi Integritas tipe file PDF vs PHP akan menghancurkan data sistem jika Author "nakal" memutuskan mengupload File PHP Web-backdoor dan menjalankannya melalui path `/files/` jurnal tersebut.
