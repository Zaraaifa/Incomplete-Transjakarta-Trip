# Studi Analisis Incomplete Journey: Mengoptimalkan Pendapatan dan Validitas Data Operasional TransJakarta

## Overview
Repositori ini berisi Jupyter Notebook yang menganalisis *perjalanan yang tidak lengkap* dalam sistem transportasi umum Transjakarta untuk bulan April 2023. Perjalanan yang tidak lengkap terjadi ketika penumpang melakukan tap in namun tidak melakukan tap out, yang menyebabkan hilangnya data dan potensi kehilangan pendapatan. Analisis ini mengidentifikasi pola, menilai dampak finansial, dan mengusulkan strategi untuk mengurangi perjalanan yang tidak lengkap di bawah 1,5% dari standar industri di Asia Tenggara (2020), yang mendukung efisiensi operasional Transjakarta dan visi kota pintar Jakarta.


## Dataset
Dataset (`Transjakarta.csv`) mencakup **37.900 catatan transaksi** dari bulan April 2023, yang merinci perjalanan penumpang. Kolom-kolom kunci:

| Column             | Description                                                  |
|--------------------|--------------------------------------------------------------|
| `transID`          | Unique transaction ID.                                       |
| `payCardBirthDate` | Passenger’s birth year (for age analysis).                   |
| `corridorName`     | Route name (e.g., "Matraman Baru - Ancol").                  |
| `tapInTime`        | Tap-in timestamp.                                           |
| `tapOutTime`       | Tap-out timestamp (missing for incomplete journeys).         |
| `payAmount`        | Fare paid (e.g., 0, 3500, 20000).                           |
| `incomplete_journey`| Boolean flag for incomplete journeys (True/False).          |

