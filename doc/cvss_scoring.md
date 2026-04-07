# Kalkulasi Skor CVSS v3.1

Berikut adalah rincian perhitungan skor untuk 5 temuan kritis utama menggunakan CVSS v3.1 Vector String.

### 1. SQL Injection (VUL-001)
* **Vector String:** `CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H`
* **Base Score:** **9.8 (Critical)**
* **Penjelasan:** Serangan dapat dilakukan dari jarak jauh tanpa autentikasi dengan dampak total pada kerahasiaan, integritas, dan ketersediaan data.

### 2. Outdated OJS Version (VUL-002)
* **Vector String:** `CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:N`
* **Base Score:** **7.5 (High)**
* **Penjelasan:** Versi lama memiliki CVE terdokumentasi yang memungkinkan modifikasi data oleh penyerang luar.

### 3. Broken Access Control - IDOR (VUL-004)
* **Vector String:** `CVSS:3.1/AV:N/AC:L/PR:L/UI:N/S:U/C:H/I:L/A:N`
* **Base Score:** **7.1 (High)**
* **Penjelasan:** Pengguna terdaftar (Author) dapat mengakses data pengguna lain dengan mengubah ID pada parameter API.

### 4. Reflected XSS (VUL-003)
* **Vector String:** `CVSS:3.1/AV:N/AC:L/PR:N/UI:R/S:C/C:L/I:L/A:N`
* **Base Score:** **6.1 (Medium)**
* **Penjelasan:** Membutuhkan interaksi korban (klik link), namun dapat menyebabkan pencurian token sesi.

### 5. Security Misconfiguration (VUL-005)
* **Vector String:** `CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:L/I:N/A:N`
* **Base Score:** **5.3 (Medium)**
* **Penjelasan:** Informasi server yang bocor memudahkan penyerang memetakan vektor serangan selanjutnya.
