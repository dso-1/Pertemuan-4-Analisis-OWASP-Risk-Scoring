# Perhitungan Skor CVSS v3.1

Dokumen ini berisi perhitungan spesifik Common Vulnerability Scoring System (CVSS) v3.1 untuk 5 temuan paling kritis, sesuai dengan format yang dipelajari pada Pertemuan 4.

---

### 1. SQL Injection (Time-based) pada parameter `username` login (VUL-002)
**Skenario:** Attacker publik dapat mengeksploitasi endpoint `/index.php/index/login` menggunakan teknik time-based blind SQL injection pada parameter `username` untuk mengekstraksi data dari database (termasuk kredensial pengguna).

**Vector:** `CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H`
- **AV:N (Network)**: Serangan dilakukan via internet jarak jauh.
- **AC:L (Low)**: Tidak membutuhkan kondisi sistem yang kompleks.
- **PR:N (None)**: Form login tersedia secara publik tanpa autentikasi.
- **UI:N (None)**: Tidak perlu interaksi pengguna.
- **S:U (Unchanged)**: Kerentanan memengaruhi komponen database secara internal.
- **C:H (High)**: Bypass penuh kontrol akses data (dapat membaca semua tabel).
- **I:H (High)**: Dapat memodifikasi seluruh data.
- **A:H (High)**: Berpotensi melakukan denial of service database (misalnya DROP/LOCK).

**Base Score:** **9.8 (CRITICAL)**

**Kalkulasi:**
ISC_base = 1 - ( 1 - 0.56 ) x ( 1 - 0.56 ) x ( 1 - 0.56 ) = 0.915

ISS = 6.42 x 0.915 = 5.87 ( Scope Unchanged )

Exploitability = 8.22 x 0.85 x 0.77 x 0.85 x 0.85 = 3.89

Base Score = Roundup ( min ( 5.87 + 3.89 , 10 ) ) = 9.8

---

### 2. Vulnerable JS Library (`ua-parser-js`) — Regular Expression Denial of Service (ReDoS) (VUL-011)
**Skenario:** Attacker publik dapat mengirimkan HTTP request dengan header User-Agent yang crafted ke aplikasi (OJS). Library ua-parser-js v0.7.7 akan memproses input tersebut menggunakan regex yang rentan, menyebabkan CPU spike dan aplikasi menjadi tidak responsif (Denial of Service)

**Vector:** `CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:N/I:N/A:H`
- **AV:N (Network)**: Serangan dilakukan melalui HTTP request (jarak jauh).
- **AC:L (Low)**: Tidak butuh kondisi khusus, cukup kirim payload regex tertentu.
- **PR:N (None)**: Tidak perlu login (User-Agent selalu diproses server).
- **UI:N (None)**: Tidak butuh interaksi user.
- **S:U (Unchanged)**: Dampak hanya pada komponen yang sama (server aplikasi).
- **C:N (None)**: Tidak ada kebocoran data.
- **I:N (None)**: Tidak ada perubahan data.
- **A:H (High)**: Server bisa hang / CPU 100% → layanan down.

**Base Score:** **10.0 (CRITICAL)**

**Kalkulasi:**
ISC_base = 1 - ( 1 - 0.56 ) x ( 1 - 0.56 ) x ( 1 - 0.56 ) = 0.915

ISS = 6.42 x 0.56 = 3.59

Exploitability = 8.22 x 0.85 x 0.77 x 0.85 x 0.85 = 3.89

Base Score = Roundup ( 3.59 + 3.89 ) = 7.5

---

### 3. Insecure File Upload pada `FileManager.inc.php` (VUL-003)
**Skenario:** Aplikasi tidak mem-validasi ekstensi file secara ketat di backend, memungkinkan aktor dengan peran minimal (seperti Author) mengunggah file berbahaya (misalnya `.php`) dan mengeksekusinya.

**Vector:** `CVSS:3.1/AV:N/AC:L/PR:L/UI:N/S:U/C:H/I:H/A:H`
- **AV:N (Network)**: via web interface.
- **AC:L (Low)**: Script upload web shell bersifat umum.
- **PR:L (Low)**: Memerlukan akses setidaknya Author untuk mencapai fitur upload file.
- **UI:N (None)**: Tidak membutuhkan partisipasi admin.
- **S:U (Unchanged)**: Tetap dalam scope *web application stack*.
- **C:H (High)**: Shell menyediakan akses penuh ke sistem file dan DB (via config config.inc.php).
- **I:H (High)**: Shell dapat mengubah, menghapus, backdooring sistem.
- **A:H (High)**: Attacker dapat menghapus semua file (Denial of service via web shell).

