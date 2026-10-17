# Jawaban Eksperimen P04

## Praktikum 2: Galeri Layout Manager

### 1. flowPanel: Alignment diubah menjadi Center
Baris tombol yang tidak penuh ikut merata ke tengah panel; saat jendela dikecilkan, tombol pindah baris dan setiap baris tetap rata tengah.
Baris `initComponents()` yang berubah:
```java
flowPanel.setLayout(new java.awt.FlowLayout(java.awt.FlowLayout.CENTER, 8, 8));
```
(Nilai `LEFT` menjadi `CENTER`.)

### 2. gridPanel: Rows 0 dan Columns 2
Terbentuk 5 baris. Dengan `GridLayout(0, 2, 8, 8)` jumlah kolom ditetapkan 2 sehingga baris dihitung otomatis dari jumlah komponen: 9 tombol / 2 kolom = 5 baris (baris terakhir berisi satu tombol).
Baris kode menjadi:
```java
gridPanel.setLayout(new java.awt.GridLayout(0, 2, 8, 8));
```

### 3. boxPanel: maximumSize lebar 32767 + Vertical Strut
Tombol melebar memenuhi lebar panel karena lebar maksimum tombol (32767) melebihi lebar panel, dan BoxLayout mengikuti ukuran maksimum komponen. `Vertical Strut` dari Swing Fillers menyisipkan jarak vertikal tetap di antara tombol sehingga jarak antar tombol sama.

## Praktikum 4: Form Biodata

### 1. Weight X `namaField` diubah menjadi 0.0
`namaField` tidak ikut melebar saat jendela dilebarkan; isian tetap pada lebar asli (20 kolom) dan sisa ruang tidak diserap kolom isian.

### 2. Direction `formPanel` di dalam `isiPanel` dari North menjadi Center
`formPanel` mengambang di tengah `isiPanel` saat jendela ditinggikan, bukan menempel di atas; baris form tidak lagi terkunci di posisi atas.

### 3. Baris `setMinimumSize(getSize())` dihapus
Jendela dapat dikecilkan melebihi ukuran awal sehingga isian (kolom isian di kanan) terpotong lebih dulu, disusul tombol Batal dan Simpan yang ikut terpotong.

## Saran dari Teman (Tahap 4)

> (Diisi setelah saling menilai di kelas)
