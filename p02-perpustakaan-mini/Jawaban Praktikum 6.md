# Jawaban Modul PBO 2 - Pertemuan 2 (Perpustakaan Mini)

Nama: M. Reza Ikhsan Fadila
NPM: 2410010279

## C. Praktikum 6 - Eksperimen

### 1. `new Koleksi(...)`
Error `Koleksi is abstract`, karena kelas abstrak tidak dapat diinstansiasi.

### 2. `hitungDenda` → `hitungdenda`
Dengan `@Override`: error "does not override" (nama berbeda). Tanpa `@Override`: tetap error karena method belum diimplementasikan. Java case-sensitive.

### 3. `new Buku("B009", "", 2020, "Anonim")`
Program berhenti: `IllegalArgumentException: Judul tidak boleh kosong` (judul `""` dianggap kosong).

### 4. `status` jadi `public`, B002 dipaksa `TERSEDIA`
Tidak error, tetapi tidak konsisten karena masih dipinjam. Enkapsulasi dilanggar; status seharusnya hanya lewat `pinjam()`/`kembalikan()`.
