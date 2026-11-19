# Data Dictionary

Descriptions below are inferred from column names and sample values in the supplied workbook. Confirm ambiguous business definitions with the dataset documentation before treating them as authoritative.

## FACT_PENJUALAN — transaction fact table

| Column | Description / likely meaning |
|---|---|
| `penjualan_id` | Unique transaction identifier; intended primary key |
| `produk_id` | Product key; links to `DIM_PRODUK` |
| `waktu_id` | Date key; links to `DIM_WAKTU` |
| `pelanggan_id` | Customer key; links to `DIM_PELANGGAN` |
| `toko_id` | Store key; links to `DIM_TOKO` |
| `karyawan_id` | Employee key; links to `DIM_KARYAWAN` |
| `promosi_id` | Promotion key; links to `DIM_PROMOSI` |
| `kuantitas` | Quantity purchased |
| `harga_satuan` | Unit selling price |
| `total_harga` | Gross line/transaction amount before discount, based on field name |
| `diskon_persen` | Discount percentage |
| `diskon_nominal` | Discount amount |
| `total_neto` | Net amount after discount |
| `hpp` | Cost of goods sold / product cost |
| `gross_profit` | Gross profit amount |
| `metode_bayar` | Payment method |
| `status_transaksi` | Transaction status |

## DIM_PRODUK — product dimension

| Column | Description / likely meaning |
|---|---|
| `produk_id` | Product primary key |
| `kode_produk` | Product code/SKU |
| `nama_produk` | Product name |
| `kategori` | Product category |
| `subkategori` | Product subcategory |
| `merek` | Brand |
| `tipe` | Product type/technology |
| `ukuran` | Product size |
| `watt` | Power rating in watts |
| `warna` | Product color |
| `garansi_tahun` | Warranty duration in years |
| `harga_normal` | Normal/list price |
| `harga_pokok` | Product cost |
| `status_aktif` | Product active-status indicator |

## DIM_WAKTU — date dimension

| Column | Description / likely meaning |
|---|---|
| `waktu_id` | Date key; values resemble YYYYMMDD |
| `tanggal` | Calendar date |
| `hari` | Day name |
| `nomor_hari` | Day number (confirm whether weekday numbering) |
| `minggu_ke` | Week number |
| `bulan` | Month name |
| `nomor_bulan` | Month number |
| `kuartal` | Quarter |
| `semester` | Half-year period |
| `tahun` | Year |
| `is_weekend` | Weekend indicator |
| `is_harbol` | Harbolnas indicator |
| `is_libur_nasional` | National holiday indicator |

## DIM_PELANGGAN — customer dimension

| Column | Description / likely meaning |
|---|---|
| `pelanggan_id` | Customer primary key |
| `kode_pelanggan` | Customer code |
| `nama_pelanggan` | Customer name — direct identifier; do not publish |
| `jenis_kelamin` | Gender category as supplied |
| `tgl_lahir` | Date of birth |
| `kelompok_umur` | Age group |
| `kota` | City |
| `provinsi` | Province |
| `segmen` | Customer segment |
| `tgl_daftar` | Registration date |
| `email` | Email — direct identifier; do not publish |
| `no_hp` | Phone number — direct identifier; do not publish |
| `is_member` | Membership indicator |

## DIM_TOKO — store dimension

| Column | Description / likely meaning |
|---|---|
| `toko_id` | Store primary key |
| `kode_toko` | Store code |
| `nama_toko` | Store name |
| `tipe_toko` | Store type |
| `format` | Store format |
| `kota` | City |
| `provinsi` | Province |
| `wilayah` | Broad geographic area |
| `region` | Region grouping |
| `luas_m2` | Store area in square meters |
| `tgl_buka` | Store opening date |
| `status_toko` | Store status |
| `target_bulanan` | Monthly sales target |

## DIM_KARYAWAN — employee dimension

| Column | Description / likely meaning |
|---|---|
| `karyawan_id` | Employee primary key |
| `nik` | Employee identity number; sensitive identifier, do not publish |
| `nama_karyawan` | Employee name; personal data, do not publish |
| `jabatan` | Job title |
| `departemen` | Department |
| `toko_id` | Store key; links to `DIM_TOKO` |
| `tgl_bergabung` | Employment start date |
| `status_kerja` | Employment status |

## DIM_PROMOSI — promotion dimension

| Column | Description / likely meaning |
|---|---|
| `promosi_id` | Promotion primary key; `0` appears to represent no promotion |
| `kode_promosi` | Promotion code |
| `nama_promosi` | Promotion name |
| `tipe_promosi` | Promotion type |
| `nilai_diskon_pct` | Discount percentage |
| `min_pembelian` | Minimum purchase amount |
| `tgl_mulai` | Promotion start date |
| `tgl_selesai` | Promotion end date |
| `is_aktif` | Active-promotion indicator |

## Notes
- Descriptions are inferred from the workbook's headers and sample values, not an official source data dictionary.
- `harga_satuan`, `total_harga`, `total_neto`, `hpp`, and `gross_profit` should be checked against the source's exact calculation definitions.
- Customer and employee identifiers should be excluded from public data extracts.
