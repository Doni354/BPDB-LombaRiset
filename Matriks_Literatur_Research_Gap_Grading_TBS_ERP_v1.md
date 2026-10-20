# Matriks Literatur & Research Gap — Conveyor Grading TBS + IoT + ERP

**Versi:** 1.0  
**Tanggal penelusuran:** 20 Oktober 2026  
**Status:** Dokumen kerja untuk diskusi pembimbing dan fondasi proposal; bukan klaim novelty final yang telah divalidasi secara exhaustif.

## 1. Ringkasan arah riset

Gagasan yang sedang dieksplorasi adalah prototipe conveyor grading Tandan Buah Segar (TBS) kelapa sawit semi-manual. Satu tandan diproses dalam satu siklus; berat dibaca oleh sensor, citra tandan diperoleh dengan satu kamera melalui pengambilan foto berulang dari beberapa sudut, hasil visual diproses oleh AI, lalu semua hasil digabung berdasarkan satu ID pemeriksaan dan dikirim ke modul ERP penerimaan.

Batasan penting:
- Conveyor, machine vision, sensor berat, model AI untuk grading, dan integrasi Vision AI dengan ERP masing-masing sudah memiliki penelitian atau contoh implementasi.
- Karena itu, kebaruan tidak boleh diklaim sebagai “alat grading pertama”, “AI grading pertama”, atau “grading TBS terintegrasi ERP pertama”.
- Kandidat kontribusi yang lebih defensible ialah evaluasi komparatif pengambilan citra satu kamera dari beberapa sudut dibanding satu citra, digabung dengan pembacaan berat dan pencatatan ERP yang dapat ditelusuri, dengan target label yang sesuai standar grading Indonesia.
- Dataset publik yang ditemukan belum otomatis sesuai dengan kelas fraksi Indonesia F00–F5. Penelitian yang menargetkan fraksi tersebut memerlukan pemetaan label yang valid dan kemungkinan pengumpulan data lokal berlabel ahli.

## 2. Matriks penelitian dan sistem terdahulu

