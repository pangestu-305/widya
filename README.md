# Toko Skincare Cantik Berseri

Aplikasi web sederhana untuk toko skincare, dibuat dengan PHP, MySQL, CSS (Bootstrap), dan JavaScript.

Panduan ini akan membantu Anda membangun aplikasi dari awal hingga dapat menampilkan produk dari database dan menerima pesan dari form kontak.

---

## Prasyarat

- **XAMPP** (sudah terinstal di komputer Anda)
- **Editor kode** (VSCode, Sublime, dsb)
- **Browser** (Chrome, Firefox, dsb)

---

## 1. Menyiapkan XAMPP

1. Jalankan **XAMPP Control Panel**.
2. Aktifkan **Apache** dan **MySQL** (klik tombol Start).
3. Buka **phpMyAdmin** di browser:  
   `http://localhost/phpmyadmin`

---

## 2. Import Database & Struktur Tabel

### a. Import Database

1. Buka **phpMyAdmin**.
2. Klik **New** lalu buat database dengan nama: `db_skincare`.
3. Pilih database `db_skincare` yang baru dibuat.
4. Klik tab **Import**.
5. Pilih file `db_skincare.sql` yang sudah disediakan, lalu klik **Go**.

### b. Struktur Tabel Utama

- **produk** (`id_produk`, `nama_produk`, `jenis_produk`, `harga`, `stok`)
- **pelanggan** (`id_pelanggan`, `nama`, `email`, `no_hp`, `alamat`)
- **transaksi** (`id_transaksi`, `id_pelanggan`, `tanggal`, `total_harga`)
- **detail_transaksi** (`id_detail`, `id_transaksi`, `id_produk`, `jumlah`, `subtotal`)

---

## 3. Struktur Folder

Letakkan semua file di dalam folder, misal:  
`C:/xampp/htdocs/toko skincare`

Struktur:
```
toko skincare/
│
├── index.html
├── produk.php
├── kontak.php
├── db.php
├── css/
│   └── style.css
├── js/
│   └── script.js
├── gambar/
│   └── (gambar produk)
├── db_skincare.sql
```

---

## 4. Koneksi ke Database (db.php)

Buat file `db.php`:
```php
<?php
$host = "localhost";
$user = "root";
$pass = "";
$db   = "db_skincare"; // Pastikan sesuai dengan nama database hasil import

$conn = new mysqli($host, $user, $pass, $db);
if ($conn->connect_error) {
    die("Koneksi gagal: " . $conn->connect_error);
}
?>
```

---

## 5. Menampilkan Produk dari Database (produk.php)

Karena struktur tabel produk adalah:
- `id_produk`
- `nama_produk`
- `jenis_produk`
- `harga`
- `stok`

Contoh kode untuk menampilkan produk:

```php
<?php
include 'db.php';
$result = $conn->query("SELECT * FROM produk");
while($row = $result->fetch_assoc()) {
?>
    <div class="col">
        <div class="card h-100 shadow-sm">
            <!-- Gambar bisa disesuaikan jika ada kolom gambar, jika tidak bisa pakai gambar default -->
            <img src="gambar/default.jpg" class="card-img-top" alt="<?php echo $row['nama_produk']; ?>">
            <div class="card-body">
                <h5 class="card-title"><?php echo $row['nama_produk']; ?></h5>
                <p class="card-text">Jenis: <?php echo $row['jenis_produk']; ?></p>
                <p class="card-text">Stok: <?php echo $row['stok']; ?></p>
                <p class="card-text fw-bold">Rp <?php echo number_format($row['harga'],0,',','.'); ?></p>
                <a href="#" class="btn btn-success">Tambah ke Keranjang</a>
            </div>
        </div>
    </div>
<?php } ?>
```
**Catatan:**  
- Jika ingin menambah kolom gambar, tambahkan kolom `gambar` pada tabel produk.
- Panggil file ini di bagian produk pada `index.html` menggunakan PHP:  
  ```php
  <div class="row row-cols-1 row-cols-md-3 g-4">
      <?php include 'produk.php'; ?>
  </div>
  ```

---

## 6. Menyimpan Pesan dari Form Kontak (opsional)

Jika ingin menyimpan pesan dari form kontak, Anda bisa membuat tabel baru misal `pesan` dan menyesuaikan script PHP-nya.

---

## 7. Menambahkan Produk

- Masukkan data produk lewat phpMyAdmin, atau buat halaman admin sederhana untuk menambah produk.

---

## 8. Menambahkan Gambar Produk

- Simpan gambar produk di folder `gambar/`.
- Pastikan nama file gambar sesuai dengan yang diinput di kolom `gambar` pada tabel `produk` (jika ada kolom gambar).
- Jika tidak ada kolom gambar, gunakan gambar default.

---

## 9. Menjalankan Aplikasi

1. Buka browser.
2. Akses:  
   `http://localhost/toko%20skincare/index.html`  
   (atau `index.php` jika sudah mengubah file utama menjadi PHP)

---

## 10. Kustomisasi

- Edit file CSS di `css/style.css` untuk mempercantik tampilan.
- Tambahkan fitur keranjang, transaksi, pelanggan, dsb sesuai kebutuhan dan tabel yang sudah ada.

---

## 11. Tips Keamanan

- Selalu gunakan prepared statement untuk query database.
- Validasi dan sanitasi semua input dari user.
- Jangan upload aplikasi ke server publik tanpa pengamanan tambahan.

---

## 12. Referensi

- [Bootstrap Docs](https://getbootstrap.com/)
- [PHP MySQLi Docs](https://www.php.net/manual/en/book.mysqli.php)
- [XAMPP Docs](https://www.apachefriends.org/)

---

**Selesai!**  
Jika butuh contoh kode lebih detail untuk bagian tertentu, silakan tanyakan! 