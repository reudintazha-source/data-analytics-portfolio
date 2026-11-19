# Contract Type vs Customer Churn: Telco Retention Analysis

Analisis hubungan antara jenis kontrak langganan (bulanan, 1 tahun, 2 tahun) dan tingkat churn pelanggan telekomunikasi, menggunakan Excel dan Power BI.

---

## Ringkasan (BLUF)

Churn terkonsentrasi di kontrak bulanan. Kontrak bulanan hanya sekitar 55% dari basis pelanggan, tetapi menyumbang sekitar 89% dari seluruh pelanggan yang churn. Memindahkan sebagian pelanggan bulanan ke kontrak jangka panjang adalah tuas retensi dengan potensi terbesar.

| Ukuran | Hasil |
|---|---|
| Churn rate kontrak bulanan | 42,7% |
| Churn rate kontrak 1 tahun | 11,3% |
| Churn rate kontrak 2 tahun | 2,8% |
| Porsi churn dari kontrak bulanan (churn share) | ±89% |
| Estimasi dampak (10% pelanggan bulanan pindah ke 1 tahun) | Churn total turun ±1,7 poin persentase (26,5% → 24,8%) |

---

## Pertanyaan Bisnis

1. Apakah jenis kontrak berkaitan dengan tingkat churn?
2. Di segmen mana churn paling terkonsentrasi?
3. Tindakan retensi apa yang paling layak diprioritaskan, dan seberapa besar potensi dampaknya?

---

## Dataset

