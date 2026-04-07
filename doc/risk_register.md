# Risk Register — OJS Security Assessment

Daftar risiko keamanan yang diidentifikasi pada server OJS (10.34.100.178) berdasarkan hasil pemindaian DAST dan analisis manual.

| ID | Kerentanan (Vulnerability) | Kategori OWASP | Dampak | Prioritas | Mitigasi |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **VUL-001** | SQL Injection (Auth Flow) | A03: Injection | Pengambilalihan Database | **Critical** | Implementasi Prepared Statements/Parameterized Queries. |
| **VUL-002** | OJS 3.3.0-8 (Outdated) | A06: Outdated Comp. | Eksploitasi CVE publik | **High** | Pembaruan (Patching) OJS ke versi LTS terbaru. |
| **VUL-003** | Reflected XSS (Search) | A03: Injection | Pencurian Sesi/Cookies | **Medium** | Implementasi Contextual Output Encoding. |
| **VUL-004** | IDOR pada API `/users` | A01: Broken Access | Kebocoran Data Privat | **High** | Validasi otoritas pada tingkat objek (Object-Level). |
| **VUL-005** | Missing Security Headers | A05: Misconfig. | Clickjacking/MIME Sniff | **Low** | Penambahan header CSP, X-Frame-Options, HSTS. |
| **VUL-006** | PHP 7.4 End-of-Life | A06: Outdated Comp. | Kerentanan RCE Unpatched | **High** | Migrasi ke PHP versi 8.1 atau yang lebih baru. |
