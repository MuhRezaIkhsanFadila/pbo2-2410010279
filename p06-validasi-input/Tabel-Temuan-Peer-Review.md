# Tabel Temuan Peer Review dan Perbaikan — P06 (2410010279)

Sumber: `Lembar-Peer-Review-Heuristik.pdf` — peninjau Daffa Surya Atmaja, 31 Oktober 2026.

Semua temuan berskor 0–2. Menurut modul, hanya temuan skor 3 dan 4 yang wajib diperbaiki,
jadi tidak ada perbaikan yang wajib dikomit.

| No | Heuristik | Temuan | Skor | Saran | Perbaikan | Commit |
|---|---|---|---|---|---|---|
| 1 | Visibilitas status sistem | Ada penghitung digit dan status jumlah kesalahan. Jelas. | 0 | - | Tidak ada | - |
| 2 | Kesesuaian dengan dunia nyata | Istilahnya jelas dan sesuai form pendaftaran. | 0 | - | Tidak ada | - |
| 3 | Kendali dan kebebasan pengguna | Batal sudah pakai konfirmasi, tapi belum bisa undo. | 1 | Tambah undo. | Tidak wajib diperbaiki (skor ≤ 2) | - |
| 4 | Konsistensi dan standar | Gaya error konsisten. Cuma tombol Daftar mati sampai centang setuju, kurang jelas kenapa. | 1 | Kasih keterangan. | Tidak wajib diperbaiki (skor ≤ 2) | - |
| 5 | Pencegahan kesalahan | Huruf ditolak saat ngetik, tapi paste tetap bisa masuk. | 2 | Batasi juga saat paste. | Tidak wajib diperbaiki (skor ≤ 2) | - |
| 6 | Mengenali, bukan mengingat | Aturan cuma di tooltip, harus hover. Wajib/opsional nggak ditandai. | 2 | Taruh aturan di bawah label, kasih tanda *. | Tidak wajib diperbaiki (skor ≤ 2) | - |
| 7 | Fleksibilitas dan efisiensi | Enter langsung Daftar, mnemonic jalan, Tab rapi. | 1 | - | Tidak ada | - |
| 8 | Desain estetis dan minimalis | Rapi, tapi baris pesan kosong bikin form keliatan longgar. | 1 | Rapatkan. | Tidak wajib diperbaiki (skor ≤ 2) | - |
| 9 | Membantu memperbaiki kesalahan | Pesan error jelas, fokus lompat ke yang salah. Status cuma bilang jumlah. | 1 | Sebut isiannya. | Tidak wajib diperbaiki (skor ≤ 2) | - |
| 10 | Bantuan dan dokumentasi | Cuma tooltip, nggak ada bantuan. | 2 | Tambah tombol Bantuan. | Tidak wajib diperbaiki (skor ≤ 2) | - |
