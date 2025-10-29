Tentu\! Sebagai *Software Engineer* yang telah merancang sistem ini, inilah rangkuman lengkap dari semua yang telah kita buat, disajikan dalam format *markdown* yang rapi.

Rangkuman ini mencakup tujuan, desain Fuzzy Logic, dan *script* implementasi final.

-----

# Rangkuman Proyek Software Engineer untuk SNITER 2025

## Topik: Peningkatan Daya Saing Talenta Digital Melalui Sistem Pendukung Keputusan Fuzzy: Model Penentuan Prioritas Tugas (Time Management) Mahasiswa yang Adaptif

### 1\. Relevansi Tema Seminar

| Pilar Seminar | Keterangan |
| :--- | :--- |
| **Smart Technology** | Implementasi Logika Fuzzy (Metode Mamdani) sebagai inti AI yang mengatasi subjektivitas dalam pengambilan keputusan. |
| **Talent Development** | Sistem berfungsi sebagai alat bantu *Time Management*, menanamkan disiplin prioritas yang krusial bagi talenta yang kompetitif secara global. |
| **Economic Innovation**| Mendorong efisiensi sumber daya (waktu dan energi mahasiswa) untuk hasil akademik dan proyek yang optimal. |

### 2\. Desain Fuzzy Logic (Metode Mamdani)

Kami memilih **Metode Mamdani** karena transparansi logikanya (mudah diinterpretasikan) yang vital untuk Sistem Pendukung Keputusan.

#### A. Variabel Input dan Output

| Variabel | Tipe | Semesta Pembicaraan | Himpunan Linguistik |
| :--- | :--- | :--- | :--- |
| **Urgensi** (Input) | Dinamis (0-100) | Rentang waktu sisa (0-30 hari) | Rendah, Sedang, Tinggi |
| **Kesulitan** (Input) | Numerik (0-100) | Usaha yang dibutuhkan (0-50 jam) | Very Easy, Easy, Medium, Hard, Very Hard |
| **Prioritas** (Output) | Crisp (0-100) | Skor Prioritas | Lowest, Low, Medium, High, Highest |

#### B. Basis Aturan Kritis (Rule Base)

Total 15 Aturan (**$3 \times 5$**). Berikut 4 contoh aturan penentu:

| Urgensi | AND | Kesulitan | THEN | Prioritas |
| :--- | :--- | :--- | :--- | :--- |
| **Tinggi** | & | **Very Hard** | THEN | **Highest** |
| **Tinggi** | & | **Very Easy** | THEN | **High** |
| **Rendah** | & | **Very Hard** | THEN | **Medium** |
| **Rendah** | & | **Very Easy** | THEN | **Lowest** |

-----

## III. Implementasi Python dan Data Testing

Kami menggunakan pustaka `scikit-fuzzy` dan `pandas` untuk implementasi.

### A. Data CSV Realistis (`data.csv`)

Data ini memuat kombinasi skenario Urgensi dan Kesulitan yang bervariasi:

```csv
task_name,due_datetime,est_effort_hours
Kuis Kecerdasan Buatan,2025-10-29 09:00:00,1
Proposal Proyek Akhir,2025-11-10 23:59:00,10
Tugas Bacaan Logika Fuzzy,2025-10-31 12:00:00,4
Revisi Skripsi Bab 1,2025-12-05 17:00:00,25
Persiapan Presentasi Sniter,2025-11-03 10:00:00,8
Mengerjakan Soal Latihan Kalkulus,2025-10-29 23:59:00,2
Meresume Chapter 5 Kewirausahaan,2025-11-05 15:00:00,3
Project UTS Mobile Programming,2025-11-20 23:59:00,35
Meeting Online Tim Proyek,2025-10-28 19:30:00,1
Membeli Buku Teks Baru,2025-11-25 12:00:00,1
Perencanaan Karir Jangka Panjang,2026-01-01 00:00:00,50
Perbaiki Bug di Aplikasi Kampus,2025-11-01 16:00:00,6
Ujian Akhir Semester (Simulasi),2025-12-15 10:00:00,15
Balas Email Dosen Pembimbing,2025-10-29 17:30:00,0.5
```

### B. Fungsi Eksekusi dan Pengurutan

Kode di *backend* akan melakukan langkah-langkah berikut:

1.  **Hitung Urgensi Dinamis:** Mengubah `due_datetime` menjadi skor 0-100 berdasarkan selisih waktu dari `CURRENT_TIME_VAR`.
2.  **Normalisasi Kesulitan:** Mengubah `est_effort_hours` menjadi skor 0-100.
3.  **Fuzzifikasi & Inferensi:** Memproses kedua skor melalui 15 aturan Mamdani.
4.  **Defuzzifikasi:** Menghasilkan **`Final Priority Score`** (0-100).
5.  **Pengurutan Hasil:** Tabel output diurutkan secara **Descending** berdasarkan:
      * Kriteria Utama: **`Final Priority Score`**
      * Kriteria Kedua (*Tie-Breaker*): **`Urgensi Score (0-100)`**

### C. Output yang Diharapkan

Tabel akhir akan menunjukkan peringkat yang akurat, membuktikan bahwa logika Fuzzy berhasil menyeimbangkan waktu dan usaha untuk memberikan keputusan terbaik kepada mahasiswa.

-----

Rangkuman ini menyediakan semua detail teknis dan format yang Anda butuhkan untuk menyelesaikan artikel Anda. Selamat menyelesaikan proyek SNITER Anda\!