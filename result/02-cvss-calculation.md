# Perhitungan CVSS v3.1 (Berdasarkan Temuan Aktual)

Dokumen ini menggunakan pendekatan konservatif: skor diberikan berdasarkan bukti yang benar-benar tersedia pada hasil scanning/SAST, dengan asumsi eksploitasi yang dijelaskan secara eksplisit.

## 1) VUL-004 - Vulnerable JS Library (ua-parser-js)

- Sumber: ZAP
- Bukti: Alert "Vulnerable JS Library (High)"
- Asumsi: library rentan dapat dimanfaatkan pada sisi klien/aplikasi tergantung konteks pemakaian.

Vector:
`CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H`

Nilai:
- AV:N, AC:L, PR:N, UI:N, S:U, C:H, I:H, A:H

Base Score: 9.8 (Critical)

## 2) VUL-012 - Endpoint /install Masih Tersedia

- Sumber: Gobuster
- Bukti: endpoint `/install` masih terdeteksi (redirect)
- Asumsi: jika proteksi instalasi gagal/bisa dibypass, potensi pengambilalihan konfigurasi sangat tinggi.

Vector:
`CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H`

Base Score: 9.8 (Critical)

Catatan:
- Ini worst-case score. Perlu verifikasi manual apakah benar endpoint dapat dipakai untuk re-install atau hanya redirect aman.

## 3) VUL-009 - HTTP Tanpa HTTPS

- Sumber: ZAP
- Bukti: "HTTP Only Site (No HTTPS)"
- Asumsi: trafik kredensial/session berisiko disadap pada jaringan tidak tepercaya.

Vector:
`CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:L/I:L/A:N`

Base Score: 6.5 (Medium)

## 4) VUL-006 - Directory Browsing pada /cache/

- Sumber: Nikto, ZAP
- Bukti: directory indexing/browsing aktif
- Asumsi: kebocoran file cache/informasi internal namun tidak langsung memberi write access.

Vector:
`CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:L/I:N/A:N`

Base Score: 5.3 (Medium)

## 5) VUL-001 - Command Injection (Backticks) pada InstallTool

- Sumber: Semgrep
- Bukti: eksekusi backticks di InstallTool.inc.php
- Asumsi: saat ini belum ada bukti user input langsung mengendalikan command, sehingga dinilai sebagai potensi serius.

Vector:
`CVSS:3.1/AV:L/AC:L/PR:L/UI:N/S:U/C:H/I:H/A:H`

Base Score: 7.8 (High)

## Ringkasan Skor

| ID | Temuan | Vector | Score | Severity |
|---|---|---|---|---|
| VUL-004 | Vulnerable JS Library | AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H | 9.8 | Critical |
| VUL-012 | Endpoint /install exposed (worst-case) | AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H | 9.8 | Critical |
| VUL-001 | Command Injection (potential) | AV:L/AC:L/PR:L/UI:N/S:U/C:H/I:H/A:H | 7.8 | High |
| VUL-009 | No HTTPS | AV:N/AC:L/PR:N/UI:N/S:U/C:L/I:L/A:N | 6.5 | Medium |
| VUL-006 | Directory Browsing | AV:N/AC:L/PR:N/UI:N/S:U/C:L/I:N/A:N | 5.3 | Medium |

## Catatan Validasi
- SQLMap pada target yang diuji: tidak menemukan SQL Injection.
- Uji SSRF CVE-2021-27188: tidak terbukti exploitable pada konfigurasi saat ini (authorization barrier/noContext).
- Dua poin di atas tidak diberi skor CVSS eksploitasi aktif karena tidak ada bukti exploit berhasil.
