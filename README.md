# Tugas Software Testing — Kuliah Asinkron

Latihan praktik **Software Testing** dengan Python dan framework bawaan `unittest`. Materi diadaptasi dari I. Sommerville, *Engineering Software Products*, Bab 9.

| | |
|---|---|
| **Nama** | Anugrah Putra Al Fatih |
| **NIM** | 26/59120/PPA/07385 |

---

## 📂 Isi Repositori

| File | Keterangan |
|---|---|
| [`Tugas_Testing_26_59120_PPA_07385.ipynb`](Tugas_Testing_26_59120_PPA_07385.ipynb) | Notebook jawaban yang sudah dikerjakan, lengkap dengan output (Bagian A, B, dan C). |
| [`Tugas_Software_Testing.ipynb`](Tugas_Software_Testing.ipynb) | Template soal asli yang belum dikerjakan. |
| `README.md` | Dokumentasi ini. |

---

## 🎯 Tujuan Pembelajaran

- Membagi input ke dalam **partisi ekuivalen** dan memilih **nilai batas** (*edge cases*).
- Menulis tes yang bisa dijalankan dengan pola **Arrange – Action – Assert**.
- Menerapkan siklus **Test-Driven Development** (merah → hijau → refactor).
- Melakukan **pengujian keamanan berbasis risiko**.
- Melakukan **code review** dengan checklist.
- Memastikan tes yang ditulis **benar-benar bisa gagal** (uji mutasi sederhana).

---

## 🧩 Struktur Tugas

### Bagian A — Latihan (Hands-on Exercises)

Latihan yang dinilai: **2, 3, 5, 6, dan 7**. Latihan 1, 4, dan 8 tetap dikerjakan sebagai latihan tambahan.

| # | Topik | Referensi Slide | Ringkasan yang dikerjakan |
|---|---|---|---|
| 1 | Equivalence partitions | Fig. 9.3, Table 9.3 | Menentukan partisi valid/tidak valid untuk validator nama `namecheck` dan memprediksi hasilnya. |
| 2 | Menjalankan dan *membaca* tes (Program 9.3) | Program 9.3 | Menjalankan 14 tes, menganalisis tes yang gagal, dan membuktikan lewat **mutasi** bahwa `test_shortname` lemah karena tidak bisa gagal. |
| 3 | Edge cases | Table 9.4 | Melengkapi 5 tes kasus tepi untuk `namecheck` (panjang tepat di batas 2 dan 40, di luar batas, dan string kosong). |
| 4 | Arrange – Action – Assert | Program 9.2 | Menyusun ulang tes dengan pola AAA. |
| 5 | Test-driven development | Fig. 9.8, Table 9.9 | Membangun fungsi secara bertahap lewat siklus merah → hijau → refactor. |
| 6 | Risk-based security testing | Table 9.11 | Mengimplementasikan `is_strong_password` (min. 12 karakter, bukan password umum, min. 3 dari 4 kelas karakter) hingga 8 tes lulus. |
| 7 | Code review dengan checklist | Table 9.13 | Me-review fungsi dengan checklist Python (nama tidak bermakna, *mutable default argument*, tipe tidak konsisten, error tidak ditangani), lalu memperbaikinya hingga 5 tes lulus. |
| 8 | Menjalankan tes dari file | Program 9.4 | Menyimpan tes sebagai skrip `.py` dan menjalankannya dari command line. |

### Bagian B — Mini-proyek `nilai_huruf`

Fungsi `nilai_huruf(skor)` dikembangkan sepenuhnya dengan TDD berdasarkan spesifikasi berikut:

| Skor | Hasil |
|---|---|
| 80 ≤ skor ≤ 100 | `'A'` |
| 70 ≤ skor < 80 | `'B'` |
| 60 ≤ skor < 70 | `'C'` |
| 50 ≤ skor < 60 | `'D'` |
| 0 ≤ skor < 50 | `'E'` |
| skor < 0 atau skor > 100 | `ValueError` |
| bukan `int`/`float` (termasuk `bool`, `str`, `None`) | `TypeError` |

**B1 — Partisi & nilai batas.** Disusun 12 partisi (6 valid, 6 tidak valid) dan 14 nilai batas, misalnya `-0.01`, `0`, `49.99`, `50`, `79.99`, `80`, `100`, `100.01`.

**B2 — Siklus TDD.** Pengembangan dilakukan dalam 4 siklus, masing-masing dengan output merah lalu hijau yang terlihat di notebook:

1. Skor valid menghasilkan huruf yang benar (`90` → `'A'`).
2. Huruf B sampai E dan semua nilai batas di dalam 0–100.
3. Skor di luar 0–100 menghasilkan `ValueError`.
4. Tipe yang salah (`bool`, `str`, `None`, `list`) menghasilkan `TypeError`.

**B3 — Kumpulan tes lengkap.** Kelas `TestNilaiHuruf` berisi **26 tes**, semuanya memakai komentar `# Arrange`, `# Action`, `# Assert`, dan **semuanya lulus** (`OK`).

**B4 — Menguji implementasi orang lain.** Tes dijalankan terhadap `nilai_huruf_v2` yang mengandung bug. Hasilnya **3 tes gagal** dan dua bug *off-by-one* ditemukan:

| Tes yang gagal | Bug | Baris |
|---|---|---|
| `test_batas_80_mendapat_A` | Memakai `skor > 80`, seharusnya `skor >= 80`. | `if skor > 80:` |
| `test_batas_100_01_ValueError` | Memakai `skor > 101`, seharusnya `skor > 100`. | `if skor < 0 or skor > 101:` |
| `test_batas_101_ValueError` | Bug yang sama: skor 101 lolos dan mendapat `'A'`. | `if skor < 0 or skor > 101:` |

> Tes yang hanya memakai wakil partisi (mis. `90`, `75`, `150`) tidak menemukan bug ini. Bug baru tertangkap oleh tes **tepat di atau di sebelah batas**.

### Bagian C — Refleksi

Refleksi sekitar 300 kata tentang:

1. Kelebihan dan kesulitan TDD yang dialami sendiri, dibandingkan dengan Table 9.10.
2. Cara memastikan tes yang ditulis **bisa gagal**, berbeda dengan `test_shortname`.

---

## 🚀 Cara Menjalankan

Tidak ada dependensi tambahan. Cukup Python 3 dan Jupyter (`unittest` sudah bawaan Python).

### Opsi 1 — Jupyter lokal

```bash
git clone https://github.com/anugrahhhhh/tugas-software-testing.git
cd tugas-software-testing
pip install notebook
jupyter notebook Tugas_Testing_26_59120_PPA_07385.ipynb
```

Lalu pilih **Kernel → Restart & Run All**.

### Opsi 2 — VS Code

Buka file `.ipynb` dengan ekstensi **Jupyter**, pilih interpreter Python, lalu klik **Run All**.

### Opsi 3 — Google Colab

Buka [colab.research.google.com](https://colab.research.google.com), pilih **File → Upload notebook**, unggah file `.ipynb`, lalu jalankan semua sel.

---

## 🛠️ Teknologi

- **Python 3**
- **`unittest`**: framework pengujian bawaan Python
- **Jupyter Notebook**

## 📚 Referensi

- Sommerville, I. *Engineering Software Products: An Introduction to Modern Software Engineering*. Pearson, 2020. Bab 9: *Testing*.
- Dokumentasi Python: [`unittest` — Unit testing framework](https://docs.python.org/3/library/unittest.html)

---

<sub>Tugas mata kuliah Software Testing — Kuliah Asinkron.</sub>
