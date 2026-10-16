# Praktikum gRPC Polyglot
<div align="justify">
Proyek ini merupakan praktikum komunikasi antarbahasa pemrograman menggunakan gRPC. Go digunakan sebagai server, sedangkan Python dan Node.js digunakan sebagai client.

## Teknologi yang Digunakan

- Go sebagai gRPC Server
- Python sebagai Client
- Node.js sebagai Client
- Protocol Buffers sebagai kontrak komunikasi
- gRPC sebagai penghubung server dan client

## Struktur Proyek

```text
grpc-polyglot-lab/
├── user.proto
├── README.md
├── .gitignore
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

## Cara Menjalankan

### 1. Menjalankan Go Server

Buka terminal pertama dari folder utama proyek, lalu jalankan:

```powershell
cd go-server
go run .
```

Server berjalan pada port `50051`. Biarkan terminal ini tetap terbuka.

### 2. Menjalankan Python Client

Buka terminal kedua dari folder utama proyek, lalu jalankan:

```powershell
cd python-client
python client.py
```

### 3. Menjalankan Node.js Client

Buka terminal ketiga dari folder utama proyek, lalu jalankan:

```powershell
cd node-client
node client.js
```

**Catatan:** Go Server harus tetap berjalan ketika Python Client dan Node.js Client dijalankan.

## Hasil Pengujian

Python Client dan Node.js Client berhasil mengirim request ke Go Server dan menerima respons data pengguna berikut:

```text
Nama: Haikal
Email: haikal@pnl.ac.id
Phone: 081234567890
```

Go Server juga berhasil mencatat request untuk User ID `1`.

## Analisis Static Code Generation dan Dynamic Runtime Loading

Pada proyek gRPC Polyglot ini, Go dan Python menggunakan pendekatan *static code generation*. Skema data yang didefinisikan dalam file `user.proto` dikompilasi terlebih dahulu untuk menghasilkan kode pendukung gRPC yang digunakan oleh server Go dan client Python. Ketika terdapat perubahan pada skema, seperti penambahan field `phone`, kode hasil generasi perlu dibuat ulang agar aplikasi dapat menggunakan field baru tersebut.

Sementara itu, Node.js menggunakan pendekatan *dynamic runtime loading* melalui library `@grpc/proto-loader`. Skema `user.proto` dibaca saat aplikasi dijalankan sehingga tidak memerlukan proses generasi kode statis yang sama seperti Go dan Python. Kedua pendekatan memungkinkan aplikasi dengan bahasa pemrograman berbeda berkomunikasi menggunakan kontrak data yang sama, tetapi memiliki alur pemrosesan skema yang berbeda.

## Kesimpulan

Praktikum gRPC Polyglot berhasil dilakukan. Go Server dapat menerima request dari Python Client dan Node.js Client. Kedua client berhasil menerima data pengguna berupa nama, email, dan nomor telepon melalui komunikasi gRPC.
</div>
