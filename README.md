📌 Dokumentasi API Catatan Keuangan
API ini memungkinkan pengguna untuk mengelola transaksi keuangan mereka, termasuk mendaftarkan akun, login, CRUD transaksi, dan melihat ringkasan keuangan.

📍 Base URL
arduino
Copy
Edit
http://localhost:8080
1️⃣ Autentikasi
🔹 Register User
Endpoint:
POST /register
Deskripsi:
Mendaftarkan user baru.

📥 Request Body (JSON):

json
Copy
Edit
{
  "name": "John Doe",
  "email": "johndoe@example.com",
  "password": "password123"
}
📤 Response (JSON):

json
Copy
Edit
{
  "message": "User registered successfully",
  "user_id": 1
}
🔹 Login User
Endpoint:
POST /login
Deskripsi:
Login user dan mendapatkan token JWT.

📥 Request Body (JSON):

json
Copy
Edit
{
  "email": "johndoe@example.com",
  "password": "password123"
}
📤 Response (JSON):

json
Copy
Edit
{
  "message": "Login successful",
  "token": "eyJhbGciOiJIUzI1..."
}
2️⃣ Manajemen Transaksi
🔹 Get Semua Transaksi
Endpoint:
GET /transaction
Deskripsi:
Mengambil semua transaksi user yang sedang login. (Butuh token JWT)

🔑 Header Authorization:

makefile
Copy
Edit
Authorization: Bearer <token_jwt>
📤 Response (JSON):

json
Copy
Edit
[
  {
    "id": 1,
    "title": "Gaji Bulanan",
    "description": "Gaji dari perusahaan",
    "amount": 5000000,
    "type": "income",
    "created_at": "2025-02-16T12:00:00Z"
  },
  {
    "id": 2,
    "title": "Belanja Bulanan",
    "description": "Beli kebutuhan rumah",
    "amount": 1500000,
    "type": "expense",
    "created_at": "2025-02-17T14:30:00Z"
  }
]
🔹 Tambah Transaksi
Endpoint:
POST /transaction
Deskripsi:
Menambahkan transaksi baru (income atau expense).

📥 Request Body (JSON):

json
Copy
Edit
{
  "title": "Beli Laptop",
  "description": "Laptop untuk kerja",
  "amount": 10000000,
  "type": "expense"
}
📤 Response (JSON):

json
Copy
Edit
{
  "message": "Transaction added successfully",
  "transaction_id": 3
}
🔹 Get Transaksi by ID
Endpoint:
GET /transaction/:id
Deskripsi:
Mengambil detail transaksi berdasarkan ID.

📤 Response (JSON):

json
Copy
Edit
{
  "id": 3,
  "title": "Beli Laptop",
  "description": "Laptop untuk kerja",
  "amount": 10000000,
  "type": "expense",
  "created_at": "2025-02-18T10:00:00Z"
}
🔹 Update Transaksi
Endpoint:
PUT /transaction/:id
Deskripsi:
Mengupdate transaksi tertentu. Semua field bersifat opsional, hanya kirim field yang ingin diubah.

📥 Request Body (JSON) (Contoh ubah title & amount):

json
Copy
Edit
{
  "title": "Beli Laptop Gaming",
  "amount": 12000000
}
📤 Response (JSON):

json
Copy
Edit
{
  "message": "Transaction updated successfully"
}
🔹 Hapus Transaksi
Endpoint:
DELETE /transaction/:id
Deskripsi:
Menghapus transaksi berdasarkan ID.

📤 Response (JSON):

json
Copy
Edit
{
  "message": "Transaction deleted successfully"
}
3️⃣ Laporan Keuangan
🔹 Get Summary (Total Income, Expense, dan Balance)
Endpoint:
GET /report/summary
Deskripsi:
Mengambil total pemasukan, total pengeluaran, dan saldo akhir dari transaksi user.

📤 Response (JSON):

json
Copy
Edit
{
  "total_income": 7500000,
  "total_expense": 2000000,
  "balance": 5500000
}