**Source**: [Google Drive](https://drive.google.com/drive/folders/1p7f4a2tUP1Ek159BUVA2bFkdQUklOe7h?usp=share_link)

## Objectives
1. Mengidentifikasi faktor-faktor yang secara signifikan berkorelasi dengan perjalanan yang tidak lengkap berdasarkan koridor dan waktu.
2. Mendeteksi pola demografis atau perilaku yang memprediksi perjalanan yang tidak lengkap.
3. Menganalisis karakteristik spasial (koridor, halte) dan temporal (waktu, hari).
4. Merekomendasikan strategi untuk mengurangi perjalanan yang tidak lengkap.
   
## Metode
### Data Preprocessing
- **Cleaning**: Handled missing `tapOutTime` values and adjusted data types (e.g., `tapInTime` to datetime).
- **Feature Engineering**:
  - Created `age_group` (<18, 18-25, ..., >55).
  - Derived `trans_type` (TransJakarta, Mikrotrans, Royaltrans) from `payAmount`.
  - Added `hour_category` (e.g., Morning Peak) and `is_weekday`.
  - Mapped `region` (e.g., Jakarta Selatan) using stop coordinates.
- **Validation**: Confirmed no duplicates and addressed outliers per statistical best practices.

### Analysis
- **Uji Statistik**:
  - Chi-square untuk korelasi (usia, koridor, jenis transportasi, dll.).
  - Uji-t dan korelasi Spearman untuk dampak usia.
- **EDA**:
  - Crosstabs dan visualisasi untuk mengeksplorasi pola.
  - Tingkat ketidaklengkapan yang dihitung (misalnya, 3,55% secara keseluruhan).
- **Tools**: Python (`pandas`, `numpy`, `matplotlib`, `seaborn`, `scipy.stats`).

## Dashboard
Hasil dashboard dapat dilihat [di sini](https://lookerstudio.google.com/reporting/eb960d8a-b71c-479e-80ed-d90e2be66b90)

## PowerPoint Presenation
Hasil PowerPoint dapat dilihat [di sini](https://www.canva.com/design/DAGkWYff3i4/9qJBISoJggvueFUfbYSXxw/edit?utm_content=DAGkWYff3i4&utm_campaign=designshare&utm_medium=link2&utm_source=sharebutton)


## Key Findings
- Skala**: 1.344 perjalanan yang tidak lengkap (3,55%) menyebabkan hilangnya pendapatan sebesar ~Rp 3.573.250.
- Faktor-faktor yang signifikan**:
  - **Usia**: Penumpang yang berusia lebih tua (&gt;55) memiliki tarif yang lebih tinggi (4,52%, p=0,002).
  - **Jenis Angkutan**: Mikrotrans menunjukkan tingkat yang lebih tinggi (p&lt;0,001).
  - **Koridor**: Titik-titik rawan termasuk “Kebayoran Lama - Tanah Abang” (p&lt;0,001).
- **Tidak Signifikan**: Jenis kelamin, metode pembayaran, waktu, dan jenis hari (p&gt;0,05).
- **Spasial**: Terkonsentrasi di Jakarta Selatan dan halte-halte seperti Kampung Cervino.
- **Temporal**: Tidak ada pola yang jelas berdasarkan waktu (p=0,446 untuk jam).
- **Finansial**: Banyak perjalanan yang tidak lengkap menghasilkan `jumlahPembayaran=0`.

## Recommendations
1. **Pendidikan yang ditargetkan untuk usia tertentu:
   - Pasang panduan tap-in/tap-out yang jelas di halte.
   - Menugaskan asisten untuk <18 and >55 penumpang selama jam-jam sibuk.
   - Tambahkan tutorial aplikasi untuk pengguna baru.
2. Audit Jenis Angkutan **Audit Jenis Angkutan**:
   - Memeriksa perangkat tap-out Mikrotrans.
   - Standarisasi prosedur dengan pengingat.
   - Menguji sistem tap-out otomatis.
3. **Peningkatan Koridor/Halte**:
   - Perbaiki perangkat di 5-10 halte teratas.
   - Perbaiki rambu dan akses.
   - Menambah bus untuk mengurangi kepadatan puncak.
4. **Pemantauan**:
   - Buatlah dasbor perjalanan yang tidak lengkap secara real-time.
   - Melakukan tinjauan statistik triwulanan.
   - Mengaktifkan umpan balik penumpang berbasis aplikasi.
5. **Kampanye Kesadaran**:
   - Menjalankan kampanye media sosial (“Tap-In, Tap-Out!”).
   - Tambahkan pengingat tap-out di dalam bus.
     

## Installation
```bash
# Clone repository
git clone https://github.com/your-username/transjakarta-incomplete-journey.git
```

## Install dependencies
```bash
pip install pandas numpy matplotlib seaborn scipy
```

## Usage
1. Download Transjakarta.csv dari tautan sumber data.
2. Tempatkan di direktori proyek.
3. Buka Transjakarta_Incomplete_Journey_Analysis.ipynb di Jupyter:
```bash
jupyter notebook Transjakarta_Incomplete_Journey_Analysis.ipynb
```
4. Jalankan seluruh kolom untuk memperoleh hasil.

## Project Structure
├── Transjakarta_Incomplete_Journey_Analysis.ipynb  # Analysis notebook
├── Transjakarta.csv                                # Dataset (external)
├── Dashboard_Transjakarta_Incomplete_Journey       # Visualizations 
└── README.md                                       # Project overview

## Limitations
- Analisis pola temporal yang terbatas karena faktor waktu yang tidak signifikan.
- Rincian dasbor yang tidak lengkap (misalnya, nama halte tertentu).

## Future Work
- Menganalisis pola temporal (misalnya, tren per jam).
- Jelajahi prediktor perilaku (misalnya, pengguna baru vs. pengguna setia).
- Mensimulasikan dampak rekomendasi.
- Menguji coba intervensi di koridor berisiko tinggi.

## Lisence
Hanya untuk penggunaan pendidikan. Penggunaan dataset sesuai dengan ketentuan Transjakarta.

## Contact
Buka masalah atau hubungi [abdillah.zaraa@gmail.com] untuk pertanyaan.
