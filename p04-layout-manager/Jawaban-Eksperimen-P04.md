# Jawaban Eksperimen P04

## Praktikum 2: Galeri Layout Manager

### 1. flowPanel: Alignment diubah jadi Center
Tombol-tombol jadi rata tengah di setiap baris. Saat jendela dikecilkan, tombol pindah baris tapi tetap di tengah.
Baris yang berubah di `initComponents()`:
```java
flowPanel.setLayout(new java.awt.FlowLayout(java.awt.FlowLayout.CENTER, 8, 8));
```
(sebelumnya `LEFT`, sekarang `CENTER`)

### 2. gridPanel: Rows 0 dan Columns 2
Terbentuk 5 baris. Kolom dipatok 2, jadi 9 tombol dibagi 2 = 4 baris penuh + 1 tombol sisa di baris terakhir. Jumlah baris dihitung otomatis.
```java
gridPanel.setLayout(new java.awt.GridLayout(0, 2, 8, 8));
```

### 3. boxPanel: maximumSize lebar 32767 + Vertical Strut
Tombol jadi melebar penuh selebar panel, karena lebar maksimumnya (32767) melebihi lebar panel. Vertical Strut menambah jarak antar tombol supaya tidak rapat.

## Praktikum 4: Form Biodata

### 1. Weight X namaField diubah jadi 0.0
`namaField` tidak ikut melebar lagi, tetap di lebar aslinya. Saat jendela dilebarkan, sisa ruang di kanan jadi kosong.

### 2. Direction formPanel di isiPanel dari North ke Center
Form pindah ke tengah. Saat jendela ditinggikan, form "mengambang" di tengah, tidak menempel di atas lagi.

### 3. Baris setMinimumSize(getSize()) dihapus
Jendela bisa dikecilkan sampai komponen terpotong. Yang rusak duluan bagian isian di kanan, lalu tombol Batal dan Simpan.

## Saran dari Teman (Tahap 4)

Nama teman: Randy Firmansyah (2410010268)

Pemeriksaan 8 butir daftar periksa: terpenuhi semua.

Saran:
1. Placeholder pada Email dan Nomor HP sudah bagus. Sebaiknya field NPM juga diberi placeholder (contoh: 2410010001) supaya pengguna langsung tahu format penulisannya.
