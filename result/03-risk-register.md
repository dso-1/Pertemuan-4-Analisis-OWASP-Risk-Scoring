# Risk Register - OJS 3.3.0-8

Formula acuan:
- Likelihood = (kemudahan eksploitasi + ketersediaan attack path)
- Impact = (dampak teknis + dampak bisnis)
- Risk Level diturunkan dari kombinasi CVSS, likelihood, dan impact.

Skala:
- Likelihood: 1 (Very Low) sampai 5 (Very High)
- Impact: 1 (Very Low) sampai 5 (Very High)

| ID | Kerentanan | OWASP | Sumber | CVSS | Likelihood | Impact | Risk | Prioritas | Status |
|---|---|---|---|---:|---:|---:|---|---:|---|
| VUL-004 | Vulnerable JS Library (ua-parser-js) | A06 | ZAP | 9.8 | 4 | 5 | Critical | 1 | Valid |
| VUL-012 | Endpoint `/install` masih tersedia | A05 | Gobuster | 9.8* | 4 | 5 | Critical | 2 | Valid (perlu verifikasi bypass) |
| VUL-001 | Command Injection via backticks (InstallTool) | A03 | Semgrep | 7.8 | 3 | 5 | High | 3 | Valid/Potensial |
| VUL-009 | HTTP tanpa HTTPS | A02 | ZAP | 6.5 | 4 | 4 | High | 4 | Valid |
| VUL-006 | Directory Browsing pada `/cache/` | A05 | Nikto/ZAP | 5.3 | 4 | 3 | Medium | 5 | Valid |
| VUL-007 | Cookie tanpa HttpOnly | A05 | Nikto/ZAP | 5.4** | 3 | 3 | Medium | 6 | Valid |
| VUL-010 | Header anti-clickjacking tidak ada | A05 | Nikto/ZAP | 4.3 | 3 | 2 | Medium | 7 | Valid |
| VUL-005 | CSP header tidak diset | A05 | ZAP | 5.4** | 3 | 3 | Medium | 8 | Valid |
| VUL-011 | SRI attribute missing | A08 | ZAP | 4.8** | 2 | 3 | Medium | 9 | Valid |
| VUL-002 | Insecure Deserialization (`unserialize`) | A08 | Semgrep | 6.2** | 2 | 4 | Medium | 10 | Potensial |
| VUL-003 | Unsafe File Deletion (`unlink`) | A05 | Semgrep | 5.5** | 2 | 3 | Medium | 11 | Potensial |
| VUL-008 | Cookie tanpa SameSite | A05 | ZAP | 3.1** | 3 | 2 | Low | 12 | Valid |

Keterangan:
- Nilai dengan tanda * adalah worst-case estimate untuk prioritisasi awal.
- Nilai dengan tanda ** adalah skor estimasi operasional internal (bukan dari NVD CVE langsung), dipakai untuk ranking remediation.

## Observasi Penting (Negative Findings)

| Item | Hasil Uji | Dampak ke Prioritas |
|---|---|---|
| SQL Injection | Tidak ditemukan oleh SQLMap pada parameter yang diuji | Menurunkan urgensi A03 dari sisi SQLi saat ini |
| SSRF CVE-2021-27188 | Tidak terbukti exploitable (authorization barrier/noContext) | Dipantau, namun bukan prioritas patch paling atas saat ini |
