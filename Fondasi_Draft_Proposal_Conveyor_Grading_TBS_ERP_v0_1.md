# Fondasi Draft Proposal Lomba Riset BPDP 2026–2027

## Pengembangan Prototipe Conveyor Grading TBS Berbasis Computer Vision dan Sensor Berat dengan Integrasi Otomatis ke Modul ERP Penerimaan

**Versi:** 0.1 — Fondasi konsep, belum proposal final  
**Tanggal penyusunan:** 20 Oktober 2026  
**Bidang kandidat:** Bidang 5 — Pascapanen & Pengolahan  
**Status:** Konsep dan metode awal; beberapa klaim serta metode masih perlu diverifikasi sebelum diajukan.

> **Catatan penting:** Dokumen ini merupakan bahan awal untuk diskusi tim dan dosen pembimbing. Ini belum proposal final dan belum menyatakan bahwa alat telah dibangun, data telah dikumpulkan, atau target kinerja telah tercapai. Tim saat ini belum memiliki lokasi pengambilan sampel TBS/grader ahli yang terkonfirmasi. Akses sampel dan validasi lapangan harus menjadi prasyarat pelaksanaan tahap eksperimen yang memerlukan tandan fisik.

---

# Ringkasan Konsep

Penelitian ini mengusulkan prototipe conveyor grading Tandan Buah Segar (TBS) kelapa sawit dengan proses pemeriksaan semi-manual. Sistem dirancang menggunakan satu kamera dengan pencahayaan terkendali untuk mengambil beberapa foto dari sudut berbeda, sensor berat berbasis load cell, serta komputer gateway untuk memproses citra dan menggabungkan keluaran pemeriksaan. Data hasil sensor dan prediksi computer vision selanjutnya dikirim secara otomatis ke modul ERP penerimaan melalui backend.

ERP yang dikembangkan dibatasi pada pengelolaan identitas pemeriksaan dan batch, data pemasok, hasil grading, verifikasi operator, bukti foto, serta laporan. Fokus penelitian bukan membangun ERP perusahaan secara lengkap, bukan menghitung penalti atau harga secara otomatis, dan bukan mengotomatisasi penyortiran fisik pada tahap MVP.

Kebaruan tidak akan diklaim sebagai “alat grading pertama” atau sekadar “grading AI yang terhubung ERP”. Literatur telah menunjukkan mesin grading berbasis machine vision, metode multi-input/multi-label berbasis beberapa sensor, dan dataset citra/video dengan sejumlah kelas grading. Selain itu, pemberitaan industri melaporkan implementasi AI grading yang terintegrasi dengan mySAP365. Karena itu, penelitian ini akan menguji kontribusi yang lebih spesifik: (1) membandingkan prediksi dari satu foto dengan agregasi prediksi beberapa foto dari tandan yang sama, jika data yang diperlukan tersedia; (2) menggabungkan hasil citra dan berat dalam satu rekaman pemeriksaan; dan (3) mengevaluasi kinerja grading serta ketertelusuran data dari proses pemeriksaan sampai ERP.

Dataset publik digunakan untuk baseline computer vision dan purwarupa perangkat lunak. Dataset tersebut tidak otomatis memiliki label fraksi F00–F5 Indonesia maupun identitas tandan yang memungkinkan pengujian multi-sudut per tandan. Oleh sebab itu, validasi klaim fraksi lokal dan eksperimen multi-sudut penuh memerlukan data yang sesuai serta label acuan dari penilai berpengalaman. Apabila akses data tersebut tidak diperoleh, ruang lingkup klaim harus dibatasi secara eksplisit.

# Usulan Judul

**Pengembangan dan Evaluasi Prototipe Conveyor Grading TBS Berbasis Computer Vision dan Sensor Berat dengan Integrasi Otomatis ke Modul ERP Penerimaan**

Alternatif judul yang lebih menonjolkan pertanyaan eksperimen:

**Evaluasi Agregasi Citra Multi-Sudut pada Prototipe Grading Tandan Buah Segar Kelapa Sawit dan Integrasinya dengan Sistem ERP Penerimaan**

Judul pertama lebih menggambarkan produk yang akan dibuat. Judul kedua lebih terarah pada kontribusi eksperimen apabila dataset multi-sudut per tandan dapat disediakan. Judul final dipilih setelah ruang lingkup data dan novelty disepakati.

# Kesesuaian dengan Prioritas Lomba

Panduan Teknis Lomba Riset Mahasiswa BPDP 2026–2027 memasukkan pada Bidang 5 (Pascapanen & Pengolahan) topik pengembangan teknologi panen dan pascapanen TBS yang dapat diintegrasikan dengan IoT dan AI, sistem traceability buah sawit berbasis IoT dan AI, serta alat deteksi kematangan buah sawit dan kualitas minyak sawit (*smart indicator*). Konsep ini paling dekat dengan topik pengembangan alat deteksi kematangan dan sistem pascapanen yang memanfaatkan IoT/AI.

Proposal harus menonjolkan masalah, kesenjangan dengan penelitian yang sudah ada, metode yang dapat diuji, manfaat yang terukur, serta prospek pengembangan. Panduan teknis menetapkan struktur proposal yang terdiri dari abstrak, Bab 1 Pendahuluan, Bab 2 Studi Pustaka, Bab 3 Metode Riset, Bab 4 Luaran Riset, Bab 5 Jadwal Kegiatan, Bab 6 Biaya dan Jadwal Penelitian, Daftar Pustaka, dan Lampiran. Batas panjang isi adalah maksimum 20 halaman di luar sampul, lembar pengesahan, daftar isi, dan lampiran. Ketentuan format dan rincian akhir wajib mengikuti dokumen resmi yang berlaku.

