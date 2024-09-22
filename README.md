# management-API
A example create API konfiguration
=======
#Management API
Management API ini dibangun dengan Node.js, Express.js, dan MariaDB/MySQL. API ini mendukung operasi CRUD (Create, Read, Update, Delete) untuk mengelola data pengguna. Aplikasi ini juga dapat dijalankan menggunakan Docker untuk memudahkan proses deployment.

#Fitur Utama
- GET /api/products  : Mendapatkan daftar produk
- POST /api/products : Menambahkan produk baru
- GET /api/products : Mendapatkan detail produk (berdasarkan ID)
- PUT /api/products : Memperbarui produk (berdasarkan ID)
- DELETE /api/products : Menghapus produk (berdasarkan ID)

#Prasyarat Sistem
Sebelum menjalankan aplikasi ini, pastikan Anda telah menginstal perangkat berikut:

Node.js: Versi 14 atau lebih tinggi
MariaDB/MySQL: Database untuk menyimpan data produk
Docker: (Opsional) Untuk menjalankan aplikasi dan database dalam container

#Instalasi dan Menjalankan Aplikasi

1. Clone Repository
Clone repository ini ke komputer/laptop Anda.

2. Konfigurasi Variabel Lingkungan
Buat file .env di direktori proyek (misal: api_db) anda untuk menyimpan konfigurasi basis data dan pengaturan server:

DB_HOST=localhost
DB_USER=root
DB_PASS=
DB_NAME=api_db
PORT=3000

*Keterangan
- DB_HOST: Host database (gunakan localhost jika dijalankan secara lokal, atau db jika menggunakan Docker).
- DB_USER: Nama pengguna untuk basis data (misalnya, root).
- DB_PASS: Kata sandi untuk pengguna basis data (disini tidak menggunakan katasandi).
- DB_NAME: Nama database yang digunakan (misalnya, api_db).
- PORT: Port yang digunakan oleh server Node.js (default 3000).

3. Menjalankan Aplikasi Tanpa Docker (Opsional)
3.1. Install Dependencies
Jalankan perintah ini untuk menginstall dependencies yang diperlukan:
 --> npm install
 
3.2. Buat Database di MariaDB/MySQL
Sebelum menjalankan aplikasi, buat database di MariaDB atau MySQL. Gunakan perintah berikut:
 --> CREATE DATABASE IF NOT EXISTS api_db;
		USE api_db;
		CREATE TABLE IF NOT EXISTS product (
		id INT AUTO_INCREMENT PRIMARY KEY,
		name VARCHAR(50) NOT NULL,
		price int NOT NULL,
		stock int NOT NULL,
		sold int NOT NULL,
		created_at VARCHAR(50) NOT NULL,
		updated_at VARCHAR(50) NOT NULL
	);

4. Menjalankan Aplikasi dengan Docker (Disarankan)
4.1. Setup Docker
Jika Anda lebih memilih menjalankan aplikasi menggunakan Docker, langkah-langkah berikut akan memandu Anda.

4.2. Jalankan Docker Compose
Pastikan Docker dan Docker Compose sudah terinstall. Untuk menjalankan aplikasi dan database, jalankan perintah berikut:
 --> docker-compose up

*Keterangan
Ini akan memulai dua container:
1. db: Container MariaDB dengan database api_db.
2. app: Container Node.js yang menjalankan aplikasi pada port 3000.

5. Menjalankan Aplikasi dengan Node.js langsung Gunakan perintah berikut pada cmd:
 --> node app.js

6. Pengujian Endpoint API
Aplikasi memiliki beberapa endpoint yang dapat Anda akses. Berikut adalah detail endpoint API dan contoh penggunaannya.

Disini Menggunakan Postman;

Detail Endpoint API
1. GET 
	http://localhost:3000/api/products
Mendapatkan daftar semua product.

Response (200 OK):
{
  "message": "Product List",
  "data": [
	  {
            "id": 1,
            "name": "Laptop X",
            "price": 12000000,
            "stock": 15,
            "sold": 0,
            "created_at": "2024-09-19T06:29:31.000000Z",
            "updated_at": "2024-09-19T06:29:31.000000Z"
       }
       ]
}    

2. POST 
	http://localhost:3000/api/products
Menambahkan product baru.
pilih tab body-raw-JSON

	{
    "name": "Smartphone Y",
    "price": 7000000,
    "stock": 30,
    "sold": 0,
    "created_at": "2024-09-19T06:29:31.000000Z",
    "updated_at": "2024-09-19T06:29:31.000000Z"
  }
	
Response (201 Created):
	{
  "message": "Product created successfully",
  "data": {
    "id": 1,
    "name": "Smartphone Y",
    "price": 7000000,
    "stock": 30,
    "sold": 0,
    "created_at": "2024-09-19T06:29:31.000000Z",
    "updated_at": "2024-09-19T06:29:31.000000Z"
  }
}

3. GET
http://localhost:3000/api/products/1 (angka 1 merupakan ID product)
Mendapatkan detail pengguna berdasarkan ID.


Response (200 OK):
	{
    "message": "Product Detail",
    "data": {
        "id": 1,
        "name": "Laptop X",
        "price": 12000000,
        "stock": 15,
        "sold": 0,
        "created_at": "2024-09-19T06:29:31.000000Z",
        "updated_at": "2024-09-19T06:29:31.000000Z"
    }
}

4. PUT
http://localhost:3000/api/products/1
Memperbarui pengguna berdasarkan ID.

	-Body:
{
    "name": "Laptop X",
    "price": 20000000,
    "stock": 50,
    "sold": 0,
    "created_at": "2024-09-19T06:29:31.000000Z",
    "updated_at": "2024-09-19T06:29:31.000000Z"
  
}
Response (200 OK):
	{
  "message": "Product updated successfully",
  "data": {
    "id": 1,
    "name": "Laptop X",
    "price": 20000000,
    "stock": 50,
    "sold": 0,
    "created_at": "2024-09-19T06:29:31.000000Z",
    "updated_at": "2024-09-19T08:48:44.000000Z"
  }
}

5. DELETE
http://localhost:3000/api/products/1
Menghapus pengguna berdasarkan ID.

Request:
	-Method: DELETE
	-Response (204 No Content):
	{}

