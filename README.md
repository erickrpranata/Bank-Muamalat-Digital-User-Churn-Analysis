# PT Sejahtera Bersama — Bank Muamalat Digital User Churn Analytics

## Project Overview

Project ini merupakan studi kasus Data Analytics yang berfokus utama pada analisis performa sales PT Sejahtera Bersama, namun saya inisiatif menambahkan analisis customer churn.

Analisis dilakukan menggunakan Customers, Orders, Products, dan Product Category. Data diolah menggunakan SQL di Google BigQuery untuk menghasilkan Tabel Master yang kemudian digunakan dalam analisis dan visualisasi dashboard menggunakan Looker Studio.

Project ini bertujuan untuk memahami tren penjualan, mengidentifikasi pola pembelian pelanggan, mengevaluasi customer churn, serta menghasilkan rekomendasi bisnis berdasarkan temuan dari data.

## Objectives

1. Menganalisis total keseluruhan sales dan quantity berdasarkan kategori produk dan kota.
2. Mengidentifikasi kategori produk dengan kontribusi sales dan volume tertinggi.
3. Menganalisis tren penjualan selama periode 2020–2021.
4. Mengukur customer churn dan repeat rate konsumen.
5. Menguji hipotesis hubungan antara volume penjualan produk dan churn rate.
6. Menyusun rekomendasi untuk meningkatkan retensi pelanggan dan performa penjualan.

## Dataset

Project menggunakan empat tabel sumber:

| Table             | Description                                                                    |
| ----------------- | ------------------------------------------------------------------------------ |
| `Customers`       | Menyimpan informasi pelanggan.                                                 |
| `Orders`          | Menyimpan data transaksi, tanggal transaksi, pelanggan, produk, dan kuantitas. |
| `Products`        | Menyimpan informasi produk, kategori, dan harga.                               |
| `ProductCategory` | Menyimpan informasi kategori produk.                                           |

### Primary Keys

* `Customers`: `CustomerID`
* `Orders`: `OrderID`
* `Products`: `ProdNumber`
* `ProductCategory`: `CategoryID`

### Table Relationships

Hubungan antartabel mengikuti struktur data berikut:

* `Customers` → `Orders`: one-to-many
* `Products` → `Orders`: one-to-many
* `ProductCategory` → `Products`: one-to-many

## Tools

* **Google BigQuery** — data processing dan SQL analysis.
* **SQL** — data joining, transformation, dan analytical queries.
* **Looker Studio** — pembuatan dashboard interaktif.
* **GitHub** — dokumentasi dan penyimpanan kode SQL.

## Data Processing

Data dari empat tabel sumber digabungkan untuk membentuk tabel master yang digunakan dalam analisis.

**Source tables:**

```text
Customers
Orders
Products
ProductCategory
```

**Data processing workflow:**

```text
Customers ─────┐
               │
Orders ────────┼── JOIN
               │
Products ──────┤
               │
ProductCategory┘
       │
       ▼
   table_master
       │
       ├── Sales Analytics
       │
       └── Churn Analytics
                │
                ▼
          Looker Studio
```

Tabel `table_master` digunakan sebagai sumber data untuk analisis penjualan dan customer churn.

## Sales Analytics

Analisis penjualan dilakukan untuk memahami kontribusi kategori produk, distribusi penjualan berdasarkan kota, serta perubahan performa penjualan dari waktu ke waktu.

### Key Metrics

* Total Sales
* Total Quantity
* Average Order Value (AOV)
* Sales berdasarkan kategori produk
* Quantity berdasarkan kategori produk
* Top 5 kategori produk berdasarkan sales 
* Top 5 kategori produk berdasarkan quantity
* Tren penjualan bulanan (2020-2021)
* Total Sales dan quantity berdasarkan kota

### Key Findings

**1. Sales dan volume penjualan tidak selalu sejalan.**

Kategori Robots menghasilkan sales tertinggi sebesar sekitar $743.51K dari 1,053 unit. Sebaliknya, eBooks mencatat volume tertinggi sebanyak 3,123 unit, tetapi sales-nya sekitar $58.97K.

Temuan ini menunjukkan bahwa kategori dengan volume penjualan tinggi belum tentu menghasilkan nilai penjualan tertinggi.

**2. Performa penjualan berbeda antar kota.**

Washington mencatat sales tertinggi sekitar $55,381.94, sekitar 64% lebih tinggi dibandingkan Houston di posisi kedua. Namun, kontribusi Washington hanya sekitar 3.2% dari total sales, sehingga penjualan tetap tersebar di banyak kota.

**3. Sales tahun 2021 cenderung lebih rendah dibandingkan 2020.**

Perbandingan bulanan secara year-over-year menunjukkan bahwa penjualan 2021 cenderung lebih rendah daripada periode yang sama pada 2020, meskipun terdapat peningkatan pada beberapa bulan, terutama April dan Juni.

## Customer Churn Analytics

