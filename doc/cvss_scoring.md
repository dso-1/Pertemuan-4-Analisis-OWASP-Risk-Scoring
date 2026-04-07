# Kalkulasi Skor CVSS v3.1

Berikut adalah rincian perhitungan skor untuk 5 temuan kritis utama menggunakan CVSS v3.1 Vector String.

### 1. Vulnerable JS Library (VUL-001)
* **Vector String:** `CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:N/I:N/A:H`
* **Base Score:** **7.5 (High)**
* **Penjelasan:** Kerentanan ini dapat dieksploitasi dari jarak jauh tanpa autentikasi dan tanpa interaksi pengguna. Dampak utamanya adalah pada ketersediaan sistem (Availability), misalnya melalui serangan Regular Expression Denial of Service (ReDoS) yang dapat menyebabkan aplikasi menjadi lambat atau tidak responsif. Tidak ada dampak langsung terhadap kerahasiaan (Confidentiality) maupun integritas (Integrity), namun tetap berisiko tinggi karena dapat mengganggu layanan secara signifikan.

### 2. HTTP Only Site (No HTTPS) (VUL-002)
* **Vector String:** `CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:N`
* **Base Score:** **9.1 (Critical)**
* **Penjelasan:** Aplikasi hanya menggunakan HTTP tanpa enkripsi sehingga seluruh komunikasi dapat disadap melalui serangan Man-in-the-Middle (MITM). Penyerang dapat mencuri kredensial, session cookie, dan memodifikasi data dalam transit. Dampak tinggi pada kerahasiaan dan integritas, tanpa mempengaruhi ketersediaan secara langsung.

### 3. Content Security Policy (CSP) Header Not Set (VUL-003)
* **Vector String:** `CVSS:3.1/AV:N/AC:L/PR:N/UI:R/S:C/C:H/I:H/A:N`
* **Base Score:** **8.8 (High)**
* **Penjelasan:** Tidak adanya CSP membuat aplikasi rentan terhadap serangan Cross-Site Scripting (XSS). Eksploitasi memerlukan interaksi pengguna (misalnya klik link berbahaya), namun dapat menyebabkan pencurian session, defacement, atau eksekusi script berbahaya pada browser korban. Scope berubah karena dampak meluas ke user environment.

### 4. Directory Browsing Enabled (VUL-004)
* **Vector String:** `CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:N/A:N`
* **Base Score:** **7.5 (High)**
* **Penjelasan:** Pengguna terdaftar (Author) dapat mengakses data pengguna lain dengan mengubah ID pada parameter API.

### 5. Application Error Disclosure (VUL-005)
* **Vector String:** `CVSS:3.1/AV:N/AC:L/PR:N/UI:R/S:C/C:L/I:L/A:N`
* **Base Score:** **5.3 (Medium)**
* **Penjelasan:** Pesan error aplikasi terekspos ke pengguna sehingga memberikan informasi internal seperti struktur path, query, atau konfigurasi sistem. Meskipun dampaknya terbatas, informasi ini dapat membantu penyerang melakukan eksploitasi lanjutan (information gathering untuk chaining attack).