**Base Score:** **8.8 (HIGH)**

**Kalkulasi:**
ISC_base = 1 - ( 1 - 0.56 ) x ( 1 - 0.56 ) x ( 1 - 0.56 ) = 0.915

ISS = 6.42 x 0.915 = 5.87 ( Scope Unchanged )

Exploitability = 8.22 x 0.85 x 0.77 x 0.62 x 0.85 = 2.83

Base Score = Roundup ( min ( 5.87 + 2.83 , 10 ) ) = 8.8

---

### 4. Hardcoded Credentials DB di `config.inc.php` (VUL-006)
**Skenario:** Kredensial *database* disimpan dalam format *plain text* pada `config.inc.php`. Kombinasikan dengan directory misconfiguration/Path Traversal (jika terekspos), penyerang akan mendapatkan akses masuk langsung ke database.

**Vector:** `CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:N` *(Asumsi dibaca secara eksternal karena miskonfigurasi directory)*
- **AV:N (Network)**: Diakses melalui remote.
- **AC:L (Low)**: Plain text, tidak ada rintangan enkripsi.
- **PR:N (None)**: Jika didapatkan via kerentanan lain/exposed path, tanpa login.
- **UI:N (None)**: Tanpa interaksi sistem lain.
- **S:U (Unchanged)**: Tidak mengubah komponen otoritatif dari dalam.
- **C:H (High)**: Total kompromi atas seluruh kerahasiaan isi database.
- **I:H (High)**: Mampu melakukan write menggunakan DB credential yang ter-leak.
- **A:N (None)**: Leaking ini saja tidak membuat down aplikasi sebelum attacker mengeksekusinya.

**Base Score:** **9.1 (CRITICAL)**

**Kalkulasi:**
ISC_base = 1 - ( 1 - 0.56 ) x ( 1 - 0.56 ) x ( 1 - 0 ) = 0.806

ISS = 6.42 x 0.806 = 5.17 ( Scope Unchanged )

Exploitability = 8.22 x 0.85 x 0.77 x 0.85 x 0.85 = 3.89

Base Score = Roundup ( min ( 5.17 + 3.89 , 10 ) ) = 9.1

---

### 5. Open Redirect pada parameter `source` (VUL-020)
**Skenario:** Input parameter `source` di endpoint login dipercaya oleh aplikasi OJS tanpa validasi yang layak. Penyerang dapat membuat link phising yang mengarahkan pengguna yang sukses login menuju situs berbahaya di luar domain kampus.

**Vector:** `CVSS:3.1/AV:N/AC:L/PR:N/UI:R/S:C/C:L/I:L/A:N`
- **AV:N (Network)**: Lewat URL jarak jauh.
- **AC:L (Low)**: Penyerang cukup membuat URL biasa (contoh: `source=http://malicious.com`).
- **PR:N (None)**: Semua orang dapat mengirimkan URL berbahaya.
- **UI:R (Required)**: Korban perlu mengklik tautan tersebut.
- **S:C (Changed)**: Dampak dirasakan ketika korban terarah ke infrastruktur eksternal penyerang.
- **C:L (Low)**: Memungkinkan credential harvesting bila pishing meyakinkan.
- **I:L (Low)**: Integritas aplikasi tidak termodifikasi, tapi user perception tertipu.
- **A:N (None)**: Tidak memberikan dampak denial of service.

**Base Score:** **6.1 (MEDIUM)**

**Kalkulasi:**
ISC_base = 1 - ( 1 - 0.22 ) x ( 1 - 0.22 ) x ( 1 - 0 ) = 0.392

ISS = 7.52 x [ 0.392 - 0.029 ] = 2.73 ( Scope Changed ⇒ x 1.08 )

Exploitability = 8.22 x 0.85 x 0.77 x 0.85 x 0.62 = 2.83

Base Score = Roundup ( min ( 1.08 x ( 2.73 + 2.83 ) , 10 ) ) = 6.1
