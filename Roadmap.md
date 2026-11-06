# Roadmap Skripsi

## Anti executive dysfunction

- **Satu langkah aktif saja.** Sisanya "parked". Jangan buka fase lain sebelum Current Step selesai.
- **Kerja menghasilkan artifact**, bukan "belajar dulu". Tiap langkah harus meninggalkan file, log, foto, atau commit.
- **Kalau macet, pakai "If stuck"**, jangan desain ulang sistem.
- **Stop rule:** kalau sebuah langkah mulai melebar, tulis "cukup" dan pindah. Sempurna bukan tujuan.
- Setelah satu langkah selesai: centang, tulis 1 baris di [[Log Bimbingan]], pindahkan pointer Current Step.
- **Dilarang** mulai dari menulis Bab II panjang atau tuning drone berhari-hari. Mulai dari sinyal dan data.

---

## Current Step

- [ ] **Step 0.1 — Tulis rumusan masalah + dua tujuan awal.** Simpan di [[Outline Skripsi]].

*(Setelah selesai, ganti isi bagian ini dengan langkah berikutnya.)*

---

## Fase 0 — Kunci Tujuan & Lingkup

**Why:** dua tujuan awal jadi patokan; semua fase harus mengarah ke sana.

- [ ] Tulis rumusan masalah: "Bisakah lokalisasi berbasis CSI fingerprint pada ESP32 memandu drone FLIX bergerak otonom dari satu titik ke titik lain?"
- [ ] Tulis dua tujuan awal: (1) lokalisasi low-cost indoor untuk FLIX; (2) uji viability CSI untuk gerak otonom.
- [ ] Tulis ruang lingkup: 2D, satu ruangan dikenal, altitude terbatas, lintasan bebas halangan, tanpa obstacle avoidance/SLAM/multi-drone.
- [ ] Tetapkan metrik di [[Metrik Evaluasi]]: error lokalisasi (meter) dan error posisi akhir terhadap target (meter), diukur dalam **n percobaan**.

**Done when:** ada rumusan masalah, dua tujuan awal, ruang lingkup, dan metrik dalam meter.
**If stuck:** salin kalimat rumusan masalah di atas; jangan bikin variasi baru.

---

## Fase 1 — Studi Literatur & Tulisan Awal

**Why:** Bab I–II harus selesai lebih awal agar menulis tidak menumpuk di akhir.

**Teknis**
- [ ] Baca [[CiUAV]], [[UbiTrack]], few-shot regression, dan survey CSI.
- [ ] Buat tabel perbandingan paper.

**Tulisan**
- [ ] Bab I Latar Belakang: 3 paragraf (GPS-denied; opsi sensor; celah CSI 2D low-cost).
- [ ] Bab I Rumusan Masalah, Tujuan, Ruang Lingkup, Sistematika.
- [ ] Bab II 2.1 WiFi Sensing & [[CSI]]: definisi, amplitude/phase, subcarrier.
- [ ] Bab II 2.2 [[Fingerprinting]]: alur offline map → online matching, metrik jarak.
- [ ] Bab II tabel penelitian terdahulu: metode, sensor, ruang, error (meter), keterbatasan.

**Done when:** klaim Bab I–II punya sitasi dan ≥20 referensi awal terkumpul.
**If stuck:** baca 1 paper, tulis 3 bullet di catatannya.

---

## Fase 2 — FLIX & Sinyal CSI

**Why:** fondasi teknis sebelum data dan gerak otonom.

**Teknis**
- [ ] FLIX hover stabil.
- [ ] Jalankan repo ESP-CSI di 2 board (TX/RX); simpan 1 CSV/JSON ke `Data/raw/`.
- [ ] Plot amplitude vs subcarrier.

**Tulisan**
- [ ] Bab II 2.3 Platform: [[flix]] + ESP-CSI (spesifikasi, alasan low-cost).
- [ ] Bab III 3.1 Diagram arsitektur sistem (drone–receiver–router–ground station).
- [ ] Bab III 3.2 Daftar komponen + tabel BOM (klaim low-cost).
- [ ] Lampiran: foto setup + caption.

**Done when:** hover stabil, data CSI + plot ada, dan diagram arsitektur/BOM masuk draft.
**If stuck:** pakai data contoh repo dulu; jangan tunggu hardware sempurna.

---

## Fase 3 — Pengumpulan Fingerprint

**Why:** "utama dari skripsi adalah datanya."

**Teknis**
- [ ] Tentukan grid (mis. 4×4) dan 2–3 tinggi; gambar denah + posisi receiver di [[Data Penelitian]].
- [ ] Tetapkan protokol: jumlah sampel, split train/test **berdasarkan lokasi**.
- [ ] Tandai titik dengan lakban + meteran; foto setup.
- [ ] Ambil data 1 titik sebagai pilot; cek apakah tiap titik terlihat beda.
- [ ] Lanjutkan seluruh grid; simpan dengan nama file konsisten.
- [ ] Buat tabel ringkas: titik, tinggi, jumlah sampel.

**Tulisan**
- [ ] Bab III 3.3 Protokol: grid, tinggi, jumlah sampel, durasi, split per lokasi.
- [ ] Bab III tabel titik & metadata.
- [ ] Bab III alasan pemilihan grid/tinggi (sitasi).
- [ ] Bab III catatan interferensi/kalibrasi.