| No. | Sumber | Fokus dan metode yang dilaporkan | Data/hasil utama | Keterbatasan/hal yang belum dibuktikan dari sumber publik | Implikasi bagi usulan |
|---|---|---|---|---|---|
| 1 | Makky & Soni (2013), *Development of an automatic grading machine for oil palm fresh fruits bunches (FFBs) based on machine vision*. Computers and Electronics in Agriculture 93, 129–139. DOI: https://doi.org/10.1016/j.compag.2013.02.008 | Mesin grading di lokasi menggunakan subsistem mekanis, pengolahan citra, deteksi, dan kontrol. Memakai standar Indonesian Oil Palm Research Institute (IOPRI) pada studi tersebut. | Pengujian 465 TBS; klasifikasi diterima/ditolak dilaporkan 93,53%, klasifikasi fraksi 88,7%, estimasi berat rata-rata R² 81,39%; waktu pemeriksaan yang dilaporkan sekitar 1 TBS/5 detik. | Fokus yang dijelaskan publikasi adalah mesin grading dan machine vision. Abstrak yang ditinjau tidak melaporkan evaluasi integrasi ERP modern; ini bukan bukti bahwa semua sistem serupa tidak memiliki integrasi. | Conveyor + machine vision bukan novelty tersendiri. Perlu kontribusi yang lebih spesifik dan eksperimen yang berbeda. |
| 2 | Pipitsunthonsan et al. (2023), *Palm bunch grading technique using a multi-input and multi-label convolutional neural network*. Computers and Electronics in Agriculture 210, 107864. DOI: https://doi.org/10.1016/j.compag.2023.107864 | Grading dengan tiga input sensor: kamera RGB, sensor inframerah, dan load cell; model multi-input/multi-label CNN. | 1.575 gambar dari 14 varietas di empat lokasi perdagangan; empat kelas: overripe, ripe, under-ripe, unripe. Akurasi 90,26%; precision 89,86%; recall 89,54%; F1 89,68%. | Kelasnya empat kategori umum, bukan otomatis fraksi F00–F5 Indonesia. Abstrak publik yang ditinjau tidak menjelaskan evaluasi integrasi dengan ERP. | Multi-sensor + AI dan kombinasi citra/berat sudah pernah diteliti. Perbandingan harus berfokus pada aspek yang berbeda, bukan sekadar mengulang sensor fusion. |
| 3 | Suharjito & Junior et al. (2023), *Annotated Datasets of Oil Palm Fruit Bunch Piles for Ripeness Grading Using Deep Learning*. Scientific Data 10, 72. DOI: https://doi.org/10.1038/s41597-023-01958-x | Dataset citra/video dari area grading pabrik, direkam dengan smartphone dengan pendekatan pengambilan sudut 360° di sekitar tumpukan/pile TBS. Label ditentukan bersama ahli grading. | Dataset yang dilaporkan berisi 4.160 gambar hasil ekstraksi, 14.559 objek beranotasi dan enam kelas: unripe, under-ripe, ripe, overripe, empty bunch, abnormal fruit. Penulis membagi data train/validation/test 70:20:10 dan mengidentifikasi ketidakseimbangan kelas serta variasi data yang terbatas sebagai keterbatasan. | Dataset berfokus pada pile/kumpulan TBS; dokumen publik yang ditinjau tidak membuktikan adanya ID yang konsisten untuk satu tandan individual di seluruh video/sudut. Kelas juga tidak sama dengan tujuh kelas fraksi Indonesia. | Sumber publik yang berguna untuk baseline object detection dan memahami kelas kondisi TBS. Namun, tidak boleh langsung dipakai untuk mengklaim evaluasi multi-view per tandan individual atau klasifikasi F00–F5. |
| 4 | Kamal et al. (2024), *Machine vision for automated maturity grading of oil palm fruits: A systematic review*. Machine Graphics & Vision 33(2), 47–75. DOI: https://doi.org/10.22630/MGV.2024.33.2.3 | Tinjauan sistematis metode machine learning/deep learning untuk grading kematangan TBS. | Menyimpulkan CNN merupakan pendekatan dominan dalam klasifikasi kematangan karena kemampuannya mempelajari fitur kompleks; membahas keterbatasan dan prospek tiap pendekatan yang ditinjau. | Review tidak menguji prototipe usulan secara langsung. | Menguatkan bahwa klasifikasi visual telah ramai diteliti; model AI harus dipilih berdasarkan dataset dan pembanding, bukan klaim bahwa memakai CNN merupakan novelty. |
| 5 | mySAP365 AIX / Sawit Indonesia (13 Agustus 2026), *INTI 2026: mySAP365 AIX Tawarkan Vision AI untuk Digitalisasi Perkebunan Sawit*. URL: https://sawitindonesia.com/inti-2026-mysap365-aix-tawarkan-vision-ai-untuk-digitalisasi-perkebunan-sawit | Laporan industri mengenai Vision AI untuk grading kematangan, identifikasi tandan busuk/janjang kosong/brondolan, serta integrasi data citra dan proses panen dengan ERP. | Menunjukkan bahwa secara industri fungsi Vision AI untuk grading TBS yang dihubungkan dengan ERP sudah ditawarkan. | Artikel media bukan evaluasi ilmiah independen. Rincian perangkat grading, dataset, metrik akurasi, dan perbandingan eksperimen tidak tersedia secara rinci dalam publikasi yang ditinjau. | Integrasi AI grading–ERP secara umum bukan novelty yang aman. Usulan harus menekankan kontribusi dan evaluasi yang jelas serta mengakui adanya sistem industri yang beririsan. |
| 6 | Science Data Bank — dataset yang dirujuk Suharjito & Junior. DOI: https://doi.org/10.57760/sciencedb.j00001.00713 | Akses data video/citra yang menyertai artikel dataset 2023. | Berpotensi dipakai untuk baseline object detection/grading pada citra pile TBS. | Lisensi, struktur file aktual, anotasi per objek, dan apakah identitas tandan konsisten antar-frame harus diverifikasi langsung sebelum penggunaan. | Kandidat dataset publik utama; bukan pengganti pengumpulan data lokal jika sasaran riset adalah standar fraksi Indonesia dan multi-view per tandan individual. |

## 3. Sintesis: apa yang sudah ada dan apa yang belum bisa kita klaim

