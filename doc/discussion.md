# Jawaban Pertanyaan Diskusi — Pertemuan 4

**1. Mengapa CVSS 9.8 (Critical) bisa memiliki risk aktual lebih rendah dari CVSS 6.5 (Medium)?**
CVSS mengukur keparahan teknis secara umum (Base Score), sedangkan *actual risk* dipengaruhi oleh konteks bisnis. Jika kerentanan 9.8 berada pada server testing yang tidak berisi data sensitif dan tidak terhubung ke internet, risiko bisnisnya lebih rendah dibanding kerentanan 6.5 pada server produksi yang menyimpan naskah jurnal internasional dan data identitas peneliti.

**2. Perbedaan Base, Temporal, dan Environmental Score? Mana yang paling relevan untuk institusi pendidikan?**
* **Base Score:** Karakteristik intrinsik kerentanan (tetap).
* **Temporal Score:** Status kerentanan saat ini (misal: apakah exploit publik sudah tersedia?).
* **Environmental Score:** Skor berdasarkan lingkungan spesifik organisasi.
* **Relevansi:** **Environmental Score** paling relevan karena institusi pendidikan perlu memprioritaskan aset berdasarkan kepentingan akademik (misal: server nilai vs server publikasi umum).

**3. Apakah A06 pada OJS harus mendapatkan skor tinggi?**
**Ya.** OJS mengelola Kekayaan Intelektual (naskah belum terbit). Komponen lama (A06) memudahkan penyerang otomatis (bot) masuk ke sistem. Jika naskah bocor atau sistem terinfeksi ransomware akibat komponen lama, reputasi akademik institusi akan hancur secara permanen.

**4. Prioritas perbaikan utama menurut pandangan CISO?**
Prioritas pertama adalah **VUL-001 (SQL Injection)**. Alasan: Kerentanan ini memungkinkan akses penuh ke database (Full Compromise) dengan kompleksitas serangan yang sangat rendah. Tanpa memperbaiki ini, penyerang bisa menjadi "admin" secara instan dan mencuri seluruh data aset kritis.