**Done when:** dataset + metadata + foto ada, dan protokol di draft sama dengan yang dipakai.
**If stuck:** kurangi grid (3×3), jangan menambah tinggi. Data kecil bersih > besar tapi kacau.

---

## Fase 4 — Model Baseline & Evaluasi

**Why:** baseline memberi angka pembanding dan komponen matematis.

**Teknis**
- [ ] Buat notebook/script training.
- [ ] Baseline pertama: kNN atau Random Forest pada fingerprint amplitude.
- [ ] Hitung error dalam **meter** (MAE, RMSE, median, max) pada test set berbasis lokasi.
- [ ] Simpan tabel hasil di [[Metrik Evaluasi]].

**Tulisan**
- [ ] Bab III formula fingerprint + metrik (MAE, RMSE, median; satuan meter).
- [ ] Bab IV tabel hasil baseline.
- [ ] Bab IV grafik CDF error.
- [ ] Bab IV pembahasan error per area/tinggi.
- [ ] Bab II/III justifikasi baseline vs model lain.

**Done when:** model bisa memprediksi koordinat + tabel/grafik error masuk draft.
**If stuck:** turunkan ambisi fitur (amplitude saja), bukan menambah model.

---

## Fase 5 — Inferensi Real-time

**Why:** menjembatani data ke gerak otonom.

**Teknis**
- [ ] Buat ground station: terima CSI → prediksi → tampilkan titik di denah.
- [ ] Uji dengan data replay (offline) dulu.
- [ ] Uji live dengan board diam di beberapa titik.
- [ ] Catat akurasi offline vs live (meter).
- [ ] Rekam video pendek sebagai bukti.

**Tulisan**
- [ ] Bab III pipeline real-time (latency, update rate).
- [ ] Bab IV akurasi offline vs live (meter).

**Done when:** lokasi tampil live + rekaman + tabel perbandingan.
**If stuck:** cukup visualizer offline dulu; lanjutkan tanpa menunggu live sempurna.

---

## Fase 6 — Gerak Otonom Titik-ke-Titik

**Why:** tujuan awal kedua — menguji viability CSI untuk gerak otonom.

**Teknis**
- [ ] Pakai mode position-hold/offboard yang sudah ada di [[flix]]; jangan tulis firmware dari nol.
- [ ] Uji satu waypoint pelan di ketinggian rendah.
- [ ] Catat posisi target vs posisi aktual (kamera atas/ArUco).
- [ ] Hitung error jarak dalam **meter** untuk **n percobaan** A→B.
- [ ] Catat kegagalan: crash, manual takeover, timeout.

**Tulisan**
- [ ] Bab III arsitektur kontrol + bagaimana estimasi CSI dipakai sebagai posisi.
- [ ] Bab IV tabel percobaan: target, aktual, error (meter), intervensi manual.
- [ ] Bab IV pembahasan keterbatasan (interferensi, tuning, latency).
- [ ] Bab V kesimpulan: jawab dua tujuan awal.
- [ ] Bab V saran.

**Done when:** minimal satu perpindahan A→B terekam dengan error meter, dan draf Bab IV–V ada.
**If stuck:** berhenti tuning setelah beberapa percobaan; tulis keterbatasan yang teramati. Jangan mengganti tujuan.

---

## Fase 7 — Paket Akhir

- [ ] Abstrak (Indonesia + Inggris).
- [ ] Konsistensi istilah, penomoran gambar/tabel, daftar pustaka.
- [ ] Rapikan repo GitHub (README, cara jalan, data/link) + deklarasi penggunaan AI.
- [ ] Slide 20 menit: masalah → metode → data → hasil → demo → kesimpulan.
- [ ] Rekam demo cadangan (jangan bergantung live).

**Done when:** buku utuh, repo bisa dijalankan orang lain, slide + demo cadangan siap.

---

## Ritme Menulis

- Setelah tiap langkah: tulis bagian yang relevan, minimal 1 paragraf.
- Akhir tiap fase: gabungkan draft, baca utuh, perbaiki transisi antar sub-bab.
- Setiap ada hasil baru (tabel/grafik): langsung tulis 3 kalimat — apa yang diukur, angkanya, artinya.
- Simpan daftar "belum ditulis" di [[Outline Skripsi]] supaya tidak lupa.
- Kirim draft per bab ke pembimbing; jangan tunggu satu buku lengkap.
- Jangan menulis Bab II sekali jadi; tumbuhkan seiring paper baru masuk.

---

## Kalau Macet / Energi Nol

Pilih **satu** dari ini, jangan lebih:

- [ ] Buka [[Outline Skripsi]] dan isi satu sub-bab kosong (1 paragraf).
- [ ] Jalankan ulang script plot CSI yang sudah ada.
- [ ] Ambil 1 titik data baru.
- [ ] Tulis 1 baris progres di [[Log Bimbingan]].
- [ ] Rapikan 1 file data / 1 nama file.
- [ ] Baca 1 paper, tulis 3 bullet di catatannya.

**Aturan macet:** kalau ragu > beberapa menit, pilih item paling atas yang belum dicentang. Jangan menambah tool baru.

---

## Di Luar Tujuan

- Lokalisasi 3D penuh.
- Multi-task learning sebagai kewajiban.
- Obstacle avoidance, SLAM, multi-drone.
- Tuning drone mendalam sebelum data & model jadi.
- Menulis teori panjang sebelum ada artifact.
