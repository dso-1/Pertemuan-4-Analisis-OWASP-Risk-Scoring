# Pemetaan Temuan ke OWASP Top 10 — 2021

Berdasarkan hasil analisis, berikut adalah pengelompokan kerentanan OJS ke dalam kategori OWASP:

1. **A01: Broken Access Control**
   * Temuan: IDOR pada endpoint API `/users` (VUL-004).
2. **A03: Injection**
   * Temuan: SQL Injection pada alur autentikasi (VUL-001).
   * Temuan: Reflected XSS pada kolom pencarian (VUL-003).
3. **A05: Security Misconfiguration**
   * Temuan: Header keamanan HTTP tidak diimplementasikan (VUL-005).
   * Temuan: Pesan error verbose yang menampilkan path internal server.
4. **A06: Vulnerable and Outdated Components**
   * Temuan: Penggunaan OJS v3.3.0-8 (VUL-002).
   * Temuan: Runtime PHP 7.4 yang sudah EOL (VUL-006).