### Sudah ada berdasarkan sumber yang ditinjau
1. Mesin conveyor/mekanis untuk grading TBS berbasis machine vision.
2. Klasifikasi grading berbasis citra dan model CNN.
3. Fusi data kamera RGB, sensor inframerah, dan load cell untuk grading.
4. Dataset citra/video grading TBS dari area pabrik yang berisi beberapa kelas kematangan dan kondisi.
5. Laporan implementasi industri tentang Vision AI grading TBS yang diintegrasikan dengan ERP.

### Belum terbukti dari penelusuran awal ini
1. Bahwa pendekatan satu kamera dengan pengambilan berulang beberapa sudut lalu agregasi prediksi per tandan memberikan hasil lebih baik daripada satu foto pada konteks label Indonesia.
2. Bahwa satu pipeline prototipe murah yang menyatukan hasil timbang, hasil AI, ID pemeriksaan, verifikasi operator, dan catatan ERP telah diuji dengan metrik end-to-end yang transparan pada konteks target kita.
3. Bahwa dataset publik yang sudah ditemukan cukup untuk mengevaluasi klasifikasi fraksi F00–F5 atau menguji multi-view untuk tandan individual.

Pernyataan “belum terbukti dari penelusuran awal” **bukan** pernyataan bahwa belum pernah ada di mana pun. Full-text dan produk komersial perlu ditelaah lebih jauh sebelum gap dinyatakan final dalam proposal.

## 4. Kandidat research gap yang paling defensible

**Kandidat gap:** Dalam sumber ilmiah dan industri yang ditinjau, machine vision untuk grading TBS, fusi beberapa sensor, dataset video multi-sudut, serta integrasi Vision AI dengan ERP telah ada secara terpisah atau pada implementasi terkait. Namun, pada sumber yang ditinjau belum ditemukan evaluasi yang secara transparan membandingkan strategi pengambilan citra berulang dengan satu kamera dan agregasi prediksi per tandan versus satu citra, sambil mengaitkan hasil visual serta berat ke satu catatan pemeriksaan ERP yang memiliki jejak verifikasi, dengan acuan label yang sesuai standar grading Indonesia.

Ini merupakan hipotesis gap untuk diselidiki lebih lanjut, bukan klaim pasti bahwa sistem seperti itu belum pernah dibuat.

### Bentuk kebaruan yang diuji
- **Kebaruan metodologis terbatas:** membandingkan prediksi satu citra dengan agregasi prediksi beberapa citra dari tandan yang sama pada dataset yang memungkinkan identitas tandan ditelusuri.
- **Kontribusi sistem:** menggabungkan hasil citra/AI dan berat sensor dengan satu `inspectionId`, lalu menyimpan prediksi, hasil verifikasi, dan hasil akhir ke modul ERP secara otomatis.
- **Kontribusi evaluasi:** menilai baik kualitas klasifikasi maupun integritas data end-to-end (kelengkapan, duplikasi, latensi, dan asosiasi ID yang benar).
- **Konteks lokal:** bila ingin mengklaim kesesuaian dengan kelas fraksi Indonesia F00–F5, data harus memiliki label berdasarkan dokumen acuan yang tepat dan diverifikasi grader/ahli. Dataset kelas umum tidak boleh langsung dipetakan ke F00–F5 tanpa validasi.

## 5. Pertanyaan penelitian kerja

**RQ1.** Apakah agregasi hasil prediksi dari beberapa foto yang diambil menggunakan satu kamera pada tandan yang sama meningkatkan macro-F1 atau konsistensi klasifikasi dibandingkan penggunaan satu foto?

**RQ2.** Apakah data berat dan hasil AI dapat digabungkan secara andal ke satu rekaman pemeriksaan ERP, berdasarkan ID yang konsisten, tanpa kehilangan atau duplikasi data?

**RQ3.** Sejauh mana grade yang dihasilkan model sesuai dengan label referensi berdasarkan standar grading yang dipilih, dan kelas mana yang paling sering salah diklasifikasikan?

Catatan: RQ1 hanya dapat diuji secara sah jika tersedia data beberapa sudut dengan identitas tandan individual yang konsisten. Jika dataset publik tidak mendukung hal tersebut, RQ1 perlu dievaluasi pada data baru yang dikumpulkan di lokasi riset pada fase pelaksanaan; tahap konsep/prototipe awal hanya menguji alur sistem dan baseline yang didukung dataset.

## 6. Judul kerja

