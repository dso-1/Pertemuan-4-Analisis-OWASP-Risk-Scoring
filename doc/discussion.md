#  Hasil Diskusi Pertemuan 4

---

### 1. Mengapa sebuah kerentanan dengan CVSS 9.8 (Critical) bisa memiliki *actual risk* yang lebih rendah dari CVSS 6.5 (Medium) dalam konteks bisnis tertentu?

**Jawaban:**
CVSS (Common Vulnerability Scoring System) mengukur **keparahan teknis (Technical Severity)** dari sebuah kerentanan (seperti vektor serangan, kompleksitas, dan dampaknya pada *Confidentiality, Integrity, Availability*). Namun, CVSS **tidak** memperhitungkan konteks bisnis.

Sedangkan *Actual Risk* (Risiko Nyata) dihitung menggunakan metrik tambahan seperti yang ada di dokumen *Risk Register*, yaitu: `Risk = Likelihood x Business Impact`.

**Contoh Kasus:**
* **Kerentanan A (CVSS 9.8 - Critical):** Ditemukan pada server *staging/testing* internal yang tidak terhubung ke internet publik dan berisi data dummy. *Business Impact*-nya sangat rendah (1). Maka *Actual Risk*-nya menjadi **Low**.
* **Kerentanan B (CVSS 6.5 - Medium):** Ditemukan pada sistem publikasi jurnal utama OJS (Production) berupa cacat logika (misalnya *Open Redirect* pada form login). Meskipun secara teknis dampaknya *Medium*, karena digunakan oleh ribuan *user* aktif dan bisa merusak reputasi universitas (Phishing), *Business Impact*-nya tinggi. Maka *Actual Risk*-nya bisa menjadi **High**.

---

### 2. Jelaskan perbedaan *CVSS Base Score*, *Temporal Score*, dan *Environmental Score*! Mana yang paling relevan untuk laporan *vulnerability assessment* institusi pendidikan?

**Jawaban:**
1.  **Base Score:** Skor dasar yang mengukur karakteristik bawaan dari kerentanan itu sendiri (seberapa mudah dieksploitasi dan seberapa besar dampak teknisnya). Skor ini konstan dan tidak berubah di berbagai lingkungan.
2.  **Temporal Score:** Menyesuaikan *Base Score* berdasarkan faktor waktu. Misalnya, apakah *exploit* publik (PoC) sudah tersebar luas, atau apakah vendor sudah merilis *patch/fix* resmi. Skor ini bisa berubah seiring berjalannya waktu.
3.  **Environmental Score:** Menyesuaikan skor berdasarkan lingkungan IT spesifik dari organisasi tersebut. Mempertimbangkan seberapa penting aset yang terancam (Asset Criticality) dan apakah ada mitigasi kompensasi (seperti WAF atau *Firewall* internal).

**Mana yang paling relevan untuk institusi pendidikan?**
Yang paling relevan adalah **Environmental Score**. Universitas memiliki prioritas aset yang unik (misalnya server pendaftaran mahasiswa dan server e-jurnal memiliki tingkat kekritisan yang berbeda). Dengan *Environmental Score*, CISO universitas bisa menurunkan prioritas *patching* untuk server riset internal, dan memfokuskan sumber daya pada sistem utama yang menyimpan data PII (Personal Identifiable Information) sivitas akademika.

---

### 3. Dalam kasus OJS, apakah A06 (Vulnerable & Outdated Components) seharusnya mendapatkan skor tinggi? Jelaskan argumen Anda!

**Jawaban:**
**Ya, sangat seharusnya mendapatkan skor tinggi.** Berdasarkan dokumen *OWASP Analysis Narrative* dan *OWASP Mapping*, OJS yang diuji menggunakan versi tertinggal (3.3.0-8) dan berjalan di atas **PHP 7.4.33** yang sudah mencapai status *End-of-Life* (EOL). 
Argumen mengapa ini sangat kritikal:
1.  **Tidak Ada Patch Keamanan:** PHP 7.4 tidak lagi menerima pembaruan keamanan. Kerentanan *Zero-day* yang ditemukan di versi ini akan menjadi "senjata abadi" bagi *attacker*.
2.  **Komponen Rentan:** Pada pemetaan (VUL-011), ditemukan library `ua-parser-js` yang memiliki CVE terkait ReDoS dengan skor CVSS 10.0 (Critical).
3.  **Dampak Sistemik:** OJS sangat bergantung pada ekosistem *framework* dan *library*. Satu komponen pihak ketiga yang *outdated* dapat menjadi pintu masuk (*entry point*) yang membuat pengamanan pada *source code* internal OJS menjadi sia-sia.

---

### 4. Seandainya Anda adalah CISO universitas yang menggunakan OJS, kerentanan mana (VUL-001 s/d VUL-010) yang akan Anda prioritaskan perbaikan pertama kali dan mengapa?

**Jawaban:**
Berdasarkan dokumen `03-risk-register.md` dan narasi analisis OWASP, prioritas perbaikan utama akan difokuskan pada:

**Prioritas 1: VUL-002 (SQL Injection pada parameter `username` login)**
* **Alasan Utama:** Menurut *Risk Register*, temuan ini memiliki skor **CVSS 9.8 (Critical)** dengan *Business Impact* Kritis (Kebocoran data) dan menempati **Prioritas 1**. 
* **Dampak:** Membiarkan SQLi di form login publik (*Authentication Bypass* / *Data Exfiltration*) berpotensi menyebabkan seluruh kredensial Administrator, Editor, dan Author tercuri. Ini akan menghancurkan kerahasiaan (*Confidentiality*) dan integritas (*Integrity*) seluruh data jurnal akademik di universitas.

**Prioritas 2: VUL-006 (Hardcoded Credentials di `config.inc.php`)**
* **Alasan Tambahan:** Memiliki skor **CVSS 9.1 (Critical)**. Jika ada kerentanan LFI (*Local File Inclusion*) atau *Directory Traversal* sekecil apa pun, *attacker* bisa membaca file `config.inc.php` ini dan langsung mendapatkan akses *root* mutlak ke dalam *database* tanpa perlu melakukan *brute-force* atau SQLi yang rumit.
