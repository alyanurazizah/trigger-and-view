💳 Sistem Database Perbankan (MySQL / MariaDB) 📌 Deskripsi

Project ini merupakan simulasi sederhana sistem perbankan menggunakan MySQL/MariaDB. Database ini dirancang untuk mengelola data nasabah, rekening, jenis rekening, serta transaksi keuangan seperti setor dan tarik tunai.

Selain itu, sistem ini juga dilengkapi dengan VIEW dan TRIGGER untuk otomatisasi proses bisnis seperti validasi, update saldo, dan pencatatan log.

🗂️ Struktur Database

Tabel jenis_rekening
Menyimpan informasi jenis rekening.

Field Tipe Keterangan id_jenis INT Primary Key nama_jenis VARCHAR Nama jenis (Reguler / Gold) biaya_tarik_tunai DECIMAL Biaya admin tarik saldo_minimum DECIMAL Batas saldo minimum kelipatan_poin INT Poin reward 2. Tabel nasabah

Menyimpan data nasabah.

Field Tipe Keterangan id_nasabah INT Primary Key nama VARCHAR Nama nasabah status VARCHAR AKTIF / BLACKLIST poin INT Poin loyalitas 3. Tabel rekening

Menyimpan data rekening nasabah.

Field Tipe Keterangan no_rekening VARCHAR Primary Key id_nasabah INT Foreign Key id_jenis INT Foreign Key saldo DECIMAL Saldo rekening pin VARCHAR PIN rekening 4. Tabel transaksi

Menyimpan data transaksi.

Field Tipe Keterangan id_trx INT Primary Key no_rekening VARCHAR Foreign Key jenis_trx VARCHAR SETOR / TARIK jumlah DECIMAL Nominal transaksi tanggal DATETIME Waktu transaksi 5. Tabel log_audit

Menyimpan riwayat aktivitas transaksi.

Field Tipe Keterangan id_log INT Primary Key waktu DATETIME Waktu no_rek VARCHAR No rekening nama_nasabah VARCHAR Nama aksi VARCHAR Jenis aksi nominal DECIMAL Nominal 👁️ VIEW 🔹 vw_info_nasabah_cs

Menampilkan informasi rekening dan nasabah.

Isi:

No rekening Nama nasabah Jenis rekening Saldo 🔹 vw_mutasi_rekening

Menampilkan riwayat transaksi rekening.

Isi:

Tanggal Nama nasabah Jenis transaksi Nominal Jenis rekening ⚙️ TRIGGER

Database ini menggunakan 6 trigger utama:

🔸 1. BEFORE INSERT Validasi nasabah (tidak boleh BLACKLIST) Validasi saldo minimum saat tarik tunai 🔸 2. AFTER INSERT Update saldo otomatis Tambah poin loyalitas Simpan log audit 🔸 3. BEFORE UPDATE Mencegah perubahan jumlah transaksi 🔸 4. AFTER UPDATE Mencatat log perubahan 🔸 5. BEFORE DELETE Mengembalikan saldo (void transaksi) 🔸 6. AFTER DELETE Mencatat log penghapusan 🔄 Alur Sistem User melakukan transaksi (INSERT ke tabel transaksi) Trigger BEFORE INSERT melakukan validasi Jika valid: Data masuk ke tabel transaksi Trigger AFTER INSERT: Update saldo Tambah poin Catat log 🧪 Contoh Pengujian ✅ Setor uang INSERT INTO transaksi (no_rekening, jenis_trx, jumlah) VALUES ('001', 'SETOR', 500000); ❌ Tarik saldo tidak cukup INSERT INTO transaksi (no_rekening, jenis_trx, jumlah) VALUES ('001', 'TARIK', 100000000); ❌ Nasabah blacklist INSERT INTO transaksi (no_rekening, jenis_trx, jumlah) VALUES ('003', 'SETOR', 100000); 🚀 Teknologi MySQL / MariaDB XAMPP (phpMyAdmin) SQL (DDL, DML, VIEW, TRIGGER) 📌 Kesimpulan

Database ini mensimulasikan sistem perbankan dengan fitur:

Relasi antar tabel (JOIN) View untuk mempermudah query Trigger untuk otomatisasi logika bisnis

Sehingga sistem menjadi lebih aman, otomatis, dan terstruktur.
