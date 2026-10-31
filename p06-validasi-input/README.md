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
├── Lembar-Peer-Review-Heuristik.md
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
`FormAnggota.java` lalu pilih **Run File**. Dari terminal:

```
javac -d build/classes -cp <flatlaf.jar> src/main/java/id/ac/uniska/pbo2/p06/*.java
java -cp "build/classes;<flatlaf.jar>" id.ac.uniska.pbo2.p06.UjiValidator
java -cp "build/classes;<flatlaf.jar>" id.ac.uniska.pbo2.p06.FormAnggota
java -cp "build/classes;<flatlaf.jar>" id.ac.uniska.pbo2.p06.FormAnggotaPerpustakaan
```

Dependency yang dipakai: `com.formdev:flatlaf:3.5.4` (sama seperti Pertemuan 3).

## Praktikum 2 — Kelas Validator dan Pengujiannya

Aturan validasi dikumpulkan di `Validator` (kelas utilitas, konstruktor privat, semua
method `static`), sehingga tidak bergantung pada GUI. Setiap method mengembalikan pesan
kesalahan, atau `null` bila nilai sudah benar.

Keluaran `UjiValidator` (seluruh baris bertanda SESUAI):

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

Baris `Nama berisi angka` adalah aturan baru dari Latihan Mandiri nomor 2.

## Praktikum 3 — FormAnggota di GUI Builder

Judul jendela: **Pendaftaran Anggota Perpustakaan**. Susunan panel:

| Panel | Layout | Isi |
|---|---|---|
| headerPanel | North, BoxLayout Y | judulLabel, keteranganLabel |
| isiPanel | Center, BorderLayout | formPanel di North |
| formPanel | GridBagLayout | isian dan label pesan |
| bawahPanel | South, BorderLayout | statusLabel di Center, tombolPanel di East |

Isian pada formPanel (Grid Y sesuai modul), setiap isian validasi punya Label pesan di
baris bawahnya dengan teks satu spasi agar tinggi baris tetap:

| Grid Y | Kolom 0 | Kolom 1 |
|---|---|---|
| 0 | Data Anggota (Grid Width 2) | |
| 1 | NPM | npmField |
| 2 | | npmPesanLabel |
| 3 | Nama lengkap | namaField |
| 4 | | namaPesanLabel |
| 5 | Program studi | prodiCombo (Pilih program studi, Teknik Informatika, Sistem Informasi, Manajemen Informatika) |
| 6 | | prodiPesanLabel |
| 7 | Jenis anggota | jenisPanel (mahasiswaRadio, dosenRadio, umumRadio) |
| 8 | Kontak (Grid Width 2) | |
| 9 | Email | emailField |
| 10 | | emailPesanLabel |
| 11 | Nomor HP | hpField |
| 12 | | hpPesanLabel |
| 13 | Alamat (Anchor Northwest) | alamatArea |
| 14 | | setujuCheck |

Aksesibilitas dan bantuan:

| Teknik | Diterapkan pada |
|---|---|
| labelFor | npmLabel→npmField, namaLabel→namaField, prodiLabel→prodiCombo, emailLabel→emailField, hpLabel→hpField, alamatLabel→alamatArea |
| displayedMnemonic | P (NPM), N (Nama), R (Program studi), J (Jenis anggota), E (Email), H (Nomor HP), L (Alamat) |
| mnemonic | M/D/U pada radio button, T pada setujuCheck, B pada batalButton |
| toolTipText | npmField: "Hanya angka, tepat 10 digit" |
| urutan komponen | mengikuti urutan baca pada Navigator |

Catatan: properti `labelFor` dan `toolTipText` tersimpan di file `.form`. Nilai
`displayedMnemonic` dan `mnemonic` ditulis di konstruktor setelah `initComponents()`
karena penulisannya melalui file `.form` hanya dihasilkan otomatis oleh editor desain
NetBeans; hasil di layar tetap sama (Alt + huruf memindahkan fokus).

## Praktikum 4 — Validasi melalui Event Handler

| Komponen | Menu Events | Isi event handler |
|---|---|---|
| npmField | Key: keyTyped | membatalkan karakter bukan angka dan digit ke-11 dengan `evt.consume()` |
| npmField, namaField, emailField, hpField | Focus: focusLost | memeriksa isian yang sudah diisi |
| prodiCombo | Item: itemStateChanged | memeriksa pilihan saat `ItemEvent.SELECTED` |
| setujuCheck | Item: itemStateChanged | mengaktifkan daftarButton |
| batalButton, daftarButton | Action: actionPerformed | memanggil `batal()` atau `daftar()` |

### Jawaban Eksperimen Praktikum 4

1. **Ketik huruf pada isian NPM.** Huruf tidak masuk ke isian sama sekali; yang tercetak
   hanya angka. Penyebabnya baris

   ```java
   if (!Character.isDigit(evt.getKeyChar()) || penuh) {
       evt.consume(); // karakter tidak dimasukkan ke isian
   }
   ```

   pada `npmFieldKeyTyped`. `evt.consume()` menandai event sudah ditangani sehingga
   karakter tidak diteruskan ke isian. Hasil uji: mengetik `A`, `b`, `2` menyisakan
   isi `"2"`, dan saat isian sudah 10 digit ketikan berikutnya diabaikan (`"2410010123"`
   tetap 10 digit).

