# Tugas Pertemuan 04 - Seleksi Multi-Kondisi dan Validasi Input

## Identitas Mahasiswa

* **Nama:** Reva Liyanasari
* **NIM:** 22252610101
* **Kelas:** 3A
* **Mata Kuliah:** Algoritma dan Pemrograman
* **Dosen Pengampu:** Dr. Aan Hendrayana, S.Si., M.Pd.

---

## Tujuan

Membangun program validasi dan klasifikasi dengan rantai `if-elif-else`.

Program melakukan validasi terhadap tipe dan rentang input, menghitung nilai akhir berdasarkan nilai ujian dan tugas, kemudian melakukan klasifikasi berdasarkan kehadiran dan nilai akhir.

## Cara Menjalankan

```bash
python3 praktik/validasi_klasifikasi_nilai.py
```

## Tabel Keputusan

Tabel berikut disusun berdasarkan setiap cabang kondisi yang terdapat pada program.

| **Cabang**                     | **Kategori**                    | **Syarat**                               | **Contoh Masukan** |
| ------------------------------ | ------------------------------- | ---------------------------------------- | ------------------ |
| `except ValueError`            | Input ditolak                   | Salah satu input bukan angka             | `80, 80, abc`      |
| `if not (0 <= ujian <= 100)`   | Input ditolak                   | Nilai ujian < 0 atau > 100               | `105, 80, 90`      |
| `elif not (0 <= tugas <= 100)` | Input ditolak                   | Nilai tugas < 0 atau > 100               | `80, -5, 90`       |
| `elif not (0 <= hadir <= 100)` | Input ditolak                   | Kehadiran < 0 atau > 100                 | `80, 80, 105`      |
| `if hadir < 80`                | Tidak memenuhi syarat kehadiran | Kehadiran < 80                           | `90, 90, 75`       |
| `if akhir >= 85`               | Predikat A                      | Nilai akhir ≥ 85 dan kehadiran ≥ 80      | `90, 80, 95`       |
| `elif akhir >= 70`             | Predikat B                      | 70 ≤ nilai akhir < 85 dan kehadiran ≥ 80 | `75, 70, 85`       |
| `elif akhir >= 60`             | Predikat C                      | 60 ≤ nilai akhir < 70 dan kehadiran ≥ 80 | `60, 60, 80`       |
| `elif akhir >= 50`             | Predikat D                      | 50 ≤ nilai akhir < 60 dan kehadiran ≥ 80 | `55, 50, 90`       |
| `else`                         | Predikat E                      | Nilai akhir < 50 dan kehadiran ≥ 80      | `40, 30, 100`      |

Nilai akhir dihitung dengan:

```text
Nilai akhir = 0.6 × nilai ujian + 0.4 × nilai tugas
```

Setelah predikat ditentukan:

| **Cabang**                       | **Status**  | **Syarat**            |
| -------------------------------- | ----------- | --------------------- |
| `if predikat in ("A", "B", "C")` | Lulus       | Predikat A, B, atau C |
| `else`                           | Belum lulus | Predikat D atau E     |

Kehadiran diperiksa sebelum klasifikasi predikat. Jika kehadiran kurang dari 80%, program langsung memberikan status **Tidak memenuhi syarat kehadiran**.

## Hasil Pengujian

Pengujian dilakukan dengan mencatat masukan, keluaran yang diharapkan, keluaran aktual, dan status pengujian. Test case berikut mengikuti ketentuan Praktik 1 pada materi.

| **Test Case** | **Masukan**   | **Keluaran yang Diharapkan**                              | **Keluaran Aktual**                                       | **Status** |
| ------------- | ------------- | --------------------------------------------------------- | --------------------------------------------------------- | ---------- |
| 1             | `90, 80, 95`  | Nilai akhir = 86.00; Predikat A; Lulus                    | Nilai akhir = 86.00; Predikat A; Lulus                    | Berhasil   |
| 2             | `75, 70, 85`  | Nilai akhir = 73.00; Predikat B; Lulus                    | Nilai akhir = 73.00; Predikat B; Lulus                    | Berhasil   |
| 3             | `60, 60, 80`  | Nilai akhir = 60.00; Predikat C; Lulus                    | Nilai akhir = 60.00; Predikat C; Lulus                    | Berhasil   |
| 4             | `55, 50, 90`  | Nilai akhir = 53.00; Predikat D; Belum lulus              | Nilai akhir = 53.00; Predikat D; Belum lulus              | Berhasil   |
| 5             | `40, 30, 100` | Nilai akhir = 36.00; Predikat E; Belum lulus              | Nilai akhir = 36.00; Predikat E; Belum lulus              | Berhasil   |
| 6             | `90, 90, 75`  | Tidak memenuhi syarat kehadiran                           | Tidak memenuhi syarat kehadiran                           | Berhasil   |
| 7             | `105, 80, 90` | Masukan ditolak: nilai ujian di luar rentang 0 sampai 100 | Masukan ditolak: nilai ujian di luar rentang 0 sampai 100 | Berhasil   |
| 8             | `80, -5, 90`  | Masukan ditolak: nilai tugas di luar rentang 0 sampai 100 | Masukan ditolak: nilai tugas di luar rentang 0 sampai 100 | Berhasil   |
| 9             | `80, 80, abc` | Masukan ditolak: seluruh data harus berupa angka          | Masukan ditolak: seluruh data harus berupa angka          | Berhasil   |

**Catatan:** Keluaran aktual dan status sebaiknya diisi berdasarkan hasil program yang benar-benar dijalankan di terminal.

## Refleksi

Salah satu masukan tidak valid yang semula dapat terlewat adalah input berupa teks, misalnya `abc`, pada nilai kehadiran. Jika input langsung dikonversi menggunakan `float()` tanpa penanganan kesalahan, program akan menghasilkan `ValueError`.

Masukan tersebut ditangani menggunakan `try-except ValueError`. Jika salah satu input bukan angka, program menolak masukan dan menampilkan pesan bahwa seluruh data harus berupa angka. Dengan demikian, validasi tipe dilakukan sebelum validasi rentang dan proses klasifikasi.