Pengumuman resmi BPDP mencantumkan batas pengajuan 30 Oktober 2026. Karena tenggat sudah dekat, dokumen ini memprioritaskan fondasi konseptual dan penelitian terdahulu; rincian anggaran dan lampiran harus diselesaikan setelah perangkat, kebutuhan sampel, dan kegiatan penelitian ditetapkan.

---

# ABSTRAK — Draf Awal

Penilaian mutu Tandan Buah Segar (TBS) kelapa sawit berperan dalam proses penerimaan bahan baku dan pengendalian kualitas. Penilaian visual secara manual dapat dipengaruhi kondisi pengamatan dan perbedaan penilai, sementara hasil pemeriksaan perlu dicatat agar dapat ditelusuri kembali pada proses penerimaan. Penelitian terdahulu telah mengembangkan mesin grading berbasis machine vision dan pendekatan pembelajaran mendalam dengan masukan multisensor. Dengan demikian, pengembangan sistem baru perlu berfokus pada kontribusi yang terukur, bukan hanya menggabungkan kamera, sensor, dan aplikasi.

Penelitian ini bertujuan mengembangkan serta mengevaluasi prototipe conveyor grading TBS semi-manual yang menggabungkan computer vision, sensor berat, dan integrasi otomatis ke modul ERP penerimaan. Prototipe menggunakan satu kamera dengan pencahayaan terkendali untuk mengambil beberapa citra, load cell untuk pengukuran berat, komputer gateway untuk pemrosesan citra dan penggabungan hasil, serta aplikasi web untuk menyimpan dan menampilkan data pemeriksaan. ERP dibatasi pada data pemeriksaan, batch, hasil grading, verifikasi operator, dan laporan.

Metode penelitian meliputi studi literatur dan pemetaan kriteria grading, pemilihan serta audit dataset publik, pembangunan baseline computer vision, perancangan perangkat pemeriksaan dan integrasi data, pengembangan modul ERP, serta pengujian kinerja. Evaluasi direncanakan mencakup precision, recall, macro-F1, akurasi klasifikasi, galat pengukuran berat, waktu pemeriksaan, kelengkapan data, keberhasilan sinkronisasi, dan konsistensi hubungan antara hasil pemeriksaan dengan identitasnya. Eksperimen perbandingan satu foto dengan beberapa foto dari tandan yang sama hanya dilakukan jika tersedia data multi-sudut dengan identitas tandan dan label yang dapat dipertanggungjawabkan.

Luaran yang ditargetkan berupa prototipe conveyor grading, model computer vision untuk kelas yang didukung data, modul ERP penerimaan, dokumentasi arsitektur, serta hasil evaluasi kinerja sistem. Penelitian tidak mengklaim penentuan kadar asam lemak bebas (ALB) secara langsung dari citra dan tidak menerapkan penalti harga secara otomatis. Validasi fraksi grading Indonesia membutuhkan label acuan sesuai standar dan keterlibatan penilai berpengalaman.

**Kata kunci:** tandan buah segar, grading, computer vision, IoT, ERP, ketertelusuran data.

---

# BAB 1. PENDAHULUAN

## 1.1 Latar Belakang — Draf

Tandan Buah Segar (TBS) merupakan bahan baku utama dalam pengolahan kelapa sawit. Kondisi dan kematangan TBS perlu dinilai pada proses penerimaan karena hasil penilaian digunakan untuk mengelompokkan mutu bahan baku dan mendukung keputusan operasional. Proses penilaian visual manual dapat menghadapi variasi hasil antarpenilai dan kondisi pengamatan. Makky dan Soni (2013) mengembangkan mesin grading TBS berbasis machine vision dengan menggunakan standar Indonesian Oil Palm Research Institute (IOPRI), serta melaporkan keberhasilan klasifikasi kelompok dan fraksi pada eksperimen mereka [1]. Studi tersebut menunjukkan bahwa otomasi grading telah diteliti lebih dari satu dekade, sehingga pengembangan sistem baru perlu mengidentifikasi kontribusi yang berbeda dan dapat dibuktikan.

Perkembangan computer vision dan deep learning membuka peluang untuk membantu proses pemeriksaan visual. Tinjauan sistematis Kamal dkk. (2024) menyebutkan bahwa convolutional neural network (CNN) menjadi pendekatan dominan dalam sejumlah penelitian klasifikasi kematangan buah sawit karena kemampuannya mempelajari fitur visual yang kompleks [2]. Pipitsunthonsan dkk. (2023) mengembangkan metode grading nondestruktif berbasis beberapa masukan sensor dan multi-label CNN serta melaporkan akurasi 90,26%, precision 89,86%, recall 89,54%, dan F1-score 89,68% pada eksperimennya [3]. Hasil ini berguna sebagai titik pembanding literatur, tetapi bukan tolok ukur yang langsung sebanding apabila penelitian ini memakai dataset, definisi kelas, atau kondisi pengambilan citra yang berbeda.

Ketersediaan data berlabel juga menjadi faktor penting. Suharjito dkk. (2023) mempublikasikan dataset citra dan video TBS dari area pabrik dengan enam kelas: *unripe*, *under-ripe*, *ripe*, *overripe*, *empty bunch*, dan *abnormal fruit* [4]. Dataset ini dapat membantu pembangunan baseline model dan purwarupa perangkat lunak. Namun, kelas tersebut belum otomatis setara dengan fraksi F00–F5 yang digunakan pada konteks Indonesia. Dataset berbentuk video atau tumpukan TBS juga tidak selalu menyediakan identitas unik per tandan pada setiap sudut, sehingga kesesuaiannya untuk eksperimen agregasi multi-sudut harus diperiksa sebelum digunakan.

