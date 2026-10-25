# p05-event-handling

Praktikum Pemrograman Berbasis Objek 2 — Pertemuan 5: Event Handling.

## Tabel Pengamatan Praktikum 2

| No | Tindakan | Event yang tercatat |
|---|---|---|
| 1 | Arahkan kursor ke tombol, lalu jauhkan | MouseEvent: kursor masuk ke tombol; MouseEvent: kursor keluar dari tombol |
| 2 | Klik tombol Klik saya | ActionEvent: tombol diklik |
| 3 | Centang lalu hapus centang Aktifkan fitur | ItemEvent: kotak dicentang; ItemEvent: centang dihapus |
| 4 | Ganti pilihan dari Pagi menjadi Malam | ItemEvent: memilih Malam |
| 5 | Klik isian, lalu ketik kata "abc" | FocusEvent: isian mendapat fokus; KeyEvent: mengetik huruf a; KeyEvent: mengetik huruf b; KeyEvent: mengetik huruf c |
| 6 | Klik tombol setelah mengetik di isian | FocusEvent: isian kehilangan fokus; ActionEvent: tombol diklik |

## Jawaban Eksperimen Praktikum 3 (Konversi Suhu)

1. Setelah pemeriksaan `if (evt.getStateChange() == ItemEvent.SELECTED)` dihapus dan `System.out.println("item berubah");` ditambahkan, pesan tercetak **dua kali** setiap pilihan diganti. Sebabnya `itemStateChanged` pada Combo Box dipanggil dua kali: sekali untuk pilihan lama (DESELECTED) dan sekali untuk pilihan baru (SELECTED).

2. Hasil tampak terlambat satu karakter karena `keyPressed` dipicu **sebelum** karakter yang diketik masuk ke dalam JTextField. Saat event dijalankan, `getText()` masih mengembalikan teks lama. `keyReleased` dipicu **setelah** karakter masuk, sehingga teks sudah lengkap.

3. Jika blok `try` dan `catch` dihapus lalu diketik huruf, jendela Output menampilkan **NumberFormatException** (stack trace) yang tidak tertangani, karena `Double.parseDouble(...)` gagal mengubah huruf menjadi angka.

## Jawaban Eksperimen Praktikum 4 (Kalkulator Sederhana)

1. Pesan `kali` tercetak **dua kali**. Tombol kaliButton memakai dua cara sekaligus (lambda di konstruktor dan event actionPerformed dari GUI Builder), sehingga dua listener terdaftar dan keduanya dijalankan untuk satu klik. Karena itu satu tombol sebaiknya hanya memakai satu cara agar aksi tidak berjalan dua kali.

2. Yang diubah di tab Design: menambahkan satu tombol baru (mis. `modButton` dengan teks "%") ke dalam operatorPanel dan mengubah jumlah kolom GridLayout operatorPanel dari 4 menjadi 5. Yang diubah di tab Source: menambahkan deklarasi variabel `modButton`, menambahkan event handler (atau lambda) yang memanggil `hitung('%')`, dan menambahkan `case '%' -> a % b` pada blok switch di method `hitung`.

3. Kursor langsung berada di isian pertama karena method `hapus()` memanggil `angka1Field.requestFocusInWindow()` yang mengembalikan fokus ke isian pertama setelah semua isian dikosongkan.

## Peta Event FormAnggotaPerpustakaan

| Komponen | Menu Events | Event | Aksi |
|---|---|---|---|
| Kotak centang setuju | Item | itemStateChanged | Tombol Daftar hanya aktif jika dicentang |
| Tombol Batal | Action | actionPerformed | Kosongkan semua isian dan kembalikan fokus ke NPM |
| Tombol Daftar | Action | actionPerformed | Tampilkan ringkasan data dengan JOptionPane |
| Isian NPM | Key | keyReleased | Label kecil menampilkan jumlah digit, misalnya "8 dari 10 digit" |
| Form (JFrame di Navigator) | Window | windowClosing | Minta konfirmasi sebelum aplikasi ditutup |

## Properti yang diubah

- `defaultCloseOperation` form diubah menjadi `DO_NOTHING`.
- Centang `enabled` pada tombol Daftar dihilangkan (tombol aktif setelah kotak setuju dicentang).
