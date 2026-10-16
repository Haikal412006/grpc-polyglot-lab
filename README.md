# Praktikum gRPC Polyglot

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
│   └── pb/
├── python-client/
│   ├── client.py
│   ├── requirements.txt
│   └── venv/
└── node-client/
    ├── client.js
    └── package.json
```

## Cara Menjalankan

### 1. Menjalankan Go Server

Buka terminal pertama, lalu jalankan:

```powershell
cd go-server
go run .
```

Server berjalan pada port `50051`.

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

**Catatan:** Go Server harus tetap berjalan saat kedua client dijalankan.

## Hasil Pengujian

Python Client dan Node.js Client berhasil mengirim request ke Go Server dan menerima respons berikut:

```text
Nama: Haikal
Email: haikal@pnl.ac.id
Phone: 081234567890
```

Go Server juga berhasil mencatat request untuk User ID `1`.

## Analisis

Go dan Python menggunakan metode *static code generation*, yaitu kode dibuat terlebih dahulu berdasarkan file `user.proto`.

Node.js menggunakan metode *dynamic runtime loading*, yaitu membaca file `user.proto` saat aplikasi dijalankan.

## Kesimpulan

Praktikum gRPC Polyglot berhasil dilakukan. Go Server dapat menerima request dari Python Client dan Node.js Client. Kedua client berhasil menerima data pengguna berupa nama, email, dan nomor telepon melalui komunikasi gRPC.

## Analisis 

Pada proyek gRPC Polyglot ini, Go dan Python menggunakan pendekatan static code generation. Skema data yang didefinisikan dalam file user.proto dikompilasi terlebih dahulu untuk menghasilkan kode pendukung gRPC yang digunakan oleh server Go dan client Python. Ketika terdapat perubahan pada skema, seperti penambahan field phone, kode hasil generasi perlu dibuat ulang agar aplikasi dapat menggunakan field baru tersebut. Sementara itu, Node.js menggunakan pendekatan dynamic runtime loading melalui library @grpc/proto-loader, sehingga skema user.proto dibaca saat aplikasi dijalankan dan tidak memerlukan proses generasi kode statis yang sama seperti Go dan Python. Kedua pendekatan memungkinkan aplikasi berbeda bahasa berkomunikasi menggunakan kontrak data yang sama, tetapi memiliki alur pemrosesan skema yang berbeda.