Selain menghasilkan grade, suatu alat perlu mengaitkan hasil pemeriksaan dengan identitas pemeriksaan yang benar. Jika data berat, hasil citra, prediksi model, serta koreksi operator tersimpan secara terpisah, sistem perlu mekanisme agar semuanya dapat ditelusuri kembali pada satu pemeriksaan. Pencatatan digital juga telah diterapkan dalam sistem industri; pemberitaan mengenai kunjungan benchmarking PalmCo pada 2025, misalnya, melaporkan sistem AI grading TBS yang terintegrasi dengan platform mySAP365 dan menghasilkan audit trail penerimaan [5]. Oleh karena itu, integrasi AI dan ERP secara umum tidak dapat diklaim sebagai kebaruan dengan sendirinya.

Berdasarkan kondisi tersebut, penelitian ini mengusulkan prototipe conveyor grading semi-manual yang menggabungkan pengukuran berat, pengambilan citra berulang menggunakan satu kamera, pemrosesan computer vision, verifikasi operator, dan pencatatan otomatis ke modul ERP penerimaan. Fokus eksperimen adalah mengevaluasi apakah agregasi beberapa citra memberikan hasil klasifikasi yang lebih baik dibandingkan satu citra, serta apakah hasil sensor dan AI dapat dicatat secara lengkap dan konsisten dalam satu rekaman pemeriksaan. Penelitian juga akan menetapkan batas klaim sesuai dukungan dataset dan metode validasi yang tersedia.

## 1.2 Identifikasi Masalah

Berdasarkan telaah awal literatur, masalah penelitian dirumuskan sebagai masalah teknis yang dapat diuji, bukan asumsi bahwa seluruh PKS menerapkan proses yang sama:

1. Klasifikasi kematangan TBS berbasis machine vision telah diteliti, tetapi performa bergantung pada dataset, definisi kelas, dan kondisi citra yang digunakan.
2. Satu foto belum tentu merepresentasikan seluruh permukaan tandan. Perlu diuji apakah pengambilan foto berulang dari beberapa sudut dan agregasi prediksi memberikan peningkatan yang bermakna.
3. Hasil pemeriksaan dari kamera dan sensor berat harus dipasangkan dengan benar ke satu identitas pemeriksaan agar catatan ERP tidak kehilangan konteks atau tertukar.
4. Dataset publik tidak otomatis memenuhi kelas fraksi F00–F5 Indonesia maupun menyediakan pasangan multi-sudut per tandan yang dibutuhkan untuk semua eksperimen.
5. Belum ada akses lokasi, TBS fisik, atau grader ahli yang terkonfirmasi pada tahap penyusunan konsep. Karena itu, rencana validasi fisik merupakan ketergantungan penting dalam pelaksanaan penelitian.

## 1.3 Rumusan Masalah

1. Bagaimana merancang prototipe conveyor grading TBS yang menggabungkan pengukuran berat, pemrosesan citra, dan pencatatan hasil pemeriksaan secara otomatis ke modul ERP penerimaan?
2. Apabila data multi-sudut dengan identitas tandan tersedia, apakah agregasi hasil beberapa foto dari satu tandan meningkatkan performa klasifikasi dibandingkan penggunaan satu foto?
3. Seberapa andal proses integrasi data dalam mempertahankan kelengkapan, keunikan, dan keterkaitan hasil pengukuran dengan identitas pemeriksaan di ERP?
4. Sejauh mana hasil model sesuai dengan label acuan dari dataset yang dipakai, dan apa batas penggunaannya untuk mendukung grading TBS pada konteks Indonesia?

## 1.4 Tujuan Penelitian

### Tujuan umum

Mengembangkan dan mengevaluasi prototipe conveyor grading TBS berbasis computer vision dan sensor berat yang terintegrasi secara otomatis dengan modul ERP penerimaan.

### Tujuan khusus

1. Merancang alur pemeriksaan semi-manual dengan identitas pemeriksaan yang konsisten.
2. Mengembangkan baseline computer vision untuk kelas grading yang benar-benar didukung dataset.
3. Mengimplementasikan pengukuran berat dan pengiriman hasil sensor melalui perangkat IoT.
4. Mengembangkan modul ERP untuk penyimpanan hasil pemeriksaan, verifikasi, dan pelaporan.
5. Mengevaluasi performa klasifikasi, galat pengukuran berat, waktu pemeriksaan, serta keandalan pencatatan dan sinkronisasi data.
6. Merumuskan keterbatasan dan kebutuhan pengembangan untuk validasi pada standar grading Indonesia.

## 1.5 Manfaat yang Diharapkan

1. **Manfaat teknis:** tersedianya rancangan dan prototipe integrasi alat grading, AI, sensor, dan ERP.
2. **Manfaat operasional potensial:** mengurangi kebutuhan penyalinan data hasil pemeriksaan secara manual dan menyediakan histori hasil grading yang dapat ditelusuri.
3. **Manfaat penelitian:** menyediakan evaluasi terukur atas pendekatan agregasi citra dan integrasi data, disertai dokumentasi keterbatasan model dan dataset.
4. **Manfaat pengembangan lanjutan:** menjadi dasar penelitian lanjutan untuk validasi pada kondisi PKS dan standar grading yang digunakan di Indonesia.

Manfaat tersebut merupakan hasil yang diharapkan, bukan klaim pengurangan biaya, peningkatan rendemen CPO, atau peningkatan kesejahteraan yang sudah terbukti.

## 1.6 Batasan Penelitian

1. Prototipe menggunakan conveyor roller manual; pengalihan atau penyortiran fisik otomatis tidak termasuk MVP.
2. Perangkat utama mencakup satu kamera dengan pencahayaan terkendali, load cell, HX711, ESP32, dan komputer gateway.
3. Model AI dibatasi pada kelas yang didukung dataset dan label yang tersedia. Kelas publik tidak otomatis dipetakan ke fraksi F00–F5.
4. ERP dibatasi pada master pemasok, identitas pemeriksaan/batch, hasil grading, verifikasi, bukti visual, dan laporan penerimaan.
5. Sistem tidak mengukur ALB secara langsung dari foto dan tidak menerapkan formula penalti/harga otomatis pada MVP.
6. Klaim akurasi akhir hanya dinyatakan berdasarkan data uji dan metode evaluasi yang benar-benar dilakukan.
7. Pengujian grading fisik pada standar Indonesia memerlukan akses TBS nyata dan label referensi yang sah; jika akses tersebut tidak diperoleh, batas klaim harus disesuaikan.

