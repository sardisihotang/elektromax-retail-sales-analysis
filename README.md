# ElektroMax — Dashboard Analisis Penjualan Ritel & Pelanggan

> Proyek portofolio pembelajaran untuk mempelajari persiapan data, pemodelan data, analisis KPI, dan pembuatan laporan interaktif menggunakan Microsoft Power BI.

## Gambaran Umum Proyek
Proyek ini bertujuan untuk mengeksplorasi dan menganalisis dataset penjualan pada bisnis ritel elektronik fiktif bernama **ElektroMax**. Dashboard disusun menjadi tiga halaman utama, yaitu Executive Overview, Product & Store, dan Customer Analysis.

Dataset Excel yang digunakan terdiri dari **7 tabel** dengan periode data **1 Januari 2023–31 Desember 2025**. Tabel transaksi (`FACT_PENJUALAN`) memiliki **56.748 baris sebelum proses penanganan data duplikat**. Proses analisis mencakup penghapusan duplikat berdasarkan primary key dan penyeragaman label status transaksi.

> **Keterangan pembelajaran:** Proyek ini dibuat sebagai bagian dari proses pembelajaran Data Analytics dengan menggunakan tutorial YouTube sebagai salah satu referensi. Kredit kepada channel tutorial dicantumkan pada bagian referensi pembelajaran.

## Pertanyaan Bisnis
- Bagaimana perkembangan kinerja penjualan bersih dari waktu ke waktu?
- Subkategori produk mana yang memberikan kontribusi penjualan bersih terbesar?
- Bagaimana perbandingan kontribusi penjualan antar toko dan wilayah?
- Segmen pelanggan mana yang memberikan kontribusi penjualan terbesar?
- Bagaimana distribusi transaksi berdasarkan metode pembayaran, promosi, dan status transaksi?

## Dataset
File Excel yang digunakan terdiri dari beberapa sheet berikut:
- `FACT_PENJUALAN`
- `DIM_PRODUK`
- `DIM_WAKTU`
- `DIM_PELANGGAN`
- `DIM_TOKO`
- `DIM_KARYAWAN`
- `DIM_PROMOSI`

**Sumber Dataset:** [Masukkan URL sumber dataset publik beserta informasi lisensi atau ketentuan penggunaannya.]

**Privasi Data:** Dataset pelanggan asli memuat informasi pribadi seperti nama, alamat email, dan nomor telepon. Informasi tersebut tidak boleh dipublikasikan secara terbuka. Gunakan dataset yang telah dianonimkan atau diagregasi, serta pastikan penggunaannya sesuai dengan ketentuan lisensi sumber data.

## Tools yang Digunakan
- Microsoft Excel — pemeriksaan dan eksplorasi awal dataset.
- Power Query — pembersihan dan transformasi data.
- Power BI Desktop — pemodelan data, pembuatan DAX measures, dashboard, dan visualisasi.

## Persiapan dan Pembersihan Data
Dataset diperiksa untuk mengetahui tipe data, nilai kosong (*missing values*), duplikasi primary key, serta ketidakkonsistenan penulisan kategori dan status transaksi.

Beberapa temuan dan proses yang dilakukan:
- Tabel `FACT_PENJUALAN` memiliki 56.748 baris dengan 20 data `penjualan_id` yang terduplikasi.
- Tabel `DIM_PRODUK` memiliki satu data `produk_id` yang terduplikasi.
- Ditemukan nilai kosong pada beberapa kolom. Penanganannya perlu disesuaikan dengan kebutuhan analisis dan makna bisnis dari masing-masing kolom.
- Menyeragamkan variasi status transaksi `selesai`, `SELESAI`, `Done`, `Sukses`, dan `Complete` menjadi `Selesai`. Variasi status retur diseragamkan menjadi `Retur` apabila memiliki makna yang sama.
- Menghapus atau menyamarkan informasi pribadi pelanggan sebelum dataset digunakan untuk publikasi.

Dokumentasi lebih lanjut dapat dilihat pada:
- [`data_cleaning.md`](documentation/data_cleaning.md)
- [`data_dictionary.md`](documentation/data_dictionary.md)

## Model Data
Dataset menggunakan struktur satu tabel fakta (`FACT_PENJUALAN`) yang terhubung dengan enam tabel dimensi, yaitu produk, waktu, pelanggan, toko, karyawan, dan promosi.

