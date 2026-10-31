# p06-validasi-input

Praktikum Pemrograman Berbasis Objek 2 — Pertemuan 6: Validasi Input dan Kegunaan.

- Nama: M. Reza Ikhsan Fadila
- NPM: 2410010279
- Kelas: 5B
- Mata kuliah: Pemrograman Berbasis Objek 2 (TIF1508)
- Repository: pbo2-2410010279

## Struktur Proyek

```
p06-validasi-input/
├── pom.xml
├── README.md
├── Refleksi-P06-2410010279.md
├── Deklarasi-Penggunaan-AI.md
├── Lembar-Peer-Review-Heuristik.pdf
├── Tabel-Temuan-Peer-Review.md
├── screenshot/
└── src/main/java/id/ac/uniska/pbo2/p06/
    ├── Validator.java                  (Praktikum 2)
    ├── UjiValidator.java               (Praktikum 2)
    ├── FormAnggota.java                (Praktikum 3 dan 4)
    ├── FormAnggota.form                (desain GUI Builder)
    ├── FormAnggotaPerpustakaan.java    (Latihan Mandiri, lanjutan Pertemuan 5)
    └── FormAnggotaPerpustakaan.form    (desain GUI Builder)
```

## Cara Menjalankan

Di NetBeans: buka proyek `p06-validasi-input`, klik kanan `UjiValidator.java` atau
`FormAnggota.java`, lalu **Run File**. Dari terminal:

```
javac -d build/classes -cp <flatlaf.jar> src/main/java/id/ac/uniska/pbo2/p06/*.java
java -cp "build/classes;<flatlaf.jar>" id.ac.uniska.pbo2.p06.UjiValidator
java -cp "build/classes;<flatlaf.jar>" id.ac.uniska.pbo2.p06.FormAnggota
java -cp "build/classes;<flatlaf.jar>" id.ac.uniska.pbo2.p06.FormAnggotaPerpustakaan
```

Dependency: `com.formdev:flatlaf:3.5.4`.

## Praktikum 2 — Validator

Aturan validasi dikumpulkan di `Validator`: kelas utilitas, konstruktor privat, semua
method `static`, dan tidak bergantung pada GUI. Tiap method mengembalikan pesan kesalahan,
atau `null` bila nilai valid.

Keluaran `UjiValidator` (semua baris SESUAI):

```
SESUAI NPM kosong: NPM wajib diisi
SESUAI NPM 5 digit: NPM harus berisi 10 digit angka
SESUAI NPM berisi huruf: NPM harus berisi 10 digit angka
SESUAI NPM benar: valid
SESUAI Nama terlalu pendek: Nama minimal 3 huruf
SESUAI Nama berisi angka: Nama tidak boleh berisi angka
SESUAI Nama benar: valid
SESUAI Email tanpa domain: Format email belum benar, contoh: nama@contoh.com
SESUAI Email benar: valid
SESUAI Nomor HP terlalu pendek: Nomor HP diawali 08 dan berisi 10 sampai 13 digit
SESUAI Nomor HP diawali 62: Nomor HP diawali 08 dan berisi 10 sampai 13 digit
SESUAI Nomor HP 12 digit: valid

Semua aturan bekerja sesuai harapan
```

Aturan `Nama berisi angka` adalah tambahan dari Latihan Mandiri nomor 2.

## Praktikum 3 — FormAnggota

Judul jendela: **Pendaftaran Anggota Perpustakaan**.

| Panel | Layout | Isi |
|---|---|---|
| headerPanel | North, BoxLayout Y | judulLabel, keteranganLabel |
| isiPanel | Center, BorderLayout | formPanel di North |
| formPanel | GridBagLayout | isian dan label pesan |
| bawahPanel | South, BorderLayout | statusLabel di Center, tombolPanel di East |

Urutan isian: NPM, Nama lengkap, Program studi, Jenis anggota, Email, Nomor HP, Alamat,
dan checkbox setuju. Setiap isian yang divalidasi punya label pesan di bawahnya; label
kosong diisi satu spasi agar tinggi baris tetap.

Aksesibilitas:

| Teknik | Diterapkan pada |
|---|---|
| labelFor | npmLabel→npmField, namaLabel→namaField, prodiLabel→prodiCombo, jenisAnggotaLabel→mahasiswaRadio, emailLabel→emailField, hpLabel→hpField, alamatLabel→alamatArea |
| displayedMnemonic | P, N, R, J, E, H, L |
| mnemonic | M/D/U pada radio, T pada setujuCheck, B pada batalButton |
| toolTipText | npmField: "Hanya angka, tepat 10 digit" |