---

# BAB 2. STUDI PUSTAKA DAN RESEARCH GAP

## 2.1 Konsep Grading TBS

Grading TBS adalah pengelompokan tandan berdasarkan karakteristik kematangan dan/atau mutu sesuai kriteria yang digunakan dalam konteks pengamatan. Pedoman dan regulasi yang berbeda dapat memiliki tujuan dan ruang lingkup berbeda: acuan klasifikasi kematangan tidak otomatis sama dengan aturan penerimaan atau pemotongan berat dalam pembelian TBS. Permentan Nomor 13 Tahun 2024 mengatur pembelian TBS produksi pekebun mitra, termasuk tata cara pembelian serta persyaratan penerimaan; regulasi itu perlu dibedakan dari referensi teknis klasifikasi visual yang digunakan untuk memberi label data [6].

Untuk baseline berbasis data publik, penelitian ini mempertimbangkan enam kelas dataset Suharjito dkk. (2023). Kelas tersebut cocok untuk eksplorasi model awal, tetapi tidak dapat diperlakukan sebagai padanan langsung setiap fraksi F00–F5. Penelitian yang mengklaim prediksi fraksi sesuai acuan Indonesia harus menggunakan label atau data yang telah diselaraskan dengan pedoman yang dipilih dan diverifikasi oleh ahli.

## 2.2 Computer Vision untuk Grading

Makky dan Soni (2013) mengembangkan mesin grading otomatis dengan subsistem mekanis, pemrosesan citra, deteksi, dan kontrol. Penelitian tersebut menggunakan prinsip machine vision nondestruktif dan melaporkan tingkat keberhasilan rata-rata 93,53% untuk klasifikasi kelompok serta 88,7% untuk klasifikasi fraksi [1].

Pipitsunthonsan dkk. (2023) mengembangkan metode grading dengan beberapa input sensor dan multi-input/multi-label CNN, dengan hasil akurasi 90,26% serta F1-score 89,68% pada eksperimennya [3]. Angka ini digunakan hanya sebagai konteks dari literatur. Perbandingan yang adil mengharuskan definisi kelas, sampel, dan protokol pengujian diketahui dan sebanding.

Kamal dkk. (2024) meninjau penelitian machine vision untuk grading kematangan buah sawit dan menempatkan CNN sebagai pendekatan dominan di antara teknik yang ditinjau [2]. Tinjauan itu membantu menunjukkan bahwa model AI untuk grading merupakan area yang telah berkembang; penelitian ini harus memperjelas kontribusi eksperimen dan sistem, bukan hanya penggunaan deep learning.

## 2.3 Dataset Publik dan Keterbatasannya

Suharjito dkk. (2023) menyediakan dataset citra/video dari area grading pabrik dan melaporkan enam kategori kelas. Data mencakup video satu kategori serta video dengan beberapa kategori tandan, dan labelnya divalidasi oleh ahli grading [4]. Dataset ini dapat digunakan untuk membangun baseline dan menguji pipeline pengolahan citra.

Sebelum menetapkan dataset sebagai dataset utama, tim harus memeriksa: (a) syarat lisensi; (b) struktur anotasi dan label; (c) jumlah sampel pada setiap kelas; (d) hubungan antara frame/video dan tandan; (e) potensi duplikasi atau frame yang sangat mirip; serta (f) apakah labelnya sejalan dengan target klasifikasi. Pemisahan data harus dilakukan berdasarkan video atau kelompok tandan/sumber, bukan membagi frame secara acak jika frame tersebut berasal dari video yang sama. Prosedur ini mengurangi risiko kebocoran data yang dapat membuat evaluasi terlalu optimistis.

Dataset Kaggle lain dapat dieksplorasi sebagai data tambahan, tetapi tidak boleh langsung digabungkan sebelum kelas, lisensi, sumber, dan kualitas label dibandingkan. Nama dataset atau klaim jumlah data dari halaman agregator harus diverifikasi langsung pada laman dataset.

## 2.4 Integrasi IoT dan ERP

Pada sistem yang diusulkan, ESP32 membaca data berat dari rangkaian load cell dan HX711. Kamera terhubung ke laptop/mini-PC yang berfungsi sebagai edge gateway untuk mengambil citra serta menjalankan pemrosesan computer vision. Gateway menyatukan data setiap stasiun berdasarkan `inspectionId`, kemudian mengirimkan rekaman ke backend.

ERP dibatasi sebagai modul penerimaan dan grading. Identitas pemeriksaan menghubungkan hasil timbangan, gambar, prediksi AI, koreksi operator, dan hasil akhir. Backend memvalidasi format dan identitas data sebelum disimpan. Sistem perlu mendukung pengiriman ulang secara aman saat koneksi terputus agar tidak menghasilkan duplikasi catatan.

Pemberitaan mengenai sistem grading AI yang terintegrasi dengan mySAP365 di PKS PGK Jambi pada 2025 memperlihatkan bahwa grading AI dan ERP telah pernah dihubungkan dalam implementasi industri [5]. Karena itu, integrasi ERP tidak menjadi klaim novelty tunggal. Nilai penelitian harus muncul dari hipotesis eksperimen serta evaluasi sistem yang spesifik.

## 2.5 Matriks Penelitian Terdahulu

