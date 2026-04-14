# Pemetaan Temuan ke OWASP Top 10 2021

Dokumen ini memetakan temuan aktual dari proses scanning (Nikto, ZAP, Gobuster, SQLMap, SSRF test) dan SAST (Semgrep) ke kategori OWASP Top 10 2021.

## Ringkasan Sumber Data
- DAST: recon_summary.md
- SAST: Temuan SAST dan Checklist.md
- Scope target: OJS 3.3.0-8 pada 10.34.100.178

## Tabel Pemetaan

| ID | Temuan | Sumber | Bukti Ringkas | OWASP | CWE | CVE | Status |
|---|---|---|---|---|---|---|---|
| VUL-001 | Command Injection via backticks pada InstallTool | Semgrep | `/bin/stty -echo`, `/bin/stty echo` di InstallTool.inc.php | A03: Injection | CWE-78 | - | Valid (High) |
| VUL-002 | Insecure Deserialization (`unserialize`) | Semgrep | `unserialize(...)` di file migration/cache | A08: Software and Data Integrity Failures | CWE-502 | - | Potensial (Medium) |
| VUL-003 | Unsafe File Deletion (`unlink`) | Semgrep | `unlink($file)`, `unlink($this->filename)` | A05: Security Misconfiguration | CWE-73 | - | Potensial (Medium) |
| VUL-004 | Vulnerable JS Library (ua-parser-js) | ZAP | Alert "Vulnerable JS Library (High)" | A06: Vulnerable and Outdated Components | CWE-1104 | CVE-2021-27292 | Valid (High) |
| VUL-005 | CSP Header tidak diset | ZAP | "Content Security Policy (CSP) Header Not Set" | A05: Security Misconfiguration | CWE-693 | - | Valid (Medium) |
| VUL-006 | Directory Browsing aktif (`/cache/`) | Nikto, ZAP | "Directory indexing found" dan "Directory Browsing" | A05: Security Misconfiguration | CWE-548 | - | Valid (Medium) |
| VUL-007 | Cookie tanpa HttpOnly | Nikto, ZAP | "Cookie OJSSID without httponly" | A05: Security Misconfiguration | CWE-1004 | - | Valid (Medium) |
| VUL-008 | Cookie tanpa SameSite | ZAP | "Cookie without SameSite Attribute" | A05: Security Misconfiguration | CWE-1275 | - | Valid (Low) |
| VUL-009 | HTTP tanpa HTTPS | ZAP | "HTTP Only Site (No HTTPS)" | A02: Cryptographic Failures | CWE-319 | - | Valid (Medium) |
| VUL-010 | Header anti-clickjacking tidak ada | Nikto, ZAP | "X-Frame-Options header tidak ada" | A05: Security Misconfiguration | CWE-1021 | - | Valid (Medium) |
| VUL-011 | Subresource Integrity (SRI) tidak dipakai | ZAP | "Subresource Integrity Attribute Missing" | A08: Software and Data Integrity Failures | CWE-353 | - | Valid (Medium) |
| VUL-012 | Endpoint `/install` masih terekspos | Gobuster | `/install` ditemukan (redirect) | A05: Security Misconfiguration | CWE-16 | - | Valid (High) |

## Temuan Yang Tidak Terbukti Eksploitabel

| ID | Item Uji | Hasil | Implikasi |
|---|---|---|---|
| OBS-001 | SQL Injection (SQLMap) | Tidak ditemukan parameter injectable | Risiko A03 dari SQLi pada endpoint yang diuji saat ini rendah |
| OBS-002 | SSRF CVE-2021-27188 | Not Vulnerable pada skenario uji; terhalang otorisasi/noContext | Risiko A10 ada secara teoritis, namun belum terbukti eksploitabel pada konfigurasi saat ini |

## Catatan Deduplikasi SAST
- 38 temuan Semgrep dideduplikasi menjadi 3 kelompok utama: Command Injection, Insecure Deserialization, Unsafe File Deletion.
- Insecure Deserialization dan Unsafe File Deletion ditandai potensial karena membutuhkan verifikasi aliran input agar dapat dinyatakan exploitable.