Semua properti aksesibilitas tersimpan di file `.form` dan `initComponents()`, jadi form
sudah bisa dipakai dengan keyboard tanpa kode tambahan.

## Praktikum 4 — Validasi melalui Event Handler

| Komponen | Event | Isi handler |
|---|---|---|
| npmField | Key: keyTyped | menolak karakter bukan angka dan digit ke-11 dengan `evt.consume()` |
| npmField, namaField, emailField, hpField | Focus: focusLost | memeriksa isian yang sudah diisi |
| prodiCombo | Item: itemStateChanged | memeriksa pilihan saat `ItemEvent.SELECTED` |
| setujuCheck | Item: itemStateChanged | mengaktifkan daftarButton |
| batalButton, daftarButton | Action: actionPerformed | memanggil `batal()` atau `daftar()` |

### Jawaban Eksperimen

1. **Huruf pada NPM.** Huruf tidak masuk karena `evt.consume()` di `npmFieldKeyTyped`;
   isian juga berhenti di 10 digit.
2. **Email `siti@` lalu Tab.** Pesan muncul saat Tab ditekan karena `emailFieldFocusLost`
   memanggil `periksaEmail()`.
3. **Nama dikosongkan lalu Tab.** Tidak ada pesan karena focusLost hanya memeriksa isian
   tidak kosong. Isian kosong baru diperiksa saat Daftar diklik.
4. **Daftar dengan form kosong.** Lima isian bergaris merah, status "5 isian perlu
   diperbaiki", dan fokus pindah ke npmField.
5. **Alt+N.** Fokus pindah ke namaField melalui `displayedMnemonic` dan `labelFor`.
6. **Batal lalu No.** Data tetap ada karena `batal()` langsung `return` bila jawabannya
   bukan `YES_OPTION`.

Tangkapan layar: `screenshot/form-anggota-awal.png` dan
`screenshot/form-anggota-pesan-kesalahan.png`.

## Praktikum 5 — Menyimpan ke GitHub

```
git status
git add .
git commit -m "P06: validasi input dan umpan balik pada form anggota"
git push
```

## Latihan Mandiri — FormAnggotaPerpustakaan

Form Pertemuan 5 ditambah label pesan di bawah tiap isian, `digitLabel`, dan `statusLabel`
di kiri bawah. Susunan dasarnya tetap.

| No | Ketentuan | Bukti |
|---|---|---|
| 1 | Aturan NPM, nama, email, nomor HP di kelas Validator | form hanya memanggil `Validator.npm/nama/email/nomorHp` |
| 2 | Nama tidak boleh berisi angka, diuji di UjiValidator | pola `.*\\d.*` dan baris `Nama berisi angka` |
| 3 | Isian salah bergaris merah dan berpesan | `tandai()` memasang `JComponent.outline = "error"` dan mengisi label |
| 4 | NPM dan Nomor HP hanya menerima angka | `npmFieldKeyTyped` (maks. 10) dan `hpFieldKeyTyped` (maks. 13) |
| 5 | Ringkasan kesalahan dan fokus ke kesalahan pertama | `statusLabel` + `salah.get(0).requestFocusInWindow()` |
| 6 | Konfirmasi sebelum mengosongkan form | `batal()` memeriksa `adaIsian()` lalu menampilkan konfirmasi |
| 7 | labelFor, displayedMnemonic, mnemonic, toolTipText | lihat tabel aksesibilitas di atas |

Hasil uji: nama `"Reza 2"` ditolak, ketikan `x` pada NPM dan `-` pada Nomor HP ditolak,
dan form kosong menghasilkan "5 isian perlu diperbaiki".

## Catatan Pengumpulan

- File `.java` dan `.form` kedua form sudah ada, jadi bisa dibuka di tab Design NetBeans.
- Bukti di `screenshot/`: form awal, form dengan pesan kesalahan, Navigator
  (`navigator-form-anggota-perpustakaan.png`), dan keluaran `UjiValidator`
  (`output-uji-validator.txt`).
- Lembar peer review diisi teman pada `Lembar-Peer-Review-Heuristik.pdf`; temuannya
  direkap di `Tabel-Temuan-Peer-Review.md` (semua skor 0–2, tidak ada perbaikan wajib).
- Tambahan hanya `digitLabel`, label pesan, `keteranganLabel`, dan `toolTipText`; susunan
  dasar, garis merah, ringkasan status, dan fokus ke kesalahan pertama tetap sama.