| Sumber | Fokus/Metode | Hasil atau kontribusi yang dilaporkan | Implikasi dan celah yang perlu diuji |
|---|---|---|---|
| Makky & Soni (2013) [1] | Mesin grading TBS berbasis machine vision; subsistem mekanis, pemrosesan citra, deteksi, dan kontrol | Rata-rata keberhasilan klasifikasi kelompok 93,53% dan fraksi 88,7% | Conveyor/mesin grading dan klasifikasi machine vision bukan konsep baru. Bandingkan dengan pendekatan mereka secara spesifik. |
| Pipitsunthonsan dkk. (2023) [3] | Grading nondestruktif menggunakan beberapa masukan sensor serta multi-input/multi-label CNN | Akurasi 90,26%; precision 89,86%; recall 89,54%; F1-score 89,68% | Sensor + AI untuk grading sudah diteliti. Perlu pertanyaan eksperimen yang lebih sempit dan evaluasi yang adil. |
| Suharjito dkk. (2023) [4] | Dataset video/citra grading area pabrik, enam kelas | Dataset beranotasi yang divalidasi ahli untuk pengembangan deteksi dan klasifikasi | Memungkinkan baseline, tetapi belum tentu menyediakan identitas tandan dan label fraksi Indonesia untuk eksperimen multi-sudut. |
| Kamal dkk. (2024) [2] | Tinjauan sistematis machine vision untuk kematangan sawit | Memetakan pendekatan ML/DL dan mengidentifikasi CNN sebagai pendekatan dominan pada literatur yang ditinjau | Membutuhkan pembanding yang jelas dan pengujian pada kondisi data yang spesifik. |
| Pemberitaan sistem mySAP365 (2025) [5] | AI grading TBS terintegrasi dengan ERP untuk penerimaan dan audit trail | Melaporkan integrasi grading AI dengan pencatatan penerimaan dan pelaporan mutu | Integrasi AI–ERP secara umum bukan novelty yang dapat diklaim sebagai yang pertama. |

## 2.6 Sintesis Kesenjangan Penelitian

Berdasarkan sumber di atas, belum tepat menyatakan bahwa mesin grading, penggunaan multi-sensor, AI grading, atau integrasi ERP belum pernah dilakukan. Kesenjangan yang akan diuji dalam penelitian ini lebih sempit:

1. **Eksperimen agregasi citra:** membandingkan klasifikasi dari satu foto dengan agregasi prediksi dari beberapa foto yang diambil pada sudut berbeda dari tandan yang sama. Ini hanya dapat dilakukan jika data mendukung pemadanan foto terhadap tandan yang sama. Dataset publik berbentuk tumpukan/video tidak otomatis memenuhi kebutuhan tersebut.
2. **Keterkaitan data end-to-end:** merancang penggabungan berat sensor, hasil citra/AI, identitas pemeriksaan, verifikasi, dan hasil akhir dalam satu rekaman ERP; lalu mengukur kelengkapan, duplikasi, serta keberhasilan sinkronisasi.
3. **Batas penerapan kelas:** menilai bagaimana kelas dataset publik dapat digunakan untuk baseline dan menjelaskan keterbatasan pemetaan ke fraksi lokal. Penelitian ini tidak akan mengklaim klasifikasi F00–F5 Indonesia tanpa label referensi yang sesuai.

Dengan demikian, kebaruan yang diajukan adalah **hipotesis kontribusi berupa evaluasi agregasi beberapa foto dari satu kamera dalam alur grading per tandan, yang dipadukan dengan hasil sensor berat dan pencatatan ERP yang dapat ditelusuri**. Ini bukan klaim prioritas absolut. Sebelum menyebutnya sebagai novelty final, tim perlu menyelesaikan pencarian literatur lanjutan, termasuk pencarian terhadap sistem multi-view/single-camera dan platform grading terintegrasi yang relevan.

---

# BAB 3. METODE RISET — RANCANGAN AWAL

## 3.1 Jenis dan Pendekatan

Penelitian menggunakan pendekatan rekayasa dan eksperimen prototipe (*research and development*). Pekerjaan dibagi menjadi kajian literatur, audit dataset, pembuatan baseline AI, pengembangan prototipe perangkat, integrasi aplikasi, dan evaluasi kuantitatif. Tahap yang memerlukan sampel TBS nyata bergantung pada ketersediaan akses dan label referensi; keadaan tersebut belum dikonfirmasi pada saat fondasi proposal ini dibuat.

## 3.2 Tahap Penelitian

### Tahap 1 — Verifikasi acuan grading dan kebutuhan sistem

1. Mengkaji pedoman klasifikasi kematangan dan ketentuan pembelian/penerimaan TBS.
2. Memisahkan label fraksi kematangan dari kriteria mutu fisik dan keputusan penerimaan.
3. Menentukan fungsi MVP: pengukuran berat, klasifikasi visual yang didukung dataset, identitas pemeriksaan, verifikasi operator, dan catatan ERP.
4. Menetapkan data yang diperlukan, risiko, dan kondisi yang membuat suatu klaim dapat diuji.

### Tahap 2 — Audit dan persiapan dataset

1. Memeriksa lisensi, label, ukuran, sebaran kelas, dan metadata dataset publik.
2. Membersihkan data duplikat atau data yang tidak sesuai kriteria.
3. Membuat pemisahan training, validation, dan testing pada tingkat video/sumber/tandan, bukan acak per frame bila terdapat hubungan antarframe.
4. Mencatat keterbatasan dataset terhadap kelas F00–F5 Indonesia.
5. Menetapkan apakah eksperimen multi-sudut per tandan bisa dilakukan dari dataset yang tersedia. Jika tidak, eksperimen ini menunggu data baru yang beridentitas per tandan.

### Tahap 3 — Pengembangan baseline AI

