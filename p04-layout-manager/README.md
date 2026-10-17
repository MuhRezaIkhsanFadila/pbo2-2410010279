# p04-layout-manager

Proyek Maven Praktikum PBO 2 Pertemuan 4: Layout Manager dan Desain Form.

- Group Id: `id.ac.uniska.pbo2`
- Package: `id.ac.uniska.pbo2.p04`
- Tema: FlatLaf 3.5.4

## Form

| Kelas | Keterangan |
| --- | --- |
| `GaleriLayout` | Galeri lima layout manager dalam Tabbed Pane |
| `FormBiodata` | Form biodata dengan BorderLayout + BoxLayout + GridBagLayout |
| `FormAnggotaPerpustakaan` | Studi kasus Perpustakaan Mini (Studio Desain) |

## Tabel Rancangan Form Anggota Perpustakaan

| Bagian | Panel | Layout |
| --- | --- | --- |
| Jendela | JFrame | BorderLayout |
| Header | `headerPanel` | BoxLayout, Y Axis |
| Isi form | `formPanel` (di dalam `isiPanel`, posisi North) | GridBagLayout |
| Tombol | `tombolPanel` | FlowLayout, Alignment Right |

## Sketsa Form

```
+---------------------------------------------------+
| headerPanel  (BoxLayout Y)                        |
|   judulLabel, keteranganLabel                     |
+---------------------------------------------------+
| isiPanel (BorderLayout)                           |
|   formPanel (GridBagLayout) - NORTH               |
|   Data Anggota: NPM, Nama, Prodi, Jenis anggota   |
|   Kontak: Email, HP, Alamat                       |
|   Persetujuan: setujuCheckBox                     |
+---------------------------------------------------+
| tombolPanel (FlowLayout RIGHT)                    |
|   batalButton, daftarButton                       |
+---------------------------------------------------+
```

## Panduan Desain di GUI Builder (tab Design)

File `.java` di proyek ini sudah berisi `initComponents()` sesuai modul dan dapat dijalankan langsung.
Untuk memunculkan tab Design dan file `.form`, buat form di GUI Builder mengikuti langkah modul,
lalu samakan nama komponen dengan daftar berikut (urutan `Insets`: atas, kiri, bawah, kanan).

### GaleriLayout

| Panel (tab) | Layout | Properti |
| --- | --- | --- |
| `borderPanel` | BorderLayout | HGap 8, VGap 8, Empty Border 12 |
| `flowPanel` | FlowLayout | Left, HGap 8, VGap 8, Empty Border 12 |
| `gridPanel` | GridLayout | Rows 3, Columns 3, HGap 8, VGap 8, Empty Border 12 |
| `boxPanel` | BoxLayout | Y Axis, Empty Border 12 |
| `gabunganPanel` | BorderLayout | HGap 8, VGap 8, Empty Border 12 |

- Semua panel memakai Empty Border 12 di keempat sisi.
- `borderPanel`: `northButton`, `southButton`, `westButton`, `eastButton`, `centerButton` (Direction sesuai nama).
- `flowPanel`: `baruButton`, `bukaButton`, `simpanButton`, `simpanSebagaiButton`, `cetakButton`, `bagikanButton`, `keluarButton`.
- `gridPanel`: `tombol1` s.d. `tombol9` (teks 1-9).
- `boxPanel`: `dashboardButton`, `dataMahasiswaButton`, `dataMataKuliahButton`, `laporanButton`.
- `gabunganPanel`: North `catatanJudulLabel`, Center `catatanTextArea`, West `hariPanel` (BoxLayout Y: `seninButton`, `selasaButton`, `rabuButton`), South `aksiPanel` (FlowLayout Right, HGap 8, VGap 0: `hapusButton`, `simpanAksiButton`).
- Tab Title: BorderLayout, FlowLayout, GridLayout, BoxLayout, Gabungan.

### FormBiodata

| Bagian | Panel | Layout | Empty Border |
| --- | --- | --- | --- |
| Jendela | JFrame | BorderLayout | - |
| Header (North) | `headerPanel` | BoxLayout, Y Axis | 16, 16, 8, 16 |
| Pembungkus (Center) | `isiPanel` | BorderLayout | - |
| Isi form (North di `isiPanel`) | `formPanel` | GridBagLayout | 8, 16, 8, 16 |
| Tombol (South) | `tombolPanel` | FlowLayout, Right | 8, 16, 16, 16 |

