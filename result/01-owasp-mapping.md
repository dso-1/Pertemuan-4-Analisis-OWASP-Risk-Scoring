## Tabel Pemetaan Temuan ke OWASP Top 10

| ID Temuan | Deskripsi | Tool | OWASP | CWE | CVE |
|:---|:---|:---|:---|:---|:---|
| VUL-001 | Unsafe Use of `eval()` pada `PKPComponentRouter.inc.php` | Semgrep | **A03 — Injection** | CWE-95 | - |
| VUL-002 | SQL Injection (Time-based) pada parameter `username` login | SQLMap | **A03 — Injection** | CWE-89 | - |
| VUL-003 | Insecure File Upload — validasi tidak memadai | Semgrep | **A08 — Software & Data Integrity Failures** | CWE-434 | - |
| VUL-004 | Missing Anti-Clickjacking Header (`X-Frame-Options`) | ZAP / Nikto | **A05 — Security Misconfiguration** | CWE-1021 | - |
| VUL-005 | Exposed `/server-status` endpoint Apache | Nikto | **A05 — Security Misconfiguration** | CWE-548 | - |
| VUL-006 | Hardcoded Credentials di `config.inc.php` | Semgrep | **A07 — Identification & Authentication Failures** | CWE-798 | - |
| VUL-007 | Cookie `OJSSID` tanpa flag `HttpOnly` | ZAP / Nikto | **A05 — Security Misconfiguration** | CWE-1004 | - |
| VUL-008 | PHP 7.4.33 End-of-Life (tidak menerima patch keamanan) | Nikto | **A06 — Vulnerable & Outdated Components** | CWE-1104 | - |
| VUL-009 | OJS 3.3.0-8 versi outdated terekspos via fingerprinting | Nikto | **A06 — Vulnerable & Outdated Components** | CWE-200 | CVE-2021-27188 (SSRF) |
| VUL-010 | Content Security Policy (CSP) Header Not Set | ZAP | **A05 — Security Misconfiguration** | CWE-693 | - |
| VUL-011 | Vulnerable JS Library (`ua-parser-js`) dengan CVE ReDoS | ZAP | **A06 — Vulnerable & Outdated Components** | CWE-1395 | CVE-2020-7793 CVE-2020-7733 |
| VUL-012 | Cookie tanpa atribut `SameSite` (CSRF risk) | ZAP | **A05 — Security Misconfiguration** | CWE-352 | - |
| VUL-013 | `/install` endpoint masih tersedia (potensi reinstall) | Gobuster | **A05 — Security Misconfiguration** | CWE-16 | - |
| VUL-014 | Directory Browsing aktif pada `/cache/` | ZAP / Nikto | **A05 — Security Misconfiguration** | CWE-548 | - |
| VUL-015 | Subresource Integrity (SRI) Attribute Missing | ZAP | **A08 — Software & Data Integrity Failures** | CWE-353 | - |
| VUL-016 | Private IP Disclosure via response body | ZAP | **A05 — Security Misconfiguration** | CWE-200 | - |
| VUL-017 | Application Error Disclosure (debug info terekspos) | ZAP | **A05 — Security Misconfiguration** | CWE-209 | - |
| VUL-018 | X-Content-Type-Options Header Missing (MIME Sniffing) | ZAP | **A05 — Security Misconfiguration** | CWE-693 | - |
| VUL-019 | HTTP Only (tanpa HTTPS) — rentan MITM | ZAP | **A02 — Cryptographic Failures** | CWE-319 | - |
| VUL-020 | Open Redirect pada parameter `source` di endpoint login | Gobuster | **A01 — Broken Access Control** | CWE-601 | - |
