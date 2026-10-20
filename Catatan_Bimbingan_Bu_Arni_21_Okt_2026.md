# Catatan Bimbingan Bu Arni — Conveyor Grading TBS + IoT + ERP
**Rabu, 21 Oktober 2026**  
**Tujuan:** pulang dengan keputusan tentang fokus masalah, novelty kerja, dataset/validasi, dan prioritas revisi proposal.

> **Deadline resmi:** Jumat, 30 Oktober 2026. Situs resmi BPDP: https://lombariset.bpdp.or.id/ (diakses 20 Oktober 2026).

## 1. Pitch 60 detik

> Bu, kami menyusun konsep prototipe conveyor grading TBS semi-manual. Satu tandan diperiksa dalam satu siklus; load cell membaca berat, satu kamera dengan pencahayaan terkendali mengambil beberapa foto dari sudut berbeda, dan AI mengestimasi kelas grading sesuai label yang didukung data. Hasil sensor, prediksi AI, dan koreksi operator digabungkan berdasarkan ID pemeriksaan lalu dicatat otomatis di modul ERP penerimaan. Kami tidak mengklaim membuat alat grading atau integrasi ERP pertama. Fokus yang ingin kami uji adalah apakah pengambilan beberapa foto dan penggabungan prediksi per tandan memberi hasil lebih konsisten, serta apakah seluruh data dapat tercatat dengan benar dan dapat ditelusuri di ERP. Saat ini dataset publik sudah menjadi kandidat awal, tetapi sampel TBS dan akses grader/PKS belum terkonfirmasi. Kami ingin meminta arahan Ibu untuk mempersempit novelty dan memastikan metode ini layak dikerjakan.

## 2. Konsep yang dibawa

`Input ID/QR → load cell membaca berat → satu kamera + LED mengambil beberapa sudut → AI mengestimasi kelas → gabungkan berdasarkan inspectionId → API/backend → ERP penerimaan, bukti visual, verifikasi, laporan.`

Ruang lingkup MVP: conveyor roller manual; satu tandan per pemeriksaan; satu kamera; load cell + HX711 + ESP32; laptop/mini-PC untuk AI dan gateway; Next.js + Firebase untuk ERP. Pemilahan otomatis, hitung penalti harga, dan pengukuran ALB langsung bukan bagian MVP.

## 3. Keputusan yang ingin dikunci bersama Bu Arni

1. **Bidang:** tetap Bidang 5 — Pasca Panen & Pengolahan, dengan ERP sebagai sarana implementasi.
2. **Masalah utama:** keterbatasan representasi satu foto terhadap tandan 3D dan kebutuhan mengikat hasil sensor/AI pada satu rekaman grading yang bisa ditelusuri.
3. **Novelty kerja:** membandingkan prediksi satu foto dengan agregasi beberapa foto dari tandan yang sama; mengevaluasi keandalan integrasi data ke ERP secara terpisah.
4. **Batas AI:** gunakan kelas yang didukung dataset publik; jangan klaim F00–F5 tanpa label yang sesuai dan validasi.
5. **Kelayakan:** sepakati apakah dataset publik + simulasi cukup untuk proposal konseptual, dan bagaimana merencanakan sampel/penilai lokal jika riset didanai.

## 4. Yang masih kurang dari draft

- Novelty belum aman: grading machine vision, sensor fusion, dan integrasi AI–ERP telah memiliki contoh terdahulu.
- Dataset belum dipastikan memiliki ID yang memungkinkan foto beberapa sudut dipasangkan ke tandan yang sama.
- Kelas publik tidak otomatis setara dengan fraksi Indonesia F00–F5.
- Belum ada sampel TBS, grader, atau mitra yang terkonfirmasi.
- Standar teknis label perlu dibedakan dari Permentan yang mengatur pembelian TBS pekebun mitra.
- Metode eksperimen, baseline, split data per tandan/video, dan target per kelas belum final.
- BOM dan anggaran belum memiliki nominal yang didukung survei harga.

## 5. Pertanyaan prioritas untuk Bu Arni