`formPanel` (GridBagLayout):

| Komponen | Grid X | Grid Y | Grid Width | Fill | Anchor | Weight X | Insets |
| --- | --- | --- | --- | --- | --- | --- | --- |
| `dataDiriLabel` | 0 | 0 | 2 | None | West | 0.0 | 0, 0, 6, 0 |
| `namaLabel` | 0 | 1 | 1 | None | West | 0.0 | 6, 0, 6, 12 |
| `namaField` | 1 | 1 | 1 | Horizontal | Center | 1.0 | 4, 0, 4, 0 |
| `npmLabel` / `npmField` | 0 / 1 | 2 | 1 | - / Horizontal | West / Center | 0.0 / 1.0 | 6, 0, 6, 12 / 4, 0, 4, 0 |
| `prodiLabel` / `prodiCombo` | 0 / 1 | 3 | 1 | - / Horizontal | West / Center | 0.0 / 1.0 | 6, 0, 6, 12 / 4, 0, 4, 0 |
| `semesterLabel` / `semesterSpinner` | 0 / 1 | 4 | 1 | - / Horizontal | West / Center | 0.0 / 1.0 | 6, 0, 6, 12 / 4, 0, 4, 0 |
| `kontakLabel` | 0 | 5 | 2 | None | West | 0.0 | 16, 0, 6, 0 |
| `emailLabel` / `emailField` | 0 / 1 | 6 | 1 | - / Horizontal | West / Center | 0.0 / 1.0 | 6, 0, 6, 12 / 4, 0, 4, 0 |
| `hpLabel` / `hpField` | 0 / 1 | 7 | 1 | - / Horizontal | West / Center | 0.0 / 1.0 | 6, 0, 6, 12 / 4, 0, 4, 0 |
| `alamatLabel` | 0 | 8 | 1 | None | Northwest | 0.0 | 6, 0, 6, 12 |
| `alamatTextArea` | 1 | 8 | 1 | Horizontal | Center | 1.0 | 4, 0, 4, 0 |

- `prodiCombo`: Teknik Informatika, Sistem Informasi, Manajemen Informatika.
- `semesterSpinner`: model Custom code `new javax.swing.SpinnerNumberModel(5, 1, 14, 1)`.
- Properti `labelFor` setiap label diarahkan ke isian pasangannya.
- Kode tambahan di konstruktor: gaya FlatLaf, placeholder, tombol default, `pack()`, `setMinimumSize(getSize())`, `setLocationRelativeTo(null)`.

### FormAnggotaPerpustakaan

Struktur sama dengan FormBiodata. Isi `formPanel` (GridBagLayout):

| Grid Y | Kolom 0 (label) | Kolom 1 (isian) |
| --- | --- | --- |
| 0 | `dataAnggotaLabel` (Grid Width 2) | - |
| 1 | `npmLabel` | `npmField` |
| 2 | `namaLabel` | `namaField` |
| 3 | `prodiLabel` | `prodiCombo` |
| 4 | `jenisAnggotaLabel` | `jenisAnggotaPanel` (FlowLayout Left: `mahasiswaRadio`, `dosenRadio`, `umumRadio`, ButtonGroup `jenisAnggotaGroup`) |
| 5 | `kontakLabel` (Grid Width 2) | - |
| 6 | `emailLabel` | `emailField` |
| 7 | `hpLabel` | `hpField` |
| 8 | `alamatLabel` (Anchor Northwest) | `alamatTextArea` |
| 9 | - | `setujuCheckBox` ("Setuju dengan tata tertib perpustakaan") |

- Tombol: `batalButton` (Batal) dan `daftarButton` (Daftar) di `tombolPanel`, `daftarButton` sebagai tombol default.
- Constraint label/isian sama dengan tabel FormBiodata.

## Tangkapan Layar

Simpan tangkapan layar di folder `screenshot/`:

1. `FormAnggotaPerpustakaan` ukuran awal.
2. `FormAnggotaPerpustakaan` saat dilebarkan.
3. Tab Design + Navigator `FormAnggotaPerpustakaan`.
4. Foto sketsa form (boleh disisipkan di README ini).
