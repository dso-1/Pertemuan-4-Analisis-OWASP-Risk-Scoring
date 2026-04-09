### 5.1 Formula Risk (OWASP Risk Rating Methodology)

```
Likelihood = (Threat Agent Factors + Vulnerability Factors) / 2
Impact     = (Technical Impact + Business Impact) / 2
Risk Score = Likelihood × Impact
```

### 5.2 Risk Register OJS — Template Terisi

| ID | Kerentanan | OWASP | CVSS Score | Rating | Likelihood | Business Impact | Risk | Prioritas |
|---|---|---|---|---|---|---|---|---|
| VUL-002 | SQL Injection (Time-based parameter login) | A03 | 9.8 | Critical | 4 (High) | 5 (Kritis — kebocoran data) | **Critical** | 1 |
| VUL-011 | RCE / Prot. Pollution pd Library ua-parser-js | A06 | 10.0 | Critical | 3 (Medium) | 5 (Kritis — RCE remote) | **Critical** | 2 |
| VUL-003 | Insecure File Upload & no verify | A08 | 8.8 | High | 4 (High) | 4 (Tinggi — backdooring) | **High** | 3 |
| VUL-008 | OJS Version out of date (3.3.0-8, PHP 7.4) | A06 | 7.5 | High | 5 (Very High) | 3 (Sedang — kompromi VM) | **High** | 4 |
| VUL-020 | Open Redirect parameter source /login | A01 | 6.1 | Medium | 4 (High) | 3 (Sedang — reputasi user) | **Medium** | 5 |
| VUL-006 | Hardcoded Credentials di config.inc.php | A07 | 9.1 | Critical | 2 (Low) | 5 (Kritis — database leak) | **High** | 6 |
| VUL-005 | Exposed Endpoint /server-status & Debug info | A05 | 5.3 | Medium | 5 (Very High) | 2 (Rendah — hanya info) | **Medium** | 7 |
| VUL-001 | Unsafe Use of eval() backend (PHP) | A03 | 7.3 | High | 2 (Low) | 4 (Tinggi — local RCE) | **Medium** | 8 |
| VUL-004 | Tidak ada flag X-Frame-Options | A05 | 4.3 | Medium | 4 (High) | 2 (Rendah — UI clickjack) | **Medium** | 9 |
| VUL-007 | Cookie tanpa HTTPOnly | A05 | 4.3 | Medium | 4 (High) | 2 (Rendah — Pencurian Sesi) | **Medium** | 10 |

### 5.3 Likelihood Scale

| Skor | Level | Deskripsi |
|---|---|---|
| 1 | Very Low | Sulit dieksploitasi, butuh skill tinggi |
| 2 | Low | Membutuhkan kondisi tertentu |
| 3 | Medium | Aktor dengan kemampuan rata-rata bisa mengeksploitasi |
| 4 | High | Mudah dieksploitasi, banyak tools otomatis |
| 5 | Very High | Otomatis dan sangat mudah |

### 5.4 Business Impact Scale

| Skor | Level | Dampak |
|---|---|---|
| 1 | Minimal | Tidak ada dampak signifikan |
| 2 | Low | Gangguan minor, tidak ada data leak |
| 3 | Medium | Gangguan signifikan, reputasi terdampak |
| 4 | High | Kebocoran data pengguna, denda regulasi |
| 5 | Critical | Kompromi sistem penuh, RCE, data breach masif |
