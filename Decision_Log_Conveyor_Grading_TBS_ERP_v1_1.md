# Decision Log v1.1 — Conveyor Grading TBS + IoT + ERP

**Status:** rekomendasi untuk membekukan baseline konsep dan MVP. Belum merupakan desain manufaktur final atau klaim novelty final.

## A. Keputusan yang direkomendasikan untuk dibekukan sekarang

| ID | Keputusan | Baseline yang dibekukan | Alasan |
|---|---|---|---|
| D-01 | Fokus riset | Prototipe conveyor grading TBS semi-manual dengan hasil pemeriksaan otomatis masuk ke modul ERP penerimaan | Paling dekat dengan arahan dosen pembimbing dan prioritas riset BPDP Bidang 5: Pascapanen & Pengolahan. |
| D-02 | Bidang lomba | Bidang 5 sebagai pilihan utama sementara; Bidang 7 alternatif bila fokus riset bergeser dominan ke interoperabilitas ERP/SCM | Objek utama yang diteliti adalah grading dan proses pascapanen; ERP adalah sistem pencatatan/pendukung, bukan tujuan tunggal. |
| D-03 | Mekanisme | Roller conveyor manual; satu tandan per siklus; operator memindahkan dan mengorientasikan tandan; belum ada motor conveyor atau mekanisme reject otomatis | Mengurangi kompleksitas mekanis agar penelitian fokus pada grading, integrasi data, dan evaluasi. |
| D-04 | Cara merepresentasikan hasil | Simpan profil grading multi-parameter, bukan satu skor/kelas komposit yang tidak punya aturan acuan | Fraksi, berat, tangkai, dan cacat adalah atribut yang berbeda. Aturan penerimaan/penalti harus terpisah dan terversi. |
| D-05 | Cakupan otomatisasi MVP | Otomatis: berat tandan + pengambilan citra + estimasi visual kelas kematangan. Kondisi tambahan seperti tangkai panjang, busuk, tandan kosong, dan kotoran: dicatat operator atau diuji sebagai fitur eksperimen sekunder jika data memadai | Memberi prototipe alur end-to-end yang dapat diselesaikan dan dievaluasi tanpa menjanjikan otomasi semua kriteria sekaligus. |
| D-06 | Pengambilan citra | Satu kamera USB sebagai baseline, pencahayaan LED difus dalam hood/ruang inspeksi, operator memutar tandan untuk mengambil beberapa sudut | Lebih murah dan sederhana dibanding tiga kamera. Tambah kamera hanya jika uji blind spot menunjukkan perlu. |
| D-07 | Stasiun timbang | Platform timbang yang terisolasi mekanis dari conveyor saat pembacaan; load cell + HX711 + ESP32 | Meminimalkan beban terbagi dan gerakan yang dapat merusak pembacaan. Kapasitas load cell belum dikunci hingga rentang berat sampel ditentukan. |
| D-08 | Edge gateway dan AI | Laptop pengembangan sebagai gateway; Python + OpenCV untuk pipeline citra dan inferensi; ESP32 membaca sensor timbang | Memanfaatkan perangkat tersedia, memisahkan inferensi citra dari mikrokontroler, serta menjaga prototipe fleksibel. Model AI tertentu belum dikunci sebelum dataset dan label ditinjau. |
| D-09 | Stack ERP | Next.js + Firebase Authentication + API Node.js pada Firebase Cloud Functions + Firestore + Firebase Storage | Stack cukup sederhana untuk prototipe web dan pencatatan gambar/data terstruktur; tidak memerlukan ERP enterprise penuh. |
| D-10 | Komunikasi | ESP32 ke gateway melalui Wi-Fi lokal dan HTTP/JSON; gateway ke backend melalui HTTPS; antrean lokal SQLite saat internet putus | Sederhana untuk MVP serta mendukung pengiriman ulang. MQTT tidak dibutuhkan kecuali nanti banyak perangkat mengirim data kontinu. |
| D-11 | Identitas data | Satu `inspectionId` per tandan per pemeriksaan; banyak pemeriksaan dapat dikelompokkan dalam satu `batchId` | Memudahkan pencocokan berat, foto, prediksi, koreksi, dan transaksi tanpa data tertukar. |
| D-12 | Human-in-the-loop | Prediksi awal, hasil koreksi, alasan koreksi, reviewer, waktu, versi model, dan versi aturan disimpan terpisah | Memungkinkan audit, evaluasi kesalahan AI, dan koreksi tanpa menghapus riwayat awal. |
| D-13 | Validasi AI | Label acuan ditetapkan grader/penilai berpengalaman memakai satu dokumen acuan tertulis; laporkan confusion matrix, macro-F1, precision/recall per kelas | Accuracy tunggal dapat menutupi performa buruk pada kelas minoritas. |
| D-14 | Pencegahan kebocoran data | Foto dari tandan yang sama tidak boleh tersebar antara training/validation/test; split berdasarkan identitas tandan | Mencegah hasil evaluasi terlalu optimistis karena model melihat tandan yang sama dalam data train dan test. |
| D-15 | Evaluasi sistem | Ukur galat timbang, performa per kelas grading, waktu pemeriksaan, kelengkapan data, keberhasilan sinkronisasi, duplikasi, dan kecocokan ID | Menilai alat sebagai sistem menyeluruh, bukan hanya model AI atau dashboard. |
| D-16 | Scope proposal | Perancangan dan prototipe awal yang diuji secara terkontrol; tidak mengklaim sudah siap dipasang di PKS produksi | Menjaga klaim, biaya, dan jadwal sesuai kemampuan prototipe mahasiswa. Akses sampel TBS dan penilai berpengalaman tetap dibutuhkan untuk validasi. |

