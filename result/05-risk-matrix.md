# Risk Matrix Karakteristik Evaluasi (need for convert to jpg file)

Matriks resiko ini menyoroti titik temu relasi antar tingkat "Likelihood (Probabilitas Terjadinya)" yang memaparkan 1 sampai 5 ke kanan, vs "Business Impact" keparahan institusi yang memanjang ke atas (1 sampai 5).

> Acuan visual text-matrix ini mengimitasikan hasil grafik 5x5 heatmap dari pemetaan Risk Register file `03-risk-register.md`.

```text
         |  VERY    |         |         |         |  VERY   |
BUSN     |  LOW     |   LOW   | MEDIUM  |  HIGH   |  HIGH   |
IMPACT   |   (1)    |   (2)   |   (3)   |   (4)   |   (5)   |
---------+----------+---------+---------+---------+---------|
VERY HIGH|          |         |         | VU-02   |         |
   (5)   |          | VU-06   |         |         |         |
---------+----------+---------+---------+---------+---------|
HIGH     |          |         |         | VU-03   |         |
   (4)   |          | VU-01   |         |         |         |
---------+----------+---------+---------+---------+---------|
MEDIUM   |          |         |         | VU-20   | VU-08   |
   (3)   |          |         |         | VU-11   |         |
---------+----------+---------+---------+---------+---------|
LOW      |          |         |         | VU-04   | VU-05   |
   (2)   |          |         |         | VU-07   |         |
---------+----------+---------+---------+---------+---------|
VERY LOW |          |         |         |         |         |
   (1)   |          |         |         |         |         |
---------+----------+---------+---------+---------+---------|
         LIKELIHOOD (Kiri-Kanan) (1=VeryLow -> 5=VeryHigh)
```

### Panduan Legenda Evaluasi
- Warna:  🔴 Critical  🟠 High  🟡 Medium  🟢 Low  ⚪ Info
