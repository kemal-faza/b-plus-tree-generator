# Panduan Penggunaan Tool B+ Tree

Dokumen ini menjelaskan cara memakai tool demo B+ Tree yang ada di proyek ini.

## 1. Tujuan Tool

Tool ini dipakai untuk:

- Membuat dan memanipulasi struktur B+ Tree.
- Menguji operasi insert, delete, seek, skip, dan navigasi key.
- Menampilkan visual struktur tree.
- Menyimpan dan memuat data tree melalui file JSON.

## 2. Struktur File

- btree.html: Antarmuka dan kontrol aksi.
- btree.js: Engine algoritma B+ Tree.
- btree-show.js: Render visual tree ke canvas.

## 3. Cara Menjalankan

1. Buka file btree.html di browser.
2. Pada bagian Action, pilih operasi dari dropdown.
3. Isi nilai pada input Number jika dibutuhkan.
4. Klik tombol Go.

## 4. Alur Cepat Pemakaian

Contoh alur dasar:

1. Pilih Build new tree, isi Order minimal 3, lalu Go.
2. Pilih Insert beberapa kali untuk menambah key.
3. Gunakan Seek atau Seek near untuk mencari key.
4. Gunakan Save tree to file untuk menyimpan data.
5. Gunakan Load tree from file untuk memuat ulang data.

## 5. Daftar Aksi dan Fungsinya

| Aksi                  | Fungsi                                                                    |
| --------------------- | ------------------------------------------------------------------------- |
| Build new tree        | Membuat tree baru dengan Order tertentu                                   |
| Insert                | Menambahkan key baru                                                      |
| Delete                | Menghapus key tertentu (atau key aktif jika kosong/0 sesuai implementasi) |
| Seek                  | Mencari key persis                                                        |
| Seek near             | Mencari key terdekat yang lebih besar atau sama                           |
| Skip                  | Pindah posisi key aktif maju/mundur                                       |
| Go to                 | Pindah ke key ke-n                                                        |
| Go top                | Pindah ke key paling kecil                                                |
| Go bottom             | Pindah ke key paling besar                                                |
| Pack                  | Menata ulang node agar lebih padat                                        |
| Hide From box         | Menyembunyikan panel From                                                 |
| Show From box         | Menampilkan panel From                                                    |
| Show history          | Menampilkan histori perintah                                              |
| Save tree to file     | Menyimpan tree (overwrite file sumber jika memungkinkan)                  |
| Save tree as new file | Selalu membuat file baru                                                  |
| Load tree from file   | Memuat tree dari file JSON                                                |
| Run script            | Menjalankan script contoh hardcoded                                       |
| Init random pool      | Menyiapkan pool angka acak                                                |
| Add random keys       | Memasukkan key acak dari pool                                             |
| Random key timer      | Benchmark insert dan seek untuk data acak                                 |

## 6. Format Data Simpan

File JSON yang disimpan memiliki bentuk umum:

- order: Orde tree.
- pairs: Daftar pasangan key dan recnum.

Contoh bentuk data:

{
"order": 5,
"pairs": [
{ "key": 10, "recnum": 10 },
{ "key": 20, "recnum": 20 }
]
}

## 7. Perilaku Save, Save As, dan Load

### Save tree to file

- Jika tree berasal dari file yang dibuka dengan akses writable browser modern, data akan ditimpa ke file yang sama.
- Jika tree berasal dari sumber non-writable, tool akan membuat file baru.
- Jika tree belum pernah di-load dari file, tool membuat file baru.

### Save tree as new file

- Selalu membuat file baru dari kondisi tree saat ini.

### Load tree from file

- Saat ada tree aktif, sistem akan meminta konfirmasi sebelum replace.
- Jika file valid, tree dibangun ulang dari isi file.
- Jika format file tidak valid, akan tampil pesan error.

## 8. Catatan Browser

- Pada browser yang mendukung File System Access API, load dapat memakai picker modern sehingga Save bisa overwrite file sumber.
- Pada browser tanpa dukungan API tersebut, load memakai input file biasa dan Save biasanya fallback ke file baru.

## 9. Troubleshooting

### Error: you have to build the tree first

Solusi: Jalankan Build new tree dulu sebelum aksi yang butuh tree aktif.

### Error: invalid number given

Solusi: Isi angka lebih besar dari 0 untuk aksi yang membutuhkan input jumlah.

### Key tidak ditemukan saat seek

Solusi: Pastikan key sudah diinsert dan tidak terhapus.

### Load gagal

Solusi: Pastikan file JSON memiliki order (>=3) dan pairs berbentuk array.

## 10. Tips Pengujian

- Gunakan Order kecil (misalnya 3 atau 4) untuk cepat memicu split node.
- Uji kombinasi Insert dan Delete berulang untuk melihat rebalance.
- Pakai Show history untuk merekam langkah uji.
- Simpan snapshot berkala dengan Save As agar mudah rollback skenario.