## B. Keputusan yang sengaja belum dibekukan

1. **Batas numerik fraksi dan standar penerimaan final.** Tetapkan satu rujukan kelas kematangan untuk pelabelan dan catat versinya. Verifikasi tabel fraksi dari dokumen teknis resmi sebelum label dataset dibuat. Jangan mengklaim sebagai SNI tanpa bukti nomor/judul SNI yang relevan.
2. **Aturan penalti atau harga.** Permentan 13 Tahun 2024 mengatur pembelian TBS produksi pekebun mitra dan memuat formula pembayaran TBS yang tidak memenuhi syarat penerimaan pada lampiran. Gunakan sebagai rujukan aturan pembelian yang relevan, bukan dianggap sebagai standar universal seluruh proses grading. Jangan mengaktifkan perhitungan penalti dalam MVP sebelum ruang lingkup dan aturan acuannya dipastikan.
3. **Kapasitas load cell.** Putuskan setelah berat minimum/maksimum TBS yang hendak diuji diketahui dan ada margin kapasitas yang memadai.
4. **Model AI, resolusi kamera, jumlah citra, dan target akurasi.** Tentukan setelah pilot pengambilan citra dan peninjauan dataset. Jangan berjanji 90–95% sebelum eksperimen.
5. **Jumlah sampel dan proporsi train/validation/test.** Tentukan berdasarkan jumlah tandan, distribusi kelas, dan desain eksperimen. Prinsip yang dibekukan adalah split per tandan, bukan rasio tertentu.
6. **Cakupan cacat fisik otomatis.** Tangkai panjang, buah busuk/rusak, tandan kosong, dan kotoran harus masuk otomatis hanya jika definisi label, sudut citra, dan sampel validasinya tersedia.
7. **Novelty final.** Anggap integrasi multi-stasiun ke ERP, audit trail, dan evaluasi end-to-end sebagai hipotesis kontribusi yang perlu dibandingkan dengan riset terdahulu, bukan klaim pertama di dunia.

## C. Baseline rujukan teknis dan peraturan

- **Permentan Nomor 131/Permentan/OT.140/12/2013** tentang Pedoman Budidaya Kelapa Sawit yang Baik tercatat berstatus berlaku pada basis data BPK; perlu memeriksa lampiran relevan untuk acuan kelas kematangan. https://peraturan.bpk.go.id/Details/160405/permentan-no-131permentanot140122013-tahun-20
- **Permentan Nomor 13 Tahun 2024** tentang Pembelian Tandan Buah Segar Kelapa Sawit Produksi Pekebun Mitra tercatat berstatus berlaku dan mencabut Permentan 01/2018. Cakupannya adalah pembelian TBS pekebun mitra; jangan menyamakan seluruh ketentuannya dengan satu standar universal grading. https://jdih.pertanian.go.id/peraturan/permentan-no13-tahun-2024
- Artikel Makky & Soni (2013) sudah melaporkan mesin grading TBS berbasis machine vision, mencakup sistem mekanis, pemrosesan citra, deteksi, dan kontrol. Oleh sebab itu, conveyor + machine vision saja bukan klaim novelty yang cukup. https://www.sciencedirect.com/science/article/abs/pii/S0168169913000471
- Panduan Lomba Riset BPDP 2026–2027 dari pengguna: Bidang 5 mencakup pengembangan teknologi panen/pascapanen TBS, sistem transportasi/logistik yang dapat diintegrasikan dengan IoT/AI, traceability, dan alat deteksi kematangan/kualitas. Bidang 7 dapat dipertimbangkan jika fokus utama berubah menjadi sistem digital/SCM.

## D. Rumusan konsep kerja

**Sistem conveyor grading TBS semi-manual berbasis multi-sensor dan computer vision yang menggabungkan hasil pemeriksaan satu tandan menjadi profil grading terstruktur dan mencatatkannya otomatis ke modul ERP penerimaan, dengan verifikasi operator serta evaluasi performa alat dan integritas data secara end-to-end.**

## E. Pertanyaan riset sementara

Bagaimana merancang dan mengevaluasi prototipe conveyor grading TBS yang mengintegrasikan pengukuran berat dan estimasi kelas kematangan berbasis citra ke modul ERP penerimaan secara otomatis, serta bagaimana kinerja grading dan keandalan pencatatan datanya?

Pertanyaan ini adalah baseline untuk diskusi dan penyusunan proposal; rumusan akhir harus diselaraskan dengan hasil tinjauan pustaka dan standar label yang dipilih.
