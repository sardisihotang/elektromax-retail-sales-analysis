# Data Cleaning & Preparation Log

## 1. Source and scope
- Source file used for inspection: `dataset_elektronik_dirty.xlsx`
- Sheets: FACT_PENJUALAN, DIM_PRODUK, DIM_WAKTU, DIM_PELANGGAN, DIM_TOKO, DIM_KARYAWAN, DIM_PROMOSI
- Transaction fact table before cleaning: 56,748 rows
- Date dimension coverage: 1 January 2023 to 31 December 2025

> Add the original dataset URL and license before public redistribution. Do not upload the source workbook as-is because the customer dimension contains direct personal identifiers.

## 2. Initial quality assessment

### Duplicate primary keys
| Table | Primary key | Repeated key count |
|---|---|---:|
| FACT_PENJUALAN | `penjualan_id` | 20 |
| DIM_PRODUK | `produk_id` | 1 |
| DIM_WAKTU | `waktu_id` | 0 |
| DIM_PELANGGAN | `pelanggan_id` | 0 |
| DIM_TOKO | `toko_id` | 0 |
| DIM_KARYAWAN | `karyawan_id` | 0 |
| DIM_PROMOSI | `promosi_id` | 0 |

Repeated-key records were inspected. The repeated fact rows shown in the source appear identical by transaction ID and transaction attributes. The repeated product record for `produk_id = 3` also appears identical. If the cleaning implementation removes duplicates, retain one record per primary key and record the rule used.

### Missing values found

**FACT_PENJUALAN**

| Column | Missing count |
|---|---:|
| `diskon_persen` | 35 |

**DIM_PRODUK**

| Column | Missing count |
|---|---:|
| `subkategori` | 2 |

**DIM_PELANGGAN**

| Column | Missing count |
|---|---:|
| `tgl_lahir` | 1 |
| `tgl_daftar` | 1 |
| `email` | 8 |

**DIM_PROMOSI**

| Column | Missing count |
|---|---:|
| `tgl_mulai` | 1 |
| `tgl_selesai` | 1 |

## 3. Cleaning rules and decisions

| Issue | Field(s) | Recommended treatment | Validation |
|---|---|---|---|
| Repeated transaction key | `FACT_PENJUALAN.penjualan_id` | Remove repeated primary-key records after checking whether the rows are exact duplicates; keep one valid record | Confirm unique `penjualan_id` after cleaning |
| Repeated product key | `DIM_PRODUK.produk_id` | Inspect and retain one canonical record if the duplicate is identical | Confirm unique `produk_id` |
| Transaction status variants | `status_transaksi` | Map `selesai`, `SELESAI`, `Done`, `Sukses`, `Complete` to `Selesai` | Check status counts before/after mapping |
| Return status variants | `status_transaksi` | If business meaning is equivalent, map `retur`, `RETUR`, `Return`, `Dikembalikan` to `Retur` | Confirm with dataset definition |
| Missing discount percentage | `diskon_persen` | Do not automatically drop transaction. Determine whether blank means no discount; if confirmed, replace with 0, otherwise retain as unknown | Compare with `diskon_nominal`, `promosi_id`, and source rules |
| Missing product subcategory | `DIM_PRODUK.subkategori` | Investigate product mapping; use an explicit `Unknown` category if unresolved | Confirm no product is silently misclassified |
| Missing customer dates/email | `DIM_PELANGGAN` | Keep transaction/customer record where possible; dates remain unknown; remove or mask email for public release | Check whether downstream analysis needs the field |
| Missing promotion dates | `DIM_PROMOSI.tgl_mulai`, `tgl_selesai` | Retain as blank if the promotion has no date (e.g. no-promotion row); do not invent dates | Confirm `promosi_id = 0` meaning |
| Placeholder demographic values | `—` in customer fields | Treat as unknown/not provided, not as a genuine category | Exclude unknown from demographic interpretation |

**Important:** “Remove nulls” should not mean deleting every row that contains any null. For example, a missing customer email does not invalidate a sales transaction. Choose treatment based on the analytical question and business meaning.

## 4. Standardization examples

| Raw value | Standard value |
|---|---|
| `Selesai`, `selesai`, `SELESAI`, `Done`, `Sukses`, `Complete` | `Selesai` |
| `Retur`, `retur`, `RETUR`, `Return`, `Dikembalikan` | `Retur` (if confirmed equivalent) |

Other fields that should be checked for consistency include `segmen` (e.g. `Regular`/`REGULAR`) and `metode_bayar` (e.g. `QRIS`/`Q-RIS`, `Tunai`/`Cash`). Do not merge labels unless their meanings are confirmed to be equivalent.

## 5. Privacy and public release
The original `DIM_PELANGGAN` includes `nama_pelanggan`, `email`, and `no_hp`. These fields are direct identifiers and must not be published in a public repository or public Power BI report. Prefer removing these columns from the public copy or replacing them with non-identifying IDs. Check whether the dataset license permits redistribution before uploading any processed data.

## 6. Final validation checklist
- [ ] Each dimension primary key is unique.
- [ ] Fact `penjualan_id` is unique.
- [ ] Foreign keys in fact table match dimension keys (including special `promosi_id = 0` row).
- [ ] Status values are standardized and counts reconciled.
- [ ] Missing values are handled with documented business rules.
- [ ] Sales/profit totals are reconciled before and after cleaning.
- [ ] Report filters and DAX measures use consistent status definitions.
- [ ] No customer names, emails, or phone numbers are exposed.