1. Apakah fokus ini tepat di Bidang 5, atau perlu digeser jika kontribusi utama adalah integrasi data ERP?
2. Mana yang paling kuat sebagai kontribusi utama: (A) eksperimen single-image vs multi-view aggregation, atau (B) integrasi end-to-end sensor/AI ke ERP? Apakah salah satunya terlalu lemah atau terlalu luas?
3. Dengan belum ada sampel TBS/mitra, apakah dataset publik + prototipe konseptual bisa diterima pada proposal? Data lapangan apa yang wajib direncanakan jika proposal didanai?
4. Apakah ada calon grader ahli, laboratorium, PKS, atau kontak untuk validasi sampel?
5. Standar/pedoman grading mana yang tepat dijadikan acuan kelas dan label?
6. Apakah conveyor manual + satu kamera + load cell + ERP realistis untuk tim dan durasi enam bulan?
7. Apa bagian yang paling perlu direvisi sebelum submit: masalah, novelty, metode, atau anggaran?

**Saran:** minta pembimbing memilih maksimal satu kontribusi utama dan satu kontribusi pendukung. Opsi awal: kontribusi utama = uji agregasi foto multi-sudut; ERP = kontribusi sistem pendukung yang dievaluasi dengan metrik integritas data.

## 6. Agenda (25–35 menit)

- **0–3 menit:** status draft konseptual; belum ada klaim alat pertama; belum ada mitra/sampel yang terkonfirmasi.
- **3–8 menit:** presentasi alur conveyor → timbang → kamera multi-foto → AI → ID → ERP.
- **8–18 menit:** bahas pertanyaan utama, novelty A/B, data, dan validasi.
- **18–25 menit:** kunci ruang lingkup MVP, bidang, acuan grading, dan batas klaim AI.
- **25–35 menit:** risiko, tim, budget, kebutuhan koneksi, dan timeline.

## 7. Yang perlu dibawa

- [ ] Draft konseptual proposal v1 (DOCX).
- [ ] Matriks penelitian terdahulu dan kandidat research gap.
- [ ] Diagram arsitektur sistem dan decision log MVP.
- [ ] Kandidat dataset publik dan hal yang belum diverifikasi: lisensi, label, jumlah, pasangan multi-sudut.
- [ ] Catatan batasan: belum ada mitra/sampel; kelas publik belum setara F00–F5; target akurasi adalah target, bukan hasil.

## 8. Rencana setelah bimbingan

| Tanggal | Output |
|---|---|
| 21 Okt | Catat keputusan bidang, masalah, novelty, dataset, validasi, dan akses mitra potensial. |
| 22–23 Okt | Revisi rumusan masalah/novelty; audit dataset, lisensi, dan kelayakan uji multi-foto. |
| 24–25 Okt | Perkuat Bab I–III: gap, eksperimen, variabel, metrik, risiko. |
| 26 Okt | Lengkapi BOM dan survei harga; susun anggaran. |
| 27–28 Okt | Kirim revisi untuk komentar pembimbing/tim. |
| 29 Okt | Final check format, halaman, daftar pustaka, biodata, persetujuan, dan lampiran. |
| 30 Okt | Tenggat proposal BPDP; submit sebelum batas akhir. |

## 9. Definisi bimbingan berhasil

- [ ] Satu rumusan masalah utama dan satu novelty kerja dipilih atau diperintahkan untuk revisi.
- [ ] Diputuskan apakah eksperimen multi-foto satu tandan dapat diuji dengan data realistis.
- [ ] Jelas mana yang bisa dikerjakan dengan dataset publik dan mana yang membutuhkan sampel/grader lokal.
- [ ] Ada arahan standar grading dan kemungkinan kontak untuk validasi.
- [ ] Ada prioritas revisi dan tanggal pengiriman ulang draft.

## Catatan sumber

- BPDP, Lomba Riset Mahasiswa: https://lombariset.bpdp.or.id/
- Panduan Teknis Proposal Lomba Riset Tingkat Mahasiswa 2026–2027 dan format proposal resmi yang dilampirkan dalam percakapan.
