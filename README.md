# Praktikum gRPC Polyglot

<div align="justify">

Proyek ini merupakan implementasi praktikum komunikasi antarbahasa pemrograman menggunakan **gRPC (Google Remote Procedure Call)**. Proyek menggunakan Go sebagai server, sedangkan Python dan Node.js digunakan sebagai client. Komunikasi antara server dan client menggunakan Protocol Buffers sebagai kontrak pertukaran data.

Praktikum ini juga membahas perbedaan pendekatan *static code generation* dan *dynamic runtime loading* dalam implementasi gRPC pada beberapa bahasa pemrograman.

</div>

## Teknologi yang Digunakan

| Teknologi | Fungsi |
|---|---|
| Go | Menjalankan gRPC Server |
| Python | Mengimplementasikan Client Python |
| Node.js | Mengimplementasikan Client JavaScript |
| gRPC | Menghubungkan server dan client |
| Protocol Buffers | Mendefinisikan struktur pesan dan layanan |
| Git & GitHub | Mengelola versi dan menyimpan kode proyek |

## Struktur Proyek

```text
grpc-polyglot-lab/
├── .gitignore
├── README.md
├── user.proto
├── go-server/
│   ├── main.go
│   ├── go.mod
│   ├── go.sum
│   └── pb/
│       ├── user.pb.go
│       └── user_grpc.pb.go
├── python-client/
│   ├── client.py
│   ├── requirements.txt
│   ├── user_pb2.py
│   └── user_pb2_grpc.py
└── node-client/
    ├── client.js
    ├── package.json
    └── package-lock.json
```

## Implementasi

### 1. Go Server

Go Server bertugas menerima request dari client, memproses permintaan, dan mengirimkan respons data pengguna. Server berjalan pada port `50051`.

### 2. Python Client

Python Client menggunakan kode gRPC hasil generasi dari `user.proto` untuk berkomunikasi dengan server Go. Client mengirimkan request dan menampilkan data pengguna yang diterima.

### 3. Node.js Client

Node.js Client menggunakan library `@grpc/grpc-js` dan `@grpc/proto-loader`. Definisi protokol dimuat saat program berjalan sehingga client dapat berkomunikasi dengan server tanpa menggunakan kode pesan hasil generasi statis yang sama seperti Python.

## Cara Menjalankan Proyek

**Persyaratan:** Go, Python, Node.js, serta seluruh dependensi proyek harus sudah terpasang.

### 1. Menjalankan Go Server

Buka terminal pertama dari folder utama proyek, kemudian jalankan:

```powershell
cd go-server
go run .
```

Jika berhasil, server akan berjalan pada port `50051`. Biarkan terminal ini tetap terbuka selama pengujian client.

### 2. Menjalankan Python Client

Buka terminal kedua dari folder utama proyek, kemudian jalankan:

```powershell
cd python-client
python client.py
```

Pastikan dependensi Python sudah dipasang dan kode hasil generasi gRPC tersedia.

### 3. Menjalankan Node.js Client

Buka terminal ketiga dari folder utama proyek, kemudian jalankan:

```powershell
cd node-client
node client.js
```

Pastikan dependensi Node.js sudah tersedia melalui `npm install`.

**Catatan:** Go Server harus tetap berjalan ketika kedua client dijalankan. Setiap terminal client harus dimulai dari folder utama proyek sebelum menjalankan perintah `cd` di atas.

## Hasil Pengujian

Pengujian dilakukan dengan menjalankan Go Server, kemudian mengirimkan request menggunakan Python Client dan Node.js Client.

Kedua client berhasil menerima respons data pengguna dengan hasil berikut:

```text
Respon dari Server -> Nama: Haikal, Email: haikal@pnl.ac.id, Phone: 081234567890
```

Hasil tersebut menunjukkan bahwa server berhasil mengirimkan data nama, email, dan nomor telepon kepada client melalui komunikasi gRPC.

Hasil Go Server

Go Server berhasil dijalankan pada port 50051. Setelah client melakukan request, server mencatat permintaan untuk User ID 1.

## Analisis Static Code Generation dan Dynamic Runtime Loading

<div align="justify">

**Static Code Generation**

Go dan Python menggunakan pendekatan *static code generation*. Definisi pesan dan layanan yang ditulis dalam `user.proto` dikompilasi terlebih dahulu untuk menghasilkan kode pendukung gRPC. Go menggunakan berkas hasil generasi seperti `user.pb.go` dan `user_grpc.pb.go`, sedangkan Python menggunakan `user_pb2.py` dan `user_pb2_grpc.py`. Ketika skema protokol berubah, misalnya dengan menambahkan field `phone`, kode hasil generasi yang terkait perlu dibuat ulang.

**Dynamic Runtime Loading**

Node.js menggunakan pendekatan *dynamic runtime loading* melalui library `@grpc/proto-loader`. Definisi `user.proto` dibaca ketika aplikasi dijalankan, sehingga client dapat menggunakan skema protokol tanpa proses generasi kode pesan statis yang sama seperti pada Go dan Python.

Kedua pendekatan memungkinkan aplikasi yang menggunakan bahasa pemrograman berbeda berkomunikasi melalui kontrak data yang sama. Perbedaannya terletak pada waktu pemrosesan definisi protokol dan cara kode pendukung digunakan oleh aplikasi.

</div>

## Kesimpulan

<div align="justify">

Praktikum gRPC Polyglot berhasil mengimplementasikan komunikasi antara Go Server dengan Python Client dan Node.js Client. Kedua client berhasil menerima respons data pengguna berupa nama, email, dan nomor telepon melalui gRPC.

Praktikum ini juga menunjukkan perbedaan antara *static code generation* yang digunakan oleh Go dan Python serta *dynamic runtime loading* yang digunakan oleh Node.js. Dengan menggunakan Protocol Buffers sebagai kontrak komunikasi, ketiga komponen dapat bertukar data secara konsisten meskipun dikembangkan menggunakan bahasa pemrograman yang berbeda.

</div>
