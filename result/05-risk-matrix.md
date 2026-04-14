# Risk Matrix 5x5 - OJS 3.3.0-8

Matriks berikut disusun dari kombinasi Likelihood dan Impact pada risk register.

## Matriks

```text
Impact \ Likelihood |   1    |   2    |   3    |   4    |   5
--------------------+--------+--------+--------+--------+-------
5 (Very High)       |        |        | VUL-001| VUL-004| 
                    |        |        |        | VUL-012| 
4 (High)            |        | VUL-002|        | VUL-009| 
3 (Medium)          |        | VUL-003| VUL-007| VUL-006| 
                    |        | VUL-011| VUL-005|        | 
2 (Low)             |        |        | VUL-008| VUL-010| 
1 (Very Low)        |        |        |        |        | 
```

## Legend
- Critical: butuh tindakan segera.
- High: perbaikan prioritas sprint terdekat.
- Medium: perbaikan terjadwal dengan kontrol kompensasi.
- Low: monitor dan hardening bertahap.

## Pemetaan Ringkas Level Risiko

| Level | ID Temuan |
|---|---|
| Critical | VUL-004, VUL-012 |
| High | VUL-001, VUL-009 |
| Medium | VUL-002, VUL-003, VUL-005, VUL-006, VUL-007, VUL-010, VUL-011 |
| Low | VUL-008 |

## Catatan
- VUL-012 memakai pendekatan worst-case sampai verifikasi manual endpoint instalasi selesai.
- VUL-002 dan VUL-003 masih berstatus potensial dan perlu validasi exploit path sebelum eskalasi level.