**“Pengembangan dan Evaluasi Prototipe Conveyor Grading TBS Berbasis Computer Vision dan Sensor Berat dengan Integrasi Otomatis ke Modul ERP Penerimaan.”**

Judul ini sengaja tidak mengklaim “grading seluruh fraksi Indonesia secara otomatis” sebelum dataset dan labelnya siap. Setelah acuan standar dan ruang lingkup kelas dipastikan, judul bisa dipersempit atau ditambah klaim multi-view.

## 7. Rencana penggunaan dataset

1. Unduh dan audit dataset Science Data Bank: pastikan lisensi, jenis anotasi, label, file video/gambar, dan apakah ID tandan individual dapat dipertahankan.
2. Telaah dataset Kaggle hanya sebagai pelengkap setelah metadata, sumber asli, lisensi, jumlah gambar per kelas, dan definisi label diperiksa. Dataset yang hanya punya label “ripe/unripe” tidak cukup untuk mengevaluasi tujuh fraksi Indonesia.
3. Bangun baseline AI dari kelas yang benar-benar tersedia pada dataset publik. Laporkan metrik per kelas, macro-F1, confusion matrix, serta akurasi; jangan hanya mengandalkan accuracy jika kelas tidak seimbang.
4. Pisahkan train/validation/test berdasarkan tandan atau video asal, bukan dengan mengacak frame dari video yang sama ke bagian data berbeda.
5. Jika target akhir mencakup fraksi lokal, rencanakan pengumpulan data berlabel ahli di lokasi riset pada fase implementasi. Ketiadaan akses tandan di kampus saat ini membatasi validasi mekanis lapangan, bukan alasan untuk mengklaim validasi telah dilakukan.

## 8. Batas klaim untuk proposal

**Boleh ditulis:** “Penelitian mengusulkan prototipe dan mengevaluasi penggabungan data grading visual serta berat ke dalam catatan ERP yang dapat ditelusuri; kontribusi dievaluasi melalui perbandingan metode pengambilan citra dan metrik integrasi.”

**Jangan ditulis sebelum bukti tersedia:**
- “Merupakan alat grading TBS pertama yang terintegrasi ERP.”
- “Belum ada penelitian yang menggabungkan kamera, AI, dan load cell.”
- “Akurasi pasti di atas 92%/95%.”
- “Dataset publik telah mewakili fraksi F00–F5 Indonesia.”
- “Sistem meningkatkan kualitas CPO/menurunkan ALB” tanpa pengukuran kualitas minyak sebagai luaran eksperimen.

## 9. Referensi utama

1. Makky, M., & Soni, P. (2013). Development of an automatic grading machine for oil palm fresh fruits bunches (FFBs) based on machine vision. *Computers and Electronics in Agriculture, 93*, 129–139. https://doi.org/10.1016/j.compag.2013.02.008
2. Pipitsunthonsan, P., Pan, L., Peng, S., Khaorapapong, T., Nakasathien, S., Channumsin, S., & Chongcheawchamnan, M. (2023). Palm bunch grading technique using a multi-input and multi-label convolutional neural network. *Computers and Electronics in Agriculture, 210*, 107864. https://doi.org/10.1016/j.compag.2023.107864
3. Suharjito, & Junior, F. A., et al. (2023). Annotated Datasets of Oil Palm Fruit Bunch Piles for Ripeness Grading Using Deep Learning. *Scientific Data, 10*, 72. https://doi.org/10.1038/s41597-023-01958-x
4. Kamal, A., Kamarudin, N. D., Ahmad, K. A. B., Rahayu, S. B., Isa, M. R. M., Makhtar, S. N., & Yaakub, Z. (2024). Machine vision for automated maturity grading of oil palm fruits: A systematic review. *Machine Graphics & Vision, 33*(2), 47–75. https://doi.org/10.22630/MGV.2024.33.2.3
5. Gunawan, I. (2026, August 13). INTI 2026: mySAP365 AIX Tawarkan Vision AI untuk Digitalisasi Perkebunan Sawit. *Sawit Indonesia*. https://sawitindonesia.com/inti-2026-mysap365-aix-tawarkan-vision-ai-untuk-digitalisasi-perkebunan-sawit
6. Dataset: Annotated Video Dataset of Oil Palm Fruit Bunch Piles for Ripeness Grading. Science Data Bank. https://doi.org/10.57760/sciencedb.j00001.00713