1. Membuat baseline klasifikasi/deteksi menggunakan kelas yang benar-benar didukung dataset.
2. Melakukan preprocessing citra yang wajar, termasuk resize dan augmentasi hanya pada data training.
3. Memilih satu model awal berdasarkan bentuk anotasi dan sumber daya komputasi; arsitektur final tidak dikunci sebelum audit data.
4. Mengukur akurasi, precision, recall, macro-F1, confusion matrix, dan performa setiap kelas.
5. Menghindari penggunaan frame dari sumber yang sama pada training dan test.

### Tahap 4 — Rancangan dan pembuatan prototipe perangkat

1. Merancang conveyor roller manual dan satu titik pemeriksaan per tandan.
2. Merancang platform load cell yang jalur bebannya terisolasi dari rangka conveyor saat pengukuran.
3. Menghubungkan load cell ke HX711 dan ESP32.
4. Menggunakan satu kamera USB dengan pencahayaan LED terkendali; operator mengambil beberapa foto dari sudut berbeda.
5. Menggunakan laptop/mini-PC sebagai gateway untuk memperoleh citra, menjalankan AI, menggabungkan hasil sensor, dan mengirimkan hasil pemeriksaan.
6. Melakukan kalibrasi berat menggunakan timbangan pembanding apabila perangkat fisik telah tersedia.

### Tahap 5 — Pengembangan backend dan ERP

Modul awal mencakup:

- Master pemasok (minimal untuk demonstrasi).
- Penerimaan dan batch.
- Pemeriksaan per tandan.
- Data berat dan metadata perangkat.
- Prediksi AI serta referensi foto.
- Verifikasi/koreksi operator.
- Hasil akhir grading dan histori.
- Dashboard dan laporan sederhana.

Setiap pemeriksaan memiliki `inspectionId` unik dan dapat memiliki `batchId`. Data prediksi AI, koreksi, dan hasil akhir dipisahkan. API memvalidasi struktur, identitas, dan status pemeriksaan sebelum data disimpan. Bila memungkinkan, gateway menyimpan antrean lokal agar data tidak hilang saat internet terputus; pengiriman ulang menggunakan ID yang konsisten untuk mencegah duplikasi.

### Tahap 6 — Pengujian integrasi dan evaluasi sistem

Pengujian mencakup:

1. Galat pengukuran berat terhadap timbangan referensi.
2. Kinerja AI pada data testing yang tidak digunakan saat pelatihan.
3. Perbandingan single-image versus multi-image aggregation jika data multi-sudut per tandan tersedia.
4. Kelengkapan rekaman ERP dan konsistensi pemadanan ID.
5. Keberhasilan sinkronisasi, duplikasi, kehilangan data, dan latensi dari akhir pemeriksaan ke rekaman ERP.
6. Waktu pemeriksaan per tandan dan jumlah intervensi operator.

## 3.3 Rencana Data dan Sampel

### Dataset publik

Dataset utama kandidat adalah Suharjito dkk. (2023) karena menyediakan citra/video dari lingkungan grading pabrik dengan enam kelas dan label yang divalidasi ahli [4]. Dataset Kaggle lain dapat digunakan sebagai kandidat tambahan setelah struktur, lisensi, definisi kelas, dan sumber data diperiksa.

Jumlah sampel final **belum ditetapkan** sampai audit dataset selesai. Unit data harus didefinisikan secara konsisten: objek/tandan, bukan hanya jumlah file atau frame. Jika satu tandan muncul di banyak frame, seluruh frame yang berkaitan harus tetap berada pada satu kelompok split.

### Data fisik dan label acuan

Jika memungkinkan selama pelaksanaan riset, citra TBS baru perlu dikumpulkan menggunakan satu kamera dan beberapa sudut pengambilan. Setiap tandan diberi ID unik dan label berdasarkan penilaian grader berpengalaman menggunakan dokumen acuan yang disepakati. Penilai perlu mendokumentasikan ketidakpastian atau perbedaan penilaian.

Karena lokasi dan mitra belum dikonfirmasi, rencana ini belum boleh menuliskan nama PKS, jumlah tandan, atau ketersediaan grader seolah-olah sudah tersedia. Jika data baru tidak dapat diperoleh, kesimpulan dibatasi pada dataset publik dan prototipe perangkat lunak/integrasi; klaim tentang validitas grading fraksi Indonesia tidak dibuat.

## 3.4 Variabel dan Metrik Evaluasi

| Aspek | Metrik | Data pembanding |
|---|---|---|
| Klasifikasi AI | Akurasi, precision, recall, macro-F1, confusion matrix, hasil per kelas | Label dataset/label grader yang sesuai |
| Agregasi citra | Perbedaan macro-F1 dan konsistensi hasil antara satu foto dan beberapa foto per tandan | Tandan yang sama, bila identitas dan foto multi-sudut tersedia |
| Pengukuran berat | Galat absolut, galat relatif, repeatability | Timbangan referensi |
| Integrasi | Persentase pengiriman sukses, kelengkapan field, duplikasi, kehilangan/rekaman tertukar | Log gateway dan database ERP |
| Latensi | Waktu dari pemeriksaan selesai hingga data tersedia di ERP | Timestamp proses dan backend |
| Proses | Waktu pemeriksaan per tandan dan jumlah koreksi operator | Observasi pada prototipe dan, bila tersedia, proses pembanding |

Target awal AI: akurasi setidaknya 90% sebagai sasaran sementara, dengan target aspiratif ≥92%. Angka 90,26% dari Pipitsunthonsan dkk. (2023) hanya menjadi konteks pembanding literatur [3], bukan pembanding langsung jika dataset dan kelas berbeda. Macro-F1 harus dilaporkan bersama akurasi untuk mengungkap performa pada kelas yang jumlahnya sedikit. Target final ditinjau kembali setelah pilot dan audit distribusi kelas.

## 3.5 Arsitektur Teknologi Konseptual