2. **Isi email dengan `siti@`, lalu tekan Tab.** Pesan kesalahan muncul **saat Tab
   ditekan**, bukan saat mengetik. Tab membuat emailField kehilangan fokus, sehingga
   `emailFieldFocusLost` berjalan dan memanggil `periksaEmail()`. Hasil uji:
   `emailPesanLabel` berisi "Format email belum benar, contoh: nama@contoh.com".

3. **Klik isian Nama tanpa mengetik, lalu tekan Tab.** Tidak ada pesan kesalahan, karena
   `namaFieldFocusLost` lebih dahulu memeriksa `if (!namaField.getText().isBlank())`.
   Isian kosong sengaja tidak ditandai saat pengguna hanya melewatinya; isian kosong baru
   diperiksa ketika tombol Daftar diklik. Hasil uji: `namaPesanLabel` tetap berisi spasi.

4. **Centang persetujuan, lalu klik Daftar dengan form kosong.** Kelima isian bertanda
   merah, `statusLabel` berbunyi "5 isian perlu diperbaiki", dan fokus berpindah ke
   **npmField** karena `daftar()` memanggil `salah.get(0).requestFocusInWindow()` dan
   NPM adalah isian pertama yang diperiksa.

5. **Tekan Alt bersama huruf N.** Fokus berpindah ke **namaField**. Yang mengaturnya
   adalah properti `displayedMnemonic` bernilai N pada `namaLabel` yang dipasangkan
   dengan `labelFor` = namaField: saat mnemonic diaktifkan, label meminta fokus untuk
   komponen `labelFor`-nya.

6. **Isi beberapa isian, klik Batal, lalu pilih No.** Data tetap ada. `batal()` memanggil
   `JOptionPane.showConfirmDialog` lebih dahulu dan langsung `return` bila jawabannya
   bukan `YES_OPTION`, sehingga `kosongkan()` tidak dijalankan. Hasil uji: setelah
   menekan No, NPM masih "2410010123" dan Nama masih "Siti Rahmah".

Tangkapan layar: `screenshot/form-anggota-awal.png` (form saat pertama dibuka) dan
`screenshot/form-anggota-pesan-kesalahan.png` (setelah Daftar diklik dengan data salah).

## Praktikum 5 — Menyimpan ke GitHub

```
git status
git add .
git commit -m "P06: validasi input dan umpan balik pada form anggota"
git push
```

## Latihan Mandiri — FormAnggotaPerpustakaan

Form dari Pertemuan 5 dikembangkan tanpa mengubah susunan dasarnya (headerPanel,
formPanel GridBagLayout, tombolPanel) dengan tambahan baris label pesan di bawah setiap
isian dan statusLabel di kiri bawah.

| No | Ketentuan | Bukti |
|---|---|---|
| 1 | Aturan NPM, nama, email, nomor HP di kelas Validator | `FormAnggotaPerpustakaan` hanya memanggil `Validator.npm/nama/email/nomorHp` lewat `periksaNpm()`, `periksaNama()`, `periksaEmail()`, `periksaHp()` |
| 2 | Nama tidak boleh berisi angka, diuji di UjiValidator | `Validator.nama` menambah pola `.*\\d.*`; UjiValidator memuat baris `Nama berisi angka` |
| 3 | Isian salah bergaris merah dan berpesan di bawahnya | `tandai()` memasang `JComponent.outline = "error"` dan mengisi label pesan; lihat `screenshot/form-anggota-perpustakaan-kesalahan.png` |
| 4 | NPM dan nomor HP hanya menerima angka lewat keyTyped | `npmFieldKeyTyped` (maks. 10 digit) dan `hpFieldKeyTyped` (maks. 13 digit) |
| 5 | Ringkasan jumlah kesalahan dan fokus ke kesalahan pertama | `statusLabel.setText(salah.size() + " isian perlu diperbaiki")` lalu `salah.get(0).requestFocusInWindow()` |
| 6 | Konfirmasi sebelum mengosongkan form berisi data | `batal()` memeriksa `adaIsian()` lalu menampilkan `JOptionPane.showConfirmDialog` |
| 7 | labelFor, displayedMnemonic, mnemonic, toolTipText | lihat tabel aksesibilitas di atas; toolTipText juga pada hpField |

Hasil uji: nama `"Reza 2"` ditolak dengan pesan "Nama tidak boleh berisi angka";
ketikan `x` pada NPM dan `-` pada Nomor HP ditolak; form kosong menghasilkan
"5 isian perlu diperbaiki".

## Catatan Pengumpulan

- File `.java` dan `.form` untuk kedua form sudah ada di dalam proyek, jadi keduanya
  dapat dibuka pada tab Design NetBeans.
- Tangkapan layar jendela Navigator (memperlihatkan label pesan) perlu diambil langsung
  di NetBeans pada komputer sendiri: buka `FormAnggota.java` di tab Design, buka jendela
  **Window → Navigator**, lalu tangkap layarnya.
- Lembar peer review diisi oleh teman (`Lembar-Peer-Review-Heuristik.md`), lalu temuannya
  dicatat pada `Tabel-Temuan-Peer-Review.md` beserta commit perbaikannya.