Diagram model data dapat dilihat pada [`data_model.png`](documentation/data_model.png).

Diagram tersebut menggambarkan rancangan hubungan antartabel berdasarkan kolom ID yang saling berhubungan. Kardinalitas relasi dan arah filter perlu disesuaikan serta diverifikasi kembali pada model Power BI yang digunakan.

## Halaman Dashboard
Dashboard terdiri dari tiga halaman utama:

1. **Executive Overview** — menampilkan KPI utama dan tren penjualan untuk memberikan gambaran umum kinerja bisnis.
2. **Product & Store** — menganalisis kontribusi subkategori produk, performa toko, wilayah, dan perbandingan margin keuntungan.
3. **Customer Analysis** — menganalisis segmen pelanggan, kelompok umur, jenis kelamin, promosi, dan metode pembayaran.

Screenshot dashboard dapat dilihat pada folder `screenshots/`:
- `executive_overview.png`
- `product_store.png`
- `customer_analysis.png`

## Temuan Awal dari Dataset
Hasil berikut dihitung dari dataset setelah mempertahankan satu baris untuk setiap `penjualan_id`, menyeragamkan status transaksi, dan hanya memasukkan transaksi berstatus `Selesai`.

Angka ini merupakan hasil analisis untuk keseluruhan periode tiga tahun, sehingga dapat berbeda dengan tampilan dashboard yang menggunakan filter tahun tertentu.

- Jumlah transaksi selesai: **48.182 transaksi**.
- Total penjualan bersih (`total_neto`): **Rp247,09 miliar**.
- Total laba kotor (`gross_profit`): **Rp76,31 miliar**.
- Gross Profit Margin (laba kotor dibagi penjualan bersih): **30,9%**.
- Subkategori dengan penjualan bersih tertinggi: **Televisi** (Rp62,92 miliar).
- Subkategori dengan penjualan bersih tertinggi kedua: **AC** (Rp60,28 miliar).
- Label segmen pelanggan dengan kontribusi penjualan terbesar: **Regular** (Rp124,32 miliar). Variasi penulisan seperti `Regular` dan `REGULAR` perlu diseragamkan sebelum hasil segmentasi ditafsirkan sebagai satu kategori.

Temuan tersebut bersifat deskriptif dan tidak menunjukkan hubungan sebab-akibat. Seluruh angka perlu divalidasi kembali setelah aturan pembersihan data ditetapkan dan disesuaikan dengan filter serta definisi KPI pada dashboard.

## Rekomendasi untuk Ditindaklanjuti
- Mengevaluasi persediaan dan strategi penjualan pada subkategori produk dengan kontribusi penjualan tertinggi.
- Menyeragamkan penulisan segmen pelanggan sebelum melakukan perbandingan antarsegmen.
- Mengevaluasi efektivitas promosi berdasarkan penjualan bersih dan laba dengan metode perbandingan yang jelas.
- Membandingkan kinerja toko menggunakan periode, status transaksi, dan definisi penjualan yang konsisten.

## Keterbatasan Analisis
- URL sumber dataset publik dan informasi lisensinya belum dicantumkan dalam dokumentasi proyek ini.
- Dataset memiliki nilai kosong dan penulisan kategori yang tidak konsisten sehingga keputusan pembersihan perlu didokumentasikan dan divalidasi.
- Beberapa data pelanggan menggunakan nilai placeholder seperti `—` yang tidak boleh dianggap sebagai kategori demografis sebenarnya.
- Hasil dashboard dapat berbeda dari hasil perhitungan keseluruhan periode apabila menggunakan filter tahun atau definisi KPI yang berbeda.
- Analisis ini bersifat deskriptif dan belum membuktikan adanya pengaruh sebab-akibat dari promosi maupun karakteristik pelanggan terhadap penjualan.

## Referensi Pembelajaran
- Channel YouTube: **@alvinowrp**

## Cara Melihat Proyek
1. Buka dashboard Power BI interaktif melalui tautan berikut: https://lnkd.in/g-3xF4Fp
2. Lihat dokumentasi dan screenshot dashboard pada folder `screenshots/`.
3. Buka file `.pbix` menggunakan Microsoft Power BI Desktop apabila file tersebut disertakan dalam repository.

## Pembuat
**Sardianto Sihotang**  
[GitHub](https://github.com/sardisihotang) · [LinkedIn](https://www.linkedin.com/in/sardianto-sihotang-a44350293/)