- **Perangkat:** conveyor roller manual, platform load cell, HX711, ESP32, kamera USB, LED diffuse.
- **Edge gateway:** Python, OpenCV, model computer vision, penyatuan hasil sensor/citra.
- **Komunikasi:** HTTP/JSON pada jaringan lokal antara ESP32 dan gateway; HTTPS dari gateway ke backend.
- **Backend:** Node.js API melalui Firebase Cloud Functions.
- **Database:** Cloud Firestore untuk data pemasok, batch, pemeriksaan, hasil stasiun, perangkat, dan verifikasi.
- **Penyimpanan media:** Firebase Storage untuk foto pemeriksaan.
- **Aplikasi:** Next.js dan Firebase Authentication untuk modul ERP.

Arsitektur ini merupakan pilihan rancangan awal. Implementasi rinci, BOM, kapasitas load cell, dan tipe model akan ditetapkan setelah estimasi berat, format data, dataset, dan kebutuhan prototipe dipastikan.

## 3.6 Risiko dan Mitigasi

| Risiko | Dampak | Mitigasi |
|---|---|---|
| Dataset publik tidak sesuai dengan fraksi Indonesia | Model tidak dapat diklaim mengklasifikasi F00–F5 | Batasi baseline pada label dataset dan rencanakan data berlabel lokal sebelum membuat klaim fraksi Indonesia. |
| Dataset tidak memiliki identitas tandan lintas sudut | Eksperimen satu foto vs multi-foto tidak dapat diuji secara sah | Audit metadata terlebih dahulu; bila tidak memadai, kumpulkan data baru atau ubah novelty yang diusulkan. |
| Kelas tidak seimbang | Akurasi dapat menutupi kegagalan pada kelas minoritas | Laporkan macro-F1, recall/precision per kelas, dan confusion matrix. |
| TBS fisik dan grader tidak tersedia | Validasi lapangan tidak dapat dilakukan | Nyatakan sebagai ketergantungan; jangan mengklaim validasi lapangan sebelum akses dipastikan. |
| Data ganda atau tertukar pada integrasi | Laporan ERP tidak dapat dipercaya | Gunakan `inspectionId` konsisten, validasi payload, dan mekanisme idempotensi. |
| Pencahayaan/orientasi memengaruhi prediksi | Performa turun pada kondisi berbeda | Gunakan pencahayaan terkendali, pengambilan beberapa sudut, dan uji robustness jika sampel memadai. |
| Lingkup MVP terlalu luas | Jadwal dan biaya meningkat | Wajibkan otomatisasi berat + baseline visual + integrasi; cacat lain hanya ditambahkan jika data dan waktu tersedia. |

---

# BAB 4. LUARAN RISET

Luaran yang ditargetkan:

1. Dokumen arsitektur perangkat, edge gateway, backend, dan modul ERP.
2. Prototipe conveyor grading TBS semi-manual dengan pengukuran berat dan stasiun inspeksi visual.
3. Baseline model computer vision untuk kelas yang didukung dataset.
4. Modul ERP penerimaan dan grading yang dapat menyimpan data hasil pemeriksaan, prediksi, verifikasi, dan histori.
5. Dataset kerja dan dokumentasi protokol pemisahan data, sejauh lisensi dan hak penggunaan mengizinkan.
6. Laporan evaluasi performa AI, sensor berat, alur integrasi, dan keterbatasan validasi.
7. Rekomendasi pengembangan lanjutan menuju validasi di lingkungan PKS.

Luaran akhir tidak mencakup klaim pengukuran ALB langsung dari citra, klaim peningkatan rendemen CPO tanpa uji pengolahan, atau perhitungan penalti/harga otomatis pada MVP.

---

# BAB 5. JADWAL KEGIATAN — RANCANGAN TENTATIF

Jadwal berikut merupakan contoh alokasi enam bulan sejak pelaksanaan riset disetujui; durasi harus disesuaikan dengan ketentuan BPDP dan ketersediaan dana.

| Kegiatan | Bln 1 | Bln 2 | Bln 3 | Bln 4 | Bln 5 | Bln 6 |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| Verifikasi acuan grading dan literatur | ● | ● | | | | |
| Audit dataset dan pembuatan baseline AI | ● | ● | ● | | | |
| Rancangan mekanis dan pengadaan komponen | ● | ● | | | | |
| Pembuatan conveyor dan integrasi sensor | | ● | ● | | | |
| Pengembangan backend dan ERP | | ● | ● | ● | | |
| Integrasi AI–sensor–ERP | | | ● | ● | | |
| Uji coba, kalibrasi dan evaluasi | | | | ● | ● | |
| Analisis hasil, laporan, perbaikan prototipe | | | | | ● | ● |
| Penyusunan luaran akhir | | | | | ● | ● |

---

# BAB 6. BIAYA DAN KEBUTUHAN SUMBER DAYA — KERANGKA AWAL

Anggaran final belum disusun karena spesifikasi alat dan kebutuhan data belum dibekukan. Komponen biaya yang perlu dihitung setelah desain MVP disepakati:

1. Rangka conveyor, roller, platform timbang, dudukan kamera, serta material mekanis.
2. Load cell, HX711, ESP32, catu daya, kabel, konektor, dan komponen pendukung.
3. Kamera USB dan pencahayaan LED serta ruang inspeksi.
4. Material prototipe dan komponen pengganti untuk kalibrasi/perbaikan.
5. Komputasi/penyimpanan dan biaya layanan aplikasi jika melampaui tingkat gratis.
6. Pengumpulan data dan validasi oleh penilai berpengalaman apabila akses dan kerja sama tersedia.
7. Dokumentasi, pengujian, dan penyusunan luaran.

Tidak disarankan mencantumkan biaya sensor tambahan untuk setiap cacat visual sebelum parameter tersebut dipastikan masuk MVP. Penetapan anggaran harus mengikuti batas pendanaan, format resmi, dan bukti harga yang dapat dipertanggungjawabkan.

---

# Klaim yang Dapat dan Belum Dapat Ditulis