Analisis churn dilakukan untuk memahami pelanggan yang tidak kembali melakukan pembelian dalam periode observasi serta mengevaluasi pola pembelian ulang berdasarkan kategori produk.

### Key Metrics

* Total Customer
* Churn Customer
* Churn Rate
* Average Customer Value
* Customer churn berdasarkan kategori produk
* Average Order Value dan churn rate berdasarkan kategori
* Quantity, churn rate, dan repeat purchase rate berdasarkan kategori

### Churn Definition

Dalam project ini, customer dikategorikan sebagai churn apabila tidak melakukan pembelian selama **365 hari atau 12 bulan**, berdasarkan definisi dan periode observasi yang digunakan dalam analisis.

### Key Findings

**1. Customer churn mencapai 31.24%.**

Dari 1,671 pelanggan unik, sebanyak 522 pelanggan dikategorikan sebagai churn berdasarkan periode observasi yang digunakan.

**2. Repeat purchase rate masih rendah.**

Repeat purchase rate seluruh kategori produk berada di bawah 20%. eBooks memiliki repeat purchase rate tertinggi sebesar 19.61%, sedangkan Robot Kits memiliki repeat purchase rate terendah sebesar 4.14%.

Temuan ini menunjukkan sebagian besar customer hanya membeli sekali per kategori.

**3. Average Order Value belum cukup untuk menjelaskan churn.**

Robots memiliki AOV dan churn rate tertinggi. Namun, pola tersebut tidak konsisten pada semua kategori. Hal ini menunjukkan bahwa AOV saja belum cukup untuk menjelaskan perbedaan churn antar kategori.

**4. Hipotesis volume penjualan tinggi dan churn tinggi tidak didukung oleh hasil analisis.**

Hipotesis awal menyatakan bahwa kategori dengan volume penjualan tinggi memiliki churn rate lebih tinggi.

Namun, eBooks mencatat volume tertinggi sebanyak 3,123 unit dan churn rate terendah sebesar 42.96%. Sebaliknya, Robots mencatat volume 1,053 unit dan churn rate tertinggi sebesar 51.67%.

Selisih churn rate kedua kategori tersebut adalah 8.71 poin persentase. Dengan demikian, hasil analisis tidak menunjukkan pola yang mendukung hipotesis awal secara konsisten.

## Business Recommendations

### 1. Strengthen Customer Retention

Memprioritaskan strategi re-engagement untuk kategori Robots dan Robot Kits yang memiliki churn rate sekitar ±51% serta repeat purchase rate relatif rendah.

Strategi yang dapat dieksplorasi meliputi personalized offers, rekomendasi produk, paket bundling, dan program loyalitas.

### 2. Learn from eBooks Customer Behavior

Menganalisis pola pembelian pelanggan eBooks yang memiliki repeat purchase rate tertinggi dan churn rate terendah untuk mengidentifikasi pendekatan yang berpotensi diterapkan pada kategori lain.

### 3. Improve Sales and Customer Value

Mengevaluasi peluang cross-sell dan upsell dari kategori dengan volume pembelian tinggi, seperti eBooks dan Training Videos, menuju produk dengan nilai transaksi lebih tinggi, dengan mempertimbangkan kesesuaian produk dan pola pembelian pelanggan.

### 4. Investigate the 2021 Sales Decline

Menelusuri perubahan jumlah pelanggan, frekuensi pembelian, dan nilai transaksi berdasarkan kategori produk dan kota. Periode April dan Juni 2021 dapat dianalisis lebih lanjut untuk memahami faktor yang berpotensi menjelaskan peningkatan penjualan pada bulan tersebut.

## Dashboard

Project ini divisualisasikan melalui dua dashboard utama di Looker Studio:

1. **Sales Analytics** — untuk memantau performa penjualan, volume produk, tren bulanan, dan kontribusi kota.
2. **Churn Analytics** — untuk memantau churn rate, repeat purchase rate, dan pola pembelian pelanggan berdasarkan kategori.

Dashboard: *https://datastudio.google.com/reporting/843cdd28-53df-4010-a2b4-9f7409ad8329*

## Repository Structure

```text
Bank-Muamalat-Digital-User-Churn-Analysis/
├── table_master.sql
└── README.md
```

## Learning Outcomes

Melalui project ini, saya mempraktikkan beberapa tahapan Data Analytics:

* Memahami struktur data dan relasi antartabel.
* Menggabungkan beberapa tabel menggunakan SQL.
* Menyiapkan data untuk analisis penjualan dan customer churn.
* Menghitung serta menginterpretasikan business metrics.
* Menguji hipotesis menggunakan data.
* Menerjemahkan temuan analisis menjadi rekomendasi bisnis.
* Menyajikan hasil analisis melalui dashboard interaktif.

## Author

**Erick R Pranata**

Aspiring Data Analyst

**Tools:** SQL · Google BigQuery · Looker Studio · Data Analytics · Data Visualization