- **Sumber:** [Telco Customer Churn (Kaggle)](https://www.kaggle.com/) — file `WA_Fn-UseC_-Telco-Customer-Churn.csv`
- **Isi:** 7.043 pelanggan layanan telekomunikasi (Internet & Phone)
- **Variabel utama yang dipakai:** `Contract`, `Churn`, `tenure`, `MonthlyCharges`
- **Catatan:** dataset publik, bukan data operasional perusahaan

---

## Metodologi

**Tools:** Excel (pembersihan data, Pivot Table), Power BI (dashboard interaktif)

**Langkah analisis:**
1. Pemeriksaan kualitas data (duplikat, nilai kosong, tipe data, konsistensi label)
2. Pembuatan kelompok langganan: *Monthly* (kontrak bulanan) dan *Annually* (kontrak 1 dan 2 tahun)
3. Pembuatan kelompok masa berlangganan (*tenure group*): New Customer, Middle Customer, Long Term Customer (batas: `[isi batas bulan, misal 0-12 / 13-48 / 49+]`)
4. Perhitungan churn rate dan churn share per segmen
5. Estimasi skenario dampak migrasi kontrak
6. Visualisasi di Power BI dan penyusunan ringkasan

**Definisi metrik** (penting, sering tertukar):

| Metrik | Definisi | Contoh |
|---|---|---|
| **Churn rate** | Pelanggan churn ÷ semua pelanggan **dalam kelompok itu** | Churn rate bulanan = 1.655 ÷ 3.875 = 42,7% |
| **Churn share** | Pelanggan churn di kelompok itu ÷ **semua pelanggan churn** | Churn share bulanan = 1.655 ÷ 1.869 ≈ 88,6% |
| **Poin persentase** | Selisih langsung antar persentase | 26,5% → 24,8% = turun 1,7 poin |

Churn didefinisikan sebagai `Churn = Yes` pada dataset.

---

## Temuan Utama

### 1. Churn sangat terkonsentrasi di kontrak bulanan

| Kontrak | Pelanggan | Porsi pelanggan | Pelanggan churn | Churn rate | Churn share |
|---|---|---|---|---|---|
| Bulanan | 3.875 | 55,0% | 1.655 | **42,7%** | **88,6%** |
| 1 tahun | 1.473 | 20,9% | 166 | 11,3% | 8,9% |
| 2 tahun | 1.695 | 24,1% | 48 | 2,8% | 2,6% |
| **Total** | **7.043** | **100%** | **1.869** | **26,5%** | **100%** |

Kontrak bulanan hanya 55% pelanggan, tetapi menyumbang ±89% dari seluruh churn.

### 2. Makin panjang kontrak, makin rendah churn

Churn rate turun dari 42,7% (bulanan) ke 11,3% (1 tahun) dan 2,8% (2 tahun). Penurunan terbesar terjadi pada langkah pertama, dari bulanan ke 1 tahun (31,4 poin persentase).

Angka gabungan kontrak tahunan (6,76%) menyembunyikan perbedaan antara kontrak 1 tahun dan 2 tahun, sehingga analisis sebaiknya memisahkan keduanya.

### 3. Pelanggan baru di kontrak bulanan paling rawan

| Kelompok masa berlangganan | Churn rate: Bulanan | Churn rate: Tahunan |
|---|---|---|
| New Customer | **51,4%** | 6,8% |
| Middle Customer | 35,7% | 6,0% |
| Long Term Customer | 29,6% | 7,0% |

Pelanggan bulanan baru menyumbang sekitar 54,8% dari seluruh churn. Di kontrak tahunan, churn stabil di kisaran 6-7% pada semua kelompok.

### 4. Jenis kontrak berperan, tidak sekadar lama berlangganan

Pelanggan bulanan dengan masa berlangganan terlama (churn 29,6%) masih jauh lebih rentan dibanding pelanggan tahunan yang baru bergabung (6,8%).

---

## Rekomendasi

1. **Target:** pelanggan kontrak bulanan, dengan prioritas pelanggan baru (churn 51,4%).
2. **Tindakan:** tawarkan insentif migrasi ke kontrak 1 tahun (diskon, bonus kuota, atau benefit tambahan). Kontrak 2 tahun menjadi tahap upsell berikutnya.
3. **Ukuran keberhasilan:** persentase pelanggan yang bermigrasi dan churn rate enam bulan setelah migrasi.
4. **Riset lanjutan:** telusuri alasan churn (survei keluar, data keluhan), termasuk pada kontrak jangka panjang.

---

## Estimasi Dampak

**Rumus:** porsi pelanggan bulanan (55%) × persentase yang berpindah × selisih churn rate (42,7% − 11,3% = 31,4 poin)

| Pelanggan bulanan yang berpindah ke 1 tahun | Churn total | Pelanggan tertahan |
|---|---|---|
| 5% | 26,5% → 25,7% | ±60 |
| **10%** | **26,5% → 24,8%** | **±120** |
| 20% | 26,5% → 23,1% | ±240 |

**Asumsi:** pelanggan yang berpindah berperilaku seperti pelanggan kontrak 1 tahun saat ini. Estimasi ini belum dikurangi biaya insentif.

---

## Batasan

1. **Korelasi, bukan kausalitas.** Data bersifat observasional. Pelanggan yang memang setia bisa lebih cenderung memilih kontrak panjang.
2. **Efek terkunci kontrak.** Churn rendah di kontrak panjang bisa sebagian disebabkan belum jatuh tempo atau adanya denda pemutusan, bukan semata kepuasan.
3. **Asumsi dampak optimistis.** Estimasi menganggap perilaku pelanggan yang berpindah sama dengan pelanggan kontrak 1 tahun saat ini.
4. **Data satu waktu dan publik.** Tidak ada data biaya insentif, alasan churn, maupun perilaku saat perpanjangan kontrak.

---

## Langkah Lanjutan

- Pilot ke kelompok kecil dengan kelompok pembanding (A/B test) sebelum peluncuran penuh
- Analisis churn pada masa perpanjangan kontrak
- Ulangi analisis dengan SQL dan tambahkan analisis kohort

---

## Struktur Repositori

```
├── data/
│   ├── raw/                 # dataset asli dari Kaggle
│   └── clean/               # data setelah pembersihan
├── excel/
│   └── churn_analysis.xlsx  # pivot dan perhitungan
├── powerbi/
│   └── churn_dashboard.pbix # dashboard Power BI
├── presentation/
│   └── Contract_Type_vs_Customer_Churn.pptx
├── images/
│   └── dashboard.png        # tangkapan layar dashboard
└── README.md
```

> Sesuaikan nama file dan folder dengan isi repositori kamu.

---

## Cara Menggunakan

1. Unduh dataset dari Kaggle, lalu letakkan di `data/raw/`.
2. Buka `excel/churn_analysis.xlsx` untuk melihat langkah pembersihan dan pivot.
3. Buka `powerbi/churn_dashboard.pbix` dengan Power BI Desktop. Gunakan slicer *Contract*, *Tenure Group*, dan *Churn* untuk eksplorasi.

---

## Tentang Saya

**[Nama Kamu]** — Data / Business Intelligence Analyst (membangun portofolio lewat studi kasus data publik)

- LinkedIn: https://www.linkedin.com/in/reudinta-zesha/
- Portofolio: https://reudintazha-source.github.io/portfolio/)

Masukan mengenai metode atau segmentasi sangat diterima lewat *Issues* atau pesan langsung.

---

## Sumber dan Catatan

- Dataset: Telco Customer Churn, Kaggle (hak cipta tetap pada pemilik dataset)
- Proyek ini dibuat untuk tujuan pembelajaran dan portofolio, bukan merupakan rekomendasi bisnis untuk perusahaan tertentu.