## Dapat ditulis berdasarkan sumber yang sudah diperiksa

- Machine vision untuk grading TBS telah diteliti sejak paling tidak 2013 [1].
- Metode multi-input/multi-label CNN untuk grading TBS telah dipublikasikan dan melaporkan akurasi 90,26% pada eksperimennya [3].
- Dataset publik enam kelas dari video/citra grading area pabrik tersedia untuk penelitian computer vision [4].
- Literatur sistematis mengulas beragam teknik machine vision dan pembelajaran mendalam untuk grading kematangan [2].
- Pemberitaan industri menyebut implementasi AI grading TBS terhubung dengan platform mySAP365 [5].
- Bidang 5 BPDP 2026–2027 mencakup teknologi pascapanen TBS yang terintegrasi IoT/AI serta alat deteksi kematangan [7].

## Belum boleh diklaim tanpa bukti tambahan

- Sistem ini merupakan alat grading TBS pertama yang terintegrasi ERP.
- Tidak ada penelitian terdahulu yang menggunakan beberapa foto dari satu kamera untuk grading.
- Model akan mencapai akurasi ≥92% pada kelas grading Indonesia.
- Dataset publik dapat langsung menghasilkan klasifikasi fraksi F00–F5.
- Prototipe meningkatkan rendemen CPO, menurunkan ALB, atau meningkatkan pendapatan.
- Semua cacat fisik TBS dapat dideteksi otomatis.
- Sistem sudah diuji atau divalidasi pada PKS.

---

# DAFTAR PUSTAKA AWAL

[1] Makky, M., & Soni, P. (2013). Development of an automatic grading machine for oil palm fresh fruits bunches (FFBs) based on machine vision. *Computers and Electronics in Agriculture, 93*, 129–139. https://doi.org/10.1016/j.compag.2013.02.008

[2] Kamal, A., Kamarudin, N. D., Bin Ahmad, K. A., Rahayu, S. B., Mohd Isa, M. R., Makhtar, S. N., & Yaakub, Z. (2024). Machine vision for automated maturity grading of oil palm fruits: A systematic review. *Machine Graphics & Vision, 33*(2), 47–75. https://doi.org/10.22630/MGV.2024.33.2.3

[3] Pipitsunthonsan, P., Pan, L., Peng, S., Khaorapapong, T., Nakasathien, S., Channumsin, S., & Chongcheawchamnan, M. (2023). Palm bunch grading technique using a multi-input and multi-label convolutional neural network. *Computers and Electronics in Agriculture, 210*, 107864. https://doi.org/10.1016/j.compag.2023.107864

[4] Suharjito, S., Junior, F. A., Koeswandy, Y. P., et al. (2023). Annotated datasets of oil palm fruit bunch piles for ripeness grading using deep learning. *Scientific Data, 10*, Article 72. https://doi.org/10.1038/s41597-023-01958-x. Dataset tersedia melalui Science Data Bank: https://doi.org/10.57760/sciencedb.j00001.00713. Artikel menyebut lisensi CC BY 4.0; ketentuan untuk komponen data individual tetap harus diperiksa.

[5] InfoSAWIT. (2025, 26 September). PalmCo PTPN 4 benchmarking sistem grading AI TBS di PKS PGK Jambi. https://www.infosawit.com/2025/09/26/palmco-ptpn-4-benchmarking-sistem-grading-ai-tbs-di-pks-pgk-jambi/

[6] Kementerian Pertanian Republik Indonesia. (2024). Peraturan Menteri Pertanian Nomor 13 Tahun 2024 tentang Pembelian Tandan Buah Segar Kelapa Sawit Produksi Pekebun Mitra. JDIH Kementerian Pertanian: https://jdih.pertanian.go.id/peraturan/permentan-no13-tahun-2024

[7] Badan Pengelola Dana Perkebunan (BPDP). (2026). Panduan Teknis Proposal Lomba Riset Tingkat Mahasiswa 2026–2027 (dokumen yang diberikan dalam percakapan); dan Pengumuman Call for Proposal Lomba Riset Tingkat Mahasiswa 2026–2027. https://www.bpdp.or.id/pengumuman-call-for-proposal-lomba-riset-tingkat-mahasiswa-2026

[8] Badan Pengelola Dana Perkebunan (BPDP). (2026, 26 Juni). Pengumuman 10 Besar Lomba Riset Tingkat Mahasiswa 2025–2026. https://www.bpdp.or.id/pengumuman-10-besar-lomba-riset-tingkat-mahasiswa-2025-2026

---

# Daftar Pekerjaan yang Harus Diselesaikan Sebelum Proposal Final

- [ ] Cocokkan kembali isi proposal dengan format resmi BPDP 2026–2027 dan aturan halaman.
- [ ] Verifikasi dokumen teknis yang benar untuk label kematangan/fraksi Indonesia; jangan menyamakan acuan budidaya, standar grading, dan aturan pembelian.
- [ ] Audit dataset utama: lisensi, kelas, jumlah unit tandan, label, dan struktur video.
- [ ] Pastikan apakah dataset bisa mendukung perbandingan single-image versus multi-image pada tandan yang sama.
- [ ] Putuskan apakah target utama baseline memakai enam kelas publik atau label fraksi Indonesia. Jangan mencampur dua skema label.
- [ ] Tentukan protokol pelabelan dan sumber label acuan untuk validasi.
- [ ] Periksa literatur lanjutan dan sistem komersial yang paling dekat sebelum mengunci klaim novelty.
- [ ] Tentukan spesifikasi dan harga komponen berdasarkan rentang berat serta desain platform timbang.
- [ ] Tentukan anggaran serta jadwal yang cocok dengan aturan lomba dan kemungkinan akses sampel.
- [ ] Konfirmasi terminologi, ruang lingkup, dan fokus penelitian dengan Bu Arni sebelum proposal difinalisasi.
